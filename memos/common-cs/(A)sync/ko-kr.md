# (비)동기 (A)synchronous
------
## '한 번에 하나씩' - 동기 프로그래밍
- 코드는 순서대로 실행됨
- 작업이 완료될 때까지 프로그램이 중단될 수 없음
  - 먼저 착수한 작업이 끝날때가지 대기해야 함
- 모든 작업은 *이전 작업의 실행이 완료될 때까지 기다려야* 함
  - 위 문제의 대응으로 '비' 동기 방식의 프로그래밍이 제시

## I/O 작업은 비동기 방식이 기본
- 대용량 파일을 위한 비동기 쓰기의 예시
```C#
File.WriteAllTextAsync("hero.json", jsonString).ContinueWith(task => {
    Console.WriteLine("Successfully copied : 1");
});
Console.WriteLine("Successfully copied : 2");

// returns 'can' be:
// # Successfully copied : 2
// # Successfully copied : 1
```

## 비동기 프로그래밍
1. 작업 완료를 기다리지 않고 다른 작업을 시작할 수 있게 허용하는 방식
2. **메인 스레드를 막지 않음**
>  - 대용량 파일의 다운로드 도중 웹 검색을 하거나 음악을 청취할 수 있음
> - 어플리케이션이 버벅임없이 즉각 반응하게 함

### 프로세스 (Process)
1. *운영체제로부터* 독립적인 *자원을 할당*받아 실행되는 프로그램의 **인스턴스**
   - 독립적인 메모리 공간, 파일 핸들과 보안 자격을 *운영체제로부터* 할당받아 프로세스들간의 안전성을 보장

### 쓰레드 (Thread)
1. 컴퓨터가 프로그램을 실행하는 최소단위
2. 하나의 프로세스는 ***최소 하나*** 이상의 쓰레드를 가짐
> - 웹브라우저의 프로세스에서 하나는 페이지를 표시하고, 다른 하나는 사용자의 입력을 처리하고..

## 동시성과 병렬성
여러 작업을 처리하는 것에 대한 차이
- 동시성 : 여러 작업을 **번갈아**가면서 처리 (논리적)
- 병렬성 : 여러 작업을 *실제로* **동시에** 처리하는 것 (물리적)
  - ❗물론 이 안에서도 동시성과 병렬성을 양립시켜 최대 성능을 꾀할 수 있음

### 동시성 (Concurrency)
- 여러 작업이 논리적으로 동시에 실행되는 ***것처럼*** 보이는 개념 (싱글 코어)
- **시분할 방식**으로 여러 쓰레드를 활용해 동시성을 구현할 수 있음
> - 문서작업을 하면서, 회의 준비를 하고 점심 커피를 미리 주문도 하는 회사원의 이미지

### 병렬성 (Parellelism)
- 여러 작업이 **물리적으로** 동시에 실행되는 개념 (멀티 코어)
- 멀티코어 환경에서 **실제로** 여러 쓰레드가 병렬로 실행될 수 있음
> - 회사원 여럿이 함께 일하는 이미지

## 콜백(Callback)의 미로, 콜백 지옥
```C#
static void Main(String[] args)
{
    AsyncExam p = new AsyncExam();
    Console.WriteLine("1. Main method started.");

    // Define callback and deliver.
    p.FetchData(data =>
    {
        Console.WriteLine("2. Data obtained from callback.");
    });

    Console.WriteLine("3. Main method ended. (Can progress asynchronous tasks on background)");

    // Program waits; Preventing a program from getting ended before asynchronous tasks is done.
    // Need proper syncing mechanisms for real programs
    Console.ReadLine();
}
```
### 콜백을 이용한 동기화 방식의 문제
- 코드 깊이가 (수평적으로) 깊어짐
  - 떨어지는 관리 용이성
  - 가독성 저하
- 순서의 예측이 어려움
- 병렬처리가 어려움
- 디버깅이 어려움
  - try-catch 의 사용이 불가

#### 참고 : 유니티의 Coroutine도 콜백
<details>
<summary>Example</summary>

```C# (Unity)
// Unity's Coroutine uses Callbacks.
void Start()
{
    StartCoroutine(DownloadData(data => {
        Debug.log("Data downloaded successfully : " + data);
        StartCoroutine(ProcessImage(data, texture => {
            Debug.log("Image parsed successfully : " texture.name);
            // And some UI update logics sample; or another callback..
        }));
    }));
}
```

</details>

## async와 await를 이용한 현대적 비동기
```C#
static async Task Main(string[] args)
{
    AsyncExam p = new AsyncExam();
    Console.WriteLine("1. Main method started.");

    var result = await.FetchDataAsync();

    Console.WriteLine($"2. Data obtained from callback: {result}");

    Console.WriteLine("3. Main method ended. (Can progress asynchronous tasks on background)");

    // Program waits; Preventing a program from getting ended before asynchronous tasks is done.
    // Need proper syncing mechanisms for real programs
    Console.ReadLine();
}
```
- **await** 키워드는 ***해당 Task가 종료***될 때까지 메서드 실행을 기다림
- 눈으로 보기에 더 *깔끔한 코드* 제공
- try-catch 를 통한 예외처리 가능
