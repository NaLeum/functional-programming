# 제너레이터/이터레이터
- 제너레이터 : 이터레이터이자 이터러블을 생성하는 함수

<code>

    function *gen(){
        yield 1;
        yield 2;
        yield 3;
        return 100;
    }

    let iter = gen();
    console.log(iter.next());
    console.log(iter.next());
    console.log(iter.next());
    console.log(iter.next());    

    console.log(iter[Symbol.iterator]()===iter);

    for(const a of gen()) console.log(a)
    // 순회할때 리턴값이 없이 순회한다. 
</code>

제너레이터는 순회할 값을 문장으로 표현한것이라고 말할 수 있다.

자바스크립트에서는 어떤 이터러블이라도 순회할 수 있다. 

제너레이터는 순회할 수 있는 값을 만들 수 있다. 

자바스크립트에서는 제너레이터를 통해서 어떤한 상태나 값이든 순회할 수 있는 값으로 만들 수 있다. 


# odds
제너레이터를 활용해서 홀수만 발생하여 순회하는 함수를 만들어보자

<code>

    function *odds(){
        yield 1;
        yield 3;
        yield 5;
        yield 7;
        
    };

    let iter2 = odds();
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());
     

자동으로 만들어보자
    
    function *odds(limit){
        for(let i = 0; i< limit; i++){
            if(i%2) yield i;
        }
    }
    let iter2 = odds(10);
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());    
    console.log(iter2.next());    

다른것도 만들어보자

    // 무한히 증가하는 이터레이터 
    function *ifinity(i=0){
        wihile(true) yield i++;
    }
이터레이터의 next를 평가할떄까지만 동작하기 때문에 브라우저가 멈추지 않는다. 

둘을 합쳐보면 
    
    function *odds(limit){
        for(const a of infinity(1)){
            if(a%2) yield i;
            if(a === limit) return;
        }
    }
    let iter2 = odds(10);
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());    
    console.log(iter2.next());  

리미트를 받는 제너레이터를 만들게되면 

    // 리미트를 받는 제너레이터
    function *limit(l,iter){
        for(const a of iter){
            yield a;
            if(a === l) return;
        }
    }

    function *odds(l){
        for(const a of limit(l,infinity(1))){
            if(a%2) yield i;
        }
    }
    let iter2 = odds(10);
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());    
    console.log(iter2.next());  
</code>

# for of, 전개 연산자, 구조 분해, 나머지 연산자
