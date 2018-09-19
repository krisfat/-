# 旋转图片验证码
<p>极速漫画 或者类似于蘑菇街的旋转图片验证码的破解.</p>
<p>之前偶然间发现旋转图片进行验证的这种验证码，看到没有人写出一个完整的方法，所以就自己写了一个，小弟不才入行不到两年，对图像对比这方面还是不算精通，而且获取图片的时候图片的质量会有所降低，可能会有一些瑕疵，识别率达不到100%，忘大家海涵。</p>
<p>首先在破解这个图片验证码的时候，所考虑的第一个问题，就是找到图片。在登录页面的开发者工具中，发现了图片的来源。</p>
![登录页面](/Users/krisfat/GIT/Picture-verification-code/屏幕快照 2018-09-19 下午12.40.22.png)
<pre><code>background-image: url("/image3.ashx?t=1537331812000")
</code></pre>	  
这个属性中url中？后为提交的时间戳，前面为提交的地址，所以我访问了域名加上这段接口尝试一下。
![原始图片](/Users/krisfat/Desktop/屏幕快照 2018-09-19 下午12.57.36.png)  
这里可以拿到显示的四张验证码的所有图片，这里只要循环，一直在从这个url获取图片，理论上就可以拿到该网站的所有图片。  
之后将获取到由16张小图构成的大图进行切割，切割成小图，这里只要去第一排的四张就行，要是16张图片全部都获取的话，之后进行比对的时候耗时太长。  
获取到所有的小图之后。  
这时候所有的图片面向四个方向的都有，并且有很多重复的，所以先进行去重。将图片转换成直方图数据进行对比。  
![小图](/Users/krisfat/Desktop/屏幕快照 2018-09-19 下午1.12.57.png)
之后剩下的图片就少了很多。将剩下的图片全部转到正确的方向。windows选中统一方向的图片，右键，旋转。mac选中所有的之后通过预览打开，command + a 全选，command + r进行旋转。  
这时直方图算法不能在进行去重了，可以使用一下软件进行去重或者手动（其实第一步也可以使用去重的软件，但是一开始我没找到 - -!!）  
这是基本就拿到了该网站的所有图片的正确方向了，之后登录的时候获取网上的图片进行旋转对比，找到旋转的次数，通过这个次数进行点击就可以了，具体的看代码。  
但是有一些问题就是，在进行图片验证的时候，网上截图会和我之前下载的图片存在一些差别，个别图片会存在像素点界别的差距，还有几张图片过于相似，所以成功率大概有80%左右，如果失败了，请在此尝试。如果您对图片对比方面有更高的见解，可以联系我，进行完善。

