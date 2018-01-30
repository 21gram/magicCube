##开发笔记：

1. blender默认是不能导出为json类型的模型的，要从github上的threejs项目里下载代码，把addons里的io_three文件夹copy到blender安装目录里的相应位置D:\Program Files\Blender Foundation\Blender\2.79\scripts\addons，然后在用户设置-插件那里开启这个插件

2. threejs的这个导出插件，不同版本会有不同的问题，有的导出很慢，感觉现在还没稳定下来，可能是我导出的时候没设置对吧。

3. 导出来之前，要把正方体的每一面都三角化。

4. 导出来的时候，建模时设计的正方体圆角效果都没有了，估计没设置对？

5. 导出来之后，模型的坐标是错乱的，我用的是r86的版本，导出来之后每个mesh要x *= -1, z *= -1才能正常使用，其它版本或模型可能处理方式不一样。网上看到的其他人有不同的处理方法。

6. threejs里的add方法是移动元素，不是复制哦。

7. 转动魔方某一面的时候，先把该面的9个小格放到一个Group或Object3D里，然后转动这个父级元素，而不是转动每个小格。

8. 转动完之后，要把小格从Group里放回scene，但要先把小格的position计算好。使用child.applyMatrix(matrixWorld)计算元素的matrix。这是本地空间(this.matrix)和世界空间(this.matrixWorld)进行坐标转换。

9. 更新完matrix之后，postion会有偏差，不准确。因为建模的时候定好每一格的大小是1，位置都是整数。用Math.round方法限制postion的xyz都是整数。