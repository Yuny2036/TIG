# C# 범용사항 메모
------
별도의 마크다운을 만들기에 여러 이유로 애매하다면 이 문서에 기재할 것

## Auto-property != Field

```C#
public float volume { get; set; }
```

- ❗ Property는 <u>실제 Field가 아님</u> 
- 다만, Auto-property 가 내부적으로 Field를 생성해, 우리 입장에서는 Field인 것*** 처럼*** 보임