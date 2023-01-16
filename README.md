■ 컨셉
- 로그인, 로그아웃, 회원가입 기능 구축, 페이지 디자인
- 메인페이지 디자인 및 레퍼런스 확인, 백엔드 & 프론트엔드 구축
- 세부 페이지 코멘트 기능 구축, 수정 기능 구축
- 와이어 프레임 디자인, 글꼴 및 메인 컬러 & 서브 컬러 선정
- 로고 디자인, 메인컬러 선정, 프로젝트 네임 선정

■ 세부사항
- JWT방식으로 토큰발행하고 쿠키로 저장하는 방식을 통해  로그인 상황 유지 구현
- hashlib 을 이용한  pw 암호화 그리고 pw암호를 이용한 로그인 기능 구현 
- 책 도서 리뷰 등록, 수정 기능 구현 - 현재 등록 기능은 구현/ 수정기능은  api가 있으나 font-end 에서 미구현
- 책 상세보기 페이지를 통해 저장된 책 데이터를 db를 통해 보여주기 기능 구현
- 책 상세보기 페이지에서 댓글기능 구현
- 등록된 도서를 최신순으로 좌측 상단에서부터 차례대로 나열
- 등록된 도서 중 상대적으로 높은 좋아요를 받은 4개의 도서를 페이지 최상단에 고정하여 노출
- 반응형 웹을 고려하여 페이지의 폭에 따라 유동적으로 반응할 수 있도록 CSS를 구성
- HTML구성 시 웹표준에 맞출 수 있도록 h태그와 p태그를 구분하여 사용

■ api 명세서
로그인	post	/api/logIn	userId(string), userPassword(int)-pwHash	유저의 아이디와 암호화한 비밀번호를 확인하여 로그인과 토큰 발행을 한다. 

회원가입	post	/api/register	userNumber(int), userId(string), userPassword(int), userNickName(string)	새로운 유저를 등록한다. 
각 파라미터는 
userId : 유저의 고유아이디
userPassword: 유저의 비밀번호
userNickname : 유저의 고유 닉네임
userNumber: 등록한 순서 순으로 부여된다. 

로그인 유지	get	/api/valid	userId(string), userNickName(string)	유저가 로그인 하면 토큰이 발행되고 그것을 쿠키로 저장한다. 해당 쿠키를 확인하고 로그인상태를 유지한다. 

메인페이지	get	/api/book/list		

책 세부페이지 등록	post	/api/book/register	bookIdGive(int)
bookTitleGive(string)
bookAuthorGive(string)
bookThumbnailGive(string)
bookPublisherGive(string)
bookSummeryGive(string)	새로운 책을 등록한다
각 파라미터는
bookIdGive: 등록한 책의 고유 id. 등록한 순서에 따라 차례대로 오름차순으로 +1씩 증가함
bookTitleGive: 책의 제목
bookAuthorGive: 책의 저자
bookThumbnailGive: 책의 표지
bookPublisherGive: 책의 출판사
bookSummeryGive: 책의 개요

책 세부페이지 수정	post	/api/book/modify	bookTitleGive(string)
bookAuthorGive(string)
bookThumbnailGive(string)
bookPublisherGive(string)
bookSummeryGive(string)	bookTitleGive : 책의 제목
bookAuthorGive : 책의 저자
bookThumbnailGive : 책의 표지
bookPublisherGive : 책의 출판사
bookSummeryGive : 책의 개요

책 세부페이지	get	/api/book/detail	bookId(int)	책의 상세 정보 호출, 책에 달리는 댓글도 같이 추가

댓글 등록	post	/api/comment	bookId(int), comment(string)	jwt로 유저아이디를 받아와서 해당 책에 관한 댓글을 추가

대댓글 등록	post	/api/comment	commentId(int), comment(string)	댓글에 대한 대댓글 기능

댓글 삭제	delete	/api/comment	commentId(int)	댓글을 삭제하고 부모 댓글이면 자식댓글들도 일괄 삭제

댓글 목록	get	/api/comment/list	bookId(int)	책에 달린 댓글 목록

아이디 중복체크	post	/idcheck	userId(string)	회원가입 시 다른유저와 아이디 중복이 되지않게하기 설정

닉네임 중복체크	post	/ninkcheck	userNinkName(string)	회원가입 시 다른유저와 닉네임 중복이 되지않게하기 설정
