# for of, 전개 연산자, 구조 분해, 나머지 연산자

제너레이터는 이터러블/이터레이터 프로토콜을 따르고 있기 때문에 for of, 전개 연산자, 구조분해, 나머지 연산자 등, 자바스크립트의 이터러블/이터레이터 프로토콜을 따르고 있는 함수들과 같이 잘 사용할 수 있다. 

<code>

    console.log(...odds(10));
    console.log(...odds(10),...odds(20));

    const [head, ...tail] = odds(5);
    console.log(head);
    console.log(tail);

    const [a, b, ...rest] = odds(10);
    console.log(a);
    console.log(b);
    console.log(rest);
</code>