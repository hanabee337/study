### H/W : 2017.02.20
0. 유저 모델에 img_profile 필드 추가, migrations
1. change_profile_image.html 파일 작성
2. ProfileImageForm 작성
3. 해당 Form 템플릿에 렌더링
4. request.method == 'POST' 일 때, 
request.FILES의 값을 이용해서 request.user의 img_profile을 변결, 저장
5. 처리 완료 후, member:profile로 이동
6. progile.tml에서 user의 프로필 이미지를 img태그를 사용해서 보여줌. {{ MEDIA_URL }}을 사용함.

### H/W : 2017.02.21 
1. video app을 생성하고
2. 유튜브 영상의 정보를 저장할 수 있는 Model 구현, Migration
3. POST 요청을 받으면 요청에서 온 키워드로 유투브를 검색 후, 결과를 DB에 저장하는 View 구현
4. 위 View를 나타낼 수 있는 Template 구현
5. View와 Template연결
6. 실행해 보기

### 실습 내용 -2017.02.22 
### AbstractUser를 상속받아 CustomUser구현
1. member app생성
2. AbstractUser를 상속받은 MyUser를 생성
3. AUTH_USER_MODEL에 등록
4. 마이그레이션 해본다
**extra
5. Django admin에 MyUser를 등록
6. 기본 UserAdmin을 상속받아 사용자 관련 모듈이 잘 작동하도록 설정
    (기본값으로 두면 패스워드 해싱등이 동작하지 않음)

### search view의 동작 변경
1. keyword로 전달받은 검색어를 이용한 결과를 데이터베이스에 저장하는 부분 삭제
2. 결과를 적절히 가공하거나 그대로 템플릿으로 전달
3. 템플릿에서는 해당 결과를 데이터베이스를 거치지 않고 바로 출력

### Next, Prev버튼 추가
1. Youtube Search API에 요청을 보낸 후, 결과에
    1-2. nextPageToken만 올 경우에는 첫 번째 페이지
    1-3. 둘다 올 경우에는 중간 어딘가
    1-4. prevPageToken만 올 경우에는 마지막 페이지 임을 알 수 있음
2. 템플릿에 nextPageToken, prevPageToken을 전달해서
    해당 token(next또는 prev)값이 있을 경우에 따라
    각각 '다음' 또는 '이전' 버튼을 만들어 줌


### H/W : 2017.02.22
1. 북마크 기능을 만든다.
   검색 결과의 각 아이템에 '북마크하기'버튼을 만들어서 누르면 DB에 저장
2. 북마크 목록 보기 페이지를 만든다.
   북마크한 영상 목록을 볼 수 있는 페이지 구현
**extra
3. 사용자 별로 북마크를 구분할 수 있도록 한다.
4. 검색 결과에서 이미 북마크를 누른 영상은
   '북마크 되어있음' 또는 '북마크 해제'버튼이 나타나도록 한다.
5. 북마크 목록에서 해당 아이템을 클릭 할 경우 유튜브 페이지로 이동하지 않고,
   자체 video_detail페이지를 구현해서 보여주도록 한다.
6. 그외 넣고싶은 기능 마음껏 넣어보기
7. 또는 CSS로 반응형 모바일 만들어보기
8. 로그인/회원가입 만들기