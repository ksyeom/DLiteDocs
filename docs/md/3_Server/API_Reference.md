# API Reference

## Inference (GPU)

### Default

#### /v1/health

`GET /v1/health`

*서버의 Live 상태를 확인합니다.*

<h6>Parameters</h6>

<h6 id="health_v1_health_get-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|Inline|


#### /v1/info/server

`GET /v1/info/server`

*서버의 기본적인 버전 정보들을 확인합니다.*

<h6>Parameters</h6>

<h6 id="server_info_v1_info_server_get-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|Inline|


#### /v1/info/model

`GET /v1/info/model`

*서비스중인 추론모델의 이름을 식별합니다.*

<h6>Parameters</h6>

<h6 id="model_info_v1_info_model_get-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|Inline|

#### /v1/info/model/{model_name}

`GET /v1/info/model/{model_name}`

*지정한 추론모델의 구성정보를 확인합니다.*

<h6 id="model_detail_info_v1_info_model__model_name__get-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|model_name|path|string|true|none|

<h6>Parameters</h6>

<h6 id="model_detail_info_v1_info_model__model_name__get-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|Inline|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|


### Face Identification

#### /v1/detect

`POST /v1/detect`

*단일 이미지에서 다수 사용자 얼굴을 탐지합니다. (얼굴영역, 랜드마크)*

<h6>Body Parameter</h6>

```json
{
  "seq": 0,
  "maxResults": 750,
  "detectSortType": 0,
  "image": "string"
}
```

<h6 id="detect_v1_detect_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[DetectReqBody](#schemadetectreqbody)|true|none|

<h6>200 Response</h6>

```json
{
  "seq": 0,
  "faces": []
}
```

<h6 id="detect_v1_detect_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[DetectResponse](#schemadetectresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/feature

`POST /v1/feature`

*단일 이미지에서 단일 사용자의 얼굴 특징점을 추출합니다.*

<h6>Body Parameter</h6>

```json
{
  "image": "string"
}
```

<h6 id="feature_v1_feature_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[FeatureReqBody](#schemafeaturereqbody)|true|none|

<h6>200 Response</h6>

```json
{
  "version": "1.10.3",
  "feature": "",
  "face_detect": {
    "processed": true,
    "confidence": 0,
    "boundingBox": {
      "left": 0,
      "top": 0,
      "right": 0,
      "bottom": 0
    },
    "landmarks": [
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      }
    ]
  }
}
```

<h6 id="feature_v1_feature_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[FeatureResponse](#schemafeatureresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/feature_only

`POST /v1/feature-only`

*전처리된 단일 이미지 (Aligned 112x112) 에서 단일 사용자의 얼굴 특징점을 추출합니다.*

<h6>Body Parameter</h6>

```json
{
  "image": "string"
}
```

<h6 id="feature_only_v1_feature_only_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[FeatureReqBody](#schemafeaturereqbody)|true|none|

<h6>200 Response</h6>

```json
{
  "version": "1.10.3",
  "feature": "",
  "face_detect": {
    "processed": true,
    "confidence": 0,
    "boundingBox": {
      "left": 0,
      "top": 0,
      "right": 0,
      "bottom": 0
    },
    "landmarks": [
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      }
    ]
  }
}
```

<h6 id="feature_only_v1_feature_only_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[FeatureResponse](#schemafeatureresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/multi_feature

`POST /v1/multi-feature`

*단일 이미지에서 다수 사용자의 얼굴 특징점들을 추출합니다.*

<h6>Body Parameter</h6>

```json
{
  "image": "string",
  "maxResults": 128
}
```

<h6 id="multi_feature_v1_multi_feature_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[MultiFeatureReqBody](#schemamultifeaturereqbody)|true|none|

<h6>200 Response</h6>

```json
{
  "version": "1.10.3",
  "feature_info_list": []
}
```

<h6 id="multi_feature_v1_multi_feature_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[MultiFeatureResponse](#schemamultifeatureresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/embeddings

`POST /v1/embeddings`

*단일 이미지에서 단일 사용자의 얼굴 특징점 배열을 추출합니다.*

<h6>Body Parameter</h6>

