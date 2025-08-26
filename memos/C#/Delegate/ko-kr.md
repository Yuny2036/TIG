# delegate
```CSharp
class Program
{
    // delegate function
    public delegate void OnClick();

    static void SayHello()
    {
        Console.WriteLine("Hello.");
    }

    // 원하는 함수를 onClick에 넣자.
    void SetOnClick(OnClick onClick)
    {
        onClick();
    }

    static void Main(string[] args)
    {
        var Program = new Program();

        // 이미 만든 함수의 대입
        program.SetOnClick(SayHello);

        // 즉석으로 만든 함수의 대입
        program.SetOnClick(() => { COnsole.WriteLine("World!")});
    }
}
```
------
## *입력과 출력이 같다면, 같은 함수*
해당 맥락에서, 입력과 출력 만을 명시한 대리함수를 선언해 상황에 따라 다양한 작동을 제공할 수 있는데, 이 때 `delegate` 를 사용함