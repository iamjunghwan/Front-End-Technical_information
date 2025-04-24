<details>
<summary>🩻 HTML 데이터 속성(data-)은 무엇인가요?
 </summary>
<br/>
**데이터 속성은 사용자 정의 데이터를 HTML 요소에 저장하기 위해 사용되는 속성**입니다. 선언 방법은 `data-`로 시작하는 속성을 HTML 태그에 추가하면 됩니다. 예를 들어, `<div data-user-id="12345" data-role="admin"></div>`와 같이 사용할 수 있습니다. 여기서 `data-user-id`와 `data-role`이 데이터 속성에 해당합니다.

데이터 속성은 자바스크립트를 통해 읽을 수 있습니다. 구체적으로는, 자바스크립트에서 dataset 객체를 사용하여 요소의 데이터 속성에 접근할 수 있습니다. 예를 들어, 위의 요소에서 `해당요소.dataset.userId`를 호출하면 "12345"라는 값이 반환됩니다.

또한, CSS에서도 `attr()` 함수나 속성 선택자를 통해 접근할 수 있습니다.

```css
/* attr() 함수를 사용하여 접근 */
article::before {
  content: attr(data-parent);
}

/* 속성 선택자를 사용하여 접근 */
article[data-columns="3"] {
  width: 400px;
}
```

## **데이터 속성은 언제 활용하나요? 🤔**

**DOM 요소에 특정 데이터를 바인딩하고, 자바스크립트 로직에서 해당 데이터를 활용하기 위해 사용**됩니다. 예를 들어, 버튼 클릭 이벤트에서 특정 데이터를 전달하거나, 데이터를 기반으로 UI를 동적으로 변경해야 할 때 유용합니다. 이렇게 하면 HTML과 자바스크립트 간 데이터 상호작용을 간단하게 구현할 수 있습니다.

</details>
<br/>

<details>
<summary>📄 HTML Doctype이 무엇인지 설명해주세요.
 </summary>
<br/>
HTML의 `<!DOCTYPE>`은 웹 브라우저에 해당 문서가 어떤 HTML 버전을 기반으로 작성되었는지 알려주는 역할을 하는 선언문입니다. 문서의 최상단에 위치하며, 브라우저가 HTML 문서를 해석하고 렌더링하는 방식을 결정합니다. 대소문자를 구분하지 않지만, 강조하기 위해 대문자를 사용하는 경우가 많습니다.

과거에는 HTML의 다양한 버전(ex. XHTML 1.1, HTML 4.01 등)이 존재했기 때문에 브라우저가 문서를 올바른 방식으로 해석하기 위해, 적절한 방식으로 Doctype을 직접 지정해야 했습니다. HTML5에 접어들어서는 선언 방식이 단순화되어 `<!DOCTYPE html>`으로 간단하게 선언할 수 있습니다. 이 선언문은 HTML5를 사용하고 있음을 명시합니다.

## **Doctype을 선언하지 않아도 되나요? 🤔**

아니요, Doctype을 꼭 선언해 주어야 합니다. 만약 Doctype 선언이 없다면 브라우저는 문서를 **쿼크 모드(quirks mode)** 로 렌더링할 수 있습니다. 쿼크 모드는 오래된 웹사이트와의 호환성을 유지하기 위해 표준과 다른 방식으로 동작합니다. 이는 예상치 못한 동작을 발생시킬 수 있습니다. 따라서 정확하고 일관된 렌더링을 위해 Doctype 선언은 필수적입니다. 오늘날에는 대부분 HTML5를 사용하므로 `<!DOCTYPE html>`을 선언해주면 됩니다.

</details>
<br/>

<details>
<summary>🎐 Node와 Element의 차이에 대해 설명해주세요.
 </summary>
<br/>
Node와 Element의 핵심적인 차이점에 대해 설명드리겠습니다.

Node는 **DOM을 구성하는 가장 기본적인 구성 단위**입니다. Node에는 여러 가지 타입이 존재합니다. "Document Node"는 HTML 문서 전체를 나타내는 루트 노드이며, "Element Node"는 HTML 태그를 나타내고, "Text Node"는 텍스트 내용을, "Comment Node"는 주석을 나타냅니다. 이처럼 Node는 DOM 트리의 모든 구성 요소를 포함하는 포괄적인 개념입니다.

반면 Element는 Node의 특정 타입 중 하나로, **HTML이나 XML 태그로 표현되는 객체**를 의미합니다. 쉽게 말해, 모든 Element는 Node이지만, 모든 Node가 Element인 것은 아닙니다. Element는 `id`, `class`, `style`과 같은 HTML 속성을 가질 수 있으며, `querySelector()`나 `getElementsByClassName()`과 같은 메서드를 사용할 수 있다는 특징이 있습니다.

