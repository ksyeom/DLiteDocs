# API Reference

> v1.9.11

## C Inferface

### CreateCURecognizer

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | void* CreateCURecognizer() | SDK의 인스턴스를 생성한다. 이후 모든 인터페이스를 호출할 때 포인터를 사용한다. |
| 리턴 값 | void* | 생성 된 SDK 포인터 |

### DisposeCURecognizer

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | void DisposeCURecognizer(void* pRecognizer) | CreateCURecognizer에서 생성한 SDK 포인터의 메모리를 해제한다. |
| 파라미터 | void* pRecognizer | CreateCURecognizer에서 생성 한 객체 포인터 |

### Init

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | bool Init(void* pRecognizer, void* root_dir, void* config_filepath) |  SDK를 초기화한다. |
| 파라미터 | void* pRecognizer | CreateCURecognizer에서 생성 한 객체 포인터 |
| 파라미터 | void* root_dir | SDK가 설치된 경로의 Root Path |
| 파라미터 | void* config_filepath | SDK  설정 값이 포함된 json파일 |
| 리턴 값 | bool | 초기화 성공 여부 |

### GetSDKVersion

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | ResultCode GetSDKVersion(void* pRecognizer, char* const buf, int buf_len) |  SDK의 버전을 조회한다. |
| 파라미터 | void* pRecognizer | CreateCURecognizer에서 생성 한 객체 포인터 |
| 파라미터 | char* const buf | 문자열을 받을 버퍼 |
| 파라미터 | int buf_len | 버퍼의 길이 |
| 리턴 값 | ResultCode | 성공 여부를 결과 코드로 리턴 |

### DetectFaceTopN

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | ResultCode DetectFaceTopN(void* pRecognizer, const char* bgrData, int w, int h, int type,
FaceExtractResult* csresult, int topN, int* outCnt) | 상위 N개의 얼굴 검출하고 결과를 즉시 리턴 한다. |
| 파라미터 | void* pRecognizer | CreateCURecognizer에서 생성 한 객체 포인터 |
| 파라미터 | const char* bgrData | BGR 이미지 데이터 |
| 파라미터 | int w | 이미지 너비 |
| 파라미터 | int h | 이미지 높이 |
| 파라미터 | int type | 이미지 타입 CV_8UC3 16 |
| 파라미터 | FaceExtractResult* csresult | 리턴할 결과값 - 임베딩은 포함안됨 |
| 파라미터 | int topN, int* outCnt | 검출할 상위 n개 |
| 파라미터 | int* outCnt | 실제 몇 개가 검출 되었는지 개수 |
| 리턴 값 | ResultCode | 성공 여부를 결과 코드로 리턴 |

### DetectFaceAtt

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | ResultCode DetectFaceAttr(void* pRecognizer, const char* bgrData, int w, int h, int type, float* attrScores, FaceAttribute attrib) | 얼굴의 특징을 검출 |
| 파라미터 | void* pRecognizer | CreateCURecognizer에서 생성 한 객체 포인터 |
| 파라미터 | const char* bgrData | BGR 이미지 데이터 |
| 파라미터 | int w | 이미지 너비 |
| 파라미터 | int h | 이미지 높이 |
| 파라미터 | int type | 이미지 타입 CV_8UC3 16 |
| 파라미터 | float* attrScores | 결과 점수 |
| 파라미터 | FaceAttribute attrib | 검출할 속성 |
| 리턴 값 | ResultCode | 성공여부를 결과코드로 리턴 |

### AlignCropFace

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | ResultCode AlignCropFace(void* pRecognizer, float* landmarks, int landmarksCnt, const char* bgrData, int w, int h, int type, char* alignedFaceData) | 랜드마크를 이용해서 112 크기의 Aligned 이미지를 만들어 낸다. |
| 파라미터 | void* pRecognizer | CreateCURecognizer에서 생성 한 객체 포인터 |
| 파라미터 | float* landmarks | 랜드마크 배열 포인터로 10개의 float |
| 파라미터 | int landmarksCnt | 랜드마크 개수로 10개 |
| 파라미터 | const char* bgrData | BGR 이미지 데이터 |
| 파라미터 | int w | 이미지 너비 |
| 파라미터 | int h | 이미지 높이 |
| 파라미터 | int type | 이미지 타입 CV_8UC3 16 |
| 파라미터 | char* alignedFaceData | 정렬된  112x112의 cv::Mat 형태의 BGR 이미지 |
| 리턴 값 | ResultCode | 성공여부를 결과코드로 리턴 |

