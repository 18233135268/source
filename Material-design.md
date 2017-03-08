

# Material design

## Introduction

### Principles

#### 实体感就是(通过设计方式来表达)隐喻

![](http://design.1sters.com/material_design/material-design/images/materialdesign-principles-layersquares_large_mdpi.png)

- 实体的表面和边缘提供基于真实效果的视觉体验，熟悉的触感让用户可以快速地理解和认知。实体的多样性可以让我们呈现出更多反映真实世界的设计效果，但同时又绝不会脱离客观的物理规律。
- 光效、表面质感、运动感这三点是解释物体运动规律、交互方式、空间关系的关键。真实的光效可以解释物体之间的交合关系、空间关系，以及单个物体的运动。


#### 鲜明、形象、深思熟虑

![](http://design.1sters.com/material_design/material-design/images/materialdesign-principles-circleplus_large_mdpi.png)

新的视觉语言，在基本元素的处理上，借鉴了传统的印刷设计——排版、网格、空间、比例、配色、图像使用——这些基础的平面设计规范。在这些设计基础上下功夫，不但可以愉悦用户，而且能够构建出视觉层级、视觉意义以及视觉聚焦。精心选择色彩、图像、选择合乎比例的字体、留白，力求构建出鲜明、形象的用户界面，让用户沉浸其中。

Material Design设计语言强调根据用户行为凸显核心功能，进而为用户提供操作指引。

#### 有意义的动画效果

![](http://design.1sters.com/material_design/material-design/images/materialdesign-principles-flyingsquare_large_mdpi.png)

动画效果(简称动效)可以有效地暗示、指引用户。动效的设计要根据用户行为而定，能够改变整体设计的触感。

动效应当在独立的场景呈现。通过动效，让物体的变化以更连续、更平滑的方式呈现给用户，让用户能够充分知晓所发生的变化。

动效应该是有意义的、合理的，动效的目的是为了吸引用户的注意力，以及维持整个系统的连续性体验。动效反馈需细腻、清爽。转场动效需高效、明晰。

## Environment

Material design设计的是一个包含光线，实物，和阴影的三维环境，z轴垂直于显示平面，正面延伸到用户视线。每一片material占有一个确定的z轴位置并且厚度都是标准的1dp，其实就相当于屏幕一个像素的厚度，具有160的像素密度。在网页页面中，z轴是用于分层而不是用于透视的，3D世界就是通过操纵y轴来仿真的。

- 所有的实物都具有x,y,z三个维度
- 所有的实物都具有一个确定的z轴坐标
- 主光线的投影方向决定阴影的方向
- 阴影产生于重叠的实体的高度差
- Material 厚度  1dp

在Material environment中，场景由虚拟光线来照亮，主光源产生定向的阴影，环绕的光线在实物的各个方向产生轻微柔弱的阴影。这里所说的阴影就由这两种光线产生。在安卓开发中，当光源被处在不同z轴位置的多层实体锁住的时候，阴影产生。在网页开发中，仅仅操控y轴来描绘阴影，以下这些栗子展示了具有6dp高度的卡片的投影情况：

Shadow cast by key light

<img src="https://material-design.storage.googleapis.com/publish/material_v_9/0B6Okdz75tqQsSFZUZ01GTk13T28/whatismaterial_environment_shadow1.png" height="400px" width="400px">



Shadow cast by ambient light

<img src="https://material-design.storage.googleapis.com/publish/material_v_9/0B6Okdz75tqQsdDhaaTMwMTFVLTA/whatismaterial_environment_shadow2.png" height="400px" width="400px">

Combined shadow from key and ambient lights

<img src="https://material-design.storage.googleapis.com/publish/material_v_9/0B6Okdz75tqQsNnVmbTNMUF9DR0U/whatismaterial_environment_shadow3.png" height="400px" width="400px">

## Material properties

懂得材料的这些品质有利于我们更好的操纵它们使我们的设计更符合material design的 视觉美感。

材料的特性：

1. 实物的，立体的
2. 在空间占据独一的位置
3. 不可穿过的
4. 仅沿着它所在的平面改变尺寸
5. Unbendable（不可以弯曲折叠）
6. 可以连接其他的材料
7. 可以被创建和销毁
8. 可以沿着任何轴移动



#### Physical properties

- 材料具有**变化的长宽尺寸**（以 dp 为计）和**均匀的厚度**（1dp）。不要使材料的厚度不一致，材料总是1dp厚度的。

- 阴影是由于材料元件之间的相对高度（Z 轴位置）而自然产生的，阴影描述了材料元件之间的相对高度。(值得注意的是，阴影不是近似于给材料描绘颜色，阴影的产生是自然的，动态的，由材料相对高度决定)

- 内容可以以任何形状和颜色显示在材料上。内容不增加材料的厚度，内容的展示能够独立于材料，（放大缩小移动位置等等）但要被限制在材料的范围里。

- 材料是实物。

  输入事件不能穿过材料。输入事件只影响前景材料，不能从材料下面穿过。

<img src="https://material-design.storage.googleapis.com/publish/material_v_9/0Bx4BSt6jniD7bDZac2JGV2RUNk0/whatismaterial_properties_physical3.png" height="400px" width="400px">

(True)

<img src="https://material-design.storage.googleapis.com/publish/material_v_9/0Bx4BSt6jniD7RVdsUWRKN2xlaGc/whatismaterial_properties_physical4.png" height="400px" width="400px">

(False)

- 多个材料元件不能同时占用相同的空间点。材料不能穿过其他材料。一片材料不能在改变高度时穿过另一片材料。因为材料具有不可穿过的特性（前面提到）

<img src="https://material-design.storage.googleapis.com/publish/material_v_9/0Bx4BSt6jniD7aVhXV0EtZ29OSU0/whatismaterial_properties_physical5.png" height="400px" width="400px">

(True)

<img src="https://material-design.storage.googleapis.com/publish/material_v_9/0Bx4BSt6jniD7UFdUMnRKaW5PSXM/whatismaterial_properties_physical6.png" height="400px" width="400px">

(False)





#### Transforming material

- 材料可以改变形状
- 材料扩展和收缩仅仅在它所在的平面内
- 材料不可以弯曲折叠
- 多片材料可以拼接在一起成为单独一片材料
- 当材料被割开时能自己复原。比如说，当你从一片材料中移除了一部分，这一片材料将再次愈合变为一块完整的材料

#### Movement of material

- 材料能在环境中的任何地方自动产生或消失。（比如从一个点延展出来，消失于某一个点）
- 材料可以沿着任何轴移动（甚至旋转）
- Z轴方向的运动一般都是由用户与材料交互而产生的。（也就是说用户点击或者聚焦到某块具体材料这种行为产生以后，材料进行Z轴的移动）


## Elevation and shadows

Material design 中的对象与现实生活中的对象具有相似的性质。依据这些现实对象的特性构造出来的空间模型对于用户来说是非常熟悉的，这一模型也可以被长期应用于移动应用当中。两个概念：高度 光影

- 高度：由两个材料的一个平面顶部到另一个平面顶部的高度差测得，一个元件的高度表明了它的表面之间的距离和它产生阴影的深度。
- 静止高度：所有的材料元件都有静止高度。组件在应用中具有一致的静止高度，可能在跨平台和设备中又有不一致的静止高度。
- 动态高度偏移：动态高度偏移坐标是一个组件相对于它静止位置移动的目标


#### Elevation(Android)

高度是在 Z 轴上两个不同平面之间的一种相对深度或距离。

*详述*

- “高度”的度量单位与 XY 轴的度量单位相同，主要是 dp。由于所有 Material 元素都具有 1 dp 的厚度，所以“高度”度量的是从一个平面顶部到另一个平面顶部的距离。
- 一个子对象的高度与其父对象的高度相关。

图例：



<img src="https://material-design.storage.googleapis.com/publish/material_v_9/0B6Okdz75tqQsTVdGcm1LX0dVeGM/whatismaterial_3d_elevation1.png" height="400px" width="400px">

两个对象之间的多种高度的测量。（图中的2dp , 8dp是resting elevation）

#### Resting elevation

所有 Material 除去大小以外，有一个“静止高度”，或者称“默认高度”，它是不会变化的。当一个对象的高度产生变化时，它将会尽快恢复到自身的静止高度。

桌面端的静止高度比推荐值要低2dp来适应鼠标及非触摸环境（Desktop resting elevation is 2dp below the listed values to accommodate mouse and non-touch environments）

##### 组件高度

- 组件跨平台保持一样的静止高度。（比如，一个浮动动作按钮的高度不会在某一个应用中是一个数值而在另一个应用中是另一个数值）
- 元素在某一平台中可能会存在多种静止高度，这取决于环境的深度。（比如，TV 相比于移动端和桌面来说就具有更深的层次因为它有各一个更大的屏幕，所以它处在视线的更远处，同样，TV和desktop比手机端的深度值更高）

##### 感应高度与动态高度偏移

一些组件元素具有感应高度，也就是说它们会根据用户的输入（比如不进行任何操作时，聚焦时，按压选择时）或系统事件来改变高度。这些高度的变化会通过动态高度偏移而不断生成。（感应高度是交互的）

动态高度偏移是某一元素相对于它的静止状态移动的目标高度，可以确定的是高度的变化在事件和元素类型之间是一致的。比如说，所有通过按压来提升的元素相对于其静态高度来说都具有相同的高度变化。

一旦输入事件完成或被取消，那么元素将会恢复到它的静止高度上。

##### 避免高度冲突

具有感应高度的元素当它在静止高度与动态高度偏移之间移动的时候可能会遇到其他的元素。由于material不可穿过，没有任何一种方式能够让元素之间产生冲突，无论是基于均元素基础（per-component basis）还是通过使用完整应用布局。

在元素水平上，元素可以在它们产生冲突之前提前移动或被移动。比如说，一个“浮动动作按钮”（FAB）可以在用户选择一张卡片之前消失或移出屏幕，或者在某一个 “snack bar” 出现时移动。

在布局水平上，你需要通过设计你的应用布局来将产生冲突的机会减小到最少。比如说，可以通过将 FAB 置于某个卡片流的一端来避免当用户尝试获取某个卡片时所产生的冲突。



参考的高度值列表：

| elevation(dp) | Component                                |
| :------------ | ---------------------------------------- |
| 24            | Dialog  /  Picker                        |
| 16            | Nav drawer / Right drawer/Model bottom Sheet |
| 12            | Floating action button (FAB - pressed)   |
| 9             | Sub menu (+1dp for each sub menu)        |
| 8             | Bottom navigation bar / Menu / Card (when picked up) / Raised button (pressed state) |
| 6             | Floating action button (FAB - resting elevation)   / Snackbar |
| 4             | App Bar                                  |
| 3             | Refresh indicator / Quick entry / Search bar (scrolled state) |
| 2             | Card (resting elevation) *  /   Raised button (resting elevation)*  / Quick entry / Search bar (resting elevation) |
| 1             | Switch                                   |



##### 元素高度比较

以下的图示对比了元素的静止高度和动态高度偏移。

![](https://material-design.storage.googleapis.com/publish/material_v_9/0Bzhp5Z4wHba3VG9SaVpNbkpHb2s/whatismaterial_3d_elevation2.png)

在这一图示中，只有元素的高度和布局是精确的，元素的其他尺寸和整体的元素布局只是为了说明而列出的。



一个包含卡片和浮动动作按钮 的应用布局的实例以及它在Z轴上元素高度的横截面图表。

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B8v7jImPsDi-cUtqZzE0REdJdnc/whatismaterial_3d_elevation3.png)

一个包含开放导航抽屉的应用布局实例与它在Z轴上元素高度的横截面图表。



#### Shadows

“阴影”提供了对象所处深度和方向性移动的重要视觉线索。它们是唯一的可表明不同平面之间分离程度的视觉线索。某一对象的“高度”决定了其具体“阴影”的表现形式。



一旦没有了阴影，没有什么可以表明浮动动作按钮是从背景层分离出来的。

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B6Okdz75tqQsYUJ6a1luU1ZtUWs/whatismaterial_3d_elevation_shadow1.png)



卷曲的阴影说明浮动动作按钮与底下蓝色的那片材料是两个分离开来的元素。但是由于它们的阴影非常的相似以至于会被误认为它们在同一高度上。

![](https://material-design.storage.googleapis.com/publish/material_v_9/0Bzhp5Z4wHba3ZDc2TUNPMEdNSkE/whatismaterial_3d_elevation_shadow2.png)



更柔和、更大的阴影表明 浮动动作按钮相比于有更卷曲阴影的蓝色的材料处在更高的高度。

![](https://material-design.storage.googleapis.com/publish/material_v_9/0Bzhp5Z4wHba3UW5QQ010bm0tZFk/whatismaterial_3d_elevation_shadow3.png)



在运动中，阴影提供了关于某个对象移动的方向以及不同平面之间距离是否正在增加或减少的有用线索。



如下图，如果没有一个阴影来表明高度，那么到底这个正方形是它的自身尺寸在增加还是它的高度在增加就不可明确了。

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B6Okdz75tqQsRlUtdkk1c2xwUkU/whatismaterial_3d_elevation_shadow4.png)



如下图，当某一个对象的高度增加时它的阴影会变得更柔和、更大，当其高度减小时，阴影会变得更卷曲。



![](https://material-design.storage.googleapis.com/publish/material_v_9/0B6Okdz75tqQsY1hrcHlOdEJuU1k/whatismaterial_3d_elevation_shadow6.png)

在这一实例中，连贯的阴影帮助用户明白这个对象是它的形状在改变而不是它的高度在增加



##### Component reference shadows

下面的元素阴影应被用于权威标准参考。如果在说明中有些元素阴影跟下面的参考阴影有不一致的情况出现，都遵从参考阴影。

**App bar：4dp**

如图是一个app bar 的实例

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B-Ef4kCjUzkPZ1lQV2ZEeTAxMzg/whatismaterial_3d_elevation_component06.png)

**Raised button:**

- Resting state: 2dp
  Pressed state: 8dp

在桌面端，升起的按钮也可以具有以下高度

- Resting state: 0dp

​       Pressed state: 2dp

。。。未完待续

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B-Ef4kCjUzkPSy1NQUtNdW5idXc/whatismaterial_3d_elevation_component02.png)



**Floating action button (FAB)：**

- Resting state: 6dp

​       Pressed state: 12dp

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B-Ef4kCjUzkPRFp6VHZ0UTc1V2M/whatismaterial_3d_elevation_component08.png)



**Card:**

- Resting state: 2dp

  Raised state: 8dp

在桌面端，。。。未完待续

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B-Ef4kCjUzkPb1Y5MjNXT2owMFE/whatismaterial_3d_elevation_component03.png)