예를 들어 `<div>Hello<!--주석-->World</div>`라는 HTML이 있다면, div 태그는 Element Node이면서 동시에 Node입니다. 반면 'Hello'와 'World'라는 텍스트는 Text Node이며, 주석은 Comment Node입니다. 이들은 모두 Node이지만 Element는 아닙니다.

## **Node와 Element의 차이와 관련된 구체적인 예시를 들어주세요. 🤔**

예를 들어, `textContent`라는 속성은 Node의 속성이므로 모든 종류의 Node에서 사용할 수 있지만, `innerHTML`은 Element의 속성이므로 Element에서만 사용할 수 있습니다.

또한, `childNodes`와 `children` 속성에도 중요한 차이가 있습니다. Node의 속성인 `childNodes`는 주어진 요소의 모든 자식 Node를 포함하는 `NodeList`를 반환합니다. 여기에는 Element뿐만 아니라 모든 종류의 Node가 포함됩니다. 따라서 HTML 태그뿐 아니라 텍스트, 주석도 `childNodes`에 포함됩니다. 반면 Element의 속성인 `children`은, Element 타입의 자식 노드만을 포함하는 `HTMLCollection`을 반환합니다. 여기에는 텍스트 노드나 주석 노드는 제외되고 HTML 요소 노드만 포함됩니다.

</details>
<br/>

<details>
<summary>🤲 쌓임 맥락에 대해 설명해주세요.</summary>
<br/>
**쌓임 맥락(Stacking Context)은 가상의 z축을 상정하여 HTML 요소들을 3차원으로 개념화한 것**입니다. 쌓임 맥락은 요소들이 쌓이는 순서에 영향을 미칩니다.

기본적으로 HTML 요소는 DOM 순서에 따라 쌓입니다. HTML 상에서 위쪽에 위치할수록 아래쪽에 쌓이는 방식입니다. 또한, `position` 속성이 적용되어 있는 요소들은 `z-index` 값이 낮을수록 아래쪽으로, 높을수록 위쪽으로 쌓입니다.

그런데 **특정 조건이 충족되면 새로운 쌓임 맥락이 생성**됩니다. 이 쌓임 맥락은 독립적인 3차원 공간을 만들며, 부모 쌓임 맥락의 영향을 받지 않고 해당 쌓임 맥락 내에서만 비교가 이뤄져 쌓임 순서가 결정됩니다.