### ExtractFace

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | ResultCode ExtractFace(void* pRecognizer, const char* bgrData, int w, int h, int type, char* embedding, int embedding_size, bool do_normalize = false) | 특징점 추출 |
| 파라미터 | void* pRecognizer | CreateCURecognizer에서 생성 한 객체 포인터 |
| 파라미터 | const char* bgrData | BGR 이미지 데이터 |
| 파라미터 | int w | 이미지 너비 |
| 파라미터 | int h | 이미지 높이 |
| 파라미터 | int type | 이미지 타입 CV_8UC3 16 |
| 파라미터 |  char* embedding | 추출된 특징점을 저장할 버퍼 |
| 파라미터 | int embedding_size | 특징점을 저장할 버퍼의 크기, 반드시 2048바이트이어야 함 |
| 파라미터 | bool do_normalize | 특징점을 노말라이즈 함 |
| 리턴 값 | ResultCode | 성공여부를 결과코드로 리턴 |

### DetectAndExtractTopN

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | ResultCode DetectAndExtractTopN(
void* pRecognizer,
const char* bgrData, int width, int height, int type,
FaceExtractResult* csresult, int topN, int* outCnt, bool do_normalize) | 특징점 추출하는데, 내부적으로 Detection -> Align -> Extraction 모든 수행
검출된 얼굴 중 Top N개의 얼굴의 특징점을 뽑아낸다. |
| 파라미터 | void* pRecognizer | CreateCURecognizer에서 생성 한 객체 포인터 |
| 파라미터 | const char* bgrData | BGR 이미지 데이터 |
| 파라미터 | int w | 이미지 너비 |
| 파라미터 | int h | 이미지 높이 |
| 파라미터 | int type | 이미지 타입 CV_8UC3 16 |
| 파라미터 | FaceExtractResult* csresult | 검출한 얼굴의 결과 값으로 특징점이 포함 |
| 파라미터 | int topN | 검출할 얼굴의 최대 개수 |
| 파라미터 | int* outCnt | 검출된 얼굴 개수 |
| 파라미터 | bool do_normalize | 특징점을 노말라이즈 함 |
| 리턴 값 | ResultCode | 성공여부를 결과코드로 리턴 |

### MatchFeature

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | float MatchFeature(void *pRecognizer, const char *srcFeature, int srcFeatureLen, const char *destFeature, int destFeatureLen) | 특징점 매칭 |
| 파라미터 | void* pRecognizer | CreateCURecognizer에서 생성 한 객체 포인터 |
| 파라미터 | const char *srcFeature | 특징점1 |
| 파라미터 | int srcFeatureLen | 특징점1의 길이로 2048로 고정 |
| 파라미터 | const char *destFeature | 특징점2 |
| 파라미터 | int destFeatureLen | 특징점2의 길이로 2048로 고정 |
| 리턴 값 | ResultCode | 성공여부를 결과코드로 리턴 |

### getDetectorInputWidth

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | int getDetectorInputWidth(void* pRecognizer) | FaceDetector의 입력 이미지 폭을 구함 |
| 파라미터 | void* pRecognizer | CreateCURecognizer에서 생성 한 객체 포인터 |
| 파라미터 | int | 입력 이미지의 폭 |
| 리턴 값 | int buf_len | 버퍼의 길이 |

### getDetectorInputHeight

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | int getDetectorInputHeight(void* pRecognizer) | FaceDetector의 입력 이미지 높이를 구함 |
| 파라미터 | void* pRecognizer | CreateCURecognizer에서 생성 한 객체 포인터 |
| 파라미터 | int | 입력 이미지의 높이 |
| 리턴 값 | int buf_len | 버퍼의 길이 |

### FaceAttribute

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| enum | FaceAttribute | 얼굴의 특징 |
|  | FA_BLUR | 이미지가 Blurry 한지 여부로 0~1 사이의 확률 값 |
|  | FA_FRONTAL | 얼굴이 정면을 향하는지 여부로 0~1 사이의 확률 값 |
|  | FA_SUNGLASS | 선그라스를 착용 여부로 0~1 사이의 확률 값 |
|  | FA_HAT | 모자를 착용했는지 여부로  0~1 사이의 확률 값 |

