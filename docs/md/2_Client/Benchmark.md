# Benchmark

Face Detection과 Face Feature Extraction의 디바이스별 추론속도 확인

## NUC

### 디바이스 정보
| H/W Model | NUC10FNH                               |
|-----------|----------------------------------------|
| CPU       | Intel Core i7-10710U (6Core 12Threads) |
| RAM       | 64G                                    |
| OS        | Ubuntu 18.04                           |

### 추론모델
| Detection  | fd-003-ov20214-fp16.cubox |
|------------|---------------------------|
| Extraction | fr-01-ov20214-fp16.cubox  |

### 결과
| Latency    | Detection                      | 13 (ms)      |
|------------|--------------------------------|--------------|
|            | Feature-Extraction             | 55 (ms)      |
|            | Detection + Feature-Extraction | 68 (ms)      |
| Throughput | Total FPS                      | **14 (fps)** |