**Menus and sub menus**

Menus: 8dp

Sub menus: 9dp (+1 dp for each sub menu)

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B-Ef4kCjUzkPN0FNTXJ0eU5ybXM/whatismaterial_3d_elevation_component09.png)

**Dialogs:24dp**

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B-Ef4kCjUzkPbEVrM01tYlVwR28/whatismaterial_3d_elevation_component12.png)

**Nav Drawer & Right drawer:16dp**

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B-Ef4kCjUzkPT2pNX0hoeWN5YzA/whatismaterial_3d_elevation_component10.png)

**Modal bottom sheet:16dp**

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B-Ef4kCjUzkPRXF4amhNZVFFcjQ/whatismaterial_3d_elevation_component11.png)

**Refresh indicator:3dp**

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B-Ef4kCjUzkPMWh1ZmwtTHlwMk0/whatismaterial_3d_elevation_component05.png)

**Quick entry/Search bar:**

Resting state: 2dp

Scrolled state: 3dp

![](https://material-design.storage.googleapis.com/publish/material_v_9/0Bzhp5Z4wHba3alQzSmJWQlg0ZWc/whatismaterial_3d_elevation_component04.png)



**Snackbar:6dp**

Snackbar 是一种针对操作的轻量级反馈机制，常以一个小的弹出框的形式，出现在手机屏幕下方或者桌面左下方。它们出现在屏幕所有层的最上方，包括浮动操作按钮。
它们会在超时或者用户在屏幕其他地方触摸之后自动消失。Snackbar 可以在屏幕上滑动关闭。当它们出现时，不会阻碍用户在屏幕上的输入，并且也不支持输入。屏幕上同时最多只能现实一个 Snackbar。Snackbar 中不能包含图标，操作只能以文本的形式存在。Snackbar具有暂时性，它不应该成为通往核心操作的唯一方式。作为在所有层的上方，Snackbar 不应该持续存在或相互堆叠。

(Android 也提供了一种主要用于提示系统消息的胶囊状的提示框 Toast。Toast 同 Snackbar 非常相似，但是 Toast 并不包含操作也不能从屏幕上滑动关闭。)

**Switch：1dp**

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B-Ef4kCjUzkPc1E0T1BZZ2V2d2s/whatismaterial_3d_elevation_component01.png)



