## async / await

기존의 자바스크립트에서 비동기 코드를 작성할때에는 callback 혹은 promise를 사용했는데, 이를 대체하는 새로운 비동기 코드의 작성방법이다. 
이를 사용하면, 비동기 코드의 스타일이 동기식 코드의 스타일과 유사하게 만들어 코드를 더욱 간결하게 만드는 장점이 있다. 

## 장점

### 에러처리

async/await는 동기와 비동기 에러 모두를 try/catch를 통해서 처리할 수 있게 한다. 
promise를 사용한 것과 async/await를 사용한 예제를 비교해 보자

- promise
~~~
const makeRequest = () => {
  try {
    getJSON()
      .then(result => {
        // this parse may fail
        const data = JSON.parse(result)
        console.log(data)
      })
      // uncomment this block to handle asynchronous errors
      // .catch((err) => {
      //   console.log(err)
      // })
  } catch (err) {
    console.log(err)
  }
}
~~~

promise를 사용한 위의 예제에서 JSON.parse가 오류가 발생하더라도 catch 구문은 실행되지 않는다. 
promise안에서 발생한 에러이기 때문이다. 에러처리를 위해서는 promise상에서 .catch를 호출해야 한다. 

- async/await
~~~
const makeRequest = async () => {
    try {
        const data = JSON.parse(await getJSON());
        console.log(date);
    } catch (err) {
        console.log(err);
    }
}
~~~
async/await 에서는 catch 블록에서 에러를 출력할 수 있다. 

비교해 보면 알겠지만 코드가 훨씬 더 간결해 진다. 

### promise 연쇄

promise가 연쇄적으로 발생하는 경우를 생각해 보자. 

~~~
const makeRequest = () => {
  return promise1()
    .then(value1 => {
      // do something
      return promise2(value1)
        .then(value2 => {
          // do something          
          return promise3(value1, value2)
        })
    })
}
~~~

이렇게 작성된 코드는 코드의 가독성을 훼손시킨다. 이를 async/await를 사용해서 구현하면 다음과 같이 
바꿀 수 있다. 

~~~
const makeRequest = async () => {
  const value1 = await promise1()
  const value2 = await promise2(value1)
  return promise3(value1, value2)
}
~~~