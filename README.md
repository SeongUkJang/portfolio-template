#가로 스크롤
GSAP (GreenSock Animation Platform)과 ScrollTrigger 플러그인을 사용하여 스크롤 이벤트를 기반으로 애니메이션을 적용하는 코드입니다.

### 1. **ScrollTrigger.matchMedia()** 사용

```jsx
gsap.registerPlugin(ScrollTrigger)

ScrollTrigger.matchMedia({
    "(min-width:1024px)": function(){
        let item = gsap.utils.toArray('.skill-wrap li')

        gsap.to(item, {
            xPercent: -100 * (item.length - 1),
            ease: 'none',
            scrollTrigger: {
                trigger: '#s2 .skill-wrap',
                pin: true,
                scrub: 1,
                snap: 1 / (item.length - 1)
            }
        })
    }
})

```

- **목적**: 화면 크기가 `1024px` 이상일 때 특정 애니메이션을 실행합니다.
- **동작**: `.skill-wrap li` 항목들이 가로로 스크롤되며, 스크롤에 따라 아이템들이 애니메이션 효과를 받습니다. `pin` 옵션으로 스크롤 시 해당 요소가 고정되고, `scrub` 옵션으로 스크롤 속도와 애니메이션의 진행이 맞춰집니다. `snap` 옵션은 스크롤 위치가 각 항목에 맞게 "딱" 맞춰지게 합니다.

---

### 2. **Scene 1: 타임라인 애니메이션**

```jsx
const scene1 = gsap.timeline()

ScrollTrigger.create({
    animation: scene1,
    trigger: "#s1",
    start: "top 20%",
    end: "top 80%",
    scrub: 1
})

scene1.to('#s1 .img-wrap', { opacity: 1, x: 10 })
scene1.to('#s1 .img-wrap .name', { opacity: 1, x: 10 })
scene1.to('.pf-con h3', { opacity: 1, x: -10, stagger: .2 })
scene1.to('.pf-con dl>*', { opacity: 1, x: -10, stagger: .2, duration: .2 })
scene1.to('.skill-list li>*', { opacity: 1, x: -10, stagger: .2, duration: .2 })
scene1.to('.pg-wrap .pg.pg1', { width: '70%', delay: -.2 })
scene1.to('.pg-wrap .pg.pg2', { width: '60%', delay: -.2 })
scene1.to('.pg-wrap .pg.pg3', { width: '80%', delay: -.2 })
scene1.to('.pg-wrap .pg.pg4', { width: '90%', delay: -.2 })

```

- **목적**: `#s1` 요소에 대한 스크롤 애니메이션을 설정합니다.
- **동작**:
    - **타임라인**: `scene1`은 여러 개의 애니메이션을 순차적으로 적용하는 타임라인입니다.
    - `ScrollTrigger.create()`는 `#s1` 요소가 화면에서 특정 범위에 들어올 때 애니메이션을 실행합니다. `start`와 `end` 속성으로 시작과 끝 지점을 설정하며, `scrub`을 통해 스크롤 진행에 맞춰 애니메이션이 진행됩니다.
    - 다양한 요소들에 대해 애니메이션을 설정합니다:
        - **이미지**: `.img-wrap`와 `.name`의 opacity가 0에서 1로 바뀌고, X축으로 이동합니다.
        - **텍스트**: `.pf-con h3`, `.pf-con dl`, `.skill-list li` 등 여러 텍스트 요소들이 스크롤에 맞춰 나타나고 이동합니다.
        - **진행률 표시**: `.pg-wrap .pg` 클래스 요소들의 너비가 변경됩니다 (각각 70%, 60%, 80%, 90%).

### 요약

- **첫 번째 부분**은 `matchMedia`를 사용하여 화면 크기가 1024px 이상일 때, 특정 요소들을 스크롤에 따라 이동시키는 애니메이션을 적용합니다.
- **두 번째 부분**은 `ScrollTrigger`를 사용해 `#s1` 요소에 스크롤 애니메이션을 추가하며, 다양한 요소들이 스크롤에 맞춰 나타나거나 이동하고, 진행률 바가 변화하는 효과를 제공합니다.

각각의 스크롤 애니메이션은 스크롤 위치에 따라 매끄럽게 진행되며, `scrub`과 `snap` 옵션을 통해 사용자 경험을 더 좋게 만들어줍니다.