#### Object relationships

**Object hierarchy**

你怎样去组织在某一应用中的对象或对象集合取决于它们怎样依据其他对象来移动。对象可以彼此之间独立地移动或在受到比它更高层次对象限制的条件下移动。

所有对象都是以“父-子”关系描述的层级体系的一部分。“子”元素在这一关系体系中代表它们“父”元素的下级元素。对象可以是这一系统的“子”元素或其他对象的“子”元素。

“父-子”元素说明：

- 每一个对象只有一个“父”元素。
- 每一个对象可以有任意数量的“子”元素。
- “子”元素继承来自“父”元素的可变化的属性，比如位置、旋转、大小（规模）和高度。
- “兄弟”元素是指与某一对象处在同一层级的对象。

**Exceptions**

以根元素为父元素的一些元素，比如主 UI 元素，它们相对于其他对象来说自主地移动。比如说，浮动动作按钮不会跟内容一起滚动。（对于屏幕来说位置固定）其他元素包括：

- 一个应用的边导航抽屉
- 动作条
- 对话

**Interaction**

某个对象如何跟其他对象交互由它们在“父-子”等级中所处位置决定。

比如：

- “子”元素与其“父”元素在Z轴上的分离距离最近；其他对象不能插入父子元素之间。
- 在一个滚动的卡片集合中，所有卡片之间都是同层次的“兄弟”元素，所以它们的关系就像坐在同一辆马车上一样共同移动。它们都是控制它们移动的卡片集合对象的子元素。

