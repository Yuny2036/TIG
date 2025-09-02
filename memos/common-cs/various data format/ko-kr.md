# 여러가지 데이터 형식
------
## csv
- 콤마로 분리한 값(Comma Seperated Value, CSV)
- 단순함
```csv
name, hp, mp
John, 100, 0
Jane, 30, 120
```

## properties
- 키(Key)와 값(Value)의 쌍으로 이루어진 데이터. 
- C# 에서는 `Properties` 클래스로 읽고 쓸 수 있음
```properties
heroName = John
heroHp = 100
```

## xml
- <> 태그를 활용한 기술 방식
- 포함 관계를 기술할 수 있음
- DOM Parser, SAX Parser 등의 Parser 를 제작할 필요가 있음
```xml
<note>
    <to>John</to>
    <from>Jane</from>
    <heading>Reminder</heading>
    <body>Don't forget me this weekend.</body>
</note>
```

## json
- 네트워크 통신에서 가장 많이 사용
- xml에 비해 적은 용량
- [] 로 리스트, {} 로 객체 표현
- 키(Key)와 값(Value)의 형태
- `Dictionary<string, object>` 와 동일 형태
```json
{
    "name" : "Jane",
    "age" : 25,
    "gender" : "Female",
    "address" : "Seoul, South Korea",
    "hobby" : ["Basketball", "Meditation"],
    "family" : {
        "#" : 2,
        "father" : "John",
        "mother" : "Lily"
    },
    "company" : "3L"
}
```

