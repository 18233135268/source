### Bootstrap基础

> [Bootstrap官网](http://getbootstrap.com/2.3.2/index.html)

1、下载[http://getbootstrap.com/2.3.2/getting-started.html](http://getbootstrap.com/2.3.2/getting-started.html)

2、文件

```
bootstrap/
  ├── css/
  │   ├── bootstrap.css
  │   ├── bootstrap.min.css
  ├── js/
  │   ├── bootstrap.js
  │   ├── bootstrap.min.js
  └── img/
      ├── glyphicons-halflings.png
      └── glyphicons-halflings-white.png
```

3、熟悉HTML、css、js语法和应用，相关文档：

#### [Scaffolding](http://getbootstrap.com/2.3.2/scaffolding.html)

#### [Base CSS](http://getbootstrap.com/2.3.2/base-css.html)

#### [Components](http://getbootstrap.com/2.3.2/components.html)

#### [JavaScript plugins](http://getbootstrap.com/2.3.2/javascript.html)

4、组件列表

* Button groups
* Button dropdowns
* Navigational tabs, pills, and lists
* Navbar
* Labels
* Badges
* Page headers and hero unit
* Thumbnails
* Alerts
* Progress bars
* Modals
* Dropdowns
* Tooltips
* Popovers
* Accordion
* Carousel
* Typeahead

5、HTML模板

一个典型的html文件：

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Bootstrap 101 Template</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
  </head>
  <body>
    <h1>Hello, world!</h1>
    <script src="http://code.jquery.com/jquery.js"></script>
  </body>
</html>
```

将上面的文件改成bootstrap模板（包含了一些css和js文件）：

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Bootstrap 101 Template</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Bootstrap -->
    <link href="css/bootstrap.min.css" rel="stylesheet" media="screen">
  </head>
  <body>
    <h1>Hello, world!</h1>
    <script src="http://code.jquery.com/jquery.js"></script>
    <script src="js/bootstrap.min.js"></script>
  </body>
</html>
```





