**Elevation**

你会如何确定对象的高度（即它们在 Z 轴的位置）取决于你想描述的内容层次以及某一个对象是否需要相对于其他对象自主移动。





# Motion

### Material motion

Material design世界中的动作是用来描述材料在空间的关系、功能，以及达到使材料优美流畅的目的的。

#### 为什么动作这么重要？

动作展示了一个APP是如何组织起来的以及它能做什么

动作具有以下的作用：

- 在一堆视图中引导了用户的注意力
- 暗示了用户在完成一个手势后会发生什么
- 元素之间的层次性的、空间性的关系
- 使用户从场景背后发生的事情（比如加载内容或者是加载下一个视图）当中转移注意力
- 把应用形象化，为它润色，增加它的趣味

#### Material怎样移动呢？

研究material所处环境的灵感来自于真实世界中的力。比如重力和摩擦力。这些力体现在用户输入具有影响力的元素到屏幕以及元素之间如何相互作用。

动作状态的材料具有以下特征：

##### Responsive

Material充满了能量，它能在用户触发它的地方快速精确地响应用户输入。

移动设备上的较大的动画时间长300 - 400 ms。较小的动画可以短至150 - 200 ms。比这些时间值更长的动画或者更短的动画h会更加迟钝或者困难。

下面的动画展示了（用户触碰一个点，由这个点展开涟漪布满整个卡片，同时卡片z轴位置提高来表明处在活跃状态）

