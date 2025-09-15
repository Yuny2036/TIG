# C# 범용사항 메모
------
별도의 마크다운을 만들기에 여러 이유로 애매하다면 이 문서에 기재할 것

## Auto-property != Field

```C#
public float volume { get; set; }
```

- ❗ Property는 <u>실제 Field가 아님</u> 
- 다만, Auto-property 가 내부적으로 Field를 생성해, 우리 입장에서는 Field인 것***처럼*** 보임

## Named-parameter
```C#
// Method in Class of somewhere
public bool CanFinish(int former, int latter, string status) {
    // Yes, your codes here
}

// Calling the method with named-parameter
static void Main(string[] args)
{
    CanFinish(
        status: "RNG",
        former: 20050,
        latter: 17
    );
}
```

- 메서드를 만들 때, 각 매개변수의 이름을 지정
- 호출할 때, **매개변수의 이름과 값**을 `:` 를 사용해 직접 연결
- 이름으로 연결해 호출할 때는 매개변수의 순서는 무관
- 매개변수의 이름을 명시, 용도에 대한 안내 보조