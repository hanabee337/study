##Pair Programming 3(2017.02.22)

####Part1
1. 가상환경을 설정하고, git repository를 만듭니다. ( .gitignore 생성 ) 적절하게 커밋.
2. 기본환경 세팅 (한국 시간, 한국어, 정적 파일 위치, 템플릿 폴더 위치)
3. runserver를 통해 It worked를 확인합니다.

####Part2
1. youtube data api 홈페이지로 들어가 api key를 가져온다.
2. .conf 폴더를 만들고 API key를 json 파일에 넣어준다.
3. video app을 생성하고 json파일을 이용하여, 구글 API를 호출한다. (임의의 q를 넣어줌)
4. 호출한 json 정보를 제목, 내용, 영상으로 list view를 만듭니다.

####Part3
1. GET요청시에는 검색 input이 하나 있는 페이지를 단순 render
2. POST요청으로는 keyword 또는 q라는 이름으로 검색키워드 정보를 전달
3. 전달받아온 키워드를 이용해 유튜브 검색 API실행
4. 저장되어있는 모든 데이터를 템플릿에 전달

####Part4
1. 유튜브 영상의 정보를 저장할 수 있는 Model구현, Migrations
2. POST요청을 받으면 요청에서 온 키워드로 유튜브를 검색 후 결과를 DB에 저장하는 View구현
3. Model에 저장해놓은 list를 보여주는 View 구현