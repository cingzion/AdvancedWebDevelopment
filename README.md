## 课时1：基础概述：类库和框架的区别以及市场中主流框架的现状
- 1、类库
> JQuery、Zepto、underscore....
类库提供的是真实项目中常用到的方法，它是一个工具包，基于这个工具包可以快速开发任何的项目
- 2、插件
> TAB选项卡插件、Banner轮播图片插件、Dialog模态框插件、Drag拖拽插件...
> isCroll局部滚动插件、jQuery中有发遥插件
插件是把项目中东某一个具体的功能进行封装

- 3、UI组件
> bootstrap、swiper、mui、妹子UI...
UI组件库一般是多个插件的集合体，不公提供了JS对应的功能，而且把结构、样式等也都实现了，我们只需要做一名 CV 工程师就可以快速构建一个产品

- 4、框架
> vue、react、umi-app、react native、flutter、angular(NG)
>、backbone...
一般来说，框架是类库和组件综合体，里面提供了大量供我们操作的方法，也有配套的UI组件库供我们快速开发; 框架是具备独立的编程思想的，例如：Vue是MVVM思想，让我们告别传递的DOM操作，按照视图和数据的相互渲染来完成项目开发，但是不管怎么变，都一定会比我们之前基于原生操作更简单，性能更好....

- 市面上常用的框架: vue(MVVM)  /  react(MVC)

- APP框架：umi-app / react native / flutter

- Vue 我们现在学习和使用的是第二代版本：尤雨溪


## 课时2：VUE是渐进式框架
> 什么是渐进式框架：类库或者框架都是重量级的，里面包含很多方法，但是实际项目开发中，我们用不到这么多东西，所以在开发他们的时候，会把功能按照模块进行单独开发，使用者可根据自身情况选择一个模块一个模块的导入使用

- vue：基础模块(基础语法、核心实现、组件开发、相关指令等都在这里)
- vue-router: 构建 SPA 单页面应用的路由
- vuex: 公共状态管理
- vue-cli: vue脚手架
- components: vue element、iview、 vux...
- axios、fetch 
- ... 这些东西就是 VUE 全家桶


## 课时3：VUE是MVVM双向数据绑定的框架
- MVC & MVVM
> 传统操作 DOM 模式
- MVC: model view controller
- MVVM: model view viewModel

- VUE 是  MVVM 框架
> MVVM是双向数据绑定的框架：vue 本身实现了数据和视图的相互监听影响

> MVC 是单向数据绑定，数据更改可以渲染视图，但是视图更改没有更改数据，需要我们自己在控制层基于 change 事件实现更改(React)
  1. m: mode 数据层
  2. v: view 视图层
  3. vm: viewModel 数据和视图的监听层(当数据或者视图发生改变、vm层会监听到，同时把对应的另外一层特跟着改变或者重新渲染)
    + 数据层改变：vm 会帮我们重新渲染
    + 视图层改变：vm 也会帮我们把数据重新更改

- 1、传统的方式
```jsx harmony
    <body>
        <div id="app"></div>
    
        <!--  import js  -->
        <script>
            // 传统的方式
            // 把 msg 数据绑定在页面 #app 中，一秒后，让数据更改，同时希望视图也跟着更改
            let msg = 'hello world~~~';
    
            setTimeout(() => {
                msg = '你好世界~~~';
                app.innerHTML = msg;
            }, 1000);
    
    
            let app = document.getElementById('app');
    
            app.innerHTML = msg;
        </script>
    </body>
```

