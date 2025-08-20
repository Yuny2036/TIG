# Unity - Grab for XR
------
## Near-Far Interactor
**Near-Far Interactor** 를 통해 잡기(Grab) 시도를 발생시킬 수 있다. Interactor 에서 Grab을 시도하면 인접한 범위(Near) 혹은 가상의 광선(Ray)을 쏘아 먼 거리(Far)에 있는 Object를 잡으려 한다. 이렇게, 거리에 따라 달라지는 상호작용 방법을 하나의 Component에서 발생시킬 수 있다.

### Interactables
모든 객체가 작용주체와 상호작용을 할 수는 없다. 개발 과정에서 사용자가 상호작용했으면 하는 특정 Object에 *Interactable* Component를 추가해주면 비로소 상호작용을 할 수 있다.

각 Component 에 따른 대략적인 사용례를 적어보자면 아래와 같다:
- XR Grab Interactable : 공을 던지기, 검을 휘두르기
- XR Simple Interactable : 버튼을 누르기, 레버를 당기기, 스위치를 조작하기
- XR Socket Interactable : 컵을 받침대에 놓기, 열쇠를 자물쇠 구멍에 넣기, 총에 탄창을 장착하기