![](https://material-design.storage.googleapis.com/publish/material_v_9/0B14F_FSUCc01aGFDUmZwNG1sTTQ/Responsive_02_Feedback-v2.webm)

##### Natural

材料描述了真实世界中物体的移动由力的作用产生这样一个特点。

- 在真实世界中，一个物体快速地进行加速或减速是由重力和表面摩擦力影响的，相似地，在material design中，开始和停止也不可瞬间就发生。
- 真实世界中的力（比如重力），更多的是使一个元素沿着一条弧运动而不是沿着一条直线运动。
- 材料的转换也是沿着一条弧线进行的。（动画中一张卡片由小变大是沿着弧线增大的）



##### Aware

材料可以感知周围的环境，包括在它周围的用户以及其他材料，它可以被对象吸引并且恰当地响应用户的意图。

- 当元素转换到视线中时，它们以及它们的环境在某种程度上被精心地安排好了，这就定义了它们之间的关系。
- material自身发生变化（扩大时）可以把其他材料平滑地推出视野。
- 元素可以吸引其他的元素，并且当它们彼此靠近的时候可以和它们合并



##### Intentional（表现一种趋势）

处在动作状态的材料在恰当地时间点引导用户的注意力到恰当的位置

- 材料可以一个动画的形式转换视图引导用户进行下一步的互动
- 动作可以产生不同的信号进行交流，比如一个动作是否不可用。（比如向右滑动时受到阻力）
- 动画可以使用户关注某个需要注意的对象（比如响铃时图标震动，四周展开多层涟漪）

#### 怎样让过渡更巧妙？

成功的动画设计具有以下的几点特征：

##### Motion is quick

一个互动在不必要的情况下不应该让用户等待太长的时间，动画完成速度应该非常快

##### Motion is clear

用于转换视图的动画应该非常清楚明确，简单，连贯，应该避免立即执行太多步骤

- 一个好的转换动画应该保持以一个清晰的路径进入下一个视图。
- 当许多项元素需要沿着不同方向移动或者横穿路径的时候，视图的转换会使人非常困惑。

##### Motion is cohesive

材料元素在运动时，速度、响应能力和趋势要一致，你的app中的动画要和所有用户化的动画体验保持一致。也就是说，虽然不同的app有不一样的功能，但是相似的动画体验让人感觉它们之间是有关联的。

#### Implications of motion(动作的暗示)

- 在转换的过渡期间,用户被引导到下一个视图。转换动画使得界面的层次结构发生转变。加载在场景的背后发生以减少延迟。
- 如果没有转换视图的动画发生，并且没有一个清晰的聚焦点，那么新的视图和旧的视图之间是什么关系用户就无法得知。不要让加载过程太明显地出现（比如用一个转动的圆圈表示加载）



物理世界中物体拥有质量，所以只有当施加给它们力量的时候才会移动，因此物体没法在瞬间开始或者结束动作。动画突然开始或者停止，或者在运动时突兀的变化方向，都会使用户感到意外和不和谐的干扰。

## Duration and easing（反应时间、历时与缓冲时间）

动作状态的材料是自然的，响应着的。使用这些缓冲曲线和延续模式来创造平滑的，连贯的动画。

### Speed

当元素在不同的位置之间移动或者不同状态之间转变，移动动作应该足够得快不会让用户等待，但是状态转变要足够得慢，这样用户才能理解发生的转变。

### Dynamic durations(动态的历时模式)

比起把单一的历时模式应用在所有的动画当中，我们更倾向于调整每一个动画历时来适应它所需经过的路程，元素的速度，以及界面的变化。

- 对象离开屏幕时可能需要更短的历时，因为它们只需要较少的注意力。
- 当对象需要经过很长的路程或者界面区域有戏剧性变化时需要用更长的历时。
- 当对象经过的路程较短或者界面区域变化较少的时候我们用更短的历时，使得动作不会展现得太慢。

### Common durations

***移动设备上：***

移动端的视图转换典型历时超过300ms，在这个边缘

- 较大的，复杂的，充满整个屏幕的视图转换可能需要更长的历时，超过375ms；
- 对象进入屏幕发生时间超过225ms
- 对象离开时间超过195ms

转换如果超过了400ms就会让人感觉非常得慢。

***有更大的屏幕的设备：***

在较大的屏幕上经过较长的路程的对象比起那些相同时间经过较短路程的对象具有更高的速度峰值，因此，较大的屏幕应该具有更长的历时以至于动作不会显得太快。

***平板电脑上：***

在平板电脑上的历时要比在移动设备上的历时多30%，举个栗子，一个300ms的移动端历时将会在平板电脑端增加到390ms。

***可穿戴的设备：***

在可穿戴设备上的历时要比在移动设备上的历时少30%，举个栗子，一个300ms的移动端历时将会在平板电脑端增加到210ms。

***电脑桌面端：***

桌面端动画应该比移动端更快，更简单，这些动画应该历时150ms至200ms。

因为桌面端的转换可能更不容易被注意被察觉，它们需要立刻响应并且要比移动端要快。

复杂的网页转换经常导致掉帧（即动画变卡顿）(除非他们为GPU加速建造)。短时间的历时会让这些不太明显，因为动画完成得很快。

因此，电脑桌面端的视图转换要更快



### Natural easing curves

这些自然的缓冲曲线影响一个对象的移动速度，透明度和大小比例。

速度或者展示的对象发生变化的时候应该在整个动画的历时过程中平滑地改变，这样动作就不会显得太机械太呆板。(加速的缓冲曲线还可以不对称，这样看起来会更自然，更使人愉悦)

#### Easing curves

缓冲曲线根据平台或者软件的不同可能会叫不同的名字，以下这些指导方针应该作为标准来参考：



***Standard curve:***

这是最普通的缓冲曲线，对象在屏幕位置之间迅速地加速和减速，在属性改变中，它适用于增大和缩减材料。

| Platform      | Protocol                                 |
| ------------- | ---------------------------------------- |
| Android       | FastOutSlowInInterpolator                |
| iOS           | [[CAMediaTimingFunction alloc] initWithControlPoints:0.4f:0.0f:0.2f:1.0f] |
| CSS           | cubic-bezier(0.4, 0.0, 0.2, 1);          |
| After Effects | Outgoing Velocity: 40%     Incoming Velocity: 80% |

***Deceleration curve("Easing out"):***

对象以饱和的速度从屏幕外进入到屏幕中并慢慢地减速直到到达它的静止位置。

在减速期间，对象可能会增大（大小和不透明度）至100%。在有些情况下，当对象以0%的不透明度进入屏幕，它们可能在快要进入时从更大的尺寸稍微缩减。（？？）

| Platform      | Protocol                                 |
| ------------- | ---------------------------------------- |
| Android       | LinearOutSlowInInterpolator              |
| iOS           | [[CAMediaTimingFunction alloc] initWithControlPoints:0.0f:0.0f:0.2f:1.0f] |
| CSS           | cubic-bezier(0.0, 0.0, 0.2, 1);          |
| After Effects | Outgoing Velocity: 0%Incoming Velocity: 80% |



***Acceleration curve ("Easing in"):***

对象以饱和速度离开屏幕，当离开屏幕后不会减速。

它们在动画的开始加速，可能减小尺寸或者不透明度到零。有些情况下，当对象以0%的透明度离开屏幕，它们在快离开屏幕时也可能稍微地增大或减小尺寸。

| Platform      | Protocol                                 |
| ------------- | ---------------------------------------- |
| Android       | FastOutLinearInInterpolator              |
| iOS           | [CAMediaTimingFunction alloc] initWithControlPoints:0.4f:0.0f:1.0f:1.0f] |
| CSS           | cubic-bezier(0.4, 0.0, 1, 1);            |
| After Effects | Outgoing Velocity: 40%     Incoming Velocity: 0% |



