# Unity - UI and Canvas for VR
------
## 본 문서의 작성 시기
> 6000.0 Unity  
> 3.0.8 XR Interaction Toolkit
## XR Canvas
Unity Editor 로 프로젝트를 개발할 때, UI 구현을 위해 자주 사용되는 Canvas. 이 Canvas는 일반 프로젝트와 XR 프로젝트가 서로 다른 걸 쓴다.

XR 에서 쓸 Canvas 는 메뉴의 `GameObject > XR` 탭에서 찾을 수 있다.

### ❔ Tracked Device Graphic Raycaster
GameObject 자체가 다른 것이 아니고, XR UI 옵션으로 Canvas 를 생성했을 때 컴포넌트의 구성이 다른 걸 볼 수 있는데, 해당 컴포넌트가 XR 환경에서 상호작용에 쓰인다.

요는 XR Controller 장치가 UI 에 Raycast 상호작용을 할 수 있게끔 기능 추가를 해주는 것 정도로 여기면 된다.

