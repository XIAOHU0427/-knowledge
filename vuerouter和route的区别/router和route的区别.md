*vue中的router和route的区别是什么*
  
区别：router是Vue.use（"VueRouter"）和VueRouter构造函数得到的一个实例对象。它是一个全局对象，
而route它是一个跳转的路由对象，每一个路由都有一个route对象，是一个局部对象。
  
*router是什么*
  
router是VueRouter的一个对象，通过Vue.use(VueRouter)和VueRouter构造函数得到一个router的实例对象，这个对象中是一个全局的对象，他包含了所有的路由包含了许多关键的对象和属性。
类似于history对象
*$router.push（{path：‘home’}）; 本质是向history栈中添加一个路由，在我们看来是切换路由，但本质是添加一个history记录  
*route是什么*
  
route是一个跳转的路由对象，每一个路由都会有一个route对象，是一个局部的对象，可以获取对应的name,path,params,query等。