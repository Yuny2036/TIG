# 고계함수 Higher-Order Function
함수를 다루는, 더 높은 수준의 함수
- 함수를 다룬다 == 함수를 Parameter로 씀
- 도식 :: G : (A => B) => C
> 참고 : 일차함수 == 숫자나 문자열 같은 일반적인 데이터를 받는 함수  
> 도식 :: f : A => B

## C# 에서 제공하는 고계함수, LINQ Expression
```CSharp
class Program
{
    static void Main(string[] args)
    {
        // items >>> List
        var items = new List<int> {1, 2, 3, 4, 5};

        // results >>> IEnumerable
        var results = items.Where(e => e % 2 == 0);

        // IEnumerable to List; resultsItems >>> List<int>
        var resultsItems = results.TolIst();
        resultsItems.ForEach(item => Console.WriteLine(item));
    }
}
```
