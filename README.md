# portfolio-template

### 핵심 포인트

- `mousemove` 이벤트로 커서의 위치를 업데이트.
- `mouseenter`와 `mouseleave` 이벤트로 링크와 버튼 위에서 커서 크기를 변화.
- `gsap` 라이브러리를 사용하여 부드러운 애니메이션 효과 구현.

---

커스텀 커서를 만들고, 

마우스 움직임에 따라 커서의 위치를 부드럽게 이동시키며, 

링크(`a`)나 버튼(`button`) 위에 마우스를 올리면 

커서가 크기가 바뀌는 효과를 추가하는 JavaScript 코드입니다. 

`gsap` 라이브러리를 사용하여 애니메이션을 처리하고 있습니다. 

---

- 1. **`DOMContentLoaded` 이벤트**
    
    ```jsx
    document.addEventListener('DOMContentLoaded', function () { //start
    
    ```
    
    - 이 이벤트는 DOM이 완전히 로드되었을 때 실행됩니다. 이 안에 작성된 코드들은 페이지가 완전히 로드된 후에 실행됩니다.
- 2. **커서 요소 선택**
    
    ```jsx
    const customCursor = document.querySelector('.cursor-wrap')
    const customCursor2 = document.querySelector('.cursor-wrap .cursor')
    
    ```
    
    - `customCursor`: 커서의 외부 래퍼(div) 요소를 선택합니다.
    - `customCursor2`: 실제 커서를 나타내는 내부 요소를 선택합니다.
- 3. **마우스 움직임에 따라 커서 이동**
    
    ```jsx
    document.addEventListener('mousemove', function (e) {
        console.log(e.clientX, e.clientY);  // 마우스의 x, y 좌표를 콘솔에 출력
    
        gsap.to(customCursor, {
            x: e.clientX,  // 마우스의 X 좌표로 커서 위치 이동
            y: e.clientY,  // 마우스의 Y 좌표로 커서 위치 이동
            xPercent: -50,  // 커서가 정확히 마우스를 따라가게 하기 위한 보정 (커서 중앙에 맞추기)
            yPercent: -50,  // 커서가 정확히 마우스를 따라가게 하기 위한 보정
            duration: .1,  // 이동 시간 (0.1초)
            opacity: 1      // 커서의 투명도를 1로 설정 (보이도록 함)
        })
    })
    
    ```
    
    - 마우스가 움직일 때마다 `mousemove` 이벤트가 발생합니다.
    - `gsap.to()`를 사용하여 `customCursor` 요소를 마우스의 x, y 좌표에 맞게 이동시킵니다.
    - `xPercent`와 `yPercent`는 커서의 중앙을 마우스 위치에 맞추기 위해 사용합니다.
- 4. **링크와 버튼에 마우스 올리기 효과**
    
    ```jsx
    document.querySelectorAll('a,button').forEach((el) => {
        el.addEventListener('mouseenter', () => {
            gsap.to(customCursor2, {
                scale: .3,  // 커서 크기를 30%로 줄임
                duration: .1  // 애니메이션 시간 0.1초
            })
        })
    
        el.addEventListener('mouseleave', () => {
            gsap.to(customCursor2, {
                scale: 1,  // 커서 크기를 원래 크기(100%)로 되돌림
                duration: .1  // 애니메이션 시간 0.1초
            })
        })
    })
    
    ```
    
    - `a` 태그와 `button` 태그에 마우스를 올리면(`mouseenter`), 커서 크기가 30%로 축소됩니다.
    - 마우스가 떠나면(`mouseleave`), 커서 크기가 원래 크기로 돌아옵니다.
- 5. **특정 요소에 마우스 올리기 (커서 애니메이션 추가)**
    
    ```jsx
    const mouseTl = gsap.timeline({ paused: true })
    
    mouseTl.to('.cursor-wrap .learn-more', {
        opacity: 1,
        duration: .1
    })
    
    mouseEventEl.forEach((el) => {
        el.addEventListener('mouseenter', () => {
            mouseTl.play()
        })
        el.addEventListener('mouseleave', () => {
            mouseTl.reverse()
        })
    })
    
    ```
    
    - `mouseEventEl`은 `.mouse-event` 클래스를 가진 요소들을 선택합니다.
    - 마우스를 올리면 커서에 `learn-more` 요소가 나타나도록 애니메이션을 실행하고, 마우스를 떼면 다시 사라지게 합니다.

---

### 최종 코드 요약

1. 페이지가 로드되면 커스텀 커서가 준비됩니다.
2. 마우스를 움직일 때 커서가 부드럽게 마우스를 따라 다닙니다.
3. 링크(`a`)와 버튼(`button`) 위에 마우스를 올리면 커서가 작아지고, 마우스를 떼면 원래 크기로 돌아옵니다.
4. `gsap` 라이브러리를 사용하여 애니메이션 효과를 적용합니다.
