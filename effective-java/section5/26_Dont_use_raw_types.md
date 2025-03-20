# 26. 로 타입은 사용하지 말라

<br>

# 제네릭(Generics)이란?

자바 5(JDK 1.5) 이후 부터 사용가능 **타입을 파라미터로 가지는 클래스와 인터페이스** 이다

즉, 담을 수 있는 데이터 타입을 미리 지정하는 방법이다

### 제네릭의 작동 방식

```java
// 모든 타입의 물건을 담을 수 있는 상자 만들기
public class Box<T> {    // T는 타입 파라미터
    private T item;      // T 타입의 아이템을 담을 변수

    public void put(T item) {  // T 타입의 아이템을 넣는 메서드
        this.item = item;
    }

    public T get() {           // T 타입의 아이템을 꺼내는 메서드
        return item;
    }
}
```

### 제네릭 사용 예시

```java
// 문자열만 담는 상자
Box<String> stringBox = new Box<>();
stringBox.put("안녕하세요");     // 문자열만 넣을 수 있어요
String greeting = stringBox.get();  // 꺼낼 때 형변환이 필요 없어요!

// 숫자만 담는 상자
Box<Integer> numberBox = new Box<>();
numberBox.put(100);           // 숫자만 넣을 수 있어요
Integer number = numberBox.get();  // 꺼낼 때 형변환이 필요 없어요!
```

## 제네릭의 중요한 특징

1. 타입 안정성(Type Safety)

   잘못된 타입의 물건이 들어가지 않도록 컴파일러가 확인해준다

2. 형변환이 필요 없음 (불필요한 cast 제거)

   제네릭을 사용하면 꺼낼 때 무슨 타입인지 확인하는 과정이 필요 없다

3. 다양한 타입 문자를 사용

   - `<T>`: 일반적인 타입을 나타냄 (Type의 첫 글자)

   - `<E>`: 컬렉션의 요소 타입을 나타냄 (Element의 첫 글자)

   - `<K, V>`: 키와 값을 나타냄 (Key, Value의 첫 글자)

4. 예시

   ```java
   // 아무 종류의 선물을 담을 수 있는 선물 상자 만들기
   public class GiftBox<T> {
       private T gift;  // T 타입의 선물

       // 선물을 넣는 메서드
       public void putGift(T newGift) {
           this.gift = newGift;
       }

       // 선물을 꺼내는 메서드
       public T getGift() {
           return gift;
       }
   }

   // 사용하는 방법
   GiftBox<Chocolate> chocolateBox = new GiftBox<>();  // 초콜릿만 담는 상자
   chocolateBox.putGift(new Chocolate());  // 초콜릿 넣기

   GiftBox<Toy> toyBox = new GiftBox<>();  // 장난감만 담는 상자
   toyBox.putGift(new Toy());  // 장난감 넣기
   ```

<br>

# 로 타입(Raw Type)이란?

제네릭 타입에서 타입 정보를 모두 지워버린 것 -> 어떤 타입의 객체든지 넣을 수 있다

자바 5(JDK 1.5) 이전에는 제네릭이 없었기 때문에, 모든 컬렉션은 로 타입이었다

```java
// 제네릭을 사용한 리스트
List<String> nameList = new ArrayList<>();  // 문자열만 담는 리스트
nameList.add("철수");
nameList.add("영희");
// nameList.add(123);  // 컴파일 오류! 숫자는 문자열이 아니에요

// 로 타입을 사용한 리스트
List nameListRaw = new ArrayList();  // 아무거나 담는 리스트
nameListRaw.add("철수");
nameListRaw.add("영희");
nameListRaw.add(123);  // 오류 없음! 아무거나 넣을 수 있어요
```

➔ 타입을 지정하지 않아도 사용가능한거면 오히려 더 좋지 않나? 라고 생각할 수 있음

## 로 타입의 문제점

1. 타입 안정성을 잃게 된다

   - 로 타입을 사용하면 어떤 타입의 값이 들어갈지 모른다

   - 꺼낼 때 **타입 변환 오류(ClassCastException)** 가 발생할 수 있다

   ```java
   List list = new ArrayList();
   list.add("Hello");
   list.add(42);  // ❗ 문제 발생 (숫자가 들어감)

   // 데이터 꺼내기
   for (Object obj : list) {
       String str = (String) obj;  // ❌ 숫자를 문자열로 변환할 수 없음! (오류 발생)
       System.out.println(str);
   }
   ```

2. 컴파일러가 오류를 잡아주지 못한다

   - 로 타입을 쓰면 컴파일러가 잘못된 데이터 입력을 막아주지 못한다

   - 실행 중에야 오류를 발견할 수 있다 (너무 늦음)

   ```java
   private final Collection stamps = new ArrayList();  // 로 타입 사용 ❌

   stamps.add(new Coin());  // ❌ 엉뚱한 타입이 들어가도 컴파일 오류 없음!
   stamps.add(new Stamp()); // ❌ Stamp만 넣으려 했는데...

   // 나중에 꺼낼 때 오류 발생! (ClassCastException)
   for (Object obj : stamps) {
       Stamp stamp = (Stamp) obj;
       stamp.cancel();
   }
   ```

### ✅ 제네릭을 사용하면?

```java
private final Collection<Stamp> stamps = new ArrayList<>();  // ✅ 타입 명확하게 지정!

stamps.add(new Stamp()); // ✅ Stamp만 추가 가능!
stamps.add(new Coin());  // ❌ 컴파일 오류 발생 (잘못된 타입 차단!)
```

## 로 타입 대신 사용할 수 있는 것들

1. 매개변수화 타입 - `List<Object>`

   모든 종류의 객체를 담을 수 있지만, 컴파일러에게 그 의도를 명확히 알려준다

   ```java
   // 로 타입 (안 좋은 방법)
   List badList = new ArrayList();

   // 매개변수화 타입 (좋은 방법)
   List<Object> goodList = new ArrayList<>();

   ```

2. 비한정적 와일드카드 타입 - `List<?>`

   타입 안전성을 유지하면서, 다양한 타입을 받을 수 있다

   ```java
   // 비한정적 와일드카드 타입
   List<?> someList = new ArrayList<>();

   // null만 추가할 수 있어요
   someList.add(null); // 가능

   // 다른 것은 추가할 수 없어요
   someList.add("문자열"); // 컴파일 오류! 👍
   ```

<br>

## 로 타입 대신 사용할 수 있는 것들

1. class 리터럴에는 로 타입을 써야 해!

   ```java
   Class<?> clazz = List.class;  // ✅ 올바른 사용법
   ```

   ✔️ `List<String>.class` 같은 형태는 사용할 수 없다

2. instanceof 연산자에서는 로 타입 사용!
   ```java
   if (obj instanceof Set) {  // ✅ raw 타입 사용
       Set<?> set = (Set<?>) obj;  // 와일드카드 타입으로 변환
   }
   ```
   ✔️ 하지만 로 타입을 그대로 쓰면 안 되고, `Set<?>`로 변환해야 안전하다

<br>

---

## 🧩 어려웠던 점

로 타입을 쓰면 왜 위험한지 구체적인 이유를 정리하는 과정이 필요했다

<br>

## 💡 느낀 점

제네릭을 사용하면 프로그램이 더 안전하고 명확해진다는 것을 느꼈다
