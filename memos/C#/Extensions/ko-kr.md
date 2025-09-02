# 확장 메서드 Extensions
------
```C#
using System;

public static class IntExtensions
{
    public static int? MyTryParse(this string str)
    {
        try
        {
            return int.Parse(str);
        }
        catch
        {
            return null;
        }
    }
}

class Program
{
    static void Main()
    {
        int? numString = "9989".MyTryParse();

        Console.WriteLine(numString.GetType());
    }
}
```
### 특징
- `static` 클래스의 `static` 메서드로 정의
- **첫 번째 매개변수에 `this` 키워드**를 사용하여 *어떤 타입을 확장할 지 지정*

### 사용
사용은 인스턴스 메서드처럼, 실제는 `static` 메서드
- `public static` 클래스 안에 선언
- `public static ReturnType MethodName(this TargetType parameter, ...)` 의 형태
- 확장한 타입의 인스턴스에, **인스턴스 메서드처럼** 사용