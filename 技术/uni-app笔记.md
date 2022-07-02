## 全局文件

### pages.json页面路由

​	

### mainfest.json应用配置

### uni.scss文件

​	作用:为了方便整体控制应用的风格。比如按钮颜色、边框风格，`uni.scss`文件里预置了一批scss变量预置

### main.js文件

​	项目的入口文件,主要作用是初始化vue实例并使用需要的插件

### unpackage

​	打包目录

## 页面

### 页面生命周期	

#### **onLoad:** 

​	监听页面加载,其参数为上个页面传递的数据,参数类型为object

#### **onShow:**	

​	监听页面显示.页面每次出现在屏幕上都出发

#### **onReady:**

​	监听页面初次渲染完成

#### **onHide:**

 	监听页面隐藏

#### **onUnload:**

​	监听页面卸载

#### **onPullDownRefresh:**

​	监听用户下拉刷新

- 两种方式开启下拉刷新:

  - 需要在*pages.json* 里,找到当前页面的pages节点,并在style选项中开启 *enablePullDownRefresh*

  - 通过调用uni.startPullDownRefresh方法来开启下拉刷新

    ```js
    // 仅做示例，实际开发中延时根据需求来使用。
    export default {
    	data() {
    		return {
    			text: 'uni-app'
    		}
    	},
    	onLoad: function (options) {
    		setTimeout(function () {
    			console.log('start pulldown');
    		}, 1000);
    		uni.startPullDownRefresh();
    	},
    	onPullDownRefresh() {
    		console.log('refresh');
    		setTimeout(function () {
    			uni.stopPullDownRefresh();
    		}, 1000);
    	}
    }
    ```

### 页面调用接口

### 页面通讯

#### 父传子

1. 父组件通过零v-bind绑定数据

   ```
   
   ```

   

2. 子组件通过props接收来自外界传递到组件内部的值

   

#### 子传父

通过$emit触发事件进行传递参数

1. 为子组件methods添加emit触发事件

   - 设置参数:触发事件的名称, 所传参数
   - `this.$emit('myEven', this.num)`

2. 父组件接收该事件

   - 在父组件相应的子组件位置接收该触发事件

     `<test v-if="flag" :title="title" @myEven="getNum"></test>`

   - 在父组件methods中添加相应的方法 (getNum)

#### 兄弟组件

##### uni.$emit(eventName,OBJECT)

​	触发全局的自定义事件.附加参数都会传给监听器回调

##### uni.$on(eventName,callback)

​	监听全局的自定义事件, 事件可以由uni.emit触发, 回调函数会接收所有传入事件触发函数的额外参数

​	被修改界面添加监听

```
		created() {
			uni.$on('update', num => {
				this.num += num
			})
		}
```

​	修改数据界面添加事件

```
		methods: {
			addNum() {
				uni.$emit('update',this.num)
			}
		}
```



##### uni.$once(eventName,callback)

​	监听全局的自定义事件, 但是只触发一次,在触发之后移除监听器	

##### uni.$off([eventName, callback])

​	移除全局自定义事件监听器

### 页面路由跳转 

#### 页面路由跳转方式:

##### navigator组件跳转



##### 调用API跳转:



