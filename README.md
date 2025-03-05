# portfolio-template

### 코드 설명

- **GSAP와 ScrollTrigger 플러그인 등록:**
    
    ```jsx
    gsap.registerPlugin(ScrollTrigger);
    
    ```
    
    - `GSAP`는 애니메이션을 쉽게 만들 수 있게 도와주는 라이브러리입니다.
    - `ScrollTrigger`는 스크롤을 트리거로 하는 애니메이션을 만들 수 있게 해주는 GSAP의 플러그인입니다. (이 코드에서는 사용되지 않았지만, 나중에 추가할 수 있습니다.)
- **마우스 움직임에 반응하는 효과 적용:**
    
    ```jsx
    document.querySelectorAll('.hover-effect').forEach((element) => {
        element.addEventListener('mousemove', (e) => {
    
    ```
    
    - `.hover-effect` 클래스를 가진 모든 요소들에 대해, 마우스를 움직일 때마다 `mousemove` 이벤트를 감지합니다.
- **마우스 위치에 따른 회전 값 계산:**
    
    ```jsx
    const { width, height, left, top } = element.getBoundingClientRect();
    const x = ((e.clientX - left - width / 2) / width) * 20; // x축 회전값
    const y = ((e.clientY - top - height / 2) / height) * 20; // y축 회전값
    
    ```
    
    - 요소의 `width`, `height`, `left`, `top` 값을 이용해, 마우스의 위치에 따른 회전 값을 계산합니다.
    - `x`와 `y` 값은 각각 x축과 y축에 대한 회전값으로, 마우스가 움직일 때마다 해당 값이 변합니다.
- **회전 애니메이션 적용:**
    
    ```jsx
    gsap.to(element, {
        rotateX: x,
        rotateY: y,
        transformPerspective: 1000, // 원근감 효과
        ease: 'power2.out',
        duration: 0.3
    });
    
    ```
    
    - 계산된 `x`와 `y` 값을 이용해 요소를 회전시킵니다. `transformPerspective`는 원근감을 주어 더 자연스러운 3D 효과를 만듭니다.
- **자식 요소에 랜덤한 애니메이션 적용:**
    
    ```jsx
    gsap.to(element.querySelectorAll('span'), {
        rotateX: () => gsap.utils.random(-15, 15),
        rotateY: () => gsap.utils.random(-15, 15),
        translateZ: () => gsap.utils.random(-30, 30),
        ease: 'power2.out',
        duration: 0.3,
        stagger: 0.5
    });
    
    ```
    
    - 요소 내부에 있는 `<span>` 요소들에 대해 랜덤한 회전 및 Z축 이동을 적용합니다.
    - `rotateX`, `rotateY`, `translateZ`는 랜덤 범위로 회전 및 이동 효과를 적용하여 요소들이 독특한 3D 애니메이션을 보이도록 합니다.
    - `stagger: 0.5`는 자식 요소들 사이에 애니메이션의 지연을 줘서 더 동적인 느낌을 제공합니다.
- **마우스가 떠날 때 초기화:**
    
    ```jsx
    element.addEventListener('mouseleave', () => {
        gsap.to(element, {
            rotateX: 0,
            rotateY: 0,
            ease: 'power2.out',
            duration: 0.3
        });
        gsap.to(element.querySelectorAll('span'), {
            rotateX: 0,
            rotateY: 0,
            translateZ: 0,
            ease: 'power2.out',
            duration: 0.3,
            stagger: 0.5
        });
    });
    
    ```
    
    - 마우스가 요소를 떠나면(`mouseleave` 이벤트) 요소와 그 자식 요소들의 회전 및 이동 효과를 초기화하여, 기본 상태로 돌아가게 만듭니다.

### 정리

- **마우스 움직임**에 따라 요소는 **3D 회전**하고, 자식 `<span>` 요소들도 랜덤하게 **회전 및 이동**합니다.
- 마우스가 요소를 **벗어나면**, 회전 효과와 이동이 초기화됩니다.
- **GSAP**는 애니메이션을 쉽게 만들 수 있도록 도와주는 라이브러리이며, **transformPerspective**를 이용한 원근 효과와 **ease**로 부드러운 전환을 제공합니다.
