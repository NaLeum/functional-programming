함수형 프로그래밍에서는 코드를 값으로 다루는 아이디어를 자주 사용한다. 

코드를 값으로 다룰수있기 떄문에 어떠한 함수가 코드인 함수를 받아서 평가하는 시점을 원하는대로 다룰수가 있어서 코드의 표현력을 높인다던지 재밌고 좋은 아이디어를 많이 가지고 있다. 


    const products = [
        {name:'반팔티',price:15000},
        {name:'긴팔티',price:20000},
        {name:'헨드폰케이스',price:15000},
        {name:'후드티',price:30000},
        {name:'바지',price:25000},
    ];

    console.log(
        reduce(
            add, 
            map(p=>p.price, 
            filter(p=>p.price<20000, products))));

# 코드를 값으로 다루어 표현력 높이기

## go, pipe

go

    const go = (...args) => reuduce((a,f)=>f(a),args);

    go(
        0,
        a => a + 1,
        a => a + 10,
        a => a + 100,
        console.log 
    )

pipe

go 함수와 다르게 함수를 리턴하는 함수
go 함수가 인자와 함수들을 나열해서 즉시 값을 평가한다고 하면
pipe함수는 함수들을 나열해서 합성된 함수를 만든다. 


    const pipe = (f, ...fs) => (...as) => {
        go(f(...as), ...fs);
    };

    const f = pipe(
        a => a + 1,
        a => a + 10,
        a => a + 100, 
    );
    console.log(f(0))


    