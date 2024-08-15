问题驱动

**首先如何从后端拿到token放到前端的session？**

A：axios

```js
  methods: {
      login(){
       
        if(!this.form.phone || !this.form.code){
          this.$message.error("手机号和验证码不能为空！");
          return
        }
        axios.post("/user/login", this.form)
        .then(({data}) => {
            if(data){
              // 保存用户信息到session
              sessionStorage.setItem("token", data);
            }
            // 跳转到首页
            location.href = "/index.html"
        })
        .catch(err => this.$message.error(err))
      }
```

**然后如何把这个数据放到请求头去呢**

A：放一个请求的拦截器，token不为空则把他取出来放到**指定字段的请求头**中

```js
let token = sessionStorage.getItem("token");
axios.interceptors.request.use(
  config => {
    if(token) config.heeadrs['authorization'] = token  //authorization是请求头里的一个字段
    return config
  }
```

我一开始有一个误区：我认为这里的token是和后端return的字段匹配，这里的token只是和前面session保存的字段匹配罢了。

**为什么我们return东西他能准确地抓到token呢？**

A：因为只用根据业务return一个token，而不是像别的VO啊这种





**token原理**

登入了之后这个请求头访问什么东西都是带着这个token直到我的redis里面的token失效，然后拦截，强制重新登入这时候再获得新的token保存在session里面