```json
{
  "image": "string"
}
```

<h6 id="embeddings_v1_embeddings_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[EmbeddingsReqBody](#schemaembeddingsreqbody)|true|none|

<h6>200 Response</h6>

```json
{
  "version": "1.10.3",
  "embeddings": [],
  "face_detect": {
    "processed": true,
    "confidence": 0,
    "boundingBox": {
      "left": 0,
      "top": 0,
      "right": 0,
      "bottom": 0
    },
    "landmarks": [
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      }
    ]
  }
}
```

<h6 id="embeddings_v1_embeddings_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[EmbeddingsResponse](#schemaembeddingsresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/embeddings_only

`POST /v1/embeddings-only`

*전처리된 단일 이미지 (Aligned 112x112) 에서 단일 사용자의 얼굴 특징점 배열을 추출합니다.*

<h6>Body Parameter</h6>

```json
{
  "image": "string"
}
```

<h6 id="embeddings_only_v1_embeddings_only_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[EmbeddingsReqBody](#schemaembeddingsreqbody)|true|none|

<h6>200 Response</h6>

```json
{
  "version": "1.10.3",
  "embeddings": [],
  "face_detect": {
    "processed": true,
    "confidence": 0,
    "boundingBox": {
      "left": 0,
      "top": 0,
      "right": 0,
      "bottom": 0
    },
    "landmarks": [
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      }
    ]
  }
}
```

<h6 id="embeddings_only_v1_embeddings_only_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[EmbeddingsResponse](#schemaembeddingsresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/multi_embeddings

`POST /v1/multi-embeddings`

*단일 이미지에서 다수 사용자의 얼굴 특징점 배열들을 추출합니다.*

<h6>Body Parameter</h6>

```json
{
  "image": "string",
  "maxResults": 128
}
```

<h6 id="multi_embeddings_v1_multi_embeddings_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[MultiEmbeddingsReqBody](#schemamultiembeddingsreqbody)|true|none|

<h6>200 Response</h6>

```json
{
  "version": "1.10.3",
  "embeddings_info_list": []
}
```

<h6 id="multi_embeddings_v1_multi_embeddings_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[MultiEmbeddingsResponse](#schemamultiembeddingsresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/score

`POST /v1/score`

*2개의 이미지로부터, 각각 포함되어 있는 얼굴간의 유사도를 측정합니다.*

<h6>Body Parameter</h6>

```json
{
  "image1": "string",
  "image2": "string"
}
```

<h6 id="image_score_v1_score_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[ScoreReqBody](#schemascorereqbody)|true|none|

<h6>200 Response</h6>

```json
{
  "score": 0,
  "face_detects": []
}
```

<h6 id="image_score_v1_score_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[ScoreResponse](#schemascoreresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/feature-score

`POST /v1/feature-score`

*2개의 특징점간의 유사도를 측정합니다.*

<h6>Body Parameter</h6>

```json
{
  "feature1": "string",
  "feature2": "string"
}
```

<h6 id="feature_score_v1_feature_score_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[FeatureScoreReqBody](#schemafeaturescorereqbody)|true|none|

<h6>200 Response</h6>

```json
{
  "score": 0
}
```

<h6 id="feature_score_v1_feature_score_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[FeatureScoreResponse](#schemafeaturescoreresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/file/detect

`POST /v1/file/detect`

*단일 이미지 파일에서 다수 사용자 얼굴을 탐지합니다. (얼굴영역, 랜드마크)*

<h6>Body Parameter</h6>

```yaml
seq: 0
maxResults: 750
detectSortType: 0
image: string

```

<h6 id="file_detect_v1_file_detect_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[Body_file_detect_v1_file_detect_post](#schemabody_file_detect_v1_file_detect_post)|true|none|

<h6>200 Response</h6>

```json
{
  "seq": 0,
  "faces": []
}
```

<h6 id="file_detect_v1_file_detect_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[DetectResponse](#schemadetectresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/file/feature

`POST /v1/file/feature`

*단일 이미지 파일에서 단일 사용자의 얼굴 특징점을 추출합니다.*

<h6>Body Parameter</h6>

