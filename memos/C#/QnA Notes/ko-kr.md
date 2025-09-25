# 질문 답변 노트 <Sub> My QnA Notes</sub>
------
## 문서 개요
**C#**과 관련하여, 카테코리를 뚫어서 보관하기 난해하거나 어디에 넣어야 할 지 모르겠지만 메모의 필요성을 느꼈을 때, 해당 정보들을 기록하고자 개설한 문서이다.

문서의 내용이 순서없이 무분별하게 적힐 가능성이 적지 않으므로 <sub>웹 열람, Windows 운영체제 기준</sub> `Ctrl + F` 를 이용해 키워드를 찾는 식으로 내용을 검색하기를 권한다.

------
------
## 반환값이 있는 메서드를 변수에 담지 않고 사용하면, 그 반환값은 어떻게 되나요?
```C#
// 가상의 C# 엔진이라 가정
public float MoveAndReturnLength(object target, float length)
{
    target.TranslateX(length);
    return length;  // 이 부분
}
```
반환값은 힙 <sub>Heap</sub>영역에 올라가 있다가, 가비지 콜렉터 <sub>Garbage Collector, GC</sub>가 아무도 참조하지 않는 이 반환값을 발견하고 처리하기 때문에, 최종적으로는 자원의 누수를 염려하진 않아도 된다.

어떤 식으로 메서드를 구축해둘 지는 개발자 본인의 몫.