### ResultCode

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| enum | ResultCode | SDK 함수의 결과값을 리턴 |
|  | K_ERROR_INVALID | 유효하지 않는 값 에러 |
|  | K_SUCCESS | 성공 |
|  | K_ERROR_EMPTY_IMAGE | 이미지가 없음 |
|  | K_ERROR_FACE_NONE | 얼굴을 찾을 수 없음 |
|  | K_ERROR_LANDMARK_NONE | 랜드마크가 없음 |
|  | K_ERROR_LANDMARK_NOTMATCH | 랜드마크의 개수가 불일치 |
|  | K_ERROR_EMBEDDING_NONE | 특징점을 추출할 수 없음 |
|  | K_ERROR_EMBEDDING_BUFFER_NONE | 특징점 저장할 버퍼의 에러 |
|  | K_ERROR_PENDING_INIT | SDK  초기화 중 |
|  | K_ERROR_UNKNOWN | 알 수 없는 에러 |

---

## C++ Interface

### Init

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | bool Init(const std::string& root_dir, const std::string& config_filepath) |   SDK를 초기화 |
| 파라미터 | const std::string& root_dir | SDK가 설치된 경로의 Root Path |
| 파라미터 | const std::string& config_filepath | SDK  설정 값이 포함된 json파일 |
| 리턴 값 | bool | 초기화 성공 여부 |

### GetVersion

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | std::string GetVersion() |   SDK의 버전을 조회 |
| 리턴 값 | std::string | 버전 |

### DetectFace

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | cu::FaceROIs DetectFace(const std::vectorcv::Mat& frames) |  얼굴 검출 |
| 파라미터 |  std::vectorcv::Mat | bgr 이미지 |
| 리턴 값 | FaceROIs  | 검출된 영역 정보 |

### GetFaceCount

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | cu::Result<cu::FaceSDKError> GetFaceCount(size_t &count) | 마지막에 검출된 이미지에서 얼굴의 개수를 구한다. |
| 파라미터 | size_t &count | coutn 배열의 개수를 채움. |
| 리턴 값 | cu::Result<cu::FaceSDKError> | FaceSDKError 정보를 리턴. |

### GetFaceAt

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | cu::Resultcu::FaceSDKError GetFaceAt(size_t index, cu::Face** outFace) |  얼굴의 정보를 Index로 가져온다. |
| 파라미터 | size_t index | 배열의 index |
| 파라미터 | cu::Face** outFace | 결과 정보 |
| 리턴 값 | cu::Result<cu::FaceSDKError> | FaceSDKError 정보를 리턴. |

### DetectHat

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | float DetectHat(const cv::Mat& cropped_face) | 모자 착용 여부를 스코어로 측정한다. |
| 파라미터 | cv::Mat& cropped_face | 얼굴을 crop + align 한 이미지 |
| 리턴 값 | float | 0~1 사이의 스코어 |

### DetectSunglasses

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | float DetectSunglasses(const cv::Mat& cropped_face) |  Sunglasses 착용 여부를 스코어로 측정한다. |
| 파라미터 | const cv::Mat& cropped_face | cropped_face 얼굴을 crop + align 한 이미지 |
| 리턴 값 | float | 0~1 사이의 스코어 |

### DetectBlur

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | float DetectBlur(const cv::Mat& cropped_face) |  얼굴의 Blurry 정도를 측정한다. |
| 파라미터 | const cv::Mat& cropped_face | 얼굴을 crop + align 한 이미지 |
| 리턴 값 | float | 0~1 사이의 스코어 |

### DetectFrontal

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | float DetectFrontal(const cv::Mat& cropped_face) |  얼굴이 정면을 향하는지에 대한 스코어를 측정한다. |
| 파라미터 | const cv::Mat& cropped_face | 얼굴을 crop + align 한 이미지 |
| 리턴 값 | float | 0~1 사이의 스코어 |

### DetectSmartPhone

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | cu::ObjectBBoxes DetectSmartPhone(const cv::Mat& frame) |  스마트폰을 검출 |
| 파라미터 | const cv::Mat& frame | BGR 이미 |
| 리턴 값 | cu::ObjectBBoxes | Object 검출 정보 |