***Sharp curve:***

急弯曲线适用于随时可能回到屏幕的对象。

对象可能迅速地从屏幕的开始点加速，然后迅速地以一条非对称曲线减速到它在屏幕外的静止位置。这个过程的减速要比标准曲线的减速要快因为它不遵循一条确定的路径移动到屏幕外的点。对象还随时有可能从那个屏幕外的点回来。

| Platform      | Protocol                                 |
| ------------- | ---------------------------------------- |
| Android       | -                                        |
| iOS           | -                                        |
| CSS           | cubic-bezier(0.4, 0.0, 0.6, 1);          |
| After Effects | Outgoing Velocity: 40%      Incoming Velocity: 40% |





## Movement

材料的运动遵守力作用的原理，就像真实世界中一样。



屏幕上的移动：

- 向上的弧线
- 向下的弧线

进进出出的移动：

- 独立的移动
- 关联的移动

### Movement within screen bounds

元素在屏幕范围内两个点之间的移动遵从一条自然的凹形曲线，所有的屏幕上的移动的缓冲曲线使用的是标准曲线（Standard curve）

***向上的弧线：***

克服重力向上运动需要费力气，元素在屏幕上向上移动应该类似地在加速过程中通过更慢速的移动来描绘出这种 “费劲“ 。

- 当元素沿着对角线向上移动，开始缓慢地上升，结束的时候迅速地上升。
- 不要扭曲物理事实，因为设计材料的移动时忽略重力会使移动看起来不自然。

