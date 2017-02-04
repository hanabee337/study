###5일차
####Lesson 내용
1.다방앱 - footer 만들기
2.반응형


#### 다방앱 - footer 만들기 순서
윗줄 아랫줄 먼저 만들고
ul를 좌측 맨아래로 세로로 오게 만들고
그 다음 float: left 정렬
list가 붙어 있으므로 서로 띄우는 작업
margin: 0 auto; -> float된 리스트들을 가운데 정렬
각 리스트들이 꽉 차도록 display: inline-block 으로 설정, width=100%
list가 윗줄에 붙어 있으므로 line-height 설정해서 가운데 정렬
 float된 list들이 width를 넘치게 됨 -> box-sizing; boder-box 설정

inline-block으로 설정해서  위아래를 맞춤.
부모 요소가 height가 설정되어 있지 않으면, 자식 요소가 position:relative가 안먹음.