- 2、案例
```jsx harmony
    <!doctype html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport"
              content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <div id="app">
            {{ msg }}
        </div>
    
        <div id="box">
            <p>{{ n }}</p>
            <div>
                <button @click="handle">点我呀~~~</button>
                <button v-on:click="handle">点我呀~~~</button>
            </div>
        </div>
    
        <!--  import js  -->
        <script src="../node_modules/vue/dist/vue.js"></script>
        <script>
            // 传统的方式
            // 把 msg 数据绑定在页面 #app 中，一秒后，让数据更改，同时希望视图也跟着更改
            let msg = 'hello world~~~';
    
    
    
            // => 每当创建一个实例，就相当于创建一个 vieModel 监听器：可以监听对应视频和对应数据相互改变
            let vm1 = new Vue({
                el: '#app', // => el: element 当前监听器监听的视图(基于 querySelector 获取 )
                data: {     // => data: 当前监听器监听的数据(这些监听的数据会挂载到 vm1 实例上, 也就是 vm1.msg=xxx来操作了)
                    msg,
                }
            });
    
            setTimeout(() => {
                vm1 = '你好世界~~~';
            }, 1000);
    
            /*------------------------------------------*/
            let vm2 = new Vue({
                el: '#box',
                data: {
                    n: 0,
                },
                methods:{// => methods 放视图、需要使用的方法
                    handle(){
                        // this:vm2
                        this.n++;
                    }
                }
            })
    
            // 传统的写法
            /*let box = document.querySelector('#box'),
                span = box.querySelector('p'),
                button = box.querySelector('button');
    
            span.innerHTML = 0;
            button.onclick = () => {
                span.innerHTML++;
            }*/
    
        </script>
    
    </body>
    </html>
```

- 案例
```jsx harmony
    <!doctype html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport"
              content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <div id="app">
            <label>人民币：￥ <input type="text" v-model="priceRMB"></label>
            <br>
            <label>美元：$ <span>{{ priceRMB / 7.1477 }}</span></label>
        </div>
        <!-- import js -->
        <script src="../node_modules/vue/dist/vue.js"></script>
        <script>
            // => model 先实现把数据绑定到视图层(给 input 设置 value 值), 然后监听文本框内容的改变，一旦改变，会把数据也跟着变;视图会重新的渲染
            let vm = new Vue({
               el: '#app',
               data: {
                   priceRMB: 0
               }
            });
        </script>
    </body>
    </html>
```

## 课时4：VUE的基础语法：数据修改时的细节问题
- 案例
```jsx harmony

    <!doctype html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport"
              content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <div id="app">
            <p>{{obj.name}}</p>
            <p>{{arr}}</p>
        </div>
        <!-- import js -->
        <script src="../node_modules/vue/dist/vue.js"></script>
        <script>
            let obj = {
                // name: '',
            };
    
            let arr = [10];
    
            let vm = new Vue({
                // => 基于 querySelector 获取视图容器: 指定的窗口不能是 html 和 body, 也就是说：不能在 body 和 html 上面绑定 id
                el: '#app',
                data: {
                    /**
                     * 在胡子语法中绑定的数据值是对象类型，会基于 JSON.stringify 把其编译为字符串再呈现出来(而不是直接 toString 处理的)
                     *
                     *
                     * 并不是所有的数据更改最后都会通知视图生新渲染
                     *   1、初始化数据是一个对象，对象中没有 xxx 健值对，后期新增的键值对是不不会让视图重新渲染的,
                     *      解决办法：
                     *          + 最好在初始化数据的时候，就把视图重需要的数据提前声明好(可以是空值，但是要有这个属性) =》 原理：只有 data
                     *            中初始化过的属性才有 get/set
                     *
                     *          + 不要修改某个属性名，而是把对象的值整体替换(指向新的堆内存)
                     *
                     *          + 可以基于 vm.$set内置方法修改数据：vm.$set(obj, key, value)
                     *
                     *  2、如果数据是一个数组， 们修改数据基于 arr[n]=xxx或者 arr.length-- 等
                     *     操作方式，是无法让视图重新渲染的; 需要基于：
                     *     + push/pop等内置的方法
                     *     + 重新把 arr 的值重写(指向新的夫内存)
                     *     + vm.$set
                     *
                     */
                    obj,
                    arr,
                }
            });
    
            // 修改数据
            setTimeout(() => {
    
                // 第一种方式
                // vm.obj.name = "微信：88888888"
    
                // 第二种方式
                /*vm.obj = {
                    ...obj,
                    name: '深圳'
                }*/
    
                // 第三种方式
                // vm.$set(vm.obj, 'name', '中国·深圳' );
    
    
                // vm.arr[1] = 20;  // 这样修改数据是没有用的。
                // vm.arr.length--; // 这样修改数据是没有用的。
    
                // vm.arr = [...arr, 20]
                // vm.arr.push(20);
                vm.$set(vm.arr, 1, 20);
    
            }, 1000)
        </script>
    </body>
    </html>
```

