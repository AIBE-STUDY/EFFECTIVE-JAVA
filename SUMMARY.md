# Table of contents

- [🍄 All About Effective Java](README.md)

## 🐢 All About Study

- [🧩 스터디 진행 방식](all-about-study/howtostudy.md)
- [📔 깃북 활용법](all-about-study/howtousegitbook.md)
- [🔎 아이템 체크리스트](all-about-study/checklist.md)

## 💾 Effective Java

- [객체 생성과 파괴](effective-java/section2/README.md)
  - [1. 생성자 대신 정적 팩터리 메서드를 고려하라](effective-java/section2/1.Consider_static_factory_methods_instead_of_constructors.md)
  - [2. 생성자에 매개변수가 많다면 빌더를 고려하라](effective-java/section2/2.Consider_a_builder_when_faced_with_many_constructor_parameters.md)
  - [3. private 생성자나 열거 타입으로 싱글턴임을 보증하라](effective-java/section2/3.Enforce_the_singleton_property_with_a_private_constructor_or_an_enum_type.md)
  - [4. 인스턴스화를 막으려거든 private 생성자를 사용하라](effective-java/section2/4.Enforce_noninstantiability_with_a_private_constructor.md)
  - [5. 자원을 직접 명시하지 말고 의존 객체 주입을 사용하라](effective-java/section2/5.Prefer_dependency_injection_to_hardwiring_resources.md)
  - [6. 불필요한 객체 생성을 피하라](effective-java/section2/6.Avoid_creating_unnecessary_objects.md)
  - [7. 다 쓴 객체 참조를 해제하라](effective-java/section2/7.Eliminate_obsolete_object_references.md)
  - [8. finalizer와 cleaner 사용을 피하라](effective-java/section2/8.Avoid_finalizers_and_cleaners.md)
  - [9. try-finally보다는 try-with-resources를 사용하라](effective-java/section2/9.Prefer-try-with-resources-to-try-finally.md)
- [모든 객체의 공통 메서드](effective-java/section3/README.md)
  - [10. equals는 일반 규약을 지켜 재정의하라](effective-java/section3/10.Obey_the_general_contract_when_overriding_equals.md)
  - [11. equals를 재정의하려거든 hashCode도 재정의하라](effective-java/section3/11.-equals-hashcode.md)
  - [12. toString을 항상 재정의하라](effective-java/section3/12.-tostring.md)
  - [13. clone 재정의는 주의해서 진행하라](effective-java/section3/13.-clone.md)
  - [14. Comparable을 구현할지 고려하라](effective-java/section3/14.-comparable.md)
- [클래스와 인터페이스](effective-java/section4/README.md)
  - [15. 클래스와 멤버의 접근 권한을 최소화하라](effective-java/section4/15.Minimize_the_accessibility_of_classes_and_members.md)
  - [16. public 클래스에서는 public 필드가 아닌 접근자 메서드를 사용하라](effective-java/section4/16.In_public_classes,_use_accessor_methods,_not_public_fields.md)
  - [17. 변경 가능성을 최소화하라](effective-java/section4/17..md)
  - [18. 상속보다는 컴포지션을 사용하라](effective-java/section4/18..md)
  - [19. 상속을 고려해 설계하고 문서화하라. 그러지 않았다면 상속을 금지하라](effective-java/section4/19.Design_and_document_for_inheritance_or_else_prohibit_it.mdmd)
  - [20. 추상 클래스보다는 인터페이스를 우선하라](effective-java/section4/20.Prefer_interfaces_to_abstract_classes.md)
  - [21. 인터페이스는 구현하는 쪽을 생각해 설계하라](effective-java/section4/21..md)
  - [22. 인터페이스는 타입을 정의하는 용도로만 사용하라](effective-java/section4/22..md)
- [제네릭](effective-java/section5.md)
