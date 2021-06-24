## curry
코드를 값으로 다루면서 원하는 시점에 평가하는것. 

함수를 받아서 함수를 리턴하고 인자를 받아서 인자가 원하는 갯수만큼 들어왔을 때, 받아두엇던 함수를 나중에 평가시키는 함수이다. 

    const curry = f => 
    (a, ..._) => _.length ? 
    f(a,..._) : (..._) => f(a,..._); 

    const mult = curry((a,b) => a*b);
    console.log(mult(1)(2));

    const mult3 = mult(3);
    console.log(mult3(10));

이러한 함수가 있다는 것은 아래의 코드를 더 간결하게 만들 수 있다. 

변환전

    go(
        products,
        products => filter(p=>p.price < 20000, products),
        products => map(p=>p.price, products),
        prices => reduce(add,prices),
        console.log
    );


변환후

    const map = curry( (f,iter) => {
        let res = [];
        for (const a of iter){
            res.push(f(a));
        }
        return res;        
    } )

    const filter = curry( (f,iter) => {
        let res = [];
        for(const a of iter){
            if(f(a)) res.push(a)
        }
        return res;
    } )

    const reduce = curry( (f,acc,iter) => {
        if(!iter){
            iter = acc[Symbol.iteractor]();
            acc = iter.next().value;
        }
        for(const a of iter){
            acc = f(acc,a);
        }
        return acc;
    } )

 모든 함수에 curry를 적용해준 후

    go(
        products,
        products => filter(p=>p.price < 20000 )(products),
        products => map(p=>p.price)(products),
        prices => reduce(add)(prices),
        console.log
    );    

이렇다는 이야기는 products를 받아서 그대로 전달한다는 뜻이 되고 이를 코드로 다시 수정하면

    go(
        products,
        filter(p=>p.price < 20000),
        map(p => p.price),
        reduce(add),
        console.log
    );    