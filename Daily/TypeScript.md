<details>
<summary>😊 타입스크립트의 타입과 인터페이스의 차이점을 설명해주세요.
 </summary>
<br/>
**interface**는 **객체의 형태를 확장**하는 데 용이한 반면, **type**은 튜플, 인터섹션, 유니온 등을 이용하여 더 **복잡한 타입 정의 및 조합을 표현**하는 데 용이합니다.

먼저, **interface**는 선언 병합을 지원해 여러 번 선언할 수 있어, 주로 객체 타입을 **확장**할 때 유리합니다. 동일한 이름을 가진 interface를 여러 번 선언하면, 이 속성들이 자동으로 합쳐집니다. 예를 들면 다음과 같습니다.

```
interface Person {
  age: number;
  name: string;
  isBirthday: boolean;
}

interface Person {
  address: string;
}

const person1: Person = {
  age: 1,
  name: "abcd",
  isBirthday: false,
  address: "1010",
};

```

위 코드에서 Person interface를 여러 번 선언할 수 있으며, 결과적으로 하나의 interface로 병합됩니다.

반면, **type**으로 선언한 경우에는 동일한 이름을 중복 선언하면 에러가 발생합니다. 대신, **type**은 튜플과 같은 **복잡한 타입 표현**이 가능하며, **복잡한 타입 조합**을 위해 인터섹션(&)과 유니온(|) 연산자를 지원합니다.

예를 들어, type을 이용해 여러 타입을 조합하는 방식은 다음과 같습니다.

```
type BasicInfo = {
  name: string;
  age: number;
};

type ContactInfo = {
  email: string;
  phone: string;
};

// 인터섹션 타입 (&)을 사용해 두 타입을 결합하여 하나의 타입으로 생성
type PersonInfo = BasicInfo & ContactInfo;

const person2: PersonInfo = {
  name: "John",
  age: 30,
  email: "john@example.com",
  phone: "123-456-7890",
};

```

정리하자면, **interface**는 선언 병합을 통해 여러 번 선언이 가능하여 주로 객체 타입을 **확장**하는 데 유리하며, **type**은 튜플 등 복잡한 타입을 사용하고 유연한 연산자를 통해 복잡한 타입 조합을 **표현**하는 데 적합합니다.

</details>
<br/>
