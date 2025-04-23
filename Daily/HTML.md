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