## 课时5：VUE的常规指令1
> 常用的指令( directive )
- v-model
- v-html / v-text: 取消小胡子语法刷新中的闪烁问题
- v-bind( 缩写 )
- v-once
- v-if 和 v-show
- v-for
    + for in 循环 & for of 循环
        - 遍历数据类型的范围
        - 原型上方法遍历( 或者数组增 xxx:xxx 属性遍历 )
        - ....
    + Symbol.iteratoer: Array、Set、Map、String、Arguments、NodeList....
- v-on 事件绑定
    + v-on:xxx
    + methods: 和 data 类型，都会把方法持载到 vm 实例上 ( this都是当前实现 )
    + @xxx
    + @xxx="func" & @xxx="func($event,...)"

> 案例如下：
```jsx harmony

    <!doctype html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport"
              content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <!--
            vue 指令：directive
                1、都是按照 v-xxx处理的，它是 vue 中规定给元素设置自定义属性
                2、当 vue 加载成功并进行处理的时候，会按照相关的规则解析和渲染视图，遇到对应的指令实现对应的功能
    
            v-model 一般给表单元素设置，实现表单元素和数据之前的相互绑定
                1) 先把数据绑定给表单元素，一般把数据 赋值给表单元素的 value
                2) 监听表单元素的内容改变
                3) 内容改变后，会把对应的数据也改变
                4) 对应的数据改变，视图中所有用到的数据的地方都会重新渲染
                视频 <=> 数据
                在 vue 框架中给表单元素设置 value 等属性是没有意义的
    
           v-html / v-text: 给非表单元素设置内容，v-html 支持对于标签的自识别，v-text 会把所有内容部分当做文本
                传统的胡子语法，在 vue 没有加载完成之前，会把 {{ xxx }} 展示在页面中，当 vue 加载完才会出现真正的内容，这样体验不好
                <span v-html="msg" />
    
           v-bind: 给元素的内置属性动态绑定数据，例如：给 img 绑定动态的图片路径地址
                   可以简写成为 ：, 也就是 v-bind:src 等价于 ：src
                    <img :src="pic" height="560" width="640" border="1px solid red"/>
    
           v-once: 绑定的数据是一次性的，后面不论数据怎么改变，视图也都不会重新渲染
                   <span v-once v-html="msg" />
    
           v-if: 如果对应的值是 true， 当前元素会在结构中显示，如果是 false，当前元素会在结构中移除(它控制的是加载和卸载的操
                 作 =>  DOM 的增加和删除) ；还有对应的 v-else-if / v-else 等指令
    
           v-show: 和 v-if类似，只不过它是控制元素样式的显示隐藏(display的操作)
    
                   1) v-if 是控制组件存在不存在，对于结果是 false，不存在的组件来说，视图渲染的时候无需渲染这部分内容；而 v-show
                      则不行，因为不管是显示还是隐藏，结构都在，所以视图渲染的时候这部分也要渲染；
    
                   2) v-show 在过于频繁的切换操作中，v-if明显要比 v-show 要低一些
    
    
    
        -->
        <div id="app">
            <button v-html="msg" @click="handleShow"></button>
            <br />
            <img :src="pic" alt="" v-if="show"/>
        </div>
        <!-- import js -->
        <!--  开发的时候尽可通用引用未压缩版本，这样有错误会抛出异常  -->
        <script src="../node_modules/vue/dist/vue.js"></script>
        <script>
            let vm = new Vue({
                el: '#app',
                data: {
                    // => 这里的数据最后都会做为实例的属性挂载到实例的属性挂载到实现 vm.show....
                    msg: '隐藏图片',
                    show: false,
                    pic: '2.jpg',
                },
                methods: {
                    // => 这里的方法最后也会挂载到实例的私有属性上
                    handleShow(){
                        this.show = !this.show;
                        this.msg = this.show ? '隐藏图片' : '显示图片';
                    }
                }
            });
    
        </script>
    </body>
    </html>
```

