<details>
<summary>  최신 버전의 Next.js가 제공하는 캐싱 기능들에 대해 설명해주세요.
 </summary>
<br/>
최신 버전의 Next.js는 성능 최적화를 위해 다양한 캐싱 기능들을 제공합니다. 크게 리퀘스트 메모이제이션, 클라이언트 라우터 캐시, 데이터 캐시, 풀 라우트 캐시로 나누어 설명드리겠습니다.

먼저, 리퀘스트 메모이제이션은 동일한 요청이 여러 번 발생할 때, 불필요한 추가 요청을 방지하는 기능입니다. 기본적으로 Next.js는 서버 사이드에서 동일한 요청이 중복 발생하면 기존 응답을 재사용합니다. 이를 통해 하나의 페이지 내에 존재하는 중복된 요청을 방지하여 네트워크 비용을 감소시킵니다.

클라이언트 라우터 캐시는 레이아웃, 로딩 상태와 같이 공통적으로 쓰이는 요소에 대한 RSC Payload를 브라우저에 캐싱하는 기능입니다. 이를 통해 클라이언트 측에서 페이지 전환 시 캐싱된 데이터를 활용하기 때문에 빠른 탐색이 가능합니다. 또한 서버 부하가 줄어드는 효과도 있습니다.

데이터 캐시는 네트워크 요청에 대한 응답을 Next 서버에 캐싱하는 기능입니다. Next.js에서는 fetch()에 다양한 데이터 캐시 옵션을 적용할 수 있습니다. 예를 들면, { cache: 'force-cache' }을 통해 캐싱을 적용할 수 있습니다. revalidate 옵션을 통해 캐싱을 적용하되 일정 주기로 갱신하도록 설정할 수도 있습니다. 또한, { cache: 'no-store' }을 통해 캐싱 없이 항상 새로운 데이터를 가져오도록 설정할 수 있습니다.

끝으로, 풀 라우트 캐시는 서버에서 미리 생성된 페이지를 저장하고, 이후 동일한 요청이 들어오면 캐싱된 페이지를 즉시 제공하는 방식입니다. cookies(), headers()와 같은 Dynamic Function을 사용하거나 Route Segment Config를 동적 옵션으로 설정하지 않고, 데이터 캐시를 적용하면 풀 라우트 캐시가 활성화됩니다. fetch()에 revalidate 옵션을 설정하면 일정 주기로 페이지가 갱신되는 ISR 방식으로 동작하도록 설정할 수도 있습니다. 풀 라우트 캐시를 적용하면 페이지 로드 속도를 극대화할 수 있습니다.

</details>
<br/>

<details>
<summary>
🫥 Streaming SSR에 관하여 설명해주세요.
 </summary>
<br/>
`Streaming SSR`은 서버에서 렌더링된 HTML을 한 번에 완성해서 보내는 방식이 아니라, 준비된 부분부터 점진적으로 스트리밍해서 클라이언트에 전달하는 기술입니다. 이를 통해 사용자는 페이지의 중요한 콘텐츠를 더 빠르게 확인할 수 있습니다.

기존 SSR은 서버에서 모든 데이터를 처리한 뒤 완전한 HTML을 전송하는 반면, Streaming SSR은 서버가 데이터를 준비하는 즉시 HTML 조각을 스트림 형태로 보내고, 클라이언트는 이를 실시간으로 렌더링합니다. React 18에서는 `renderToPipeableStream API`를 통해 구현할 수 있으며, 이 API는 서버에서 HTML을 조각 단위로 스트리밍할 수 있도록 지원합니다. 예를 들어, onShellReady 옵션을 사용해 스트림을 응답으로 바로 전송할 수 있습니다.

```
renderToPipeableStream(<App />, {
  onShellReady() {
    res.setHeader('Content-Type', 'text/html');
    stream.pipe(res);
  },
});

```

이 방식의 가장 큰 장점은 초기 로딩 시간을 단축할 수 있다는 점입니다. HTML의 일부라도 준비되는 즉시 클라이언트가 렌더링을 시작하므로 TTFB(Time to First Byte)가 개선됩니다. 특히 데이터가 많거나 복잡한 대규모 애플리케이션에서 효과적이며, 사용자가 중요한 콘텐츠를 먼저 확인할 수 있어 전반적인 사용자 경험도 향상됩니다. 다만, 클라이언트에서 부분적으로 전송된 HTML을 제대로 Hydration할 수 있도록 설계가 필요하며, SEO나 캐싱 정책과의 호환성도 신중히 고려해야 합니다.

이러한 특징과 장점을 통해 Streaming SSR은 기존 SSR의 한계를 극복하며, 더욱 빠르고 효율적인 웹 페이지 렌더링을 가능하게 만듭니다.

## **스트리밍된 데이터와 리액트의 Hydration 과정에서 발생할 수 있는 문제는 무엇인가요? 🤔**

주요한 문제점은 렌더링 되는 HTML과 리액트의 **상태 불일치**라고 말씀드릴 수 있습니다.

HTML과 리액트 상태의 불일치 문제는 스트리밍된 HTML이 서버에서 먼저 클라이언트로 전송되고, 리액트가 실행되기 전까지는 그냥 정적인 상태로만 보여지는 데서 시작됩니다. 이후 Hydration 과정에서 이 HTML에 리액트의 상태와 이벤트 핸들러가 결합되는데, 이때 서버와 클라이언트 사이 데이터가 맞지 않으면 문제가 생길 수 있습니다.

