# portfolio-template

1. **GSAP 애니메이션**: 텍스트가 등장하는 애니메이션을 설정
2. **실시간 한국 시간 업데이트**: 페이지에 실시간 한국 시간을 표시

### 1. **GSAP 애니메이션 (텍스트 애니메이션)**

```jsx
gsap.from('#intro .char', {
    yPercent: 110,
    stagger: 0.03,
    duration: .3,
    ease: 'power1'
})

```

- *GSAP (GreenSock Animation Platform)**를 사용하여 `#intro .char` 클래스를 가진 요소들을 애니메이션합니다.
- **`yPercent: 110`**: 요소들이 `y축` 방향으로 110% 아래에서 시작합니다. 즉, 화면 바깥에서 시작해서 위로 올라오는 효과입니다.
- **`stagger: 0.03`**: 요소들이 순차적으로 등장하도록 `0.03초`씩 차이를 둡니다. 이 값은 요소들이 0.03초 간격으로 등장하게 합니다.
- **`duration: .3`**: 애니메이션이 0.3초 동안 진행됩니다.
- **`ease: 'power1'`**: `power1` 이징(easing) 함수로, 애니메이션이 부드럽게 진행되도록 설정합니다.

이 애니메이션은 `#intro .char`로 지정된 요소들을 아래에서 위로 차례대로 애니메이션하는 효과를 줍니다.

---

### 2. **실시간 한국 시간 업데이트**

```jsx
const koTime = document.querySelector('#koTime')

function updateTime() {
    const koreaTime = new Date().toLocaleTimeString("en-US", {
        timeZone: 'Asia/Seoul',
        hour: '2-digit',
        minute: '2-digit',
        second: '2-digit',
        hour12: false
    })
    koTime.textContent = koreaTime
}
updateTime()
setInterval(updateTime, 1000)

```

- **`koTime`**: `#koTime` 요소를 선택합니다. 이 요소는 실시간 시간을 표시할 곳입니다.
- **`updateTime()`**: 이 함수는 한국 시간(`Asia/Seoul` 타임존)을 가져와서 `koTime` 요소에 표시합니다.
    - `new Date().toLocaleTimeString()`을 사용하여 현재 시간을 가져오는데, `en-US` 포맷을 사용하고, `Asia/Seoul` 타임존을 설정하여 정확한 한국 시간을 가져옵니다.
    - `hour: '2-digit'`, `minute: '2-digit'`, `second: '2-digit'`는 시간을 2자리 형식으로 출력하도록 설정합니다.
    - `hour12: false`는 24시간제로 시간을 표시하도록 설정합니다.
- **`setInterval(updateTime, 1000)`**: `updateTime` 함수를 1초마다 호출하여 실시간으로 시간을 갱신합니다. 1000ms는 1초입니다.

이 코드는 한국의 현재 시간을 `#koTime` 요소에 계속해서 표시합니다.

---

### 전체적인 흐름

1. **GSAP 애니메이션**: 페이지가 로드되면 `#intro .char` 요소들이 순차적으로 애니메이션되며 나타납니다.
2. **실시간 시간 업데이트**: `#koTime` 요소에 실시간 한국 시간이 1초마다 갱신되어 표시됩니다.

### 요약

- **GSAP 애니메이션**: 텍스트가 순차적으로 등장하는 애니메이션을 적용합니다.
- **실시간 시간**: 한국 시간을 1초마다 갱신하여 표시합니다.