```yaml
image: string

```

<h6 id="file_feature_v1_file_feature_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[Body_file_feature_v1_file_feature_post](#schemabody_file_feature_v1_file_feature_post)|true|none|

<h6>200 Response</h6>

```json
{
  "version": "1.10.3",
  "feature": "",
  "face_detect": {
    "processed": true,
    "confidence": 0,
    "boundingBox": {
      "left": 0,
      "top": 0,
      "right": 0,
      "bottom": 0
    },
    "landmarks": [
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      }
    ]
  }
}
```

<h6 id="file_feature_v1_file_feature_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[FeatureResponse](#schemafeatureresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/file/feature-only

`POST /v1/file/feature-only`

*전처리된 단일 이미지 (Aligned 112x112) 파일에서 단일 사용자의 얼굴 특징점을 추출합니다.*

<h6>Body Parameter</h6>

```yaml
image: string

```

<h6 id="file_feature_only_v1_file_feature_only_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[Body_file_feature_only_v1_file_feature_only_post](#schemabody_file_feature_only_v1_file_feature_only_post)|true|none|

<h6>200 Response</h6>

```json
{
  "version": "1.10.3",
  "feature": "",
  "face_detect": {
    "processed": true,
    "confidence": 0,
    "boundingBox": {
      "left": 0,
      "top": 0,
      "right": 0,
      "bottom": 0
    },
    "landmarks": [
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      }
    ]
  }
}
```

<h6 id="file_feature_only_v1_file_feature_only_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[FeatureResponse](#schemafeatureresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/file/embeddings

`POST /v1/file/embeddings`

*단일 이미지 파일에서 단일 사용자의 얼굴 특징점 배열을 추출합니다.*

<h6>Body Parameter</h6>

```yaml
image: string

```

<h6 id="file_embeddings_v1_file_embeddings_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[Body_file_embeddings_v1_file_embeddings_post](#schemabody_file_embeddings_v1_file_embeddings_post)|true|none|

<h6>200 Response</h6>

```json
{
  "version": "1.10.3",
  "embeddings": [],
  "face_detect": {
    "processed": true,
    "confidence": 0,
    "boundingBox": {
      "left": 0,
      "top": 0,
      "right": 0,
      "bottom": 0
    },
    "landmarks": [
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      }
    ]
  }
}
```

<h6 id="file_embeddings_v1_file_embeddings_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[EmbeddingsResponse](#schemaembeddingsresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/file/embeddings-only

`POST /v1/file/embeddings-only`

*전처리된 단일 이미지 (Aligned 112x112) 파일에서 단일 사용자의 얼굴 특징점 배열을 추출합니다.*

<h6>Body Parameter</h6>

```yaml
image: string

```

<h6 id="file_embeddings_only_v1_file_embeddings_only_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[Body_file_embeddings_only_v1_file_embeddings_only_post](#schemabody_file_embeddings_only_v1_file_embeddings_only_post)|true|none|

<h6>200 Response</h6>

```json
{
  "version": "1.10.3",
  "embeddings": [],
  "face_detect": {
    "processed": true,
    "confidence": 0,
    "boundingBox": {
      "left": 0,
      "top": 0,
      "right": 0,
      "bottom": 0
    },
    "landmarks": [
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      }
    ]
  }
}
```

<h6 id="file_embeddings_only_v1_file_embeddings_only_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[EmbeddingsResponse](#schemaembeddingsresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

#### /v1/file/score

`POST /v1/file/score`

*2개의 이미지 파일로부터, 각각 포함되어 있는 얼굴간의 유사도를 측정합니다.*

<h6>Body Parameter</h6>

```yaml
image1: string
image2: string

```

