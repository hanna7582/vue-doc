# axios - HTTP 통신 라이브러리
[axios 공식 문서](https://github.com/axios/axios)
 
`Promise based HTTP client for the browser and node.js`

Promise 기반으로 만들어진 브라우저 및 node.js를 위한 HTTP 클라이언트 라이브러리로써, 비동기 방식으로 HTTP 데이터 요청을 실행한다.  
복잡한 XMLHttpRequest를 다루지 않고 AJAX 호출을 할 수 있다.

<!-- restful 개념 https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html -->

## 주요 메서드 
- axios.request(config)
- axios.get(url[, config])
- axios.delete(url[, config])
- axios.head(url[, config])
- axios.options(url[, config])
- axios.post(url[, data[, config]])
- axios.put(url[, data[, config]])
- axios.patch(url[, data[, config]])

## axios 라이브러리 설치
> npm i axios

## axios 예제
`FormApp.vue`
```html
<template>
  <div>
    <h3>등록</h3>
    <form @submit.prevent="submitForm">
          <div>
              <label for="username">id</label>
              <input type="text" id="username" v-model="username">
          </div>
          <div>
              <label for="password">password</label>
              <input type="password" id="password" v-model="password">
          </div>
          <button type="submit">login</button>
    </form>
   
    <h3>조회</h3>
    <input type="text" v-model="id">
    <button @click="getUser">조회</button>
    <ul class="result" v-show="result">
      <li>id:{{result.id}}</li>
      <li>name:{{result.name}}</li>
      <li>username:{{result.username}}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name:'formApp',
  data:function () {
    return {
      username:'',
      password:'',
      id:'',
      result:'',
    }
  },
  methods: {
    submitForm:function(){
      // e.preventDefault();      
      var url='https://jsonplaceholder.typicode.com/users';
      var data={
        username:this.username,
        password:this.password
      }      
      axios.post(url, data)
      .then((res)=>{
        console.log(res);        
      })
      .catch((err)=>{
        console.log(err);        
      });
    },
    getUser:function(){
      // 화살표 함수를 적용하지 않을 때는  // var vm = this;로 접근
      // 화살표 함수로 적용시       
      axios.get('https://jsonplaceholder.typicode.com/users?id='+this.id)
      .then(res => {
        console.log(res.data[0]);
        //vm.result=res.data[0];
        this.result=res.data[0];  
      })
      .catch((err)=>{
        console.log(err);        
      });
    }
    
  },
}
</script>
```



