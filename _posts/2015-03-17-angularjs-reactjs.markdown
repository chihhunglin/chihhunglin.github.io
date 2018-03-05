---
layout: post
title:  "AngularJS React"
date:   2015-03-17 12:03:06 +0800
categories: AngularJS ReactJS
---
已經用AngularJS了，為什麼要[React][2]

AngularJS [directives][1] 用來延伸 HTML DOM 有點複雜，那React有甚麼特點呢?
* React isn't an MVC framework : 是個 View 的庫
* React doesn't use templates : 可以用 [JSX][4]，看起來很像 XML 的Javascript
* Reactive updates are dead simple : 用了才知道...

# AngularJS app 整合 React
文章來源[Adding ReactJS to an existing AngularJS app with Grunt workflow][5]

首先有講到關於 The more data bindings you have, the longer this digest cycle takes.  So if we can reduce or eliminate certain data bindings, then our app should perform better.  This is where React can help...

步骤 ：
## Install ReactJS into my app
```sh
bower install --save react
```
## Install grunt-react
在 Build 過程把 JSX 轉譯成 Javascript
```sh
npm install --save-dev grunt-react
```

## Hello World [JSFiddle][7]
### react components  我放的位置: vim app/scripts/components/hello.js
```sh
var Hello = React.createClass({
    displayName:'Hello',
    render:function(){
        return React.createElement("div", null, "Hello ", this.props.name);
    }
});
```
### vim index.html
```sh
+    <script src="bower_components/react/react.js"></script>

+    <script src="scripts/components/hello.js"></script>
```
### angularjs directive
```sh
.directive('helloNg', function(){
    return{
        restrict:'E',
        scope:{
            name:'='
        },
        link:function(scope, el, attrs){
            scope.$watch('name', function(newValue, oldValue){
            React.render(
                React.createElement(Hello, {name:newValue}),
                el[0]);
            })
        }
    }
})
```
### angularjs controller
```sh
$scope.name = 'World';
```
### angularjs view
找個地方擺 hello-ng
```sh
<hello-ng name="name"></hello-ng>
```
## Hello World with JSX
### vim jsx/hello.jsx
```sh
var Hello = React.createClass({
    render: function() {
        return <div>Hello {this.props.name}</div>;
    }
});
```
### 修改 index.html
```sh
+    <script src="bower_components/react/react.js"></script>

+    <script src="scripts/jsx/hello.js"></script>
```

## Grunt watch
```sh
 jsx: {
        files: ['<%= yeoman.app %>/jsx/{,*/}*.jsx'],
        tasks: ['react:files']
      },
```
## Grunt Task
```sh
react: {
  files: {
    expand: true,
    cwd: '<%= yeoman.app %>/jsx',
    src: ['**/*.jsx'],
    dest: '<%= yeoman.app %>/scripts/jsx',
    ext: '.js'
  }
}
```

## Build Task
加在 usemin 之前
```sh
grunt.registerTask('build', [
  'clean:dist',
  'wiredep',
  'react',
  'useminPrepare',
  'concurrent:dist',
  'autoprefixer',
  'concat',
  'ngAnnotate',
  'copy:dist',
  'cdnify',
  'cssmin',
  'uglify',
  'filerev',
  'usemin',
  'htmlmin'
]);
```

## build:js block in my index.html
```sh
<!-- build:js({.tmp,app}) scripts/scripts.js -->
<script src="scripts/jsx/hello.js"></script> <!--在這邊...-->
<script src="scripts/app.js"></script>
<script src="scripts/controllers/main.js"></script>
<script src="scripts/directives/image_preview.js"></script>
<!-- endbuild -->
```
# [tutorail][10]

# [Complementary Tools][8]

# [react bootstrap][9]

# 參考
* Quora:[Facebook's React vs AngularJS: A Closer Look][3]
* [Faster AngularJS Rendering (AngularJS and ReactJS)][6]


[1]:https://code.angularjs.org/1.0.8/docs/guide/directive#reasonsbehindthecompilelinkseparation
[2]:http://facebook.github.io/react/blog/2013/06/05/why-react.html
[3]:http://www.quora.com/Pete-Hunt/Posts/Facebooks-React-vs-AngularJS-A-Closer-Look
[4]:http://facebook.github.io/react/docs/jsx-in-depth.html
[5]:http://patrickgrimard.com/2014/11/13/adding-reactjs-to-an-existing-angularjs-app-with-grunt-workflow/
[6]:http://www.williambrownstreet.net/blog/2014/04/faster-angularjs-rendering-angularjs-and-reactjs/
[7]:http://jsfiddle.net/reactjs/5vjqabv3/
[8]:https://github.com/facebook/react/wiki/Complementary-Tools
[9]:https://github.com/react-bootstrap/react-bootstrap
[10]:http://facebook.github.io/react/docs/tutorial.html
