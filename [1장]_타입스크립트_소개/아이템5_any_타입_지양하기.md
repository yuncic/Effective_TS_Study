# 아이템5 - any 타입 지양하기

```ts
let ageInYears: number;
ageInYears = "12";
// ~~ 'string' 형식은 'number' 형식에 할당할 수 없습니다.
ageInYears = "12" as any; // 정상
```

TS의 타입 체커를 통해 위의 코드에서 오류를 찾아냈다.
하지만 타입 단언으로 오류를 해결했다.
이렇게 하면 TS의 장점을 잃을 수 없게 된다.
그 이유를 알아보자.

### any 타입에는 타입 안정성이 없습니다.

앞의 예제에서 age는 number 타입으로 선언되었다.
그러나 as any를 사용하면 string 타입을 할당할 수 있게된다.
타입 체커는 선언에 따라 number 타입으로 판단할 것이고, 이로 인한 혼돈은 걷잡을 수 없게 될 것이다.

### any는 함수 시그니처를 무시해 버린다.

함수를 작성할 때는 시그니처를 명시해야 한다.
호출하는 쪽은 약속된 타입의 입력을 제공하고, 함수는 약속된 타입의 출력을 반환한다.
그러나 any 타입을 사용하면 약속을 어길 수 있다.

```ts
function calculateAge(birthDate: Date): number {
  // ...
}

let birthDate: any = "1990-01-19";
calculateAge(birthDate); //정상
```

birthData 매개변수는 string이 아닌 Date 타입이어야 한다.
any타입을 사용하면 calculateAge의 시그니처를 무시하게 된다.
JS에서는 종종 암시적으로 타입이 변환되기 때문에 이러한 경우 특히 문제가 될 수 있다.
string 타입은 number 타입이 필요한 곳에서 오류 없이 실행될 때가 있고, 그럴 경우 다른 곳에서 문제를 일으키게 된다.
