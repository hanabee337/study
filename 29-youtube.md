# YouTube App 만들기

### API키 작성
1. 소개문서 읽기
	- [YouTube API 시작하기](https://developers.google.com/youtube/v3/getting-started)

2. API콘솔에서 프로젝트 생성
	- [API Console](https://console.developers.google.com/iam-admin/projects)

3. 상단 왼쪽 Google APIs이미지 누르고
	- **YouTube Data API** 선택
	- 사용설정 클릭

4. 사용자 인증 정보 작성
	- 좌측 사용자 인증 정보 클릭
	- 사용자 인증 정보 만들기 -> API 키 선택
	- 생성된 API키 확인

### 클라이언트 라이브러리 설치
1. 좌측의 클라이언트 라이브러리 (English) 클릭
[https://developers.google.com/youtube/v3/libraries](https://developers.google.com/youtube/v3/libraries)

2. Google API Client Library for Python선택
[https://developers.google.com/api-client-library/python/](https://developers.google.com/api-client-library/python/)

```python
pip install --upgrade google-api-python-client
```
- 위의 것을 설치해야 json이 지원되는 듯

### API요청법 파악
1. APIs Explorer로 가상요청 보내기 (Execute without OAuth선택)
[https://developers.google.com/apis-explorer/](https://developers.google.com/apis-explorer/)

2. [Youtube Search API Test](https://developers.google.com/apis-explorer/#p/youtube/v3/youtube.search.list)

3. Request의 URL과 Response데이터 확인(postman)
