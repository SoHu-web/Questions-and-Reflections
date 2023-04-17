## 生产环境用户长时间停留在某个页面切换页面后出现无响应情况

### 页面错误显示

切换页面出现无响应情况，刷新页面后正常

### 浏览器报错信息

~~~js
Failed to load module script: Expected a JavaScript module script but the server responded with a MIME type of "text/html". Strict MIME type checking is enforced for module scripts per HTML spec.

TypeError: Failed to fetch dynamically imported module: https://xxxx.cn/yyui/assets/index-bad18e77.js
~~~



### 错误原因

发版后js文件hash值改变，访问不到原先的js文件

### 解决方法

给window添加error监听事件

~~~js
window.addEventListener('error',(event)=>{
 // event.target: <link rel="modulepreload" as="script" crossorigin="" href="/yyui/assets/index-6990dcb.js">
if((event.target as HTMLScriptElement).localName === 'script' || (event.target as HTMLScriptElement).localName === 'link') {
ElMessageBox.alert('监测到系统功能已经升级，点击“确定”自动刷新获取更新','提示',{
    confirmButtonText: '确定',
    showClose:false,
    callback: (action: any) => {
      //console.log(action);  
       // 刪除离线的缓存
      if('caches' in window) {
        caches.keys().then(function(cacheNames){
          const arr = cacheNames.map(function(cacheName){
            return caches.delete(cacheName)
          })
          return arr
        }).then(function(res){
          location.reload()
        })
      } else {
    location.reload()
      }
    }
})
}
event.preventDefault()
},true)
~~~

