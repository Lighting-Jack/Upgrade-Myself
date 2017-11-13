# 自学路径
### canvas学习
1. 由点及线，由线及面
```
* 1、beginPath
     *  开启全新的绘制，覆盖之前的状态设置，运用全新的状态
     *  beginPath + lineTo = moveTo
     * 2、closePath
     *  表示当前路径需要封闭，与beginPath配合使用
     * 3、fill
     *  先瞄边（stroke）后填充（fill）会导致填充色覆盖部分瞄边
     * 4、rect( // 绘制矩形
     *  x, // 绘制起点横坐标
     *  y, // 绘制起点纵坐标
     *  width, // 绘制宽度
     *  height // 绘制高度
     * )
     *  5、 fillStyle - rgb、rgba、hls、hlsa、纯色
     *  6、fillRect(
     *      x, // 填充起点横坐标
     *      y, // 填充起点纵坐标
     *      width, // 填充宽度
     *      height // 填充高度
     *  )
     *  7、strokeRect(
     *      x, // 瞄边起点横坐标
	 *      y, // 瞄边起点纵坐标
	 *      width, // 瞄边宽度
	 *      height // 瞄边高度
   *  8、lineCap --- round/butt/square // 仅作用于线条端点，不作用于连接处
     *  9、lineJoin
     *      round 连接处添加一个圆弧
     *      miter 连接处添加一个三角形 默认
     *      bevel 连接处添加一个多边形
     * 10、miterLimit
     *  默认是10，计算起来有点复杂
     *  )
```
2. 图形变换
```
1、translate(
     *     x, // 横向偏移
     *     y // 纵向偏移
     * )
     * 2、rotate( // 旋转中心默认在canvas左上角，想要围绕中心旋转，需要反向translate
     *     deg // 旋转角度
     * )
     * 3、scale( // 放大的不止是宽高，还有横坐标、纵坐标、线条宽度
     *     sx, //横向放大倍数
     *     sy // 纵向放大倍数
     * )
     * 4、transform( // 存在级联效果
     *     a, // 水平缩放
     *     b, // 水平倾斜
     *     c, // 垂直倾斜
     *     d, // 垂直缩放
     *     e, // 水平位移
     *     f  // 垂直位置
     * )
     * 5、setTransform( // 可消除级联效果，先将矩阵转换为单位矩阵再进行变换
     *     a,
     *     b,
     *     c,
     *     d,
     *     e,
     *     f
     * )
```
3. 与canvas进行交互
```
*    1. ctx.drawImage( image, dx, dy ); // 图片，目标图片距离画布的横向距离，目标图片距离画布的纵向距离
		 *    2. ctx.drawImage( image, dx, dy, dw, dh ); // dw: 目标图片绘制宽度;dh：目标图片绘制高度
		 *    3. ctx.drawImage(
		 *        image,
		 *        sx,sy,sw,sh, // 源图片的位置、宽、高
		 *        dx,dy,dw,dh     // 目标图片的位置、宽、高
		 *    )
		 *    4. ctx.drawImage(
		 *        canvas,
		 *        目标canvas距离画布的横向距离，
		 *        目标canvas距离画布的纵向距离
		 *    )
```
3. 图片像素的处理
```
1、getImageData用法
             *  ctx.getImageData(
             *      x, 起点横坐标
             *      y, 起点纵坐标
             *      w, 提取宽度
             *      h  提取高度
             *  )
             *  返回一个imageData对象 {
             *      width, 像素宽
             *      height， 像素高
             *      data， 像素内容
             *  }
             * 2、putImageData用法
             *   ctx.putImageData(
             *     imageData, 图片像素
             *     dx,dy, 图片像素距离目标canvas的位移
             *     dirtyX,dirtyY, 图片像素距离原始canvas的距离
             *     dirtyW,dirtyH 图片像素在原始canvas的大小
             *   )
             * 3、imageData.data
             *  将二维画布像素转换为一维数组，每四个元素为一组，存放一个像素的rgba值
             *  第i个像素
             *      r = pixelData[4*i+0]
             *      g = pixelData[4*i+1]
             *      b = pixelData[4*i+2]
             *      a = pixelData[4*i+3]
             *  第x行第y列像素
             *      i = x*width + y
             * 4、灰度滤镜算法
             *  grey = r*0.3 + g*0.59 + b*0.11
             *  r = g = b = grey
             * 5、黑度滤镜算法
             *  grey = r*0.3 + g*0.59 + b*0.11
             *  black = grey > 255/2 ? 255 : 0
			 *  r = g = b = black
             * 6、反色滤镜算法
             *  r = 255 - r
             *  g = 255 - g
             *  b = 255 - b
             * 7、模糊滤镜算法
             *  每个像素点的rgb值以及其周围的像素点的rgb值取平均值，
             *  然后赋值给该像素点
             * 8、马赛克滤镜算法
             *  每个像素点及周围像素点的rgb值取平均值，然后赋值给这一组像素点
```