예를 들어, 서버에서 렌더링된 데이터가 클라이언트에서 Hydration 시점에 변경되어 있다면 리액트가 경고를 띄우거나, 예상치 못한 UI 동작이 나타날 수 있습니다. 또, 비동기 데이터 처리를 Suspense로 하고 있다면, 데이터가 늦게 로드되면서 UI가 달라질 가능성도 있습니다.

## **그럼 이러한 불일치 문제를 해결하려면 어떻게 해야하나요? 🧐**

이런 문제를 막으려면, 서버와 클라이언트에서 동일한 데이터 소스를 사용해야 합니다. 예를 들어, Tanstack Query 같은 라이브러리를 활용하면 데이터를 동기화하기가 훨씬 수월해집니다. 또, Suspense와 fallback을 잘 활용하면, 데이터가 아직 준비되지 않았을 때도 안정적인 화면을 보여줄 수 있습니다. 이렇게 하면 사용자 입장에서 데이터가 로드되기 전에 UI가 흔들리는 문제를 줄일 수 있습니다.

</details>
<br/>

<details>
<summary>❓ Next.js를 사용하는 이유가 무엇인가요?</summary>
<br/>
React를 이용해서 웹 애플리케이션을 구현하기 위해서는 번들러 설정, 라우팅 설정, 다양한 렌더링 방식을 위한 추가 세팅 등 복잡한 과정을 거쳐야 합니다. 이러한 작업들은 시간과 노력이 많이 들며, 많은 개발자들에게 진입 장벽이 될 수 있습니다.

Next.js는 이러한 복잡한 과정을 생략하고, **기본적으로 설정된 환경에서 편하게 웹 애플리케이션을 개발할 수 있도록 도와줍니다**. 예를 들어, 파일 기반 라우팅 시스템은 별도의 라우팅 설정 없이 디렉토리 구조만으로 페이지를 생성할 수 있게 해줍니다. 또한, CSR, SSR, SSG 등 다양한 렌더링 방식을 내장되어 있는 기능만으로 쉽게 구현할 수 있게 해줍니다. 이외에도 이미지 최적화, 코드 스플리팅, 데이터 캐싱 등 현대적인 웹 애플리케이션에 필수적인 기능들을 기본적으로 제공합니다.

정리하면, Next.js는 React 기반 웹 개발의 복잡함을 줄여주며, 현대 웹 개발에서 요구되는 성능과 생산성을 모두 만족시키는 프레임워크이기 때문에 많은 개발자들이 선택하고 있습니다.

## **Next.js를 도입할 때의 단점은 없나요? 🤔**

앞서 말씀드린 것과 같이 Next.js는 많은 기능들이 기본으로 내장되어 있습니다. 이 특성이 Next.js의 장점이면서 동시에 단점으로 이어지기도 합니다.

첫째는, **구조상의 제약이 있기 때문에 커스터마이징하기 비교적 어렵다**는 점입니다. 많은 기능들이 기본 설정 및 추상화되어 있는 만큼, 기본 설정을 커스터마이징하기 어려운 경향이 있습니다. 예를 들면, Next.js는 디렉토리 구조에 기반한 라우팅 규칙이 정해져 있어서 자유로운 구조 설계가 어렵습니다.

둘째는, **러닝커브가 존재한다**는 점입니다. Next.js에서 제시하는 기본적인 구조와 규칙에 대해 이해해야 합니다. 더불어 React를 넘어선 새로운 개념들을 익혀야 하는 경우도 있고, Next.js의 버전이 업데이트될 때마다 변경사항을 추가로 학습해야 합니다. 이러한 점은 학습 부담을 높이는 원인이 됩니다.

</details>
<br/>

<details>
<summary> 🤞 Next.js Middleware </summary>

**Next.js의 미들웨어는 요청이 완료되기 전에 코드를 실행할 수 있게 해주는 기능**입니다. 미들웨어는 `middleware.ts` 파일로 프로젝트 루트나 `src` 디렉토리에 위치합니다. 서버 사이드에서 실행되며, 요청이 라우트 핸들러나 페이지에 도달하기 전에 동작합니다.
사용 예시를 들자면, 인증 및 권한 검사나 리다이렉션 처리, 요청/응답 헤더 수정 등 입니다.
Edge Runtime에서 실행되어 매우 빠른 성능을 제공하며, 그렇기에 Node.js API의 일부만 사용 가능합니다.

## Edge Runtime이란 무엇인가요? 🤔

Edge Runtime은 서버리스 환경에서 실행되는 경량화된 JavaScript 런타임입니다. CDN의 엣지 노드에서 코드를 실행하여 사용자와 가장 가까운 위치에서 빠른 응답을 제공합니다.
전 세계 여러 지역에 분산된 엣지 서버에서 코드를 실행하기에, 콜드 스타트가 거의 없고 매우 빠른 응답 시간을 가지고 있습니다.
그렇기에 fs나 워커 스레드 같은 기능들은 사용이 불가능하며, `fetch`나 `URL`, `URLSearchParams` 같은 기능들이 사용 가능합니다.

## 실제로 Middleware를 사용하신 적이 있나요? 🤔

실제 프로젝트에서는 주로 인증 검사와 리다이렉션 로직을 미들웨어로 구현했습니다.
예를 들어, 로그인하지 않은 사용자가 대시보드에 접근하려 할 때 로그인 페이지로 리다이렉트시킴으로써 서버단에서 처리하며 보안성을 높였습니다.

</details>
<br/>
