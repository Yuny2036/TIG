# 캡슐화 Encapsulation

## Why capsule?
1. 사람의 실수로 발생하는 문제들을 미연에 방지하고자 함
   - 의도적으로 접근에 제한을 두어 속성이 덮어쓰이거나 잘못된 조작을 하는 것을 미연에 차단
   - 잘못된 접근에 대해 개발자에게 제어할 방법을 제공
```Java
public class Inn() {
  void checkIn(Hero hero) {
    // ??? "아니 내 실수는 맞는데, 왜 직접 값에 접근이 가능한거냐고"
    hero.hp = -100;
  }
}
```
2. 구현된 프로그래밍이 '현실세계' 의 직관에 일치하게 프로그래밍하려는 제어 방법

## How encapsulate?
|제한 강도|명칭|설정 방법|접근 가능 범위|
|---|---:|---:|---|
|엄격|private|private|자기 자신의 클래스|
|덜 엄격|*packaged private* (기본값)|*아무것도 쓰지 않음*|자신과 같은 패키지에 소속된 클래스|
|약간 느슨|protected|protected|자신과 같은 패키지에 소속되었거나, 자신을 상속받은 자식 클래스|
|느슨|public|public|모든 클래스|

## 내가 너무 바보에요 | 귀찮아요
- 모든 필드 private
- 모든 메서드 public
- ***이유가 딱히 없으면*** 모든 클래스 public

## getter, setter
- 메서드를 경유하는 필드 조작
- 객체의 속성에 대한 권한은 당사 객체에게만 유지하는 일종의 철?학
```Java
private int hp;

// getter
public int getHP() {
  return hp;
}

// setter
public void setHP(int hp) {
  this.hp = hp;
}
```

### Why getter, setter?
1. 읽기 전용, 쓰기 전용의 필드 실현
2. 필드의 이름 등 클래스 내부 설계를 자유롭게 변경 가능
3. 필드로의 엑세스를 검사할 수 있음
```Java
public void setName(String name) {
  if (name == null) throw IllegalArgumentException("Name can be *null*");
  if (name.length >= 10) throw IllegalArgumentException("Name's too long");
  this.name = name;
}
```

### throwing Exceptions
- 예외를 던지는 것으로 작업물에 접근하는 다른 개발자가 (우리의) 코드를 잘못 사용하고 있음을 인지시킬 수 있음
- Test codes에서 예외를 고의로 받아서 예외처리를 제대로 하고 있는지 잊지말고 확인하기
  ```Java
  assertThrows(IllegalArgumentException.class, () -> {
    sally.setMP(11); // 0 ~ 10 까지의 정수만을 mp로 가짐
  });
  ```
