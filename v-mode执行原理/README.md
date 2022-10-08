*v-model原理 = v-bind（：value） + v-on(@input)*  
*v-model实现数据双向绑定如下*  
  
```<template>
  <div id="app">
    <input type="text" v-model="str">
  </div>
</template>
 
<script>
export default {
data(){
  return{
    str:''
  }
}
}
</script>
```
<br>
<br>
*其原理如下*  
 
 ``` 
<template>  
  <div id="app">  
    <!-- 给input输入框绑定@input事件，随时监听value的值 -->  
    <input type="text" :value="str" @input="onInputFn">  
  </div>
</template>
 
<script>
export default {
data(){
  return{
    str:''
  }
},
methods:{
  onInputFn(e){
    // 把监听到的value值传给str
    this.str = e.target.value
  }
}
}
</script>
```