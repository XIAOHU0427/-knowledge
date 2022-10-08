###Vue Router是如何传参的  
####query和params是什么？  
params：/router1/:id ，/router1/123，/router1/789 ,这里的id叫做params  
query：/router1?id=123 ,/router1?id=456 ,这里的id叫做query。  
####路由界面：  
router.js:  
路由设置这里，当你使用params方法传参的时候，要在路由后面加参数名，并且传参的时候，参数名要跟路由后面设置的参数名对应。使用query方法，就没有这种限制，直接在跳转里面用就可以。
  

*注意*：如果路由上面不写参数，也是可以传过去的，但不会在url上面显示出你的参数，并且当你跳到别的页面或者刷新页面的时候参数会丢失（如下图所示），那依赖这个参数的http请求或者其他操作就会失败
  

注意看上面的路由参数，id这个参数是我们有设置在路由上面的，id2我没有设置在路由里面，所以刷新之后id2就不见了，在项目中，我们总不可能要求用户不能刷新吧。  
####组件1  
```
<template>
  <div class="app_page">
    <h1>从这个路由传参到别的路由</h1>
    <router-link :to="{ name:'router1',params: { id: status ,id2: status3},query: { queryId:  status2 }}" >
      router-link跳转router1
    </router-link>
  </div>
</template>
<script>
export default {
  name: 'app_page',
  data () {
    return {
      status:110,
      status2:120,
      status3:119
    }
  },
}
</script>
```
####编程式导航跳转：  
上面的router-link传参，也可以使用router文档里面的编程式导航来跳转传参。
  
```
    this.$router.push({  name:'router1',params: { id: status ,id2: status3},query: { queryId:  status2 }});
    //编程跳转写在一个函数里面，通过click等方法来触发
```
  
这两种传参效果是一模一样的，编程式导航，可以用来做判断跳转，比如是否授权，是否登录，等等状态，对此不太了解的小伙伴们，可以跳过这个编程式导航，以后再来看。

####组件二
  
```
<template>
  <div class="router1">
    <h1>接收参数的路由</h1>
    <h1> params.id：{{ $route.params }}</h1>
    <h1>query.status:{{ $route.query.queryId }}</h1>
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
  </div>
</template>
```
传参还是比较简单的，按着上面组件的使用方法就可以成功传过去了。

*提示*：获取路由上面的参数，用的是$route，后面没有r。
  

###params传参和query传参有什么区别：
  
  
1、params是路由的一部分,必须要有。query是拼接在url后面的参数，没有也没关系。

params一旦设置在路由，params就是路由的一部分，如果这个路由有params传参，但是在跳转的时候没有传这个参数，会导致跳转失败或者页面会没有内容。

比如：跳转/router1/:id  
```
<router-link :to="{ name:'router1',params: { id: status}}" >正确</router-link>
<router-link :to="{ name:'router1',params: { id2: status}}">错误</router-link>
```
  
2、params、query不设置也可以传参，但是params不设置的时候，刷新页面或者返回参数会丢失，query并不会出现这种情况，这一点的在上面说过了
