# 람다(Lambda) 식
------
```CSharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello, World!");

        // 람다(Lambda)식
        // 제네릭에 입력과 출력(마지막) 타입을 적는다.
        Func<int, string> myFunction = age => $"나는 {age}살 입니다.";

        // 입력과 출력의 타입이 동일하면 생략할 수 있다.
        Func<int, int, int> myFunction2 = Math.Max;

        // 예시 :: f(x) = 2x + 3
        // f(10)
        Func<int, int> f = x => 2 * x + 3;
        Console.WriteLine(f(10));
    }
}
```
------
## 1급 객체 (first-class object, first-class citizen)
- 변수에 대입 가능한 객체를 1급 객체라 부름.
- 1급 객체에 해당하는 것 : **값, 인스턴스, 함수**

## 함수 (Function)
- 동일한 입력에 동일한 출력을 보이는 기능 따위
- 참고 : 컴퓨터 프로그래밍에서, `void` 도 출력

## 입출력의 타입이 모두 동일한 람다
```CSharp
var list = new list<int> {1, 2, 3};

list.ForEach(element => Console.WriteLine(element));
list.ForEach(Console.WriteLine);
```
- 입출력이 동일하다는 조건하에, 축약해 작성이 가능함