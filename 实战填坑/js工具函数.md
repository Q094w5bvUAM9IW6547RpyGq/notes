## 格式化数据（每三位加分号）

强推：`Number.prototype.toLocaleString()`

[介绍](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString)

```js
//方式一
formatter (number) {
  const numbers = number.toString().split('').reverse()
  const segs = []
  while (numbers.length) segs.push(numbers.splice(0,      3).join(''))  
  return segs.join(',').split('').reverse().join('')
}
```

![image-20220104142725379](D:\FfWork\notes\实战填坑\js工具函数.assets\image-20220104142725379.png)

```
//方式二
function({value}) {
  return (value || 0).toString().replace(/(\d)(?=(?:\d{3})+$)/g, '$1,') + '元';
}
```

```
//方式三
function toThousands(num) {
     var num = (num || 0).toString(), result = '';
     while (num.length > 3) {
         result = ',' + num.slice(-3) + result;
         num = num.slice(0, num.length - 3);
     }
     if (num) { result = num + result; }
     return result + '元';
 }
```

```
//不同单位实现
function tranNumber(num, point){
   // 将数字转换为字符串,然后通过split方法用.分隔,取到第0个
   let numStr = num.toString().split('.')[0]
   if(numStr.length<6) { // 判断数字有多长,如果小于6,,表示10万以内的数字,让其直接显示
       console.log(numStr);
       return numStr;
     }else if(numStr.length>=6 && numStr.length<=8){ // 如果数字大于6位,小于8位,让其数字后面加单位万
        let decimal = numStr.substring(numStr.length-4, numStr.length-4+point)
        console.log(decimal);
        // 由千位,百位组成的一个数字
        return parseFloat(parseInt(num / 10000)+'.'+decimal)+'万'  
   }else if(numStr.length >8){ // 如果数字大于8位,让其数字后面加单位亿
        let decimal = numStr.substring(numStr.length-8, numStr.length-8+point);
        console.log(decimal);
        return parseFloat(parseInt(num/100000000)+'.'+decimal)+'亿'
   }
}
```

> 注：point 可指定数据的精度，建议14

## 进度条[Nprogress](https://ricostacruz.com/nprogress/)

```
import NProgress from 'nprogress' // Progress 进度条
import 'nprogress/nprogress.css' // Progress 进度条样式
 
 NProgress.start() //开启进度条
 NProgress.done() //结束进度条
```

## [js-cookie](https://www.npmjs.com/package/js-cookie)

> cookie是一个存储在客户端的字符串属性,可以用它对当前网页的cookie进行读,写,增.删等操作;javascript能够用document对象的cookie属性对cookie进行操作;

1、安装，引入

```
npm install js-cookie --save
import Cookies from 'js-cookie'
```

2、存入

```
// Create a cookie, valid across the entire site:  
Cookies.set('name', 'value');  
   
// Create a cookie that expires 7 days from now, valid across the entire site:  
Cookies.set('name', 'value', { expires: 7 });  
   
// Create an expiring cookie, valid to the path of the current page:  
Cookies.set('name', 'value', { expires: 7, path: '' });  
```

3、取出

```
// Read cookie:  
Cookies.get('name'); // => 'value'  
Cookies.get('nothing'); // => undefined  
   
// Read all visible cookies:  
Cookies.get(); // => { name: 'value' }  
```

4、删除

```
// Delete cookie:  
Cookies.remove('name');  
   
// Delete a cookie valid to the path of the current page:  
Cookies.set('name', 'value', { path: '' });  
Cookies.remove('name'); // fail!  
Cookies.remove('name', { path: '' }); // removed!  
Cookies.remove('name', { path: '', domain: '' }); // removed! 
```

5、命名空间

如果担心不小心修改掉Cookies中的数据，可以用noConflict方法定义一个新的cookie。

```
var Cookies2 = Cookies.noConflict();
Cookies2.set('name', 'value');
```

6、set方法的参数解释

1. 第一个：name,必选参数，这个是cookie的变量名 

2. 第二：value,可选参数，这个cookie变量的值

3. 第三个：expire,可选参数，这个是用来设置cookie变量保存的时间 

4. 第四个：path,cookie的有效范围，这个参数是下一个参数domain基础上的有效范围，如果path设置为”/”，那就是在整个 domain都有效，比如setcookie(“user”,”php”,time()+3600,”/”),这样我们domain下的任何目录，任何文件都可以通过$_COOKIE['user']来调用这个cookie变量的值。如果path设置为”/test”,那么只在domain下的/test 目录及子目录才有效，比如domain下有两个目录: test1,test2,我们设置为setcookie(“user”,”php,time()+3600,”/test1″)，那么只有test1目录下才能通过$_COOKIE['user']调用user这个cookie变量的值，test2目录下获取不到。 

5. 第五个：domain,cookie有效的域名，如果domain,设置为googlephp.cn，那么在googlephp.cn下的所有子域都有效。假设googlephp.cn有两个子域，php.googlephp.cn，css.googlephp.cn，我们设置为 setcookie(“user”,”php”,time()+3600,”/”,”php.googlephp.cn”),那么只有在 php.googlephp.cn这个子域下才能获取user这个cookie变量的值. 再举一个例子：setcookie(“user”,”php”,time()+3600,”/test”,”php.googlephp.cn”),那么只有在php.googlephp.cn这个子域下的test目录下才能获取user这个cookie变量的值. 

   例如设成".hanj.com"则在.hanj.com下的所有服务器下的文件都可以调用cookie，在hanj的所有子域名下都可以访问，实现跨站点通信

   ```
   Cookies.set("token", v, { domain: '.guohua.com' });
   ```

   注意：通过domain设置的cookie清除的时候也必须使用domain清除

   ```
   Cookies.remove("token", { domain: '.guohua.com' });
   ```