<h6 id="file_score_v1_file_score_post-parameters">Parameters</h6>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|[Body_file_score_v1_file_score_post](#schemabody_file_score_v1_file_score_post)|true|none|

<h6>200 Response</h6>

```json
{
  "score": 0,
  "face_detects": []
}
```

<h6 id="file_score_v1_file_score_post-responses">Responses</h6>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful Response|[ScoreResponse](#schemascoreresponse)|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Validation Error|[HTTPValidationError](#schemahttpvalidationerror)|

---

### Schemas

<h4 id="schemabody_file_detect_v1_file_detect_post">/v1/file/detect body</h4>

```json
{
  "seq": 0,
  "maxResults": 750,
  "detectSortType": 0,
  "image": "string"
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|seq|integer|false|none|none|
|maxResults|integer|false|none|none|
|detectSortType|integer|false|none|none|
|image|string(binary)|true|none|none|

<h4 id="schemabody_file_embeddings_only_v1_file_embeddings_only_post">/v1/file/embeddings-only body</h4>

```json
{
  "image": "string"
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|image|string(binary)|true|none|none|

<h4 id="schemabody_file_embeddings_v1_file_embeddings_post">/v1/file/embeddings</h4>

```json
{
  "image": "string"
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|image|string(binary)|true|none|none|

<h4 id="schemabody_file_feature_only_v1_file_feature_only_post">/v1/file/feature-only body</h4>

```json
{
  "image": "string"
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|image|string(binary)|true|none|none|

<h4 id="schemabody_file_feature_v1_file_feature_post">/v1/file/feature</h4>

```json
{
  "image": "string"
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|image|string(binary)|true|none|none|

<h4 id="schemabody_file_score_v1_file_score_post">/v1/file/score</h4>

```json
{
  "image1": "string",
  "image2": "string"
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|image1|string(binary)|true|none|none|
|image2|string(binary)|true|none|none|

<h4 id="schemaboundingbox">BoundingBox</h4>

```json
{
  "left": 0,
  "top": 0,
  "right": 0,
  "bottom": 0
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|left|integer|false|none|none|
|top|integer|false|none|none|
|right|integer|false|none|none|
|bottom|integer|false|none|none|

<a id="schemadetectreqbody">DetectReqBody</a>

```json
{
  "seq": 0,
  "maxResults": 750,
  "detectSortType": 0,
  "image": "string"
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|seq|integer|false|none|reserved|
|maxResults|integer|false|none|none|
|detectSortType|integer|false|none|none|
|image|string|true|none|base64 encoded data|

<h4 id="schemadetectresponse">DetectResponse</h4>

```json
{
  "seq": 0,
  "faces": []
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|seq|integer|false|none|none|
|faces|[[DetectResult](#schemadetectresult)]|false|none|none|

<h4 id="schemadetectresult">DetectResult</h4>

```json
{
  "processed": true,
  "confidence": 0,
  "boundingBox": {
    "left": 0,
    "top": 0,
    "right": 0,
    "bottom": 0
  },
  "landmarks": [
    {
      "x": 0,
      "y": 0
    },
    {
      "x": 0,
      "y": 0
    },
    {
      "x": 0,
      "y": 0
    },
    {
      "x": 0,
      "y": 0
    },
    {
      "x": 0,
      "y": 0
    }
  ]
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|processed|boolean|false|none|none|
|confidence|number|false|none|none|
|boundingBox|[BoundingBox](#schemaboundingbox)|false|none|none|
|landmarks|[[Landmark](#schemalandmark)]|false|none|none|

<h4 id="schemaembeddingsinforesult">EmbeddingsInfoResult</h4>

```json
{
  "embeddings": [],
  "face_detect": {
    "processed": true,
    "confidence": 0,
    "boundingBox": {
      "left": 0,
      "top": 0,
      "right": 0,
      "bottom": 0
    },
    "landmarks": [
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      }
    ]
  }
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|embeddings|[number]|false|none|none|
|face_detect|[DetectResult](#schemadetectresult)|false|none|none|

<h4 id="schemaembeddingsreqbody">EmbeddingsReqBody</h4>

```json
{
  "image": "string"
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|image|string|true|none|base64 encoded data|

<h4 id="schemaembeddingsresponse">EmbeddingsResponse</h4>

```json
{
  "version": "1.10.3",
  "embeddings": [],
  "face_detect": {
    "processed": true,
    "confidence": 0,
    "boundingBox": {
      "left": 0,
      "top": 0,
      "right": 0,
      "bottom": 0
    },
    "landmarks": [
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      }
    ]
  }
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|version|string|false|none|none|
|embeddings|[number]|false|none|none|
|face_detect|[DetectResult](#schemadetectresult)|false|none|none|

<h4 id="schemafeatureinforesult">FeatureInfoResult</h4>

```json
{
  "feature": "",
  "face_detect": {
    "processed": true,
    "confidence": 0,
    "boundingBox": {
      "left": 0,
      "top": 0,
      "right": 0,
      "bottom": 0
    },
    "landmarks": [
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      }
    ]
  }
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|feature|string|false|none|none|
|face_detect|[DetectResult](#schemadetectresult)|false|none|none|

<h4 id="schemafeaturereqbody">FeatureReqBody</h4>

```json
{
  "image": "string"
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|image|string|true|none|base64 encoded data|

<h4 id="schemafeatureresponse">FeatureResponse</h4>

```json
{
  "version": "1.10.3",
  "feature": "",
  "face_detect": {
    "processed": true,
    "confidence": 0,
    "boundingBox": {
      "left": 0,
      "top": 0,
      "right": 0,
      "bottom": 0
    },
    "landmarks": [
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      },
      {
        "x": 0,
        "y": 0
      }
    ]
  }
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|version|string|false|none|none|
|feature|string|false|none|none|
|face_detect|[DetectResult](#schemadetectresult)|false|none|none|

<h4 id="schemafeaturescorereqbody">FeatureScoreReqBody</h4>

```json
{
  "feature1": "string",
  "feature2": "string"
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|feature1|string|true|none|base64 encoded data|
|feature2|string|true|none|base64 encoded data|

<h4 id="schemafeaturescoreresponse">FeatureScoreResponse</h4>

```json
{
  "score": 0
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|score|number|false|none|none|

<h4 id="schemahttpvalidationerror">HTTPValidationError</h4>

```json
{
  "detail": [
    {
      "loc": [
        "string"
      ],
      "msg": "string",
      "type": "string"
    }
  ]
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|detail|[[ValidationError](#schemavalidationerror)]|false|none|none|

<h4 id="schemalandmark">Landmark</h4>

```json
{
  "x": 0,
  "y": 0
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|x|integer|false|none|none|
|y|integer|false|none|none|

<h4 id="schemamultiembeddingsreqbody">MultiEmbeddingsReqBody</h4>

```json
{
  "image": "string",
  "maxResults": 128
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|image|string|true|none|base64 encoded data|
|maxResults|integer|false|none|none|

<h4 id="schemamultiembeddingsresponse">MultiEmbeddingsResponse</h4>

```json
{
  "version": "1.10.3",
  "embeddings_info_list": []
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|version|string|false|none|none|
|embeddings_info_list|[[EmbeddingsInfoResult](#schemaembeddingsinforesult)]|false|none|none|

<h4 id="schemamultifeaturereqbody">MultiFeatureReqBody</h4>

```json
{
  "image": "string",
  "maxResults": 128
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|image|string|true|none|base64 encoded data|
|maxResults|integer|false|none|none|

<h4 id="schemamultifeatureresponse">MultiFeatureResponse</h4>

```json
{
  "version": "1.10.3",
  "feature_info_list": []
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|version|string|false|none|none|
|feature_info_list|[[FeatureInfoResult](#schemafeatureinforesult)]|false|none|none|

<h4 id="schemascorereqbody">ScoreReqBody</h4>

```json
{
  "image1": "string",
  "image2": "string"
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|image1|string|true|none|base64 encoded data|
|image2|string|true|none|base64 encoded data|

<h4 id="schemascoreresponse">ScoreResponse</h4>

```json
{
  "score": 0,
  "face_detects": []
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|score|number|false|none|none|
|face_detects|[[DetectResult](#schemadetectresult)]|false|none|none|

<h4 id="schemavalidationerror">ValidationError</h4>

```json
{
  "loc": [
    "string"
  ],
  "msg": "string",
  "type": "string"
}

```

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|loc|[anyOf]|true|none|none|

anyOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|string|false|none|none|

or

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|integer|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|msg|string|true|none|none|
|type|string|true|none|none|












## Inference (CPU)

## Matching