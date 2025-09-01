# 예외와 오류
## 예외 (Exception)
프로그램을 설계할 때, 실행 시에 발생할 수 있는 것을 예측하여 사전에 예외 처리가 되도록 할 필요가 있음

이럴 때 적절한 조치가 없으면, 프로그램은 **오류(Error)**가 발생하며 죽음

## 오류의 종류
1. 문법 오류 (Syntex Error)
2. 런타임 오류 (Runtime Error)
3. 논리 오류 (Logic Error)

### 오류의 상황별 처리
1. 문법 오류
   - 코드의 형식적 오류로 발생
   - 컴파일 단계에서 발견
   - 컴파일러가 지적하는 내용을 보고 대응
2. 런타임 오류
   - 실행 중 예상 외의 사태가 발생하여 동작이 중지됨
   - 실행 도중 프로그램 혹은 서비스가 강제로 종료되며 인지
   - 해당 시점에 실행된 코드를 유추하여 수정
     - 오류 메시지나 로그 등의 보조를 받을 수도 있음
     - 예외 처리를 통해 런타임 에러를 대처
3. 논리 오류
   - 기술한 처리 내용에 논리적인 오류가 있음
   - 실행 시에 예상과 다른 값이 출력되며 인지
   - 스스로 원인을 찾아 논리를 교정해야 함

## 기타 예외적인 상황들
1. 메모리 부족
2. 파일을 찾을 수 없음
3. 불량한 네트워크 통신 상태

## 예외 처리의 흐름, try-catch
```Csharp
try
{
    // Your codes with error
}
catch (ArgumentException argEx)
{
    // when ArgumentException happens.
}
catch (Exception e)
{
    // when all the other exception happens.
}
```
- `try-catch` 문으로 예외를 처리할 수 있음.
- 다양한 종류의 예외가 있음.

### throw 를 통한 예외 처리 미루기
```CSharp
static void Main(string[] args)
{
    try
    {
        SomeError();
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }

    Console.WriteLine("Hello, World!");
}

static void SomeError()
{
    try
    {
        SomeError2();
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
        throw; // postpones exception handling
    }
}

static void SomeError2()
{
    throw new ArgumentException("오류 발생");
}
```
- `throw` 를 통해 예외의 처리를 상위 메서드로 미룰 수 있음.
- Main 처럼 최상위 메서드에서 발생한 예외는 각 언어에 따라 책임지는 주체가 다름
  - 예시
    - Java : JVM (자바 가상 머신)
    - C# : CLR (공용 언어 런타임)

### finally 를 이용한 필수 실행부 작성
```CSharp
try
{
    SomeError();
}
catch (Exception e)
{
    Console.WriteLine(e.Message);
}
finally
{
    Console.WriteLine("Must be executed!");
}
```

## 사용자 정의 예외 클래스
```CSharp
public class InventoryFullException : Exception
{
    public InventoryFullException() : base("인벤토리가 가득 찼습니다.")
    {

    }
}
```