## 课时6：VUE的常规指令2：循环处理
```jsx harmony
    
    <!doctype html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport"
              content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <!--
            v-for: 循环动态绑定数据
                   想循环谁就给谁设置 v-for
                   循环类似 for/for in 的语法: v-for='(item, index) in arr'
    
        -->
        <div id="app">
            <table>
                <thead>
                    <tr>
                        <th>编号</th>
                        <th>姓名</th>
                        <th>年龄</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(item, index) in arr">
                        <td v-html='item.id' />
                        <td v-html='item.name'/>
                        <td v-html='item.age'/>
                    </tr>
                </tbody>
            </table>
        </div>
        <!-- import js -->
        <!--  开发的时候尽可通用引用未压缩版本，这样有错误会抛出异常  -->
        <script src="../node_modules/vue/dist/vue.js"></script>
        <script>
            let vm = new Vue({
                el: '#app',
                data: {
                    arr: [
                        {id: 1, name: '张三', age: 25, },
                        {id: 2, name: '李四', age: 24, },
                        {id: 3, name: '王五', age: 26, },
                    ]
                },
                methods: {
    
                }
            });
    
        </script>
        <script>
            // JS 中循环的几种方式： for循环、while循环、do while循环 | for in 循环 | for of 循环
            let arr = [10, 20, 30, 40],
                obj = { name: '深圳', year: 10, 1: 100};
    
            Object.prototype.AA = 12;
    
            // => ES6新增 for of 循环
            // 1、获取的不是属性名是属性值
            // 2、不会遍历原型上公有的属性方法(哪怕是自定义的)
            /*for(let item of arr) {
                console.log(item); // 是值
            }*/
            // 3、只能遍历被迭代的数据类型值(Symbol.iterator): Array, String、Arguments、NodeList、Set、Map等，但是普通对象不可能被迭代的数据，所以不能用 for of 循环
    
            // new String("123456")
                /*
                0: "1"
                1: "2"
                2: "3"
                3: "4"
                4: "5"
                5: "6"
                */
            /*for(let item of obj) {
                console.log(item); // 是值
            }*/
    
            /*
            6-vue的常规指令2.html:63 10
            6-vue的常规指令2.html:63 20
            6-vue的常规指令2.html:63 30
            6-vue的常规指令2.html:63 40
            */
    
            // for in 循环
            /*for (let key in arr) {
                if (!obj.hasOwnProperty(key)) break;
                console.log(key, arr[key]);
            }*/
    
            // for in 循环
            /*for(let key in obj){
                // => key 遍历的属性名
                // => obj[key]属性值
                // => 优先遍历属性名为数字的
                // => 会把所属类原型上自定义的属性主就去也遍历到
                // obj.hasOwnProperty(key) 判断这个 key 是不是 obj 私有的。
                if(!obj.hasOwnProperty(key)) break;
                console.log(key) // AA
            }*/
    
    
    
    
        </script>
    </body>
    </html>
```

## 课时7：VUE的常规指令2：事件处理
```jsx harmony
    
    <!doctype html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport"
              content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
    <!--
        v-on( 简写 @) : 用来实现事件绑定指令
            v-on:click = 'xxx'
            @click='xxx'
            <button v-on:click="func" ></button>
            <button @click="func" ></button>
    
        1. 需事件触发的时候，需要传递参数信息，把方法加小括号，$event 是事件对象
            v-on:click='sum($event, 10, 20)'
             <button v-on:click="sum($event, 10, 20)" ></button>
    
        2. 事件修饰符
            常规修饰符： @click.prevent/stop = 'xxx'
            按键修饰符： @keydown.enter/space/delete/up/right/down/left...='xxx'
            键盘码： @keydown.13 = 'xxx'
            组合按钮：@keydown.alt.67 = 'xxx' // => Alt+c
    -->
    <div id="app">
        <!--  不能绑定多个事件  -->
        <!--<button v-on:click="func" ></button>-->
    
        <!--  $event 这是固定写法，指定当前的事件，后面其它的都是参数  -->
        <!--<button v-on:click="sum($event, 10, 20)" ></button>-->
    
        <!--<a href="http://www.baidu.com/" @click.prevent.stop="func">百度</a>-->
    
        <!--<input type="text" placeholder="请输入搜索内容"  v-model="text" @keydown.enter="func"/>-->
        <input type="text" placeholder="请输入搜索内容"  v-model="text" @keydown.alt.67="func"/>
    
    
    </div>
    
    <!-- import js -->
    <!--  开发的时候尽可通用引用未压缩版本，这样有错误会抛出异常  -->
    <script src="../node_modules/vue/dist/vue.js"></script>
    <script>
        let vm = new Vue({
            el: '#app',
            data: {
                text: '',
            },
            methods: { // 方法区
                /*func(ev) {
                    // ev.preventDefault(); //
                    console.log(); // this 就是当前实例
                },*/
                func(ev) {
                    /*if(ev.keyCode === 13){
                        alert("中国深圳")
                    }*/
                    alert("中国深圳", this.text);
    
    
                },
                sum(ev, n, m){
                    console.log(arguments)
                },
            }
        })
    </script>
    </body>
    </html>
```

