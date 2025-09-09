# DataSource
------
## 👀 서론:  내가 짠 코드에 갇힌 나
- 내가 짠 코드인데 어디에서부터 손을 대야 하나
- 사소한 거라 생각하고 바꿨는데 엉뚱한 곳에서 펑
- 스파게티 코드들

## ‼️ UI, 데이터, 로직의 분리가 필요한 이유
1. 유지보수 지옥에서 벗어나야 함
   - 아이템 능력치를 바꾸려고 코드를 수정하는 건 그만
2. 협업의 비효율성
   - 개발자에게 의존하는 기획자와 아티스트는 그만

DataSource 는 <u>**UI, 데이터, 로직을 분리**</u>할 수 있는 그 방법을 제시

## DataSource 는..
- 앱이 사용하는 **원천 데이터**
  - ‼️ 파일, 텍스트나 Json, DB 처럼 <u>형태가 다양</u>
- 앱은 단독으로 데이터를 만들어 내지 않음
- 대부분의 앱은 **<u>외부에서 데이터를 받아</u>** 화면에 뿌림

### DataSource 는 어디서 쓰나..
아이템 능력치나 세이브 데이터와 같이 실제로도 쉽게 그 활용처를 확인할 수 있음

## DataSource 의 역할
- 외부 저장소와 직접 통신
- Raw 데이터 수신 및 처리
- CRUD 작업 수행

### 용어 중간 정리
- Raw data : 가공처리를 거치지 않은 상태의 *날것 데이터*
- CRUD : Create(생성), Read(읽기), Update(변경), Delete(삭제)

## DataSource 의 종류
- 앞서 언급한 바와 같이, ***종류가 무궁무진***함
- 텍스트나 파일, Json이나 XML, CSV에서 가져오거나, RDBMS, NoSQL 등 **외부의 DB에서 가져오는 것도 가능**
  - 적재적소에 알맞은 DataSource 를 선택할 것

## 1. 데이터 모델 정의
저장할 데이터 모양의 클래스 작성
```C#
public class Person
{
    public string name { get; set; }
    public int age { get; set; }

    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }
}
```

## 2. 데이터 소스의 기능 정의
- 데이터 소스에 대한 **추상화**를 담당
- **기능만 제공** : 데이터 출처는 고려 않음
- **일반적으로 비동기**로 구현
  - **데이터 송수신 환경**이나 데이터 분량의 차이 등으로 발생하는 문제를 고려
```C#
public interface IDataSource
{
    public Task<List<Person>> GetPeopleAsync();
    public Task SavePersonAsync(List<Person> people);
}
```

## 3. 인터페이스를 구현하는 데이터 소스
기능을 실제로 구현
```C#
public class InMemeoryDataSource : IDataSource
{
    private readonly List<Person> _people = new List<Person>();

    public async Task<List<Person>> GetPeopleAsync()
    {
        await Task.Delay(5000);
        return _people;
    }

    public Task SavePersonAsync(List<Person> people)
    {
        await Task.Delay(5000);
        _people.AddRange(people);
    }
}
```

## DataSource의 작명?
|분류 기준|클래스예시|비고|
|---|---|---|
|저장소 위치 기준|LocalUserDataSource <br>Remote~ <br> Cached~|어디에 저장하는가|
|기술 스택 기준|RoomUserDataSource <br>Retrofit~ <br>SharedPrefs~|어떤 기술로 구현했는가|

사전에 **컨벤션**을 통해 작명에 <u>일관성을 부여</u>할 것

## 인터페이스를 사용하기
```C#
// 인터페이스 정의
public interface IUserDataSource
{
    Task<User> GetUser(string userId);
    Task SaveUser(User user);
}

// 파일 기반의 데이터 소스 구현
// 파일기반이 아니라 다른걸 했다면 클래스 이름도 맞춰서; 그러니 컨벤션을 하면서 들어갈 것
public class FileUserDataSource : IUserDataSource
{
    public async Task<User> GetUser(string userId)
    {
        // User 정보 얻어오는 로직
    }

    public async Task SaveUser(User user)
    {
        // User 정보 저장하는 로직
    }
}
```

- 데이터 저장 방식을 유연하게 변경 가능
  - 예시 : 외부에 있는 MongoDB에서 데이터를 받아오려고 함 > `public class NoSQLUserDataSource : IUserDataSource` 로 하나 **새로 만들어** 씀
  - 기존의 파일 기반 데이터 소스 구현도 <u>양립 가능</u>

### ❔ 인터페이스의 작명에 대문자 I
- **인터페이스 명의 맨 앞에 I**를 붙이는 것이 업계 관례
- 인터페이스와 구현체를 구분하는 단 한 글자

## 코드 뿐 아니라 디렉터리도 구조화하기
```
YourProjectName
┠ Models
┖--- Person.cs              // 데이터 모델
┠ Interfaces
┖--- IDataSources.cs        // 데이터 소스 계약 정의
┠ DataSources
┖--- JsonFileDataSource.cs  // Json 파일 기반 데이터 소스 구현체
┖ Program.cs                // 애플리케이션 진입점(entry point)
```
