#Day4
#CSS 화면 표시 속성
>###1.화면 표시방법
>		display: block
		span{
			dislay: block;
		}
		span은 원래 인라인 속성 하지만 display 속성에서 block 속성 강제 부여
.	
>		
		display: inline
		div {
			display: inline;
		}
		반대로 div가 block 속성이지만, inline속성으로 강제 부여

.
>		display: inline-block
		기존 inline요소가 block요소와 같이 높이 상.하 값 가질 수 있음.
.
>		
		dispaly: none
		div {
			display: none;
		}
		화면에 완전히 보이지 않음
        
>###2. 화면 넘침 표시
>		div {
			overflow:auto; -> 콘텐츠가 넘칠경우, scroll
 			overflow:scroll; -> 콘테츠가 넘치지 않
			}

#CSS float 속성
####CSS로 요소를 띄운다.

>		float 속성은 중간에 이미지를 넣은 단락을 만들고자 하는 경우 사용.
		Element1이 block 요소라면, 해당 요소가 가로 너비를 모두 차지함.
		Element3을 float: right; 로 지정하면 Element1이 먼저 우측 공간도 
		차지하고 있으므로 Element2는 공간이 없으므로 
		Element1 다음 밑 공간의 우측으로 이동(float된 상태로) -> 
		그러면, Element3은 Element1 다음 밑 공간에서 우측도 차지함.
		Element2는 Element3의 우측 공간에서 float된 상태.
.
>	
		전체 block들을 float: right 하면, Element1부터 자례로 오른쪽부터 공간 
		차지함. 그렇게 이동하다가, 만약 부모 element보다 가로가 길어 오버되는 
		경우, 그 elemnt부터는 밑의 공간으로 이동하게 됨.
  .
  
#CSS Clear 속성
>		float요소과 겹치는 경우, float의 속성을 해제 할 수 있음.
		p {
		clear:both;
		clear:left;
		clear:right;
		} 
  .
#CSS float 레이아웃
###float 레이아웃
>		css로 레이아웃을 구현할 때는 float 속성을 자주 사용함.
  .
#CSS Position
###CSS 요소의 위치 설정

####position
>		**요소의 위치를 지정**
		**static** : 기본갑
		**relative**: static과 같은 순서로 배치, 
		but, 상/하/좌/우 속성을 이용해 위치 지정 가능
		**fixed**: 브라우저 창 기준으로 위치
		**absolute**: 자신과 가장 가까운 'position'이 static이 아닌 부모를 기준
.
>	
		relative position은 자신의 위치를 기준으로 정렬함.
		fixed는 표시영역을 기준으로 정렬
		(창 크기를 줄이거나 늘려도 항상 따라 다니는 요소)
		absolute요소가 참조할 부모가 없으면 body(브라우저)기준으로 정렬.
  
  .
#CSS 가운데 정렬
####css를 사용하여 레이아웃을 가운데 정렬하는 방법을 익히자
###가로 가운데 정렬

####1. 부모의 가운데로 정렬하는 법
>		
		width: 500px;
		margin: 0 auto;
		전체 크기가 정해져 있지 않을 경우, 내용의 woidth만 지정하고,
		좌/우 여백은 auto로 같게 지정한다.
####2. 부모의 가로/세로 가운데 정렬
>		
		height: 부모요소의 height
		line-height: 부모요소의 height
		width: 500px;
		margin:0 auto;
		부모요소의 height와 line-heght의 값이 같을 경우, 
		내부의 요소들은 세로 가운데로 정렬됨.
		
####3.  부모의 가로/세로 가운데 정렬
>		
		position: absolute;
		width:200px;
		height:100px;
		top:50%
		left:50%
		transform:translate(-50%, -50%)
		요소를 absolute position으로 설정한 뒤, 상단과 왼쪽에서 각각 부모의
		50%만큼 이동한 후,transform:translate(-50%,-50%)에 의해 자신의
		width와 height의 50%만큼을 외쪽과 위쪽으로 이동한다.