대표적으로 쌓임 맥락이 생성되는 조건은 다음과 같습니다. ([MDN 참고 자료](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_positioned_layout/Understanding_z-index/Stacking_context#%EC%84%A4%EB%AA%85))

1. `position` 속성이 `relative` 또는 `absolute`이고 `z-index` 값이 `auto`가 아닌 경우
2. `postion` 속성이 `fixed` 또는 `sticky`인 경우
3. `display`가 `flex` 또는 `grid`이고, `z-index`가 설정된 경우
4. `opacity` 값이 1 미만인 경우
5. `transform`, `filter`, `backdrop-filter` 등의 속성이 적용되는 경우

쌓임 맥락이 동작하는 간단한 예시를 설명드리겠습니다.

```html
<div style="position: relative; z-index: 1;">
  A 요소 (z-index: 1)
  <div style="position: absolute; z-index: 999;">A-1 요소 (z-index: 999)</div>
</div>
<div style="position: relative; z-index: 2;">B 요소 (z-index: 2)</div>
```

위 예시에서 **가장 위쪽에 쌓이는 요소는 B 요소입니다. 그 다음 A-1 요소, A 요소 순**으로 쌓입니다.

최상위 쌓임 맥락 내의 요소들인 A 요소와 B 요소의 `z-index` 값을 비교했을 때, B 요소가 크기 때문에 가장 위쪽에 쌓입니다. 그리고 A 요소가 형성한 쌓임 맥락 내에서 `z-index` 값을 비교했을 때, A 요소보다 `z-index`가 큰 A-1 요소가 더 위쪽에 쌓이게 됩니다.

이런 예시를 보면 `z-index` 값이 더 크다고 무조건 위쪽에 쌓이는 것이 아니며, 쌓임 맥락을 고려해야 한다는 사실을 알 수 있습니다.

</details>
<br/>

<details>
<summary>🤪 HTML link 요소의 rel 속성 값 preconnect, preload, prefetch에 대해 설명해주세요.
 </summary>
<br/>
`<link>`는 외부 리소스와의 연결을 돕는 요소이며, `rel` 속성 값인 **preconnect**, **preload**, **prefetch**는 **리소스 로드의 우선순위를 설정하여 로드 성능을 최적화하기 위해 사용됩니다**.

### **1. preconnect**

`preconnect`는 **브라우저가 특정 origin에 대한 네트워크 연결을 미리 설정하도록 지시합니다**. 이를 통해 DNS 조회, TLS 핸드셰이크, TCP 연결을 미리 완료하여 리소스 로드 지연을 줄일 수 있습니다. 외부 API나 CDN의 리소스를 사용할 경우 `preconnect`를 사용하면 첫 번째 요청의 대기 시간을 줄일 수 있습니다.

```html
<link
  rel="preconnect"
  href="https://external-resource.com"
  crossorigin="anonymous"
/>
```

`preconnect`는 리소스 자체를 로드하지 않고, 요청할 origin과의 연결만 미리 준비합니다. 자주 사용하는 외부 리소스의 도메인에 대해 적용하는 것이 효과적입니다.

### **2. preload**

`preload`는 **특정 리소스를 미리 가져오도록 브라우저에 지시합니다**. 예를 들어, 웹 폰트를 preload하면 해당 리소스가 실제로 사용되기 전에 다운로드가 완료됩니다.

```html
<link
  rel="preload"
  href="/fonts/my-font.woff2"
  as="font"
  crossorigin="anonymous"
/>
```

웹 폰트가 늦게 로드되면 텍스트가 기본 폰트로 잠시 표시되는 FOUT 현상이 발생할 수 있는데, 이를 `preload`로 방지할 수 있습니다.

### **3. prefetch**

`prefetch`는 **브라우저가 향후 필요할 가능성이 있는 리소스를 미리 가져오도록 지시합니다**. `preload`와는 다르게, 현재 화면에 즉시 필요하지 않지만 다음에 필요할 가능성이 있는 리소스를 미리 로드하는 역할을 합니다. `prefetch`는 다른 속성 값에 비해 우선순위가 상대적으로 낮습니다.

```html
<link rel="prefetch" href="/next-page.css" as="style" />
```

사용자가 페이지에서 버튼을 클릭해 다음 화면으로 이동할 가능성이 높을 경우, 다음 화면에 필요한 css 리소스를 미리 준비하는 방식으로 사용할 수 있습니다.

</details>
<br/>

<details>
<summary>🙃 image 요소의 alt 속성은 어떤 목적으로 사용하나요?</summary>
<br/>
이미지의 `alt` 속성은 단순 부가 설명이 아니라 여러 중요한 기능을 가지는 속성입니다.

먼저, `alt` 속성은 **이미지를 로드할 수 없는 상황에서 대체 텍스트를 제공하여** 사용자에게 콘텐츠를 이해할 수 있도록 돕는 역할을 합니다. 예를 들어, 네트워크 문제로 이미지가 로드되지 않는 경우, alt 속성의 텍스트가 대신 표시되어 이미지의 의도를 전달할 수 있습니다.

또한, `alt` 속성은 **접근성 측면에서 큰 도움을 줍니다**. 스크린 리더를 사용하는 시각 장애 사용자는 이미지를 직접 볼 수 없기 때문에, `alt` 속성을 통해 이미지의 내용을 음성으로 듣게 됩니다. `alt` 속성을 적절히 설정하면 웹 페이지 내 이미지 컨텐츠에 시각 장애 여부와 상관 없이 누구나 접근할 수 있게 됩니다.

마지막으로, `alt` 속성은 **SEO 측면에서도 중요한 요소로 작용합니다**. 검색 엔진은 이미지를 시각적으로 분석할 수 없기 때문에, `alt` 속성에 포함된 텍스트를 기반으로 이미지의 콘텐츠를 이해하고 이를 검색 결과에 반영합니다. 적절한 키워드가 포함된 `alt` 속성은 이미지 검색에서 상위 노출을 도울 수 있습니다.

이처럼 `alt` 속성에는 단순한 부가 설명 이상의 기능이 있습니다. 사용자 경험, 접근성, SEO 측면에서 중요한 역할을 합니다.

## **모든 이미지에 alt 속성을 꼭 작성해야 하나요? 🤔**

반드시 그렇지는 않습니다. 장식적인 용도로만 사용되는 이미지에는 `alt` 속성을 비워두는 것이 더 좋습니다. 예를 들어, 배경으로 사용되는 이미지나 레이아웃 디자인을 위한 이미지는 의미를 전달하지 않아도 되므로 `alt=""`로 빈 값을 설정하는 것이 좋습니다. 이렇게 설정하면 스크린 리더가 이를 건너뛰도록 하여 사용자가 불필요한 요소에 대한 설명을 듣지 않고 넘어갈 수 있습니다.

반면, 만약 중요한 정보나 컨텐츠를 담고 있는 이미지라면 항상 적절한 alt 텍스트를 제공해야 합니다.

</details>
<br/>
