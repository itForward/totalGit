#浅谈移动端rem布局#

移动端布局，不用关心IE6 7 8浏览器兼容等问题，只要兼容chrome内核浏览器，但是要注意尺寸的兼容。移动端布局具有多种方式，简单总结下来，主要包括以下四种方式：

**1,流体布局(百分比布局)**

* 100% 
* %  -> 相对 父级宽度
* 优点：适配各种设备
* 缺点：字体不能百分比，很少有一款跟设计师图纸一样
* 宽度一定是百分比
* 高度要么写死，要么自适应

**2,定宽布局**

* 加min-width ，max-width
* 宽度：最外层盒子加min-width ，max-width
* 横方向适应，纵方向跟之前一样

**3,响应式布局**

* 主要是媒体查询，根据不同尺寸，做出不同的展示
* 优点：
面对不同分辨率设备灵活性强，能够快捷解决多设备显示适应问题
* 缺点：
兼容各种设备工作量大，效率低下，代码累赘，会出现隐藏无用的元素，加载时间加长

其实这是一种折中性质的设计解决方案，多方面因素影响而达不到最佳效果
一定程度上改变了网站原有的布局结构，会出现用户混淆的情况

**4， 相对单位布局**

* %	相对父级宽度
* em	相对父级字体大小
* rem	相对根字体html字体的大小
* vw--viewport width   相对可视区宽度
	* 1vw=等于视口宽度的 1%
* vh--viewport height  相对可视区高度
	* 1vh=等于视口高度的 1%

vmin	可视区宽度和高度比较小的那个值

vmax    可视区宽度和高度比较大的那个值

##现在着重介绍一下rem布局：##
在实际开发中，设计师会设计不同尺寸的设计图。640px、750px、1080px等，根据不同的尺寸，应该怎么使用rem进行计算呢。下面简单介绍一下：
		
假如设计图大小为1080px,那么为了方便计算，我们取html{font-size:100px;},那么为了适配不同的尺寸，我们需要写上以下代码来整体把控各个尺寸下，通过设置html的font-size值来控制全局的rem输出，这段代码其实是这个rem的精髓所在。并且我们需要给最外层盒子设置一下宽度，不妨给最外层盒子定义个class,名字是wrap，那么此时，.wrap{width:10.8rem;} 则具体代码为：

	html{font-size: 100px;}
	.wrap{width:10.8rem;}

	<script>
		window.onload=window.onresize=function()
		{
			document.documentElement.style.fontSize=document.documentElement.clientWidth/10.8+'px';
		};
	</script>


上述代码document.documentElement.clientWidth/10.8部分实际就是document.documentElement.clientWidth/（1080/100）;如果此时换成640px的设计图，html的字体大小仍然是100px的话，那么此时应该改为：
		
	html{font-size: 100px;}
	.wrap{width:6.4rem;}

	<script>
		window.onload=window.onresize=function()
		{
				document.documentElement.style.fontSize=document.documentElement.clientWidth/6.4+'px';
		};
	</script>

**给margin padding 设置rem**

上面展示的是怎么通过计算获取到不同分辨率下的html font-site的值。实际开发如果设计师是按照640的宽度去设计的，那么对于margin-top:50px;padding-top:30px;换算成rem就是：

	margin-top:0.5rem;/*50/100=0.5*/
	padding-top:0.3rem;/*30/100=0.3*/
同样的还可以设置border、width、height等一切尺寸转换成rem进行切图。

rem的使用我只是总结了大家比较常用的一些属性，其实他的范围肯定不止是这么多，实际的项目开发中我相信大家在使用他的过程会发现许多惊喜的。