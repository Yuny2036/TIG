# 이벤트 시스템 <sub>Event System</sub>
------
## 개요
> 이벤트 시스템은 키보드, 마우스, 터치, 커스텀 입력 등 입력 기반 애플리케이션의 오브젝트에 이벤트를 전송하는 방법입니다. 이벤트 시스템은 이벤트를 전송에 함께 작용하는 일부 컴포넌트로 구성됩니다. *[출처](https://docs.unity3d.com/Packages/com.unity.ugui@2.0/manual/EventSystem.html)*

유니티에는 개발자가 바로 사용할 수 있도록 이벤트 시스템을 이미 구축해놓았다.

해당 문서는 그에 대한 이야기 대신, 이벤트 시스템을 직접 구현하는 것을 통해 이벤트 시스템의 맥락을 이해하는 것을 목적으로 한다.

## 이벤트와 수발신
이벤트 시스템은 크게 **네 가지가 필요하다**고 보면 된다.

1. 이벤트 발신인 <sub>Dispatcher</sub>
2. 이벤트 수신인 <sub>Listener</sub>
3. 이벤트 <sub>Event</sub>
4. 이벤트 체인 <sub>Event Chain</sub>

### 이벤트 발신인 <sub>Dispatcher</sub>
```C#
// C#, Unity
public interface IMonoEventDispatcher
{
    GameObject gameObject { get; }
}
```

이벤트 발신인 <sub>Dispatcher</sub>은 이벤트 <sub>Event</sub>를 발생시키는 객체이다. 발생한 이벤트는 발신인을 기준으로 하여 점점 상위 계층 (혹은 설정한 방향) 으로 뻗어나간다.

### 이벤트 수신인 <sub>Listener</sub>
```C#
// C#, Unity
public interface IMonoEventListener
{
    GameObject gameObject { get; }
    EventChain OnEventHandle(IEvent param);
}
```

이렇게 나아가는 이벤트는 이벤트 수신인 <sub>Listener</sub>이 받을 수 있는데, 이 때 이벤트 수신인이 해당 이벤트를 처리하는 로직을 구현했다면, 그 동작을 수행한다.

### 이벤트 체인 <sub>Event Chain</sub>
```C#
// C#, Unity
public interface IEvent { }

public enum EventChain
{
    Continue,
    Break,
}
```

이벤트 수신인이 동작을 수행한 뒤에 해당 이벤트의 종료 여부를 결정하게 된다. 만약 이벤트가 전역적으로 모두가 수신하기를 필요로 하는 이벤트라면 첫 이벤트 수신인이 이벤트 체인 <sub>Event Chain</sub>을 끊지 않고, 체인의 상태를 그대로 반환한다.

이로써 수신인이 이벤트에 따른 동작을 수신한 뒤 이벤트를 종료하는 구조를 가질 수도, 혹은 수행하면서도 이벤트는 계속해서 뻗어나가는 구조를 가질 수도 있다.