6. secure
   true或false，表示cookie传输是否仅支持https。默认为不要求协议必须为https。:默认情况下为false;用http协议不安全传输;true:用https等协议安全传输.

## [psl(公共后缀列表)](https://www.npmjs.com/package/psl)

> psl是一个javascript基于公共后缀列表的域名解析器

1、安装

```
npm install --save psl
```

2、使用

```
psl.parse(domin)
基于公共后缀列表解析域。返回Object具有以下属性的 ：
tld: 顶级域（这是公共后缀）。
sld: 二级域名（域名的第一个私有部分）。
domain: 域名是sld+ tld。
subdomain: 域左侧的可选部分

const p_psl = psl.parse(document.domain) //document.domin =localhost
后台打印结果:
```

![image-20220106152457823](D:\FfWork\notes\实战填坑\js工具函数.assets\image-20220106152457823.png)

```js
psl.get(domain)
获取域名，sld+ tld。null如果无效则返回
```

```js
psl.isValid(domain)
检查域是否具有有效的公共后缀。返回Boolean指示域是否具有有效公共后缀的 。
```

## storage.js(js-cookie+psl) cookie存储

```js
import Cookies from 'js-cookie'
const psl = require('psl')

export default {
  setItem: (key, value, options = {}) => {
    const p_psl = psl.parse(document.domain)
    let domain = p_psl.domain
    if (/\d+\.\d+\.\d+\.\d+/.test(p_psl.input)) domain = p_psl.input
    options = { domain, ...options }
    Cookies.set(key, value, options)
  },
  getItem: (key) => {
    return Cookies.get(key)
  },
  removeItem: (key, options = {}) => {
    const p_psl = psl.parse(document.domain)
    let domain = p_psl.domain
    if (/\d+\.\d+\.\d+\.\d+/.test(p_psl.input)) domain = p_psl.input
    options = { domain, ...options }
    Cookies.remove(key, options)
  }
}
```

## 路由导航封装函数

> 在整个基于vue+elementUI的项目中，需要在进入页面之前或之后做一些判断或者处理，需要用到路由导航守卫
>
> 命名为permission.js

主要操作：

1、进度条开启和结束

2、验证用户登录信息



> 1、从缓存中获取token值
>
> 2、用户登录的时候检查token值有无
>
> - 有的话登录成功
> - 没有的话，使用状态管理器 获取到

```js
import router from './router' //引入路由
import store from './store' //状态管理器
import NProgress from 'nprogress' // Progress 进度条
import 'nprogress/nprogress.css' // Progress 进度条样式
import Storage from '@/utils/storage' //js-cookie封装好的cookie

const whiteList = ['login', 'forget', 'invite', 'home', 'wap'] 

router.beforeEach((to, from, next) => {
  // 解决keep-alive不能缓存三级菜单
  if (to.matched && to.matched.length > 2) {
    to.matched.splice(1,1)
  }
  NProgress.start() //开启进度条
  const accessToken = Storage.getItem('materials_access_token') //获取用户token
  if (accessToken) {
    if (to.path === '/login') {
      next({ path: '/home' })
      NProgress.done() //进度条加满
    } else {
      // 如果没有获取到常量,则请求获取常量
      if (!store.getters.constant || JSON.stringify(store.getters.constant) === '{}') {
        store.dispatch('setConstant')
      }
      if (store.getters.addRouters.length === 0) {
        store.dispatch('GenerateRoutes').then(() => {
          router.addRoutes(store.getters.addRouters)
          store.dispatch('GenerateModule', to)
          next({ ...to, replace: true })
        }).catch(() => {
          store.dispatch('fedLogoutAction').then(() => {
            Message.error('验证失败,请重新登录')
            window.location.replace(`/login?forward=${location.pathname}&${location.search.substr(1)}`)
          })
        })
      } else {
        store.dispatch('GenerateModule', to)
        next()
      }
    }
  } else {
    if (whiteList.indexOf(to.name) !== -1) {
      next()
    } else {
      next(`/login?forward=${location.pathname}&${location.search.substr(1)}`)
      NProgress.done()
    }
  }
})

router.afterEach(() => {
  NProgress.done()
})

```

## elementUI 输入框 enter键聚焦



## sortable.js拖拽插件

> 使用在elementUI的el-table组件中

## 树组件和抽屉组件组合成拖拽组件

## 判断路由权限

## 获取验证码倒计时

```
/* 获取验证码倒计时 */
    countDownTime(seconds) {
      const that = this;
      seconds -= 1;
      if (seconds < 0 || !that.vertifyForm.sending_code) {
        that.$set(that.vertifyForm, 'sending_code', false)
        that.$set(that.vertifyForm, 'code_msg', '获取验证码')
        return false;
      }
      that.$set(that.vertifyForm, 'code_msg', `发送成功(${seconds})`)
      setTimeout(() => {
        that.countDownTime(seconds);
      }, 1000);
    },
  }
// 调用
this.countDownTime(60)
```

```
 <!-- 手机验证弹窗 -->
    <Verify-phone-pop
    :verifyDialogVisible="verifyDialogVisible"
    @changeVerifyDialog="changeVerifyDialog"
    >
    </Verify-phone-pop>
    import VerifyPhonePop from '../../components/VerifyPhonePop/index.vue' // 手机验证弹窗
    components:{
    VerifyPhonePop
  },
  verifyDialogVisible:false, //手机验证弹窗开关
  
  /* 手机验证组件打开 */
    changeVerifyDialog(v) {
      this.verifyDialogVisible = v
    }
    
    else if(response.code === 201) {
                  this.verifyDialogVisible = true
                }
```



