## <img src='https://d14xs1qewsqjcd.cloudfront.net/assets/logo-black.svg'>
### 安装 & 运行
#### Mac/Linux
```shell
$ curl https://install.meteor.com/ | sh
```
#### Windows

```html
https://www.meteor.com/install
```

#### 创建一个demo

```shell
$ mkdir meteor_demo
$ cd meteor_demo
$ meteor create my_app
```
### 文件

```
client/main.js        # 客户端的入口
client/main.html      # html页面
client/main.css       # css风格文件
server/main.js        # 服务端的入口
package.json          # npm包控制文件
.meteor               # 内部 Meteor 文件
.gitignore            # git控制文件
```

#### 运行

```shell
$ cd my_app
$ meteor npm install
$ meteor
```

在浏览器中访问 http://localhost:3000

### 在模板中定义视图

#### 在meteor中使用Angular

1、 移除默认的meteor UI包：Blaze

```shell
$ meteor remove blaze-html-templates
```

2、 添加angular的UI 包

```shell
$ meteor add angular-templates
```

3、 添加需要的npm包

```shell
$ meteor npm install --save angular angular-meteor
```

4、 在创建好的app中

4.1、 替换client/main.html中的代码

```html
<head>
  <title>Todo List</title>
</head>
<body>
  <div class="container" ng-app="simple-todos">
  </div>
</body>
```

4.2、 替换client/main.js的代码

```javascript
import angular from 'angular';
import angularMeteor from 'angular-meteor';
 
angular.module('simple-todos', [
  angularMeteor
]);
```

4.3、 创建todosList组件  imports/components/todosList.html

```jsx
<header>
  <h1>Todo List</h1>
</header>
<ul>
  <li ng-repeat="task in $ctrl.tasks">
    {{task.text}}
  </li>
</ul>
```

4.4、 添加一些函数 imports/components/todosList/todosList.js

```javascript
import angular from 'angular';
import angularMeteor from 'angular-meteor';
import template from './todosList.html';
 
class TodosListCtrl {
  constructor() {
    this.tasks = [{
      text: 'This is task 1'
    }, {
      text: 'This is task 2'
    }, {
      text: 'This is task 3'
    }];
  }
}
 
export default angular.module('todosList', [
  angularMeteor
])
  .component('todosList', {
    templateUrl: 'imports/components/todosList/todosList.html',
    controller: TodosListCtrl
  });
```

5、 在app中实现todoList组件

5.1、 在模板中引入组件 client/main.html

```html
<body>
  <div class="container" ng-app="simple-todos">
    <todos-list></todos-list>
  </div>
</body>
```

5.2、 将模块引入app client/main.js

```javascript
import angular from 'angular';
import angularMeteor from 'angular-meteor';
import todosList from '../imports/components/todosList/todosList';
 
angular.module('simple-todos', [
  angularMeteor,
  todosList.name
]);
```

6、 重新再浏览器中访问 http://localhost:3000 查看效果
7、 添加css  client/main.css

```css
body {
    font-family: sans-serif;
    background-color: #315481;
    background-image: linear-gradient(to bottom, #315481, #918e82 100%);
    background-attachment: fixed;
 
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
 
    padding: 0;
    margin: 0;
 
    font-size: 14px;
}
 
.container {
    max-width: 600px;
    margin: 0 auto;
    min-height: 100%;
    background: white;
}
 
header {
    background: #d2edf4;
    background-image: linear-gradient(to bottom, #d0edf5, #e1e5f0 100%);
    padding: 20px 15px 15px 15px;
    position: relative;
}
 
#login-buttons {
    display: block;
}
 
h1 {
    font-size: 1.5em;
    margin: 0;
    margin-bottom: 10px;
    display: inline-block;
    margin-right: 1em;
}
 
form {
    margin-top: 10px;
    margin-bottom: -10px;
    position: relative;
}
 
.new-task input {
    box-sizing: border-box;
    padding: 10px 0;
    background: transparent;
    border: none;
    width: 100%;
    padding-right: 80px;
    font-size: 1em;
}
 
.new-task input:focus{
    outline: 0;
}
 
ul {
    margin: 0;
    padding: 0;
    background: white;
}
 
.delete {
    float: right;
    font-weight: bold;
    background: none;
    font-size: 1em;
    border: none;
    position: relative;
}
 
li {
    position: relative;
    list-style: none;
    padding: 15px;
    border-bottom: #eee solid 1px;
}
 
li .text {
    margin-left: 10px;
}
 
li.checked {
    color: #888;
}
 
li.checked .text {
    text-decoration: line-through;
}
 
li.private {
    background: #eee;
    border-color: #ddd;
}
 
header .hide-completed {
    float: right;
}
 
.toggle-private {
    margin-left: 5px;
}
 
@media (max-width: 600px) {
    li {
        padding: 12px 15px;
    }
 
    .search {
        width: 150px;
        clear: both;
    }
 
    .new-task input {
        padding-bottom: 5px;
    }
}
```











