# Getting Started

## Prerequisites
### H/W Requirements
| 구분                | Description                                        |
|---------------------|----------------------------------------------------|
| CPU                 | Intel 2nd Gen Core CPU or higher (16 core or more) |
| CPU instruction set | SSE4.2, AVX, AVX2, AVX-512                         |
| GPU                 | T4(단종모델), A10, A30 (With Driver)                |
| RAM                 | 16G (For Inference), 128G (For Matching)           |
| Hard drive          | NVMe SSD or higher, 100G 이상                      |
| OS                  | Ubuntu 20.04                                       |

### S/W Requirements
| 구분                     | Description                                  |
|--------------------------|----------------------------------------------|
| Docker                   | v19.03 이상                                  |
| Docker-Compose           | v1.29.2 이상                                 |
| NVIDIA-Container-Toolkit | 컨테이너에서 GPU 사용을 위해 필요한 패키지      |


## Service Port
| 구분 | PORT |
|-|-|
| (GPU) Inference API   | 8080 |
| (CPU) Inference API   | 8081 |
| Matching API          | 8082 |


## Server Installation (With Docker Compose)

### Start
```bash
$ docker-compose up -d
```

### Stop
```bash
$ docker-compose down
```

### docker-compose.yml
* Inference Server (GPU)
```yaml
version: "3.8"
(...)
```

* Inference Server (CPU)
```yaml
version: "3.8"
(...)
```

* Matching Server
```yaml
version: "3.8"
(...)
```

## Hello DLiteServer

### Python
* Hello GPU-Inference
* Hello CPU-Inference
* Hello Matching

### C++
* Hello GPU-Inference
* Hello CPU-Inference
* Hello Matching