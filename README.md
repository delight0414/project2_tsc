## 🚩Project - HYBE

#### 📰 Intro 
기존에 있던 HTML, Javascript로 개발했던 프로젝트를 React, Typescript, Recoil로 마이그레이션했습니다. Typescript로 오류를 최소화하고 Recoil를 사용하여 React에 친화적인 데이터 상태관리를 하였습니다.

##
#### 👩‍💻 Stack 
<div>
  <img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=white">
  <img src="https://img.shields.io/badge/Recoil-3578e5?style=for-the-badge&logo=recoil&logoColor=white">
  <img src="https://img.shields.io/badge/css-1572b6?style=for-the-badge&logo=css3&logoColor=white">
  <img src="https://img.shields.io/badge/typescript-3178c6?style=for-the-badge&logo=typescript&logoColor=white">
</div>
<div>
  <img src="https://img.shields.io/badge/Figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white">
  <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white">
  <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white">
</div>
<div>
  <img src="https://img.shields.io/badge/gsap-0AE448?style=for-the-badge&logo=gsap&logoColor=white">
  <img src="https://img.shields.io/badge/swiper.js-6332F6?style=for-the-badge&logo=aos&logoColor=white">
  <img src="https://img.shields.io/badge/aos-1FA2ED?style=for-the-badge&logo=aos&logoColor=white">
</div>

##
#### 💻 Code review
🔸 해상도 720px 미만일 경우에만 Swiper가 작동되게 했다. HTML로 개발했을때도 destroy()를 사용했는데 이번에도 동일하게 사용했다.
```typescript
let winw: number = 0;

const [swiperInstance, setSwiperInstance] = useState<SwiperCore | null>(null);
// swiperInstance: Swiper 인스턴스  setSwiperInstance : Swiper 업데이트 함수

const [isSwiperActive, setIsSwiperActive] = useState(false);
// isSwiperActive: 현재 상태  setIsSwiperActive: 업데이트 함수
```
  1️⃣ 해상도에 따라서 destroy하기
```typescript
const updateSwiperStatus = () => {
  const width = window.innerWidth;

// 720px 미만이면 swiper 활성화
if (width < 720) {
  setIsSwiperActive(true);
}

// 720px 미만이면 swiper 비활성화
else {

// 720px 미만이면 swiper 비활성화
  setIsSwiperActive(false);

// swiper가 존재한다면 인스턴스를 파괴하고 null로 만들어서 swiper 비활성화
  if (swiperInstance) {
    swiperInstance.destroy(false, true);
    setSwiperInstance(null);
    }
  }
};
```
  2️⃣ resize가 될 때 destroy하기
```typescript
useEffect(() => {
// 초기 swiper 상태 설정
  updateSwiperStatus();

// swiperInstance가 변경되고 resize 이벤트가 발생되면 함수 호출됨
  window.addEventListener('resize', updateSwiperStatus);
}, [swiperInstance]);

return(
  {isSwiperActive ? (
    Swiper is active
  ) : (
    Swiper is not active
  )}
)
```

