> 使用前端路由是因为，vue创建是一个单页面网站
> 
> 即，用户直接获取了整个网站的所有交互
> 
> 访问资源无需加载

## 安装与使用

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110113338.png)

## 动态路由

```js
{ path:"/path/:id" , component:Product}
```

> 带了 `:` 就说明是动态路由

## 编程式导航

| 声明式                      | 编程式                |
| :----------------------- | ------------------ |
| `<router-link :to="..."` | `router.push(...)` |

## 路由守卫

导航路由守卫可以控制路由的访问权限，示意图如下：

全局导航守卫会拦截每个路由规则，从而对每个路由进行访问权限控制，

你可以使用 `router.beforeEach` 注册一个全新的全局前置守卫：

```js
router.beforeEach((to, from, next) => {
	if (to.path === '/main' && !isAuthenticated){
		next('/login')
	}
	else{
		next()
	}
})
```

- `to` : 即将要进入的目标
- `from` : 当前导航正要离开的路由
- 在守卫方法中如果声明了 `next` 形参，则必须调用 `next()` 函数，否则不允许用户访问任何一个路由！
	- 直接放行: `next()`
	- 强制其停留在当前页面：`next(false)`
	- 强制其转到登录页面：`next('/login')`