## 课时8：VUE中的表单元素处理
```jsx harmony
    
    <!doctype html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport"
              content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>8-vue中的表单元素处理</title>
    </head>
    <body>
    
    <!--
        单选或者复选按钮
            1、按照 v-model 进行分组，单选框准备的数据是一具值，复选框准备的数据是一个数组
            2、每一个框都有自己的 value, 谁被选中，数据值是被选中元素的 value 值； 相反，
               值是多少，对应 value 的元素也会被轮动认选中;
    
    -->
    <div id="app">
        <h1>姓别：</h1>
        <label><input type="radio" value='0' v-model.number="sex" checked/>男</label>
        <label><input type="radio" value='1' v-model.number="sex"/>女</label>
        <div>
            <button @click="submit">提交</button>
        </div>
    
        <h1>全选/非全选</h1>
        <div @change="delegate">
            <p><label><input type="checkbox" value="ok" v-model="all" @click="handleAll"/>全选/全不选</label></p>
            <p><label><input type="checkbox" value="song" v-model="hobby" />唱歌</label></p>
            <p><label><input type="checkbox" value="dance" v-model="hobby"/>跳舞</label></p>
            <p><label><input type="checkbox" value="read" v-model="hobby"/>读书</label></p>
            <p><label><input type="checkbox" value="javascript" v-model="hobby"/>编程</label></p>
            <p><button @click="handleSub">提交</button></p>
        </div>
    </div>
    
    <!-- import js -->
    <!--  开发的时候尽可通用引用未压缩版本，这样有错误会抛出异常  -->
    <script src="../node_modules/vue/dist/vue.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                sex: 0,
                hobby: ['javascript'],
                all: ['ok'],
            },
            methods: {
                submit() {
                    console.log(this.sex)
                },
                handleSub(){
                    console.log(this.hobby)
                },
                handleAll(){
                    // => click 事件处理比视图更新后数据的更改要先去做
                    if(!this.all.includes('ok')){
                        this.hobby = ['song', 'dance', 'read', 'javascript'];
                    }else{
                        this.hobby = [];
                    }
                },
                delegate(){
                    // => change 事件处理，要晚于数据更新
                    console.log(this.hobby)
                    this.all = this.hobby.length >= 4 ? ['ok'] : [];
    
                }
            }
        });
    </script>
    </body>
    </html>
```