***向下的弧线：***

真实世界中物体降落受到重力的加速，元素在屏幕上向下移动应该类似地在加速过程中通过更快速的移动来描绘出这种 “省力” 。

- 当元素沿着对角线向下移动，开始快速地下降，结束的时候稍微缓慢一些。
- 不要扭曲物理事实，因为设计材料的移动时忽略重力会使移动看起来不自然。

***不是一条弧线的时候：***

对象沿着一条轴（要么是水平轴，要么垂直于水平轴，但不能同时两个轴）而不是沿着一条弧线的时候，这些移动会更简单并且可能以稍微快的速度移动。

- 使运动的路径笔直地沿着一条轴
- 不要把一条不自然的弧线应用到单轴的移动上，也就是不要让材料沿着一条不自然的弧线移动。

对象进入和退出屏幕同样沿着一条单一的轴

原则是： 线性出入，直线进入直线退出。不要使进入和退出的路径是一条弧线，这样看起来非常复杂，画龙添足。

### Movement in and out of screen bounds

#### 独立的移动

对象进入屏幕和退出屏幕被认为是独立的因为它们不影响到屏幕上的其他内容的位置。

***进入屏幕：***

物体进入屏幕的缓冲曲线用的是减速曲线（deceleration curve）因为进入时非常迅速，这表明它们已经经历过峰值速度了。

