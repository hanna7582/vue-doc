# Vue Router 
[Vue Router 공식 문서](https://router.vuejs.org/)
  
## 화면 전환
| 구분 | 구조 | 처리
| --- | --- | --- 
| 서버 사이드 라우팅 | url에 해당하는 html파일이 1개씩 존재 | 서버에서 결정 
| 클라이언트 사이드 라우팅 | 하나의 html을 사용하고 js를 사용하여 변경 | 클라이언트에서 결정 

### 서버 사이드 라우팅 처리과정
1. 클라이언트가 서버에 페이지를 요청한다.
2. 서버는 요청받은 url에 해당하는 html파일을 찾는다.
3. 서버는 찾아온 html에 필요한 내용을 추가적으로 담는다.
4. 완성된 html을 클라이언트에 응답으로 보내준다.

### 클라이언트 사이드 라우팅 처리과정
1. 클라이언트가 서버에 페이지를 요청한다.
2. 서버는 index.html파일을 찾아 응답으로 보내준다.
3. 클라이언트는 현재 url에 따라 페이지의 내용을 결정하고 그린다.
4. 추가로 필요한 정보는 클라이언트에서 서버로 ajax를 이용하여 요청한다.
   
## 사용예시
```html
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
    <div id="app">
        <div>
            <router-link to="/login">login</router-link>
            <router-link to="/main">main</router-link>
        </div>
        <router-view></router-view>
    </div>
    <script>
        var LoginComponent = {
            template: '<div>login page</div>'
        }
        var MainComponent = {
                template: '<div>main page</div>'
            }
            //라우터 인스턴스 생성
        const router = new VueRouter({
            // url의 #값을 제거
            mode: 'history',
            //페이지의 라우팅 정보
            routes: [{
                //페이지의 url이름
                path: '/login',
                component: LoginComponent
            }, {
                path: '/main',
                component: MainComponent
            }]
        })

        new Vue({
            el: '#app',
            components: {
                LoginComponent,
                MainComponent
            },
            //라우터 등록
            router: router,
            data: {

            }
        })
    </script>
```