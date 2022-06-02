# :pushpin: GO-Cloud Project
[TEST](#4.-트러블-슈팅)
> 공간대여 플랫폼 개발 | [구현 영상](https://youtu.be/LltdW7TfhcU)

</br>

## 1. 제작 기간 & 참여 인원

- 2022년 04월 11일 ~ 04월 21일 (11일)
- 팀 프로젝트(프론트 4명 백엔드 2명)
- 프론트엔드 깃헙 주소: https://github.com/wecode-bootcamp-korea/31-2nd-GoCloud-frontend
- 백엔드 깃헙 주소: https://github.com/wecode-bootcamp-korea/31-2nd-GoCloud-backend

</br>

## 2. 사용 기술

`Front-end`

- React 18
- React Router v6
- JavaScript
- Styled-Component
- HTML/CSS

</br>

## 3. 내가 맡았던 기능 구현

제가 이 프로젝트에서 맡은 페이지는 **상세페이지와 예약리스트 페이지** 입니다.

<br>

### 상세페이지

![2차 프로젝트 상세페이지](https://user-images.githubusercontent.com/80018243/165205667-1476b2f3-8dcb-4d3f-af88-944dce48f7cd.gif)

<br>

**DatePicker를 이용하여 날짜 및 시간 선택 & 예약기능 구현**

- 날짜와 시간을 선택한 후 예약하기 기능 구현

  - 기본 이용시간 1시간으로 고정

- filter를 적용하여 현 시간 이전은 선택하지 못하도록 구현  
  :pushpin: [코드확인](https://github.com/Geuni620/31-2nd-GoCloud-frontend/blob/b67968227a897be2230613600e2271ef5cdf2e75/src/pages/Detail/Picker.js#L7)

<br>

**Path Parameter 사용하여 리스트페이지에서 상세페이지로 이동**

- `useParams` hook을 상세페이지 해당 id를 읽고 리스트페이지에서 페이지를 클릭하면 상세페이지로 이동하도록 구현

<br>

**Swiper를 이용하여 슬라이드 기능 구현**

- Swiper 라이브러리를 이용하여 상세페이지 이미지를 슬라이드되도록 구현

<br>

**React-Scroll를 이용하여 Scroll Spy 기능 구현**

- 상세피이지 안에서 페이지 내용을 편하게 확인할 수 있도록 목차개념의 Nav bar를 만듦

- 만들어진 Nav bar는 `position: sticky`를 이용하여 스크롤을 내릴 때 일정 위치가 되면 상단에 고정되도록 구현했음.
- `React-Scroll` 라이브러리를 이용하여 상단 고정된 Nav bar에 메뉴 탭을 클릭하면 해당 위치로 이동하도록 구현
- 클릭했을 때 클릭 이벤트를 읽어서 해당 메뉴탭의 색상이 활성화 되도록 했음.

  - 이 과정의 트러블슈팅은 [여기](#4.-트러블-슈팅)

<br>

**Custom hooks인 useFetch를 사용하여 관심사의 분리 개념 적용**

- fetch를 덕지덕지 붙여서 전체적으로 코드가 어지러워진다는 것을 알게 됨
- 관심사 분리 개념을 적용해서 useFetch hooks를 만들고 코드를 간결하게 수정했음

  [관심사의 분리](https://kaki104.tistory.com/725)

<br>

### 예약리스트 페이지

![2차 프로젝트 예약리스트](https://user-images.githubusercontent.com/80018243/165205894-a91cdc38-d2b9-457c-b165-c3adb0ca411e.gif)

- Path Parameter 사용하여 예약한 상세페이지 이동

<br>

## 4. 트러블 슈팅

### 4-1. 상세페이지 Nav bar의 색상이 차례로 활성화되는 오류

- 첫 번째에서 세 번째 메뉴탭을 클릭하면 스크롤이 자동으로 이동하는 과정에서 두 번째 메뉴탭이 활성화되었다가 꺼지고, 세 번째 메뉴탭의 위치에 도달했을 때 세 번째 메뉴탭이 켜지는 오류 발생.
- 원하던 기능은 메뉴탭을 클릭했을 때 클릭한 메뉴만 활성화 되고, 해당 위치로 이동하도록 구현하고 싶었음.

  :pushpin: [코드확인](https://github.com/Geuni620/31-2nd-GoCloud-frontend/blob/b67968227a897be2230613600e2271ef5cdf2e75/src/pages/Detail/MainNav.js#L14)

  1. Link에 onClick으로 handleEventRead함수를 만들어주고 클릭된 이벤트의 id값을 읽도록 구현  
     → 첫 번째 메뉴탭을 클릭하면 id값 1번 출력

  2. 읽어진 id를 `idCheck` state에 담아줬음
  3. 담겨진 `idCheck` state를 이용해 className에 조건문을 작성하여 읽어진 아이디값과 idcCheck에 담겨진 값이 같을 경우에만 활성화되도록 구현함.

<br>

### 4-2. DatePiker 라이브러리 설치시 에러발생

- 프로젝트 시작할 당시, React 18버전으로 업데이트 됨.
- 업데이트 되면서 기존에 사용할 수 있던 라이브러리의 버전차이로 사용하지 못하는 경우가 발생했음.

  :pushpin: [참고자료](https://velog.io/@yonyas/Fix-the-upstream-dependency-conflict-installing-NPM-packages-%EC%97%90%EB%9F%AC-%ED%95%B4%EA%B2%B0%EA%B8%B0)

  → `--legacy-peer-deps`를 이용하여 충돌을 무시하는 방향으로 라이브러리 설치, 문제없이 동작함.

<br>

### 4-3. DatePiker 기존 스타일 변경

- 라이브러리 설치된 이후 기존 스타일을 변경하고 싶은데 라이브러리 스타일이 우선권을 가지는 경우 Styled Component로 변경이 불가능한 문제 발생

- CSS `!important`를 알게 됐고, 남발할 시 협업간의 문제가 발생할 수 있으니 꼭 필요한 경우에만(!) 사용해야한다는 점을 숙지 함.
