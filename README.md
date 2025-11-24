# 202130129
## 전진영

## 1119 수업내용
### Global CSS
* 전역 CSS를 사용하여 응용 프로그램 전체에 스타일을 적용할 수 있습니다.

* app/global.css 파일을 만들고 루트 레이아웃으로 가져와 애플리케이션의 모든 경로에 스타일을 적용합니다.

* RootLayout은 앞에서 작성한 것과 동일합니다.

### 알아두면좋아요
* 전역 app 스타일은 디렉토리 내의 모든 레이아웃, 페이지 또는 검포년트로 가져올 수 있습니다.
그러나 Next.js는 스타열시트에 대한 React의 기본 제공 지원을 사용하여 Suspense와 통합하기 때문에 현재
충돌로 이어질 수 있는 경로 사이를 탐색할 때 스타일시트가 제거되지 알습니다.

진정한 글로벌 CSS(예: Tailwind의 기본 스타일)에는 전역 스타일을 사용하고, 컴포년트 스타일링에는
Tailwind CSS, 필요한 경우 사용자 정의 CSS에는 CSS 모듈을 사용하는 것이 좋습니다.

### Bootstrap 실습
* Blog2Page에 Bootstrap을 import하지 않아도 사용할 수 있습니다.

이것은 Blog2Layout에 import하는 것 만으로 해당 디렉토리 및 하위 디렉토리 전체에
사용이 가능하기 때문입니다.

이제 local Layout이 어디까지 영향을 미치는지 확인해 보겠습니다.

다음 컴포넌트에서는 Bootstrap의 Alerts중 하나를 사용하고, 내용에는 컴포넌트의 경
로를 출력해서 확인하기 좋게 합니다.

/blog2/Blog2Com.tsx 컴포넌트를 만들고 출력을 확인해 보세요.

/blog2/components/Blog2Com2.tsx 컴포넌트를 만들고 출력을 확인해 보세요.

/components/Blog2RootCom.tsx 컴포넌트를 만들고 출력을 확인해 보세요.

blog3 페이지를 만들고, 지금까지 만든 컴포넌트를 추가해 줍니다.

/blog3/Blog3Com.tsx 컴포넌트를 만들고 blog3 페이지에 삽입해 줍니다.

## 1112 수업내용
### 스트리밍
* 경고(Warning): 아래 내용은 애플리케이션에서 cacheComponents. config_옵션이 활성화
되어 있다고 가정합니다. 이 플래그는 Next.js 15 Canary에서 도입되었습니다.
* Next.js의 별칭은 latest과 canary 두가지가 있습니다. latest는 현재 가장 최신 안
정 버전, canary는 안정화 직전의 최신 개발 버전을 의미합니다.

* 서버 컴포넌트에서 async/await를 사용하는 경우 Next.js는 동적 렌더링을 선택합니다.

* 즉, 모든 사용자 요청에 대해 서버에서 데이터를 가져와서 렌더링합니다.

* 데이터 요청 속도가 느린 경우, 모든 데이터를 가져올 때까지 전체 경로의 렌더링이 차
단됩니다.

* 초기 로드 시간과 사용자 경험을 개선하려면 스트리밍을 사용하여 페이지의 HTML을 더
작은 단위의 블록으로 나누고, 점진적으로 서버에서 클라이언트로 해당 블록을 전송할
수 있습니다.

### 스트리밍 loading.tsx를 사용하는 방법
* 1. loading.tsx 파일로 페이지 감싸기
* 2. <Suspense>로 컴포넌트를 감싸기

* 데이터를 가져오는 동안 전체 페이지를 스트리밍하려면, page와 같은 디렉토리에 loading.tsx 파일을 생성 합니다.
* 예를 들어, app/blog/page.tsx를 스트리밍하려면, app/blog 디렉토리 안에 loading.tsx 파일을 추가하면 됩니다.

### 순차적 데이터 fetch
* 트리 구조 내 중첩된 컴포넌트 각각이 자체 데이터를 가져올 때 중복 요청이 제거되지 않으면 순차적 데이터 가져오기가 발생하며, 이로 인해 응답 시간이 길어집니다.

* 한 번의 fetch가 다른 하나의 fetch 결과에 따라 달라지는 경우 이 패턴이 필요할 수 있습니다/
* 예를 들어, <Playlists> 컴포넌트는 <Artist> 컴포넌트가 데이터 fetch를 완료한 후에 데이터를 fetch를 시작합니다.
* 그 이유는 <Playlists>가 artlistID prop에 따라 달라지기 때문입니다.

### 문서 코드 수정 및 lib 생성
* page에서 Suspense, getArtist, getArtistPlaylists를 import 합니다.

* getArtist(username) 생성 합니다.
: username으로 users 조회 → 첫 결과를 반환(id, name), 없으면 예외 발생합니다.

* getArtistPlaylists(artistID) 생성 합니다.
: artistID(userId)로 albums 조회 → [{id,name}, .] 배열을 반환합니다.

* Next.js 서버 환경에서 fetch를 사용하므로 page.tsx에서 await/비동기 호출로 바로 사
용 가능합니다.

* URL 세그먼트는 /artist/Bret와 같이 호출합니다.

* Link도 레이아웃에 추가해 줍니다. RootLayout과 PageLayout 모두 생성해 보세요.