## 课时9：filters过滤器方法
- 计算属性、过滤器、监听器
    + methods 普通方法
    + filters 过滤器
        - 只能应用到胡子语法和 v-bind 中
        - 小练习：输入内容的单词首字母大写
        ```jsx harmony
      
           <!DOCTYPE html>
           <html lang="en">
           <head>
               <meta charset="UTF-8">
               <title>课时9：filters过滤器方法</title>
           </head>
           <body>
           
           <!--
           
           -->
           
           <div id="app">
               <input type="text" v-model="text" />
               <br>
               <!--<span v-text="text.replace(/\b[a-zA-Z]+\b/g, item => {
                   return item.charAt(0).toUpperCase()+item.substring(1);
               })"></span>-->
           
               <!--  使用普通方法  -->
               <!--<span v-text="toUp(text)"></span>-->
           
               <!--
                   使用过滤器
                   过滤器的语法：按照竖线分隔，把竖线左侧的值传传递给右侧的过滤方法，经过方法的处理，把处理后的结果
                   展示在视图中
           
                   过滤器方法只能在胡子语法{{ }} 和 v-bind 中使用（过滤器的方法没有挂载到实例上）
               -->
               <!--<h1>{{ text | filterA }}</h1>-->
               <h1>{{text|toUp|filterB}}</h1>
               <!--<img :src="pic|picHandle" alt="">-->
           </div>
           
           <!-- import js -->
           <!--  开发的时候尽可通用引用未压缩版本，这样有错误会抛出异常  -->
           <script src="../node_modules/vue/dist/vue.js"></script>
           <script>
               const vm = new Vue({
                   el: '#app',
                   data: {
                       // =》 响应试数据：data 中准备的要在视图中渲染的数据（model）
                       text: '',
                   },
                   methods: {
                       /*
                         => 都会挂载到实例上，（不能和 data 中的属性名冲突）：这里的制定的方法是普通方法
                            可以在视图中调取使用，也可以在其它方法中调取使用
                        */
                       toUp(value){
                           return value.replace(/\b[a-zA-Z]+\b/g, item => {
                               return item.charAt(0).toUpperCase()+item.substring(1);
                           });
                       },
                       AA(){
                           this.toUp('');
                       },
                   },
                   filters: {
                       /*
                         => 设置过滤器：把需要在视图中的渲染的数据进行二次或者多的处理
           
                        */
                       toUp(value) {
                           // =》 value：需要过虑的数据 return 返回的是过虑后的结果
                           return value.replace(/\b[a-zA-Z]+\b/g, item => {
                               return item.charAt(0).toUpperCase()+item.substring(1);
                           });
                       },
                       filterB(value){
                           return value.split('').reverse().join('');
                       },
                       picHandle(value){
                           return value.length === 0 ? 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=273222513,3973617089&fm=26&gp=0.jpg': value;
                       }
                   }
               })
           </script>
           </body>
           </html>
        ```
                                                                               >
        
    + computed
        - getter & setter
        - 相对于普通方法讲，计算属性是基于它们的响应式依赖进行缓存的
        - 依赖 data 中的数据变量
        - 小练习：输入内容的单词首字母大写
        - 小练习：全选和非全选
        - 10-1-computed 计算属性
        ```jsx harmony
              
              <!DOCTYPE html>
              <html lang="en">
              <head>
                  <meta charset="UTF-8">
                  <title>Title</title>
              </head>
              <body>
              
              <div id="app">
                  <input type="text" v-model="text" />
                  <br>
                  <!--<span v-text="toUp(text)"></span>-->
                  <span v-text="toUP"></span>
              </div>
              
              <!-- import js -->
              <!--  开发的时候尽可通用引用未压缩版本，这样有错误会抛出异常  -->
              <script src="../node_modules/vue/dist/vue.js"></script>
              <script>
              
                  const vm = new Vue({
                      el: '#app',
                      data: {
                          text: '',
                      },
                      computed: {
                          /**
                           *  => 计算属性：它不是方法是一个属性，所以在视图中调取的时候不能加括号执行
                           *
                           *  toUP 和 data 中和 text 一样，都会挂载到实例上, 这存储的值是对应方法
                           *  返回的结果 (getter 函数处理的结果)
                           *
                           *  => 计算属性有自己的缓存处理：第一次获取这个属性值，会把某个响应式数据(text),
                           *  当第一次结果获取后，会把这个结果缓存下来；后期视图重新渲染，首先看 text 值是
                           *  否发生更改，如果发生更改，会重新计算 toUP 属性值，如果没有更改，则还会拿上次
                           *  缓存的结果进行渲染；
                           *
                           */
                          toUP() {
                              return this.text.replace(/\b[a-zA-Z]+\b/g, item => {
                                  return item.charAt(0).toUpperCase() + item.substring(1);
                              });
                          }
                      },
                      methods: {
                           // 方法
                          /*toUp(value){
                              return value.replace(/\b[a-zA-Z]+\b/g, item => {
                                  return item.charAt(0).toUpperCase() + item.substring(1);
                              });
                          }*/
                      }
                  })
              
              </script>
              </body>
              </html>
        ```
        - 10-2-computed 计算属性
        ```jsx harmony
              
              <!DOCTYPE html>
              <html lang="en">
              <head>
                  <meta charset="UTF-8">
                  <title>Title</title>
              </head>
              <body>
              
              <div id="app">
                  <p>正常的结果：{{ text }}</p>
                  <p>反转结果是：{{ reverseMethod() }}</p>
                  <p>反转结果是：{{ reverseComputed }}</p>
                  <p>{{ now2() }}</p>
              </div>
              
              <!-- import js -->
              <!--  开发的时候尽可通用引用未压缩版本，这样有错误会抛出异常  -->
              <script src="../node_modules/vue/dist/vue.js"></script>
              <script>
              
                  const vm = new Vue({
                      /*
                       => 真实项目中： 我们一般用一个计算属性和某些响应式数据过行关联，响应式数据发生改变计算属性
                       的 getter 函数重新执行，否则使用的是上一次计算出来的缓存结果。
                       */
                      el: '#app',
                      data: {
                          text: 'MY NAME IS JEAN',
                      },
                      computed: {
                          // => getter 函数
                          reverseComputed() {
                              console.log('computed')
                              return this.text.split('').reverse().join('');
                          },
                          now1(){
                              // => 计算属性中必须要关联一个响应式数据，否则 getter 函数只执行一次
                              return new Date();
                          }
                      },
                      methods: {
                          reverseMethod(){
                              console.log('methods')
                              return this.text.split('').reverse().join('');
                          },
                          now2(){
                              // => 计算属性中必须要关联一个响应式数据，否则 getter 函数只执行一次
                              return new Date();
                          }
                      }
                  });
              
                  let n = 0;
              
                  let timer = setTimeout(() => {
                      // =》 强制更新视图的重新渲染
                      n++;
                      if(n > 5) {
                          clearInterval(timer);
                          return;
                      }
              
                      if(n === 3) {
                          vm.text = 'Welcome to Jean';
                          return;
                      }
                      vm.$forceUpdate();
                  }, 1000)
              
              </script>
              </body>
              </html>
        ```
        - 10-3-computed 计算属性
        
    + watch
        - 当需要在数据变化的执行异步或者开销较大的操作时应用监听器
        - 小练习：全选和非全选
        - 小练习：数据异步绑定的处理
     
    
    
