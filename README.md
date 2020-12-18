1.创建场景对象Scene
  this.scene = new THREE.Scene();
2.网格模型添加到场景中
      let geometry = new THREE.BoxGeometry(0.2, 0.2, 0.2);//长宽高
      let material = new THREE.MeshNormalMaterial();
      this.mesh = new THREE.Mesh(geometry, material);
      this.scene.add(this.mesh);
3.
let container = document.getElementById("container");
this.camera = new THREE.PerspectiveCamera(
  70,
  container.clientWidth / container.clientHeight,
  0.01,
  10
);
this.camera.position.z = 1;
4.创建渲染器对象
this.renderer = new THREE.WebGLRenderer({ antialias: true });
this.renderer.setSize(container.clientWidth, container.clientHeight);
container.appendChild(this.renderer.domElement);
5.创建控件对象
this.controls = new OrbitControls(this.camera, this.renderer.domElement);
6.渲染
requestAnimationFrame(this.animate);
this.mesh.rotation.x += 0.01;
this.mesh.rotation.y += 0.02;
this.renderer.render(this.scene, this.camera);

官方 
    /**
     * 创建场景对象Scene
     */
    var scene = new THREE.Scene();
    /**
     * 创建网格模型
     */
    // var geometry = new THREE.SphereGeometry(60, 40, 40); //创建一个球体几何对象
    var geometry = new THREE.BoxGeometry(100, 100, 100); //创建一个立方体几何对象Geometry
    var material = new THREE.MeshLambertMaterial({
      color: 0x0000ff,
    }); //材质对象Material
    this.mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
    scene.add(mesh); //网格模型添加到场景中
    /**
     * 光源设置
     */
    //点光源
    var point = new THREE.PointLight(0xffffff);
    point.position.set(100, 200, 300); //点光源位置
    scene.add(point); //点光源添加到场景中
    //环境光
    var ambient = new THREE.AmbientLight(0x444444);
    scene.add(ambient);
    // console.log(scene)
    // console.log(scene.children)
    /**
     * 相机设置
     */
    var width = window.innerWidth; //窗口宽度
    var height = window.innerHeight; //窗口高度
    var k = width / height; //窗口宽高比
    var s = 200; //三维场景显示范围控制系数，系数越大，显示的范围越大
    //创建相机对象
    var camera = new THREE.OrthographicCamera(-s * k, s * k, s, -s, 1,1000);
    camera.position.set(200, 300, 200); //设置相机位置
    camera.lookAt(scene.position); //设置相机方向(指向的场景对象)
    /**
     * 创建渲染器对象
     */
    var renderer = new THREE.WebGLRenderer();
    renderer.setSize(width, height); //设置渲染区域尺寸
    renderer.setClearColor(0xb9d3ff, 1); //设置背景颜色
    document.body.appendChild(renderer.domElement); //body元素中插入canvas对象
    //执行渲染操作   指定场景、相机作为参数
    renderer.render(scene, camera);

    /*
    1.2
      旋转动画、 requestAnimationFrame 周期性渲染
        requestAnimationFrame相当于一个定时器
    */
    修改代码
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
      var geometry = new THREE.BoxGeometry(100, 100, 100); //创建一个立方体几何对象Geometry
      var material = new THREE.MeshLambertMaterial({
        color: 0x0000ff,
      }); //材质对象Material
      this.mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
      this.scene.add(this.mesh); //网格模型添加到场景中
      /**
       * 光源设置
       */
      //点光源
      var point = new THREE.PointLight(0xffffff);
      point.position.set(100, 200, 300); //点光源位置
      this.scene.add(point); //点光源添加到场景中
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

    },
    // 渲染函数
    render() {
      this.renderer.render(this.scene,this.camera);//执行渲染操作
      this.mesh.rotateY(0.01);//每次绕y轴旋转0.01弧度
      requestAnimationFrame(this.render);//请求再次执行渲染函数render
    },

    /*
      1.3
        鼠标操作三维场景
          1.import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls.js';
          2.初始化时 创建控件对象
              this.controls = new OrbitControls(this.camera, this.renderer.domElement);
          3.左键-旋转
            中键-缩放
            右键-平移
    */

    /*
      1.4
        3D场景中插入新的几何体
        var geometry = new THREE.SphereGeometry(40, 40, 40); //创建一个球体几何对象
        第一个参数radius约束的是球的大小，参数widthSegments、heightSegments约束的是球面的精度
          //长方体 参数：长，宽，高
          var geometry = new THREE.BoxGeometry(100, 100, 100);
          // 球体 参数：半径60  经纬度细分数40,40
          var geometry = new THREE.SphereGeometry(60, 40, 40);
          // 圆柱  参数：圆柱面顶部、底部直径50,50   高度100  圆周分段数
          var geometry = new THREE.CylinderGeometry( 50, 50, 100, 25 );
          // 正八面体
          var geometry = new THREE.OctahedronGeometry(50);
          // 正十二面体
          var geometry = new THREE.DodecahedronGeometry(50);
          // 正二十面体
          var geometry = new THREE.IcosahedronGeometry(50);
        同时绘制多个几何体
          需要创建多次几何体然后 scene.add(mesh1) 添加多次，注意此时的几何体会重叠在一起
        辅助三维坐标系AxisHelper
          var axisHelper = new THREE.AxisHelper(250);
          scene.add(axisHelper);
    */

    /*
      1.5
        材质效果
          color	材质颜色，比如蓝色0x0000ff
          wireframe	将几何图形渲染为线框。 默认值为false
          opacity	透明度设置，0表示完全透明，1表示完全不透明
          transparent	是否开启透明，默认false
        材质类型
          MeshBasicMaterial	基础网格材质，不受光照影响的材质
          MeshLambertMaterial	Lambert网格材质，与光照有反应，漫反射
          MeshPhongMaterial	高光Phong材质,与光照有反应
          MeshStandardMaterial	PBR物理材质，相比较高光Phong材质可以更好的模拟金属、玻璃等效果
    */

    /*
      1.6
        threejs光源
          光源类型
            AmbientLight	环境光
            PointLight	点光源
            DirectionalLight	平行光，比如太阳光
            SpotLight	聚光源
    */

    /*
      2.1
        顶点位置数据解析渲染
          立方体网格模型Mesh是由立方体几何体 geometry (网格模型)和材质 material (材质对象)两部分构成
          new THREE.BufferGeometry(); //创建一个Buffer类型几何体对象
          new THREE.BufferAttribute(vertices, 3) //创建属性缓冲区对象
          渲染模式
            三角面(网格)渲染模式 new THREE.MeshBasicMaterial
            点渲染模式           new THREE.PointsMaterial
            线条渲染模式         new THREE.LineBasicMaterial

          var geometry = new THREE.BufferGeometry(); //创建一个Buffer类型几何体对象
          //类型数组创建顶点数据
          var vertices = new Float32Array([
            0, 0, 0, //顶点1坐标    红绿蓝
            50, 0, 0, //顶点2坐标
            0, 100, 0, //顶点3坐标
            0, 0, 10, //顶点4坐标
            0, 0, 100, //顶点5坐标
            50, 0, 10, //顶点6坐标
          ]);
          // 创建属性缓冲区对象
          var attribue = new THREE.BufferAttribute(vertices, 3); //3个为一组，表示一个顶点的xyz坐标
          // 设置几何体attributes属性的位置属性
          geometry.attributes.position = attribue;

          // 三角面(网格)渲染模式
          var material = new THREE.MeshBasicMaterial({
            color: 0x0000ff, //三角面颜色
            side: THREE.DoubleSide //两面可见
          }); //材质对象
          this.mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh

          // 点渲染模式
          var material = new THREE.PointsMaterial({
            color: 0xff0000,
            size: 10.0 //点对象像素尺寸
          }); //材质对象
          var points = new THREE.Points(geometry, material); //点模型对象
          this.scene.add(points); //点对象添加到场景中

          // 线条渲染模式
          var material=new THREE.LineBasicMaterial({
              color:0xff0000 //线条颜色
          });//材质对象
          var line=new THREE.Line(geometry,material);//线条模型对象
          this.scene.add(line);//线条对象添加到场景中
    */

    /*
      2.2
        顶点颜色数据插值计算
          var geometry = new THREE.BufferGeometry(); //创建一个Buffer类型几何体对象
          //类型数组创建顶点数据
          var vertices = new Float32Array([
            0, 0, 0, //顶点1坐标    红绿蓝
            50, 0, 0, //顶点2坐标
            0, 100, 0, //顶点3坐标

            0, 0, 10, //顶点4坐标
            0, 0, 100, //顶点5坐标
            50, 0, 10, //顶点6坐标
          ]);
          // 创建属性缓冲区对象
          var attribue = new THREE.BufferAttribute(vertices, 3); //3个为一组，表示一个顶点的xyz坐标
          // 设置几何体attributes属性的位置属性
          geometry.attributes.position = attribue;
          //类型数组创建顶点颜色color数据
          var colors = new Float32Array([
            1, 0, 0, //顶点1颜色
            0, 1, 0, //顶点2颜色
            0, 0, 1, //顶点3颜色

            1, 1, 0, //顶点4颜色
            0, 1, 1, //顶点5颜色
            1, 0, 1, //顶点6颜色
          ]);
          // 设置几何体attributes属性的颜色color属性
          geometry.attributes.color = new THREE.BufferAttribute(colors, 3); //3个为一组,表示一个顶点的颜色数据RGB

          // 三角面(网格)渲染模式
          var material = new THREE.MeshBasicMaterial({
            // color: 0x0000ff, //三角面颜色
            vertexColors: THREE.VertexColors, //以顶点颜色为准
            side: THREE.DoubleSide //两面可见
          }); //材质对象
          this.mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
          this.scene.add(this.mesh);//三角面对象添加到场景中
    */

    /*
      2.3
        顶点法向量数据光照计算
          var geometry = new THREE.BufferGeometry(); //声明一个空几何体对象
          //类型数组创建顶点位置position数据
          var vertices = new Float32Array([
            0, 0, 0, //顶点1坐标
            50, 0, 0, //顶点2坐标
            0, 100, 0, //顶点3坐标

            0, 0, 0, //顶点4坐标
            0, 0, 100, //顶点5坐标
            50, 0, 0, //顶点6坐标

          ]);
          // 创建属性缓冲区对象
          var attribue = new THREE.BufferAttribute(vertices, 3); //3个为一组
          // 设置几何体attributes属性的位置position属性
          geometry.attributes.position = attribue
    */

    /*
      2.4
        var geometry = new THREE.BufferGeometry(); //声明一个空几何体对象
        //类型数组创建顶点位置position数据
        var vertices = new Float32Array([
          0, 0, 0, //顶点1坐标
          80, 0, 0, //顶点2坐标
          80, 80, 0, //顶点3坐标
          0, 80, 0, //顶点4坐标
        ]);
        // 创建属性缓冲区对象
        var attribue = new THREE.BufferAttribute(vertices, 3); //3个为一组
        // 设置几何体attributes属性的位置position属性
        geometry.attributes.position = attribue
        var normals = new Float32Array([
          0, 0, 1, //顶点1法向量
          0, 0, 1, //顶点2法向量
          0, 0, 1, //顶点3法向量
          0, 0, 1, //顶点4法向量
        ]);
        // 设置几何体attributes属性的位置normal属性
        geometry.attributes.normal = new THREE.BufferAttribute(normals, 3); //3个为一组,表示一个顶点的xyz坐标
        通过顶点索引组织顶点数据，顶点索引数组indexes通过索引值指向顶点位置geometry.attributes.position、顶点法向量geometry.attributes.normal中顶面数组。

        // Uint16Array类型数组创建顶点索引数据
        var indexes = new Uint16Array([
          // 0对应第1个顶点位置数据、第1个顶点法向量数据
          // 1对应第2个顶点位置数据、第2个顶点法向量数据
          // 索引值3个为一组，表示一个三角形的3个顶点
          0, 1, 2,
          0, 2, 3,
        ])
        // 索引数据赋值给几何体的index属性
        geometry.index = new THREE.BufferAttribute(indexes, 1); //1个为一组
    */

    /*
      2.7
        访问几何体对象的数据
          var geometry = new THREE.BoxGeometry(100, 100, 100); //创建一个立方体几何对象Geometry
          console.log('几何体顶点位置数据',geometry.vertices);
          console.log('三角行面数据',geometry.faces);

          var geometry = new THREE.PlaneBufferGeometry(100, 100);//创建一个矩形平面几何体
          console.log('几何体顶点位置数据',geometry.attributes.position);
          console.log('几何体索引数据',geometry.index);
          var geometry = new THREE.BoxGeometry(100, 100, 100); //创建一个立方体几何对象Geometry
          // 遍历几何体的face属性,删除face就是删除了立方体的面
          geometry.faces.forEach(face => {
            // 设置三角面face三个顶点的颜色
            face.vertexColors = [
              new THREE.Color(0xffff00),
              new THREE.Color(0xff00ff),
              new THREE.Color(0x00ffff),
            ]
          });
          var material = new THREE.MeshBasicMaterial({
            // color: 0x0000ff,
            vertexColors: THREE.FaceColors,
            // wireframe:true,//线框模式渲染
          }); //材质对象Material
    */
    
    /*
      2.8
        几何体旋转、缩放、平移变换
    */
        var geometry = new THREE.BoxGeometry(100, 100, 100); //创建一个立方体几何对象Geometry
        // 几何体xyz三个方向都放大2倍
        geometry.scale(2, 2, 2);
        // 几何体沿着x轴平移50
        geometry.translate(50, 0, 0);
        // 几何体绕着x轴旋转45度
        geometry.rotateX(Math.PI / 4);
        // 居中：偏移的几何体居中
        geometry.center();
        // 几何体xyz方向分别缩放0.5,1.5,2倍
        // geometry.scale(0.5, 1.5, 2);
        console.log(geometry.vertices);
        var material = new THREE.MeshLambertMaterial({
          vertexColors: THREE.FaceColors,
        }); //材质对象Material
        this.mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
        // 网格模型xyz方向分别缩放0.5,1.5,2倍
        // this.mesh.scale.set(0.5, 1.5, 2)
        this.scene.add(this.mesh); //网格模型添加到场景中

    /*
      3.1
        常用材质介绍
          // 创建一个点材质对象
            var material = new THREE.PointsMaterial({
              color: 0x0000ff, //颜色
              size: 3, //点渲染尺寸
            });
            //点模型对象  参数：几何体  点材质
            var point = new THREE.Points(geometry, material);
          // 直线基础材质对象
            var material = new THREE.LineBasicMaterial({
              color: 0x0000ff
            });
            var line = new THREE.Line(geometry, material); //线模型对象
          // 虚线材质对象：产生虚线效果
            var material = new THREE.LineDashedMaterial({
              color: 0x0000ff,
              dashSize: 10,//显示线段的大小。默认为3。
              gapSize: 5,//间隙的大小。默认为1
            });
            var line = new THREE.Line(geometry, material); //线模型对象
            //  computeLineDistances方法  计算LineDashedMaterial所需的距离数组
            line.computeLineDistances();
          // 网格模型
             var material = new THREE.MeshBasicMaterial({
                color: 0xff0000,
                specular:0x444444,//高光部分的颜色
                shininess:20,//高光部分的亮度，默认30
              })
    */

    /*
      3.2
        材质共有属性、私有属性
          side:THREE.DoubleSide//两面可见||true,  THREE.FrontSide//前面||false，  THREE.BackSide//后面
          材质透明度.opacity
    */

    /*
      4.1
        点、线、网格模型介绍
          // 点渲染模式
          var material = new THREE.PointsMaterial({
            color: 0xff0000,
            size: 5.0 //点对象像素尺寸
          }); //材质对象
          var points = new THREE.Points(geometry, material); //点模型对象
          // 线条渲染模式
          var material=new THREE.LineBasicMaterial({
              color:0xff0000 //线条颜色
          });//材质对象
          // 创建线模型对象   构造函数：Line、LineLoop、LineSegments
          var line=new THREE.Line(geometry,material);//线条模型对象
          // 三角形面渲染模式  
          var material = new THREE.MeshLambertMaterial({
            color: 0x0000ff, //三角面颜色
          }); //材质对象
          this.mesh = new THREE.Mesh(geometry, material); //网格模型对象Mesh
    */

    /*
      4.2
        模型对象旋转平移缩放变换
        this.mesh.scale.set(0.5, 1.5, 2) //网格模型xyz方向分别缩放0.5,1.5,2倍
        this.mesh.position.set(80,2,10); //设置模型xyz坐标
        this.mesh.translateX(100);//沿着x轴正方向平移距离100
        沿着自定义的方向移动。
          //向量Vector3对象表示方向
          var axis = new THREE.Vector3(1, 1, 1);
          axis.normalize(); //向量归一化
          //沿着axis轴表示方向平移100
          mesh.translateOnAxis(axis, 100);
        旋转
          mesh.rotateX(Math.PI/4);//绕x轴旋转π/4
          var axis = new THREE.Vector3(0,1,0);//向量axis
          mesh.rotateOnAxis(axis,Math.PI/8);//绕axis轴旋转π/8
    */

    /*
      4.3
        对象克隆.clone()和复制.copy()
          复制方法.copy()
            var p1 = new THREE.Vector3(1.2,2.6,3.2);
            var p2 = new THREE.Vector3(0.0,0.0,0.0);
            p2.copy(p1)
          克隆方法.clone()
            var p1 = new THREE.Vector3(1.2,2.6,3.2);
            var p2 = p1.clone();
          this.scene.add(mesh,mesh2,mesh3,mesh4,mesh5);//网格模型添加到场景中
    */

    /*
      5.1
        常见光源类型
        //环境光:环境光颜色RGB成分分别和物体材质颜色RGB成分分别相乘
          var ambient = new THREE.AmbientLight(0x444444);
          scene.add(ambient);//环境光对象添加到scene场景中
          //点光源
            var point = new THREE.PointLight(0xffffff);
            //设置点光源位置，改变光源的位置
            point.position.set(400, 200, 300);
            scene.add(point);
          // 平行光
            var directionalLight = new THREE.DirectionalLight(0xffffff, 1);
            // 设置光源的方向：通过光源position属性和目标指向对象的position属性计算
            directionalLight.position.set(80, 100, 50);
            // 方向光指向对象网格模型mesh2，可以不设置，默认的位置是0,0,0
            directionalLight.target = mesh2;
            scene.add(directionalLight);
          // 聚光光源
            var spotLight = new THREE.SpotLight(0xffffff);
            // 设置聚光光源位置
            spotLight.position.set(200, 200, 200);
            // 聚光灯光源指向网格模型mesh2
            spotLight.target = mesh2;
            // 设置聚光光源发散角度
            spotLight.angle = Math.PI / 6
            scene.add(spotLight);//光对象添加到scene场景中
    */

    /*
      5.2
        Three.js光照阴影实时计算
          1.首先创建投影面
            var box=new THREE.BoxGeometry(100,100,100);//创建一个立方体几何对象
            var material=new THREE.MeshLambertMaterial({color:0x0000ff});//材质对象
            this.mesh=new THREE.Mesh(box,material);//网格模型对象
            this.scene.add(this.mesh);//网格模型添加到场景中
            // 设置产生投影的网格模型
            this.mesh.castShadow = true;
            //创建一个平面几何体作为投影面
            var planeGeometry = new THREE.PlaneGeometry(300, 200);
            var planeMaterial = new THREE.MeshLambertMaterial({
              color: 0x999999
            });
            // 平面网格模型作为投影面
            var planeMesh = new THREE.Mesh(planeGeometry, planeMaterial);
            this.scene.add(planeMesh); //网格模型添加到场景中
            planeMesh.rotateX(-Math.PI / 2); //旋转网格模型
            planeMesh.position.y = -50; //设置网格模型y坐标
            // 设置接收阴影的投影面
            planeMesh.receiveShadow = true;
          2.平行光投影计算代码
            var directionalLight = new THREE.DirectionalLight(0xffffff, 1);
            // 设置光源位置
            directionalLight.position.set(60, 100, 40);
            this.scene.add(directionalLight);
            // 设置用于计算阴影的光源对象
            directionalLight.castShadow = true;
            // 设置计算阴影的区域，最好刚好紧密包围在对象周围
            // 计算阴影的区域过大：模糊  过小：看不到或显示不完整
            directionalLight.shadow.camera.near = 0.5;
            directionalLight.shadow.camera.far = 300;
            directionalLight.shadow.camera.left = -50;
            directionalLight.shadow.camera.right = 50;
            directionalLight.shadow.camera.top = 200;
            directionalLight.shadow.camera.bottom = -100;
            // 设置mapSize属性可以使阴影更清晰，不那么模糊
            // directionalLight.shadow.mapSize.set(1024,1024)
            console.log(directionalLight.shadow.camera);
            // 设置用于计算阴影的光源对象
            directionalLight.castShadow = true;
            //定义阴影纹理贴图宽高尺寸的一个二维向量Vector2.
            directionalLight.shadow.mapSize.set(1024,1024)
          3.聚光光源投影计算代码
            var spotLight = new THREE.SpotLight(0xffffff);
            // 设置聚光光源位置
            spotLight.position.set(60, 200, 40);
            // 设置聚光光源发散角度
            spotLight.angle = Math.PI /6
            this.scene.add(spotLight); //光对象添加到scene场景中
            // 设置用于计算阴影的光源对象
            spotLight.castShadow = true;
            // 设置计算阴影的区域，注意包裹对象的周围
            spotLight.shadow.camera.near = 1;
            spotLight.shadow.camera.far = 300;
            spotLight.shadow.camera.fov = 20;
            // 设置用于计算阴影的光源对象
            spotLight.castShadow = true;
            // 聚光源设置
            spotLight.shadow.camera.near = 1;
            spotLight.shadow.camera.far = 300;
            spotLight.shadow.camera.fov = 20;
    */

    /*
      5.3
        基类Light和Object3D
          光源位置属性
            1.光源对象继承父类Object3D的位置属性.position。
              以点光源PointLight 为例，PointLight的基类是Light，Light的基类是Object3D，点光源自然继承对象Object3D的位置属性.position。
                var point = new THREE.PointLight(0xffffff);//点光源
                //设置点光源位置  
                //光源对象和模型对象的position属性一样是Vector3对象
                point.position.set(400, 200, 300);
            2.光源对象的.add()方法同样继承自基类Object3D
              //环境光对象添加到scene场景中
              scene.add(ambient);
              //点光源对象添加到scene场景中
              scene.add(point);
            3.光源颜色属性.color和强度属性.intensity
              光源颜色属性.color默认值是白色0xffffff,强度属性.intensity默认1.0,光照计算的时候会把两个属性值相乘。
              //环境光：颜色设置为`0xffffff`,强度系数设置为0.5
              var ambient = new THREE.AmbientLight(0xffffff,0.5);
              scene.add(ambient);
    */

    /*
      5.4
        组对象Group、层级模型
          //创建两个网格模型mesh1、mesh2
          var geometry = new THREE.BoxGeometry(100, 100, 100);
          var material = new THREE.MeshLambertMaterial({color: 0x0000ff});
          var group = new THREE.Group();
          var mesh1 = new THREE.Mesh(geometry, material);
          var mesh2 = new THREE.Mesh(geometry, material);
          mesh2.translateX(150);
          //把mesh1型插入到组group中，mesh1作为group的子对象
          group.add(mesh1);
          //把mesh2型插入到组group中，mesh2作为group的子对象
          group.add(mesh2);
          //把group插入到场景中作为场景子对象
          this.scene.add(group);
          // 删除父对象group的子对象网格模型mesh1
          group.remove(mesh1)
          // 一次删除场景中多个对象
          this.scene.remove(group)
          console.log('查看group的子对象',group.children);
          console.log('查看Scene的子对象',this.scene.children);
    */

    /*
      6.2
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
    */

    /*
      6.3
        Three.js获得世界坐标.getWorldPosition()
          // 声明一个三维向量用来保存世界坐标
            var worldPosition = new THREE.Vector3();
            // 执行getWorldPosition方法把模型的世界坐标保存到参数worldPosition中
            mesh.getWorldPosition(worldPosition);

            你首先在案例中测试下面源码，通过位置属性.position和.getWorldPosition()分别返回模型的本地位置坐标和世界坐标，查看两个坐标x分量有什么不同。你可以看到网格模型mesh通过位置属性.position返回的坐标x分量是50，通过.getWorldPosition()返回的坐标x分量是100，也就是说mesh的是世界坐标是mesh位置属性.position和mesh父对象group位置属性.position的累加。
              var mesh = new THREE.Mesh(geometry, material);
              // mesh的本地坐标设置为(50, 0, 0)
              mesh.position.set(50, 0, 0);
              var group = new THREE.Group();
              // group本地坐标设置和mesh一样设置为(50, 0, 0)
              // mesh父对象设置position会影响得到mesh的世界坐标
              group.position.set(50, 0, 0);
              group.add(mesh);
              scene.add(group);
              // .position属性获得本地坐标
              console.log('本地坐标',mesh.position);
              // getWorldPosition()方法获得世界坐标
              //该语句默认在threejs渲染的过程中执行,如果渲染之前想获得世界矩阵属性、世界位置属性等属性，需要通过代码更新
              scene.updateMatrixWorld(true);
              var worldPosition = new THREE.Vector3();
              mesh.getWorldPosition(worldPosition);
              console.log('世界坐标',worldPosition);

            总结
              下面对上面的案例实验进行总结。
              所谓本地坐标系或者说模型坐标系，就是模型对象相对模型的父对象而言，模型位置属性.position表示的坐标值就是以本地坐标系为参考，表示子对象相对本地坐标系原点(0,0,0)的偏移量。
              前面两节课说过Threejs场景Scene是一个树结构，一个模型对象可能有多个父对象节点。世界坐标系默认就是对Threejs整个场景Scene建立一个坐标系，一个模型相对世界坐标系的坐标值就是该模型对象所有父对象以及模型本身位置属性.position的叠加。
    */

    /*
      7.1
        常见几何体和曲线API介绍
    */

    /*
      7.2
        直线、椭圆、圆弧、基类Curve
          1.圆弧线ArcCurve
            ArcCurve( aX, aY, aRadius, aStartAngle, aEndAngle, aClockwise )
              aX, aY	圆弧圆心坐标
              aRadius	圆弧半径
              aStartAngle, aEndAngle	起始角度
              aClockwise	是否顺时针绘制，默认值为false
          2.曲线Curve方法.getPoints()
            .getPoints()是基类Curve的方法，圆弧线ArcCurve的基类是椭圆弧线EllipseCurve,椭圆弧线的基类是曲线Curve，所以圆弧线具有Curve的方法.getPoints()。
          3.几何体方法.setFromPoints()
            .setFromPoints()是几何体Geometry的方法，通过该方法可以把数组points中顶点数据提取出来赋值给几何体的顶点位置属性geometry.vertices，数组points的元素是二维向量Vector2或三维向量Vector3。
          4.绘制圆弧线案例
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
          5.绘制直线效果
              1.
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
              2.
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

    */