## 1029 수업내용
* ThemeContext.Provider는 무엇일까요?
- createContext 함수를 호출하면, React는 Context 객체 하나를 만들어줍니다.
- 이 객체 안에는 여러가지 속성이 있는데, 대표적인 것이 다음 두 가지가 입니다.
- ThemeContext.Provider,IhemeContext.Consumer입니다.
- 즉, Provider는 createContext()를 호출하면 자동으로 생성되는 React 컴포넌트입니
다. line28


 따라서 ThemeContext.Provider 컴포넌트에 현재 theme state와 함께 toggleTheme 함수
도 함께 props로 전달합니다. line28
→ 즉, 하위 컴포넌트에서는 현재 theme state를 알 수 없기 때문에 버튼 쪽으로
toggleTheme 함수와 함떼 theme state를 함께 전달하는 것입니다.
* Context provider
Provider component를 트리에서 가능한 한 깊숙이 렌더링해야 합니다.
T
• ThemeProvider가 전체 <html> 문서 대신 {children}만 래핑하는 방식을 주목하세요.

• 이렇게 하면 Next.js가 server component의 정적 부분을 더 쉽게 최적화할 수 있습니다.

### 외부 서드파티 실습

* 오류 수정 후에도 동작은 하지만 이미지가。 첫 페이지에 모두 출력되어 정상 동작이라고 :
할 수는 없습니다.

* 이유는 acme-carousel에서 제공하는 style이 적용되지 않아서 입니다.

* style은 node_modules/acme-carousel/dist/styles.css 경로에 있지만, 이렇게 특정 모
듈에 있는 스타일을 사용할 경우 global.css에 import해서 사용하는 것이 일반적 입니
다.

@import 'acme-carousel/dist/styles.css';
→ 하지만 이번 경우에는 acme-carousel의 특성 때문에 오류가 발생합니다.

* 이런 경우라면 스타일을 components/에 복사해서 사용합니다. 위치는 다른 곳이라도 상
관 없습니다.
→ gallery.tsx에 import './styles.css' 을 추가 합니다.

### 환경 변수 노출 예방
* JavaScript 모듈은 server 및 client component 모듈 간에 공유될 수 있습니다.
* 이 말의 의미는 실수로 server 전용 코드를 client로 가져올 수도 있습니다.

## 1017 수업내용
* server 및 client component를 언제 사용해야 하나요?
  * 예를 들어, <Page> component는 게시물에 대한 데이터를 가져와서, client 측 상호 작용을 처리하는 <LikeButton>에 props로 전달하는 sever component입니다.
  * 그리고, @/ui/like-button은 client component이기 때문에 use client를 사용하고 있습니다.

* isLiking state의 주요 역할
  * 중복 클릭 방지 : isLiking이 true인 동안은 버튼을 disabled로 만들어 중복 요청 즉 중복 낙관적 업데이트를 막는 역할을 합니다.
  * UI 피드백 : 로딩 상태 표시를 위해 사용이 가능합니다
  * 상태 안정화 : 서버에 요청이 끝날 떄까지 추가 상태 변경을 잠시 멈추게 해서, 일관된 동작을 보장합니다.
* Null 병합 연산자
  * 왼족 피연산자가 null 또는 undefined이면 오른쪽 값을 반환하고, 그렇지 않으면 왼쪽 값을 그대로 반환합니다.
  -> 즉 likes의 값이 mull이나 undefined이면 0을 반환하고, 값이 있으면 그 값을 그대로 반환합니다
  * or 연산자( || )와는 어떤 차이가 있을까?
  * or 연산자는 falsy 값을 전부 오른쪽 값으로 대체합니다.
*Next.js에서 server와 client component는 어떻게 작동합니까?
  * server에서 Next.js는 React의 API를 사용하여 렌더링을 조정합니다.
  * 렌더링 작업은 개별 라우팅 세그먼트 별 묶음 으로 나뉩니다
* React Sever Component Payload란 무엇인가요?
  * RSC 페이로드는 렌더링된 React Sever Component 트리의 압축된 바이너리 표현입니다.
  * client에서 React가 브라우저의 DOM을 업데이트하는데 사용됩니다.

## 0924 수업내용
5주차

* searchParams란?
  * URL의 쿼리 문자열을 읽는 방법입니다.
  * 여기서 category=shoes, page=2가 search parameters입니다.

* slug의 이해
  * 데이터 소스가 크다면 .find는 0(n)이므로 DB 쿼리로 바꿔야 합니다.

  * 하지만 promise<...>를 사용하지 않아도 오류 없이 동작했습니다.
  * 결론적으로 오류와 상관없이 Promise 사용을 권장합니다.

## 0917 수업내용
4주차

* 페이지 제작

## 0910 수업내용
3주차

* 라우팅
  * 페이지 나누기 : 앱의 각 기능을 별도의 페이지로 분리하여 관리하기 용이합니다.
  * 사용자 경험 향항 : 사용자는 즐겨찾기를 하거니, URL을 공유하거나, 브라우저의 뒤로 가기/앞으로 가기 버튼을 사용할 수 있어 일반적인 웹사이트처럼 자연스럽게 앱을 이용할 수 있습니다.
  * 체계적인 구조 : 코드의 구조를 명확하게 하고 유지보수를 쉽게 만들어 줍니다.

## 0903 수업내용
2주차

* pnpm으로 Next.js 프로젝트 생성

  * pnpm create next-app@latest

* 서버실행 : $ pnpm start

* pnpm으로 React 프로젝트 생성

  * pnpm create react-app my-app

* 서버 실행 : $ pnpm dev


## 0827 수업내용

1주차 오리엔테이션 진행
