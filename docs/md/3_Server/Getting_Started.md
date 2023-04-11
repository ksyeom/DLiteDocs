# Getting Started

## Server 설치

### 시스템 환경
| Spec.               | Description                                        |
|---------------------|----------------------------------------------------|
| CPU                 | Intel 2nd Gen Core CPU or higher (16 core or more) |
| CPU instruction set | SSE4.2, AVX, AVX2, AVX-512                         |
| RAM                 | 128G                                               |
| Hard drive          | NVMe SSD or higher                                 |
| OS                  | Ubuntu 20.04                                       |

### Server Port
| 구분 | PORT | Description |
|-|-|-|
| (GPU) Inference API   | 8080 | FastAPI framework (Python) |
| (CPU) Inference API   | 8081 | FastAPI framework (Python) |
| Matching API          | 8082 | FastAPI framework (Python) |

### With Docker Compose
```bash
$ docker-compose up -d
```

* Inference Server (GPU)
```yaml
# docker-compose.yml
version: "3.8"

```

* Inference Server (CPU)
```yaml
# docker-compose.yml
version: "3.8"

```

* Matching Server
```yaml
# docker-compose.yml
version: "3.8"

```

## Hello DLiteServer

### Python
* Hello ICU-GPU-Server
* Hello ICU-CPU-Server
* Hello MCU-Server

### C++
* Hello ICU-GPU-Server
* Hello ICU-CPU-Server
* Hello MCU-Server