# portfolio-template

이 코드에서는 HTML에서 두 개의 `div` 요소 (`.c1`과 `.c2`)를 선택하고, 그 안에 여러 개의 `div` 요소를 동적으로 생성한 후, `anime.js` 라이브러리를 사용하여 각각의 `div` 요소에 애니메이션 효과를 적용하는 방법을 보여줍니다.

### 1. HTML 구조

```html
<div class="c1"></div>
<div class="c2"></div>

```

### 2. JavaScript 설명

1. **`c1`과 `c2` 선택**:
    
    ```jsx
    const c1 = document.querySelector('.c1');
    const c2 = document.querySelector('.c2');
    
    ```
    
    - `.c1`과 `.c2` 클래스를 가진 `div` 요소를 선택하고, 변수 `c1`과 `c2`에 저장합니다. 이 `div` 요소들은 나중에 여러 개의 자식 `div`를 담게 될 요소들입니다.
2. **`appendChild` 함수 호출**:
    
    ```jsx
    appendChild(c1, num1);
    appendChild(c2, num2);
    
    ```
    
    - `appendChild` 함수는 첫 번째 인자로 받은 요소 (`c1`, `c2`)에 두 번째 인자로 받은 `idx` 값 만큼 자식 `div` 요소를 동적으로 추가하는 함수입니다. `num1`과 `num2`는 각각 250과 300으로, `c1`에는 250개의 자식 `div`, `c2`에는 300개의 자식 `div`가 추가됩니다.
3. **`appendChild` 함수**:
    
    ```jsx
    function appendChild(child, idx) {
        for (let i = 0; i < idx; i++) {
            childElement = document.createElement('div');
            child.append(childElement);
        }
    }
    
    ```
    
    - `appendChild` 함수는 주어진 `child` 요소에 `idx` 수만큼 자식 `div` 요소를 동적으로 생성하여 추가합니다.
    - `createElement('div')`로 새로운 `div` 요소를 만들고, `append()`를 사용하여 그것을 부모 요소에 추가합니다.
4. **애니메이션 적용 (anime.js)**:
    
    ```jsx
    anime({
        targets: '.circle>div',
        scale: [
            { value: .1, easing: 'easeOutSine', duration: 2000 },
            { value: 1, easing: 'easeInOutQuad', duration: 1200 }
        ],
        delay: anime.stagger(200, { grid: [20, 15], from: 'center' }),
        loop: true
    });
    
    ```
    
    - `anime.js`를 사용하여 `.circle > div` 요소들에 애니메이션 효과를 적용합니다.
    - **`scale`**: `div` 요소가 크기 변화를 겪습니다. 처음에는 `scale(0.1)`으로 작게 시작해서, `scale(1)`로 커지도록 설정합니다.
        - 첫 번째 단계에서 `scale(0.1)`은 `easeOutSine` 애니메이션으로 2000ms 동안 진행됩니다.
        - 두 번째 단계에서 `scale(1)`은 `easeInOutQuad` 애니메이션으로 1200ms 동안 진행됩니다.
    - **`delay`**: `anime.stagger(200, { grid: [20, 15], from: 'center' })`를 사용하여 `div` 요소들이 순차적으로 나타나도록 합니다. 이때 `grid: [20, 15]`는 20x15 격자로 요소들을 배치하도록 설정합니다. `from: 'center'`는 가운데에서부터 애니메이션을 시작하도록 설정합니다.
    - **`loop`**: `loop: true`로 애니메이션이 반복되도록 설정합니다.

### 3. 코드 동작 흐름

1. **`c1`과 `c2`에 자식 `div` 추가**:
    - `appendChild(c1, num1)`이 호출되면 `.c1` 요소에 250개의 `div` 요소가 추가되고, `appendChild(c2, num2)`가 호출되면 `.c2` 요소에 300개의 `div` 요소가 추가됩니다.
2. **애니메이션 시작**:
    - `.circle > div` 요소들에 대해 애니메이션이 적용됩니다. 각 `div`는 순차적으로 크기가 변하고, 이 애니메이션은 계속해서 반복됩니다.

### 4. 최종 구조

- `.c1`과 `.c2`는 각각 250개, 300개의 자식 `div`를 포함한 요소가 됩니다.
- `anime.js`는 `.circle > div` 요소들에 대해 크기 애니메이션을 적용하고, 순차적으로 나타나게 합니다.

### 5. 개선/수정 사항

- 현재 `.circle > div` 선택자가 있지만, 실제로 `.circle` 클래스는 코드에 없으므로, `.circle` 클래스를 `.c1` 또는 `.c2`로 수정해야 할 수 있습니다.
- 예시에서는 `div` 요소가 `circle` 안에 있다고 가정했기 때문에, 실제 HTML 구조에 맞게 수정이 필요할 수 있습니다.

---

이 코드의 목적은 간단히 **`div` 요소들을 동적으로 추가**하고, 그 **애니메이션을 제어**하는 것입니다. 애니메이션이 원하는 대로 실행되도록 하기 위해서는 HTML 구조와 `anime.js` 타겟이 일치해야 합니다.
