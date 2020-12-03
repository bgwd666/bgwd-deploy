# bgwd-deploy
一个简单方便的前端自动部署工具 

说到部署很多人想到 Jenkins docker 等, 但学习使用成本 可能让很多人望而却步.

倒不如试试我这个? 三步曲:

[项目github 地址](https://github.com/bgwd666/bgwd-deploy)

[npm 地址](https://www.npmjs.com/package/bgwd-deploy)

[项目代码讲解](https://segmentfault.com/a/1190000020994461)


### 第一步 
`npm i bgwd-deploy -D`

### 第二步 
**在你项目 package.json 文件 scripts 脚本下加上下面一行(比较粗暴,有更好的方法望不吝赐教)** 

`"deploy": "node ./node_modules/bgwd-deploy/index"`

![image.png](https://pr-pictures.oss-cn-shenzhen.aliyuncs.com/static/bgwd-deploy.png?OSSAccessKeyId=LTAI8DmoaMe6blcx&Expires=360001591249166&Signature=MpnbcAxb0DpYlZROthw49AltbaQ%3D)

### 第三步 
**在你项目根目录添加 deploy.config.js 文件 内容如下:**
**然后就可以 npm run deploy 部署了.**

```
// 关于团队合作 成员 PRIVATE_KEY 不一致问题, 可以每个成员单独配置自己的 PRIVATE_KEY 然后在 .gitignore 添加 deploy.config.js 忽略上传
// 配置参考文件  实际配置文件需要用户在自己项目根目录 添加 deploy.config.js
module.exports = Object.freeze({
  development: {//测试
    SERVER_PATH: 'xx.xxx.xx.xx', // ssh地址 服务器地址
    SSH_USER: 'root', // ssh 用户名
  //登录方式 (二选一, 不用的方式注释掉)
  //方式一 用秘钥登录服务器(推荐), 
    // 把本机 公钥 .ssh目录下 id_rsa.pub 放服务器 authorized_keys 文件里, 多个电脑公钥换行分开
    //private 本机私钥文件地址(需要在服务器用户目录 一般是 ~/.ssh/authorized_keys 配置公钥 并该文件权限为 600, (.ssh文件夹一般默认隐藏)
    // 一般 .ssh在用户目录下  cd ~/.ssh/  复制路径放下面 pwd 可查看当前路径 路径用 / 别 \ 例如以下 C:/Users/Administrator/.ssh/id_rsa
    PRIVATE_KEY: 'C:/Users/Administrator/.ssh/id_rsa', 
  //方式二 用密码连接服务器
    // PASSWORD: '',
    PATH: '/test/h5', // 需要上传的服务器目录地址 如 /usr/local/nginx/html/prodName
    //(该参数可选) 默认为 arrow4 加载动画 有 dots 至 dots12 如 dots6,  line ,
    // pipe , star, arrow 至 arrow4 等等, 查看更多在该项目 src下的 spinner_style.js
    LOADINGSTYLE: 'arrow4',
    // SHELL: '' // 自定义打包命令(不用请注释), 默认 npm run build , 可自定义 如 npm run build:prd 等
  },
  production: {//正式
    SERVER_PATH: '', 
    SSH_USER: 'root',
    PRIVATE_KEY: '', 
    PATH: '/test/html' ,
    // LOADINGSTYLE: 'arrow4',
    // SHELL: '' 
  }
})
```

