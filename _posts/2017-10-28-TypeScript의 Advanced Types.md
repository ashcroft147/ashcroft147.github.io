---
layout: post
title: TypeScript의 Advanced Types
comments: true
---

## union Type

union 타입은 변수의 타입을 복수의 유형으로 설정하는 것을 말한다. 

~~~
/**
 * padding을  value의 왼쪽에 padding 을 덧붙이는 함수
 */
function padLeft(value: string, padding: any) {
    if (typeof padding === "number") {
        return Array(padding + 1).join(" ") + value;
    }
    if (typeof padding === "string") {
        return padding + value;
    }
    throw new Error(`Expected string or number, got '${padding}'.`);
}

padLeft("Hello world", 4); // returns "    Hello world"
~~~

위의 예제를 보면 padLeft 함수는 padding의 type이 any type으로 정의되어 있어서,
아래의 padding의 값의 타입이 boolean 경우에 코드를 실행시켜도 compile time 에 에러가 발생하지 않는다.  

~~~
let indentedString = padLeft("Hello world", true); 
~~~

하지만 실제 padLeft 함수는 number 및 string 타입의 변수에 대해서만 처리하고 나머지는 모두 Error 처리를 하기 때문에 실제 유의미한 타입은 string, number 만 이며
코드를 변경하면 boolean 값이 paddding에 할당되면 compilation error를 발생한다. 

~~~
function padLeft(value: string, padding: string | number) { }
let indentedString = padLeft("Hello world", true); 
~~~

만약 아래 코드의 pet 변수와 같이 getSmallPet() 함수로부터 union type 객체를 리턴 받으면, pet 변수는 union type에 속한 멤버 중 공통 멤버변수만 접근할 수 있다. 
~~~
interface Bird {
    fly();
    layEggs();
}

interface Fish {
    swim();
    layEggs();
}

function getSmallPet(): Fish | Bird {
    // ...
}

let pet = getSmallPet();
pet.layEggs(); // okay
pet.swim();    // errors
~~~

## never Type

## nullable Type

## 참고자료
 - [TypeScript - Advanced Types](https://www.typescriptlang.org/docs/handbook/advanced-types.html)