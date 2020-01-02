# # 思路

要在屏幕上展示3D图形，思路大体上都是这样的：

1. 构建一个三维空间
   - Three中称之为场景(Scene)
2. 选择一个观察点，并确定观察方向/角度等
   - Three中称之为相机(Camera)
3. 在场景中添加供观察的物体
   - Three中的物体有很多种，包括Mesh,Line,Points等，它们都继承自Object3D类
4. 将观察到的场景渲染到屏幕上的指定区域
   - Three中使用Renderer完成这一工作

# # 概念

## 1. Scene

场景是所有物体的容器，也对应着我们创建的三维世界。

## 2. Camera

Camera是三维世界中的观察者，为了观察这个世界，首先我们要描述空间中的位置。

![](./IMGS/coordinate.png)

Three中使用采用常见的[右手坐标系](https://link.zhihu.com/?target=https%3A//zh.wikipedia.org/wiki/%E7%AC%9B%E5%8D%A1%E5%84%BF%E5%9D%90%E6%A0%87%E7%B3%BB%23.E4.B8.89.E7.B6.AD.E7.A9.BA.E9.96.93)定位。

Three中的相机有两种，分别是正投影相机THREE.OrthographicCamera和透视投影相机THREE.PerspectiveCamera。

![](./IMGS/camera.png)

正交投影与透视投影的区别如上图所示，左图是正交投影，物体发出的光平行地投射到屏幕上，远近的方块都是一样大的；右图是透视投影，近大远小，符合我们平时看东西的感觉。

# # 三大组件

在Three.js中，要渲染物体到网页中，我们需要3个组建：场景（scene）、相机（camera）和渲染器（renderer）。有了这三样东西，才能将物体渲染到网页中去。

- 场景：场景是所有物体的容器。
- 相机：拍摄位置，类似于transform-origin。
- 渲染器：渲染器决定了渲染的结果应该画在页面的什么元素上面，并且以怎样的方式来绘制

```js
let scene = new THREE.Scene();
let camera = new THREE.PerspectiveCamera();
let renderer = new THREE.WebGLRenderer();
```



## 1. 绘制点

点由THREE.Vector3表示，Threejs中没有提供单独画点的函数，它必须被放到一个THREE.Geometry形状中，这个结构中包含一个数组vertices，这个vertices就是存放无数的点（THREE.Vector3）的数组。

语法：

```js
THREE.Vector3(x, y, z);
```

实例：

```js
let p1 = new THREE.Vector3(1, 2, 3);
let p2 = new THREE.Vector3();
p2.set(1, 2, 3);
```

## 2. 绘制线

