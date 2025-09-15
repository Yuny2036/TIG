# DTO 와 Mapper
------
## DTO <sub>Data Transfer Object</sub>
데이터 소스를 모델 클래스로 바꾸는 과정에서 순수하게 클래스에 담기 위한 중간 전달 객체

|흐름도 |(왼쪽에서 |오른쪽으로) |
|---|---|---|
|Json|DTO|Model Class|

잘못된 데이터 소스를 받더라도 안 터지게 하려는 클라이언트 개발자의 방어 수단

### 잘못된 데이터 소스를 유발하는 실제 문제들
- 서버 API 변경으로 인한 필드 누락이나 제거
- 서버 장애시 예상치 못한 응답 구조
- 클라이언트와 서버의 버전 불일치

### DTO 코드 예시
```C#
using Newtonsoft.Json;
// Newtonsoft의 패키지를 사용했다고 가정

public class TodoDto
{
    [JsonProperty("userId")]
    public int? UserId { get; set; }

    [JsonProperty("title")]
    public string? Title { get; set; }
}
```
- 모든 필드가 Nullable 변수
- 직렬화와 역직렬화가 가능하게 하기

결과적으로, Json 데이터를 있는 그대로, 터지지 않게 받아들일 것

### DTO는 인공지능에게 사먹으세요... <sub>제발 💢</sub>
작성하려는 데이터의 Json 형태 제공하면서
> “C# Dto로 만들고 모두 nullable 하게 해 줘. newtonsoft json 사용할거야"

**번거롭고 반복적이고 파멸적인 분량**은 기계에게..  
💢 그냥 사먹으라고!

## Model 클래스 역할 재정의
```C#
public class TodoModel
{
    public int UserId { get; }
    public string Title { get; }

    public TodoModel(int UserId, string Title)
    {
        this.UserId = UserId;
        this.Title = Title;
    }

    public override bool Equals(Object? obj) { /* Your codes */}
    public override int GetHashCode() { /* Your codes */}
    public override string ToString() { /* Your codes */}
}
```

- 모든 필드는 Non-nullable 상수
- Equals(), GetHashCode(), ToString() 재정의하기
- 실제 기능에 필요한 것으로만 구성

## Mapper: <sub>DTO를 Model 클래스로 변환
> Q: 아니 Nullable로 받아와서 Non-nullable 로 변환하면 **검증은 누가**하고 **바꾸는 건 누가** 함??  
>   
> A: **Mapper**가 합니다.

순수한 데이터<sub>DTO</sub>를 Model 클래스로 변환하는 로직을 별도의 **Mapper** 클래스에 구현

|흐름도 \| |왼쪽에서 |--->>>---|오른쪽으로 |
|---|---|---|---|
|Json|DTO|(Mapper)|Model Class|

### Mapper 코드 예시
```C#
public static class TodoMapper
{
    public static TodoModel ToModel(this TodoDto dto)
    {
        // 1. ToModel 확장 메서드는 TodoDto를 인수로 받음
        // 2. 이를 TodoModel 객체로 변환하여 반환
        return new TodoModel(dto.Title!, dto.Completed!.Value);
    }
}
```

- Mapper 는 DTO 를 Model 클래스로 변환하는 기능 메서드<sub>Utility Method</sub>
  - **`static` 메서드**나 **확장 메서드**로의 사용 추천
- Nullable 을 **Non-nullabe** 로 변환하기
- DTO 전체를 변환하지 말고, <u>**필요한 부분** 만을 변환하기</u>

### *"왜 DTO 안에 안하고 이렇게 만들어요?"*
1. 데이터 저장용 클래스와 변환 **로직을 분리**
   - 문제가 생기면, Mapper 만 살펴서 수정
2. Mapper 는 복잡한 로직이 포함될 수 있어서 인간이 직접 작성

## 추천하는 폴더 구조
```
Data
├- DataSources          // Json
├- DTOs                 // DTO
├- Mapper               // Mapper (to Model Class)
├- Models               // Model
│
└- Repositories
```

## DataSource 의 반환 타입은 이렇게
```C#
public interface IPokemonApiDataSource
{
    Task<response<PokemonDto>> GetPokemonAsync(string pokemonName);
}
```
DTO를 담은 Response를 반환하여 <u>Repository 가 순수 비즈니스 로직에 집중</u>하게 하기

## Repository 에서 DTO 를 Model 로 변환하여 반환하기
```C#
// Imitated codes; Modify codes for proper usage. 

public async Task<Pokemon?> GetPokemonByNameAsync(string pokemonName)
{
    try
    {
        var response = await _dataSource.GetPokemonAsync(pokemonName);  // Get Json
        var dto = response.Body;  // Contain it into DTO
        return dto.ToModel();  // Convert it to Model via Mapper
    }
    catch (Exception e)
    {
        return null;
    }
}
```

## DTO 는 그러니까..
1. Model 클래스는 **Non-nullable 한 값만** 가지고 있도록 한다
2. Json 데이터는 <sub>문서에 명시되어 있지 않더라도</sub> **null 값을 포함할 수 있**다
3. Mapper 에서 Model 클래스로 변환시 null 따위의 **예외를 사전에 걸러내기에 용이**하다
4. **불완전한 코드가 포함될 것 같다면** 방지턱으로써 DTO가 작동해 줄 수 있다
5. Json 값에 <u>**예외가 없음이 보장**된다면</u>, 반드시 DTO를 도입할 필요는 없다

Model 클래스의 역할을 DTO와 Model로 다시 나누어
- DTO : 데이터 소스 <sub>역</sub>직렬화
- Model : DTO 에서 **필요한 내용만 활용**하는 도메인 객체 

두개로 역할을 분담시켜 사용과 관리에 용이함을 제공