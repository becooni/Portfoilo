# Portfolio

# Index
- [11번가](#11번가)
- [트라이어스앤컴퍼니](#트라이어스앤컴퍼니)
- [에이앤피알](#에이앤피알)

# [11번가](https://11st.co.kr)
*국내 대형 e-commerce 서비스*


기간 | 업무 | 기술
--- | --- | ---
2021.5 ~ 재직중 | '11번가' Android App 개발 및 앱 개발 파트 리드</br>상품상세, 리뷰작성 서비스 고도화 개발 | Kotlin</br>MVVM</br>MVI</br>RxJava</br>Retrofit</br>Jetpack LiveData, ViewModel, ViewBinding, KTX

[11번가 Android 앱 다운로드 링크](https://play.google.com/store/apps/details?id=com.elevenst)

## App 데모

### 상품 상세

ATF 영역 | 상품 이미지 | 상품 리스트
--- | --- | ---
<img src="https://github.com/becooni/portfolio/assets/5853404/e5de16e6-6c58-4b07-8398-137aee5c2a4d" width="300px"> | <img src="https://github.com/becooni/portfolio/assets/5853404/24726ff5-4c69-4cac-af8e-dcf28849557d" width="300px"> | <img src="https://github.com/becooni/portfolio/assets/5853404/248ebe26-5de3-4612-8632-85faeb22c904" width="300px">

- Vertical RecyclerView로 구성된 화면
- 블럭 단위로 구성 (1 블럭 = 1 ViewHolder)
- 상품상세 서버 api로 하나의 통 데이터를 얻어와 각 블럭마다 필요한 데이터를 제공해주고 블럭에서 UI 구현
- 필요에 따라 비동기로 블럭 지연 초기화 (스크롤이 해당 블럭에 도달하기 직전 api 호출 후 UI 초기화)

---

최대할인가 | 리뷰 필터
--- | ---
<img src="https://github.com/becooni/portfolio/assets/5853404/e8995517-7c0c-48ac-883c-34ecea712ba2" width="300px"> | <img src="https://github.com/becooni/portfolio/assets/5853404/2b485314-71e5-4f07-a83a-41bb46aaa645" width="300px">

<img src="https://github.com/becooni/portfolio/assets/5853404/9fa38dad-5c12-4429-989b-db39d74077c6" width="400px">

- Generic과 enum을 활용한 Multi-ViewType RecyclerView, Gson, BottomSheetDialogFragment
- org.json.JSONObject (map) 타입으로 데이터를 관리하던 코드를 model 클래스로 전환 (Domain, UiState class)
- 트리 구조의 데이터를 flat한 데이터로 변경하여 하나의 RecyclerView에서 Multi-ViewType 제공
- RecyclerView.ItemDecoration을 활용한 StickyHeader 구현

---

**옵션**

<img src="https://github.com/becooni/portfolio/assets/5853404/c767aa62-699a-4d31-a62d-dd0f7ca48e27" width="300px">

- Horizontal RecyclerView
- 옵션 변경 시 페이지는 유지하고 데이터만 변경
- 품절 상품 선택 시 재입고 알림 기능
- 애플케어 등 추가 구성 상품 기능

### 구매서랍

<img src="https://github.com/becooni/portfolio/assets/5853404/ab80e32d-8a65-492f-9d1b-3139f9b0dc96" width="300px">

- 상품 추가/제거 기능
- 수량 증감/입력 기능
- 수량 변경 시 제약 검사 기능
- 상태 변경(상품, 수량)시 쿠폰가격 갱신 기능
- 선물하기/주문서/장바구니 담기 기능
- 주문서 대기열 큐(NetFunnel) 기능

<img width="800" alt="image" src="https://github.com/becooni/portfolio/assets/5853404/8ebf6612-a057-4a8b-8d9a-736b46951f3f">

- Android 앱 아키텍처, MVI, UDF, SSOT을 적용한 구조 설계
  RxJava, Jetpack LiveData/ViewModel, BottomSheetDialogFragment
- 데이터가 변경될 때 영향 받는 UI 들을 UiState 단위로 그룹핑
- event를 통해서만 UiState를 변경할 수 있음
- StateMachine은 ViewModel로 부터 전달 된 event를 받아 적절한 일을 수행하고 UiState를 방출함 (StateMachine은 개념적 표현이며 실제로는 Repository -> UseCase -> ViewModel로 처리)
- 앞서 StateMachine에서 방출한 UiState를 구독하던 View가 데이터 변경을 감지하고 UI를 갱신함
- UiState에 영향이 없고 비즈니스 로직 없이 스스로 처리할 수 있는 이벤트는 View에서 스스로 처리함 예) 팝업 닫기, 하드코딩 메세지 토스트 등
- UiState에 영향이 없지만 비즈니스 로직이 필요하고 View 로직이 필요한 시나리오는 Effect로 처리 예) 화면 이동, 서버 응답 오류 얼럿 메세지, 상품 찜하기 하트 애니메이션 재생 등
- View 파일 하나에 모든 코드가 있는 레거시 코드 리팩토링
- org.json.JSONObject (map) 타입으로 데이터를 관리하던 코드를 model 클래스로 전면 전환 (Domain, UiState class)
- 전략 패턴을 활용하여 유저가 구매수량을 변경할 때 실행되는 제약을 구현 (수량 증가/감소/직접 입력할 때 최소/최대/재고 수량과 묶음(배수) 수량 제약 등을 검사)

### 리뷰 작성

- MVVM
- Livedata
- Jetpack ViewModel

메타데이터 입력 1 | 메타데이터 입력 2
--- | ---
<img src="https://github.com/becooni/portfolio/assets/5853404/d0b13285-9b1b-424f-adaa-d6da4aab4308" width="300px"> | <img src="https://github.com/becooni/portfolio/assets/5853404/d6108e09-a302-4426-8731-c3e983450045" width="300px">

- RadioButton, CheckBox, Spinner, Calendar 기능
- MediatorLiveData를 활용한 입력 데이터 유효성 검사 기능 (입력 항목 모두 선택이 완료되면 완료 표시)

별점 | 작성 | 첨부
--- | --- | ---
<img src="https://github.com/becooni/portfolio/assets/5853404/5019e841-8b90-4b2a-b952-b1515f929b9f" width="300px"> | <img src="https://github.com/becooni/portfolio/assets/5853404/d089df27-0ab2-46bb-9014-abfc9733587c" width="300px"> | <img src="https://github.com/becooni/portfolio/assets/5853404/c641321c-53fd-4590-ad46-654ed38b2cfb" width="300px">

- 작성 화면을 이탈할 때 (onStop 시점) 현재 선택된 별점 저장하는 기능
- MediatorLiveData를 활용한 입력 데이터 유효성 검사 기능 (각 항목 모두 유효한 입력일 때 저장 가능)
- 정규표현식을 활용한 작성글 유효성 검사

---

# [트라이어스앤컴퍼니](http://umsun.co.kr/)

## [엄선](https://play.google.com/store/apps/details?id=com.umsun.application)

*온라인 시식 커머스&리뷰, 가공식품 첨가물&성분 정보 서비스*

기간 | 인원 | 나의 역할 | 사용 기술
--- | --- | --- | --- 
2018.7 ~ 2020.12 | Android 1 </br> iOS 2 </br> Server 1 |  안드로이드 App 99% 담당 </br> App 서비스 고도화 & 유지보수 </br> Java -> Kotlin 90% 전환 </br> MVVM + RxKotlin 리팩토링 </br> Restful Api 설계 </br> |  Kotlin </br> MVVM </br> Clean Architecture </br> RxKotlin </br> JetPack - LiveData, ViewModel, DataBinding </br> Rest Api </br> ExoPlayer </br> 

~~앱 다운로드 링크 - https://play.google.com/store/apps/details?id=com.umsun.application~~
현재 사업 종료로 서비스 중단

## App 시연 이미지

### 회원가입

- 소셜 로그인
- 유저 프로필 정보 입력/수정
- 유저의 자녀 정보 입력/수정

로그인 | 프로필 입력
 --- | ---
 <img src="https://user-images.githubusercontent.com/5853404/109418645-dcf25f80-7a0c-11eb-8c9d-78ac58ea8aec.png" width="300px"> | <img src="https://user-images.githubusercontent.com/5853404/109419324-2e501e00-7a10-11eb-8510-0e87f7a9fb06.gif" width="300px">

### 시식 커머스

- TabLayout+ViewPager을 사용한 시식 제품 리스트 구현
- 온라인 무료시식 신청 / 유료시식 결제 기능 구현
- 신청 현황 리스트, 구매 및 결제 취소 기능 구현
- 상품 open 카운트 다운 기능 구현
- 시식 후기 SNS 리뷰 / 설문(객관식,주관식) 기능 

시식 리스트 | 시식 신청 | 신청 현황 
--- | --- | ---
<img src="https://user-images.githubusercontent.com/5853404/109419545-57bd7980-7a11-11eb-887d-6cc903cb07be.gif" width="300px"> | <img src="https://user-images.githubusercontent.com/5853404/109419561-6efc6700-7a11-11eb-8ffc-e99a4edb386d.gif" width="300px"> | <img src="https://user-images.githubusercontent.com/5853404/109419582-850a2780-7a11-11eb-998a-d9b8fd492545.gif" width="300px">

### 리뷰

- 미디어(사진+영상) 리뷰, 댓글, 대댓글 CRUD 구현
- ExoPlayer 영상 재생
- 스크롤 하면 재생중이던 영상이 중지되는 기능 구현
- 업로드용 사진 변환시 병렬처리를 통해 실행시간 감소 (by RxKotlin)
- 업로드 사진 도용 검증

리뷰 리스트 | 리뷰 작성
--- | ---
<img src="https://user-images.githubusercontent.com/5853404/109421104-49735b80-7a19-11eb-92bd-39844b0eb426.gif" width="300px"> | <img src="https://user-images.githubusercontent.com/5853404/109420844-d7e6dd80-7a17-11eb-9bc0-bb224face588.gif" width="300px">

### 식품 정보

- 카테고리 리스트 구현
- 상품정보 공유 카카오링크 구현

 식품 리스트 | 식품 상세
--- | ---
<img src="https://user-images.githubusercontent.com/5853404/109420891-34e29380-7a18-11eb-9ffc-c28f2266696c.gif" width="300px"> | <img src="https://user-images.githubusercontent.com/5853404/109421054-02856600-7a19-11eb-930a-97cd08cd52a1.gif" width="300px">

### 커뮤니티

- 유저 커뮤니티 글, 댓글, 대댓글 CRUD 기능 구현
- 댓글, 대댓글, 좋아요 등 유저반응 Notification 클릭시 해당 댓글로 이동하는 DeepLink 구현 (like 인스타그램)

톡톡 리스트 | 톡톡 상세 | 톡톡 작성
--- | --- | ---
<img src="https://user-images.githubusercontent.com/5853404/109421543-277ad880-7a1b-11eb-82ed-17b92339ddd2.gif" width="300px"> | <img src="https://user-images.githubusercontent.com/5853404/109421547-2a75c900-7a1b-11eb-9216-03616310cecc.gif" width="300px"> | <img src="https://user-images.githubusercontent.com/5853404/109421548-2ba6f600-7a1b-11eb-95ac-401d176354c3.gif" width="300px">

### 별점

- 가공 식품에 대한 경험을 평가하는 기능
- 평가 항목들을 리스팅

평가 | 리스트
--- | ---
<img src="https://user-images.githubusercontent.com/5853404/109422334-7a09c400-7a1e-11eb-9abb-344305cf2630.gif" width="300px"> | <img src="https://user-images.githubusercontent.com/5853404/109422545-585d0c80-7a1f-11eb-9c0b-71711484107b.gif" width="300px">

### 포인트

- 일일 출석체크 기능 구현
- 출석체크 달력 구현
- 포인트 내역

출석체크 | 포인트 내역
--- | ---
<img src="https://user-images.githubusercontent.com/5853404/109421933-c227e700-7a1c-11eb-83ff-abfa88437369.gif" width="300px"> | <img src="https://user-images.githubusercontent.com/5853404/109421938-c8b65e80-7a1c-11eb-92f1-b421bb6ecf65.gif" width="300px">

---

# 에이앤피알
*배달 음식 주문/관리 서비스*

기간 | 업무 | 기술
--- | --- | ---
2014.10 ~ 2018.06 | '배달캐시큐', '배달톡톡', '톡톡메시지', '피알메시지' Android App 개발 | Java, MVP, Volley, Retrofit, ButterKnife, SQLite

## 배달캐시큐, 배달톡톡

<img width="400" alt="image" src="https://github.com/becooni/portfolio/assets/5853404/24944586-cdfe-4f8b-9444-1d324cd8af03">
<img width="400" alt="image" src="https://github.com/becooni/portfolio/assets/5853404/6f3212f2-afb6-43b4-a671-8ab877cd0e4c">

- 위치기반 배달 음식점 리스트 정보 제공 기능
- GPS 정보를 가져와 한글 주소로 변환하여 표시
- Google Maps v2로 지도 제공
- 장바구니, 주문, 결제 기능
- 쿠폰/포인트 할인 기능
- 주문 내역 기능
- 주문 수락 시 FCM push 수신
- 리뷰 작성 기능 (별점, 쓰기, 수정, 카메라 촬영 및 사진 업로드)
- 음식점 메뉴를 보며 주문할 수 있도록 주문 전화를 걸때 메뉴 전단지 이미지 노출 (Service 활용)
- 매장 이름과 전화번호를 주소록 자동 저장

### 사장님 앱
- 주문 수락, 거절 기능
- 영업 개시/종료 기능
- 주문 발생 시 FCM push 수신

## 톡톡메시지, 피알메시지

<img width="300" alt="image" src="https://github.com/becooni/portfolio/assets/5853404/d8a6f57d-035e-4b81-ac01-605780189dff">

<img width="400" alt="image" src="https://github.com/becooni/portfolio/assets/5853404/af3a9b5a-ea29-4a99-9dcf-4743b8b39e5f">

- Nokia MMS Open Source를 활용하여 통화 발신/수신 후 MMS를 자동으로 발신하는 기능
- 통신사 별 MMS 규약
- 앱을 설치할 수 없는 전화는 CID 장비(발신자표시장치) 혹은 KT OPEN API를 이용하여 발신자 번호를 서버로 수집 -> 안드로이드 앱에 FCM으로 전달
- 로컬 DB에 SMS/MMS 발송 기록을 저장하고 체크하여 MMS 발신을 제한함 (통신사 별 발송 제약)
- MMS 발송 내역 기능
- 동일 고객 중복발송 제한 기간 기능
- 발송 요일 지정 기능

