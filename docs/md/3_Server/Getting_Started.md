# Getting Started
CPU 혹은 GPU를 기반으로 추론 엔진을 제공하는 ServerSDK와  
Feature-Vector를 고속으로 매칭하는 MatchingSDK를 경험해 볼 수 있습니다.


## Prerequisites
### H/W Requirements
| 구분                | Description                                        |
|---------------------|----------------------------------------------------|
| CPU                 | Intel 2nd Gen Core CPU or higher (16 core or more) |
| CPU instruction set | SSE4.2, AVX, AVX2, AVX-512                         |
| GPU                 | A10, A30, T4(단종)                                 |
| RAM                 | 64G                                                |
| Hard drive          | NVMe SSD or higher, 100G                           |
| OS                  | Ubuntu 20.04                                       |

### S/W Requirements
| 구분                     | Description                                  |
|--------------------------|----------------------------------------------|
| Docker                   | v19.03 or later                              |
| Docker-Compose           | v1.25.1 or later                             |
| NVIDIA Container Toolkit | 컨테이너에서 GPU 사용을 위해 필요한 패키지      |

* [관련 참조 사이트](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)


## REST-API Service Port
| 구분 | PORT |
|-|-|
| (GPU) Inference API   | 8080 |
| (CPU) Inference API   | 8081 |
| Matching API          | 8082 |


## Server Installation
Docker-Compose를 통해 서버를 시작/중지하는 방법을 소개합니다.

### Start Server
```bash
$ docker-compose up -d
```

### Stop Server
```bash
$ docker-compose down
```

### docker-compose.yml (예시)
<i class="fa fa-info-circle" aria-hidden="true"></i> 아래에 열거된 Docker Image는, Cubox SDK 배포 담당자에게 문의하시기 바랍니다.

#### Inference Server (GPU)
```yaml
version: "3.8"

services:
 inference-service:
  restart: always
  image: dlite-gpu-server:1.10.0-A10
  shm_size: '1gb'
  ulimits:
   memlock: -1
   stack: 67108864
  command: "tritonserver --model-repository=/models --model-control-mode=none --strict-model-config=1"
  ports:
   - 8000:8000
   - 8001:8001
   - 8002:8002
  networks:
   - gpu_infer_network
  working_dir: /opt/tritonserver/bin
  deploy:
   resources:
    reservations:
     devices:
      - capabilities: [gpu]
        driver: nvidia
        device_ids: ['0']

 api-service:
  restart: always
  image: dlite-gpu-api:1.10.3
  ports:
   - 8080:8080
  networks:
   - gpu_infer_network

networks:
 gpu_infer_network:
  driver: bridge
```

#### Inference Server (CPU)
```yaml
version: "3.8"

services:
 inference-service:
  restart: always
  image: dlite-cpu-server:1.0.3
  shm_size: '1gb'
  ulimits:
   memlock: -1
   stack: 67108864
  command: "--config_path /ovms/config/config_cubox_face_recognition_pipeline_fp16.json --rest_port 9000 --port 9001 --file_system_poll_wait_seconds 0"
  ports:
   - 9000:9000
   - 9001:9001
  networks:
   - cpu_infer_network

 api-service:
  restart: always
  image: dlite-cpu-api:1.9.8
  ports:
   - 8081:8081
  networks:
   - cpu_infer_network

networks:
 cpu_infer_network:
  driver: bridge
```

#### Matching Server
```yaml
version: "3.8"

services:
  standalone:
    image: milvusdb/milvus:v2.2.2
    command: ["milvus", "run", "standalone"]
    environment:
      ETCD_ENDPOINTS: etcd:2379
      MINIO_ADDRESS: minio:9000
    volumes:
      - ${DOCKER_VOLUME_DIRECTORY:-.}/Volumes/milvus:/var/lib/milvus
    ports:
      - "19530:19530"
      - "9091:9091"
    depends_on:
      - "etcd"
      - "minio"

  etcd:
    image: quay.io/coreos/etcd:v3.5.0
    environment:
      - ETCD_AUTO_COMPACTION_MODE=revision
      - ETCD_AUTO_COMPACTION_RETENTION=1000
      - ETCD_QUOTA_BACKEND_BYTES=4294967296
      - ETCD_SNAPSHOT_COUNT=50000
    volumes:
      - ${DOCKER_VOLUME_DIRECTORY:-.}/Volumes/etcd:/etcd
    command: etcd -advertise-client-urls=http://127.0.0.1:2379 -listen-client-urls http://0.0.0.0:2379 --data-dir /etcd

  minio:
    container_name: milvus-minio
    image: minio/minio:RELEASE.2022-03-17T06-34-49Z
    environment:
      MINIO_ACCESS_KEY: minioadmin
      MINIO_SECRET_KEY: minioadmin
    ports:
      - "9001:9001"
    volumes:
      - ${DOCKER_VOLUME_DIRECTORY:-.}/Volumes/minio:/minio_data
    command: minio server /minio_data --console-address ":9001"
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:9000/minio/health/live"]
      interval: 30s
      timeout: 20s
      retries: 3

  api-service:
    restart: always
    image: dlite-matching-api:0.1.4
    ports:
      - 8082:8082
    depends_on:
      - "standalone"

networks:
  default:
    name: milvus
```

## Hello DLiteServer
서버와 통신하는 Python 클라이언트 코드를 통해, 서버기반의 추론과 매칭 기능을 확인합니다.
### Hello GPU-Inference
```bash
# START GPU Inference Server

$ git clone (TBD)
$ python app.py
-----------------
# 결과확인
```
### Hello CPU-Inference
```bash
# START CPU Inference Server

$ git clone (TBD)
$ python app.py
-----------------
# 결과확인
```
### Hello Matching
```bash
# START Matching Server

$ git clone (TBD)
$ python app.py
-----------------
# 결과확인
```