## 课时10：computed 计算属性
```jsx harmony
      
      <!DOCTYPE html>
      <html lang="en">
      <head>
          <meta charset="UTF-8">
          <title>Title</title>
      </head>
      <body>
      
      <div id="app">
          <p>正常的结果：{{ text }}</p>
          <p>反转结果是：{{ reverseComputed }}</p>
          <input type="text" v-model="reverseComputed">
      </div>
      
      <!-- import js -->
      <!--  开发的时候尽可通用引用未压缩版本，这样有错误会抛出异常  -->
      <script src="../node_modules/vue/dist/vue.js"></script>
      <script>
      
          const vm = new Vue({
              /*
               => 真实项目中： 我们一般用一个计算属性和某些响应式数据过行关联，响应式数据发生改变计算属性
               的 getter 函数重新执行，否则使用的是上一次计算出来的缓存结果。
               */
              el: '#app',
              data: {
                  text: 'MY NAME IS JEAN',
              },
              computed: {
                  // => getter 函数
                  /*reverseComputed() {
                      console.log('computed')
                      return this.text.split('').reverse().join('');
                  },*/
                  reverseComputed: {
                      get() {
                          /*
                           => getter：只要获取这个属性值就会触发 get 函数执行
                           */
                          return this.text.split('').reverse().join('');
                      },
                      set(value) {
                          /**
                           *  => setter：给属性设置的时候会触发 set 函数, value 是给这个属性
                           *  设置的值
                           */
                          console.log('OK', value)
                      }
                  }
              },
          });
      
          let n = 0;
      
          let timer = setTimeout(() => {
              // =》 强制更新视图的重新渲染
              n++;
              if (n > 5) {
                  clearInterval(timer);
                  return;
              }
      
              if (n === 3) {
                  vm.text = 'Welcome to Jean';
                  return;
              }
              vm.$forceUpdate();
          }, 1000)
      
      </script>
      </body>
      </html>
```

