# Menu

menu 类可以用来创建原生菜单，主进程模块可以通过 remote 模块给渲染进程调用

```javascript
<!-- index.html -->
<script>
const remote = require('electron').remote;
const Menu = remote.Menu;
const MenuItem = remote.MenuItem;

var menu = new Menu();
menu.append(new MenuItem({ label: 'MenuItem1', click: function() { console.log('item 1 clicked'); } }));
menu.append(new MenuItem({ type: 'separator' }));
menu.append(new MenuItem({ label: 'MenuItem2', type: 'checkbox', checked: true }));

window.addEventListener('contextmenu', function (e) {
  e.preventDefault();
  menu.popup(remote.getCurrentWindow());
}, false);
</script>
```

# 类: Menu

创建一个新的 menu

```javascript
new Menu()
```

# 静态方法

macOS 设置应用菜单    windows 和 Linux 是为每个窗口都在其顶部设置菜单

```javascript
Menu.setApplicationMenu(menu)
```

* menu    Menu

返回应用菜单

```javascript
Menu.getApplicationMenu()
```

发送 action 给应用的第一个响应器 ( macOS ) 

```javascript
Menu.sendActionToFirstResponder(action)  
```

* action  String

加载模版  加载完模版 返回一个 Menu 类型的参数，提供给设置模版的步骤

```
Menu.buildFromTemplate(template)
```

* template  Array 

# 实例方法

在 browserWindow 中弹出 context menu

```javascript
menu.popup([browserWindow,x,y,positioningItem]) // x,y 默认都是 -1,设置菜单放置的位置
```

添加菜单项

```
menu.append(menuItem)
```

插入 menuItem 到指定的位置

```
menu.insert(pos, menuItem)
```

* pos  Integer
* menuItem  MenuItem

获取一个菜单项数组

```
menu.items()
```

# macOS Application 上的菜单的注意事项

相对于 windows 和 Linux , macOS 上的应用菜单是完全不同的 style

## 标准菜单

macOS 上 很多系统定义的标准菜单

* window
* help
* services

## 标准菜单项行为

macOS 为一些菜单项提供了标准的行为方法，例如 About xxx, Hide xxx , Hide Others

## 主菜单名

在 macOS ，无论你设置的什么标签，应用菜单的第一个菜单项的标签始终未你的应用名字.想要改变它的话，你必须通过修改应用绑定的 Info.plist 文件来修改应用名字。

# 菜单项位置

通过  Menu.buildFromTemplate 创建菜单的时候，使用 position 和 id 来放置菜单项

