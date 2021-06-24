
    const products = [
        {name:'반팔티',price:15000},
        {name:'긴팔티',price:20000},
        {name:'헨드폰케이스',price:15000},
        {name:'후드티',price:30000},
        {name:'바지',price:25000},
    ];

    let names = [];
    for (const p of products){
        names.push(p.name)
    }
    console.log(names);

    let prices = [];
    for (const p of products){
        prices.push(p.price)
    }
    console.log(prices);

# map

    const map = (f,iter) => {
        let res = [];
        for (const a of iter){
            res.push(f(a));
        }
        return res;        
    }
함수형 프로그래밍에서는 인자와 리턴값으로 소통하는 것을 권장한다. 

    map(p=> p.name, product);
    map(p=> p.price, product);


# 이터러블 프로토콜에 따른 map의 다형성
    console.log(document.querySelector("*").map(el => el.nodeName));
의 결과 값은 Array처럼 생겼지만 .map을 통해서 순회할 수 없다.
    console.log([1,2,3].map(a=>a+1));
은 순회할 수 있다.

그 이유는 document.querySelectorAll은 Array를 상속받는 객체가 아니기 때문이다.
그래서 프로토타입에 map함수가 구현이 되어있지 않다. 

앞에서 만들었던 map함수는
    
    map(el => el.nodeName,document.querySelector("*"))
가 동작을 한다. 그 이유는 document.querySelectorAll이 이터러블 프로토콜을 따르고 있기 때문이다. 

    const it = document.querySelectorAll("*")[Symbol.iterator];
이렇게 이터레이터가 있다.

    let m = new Map();
    m.set('a',10);
    m.set('b',20);
    const it = m[Symbol.iterator]();
    console.log(m.next());
    console.log(m.next());
    console.log(m.next());
    console.log(new Map(map(([k,a])=> [k,a*2],m);));
이런식으로 위에 만들었던 Map 객체를 map함수로 순회하며 새로운 Map객체르 만들어낼수있다. 


# filter
조건에 맞춰서 걸러주는 함수

명령형

    let under20000 = [];
    for(const p of products){
        if(p.price < 20000) under20000.push(p);
    }
    console.log(...under20000);
다른 조건일때는 코드를 복사해서 사용한다. 

    let over20000 = [];
    for(const p of products){
        if(p.price > 20000) over20000.push(p);
    }
    console.log(...over20000);

리팩토링

    const filter = (f,iter) => {
        let res = [];
        for(const a of iter){
            if(f(a)) res.push(a)
        }
        return res;
    }

    console.log(...filter(p => p.price < 20000, products));

    console.log(...filter(p => p.price > 20000, products));

    console.log( filter(n => n%2, function *(){
        yield 1;
        yield 2;
        yield 3;
        yield 4;
        yield 5;
    }()))
    
# reduce
reduce는 값을 축약하는 함수. 이터러블 값을 하나의 값으로 축약하는 함수

    const nums = [1,2,3,4,5];
    
    //명령형
    let total = 0;
    for(const n of nums){
        total = total + n;
    }
    console.log(total);

함수 구현

    const reduce = (f,acc,iter) => {
        if(!iter){
            iter = acc[Symbol.iteractor]();
            acc = iter.next().value;
        }
        for(const a of iter){
            acc = f(acc,a);
        }
        return acc;
    }

    const add = (a,b) => a+b;
    console.log(reduce(add,0,[1,2,3,4,5]));

    console.log(reduce(add,0,[1,2,3,4,5]));

reduce같은 경우에는 받은 함수로 어떻게 축약할지 전부 위임한다. 

    console.log(reduce((total_price,product) => total_price+product.price , 0 ,products));

