#### 官网教程:[FairyGui编辑器使用教程](https://www.fairygui.com/docs/editor)

#### 1.项目结构

![](/images/fairyguiimage/img1.png)

- .objs文件夹：内部数据文件，**不需要加入版本控制**

- assets文件夹：包数据放置目录，本地工作区的内容
- settings文件夹：项目配置文件放置目录
- FGUITest1.fairy：FairyGui项目特有的标识文件(可以重命名)

#### 2.工具初认识

![](/images/fairyguiimage/img2.png)

**项目常用的设置项**

- ###### 项目设置

![](/images/fairyguiimage/img3.png)

![img4](/images/fairyguiimage/img4.png)

- ###### 发布设置

![](/images/fairyguiimage/img5.png)

![](/images/fairyguiimage/img6.png)

#### 3.基础概念，组件和元件

- 组件，可以简单理解成是一个“容器”，里面可以包含很多东西，当然也可以包含其他的组件，也就是组件和组件直接可以相互嵌套
- 元件，一个个组成组件的简单单元，例如：文本，富文本，图片，装载器，动画等等。。。
  - 组合型元件，例如：按钮，下拉框，滚动条，滑动条，进度条，标签。。。
  - 特殊元件，列表。

#### 4.辅助设计

- 舞台背景颜色
- 设计图（临摹。。。）

#### 5.模式区分

- 编辑模式（部分辅助功能是在该模式下生效，例如：显示列表控制显示与否，或者普通组，只是辅助作用，真正运行的时候是不会生效的）
- 运行模式

#### 6.组

- 普通组，可以把选中的内容框起来，可以在编辑模式下把框起来的内容一起控制，但真正运行的时候这个组不存在；
- 高级组，和普通组基本一样，但是高级组运行发布的时候是会真正存在的，而普通组是不会的。高级组可以控制整体显示，可以设置里面元素的布局。

#### 7.关联系统
