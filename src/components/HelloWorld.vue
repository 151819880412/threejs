<template>
  <div></div>
</template>

<script>
import * as THREE from "three";
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls.js';
export default {
  props: {},
  data() {
    return {
      camera: null,
      scene: null,
      renderer: null,
      mesh: null,
    };
  },
  computed: {},
  created() {},
  mounted() {
    this.init()
    //间隔20ms周期性调用函数fun,20ms也就是刷新频率是50FPS(1s/20ms)，每秒渲染50次
    setInterval(this.render(),20);
  },
  watch: {},
  methods: {
    // 初始化
    init(){
      /**
       * 创建场景对象Scene
       */
      this.scene = new THREE.Scene();
      /**
       * 创建网格模型
       */
      // var geometry = new THREE.SphereGeometry(40, 40, 40); //创建一个球体几何对象
      // var geometry = new THREE.BoxGeometry(100, 100, 100); //创建一个立方体几何对象Geometry
      // var material = new THREE.MeshLambertMaterial({
      //   color: 0x0000ff,
      //   // wireframe:true,
      //   // transparent:true,
      //   // opacity:0.5,
      //   // specular:0x4488ee,  //new THREE.MeshPhongMaterial
      //   // shininess:12
      // }); //材质对象Material
      // this.mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
      // this.scene.add(this.mesh); //网格模型添加到场景中

      // var geometry = new THREE.BufferGeometry(); //创建一个Buffer类型几何体对象
      // //类型数组创建顶点数据
      // var vertices = new Float32Array([
      //   0, 0, 0, //顶点1坐标
      //   80, 0, 0, //顶点2坐标
      //   80, 80, 0, //顶点3坐标
      //   0, 80, 0, //顶点4坐标
      // ]);
      // // 创建属性缓冲区对象
      // var attribue = new THREE.BufferAttribute(vertices, 3); //3个为一组，表示一个顶点的xyz坐标
      // // 设置几何体attributes属性的位置属性
      // geometry.attributes.position = attribue;
      // //类型数组创建顶点颜色color数据
      // // var colors = new Float32Array([
      // //   1, 0, 0, //顶点1颜色
      // //   0, 1, 0, //顶点2颜色
      // //   0, 0, 1, //顶点3颜色

      // //   1, 1, 0, //顶点4颜色
      // //   0, 1, 1, //顶点5颜色
      // //   1, 0, 1, //顶点6颜色
      // // ]);
      // // // 设置几何体attributes属性的颜色color属性
      // // geometry.attributes.color = new THREE.BufferAttribute(colors, 3); //3个为一组,表示一个顶点的颜色数据RGB
      // var normals = new Float32Array([
      //   0, 0, 1, //顶点1法向量
      //   0, 0, 1, //顶点2法向量
      //   0, 0, 1, //顶点3法向量
      //   0, 0, 1, //顶点4法向量
      // ]);
      // // 设置几何体attributes属性的位置normal属性
      // geometry.attributes.normal = new THREE.BufferAttribute(normals, 3); //3个为一组,表示一个顶点的法向量数据

      // // Uint16Array类型数组创建顶点索引数据
      // var indexes = new Uint16Array([
      //   // 0对应第1个顶点位置数据、第1个顶点法向量数据
      //   // 1对应第2个顶点位置数据、第2个顶点法向量数据
      //   // 索引值3个为一组，表示一个三角形的3个顶点
      //   0, 1, 2,
      //   0, 2, 3,
      // ])
      // // 索引数据赋值给几何体的index属性
      // geometry.index = new THREE.BufferAttribute(indexes, 1); //1个为一组

      // // 三角面(网格)渲染模式
      // var material = new THREE.MeshBasicMaterial({
      //   // color: 0x0000ff, //三角面颜色
      //   vertexColors: THREE.VertexColors, //以顶点颜色为准
      //   side: THREE.DoubleSide, //两面可见
      //         //   color: 0x0000ff,
      //   shininess:12
      // }); //材质对象
      // this.mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
      // this.scene.add(this.mesh);//三角面对象添加到场景中

      // 点渲染模式
      // var material = new THREE.PointsMaterial({
      //   // color: 0xff0000,
      //   // size: 10.0 ,//点对象像素尺寸
      //   vertexColors: THREE.VertexColors, //以顶点颜色为准
      //   size: 10.0 //点对象像素尺寸
      // }); //材质对象
      // var points = new THREE.Points(geometry, material); //点模型对象
      // // this.mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
      // this.scene.add(points); //点对象添加到场景中

      // // 线条渲染模式
      // var material=new THREE.LineBasicMaterial({
      //     // color:0xff0000 //线条颜色
      //     vertexColors: THREE.VertexColors, //以顶点颜色为准
      // });//材质对象
      // var line=new THREE.Line(geometry,material);//线条模型对象
      // this.scene.add(line);//线条对象添加到场景中

      /**
       * 2.7
       */
      // var geometry = new THREE.BoxGeometry(100, 100, 100); //创建一个立方体几何对象Geometry
      // // 遍历几何体的face属性
      // geometry.faces.forEach(face => {
      //   // 设置三角面face三个顶点的颜色
      //   face.vertexColors = [
      //     new THREE.Color(0xffff00),
      //     new THREE.Color(0xff00ff),
      //     new THREE.Color(0x00ffff),
      //   ]
      // });
      // // pop()：删除数组的最后一个元素   shift：删除数组的第一个元素
      // geometry.faces.pop();
      // geometry.faces.pop();
      // geometry.faces.shift();
      // geometry.faces.shift();
      // var material = new THREE.MeshLambertMaterial({
      //   vertexColors: THREE.FaceColors,
      // }); //材质对象Material
      // this.mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
      // this.scene.add(this.mesh); //网格模型添加到场景中
      // console.log(geometry);
      // console.log('几何体顶点位置数据',geometry.vertices);
      // console.log('三角行面数据',geometry.faces);


      /**
       * 2.8
       * 
       */
      // var geometry = new THREE.BoxGeometry(100, 100, 100); //创建一个立方体几何对象Geometry
      // // 几何体xyz三个方向都放大2倍
      // geometry.scale(2, 2, 2);
      // // 几何体沿着x轴平移50
      // geometry.translate(50, 0, 0);
      // // 几何体绕着x轴旋转45度
      // geometry.rotateX(Math.PI / 4);
      // // 居中：偏移的几何体居中
      // geometry.center();
      // // 几何体xyz方向分别缩放0.5,1.5,2倍
      // // geometry.scale(0.5, 1.5, 2);
      // console.log(geometry.vertices);
      // var material = new THREE.MeshLambertMaterial({
      //   vertexColors: THREE.FaceColors,
      // }); //材质对象Material
      // this.mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
      // // 网格模型xyz方向分别缩放0.5,1.5,2倍
      // // this.mesh.scale.set(0.5, 1.5, 2)
      // this.scene.add(this.mesh); //网格模型添加到场景中

      /**
       * 4.1
       * 
       */
      // var geometry = new THREE.BoxGeometry(100, 100, 100); //创建一个立方体几何对象Geometry
      // // 点渲染模式
      // var material = new THREE.PointsMaterial({
      //   color: 0xff0000,
      //   size: 5.0 //点对象像素尺寸
      // }); //材质对象
      // var points = new THREE.Points(geometry, material); //点模型对象
      // this.scene.add(points); //点对象添加到场景中
      // var geometry = new THREE.BoxGeometry(100, 100, 100); //创建一个立方体几何对象Geometry
      // // 线条渲染模式
      // var material=new THREE.LineBasicMaterial({
      //     color:0xff0000 //线条颜色
      // });//材质对象
      // // 创建线模型对象   构造函数：Line、LineLoop、LineSegments
      // var line=new THREE.Line(geometry,material);//线条模型对象
      // this.scene.add(line); //点对象添加到场景中
      // var geometry = new THREE.BoxGeometry(100, 100, 100);
      // // 三角形面渲染模式  
      // var material = new THREE.MeshLambertMaterial({
      //   color: 0x0000ff, //三角面颜色
      //   wireframe:true,//网格模型以线条的模式渲染
      // }); //材质对象
      // // 通过访问属性的形式设置
      // material.wireframe = true;
      // this.mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
      // this.scene.add(this.mesh); //网格模型添加到场景中

      /**
       * 4.3
       */
      // var box=new THREE.BoxGeometry(10,10,10);//创建一个立方体几何对象
      // var material=new THREE.MeshLambertMaterial({color:0x0000ff});//材质对象
      // this.mesh=new THREE.Mesh(box,material);//网格模型对象
      // var mesh2 = mesh.clone();//克隆网格模型
      // var mesh3 = mesh.clone();//克隆网格模型
      // var mesh4 = mesh.clone();//克隆网格模型
      // var mesh5 = mesh.clone();//克隆网格模型
      // mesh2.translateX(20);//网格模型mesh平移
      // mesh3.translateX(40);//网格模型mesh平移
      // mesh4.translateX(60);//网格模型mesh平移
      // mesh5.translateX(80);//网格模型mesh平移
      // this.scene.add(mesh,mesh2,mesh3,mesh4,mesh5);//网格模型添加到场景中

      /**
       * 5.2
       * 
       */
      // var box=new THREE.BoxGeometry(100,100,100);//创建一个立方体几何对象
      // var material=new THREE.MeshLambertMaterial({color:0x0000ff});//材质对象
      // this.mesh=new THREE.Mesh(box,material);//网格模型对象
      // this.scene.add(this.mesh);//网格模型添加到场景中
      // // 设置产生投影的网格模型
      // this.mesh.castShadow = true;
      // //创建一个平面几何体作为投影面
      // var planeGeometry = new THREE.PlaneGeometry(300, 200);
      // var planeMaterial = new THREE.MeshLambertMaterial({
      //   color: 0x999999
      // });
      // // 平面网格模型作为投影面
      // var planeMesh = new THREE.Mesh(planeGeometry, planeMaterial);
      // this.scene.add(planeMesh); //网格模型添加到场景中
      // planeMesh.rotateX(-Math.PI / 2); //旋转网格模型
      // planeMesh.position.y = -50; //设置网格模型y坐标
      // // 设置接收阴影的投影面
      // planeMesh.receiveShadow = true;
      
      /**
       * 6.1
       * 
       */
      //创建两个网格模型mesh1、mesh2
      // var geometry = new THREE.BoxGeometry(100, 100, 100);
      // var material = new THREE.MeshLambertMaterial({color: 0x0000ff});
      // var group = new THREE.Group();
      // var mesh1 = new THREE.Mesh(geometry, material);
      // var mesh2 = new THREE.Mesh(geometry, material);
      // mesh2.translateX(150);
      // //把mesh1型插入到组group中，mesh1作为group的子对象
      // group.add(mesh1);
      // //把mesh2型插入到组group中，mesh2作为group的子对象
      // group.add(mesh2);
      // //把group插入到场景中作为场景子对象
      // this.scene.add(group);
      // // 删除父对象group的子对象网格模型mesh1
      // // group.remove(mesh1)
      // // // 一次删除场景中多个对象
      // // this.scene.remove(group)

      // 头部网格模型和组
      var headMesh = this.sphereMesh(10, 0, 0, 0);
      headMesh.name = "脑壳"
      var leftEyeMesh = this.sphereMesh(2, 8, 5, 4);
      leftEyeMesh.name = "左眼"
      var rightEyeMesh = this.sphereMesh(2, 8, 5, -4);
      rightEyeMesh.name = "右眼"
      var headGroup = new THREE.Group();
      headGroup.name = "头部"
      headGroup.add(headMesh, leftEyeMesh, rightEyeMesh);
      // 身体网格模型和组
      var neckMesh = this.cylinderMesh(3, 10, 0, -15, 0);
      neckMesh.name = "脖子"
      var bodyMesh = this.cylinderMesh(14, 30, 0, -35, 0);
      bodyMesh.name = "腹部"
      var leftLegMesh = this.cylinderMesh(4, 60, 0, -80, -7);
      leftLegMesh.name = "左腿"
      var rightLegMesh = this.cylinderMesh(4, 60, 0, -80, 7);
      rightLegMesh.name = "右腿"
      var rightLegMesh1 = this.cylinderMesh1(4, 70, 0, -25, 1);
      var legGroup = new THREE.Group();
      legGroup.name = "腿"
      legGroup.add(leftLegMesh, rightLegMesh,rightLegMesh1);
      var bodyGroup = new THREE.Group();
      bodyGroup.name = "身体"
      bodyGroup.add(neckMesh, bodyMesh, legGroup);
      // 人Group
      var personGroup = new THREE.Group();
      personGroup.name = "人"
      personGroup.add(headGroup, bodyGroup)
      personGroup.translateY(50)
      this.scene.add(personGroup);
      this.scene.traverse(function(obj) {
        if (obj.type === "Group") {
          console.log(obj.name);
        }
        if (obj.type === "Mesh") {
          console.log('  ' + obj.name);
          obj.material.color.set(0xffff00);
        }
        if (obj.name === "左眼" | obj.name === "右眼") {
          obj.material.color.set(0x000000)
        }
        // 打印id属性
        console.log(obj.id);
        // 打印该对象的父对象
        console.log(obj.parent);
        // 打印该对象的子对象
        console.log(obj.children);
      })
      // 遍历查找scene中复合条件的子对象，并返回id对应的对象
      var idNode = this.scene.getObjectById ( 4 );
      console.log(idNode);
      // 遍历查找对象的子对象，返回name对应的对象（name是可以重名的，返回第一个）
      var nameNode = this.scene.getObjectByName ( "左腿" );
      nameNode.material.color.set(0xff0000);
      // console.log('查看group的子对象',group.children);
      // console.log('查看Scene的子对象',this.scene.children);


      var geometry = new THREE.Geometry(); //声明一个几何体对象Geometry
      //参数：0, 0圆弧坐标原点x，y  100：圆弧半径    0, 2 * Math.PI：圆弧起始角度
      var arc = new THREE.ArcCurve(0, 0, 100, 0, 2 * Math.PI);
      //getPoints是基类Curve的方法，返回一个vector2对象作为元素组成的数组
      var points = arc.getPoints(50);//分段数50，返回51个顶点
      // setFromPoints方法从points中提取数据改变几何体的顶点属性vertices
      geometry.setFromPoints(points);
      //材质对象
      var material = new THREE.LineBasicMaterial({
        color: 0x000000
      });
      //线条模型对象
      var line = new THREE.Line(geometry, material);
      this.scene.add(line); //线条对象添加到场景中

      var geometry = new THREE.Geometry(); //声明一个几何体对象Geometry
      //参数：0, 0圆弧坐标原点x，y  100：圆弧半径    0, 2 * Math.PI：圆弧起始角度
      var arc = new THREE.ArcCurve(0, 0, 100, 0, 2 * Math.PI);
      //getPoints是基类Curve的方法，返回一个vector2对象作为元素组成的数组
      var points = arc.getPoints(50);//分段数50，返回51个顶点
      // setFromPoints方法从points中提取数据改变几何体的顶点属性vertices
      geometry.setFromPoints(points);
      //材质对象
      var material = new THREE.LineBasicMaterial({
        color: 0x000000
      });
      //线条模型对象
      var line = new THREE.Line(geometry, material);
      this.scene.add(line); //线条对象添加到场景中

      var geometry2 = new THREE.Geometry(); //声明一个几何体对象Geometry
      var R = 100; //圆弧半径
      var N = 500; //分段数量
      // 批量生成圆弧上的顶点数据
      for (var i = 0; i < N; i++) {
        var angle = 2 * Math.PI / N * i;
        var x = R * Math.sin(angle);
        var y = R * Math.cos(angle);
        geometry2.vertices.push(new THREE.Vector3(x, y, 0));
      }
      // 插入最后一个点，line渲染模式下，产生闭合效果
      // geometry2.vertices.push(geometry2.vertices[0])
      //材质对象
      var material2 = new THREE.LineBasicMaterial({
        color: 0x000000
      });
      //线条模型对象
      var line2 = new THREE.Line(geometry2, material2);
      line2.rotateY(Math.PI/2);//绕x轴旋转π/4
      this.scene.add(line2); //线条对象添加到场景中

      // var geometry3 = new THREE.Geometry(); //声明一个几何体对象Geometry
      // var p1 = new THREE.Vector3(50, 0, 0); //顶点1坐标
      // var p2 = new THREE.Vector3(0, 170, 0); //顶点2坐标
      // //顶点坐标添加到geometry对象
      // geometry3.vertices.push(p1, p2);
      // var material3 = new THREE.LineBasicMaterial({
      //   color: 0xffff00,
      // });//材质对象
      //线条模型对象
      // var line3 = new THREE.Line(geometry3, material3);
      // this.scene.add(line3); //线条对象添加到场景中

      var geometry4 = new THREE.Geometry(); //声明一个几何体对象Geometry
      var p1 = new THREE.Vector3(50, 0, 0); //顶点1坐标
      var p2 = new THREE.Vector3(0, 70, 0); //顶点2坐标
      // 三维直线LineCurve3
      var LineCurve = new THREE.LineCurve3(p1, p2);
      var pointArr = LineCurve.getPoints(10);
      geometry.setFromPoints(pointArr);
      // 二维直线LineCurve
      // var LineCurve2 = new THREE.LineCurve(new THREE.Vector2(70, 0), new THREE.Vector2(0, 90));
      // var pointArr2 = LineCurve2.getPoints(10);
      // geometry.setFromPoints(pointArr2);

      var geometry5 = new THREE.Geometry(); //声明一个几何体对象Geometry
      // 三维样条曲线  Catmull-Rom算法
      var curve = new THREE.CatmullRomCurve3([
        new THREE.Vector3(-50, 20, 90),
        new THREE.Vector3(-10, 40, 40),
        new THREE.Vector3(0, 0, 0),
        new THREE.Vector3(60, -60, 0),
        new THREE.Vector3(70, 0, 80),
        new THREE.Vector3(-70, 20, 30),
        new THREE.Vector3(0, 60, 80),
        new THREE.Vector3(10, -30, -10),
      ]);
      //getPoints是基类Curve的方法，返回一个vector3对象作为元素组成的数组
      var points = curve.getPoints(100); //分段数100，返回101个顶点
      // setFromPoints方法从points中提取数据改变几何体的顶点属性vertices
      geometry5.setFromPoints(points);
      //材质对象
      var material5 = new THREE.LineBasicMaterial({
        color: 674785,
      });
      //线条模型对象
      var line = new THREE.Line(geometry5, material5);
      this.scene.add(line); //线条对象添加到场景中
      


      // 辅助坐标系  参数250表示坐标系大小，可以根据场景大小去设置
      var axisHelper = new THREE.AxisHelper(250);
      this.scene.add(axisHelper);

      /**
       * 光源设置
       */
      //点光源
      var point = new THREE.PointLight(0xffffff);
      point.position.set(100, 200, 300); //点光源位置
      this.scene.add(point); //点光源添加到场景中
      // // 方向光
      // var directionalLight = new THREE.DirectionalLight(0xffffff, 1);
      // // 设置光源位置
      // directionalLight.position.set(60, 100, 40);
      // this.scene.add(directionalLight);
      // // 设置用于计算阴影的光源对象
      // directionalLight.castShadow = true;
      // // 设置计算阴影的区域，最好刚好紧密包围在对象周围
      // // 计算阴影的区域过大：模糊  过小：看不到或显示不完整
      // directionalLight.shadow.camera.near = 0.5;
      // directionalLight.shadow.camera.far = 300;
      // directionalLight.shadow.camera.left = -50;
      // directionalLight.shadow.camera.right = 50;
      // directionalLight.shadow.camera.top = 200;
      // directionalLight.shadow.camera.bottom = -100;
      // // 设置mapSize属性可以使阴影更清晰，不那么模糊
      // // directionalLight.shadow.mapSize.set(1024,1024)
      // console.log(directionalLight.shadow.camera);
      // // 设置用于计算阴影的光源对象
      // directionalLight.castShadow = true;
      // //定义阴影纹理贴图宽高尺寸的一个二维向量Vector2.
      // directionalLight.shadow.mapSize.set(1024,1024)

      // var spotLight = new THREE.SpotLight(0xffffff);
      // // 设置聚光光源位置
      // spotLight.position.set(60, 200, 40);
      // // 设置聚光光源发散角度
      // spotLight.angle = Math.PI /6
      // this.scene.add(spotLight); //光对象添加到scene场景中
      // // 设置用于计算阴影的光源对象
      // spotLight.castShadow = true;
      // // 设置计算阴影的区域，注意包裹对象的周围
      // spotLight.shadow.camera.near = 1;
      // spotLight.shadow.camera.far = 300;
      // spotLight.shadow.camera.fov = 20;
      // // 设置用于计算阴影的光源对象
      // spotLight.castShadow = true;
      // // 聚光源设置
      // spotLight.shadow.camera.near = 1;
      // spotLight.shadow.camera.far = 300;
      // spotLight.shadow.camera.fov = 20;


      //环境光
      var ambient = new THREE.AmbientLight(0x444444);
      this.scene.add(ambient);
      // console.log(this.scene)
      // console.log(this.scene.children)
      /**
       * 相机设置
       */
      var width = window.innerWidth; //窗口宽度
      var height = window.innerHeight; //窗口高度
      var k = width / height; //窗口宽高比
      var s = 200; //三维场景显示范围控制系数，系数越大，显示的范围越大
      //创建相机对象
      this.camera = new THREE.OrthographicCamera(-s * k, s * k, s, -s, 1,1000);
      this.camera.position.set(200, 300, 200); //设置相机位置
      this.camera.lookAt(this.scene.position); //设置相机方向(指向的场景对象)
      /**
       * 创建渲染器对象
       */
      this.renderer = new THREE.WebGLRenderer();
      this.renderer.setSize(width, height); //设置渲染区域尺寸
      this.renderer.setClearColor(0xb9d3ff, 1); //设置背景颜色
      document.body.appendChild(this.renderer.domElement); //body元素中插入canvas对象

      //创建控件对象
      this.controls = new OrbitControls(this.camera, this.renderer.domElement);
    },
    // 渲染函数
    render() {
      this.renderer.render(this.scene,this.camera);//执行渲染操作
      // this.mesh.rotateY(0.01);//每次绕y轴旋转0.01弧度
      requestAnimationFrame(this.render);//请求再次执行渲染函数render
    },

    // 球体网格模型创建函数
    sphereMesh(R, x, y, z) {
      var geometry = new THREE.SphereGeometry(R, 25, 25); //球体几何体
      var material = new THREE.MeshPhongMaterial({
        color: 0x0000ff
      }); //材质对象Material
      this.mesh = new THREE.Mesh(geometry, material); // 创建网格模型对象
      this.mesh.position.set(x, y, z);
      return this.mesh;
    },
    // 圆柱体网格模型创建函数
    cylinderMesh(R, h, x, y, z) {
      var geometry = new THREE.CylinderGeometry(R, R, h, 25, 25); //球体几何体
      var material = new THREE.MeshPhongMaterial({
        color: 0x0000ff
      }); //材质对象Material
      this.mesh = new THREE.Mesh(geometry, material); // 创建网格模型对象
      this.mesh.position.set(x, y, z);
      return this.mesh;
    },
    // 圆柱体网格模型创建函数
    cylinderMesh1(R, h, x, y, z) {
      var geometry = new THREE.CylinderGeometry(R, R, h, 25, 25); //球体几何体
      var material = new THREE.MeshPhongMaterial({
        color: 0x0000ff
      }); //材质对象Material
      this.mesh = new THREE.Mesh(geometry, material); // 创建网格模型对象
      this.mesh.position.set(x, y, z);
      this.mesh.rotateX(Math.PI/2);//绕x轴旋转π/4
      return this.mesh;
    },


  },
  components: {},
};
</script>

<style scoped rel="stylesheet/stylus" lang="stylus"></style>
