---
layout: post
title:  "Functional Programming"
subtitle: "함수형 프로그래밍"
date:   2019-01-27 21:03:00
type: "Functional Programming"
development: true
text: true
author: "Choi corder"
---

# 함수형 프로그래밍

## 1일차 - 함수형 프로그래밍 개요

이 글은 Inflearn에서 유인동님의 함수형 프로그래밍 강좌를 보고 작성한 개인적인 공부글입니다.

성공적인 프로그래밍이란?  
모든 프로그래밍 패러다임은 성공적인 프로그래밍을 위해 존재합니다 -> 성공적인 프로그래밍은 좋은 프로그래밍을 만드는 일이고 ->
좋은 프로그램은 사용성, 성능, 확장성, 기획 변경에 대한 대응력 등이 좋습니다 -> 이것들을 효율적이고 생산적으로 이루는 일을 성공적인 프로그래밍이라고 합니다.

함수형 프로그래밍이란?
함수형 프로그래밍은 성공적인 프로그래밍을 위해 부수 효과를 미워하고 조합성을 강조하는 프로그래밍 패러다임 입니다.
* 부수 효과를 미워한다. -> 순수 함수를 만든다.
 - 순수 함수는 부수 효과가 없는 수학적 함수
 - 순수 함수 들어온 인자가 같으면 항상 동일한 결과를 리턴하는 함수
 - 함수가 받은 인자외에 다른 외부 상태에 영향을 끼치지 않는 함수
 - 리턴값 외에는 외부와 소통하는 것이 없는 함수를 의미한다.
* 조합성을 강조한다. -> 모듈화 수준을 높인다.
 - 순수 함수들의 조합으로 프로그래밍을 한다.
* 순수 함수 -> 오류를 줄이고 안정성을 높인다.
* 모듈화 수준이 높다. -> 재사용이 높아서 생산성을 높다.

- 순수 함수
```javascript
function add(a, b) {
    return a + b;
}

console.log(add(2, 5));
console.log(add(2, 5));
console.log(add(2, 5));
```
add함수는 순수 함수라고 할 수 있습니다. 그 이유는 항상 동일한 인자를 주면 동일한 결과를 리턴하기 때문입니다.
2번째는 부수 효과가 없기 때문입니다.  

- 순수 함수가 아닌 함수
동일한 인자를 주었을때 상황에 따라 결과값을 달리주는 함수는 어떤 함수일까요?
```javascript
var c = 27;
function add2(a, b) {
  return a + b + c;
}

console.log( add2(10, 2) ); // 39
console.log( add2(10, 3) ); // 40
console.log( add2(10, 4) ); // 41
c = 20;
console.log( add2(10, 2) ); // 32
console.log( add2(10, 3) ); // 33
console.log( add2(10, 4) ); // 34
```
만일 이 함수 안에서 참조하고 있는 c라는 변수가 프로그래밍 동작에서 변화가 있을 수 있다고 가정한다면,
이 함수는 순수 함수가 아니게 됩니다.

하지만 c라는 함수가 상수로서 존재하게 된다면 순수 함수라고 볼 수 있습니다.

중간에 c라는 변수를 20으로 변경한다면, 결과값이 달라지게 됩니다.
결과값이 달라지는 함수는 순수 함수가 아니게 됩니다.


- 2번째로 순수 함수가 아닌 함수는 부수 효과를 일으키는 함수입니다.
부수 효과는 외부의 상태를 변경, 들어온 인자의 상태를 직접 변경하는 함수 등을 의미합니다.

```javascript
// add3은 a와 b를 더하지만 c를 b로 덮어씌우게 되어 c의 값을 변경하게 됩니다.

var c = 20;
function add3(a, b) {
  c = b;
  return a + b;
}

console.log('c: ', c); // 20
console.log( add3(20, 30) ); // 50
console.log('c: ', c); // 30
```
처음에 출력한 c와 마지막에 출력한 c의 값은 서로 달라지게 됩니다. 중간에 `c = b;`라는 부분 때문에
마지막의 c의 출력이 달라지게 됩니다.

- 순수 함수가 아닌 또 다른 함수
```javascript
var obj1 = { val: 10 };
function add4(obj, b) {
  obj.val += b;
}
console.log( obj1.val );
add4(obj1, 20);
console.log( obj1.val );
```






