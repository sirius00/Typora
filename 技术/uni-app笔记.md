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
| 打开新页面 | 新页面入栈                        | 调用 API  [uni.navigateTo](https://uniapp.dcloud.io/api/router#navigateto) 、使用组件 '<navigator open-type="navigaator">  ' |
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





# tips:

1. ## uni-app在使用v-for时block和view的使用区别:

   使用view自带换行效果

   使用block时,不带换行效果

