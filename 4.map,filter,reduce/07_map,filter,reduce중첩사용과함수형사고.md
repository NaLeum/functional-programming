
    const products = [
        {name:'반팔티',price:15000},
        {name:'긴팔티',price:20000},
        {name:'헨드폰케이스',price:15000},
        {name:'후드티',price:30000},
        {name:'바지',price:25000},
    ];

    console.log(map(p=>p.price, products));

    // 금액들을 뽑는데 특정 금액 이하의 제품만 뽑고싶다.

    console.log(map(p=>p.price, filter(p=>p.price<20000, products)));

    // 2만원 미만의 모든 상품의 가격을 다 합친 가격을 알 고 싶다. 

    console.log(
        reduce(
            add, 
            map(p=>p.price, 
            filter(p=>p.price<20000, products))));
    // 오른쪽에서부터 왼쪽으로 읽어가면 된다.

이런식으로도 작성할 수 있다. 

    console.log(
        add,
        filter(n => n < 20000,
        map(p=>p.price,products))
    )
함수형 프로그래밍에서는 함수들을 실행하고 중첩하고 사용하면서 값들을 평가해하는 식으로 사용하게 됩니다. 

