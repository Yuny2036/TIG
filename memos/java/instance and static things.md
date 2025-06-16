# 인스턴스

## 사전지식
1. Java는 자료형을 두 개로 구분
   - Java에는 `int`, `double`, `float`, `bool`, `char` 과 같이 값을 저장하는 기본형(Primitive Type)
   - `new` 로 생성한 인스턴스인 참조형(Reference Type)
  
2. null은 값이 비어있음을 의미하는 예약어
   - Primitive Type은 null을 가질 수 없음

3. 메모리에서, 실시간으로 할당하는 Heap과 Stack에 인스턴스들을 다룬다.
   - 인스턴스는 Heap에 저장
   - 그 인스턴스의 Heap 주소는 Stack에 저장
  
## 정적 _static_
1. **필드**에 `static` 키워드를 사용해 해당 필드를 같은 클래스가 공유
   - 클래스 이름을 이용해 `static` 필드에 접근하기
     ```Java
     Cleric sally = new Cleric("Whitemane", 1050);
     System.out.println(Cleric.money); // 인스턴스 자원이 아닌, 공유 자원에 접근
     ```
   - 인스턴스 없이도 접근이 가능
     ```Java
     System.out.println(Cleric.money); // 공유 자원에 접근
     ```
2. **메서드**에 `static` 키워드를 사용해 해당 메서드를 같은 클래스에서 호출
   ```Java
   public class Cleric{
     static int money = 5000;
     String name;

     static void setRandomMoney(){
       money = new Random().nextInt(5001);
       System.out.println(Cleric.money);
     }
   }
   ```
   - `static` 메서드 안에서는 `static` 한 멤버에만 접근이 가능
     ```Java
     public class Cleric{
       static int money = 5000;
       String name;

       static void setRandomMoney(){
         money = new Random().nextInt(5001);
         System.out.println(this.money); // 오류, 인스턴스 객체에 접근하려고 함
       }
     }
     ```