### ResetPassiveLiveness

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | void ResetPassiveLiveness() |  Passive Liveness를 초기화 |

### DetectPassiveLiveness

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | IPassiveLiveness::State DetectPassiveLiveness(const cv::Mat& cropped_face) |  PassiveLiveness 진행. |
| 파라미터 | const cv::Mat& cropped_face | 얼굴을 200x200 크기로 자른 사진 |
| 리턴 값 | IPassiveLiveness::State  |  |

### SetPassiveLivenessThresholds

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | void SetPassiveLivenessThresholds(float threshold0, float threshold1, float threshold2, float threshold3) |  Passive Liveness를 초기화 |
| 파라미터 | float threshold0 |  |
| 파라미터 | float threshold1 |  |
| 파라미터 | float threshold3 |  |

### AlignCropFace

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | void AlignCropFace(const cu::Landmark& landmark, const cv::Mat& face, cv::Mat& aligned_face) |  랜드마크 5개의 점을 이용하여 눈코입의 위치를 정규화된 위치로 변환하고 112 크기로 자른다. |
| 파라미터 | const cu::Landmark& landmark | 랜드마크 배열 포인터로 10개의 float |
| 파라미터 | const cv::Mat& face | BGR 이미지 데이터 |
| 파라미터 | cv::Mat& aligned_face | 정렬된  112x112의 cv::Mat 형태의 BGR 이미지 |

### ExtractFace

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | cv::Mat ExtractFace(const cv::Mat &face, bool do_normalize = false) |  특징점 추출 |
| 파라미터 | const cv::Mat &face | BGR 이미지 데이터 |
| 파라미터 | bool do_normalize = false | true일 경우 특징점을 노말라이즈 함 |
| 리턴 값 | cv::Mat | 특징점을 리턴, 512x1 행렬 |

### MatchFeature

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | float MatchFeature(const char* galleryFeature, const size_t galleryFeatureLen, const char* targetFeature, const size_t targetFeatureLen) |  두개 Feature의 유사도 비교 |
| 파라미터 | const char* galleryFeature | 특징점1 |
| 파라미터 | const size_t galleryFeatureLen | 특징점1의 길이로 2048로 고정 |
| 파라미터 | const char* targetFeature | 특징점2 |
| 파라미터 | const size_t targetFeatureLen | 특징점2의 길이로 2048로 고정 |
| 리턴 값 | float | 매칭 스코어 0~1. 1에 가까울 수록 동일 인물 |

### DetectAndExtractTopN

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | int DetectAndExtractTopN(const cv::Mat& frame, FaceExtractResults& results, int topN = 1, bool do_normalize = false) | 특징점 추출하는데, 내부적으로 Detection -> Align -> Extraction 모든 수행
검출된 얼굴 중 Top N개의 얼굴의 특징점을 뽑아낸다. |
| 파라미터 | const cv::Mat& frame | BGR 이미지 |
| 파라미터 | FaceExtractResults& results | 검출한 얼굴의 결과 값으로 특징점이 포함 |
| 파라미터 | int topN = 1 | 검출할 얼굴의 최대 개수 |
| 파라미터 | bool do_normalize = false | true일 경우 특징점을 노말라이즈 함 |
| 리턴 값 | int | 검출한 개수 |

### getDetectorInputWidth

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | size_t getDetectorInputWidth() const |  얼굴 검출 함수의 입력 이미지 폭 |
| 리턴 값 | bool | 얼굴 검출 함수의 입력 이미지 폭 |

### getDetectorInputHeight

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | size_t getDetectorInputHeight() const | 얼굴 검출 함수의 입력 이미지 높이  |
| 리턴 값 | size_t | 얼굴 검출 함수의 입력 이미지 높이 |

### getExtractorInputWidth

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | size_t getExtractorInputWidth() const | 추출 함수의 입력 이미지 폭  |
| 리턴 값 | size_t | 추출 함수의 입력 이미지 폭 |

### getExtractorInputHeight

| 구분 | 내용 | 설명 |
| --- | --- | --- |
| 함수 | size_t getExtractorInputHeight() const | 추출 함수의 입력 이미지 높이 |
| 리턴 값 | size_t  | 추출 함수의 입력 이미지 높이 |