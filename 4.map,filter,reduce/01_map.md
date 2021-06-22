
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

# filter

# reduce