## 课时12：watch监听器
- 当需要在数据变化的执行异步或者开销较大的操作时应用监听器
- 小练习：全选和非全选
- 小练习：数据异步绑定的处理
```jsx harmony
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>11-基于computed实现全选和非全选.html</title>
    </head>
    <body>
    
    <div id="app">
        <label><input type="checkbox" v-model="selected" @change="handle" />全选/非全选</label>
        <hr/>
        <span v-for="item in hobbyList">
            <label :key="item.id | handleID"><input type="checkbox" :value="item.value" v-model="checkList"/>{{item.name}}</label>
        </span>
    </div>
    
    <!-- import js -->
    <!--  开发的时候尽可通用引用未压缩版本，这样有错误会抛出异常  -->
    <script src="../node_modules/vue/dist/vue.js"></script>
    <script>
    
        const vm = new Vue({
            el: '#app',
            data: {
                hobbyList: [
                    {
                        id: 1,
                        name: '唱歌',
                        value: 'song',
                    },
                    {
                        id: 2,
                        name: '跳舞',
                        value: 'dance',
                    },
                    {
                        id: 3,
                        name: '阅读',
                        value: 'read',
                    },
                    {
                        id: 4,
                        name: '睡觉',
                        value: 'sleep',
                    },
                ],
                // 存储选中的兴趣爱好
                checkList: [],
                // 存储全选按钮的选中状态
                selected: false,
            },
            /*
              => watch 监听响应式数据的改变(watch中监听的响应式数据必须在 data 中初始化) 和
                  computed 中的 setter 类似，只不过 computed 是自己单独设置的计算属性(不能和
                  data中的冲突), 而 watch 只能监听 data 中有的属性
    
             => 监听器支持异步操作 computed 的 getter 不支持异步获取数据
             */
            watch: {
                checkList() {
                    this.selected = this.checkList.length === this.hobbyList.length ? true: false;
                }
            },
            methods: {
                handle() {
                    if(this.selected) {
                        this.hobbyList.forEach(item => {
                            this.checkList.push(item.value);
                        });
                        return;
                    }
                    this.checkList = [];
                },
            },
            // 过滤器
            filters: {
                handleID(value) {
                    return 'hobby'+value;
                }
            }
        });
    
    
    </script>
    </body>
    </html>
```

## 课时13：class和style的处理
```jsx harmony
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <style>
            .active {
                color: red;
            }
            .big{
                font-size: 20px;
            }
        </style>
    </head>
    
    <body>
    <!--
        对象方式处理动态的样式
            :class="{样式类名：响应式数据, ...}"
            响应式数据为 true 则有这个样式类，反之则没有
    
    
        数组控制样式类
            :class="[响应式数据1, ....]"
            控制响应式数据的值是对应的样式类或者没有值，来控制是否有这个样式
    -->
    <div id="app">
        <h1>{{ msg }}</h1>
        <!--<p :class="{active:a, big:true}">欢迎来到深圳，我是Jean~~~</p>-->
    
        <p :class="[active, big]">欢迎来到深圳，我是Jean~~~</p>
        <!-- 第一种方式   -->
        <button @click="handle">切换样式</button>
        <!-- 第二种方式   -->
        <!--<button @click="a=!a">切换样式</button>-->
        <button @click="handleActive">切换样式</button>
    </div>
    <!-- import js -->
    <!--  开发的时候尽可通用引用未压缩版本，这样有错误会抛出异常  -->
    <script src="../node_modules/vue/dist/vue.js"></script>
    <script>
    
        const vm = new Vue({
            el: '#app',
            data: {
                msg: 'Jean',
                a: false,
                active: '',
                big: 'big',
            },
            methods: {
                handle(){
                    this.a = !this.a;
                },
                handleActive() {
                    this.active = this.active === '' ? 'active' : '';
                }
            }
        })
    
    </script>
    
    </body>
    </html>
```

## 课时14 基于VUE实现选项卡案例

    
    
