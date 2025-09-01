# Design

## Singleton Pattern (Singleton)
소프트웨어 디자인 패턴에서 특정 생성자(Class)의 인스턴스(Instance)가 유일함(Unique)을 보장하는 디자인 패턴, 혹은 바로 그 객체  
```C# (Unity)

public static GameManager instance; // 싱글톤을 할당할 전역 변수
void Awake()
    {
        // 싱글톤 변수 instance가 비어있는가?
        if (instance == null)
        {
            // instance가 비어있다면(null) 그곳에 자기 자신을 할당
            instance = this;
        }
        else
        {
            // instance에 이미 다른 GameManager 오브젝트가 할당되어 있는 경우

            // 씬에 두개 이상의 GameManager 오브젝트가 존재한다는 의미.
            // 싱글톤 오브젝트는 하나만 존재해야 하므로 자신의 게임 오브젝트를 파괴
            Debug.LogWarning("씬에 두개 이상의 게임 매니저가 존재합니다!");
            Destroy(gameObject);
        }
    }
```
\**코드 출처 : 도서 '레트로의 유니티 게임 프로그래밍 에센스' 과정 중 일부*

### Why singleton?
1. **유일함** : 누가 어디에서 접근하더라도 동일한 객체를 가리킬 수 있다.
2. 용이함 : 상기한 *유일함*을 효과적으로 이용하기 위해, 해당 싱글톤을 (언어에 따라) `static` 와 같이 전역 처리해 사용  
   \- 전역 처리한 객체가 서비스 전반적으로 사용하는 데이터를 다루게 하여 하위의 서비스들이 데이터를 쉽게 이용 가능

------
