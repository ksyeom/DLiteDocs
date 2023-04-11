# Architecture

## DeviceSDK
> Edge Device, Desktop 환경에서 사용하는 추론 엔진

<img src="../../_static/images/1_About/CUFaceSDK_Architecture.jpg" width="100%" height="100%">


## ServerSDK, MatchingSDK
> 서버 환경에서 사용하는, (CPU, GPU) 추론 엔진과 고속의 Feature-Vector 매칭엔진

> 추론과 매칭을 수행하는 Core Engine과 외부로 Restful API를 제공하는 API Server로 구성

<img src="../../_static/images/1_About/CUFaceServer_Architecture.jpg" width="100%" height="100%">