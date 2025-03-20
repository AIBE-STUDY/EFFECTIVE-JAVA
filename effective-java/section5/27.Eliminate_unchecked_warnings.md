# 27. 비검사 경고를 제거하라

> 가능한 모든 비검사 경고는 제거하라!

## 📌 1. 발표 전 알아야 할 개념

### ✅ 로타입(RawType)

- 제네릭 타입에서 타입 매개변수를 전혀 사용하지 않을 때

```java
List list = new ArrayList();
```

- 타입 안정성을 보장하기 어려움

---

## 📕 2. 비검사 경고 완전 정복

### 2-1. 비검사 경고(Unchecked Warning)

- 자바의 제네릭 시스템이 컴파일 시점에서 **타입 안전성을 완전히 검증할 수 없을 때** 컴파일러가 발생시키는 경고
  ![Image](https://github.com/user-attachments/assets/332979e5-d846-4654-8c52-be4e2a3c529c)

### 2-2. 비검사 경고의 종류

- `비검사 형변환 경고` (Unchecked Cast Warning)
  - 로 타입입을 제네릭 타입으로 형변환할 때, 컴파일러가 검증할 수 없는 형변환일 경우

```java
    List car = new ArrayList();
    List<Car> myCar = (List<Car>) car;
```

    (우리는 일반적으로 제네릭을 사용하고 있다!)

- `비검사 메서드 호출 경고` (Unchecked Method Invocation Warning)
  - 제네릭 타입이 있는 메서드에서 토 타입을 사용할 때 발생

```java
public class Car {
    String model;
    Car(String model) {
        this.model = model;
    }
}

public class UncheckedMethodWarning {
    public static void main(String[] args) {
        List cars = new ArrayList();
        addCar(cars, new Car("Tesla"));
    } // cars는 로 타입입
    public static void addCar(List<Car> carList, Car car) {
        carList.add(car);
    } // 제네릭 타입 메서드
} // 제네릭 타입이 있는 메서드에서 로 타입 사용 시
```

![Image](https://github.com/user-attachments/assets/92f1d01b-9a15-4cce-bb51-47780d4e5ae7)

- `비검사 메개변수화 가변인수 타입 경고` (Unchecked Generic Array Creation Warning)
  - 제네릭 타입이 있는 배열을 가변인수(varargs)로 사용할 때 발생
  - 주로 배열과 제네릭을 함께 사용할 때 발생(배열은 타입을 유지하는데 제네릭은 컴파일 후 타입이 소거됨)
  - `@SafeVarargs` 어노테이션을 메서드 위에 붙여 경고를 억제함

```java
class UncheckedVarargs {
    public static <T> void rentCars(List<T>... carList) {
        for(List<T> list : carList) {
            System.out.println("Rent: "+list);
        }
    }

    public static void main(String[] args) {
        List<Car> ElectricCars = Arrays.asList(new Car("Tesla"), new Car("Ionic"));
        rentCars(ElectricCars);
    }
}
```

![Image](https://github.com/user-attachments/assets/68adfb2b-3d64-4be5-a908-88df9b5164c5)

- `비검사 변환 경고`
  - 제네릭이 없는 로로 타입을 제네릭 타입 변수에 할당 시 발생

```java
List cars = new ArrayList(); // 로로 타입
List<Car> carList = cars;
```

## 🐍 3. 비검사 경고를 제거하자!

- 비검사 경고를 그냥 둔다면?
  - `ClassCastException` 런타임 에러 발생 가능
  - 치명적인 경고가 발생해도 확인하기 힘들다
- 비검사 경고 제거릍 통해 타입 안정성 보장
- 가독성 향상 및 유지 보수 용이

### 3-1. 제네릭 타입을 사용하기

- 로타입을 사용하지 않고 구체적인 타입 지정하기
- 다이아몬드 연산자(`<>`) 사용하기
- 제네릭을 사용하여 타입 안정성을 확보한다

```java
List strings = new ArrayList(); // ❌
List<String> strings = new ArrayList<>(); // 🆗
```

### 3-2. @SuppressWarnings("unchecked")를 최소한으로 사용하기 💥

- 비검사 경고를 제거할 수는 없지만, 타입 안정성이 확실하다면! `@SuppressWarnings("unchecked")` 애너테이션을 달자
- 단, @SuppressWarnings 애너테이션은 항상 가능한 좁은 범위(변수, 메서드, 클래스 순)에 적용해야 한다.
- 안전한 이유를 항상 주석으로 남겨야 한다. (@SuppressWarnings를 사용해도 되는 이유)

```java
public class SuppresssWarningTest {
    @SuppressWarnings("unchecked")
    // carList 리스트에는 Car 객체만 추가 되어 타입이 모두 같다
    // 타입 안정성이 보장된다
    private static List<Car> cars = (List<Car>) new ArrayList();

    public static void main(String[] args) {
        cars.add(new Car("Tesla"));
        cars.add(new Car("Ionic"));

        for (Car car : cars) {
            System.out.println(car.model);
        }
    }
}
```

## 🤖 최종 결론

> 모든 비검사 경고는 잠재적인 `ClassCastException`을 뜻한다
> 가능한 모든 비검사 경고를 제거하라.
> 제거할 수 없는 경고는 가능한 좁은 범위에 `@SuppressWarnings("unchecked")`로 숨기고 이유를 주석으로 남겨라

---

## ❗어려웠던 점

- 처음에 로 타입에 대한 이해가 명확하지 않아서 어려웠는데, 우리가 코드를 작성할 때 자연스럽게 제네릭 타입을 잘 활용하고 있었다!

---

## 😶‍🌫️ 느낀점

- 경고는 잘 확인하지 않고 넘어가는 경우가 많았는데, 비검사 경고처럼 향후 런타임에 문제가 발생할 수도 있는 경고의 경우 잘 확인하고 넘어가야겠다.
