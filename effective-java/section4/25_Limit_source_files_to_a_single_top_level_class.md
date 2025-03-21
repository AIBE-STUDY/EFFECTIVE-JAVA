# 25. 톱레벨 클래스는 한 파일에 하나만 담으라

<br>

# 톱레벨 클래스란?

다른 클래스 안에 들어있지 않은, 가장 바깥쪽에 있는 클래스

보통 .java 파일 하나당 하나의 톱레벨 클래스를 작성하는 것이 원칙이다

## 왜 한 파일에 여러 개의 톱레벨 클래스를 만들면 안 될까?

- 자바는 소스 파일을 컴파일하는 순서에 따라 동작이 달라질 수 있다

- 같은 이름의 클래스를 여러 파일에서 정의하면 충돌이 날 수도 있다

- 이런 문제는 버그를 유발할 수 있고, 코드를 읽기도 어렵다

<br>

## ❌ 나쁜 예시 (한 파일에 여러 개의 톱레벨 클래스)

```java
// Main.java
public class Main {
    public static void main(String[] args) {
        System.out.println(Utensil.NAME + Dessert.NAME);
    }
}
```

```java
// Utensil.java
class Utensil {
    static final String NAME = "pan"; // 팬
}

class Dessert {
    static final String NAME = "cake"; // 케이크
}
```

➔ 여기까지만 있을때 실행하면 "pan cake"이 출력된다

```java
// Dessert.java
class Utensil {
    static final String NAME = "pot"; // 냄비
}

class Dessert {
    static final String NAME = "pie"; // 파이
}
```

➔ 만약 javac Main.java Dessert.java로 컴파일하면 충돌 오류가 발생한다

✔️ javac Dessert.java Main.java로 컴파일하면 "pot pie"로 출력된다 (결과가 달라진다)

<br>

🛑 즉, 파일을 컴파일하는 순서에 따라 실행 결과가 달라지는 문제가 발생할 수 있다

<br>

## 해결 방법

방법 1: 각 톱레벨 클래스를 별도 파일로 분리하기

```java
// Utensil.java
class Utensil {
    static final String NAME = "pan";
}

// Dessert.java
class Dessert {
    static final String NAME = "cake";
}

// Main.java
public class Main {
    public static void main(String[] args) {
        System.out.println(Utensil.NAME + " " + Dessert.NAME);
    }
}

```

✔️ 이렇게 하면 컴파일 순서에 영향을 받지 않는다

<br>

방법 2: 정적 멤버 클래스로 선언하기

```java
public class Meal {
    public static void main(String[] args) {
        System.out.println(Utensil.NAME + " " + Dessert.NAME);
    }

    private static class Utensil {
        static final String NAME = "pan";
    }

    private static class Dessert {
        static final String NAME = "cake";
    }
}
```

✔️ 이렇게 하면 Utensil과 Dessert가 Test 클래스 안에 속해 있으므로 컴파일 오류 없이 동작한다

✔️ 코드도 읽기 쉬워지고, private으로 접근을 제한할 수도 있다

<br>
<br>

---

## 🧩 어려웠던 점

“컴파일 순서가 달라지면 동작이 달라진다”는 개념을 이해하는 것이 어려웠다

<br>

## 💡 느낀 점

자바 코드를 작성할 때 보이지 않는 위험이 있다는 걸 깨달았다

자바 컴파일러가 어떻게 동작하는지 더 잘 이해하게 되었다

파일 이름과 클래스 이름을 일치시키는 것이 왜 중요한지 이제 확실히 알게 되었다