| 路由方式   | 页面栈表现                        | 触发时机                                                     |
| ---------- | --------------------------------- | ------------------------------------------------------------ |
| 打开新页面 | 新页面入栈                        | 调用 API  [uni.navigateTo](https://uniapp.dcloud.io/api/router#navigateto) 、使用组件 `<navigator open-type="navigaator">` |
| 页面重定向 | 当前页面出栈，新页面入栈          | 调用 API  [uni.redirectTo](https://uniapp.dcloud.io/api/router#redirectto) 、使用组件 `<navigator open-type="redirectTo">` |
| 页面返回   | 页面不断出栈，直到目标返回页      | 调用 API  [uni.navigateBack](https://uniapp.dcloud.io/api/router#navigateback)  、使用组件 `<navigator open-type="navigatorBack">` 、用户按左上角返回按钮、安卓用户点击物理back按键 |
| Tab 切换   | 页面全部出栈，只留下新的 Tab 页面 | 调用 API  [uni.switchTab](https://uniapp.dcloud.io/api/router#switchtab) 、使用组件 `<navigator open-type="switchTab">` 、用户切换 Tab |
| 重加载     | 页面全部出栈，只留下新的页面      | 调用 API  [uni.reLaunch](https://uniapp.dcloud.io/api/router#relaunch) 、使用组件  `<navigator open-type="reLaunch">` |

## 组件

### 内置组件

#### 视图容器



#### 基础内容



#### 表单组件



#### 路由及页面跳转

​	[页面路由跳转](# 页面路由跳转)



#### 媒体组件



#### 画布

canvas

### 组件的生命周期

#### **beforeCreate:**

​	在实例初始化之前被调用

#### **created:**

​	在实例创建完成后被立即调用

#### **beforeMount:**

​	在挂载开始之前被立即调用

#### **mounted:**

​	挂载到实例上去之后调用

#### **beforeUpdate:**

​	数据更新之前调用,发生在虚拟DOM打补丁之前

#### **update:**

​	由于数据更改导致的虚拟DOM重新渲染和打补丁,在这之后会调用该钩子

#### **beforeDestroy:**

​	实例销毁之前调用

#### **destroyed:**

​	Vue实例销毁之后调用.调用后,vue实例指示的所有东西都会解绑,所有的事件监听器会被移除,所有的子实例也会被销毁

## API

### 绘画(canvas)



## 配置网路请求

由于平台的限制,小程序项目中不支持使用axios, 而且原生的wx.request(), API功能较为简单,不支持拦截器等全局定制的功能.因此建议在uni-app项目中使用  *@escook/request-miniprogram* 第三方包发起网络数据请求

官方文档 [@escook/request-miniprogram](https://www.npmjs.com/package/@escook/request-miniprogram)



在项目的 <u>main.js</u> 文件中,通过如下方式进行配置:

```js
import { $http } from '@escook/request-miniprogram'

// 在 uni-app 项目中，可以把 $http 挂载到 uni 顶级对象之上，方便全局调用
uni.$http = $http

// 请求的根路径
$http.baseUrl = 'https://wwww.xxxxxxxx.com'

// 请求拦截器
$http.beforeRequest = function (options) {
  uni.showLoading({
	  title: "数据加载中..."
  })
}

// 响应拦截器
$http.afterRequest = function () {
  uni.hideLoading()
}
```

使用:

```js
//获取轮播图数据
async getSwiperList() {
      // 1、 发起请求（请求返回的是一个promise对象，我们可以用async和await来做优化）
      const { data: res } = await uni.$http.get('/api/xxx/xxx/xxx/swiperData')
      console.log('查看请求的结果=>>',res);
      // 2、 请求失败
      if (res.meta.status !== 200) {
        return uni.showToast({
          title: '数据请求失败！',
          duration: 1500,
          icon: 'none',
        })
      }
      // 3、 请求成功，为 data 中的数据赋值
      this.swiperList = res.message;
    },
```







# tips:

## uni-app在使用v-for时block和view的使用区别:



使用view自带换行效果

使用block时,不带换行效果

## 关于uni-app中使用canvas,在H5不显示问题

### 需要注意的问题:

1. 组件嵌套,在子组件中不能使用canvas ,也不是说不能,只能说使用了也没用,H5中显示无果,小程序一样.(我在uniapp社区提出这个bug ,但是我看有人在今年的6.7月份也提出过,但至今为止没有解决这个问题)
2. 在H5中 出现canvas闪烁的问题 ,就一定要用异步去显示canvas,
3. 绘制canvas 时  得用uniapp 中的draw()去绘制,不然 不会显示(原生一般直接填充就完事了)
4. 一定要在onReady函数中进行实例化canvas并且绘制 



```vue
 
<template>
	<view class="">
        <view style="margin:0 auto;width: 200px;padding-left: 10px;">
           <canvas style="width:  200px;; height: 200px;border: #007AFF solid 1rpx;" canvas-id="myCanvas" id="myCanvas"></canvas>
        </view>
</view>
 
</template>
 
 
<script>
export default {
 
	onReady() {
	    this.initCanvas()
	},
 
	data() {
		return {
			wendu:16
		}
	},
	methods: {
		/*初始化画布*/
		initCanvas() {
			const ctx = uni.createCanvasContext('myCanvas',this)
			ctx.beginPath();
			ctx.arc(100,100,60,0.7*Math.PI,0.30*Math.PI);
			ctx.createLinearGradient(0,0,170,0);
			/* 渐变 */
			const grd=ctx.createLinearGradient(0,0,170,0);
			grd.addColorStop("0.7","#09C4D5");
			grd.addColorStop(1,"#07D2B8");
			ctx.strokeStyle = grd;
			ctx.lineWidth = 8;
			/* 字体 */
			ctx.font="40px Arial";		//设置字体大小
			ctx.fillStyle = '#09C4D5';//fillStyle填充颜色
			ctx.fillText("16",73,110); //fillText("字体",x,y)
			ctx.font="20px Arial"	
			ctx.fillStyle = 'gray';
			ctx.fillText("℃",115,88);
			ctx.font="12px Arial"
			ctx.fillStyle = 'gray';
			ctx.fillText("室内温度",77,130);
			/* 阴影 */
			ctx.shadowBlur=2;
			ctx.shadowColor="#09C4D5";
			setTimeout(function(){	//必须延迟执行 不然H5不显示
				ctx.stroke();
				ctx.draw()		//必须加上  uniapp 没这儿玩意儿 显示不出来不比原生  不加可以显示
			 },200) 
		},
	},
 
</script>
```

