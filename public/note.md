# 戒浮躁
从一期课程开始认真学习
可以尝试一期二期对应部分一起看

(๑•̀ㅂ•́)و✧加油，你是，最笨的！

### 防止没有初始值报错
``` vue
<!--变量不为空才加载该模块-->
    <div v-if="seller.support"></div>

// 给seller初始值，防止报错
    seller: {
      type: Object,
      default() {
        return {}
      }
    }
```

### 引入组件要局部注册，才可以使用
```vue
<template>
  <div>
    <support-ico/>
  </div>
</template>

<script>
// 注意，引入的名称是驼峰制，但模板引用是a-b
import SupportIco from '~components/support-ico-support-ico'
  export default {
    name: 'v-header',
    // 注册
    components: { 
      SupportIco,
    }
  }
</script>
```

### 学习AXIOS, promise?

### 如何mock api呢，比如，用于现有的react项目中？

### 全屏/弹窗类组件，建议放到body下，而不是组件内部
避免被父组件影响
使用 cube-ui create-api
把组件申明从声明式，转换成调用式，像alert(...)，
并且会放到body下

todo 2019-06-15 20:37 学习create-api 

### 组件就近维护
把组件文件和相应的图片等资源，放在同一个文件夹中，有利于维护

### SVG -> icon font
todo 2019-06-18 13:30 
利用IcoMoon

### mock数据
旧版本：
在dev-server.js（webpack打包入口文件），引入data.json，
然后定义数据相关的变量 （与新版本的vue.config.js中类似）
```javascript
var app = express();

var appData = require('../data.json');
var seller = appData.seller;

var apiRoutes = express.Router();
apiRoutes.get('/seller', function (req, res)) {
  res.json({
    errno: 0,
    data: seller,
  })
}

// 这个'/api'是自己定义的吧？
app.use('/api', apiRoutes);
```
**注意，更新该配置文件，需要手动重新编译！**


### jsonview chrome插件

### props
```vue
// 对象语法，提供校验
Vue.component('props-demo-advanced', {
  props: {
    // 检测类型
    height: Number,
    // 检测类型 + 其他验证
    age: {
      type: Number,
      default: 0,
      required: true,
      validator: function (value) {
        return value >= 0
      }
    }
  }
})

```

### CSS细节
1. 消除空白字符带来的间隔,给父元素设置font-size:0,再给子元素设字号

2. 图文混排，**对图片设置vertical-algin: top**即可实现水平对齐

3. 网页布局常用字体： ‘PingFang SC', 'STHeitiSC-Light', 'Helvetica-Light', arial, sans-serif.

### tab知识
1. v-model双向绑定了计算属性selectedLabel，
2. 点击tab调用了selectedLabel的get和set


#### display: table替代方案
 /*--version 2--*/
        /*display: flex*/
        /*flex-direction column*/
        /*justify-content center*/
        /*align-items center*/
        /*--version 2 end--*/