***永久离开屏幕：***

对象永久离开屏幕的缓冲曲线用的是加速曲线（acceleration curve）来用稍微再短一些的时间加速离开屏幕。因为它们不会再回来了，需要较少的用户注意力。

也就是说减速曲线适用于对象进入屏幕,不影响任何其他对象的位置。在移动设备上,这种转变时间通常225 ms。加速度曲线适用于这些对象永久离开屏幕的情况。在移动设备上,这种转变时间通常195 ms。（以上两种情况不要使用标准曲线）

***暂时离开屏幕：***

对象暂时离开屏幕应该用到急弯曲线，因为它们随时可能再回到屏幕（从离开的位置回来），应该在附近出现，触手可及。

当这些对象再返回的时候使用减速曲线，在移动设备上，这种转变时间一般为300ms。



#### 关联的移动

进入屏幕或者离开屏幕的对象会使其他屏幕内的元素移动应该要用平滑的缓冲曲线，这样他们的影响程度就会降到最低，避免了太抢眼，太戏剧性的移动。

标准曲线用于进入和离开屏幕范围的对象，这些历时曲线比独立移动的对象历时更长。一般为300ms

（不要用加速或减速曲线，否则看起来很突兀）



## Transforming material

材料可以通过重叠或者划分，形状大小变换使界面看起来非常有活力！

矩阵变换：（变换包括旋转、伸缩、倾斜、调动，这些行为都是矩阵变换。）

- 非对称
- 对称

径向变换：

- 圆形对称



## Choreography

## Creative customization



