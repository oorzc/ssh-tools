# ssh tools 代码快速上传工具

## ✨ 插件功能

1. 支持实时同步代码
2. 支持非实时同步时，记录变动代码，再手动上传代码
3. 支持自动构建打包前端项目
4. 支持代码压缩上传
5. 支持上传代码检测git是否最新，适用于团队
6. 支持自定义上传目录和排除不上传目录

## 📖 使用介绍

1. 在工作区根路径下添加 ssh_tools.jsonc 文件
2. 支持自定义配置多个开发环境
3. 插件配置
   * 默认忽略.git、.svn、.DS_Store、Thumbs.db、.idea、node_modules、runtime文件及文件夹，其他请自行添加
   * 如果存在.gitignore配置文件，默认使用该配置，忽略上传内容
   ![](https://cdn.jsdelivr.net/gh/oorzc/public_img@main/img/2023%2F10%2F07%2F20231007154405.png)
4. 项目配置如下

```jsonc
{
    //环境名称，支持自定义名称
    "test": { //测试环境
        "host": "0.0.0.0", // (必填)服务器地址 
        "port": 22, // (非必填) 端口号 ，默认22
        "username": "username", // (必填)登录用户名  
        "password": "password", // 登录密码 (和私钥路径，二选一)
        // "privateKeyPath": "/your_path/id_rsa", // 私钥路径 (和登录密码，二选一)，注意：最好不要将密匙放代码根目录
        "upload_on_save": false, // 保存后实时提交，建议单人开发使用，upload_on_save设置为true时，watch、submit_git_before_upload、compress、deleteRemote无效，默认false
        "watch": true, // 监听上传目录文件变动，默认true
        "submit_git_before_upload": true, // 团队开发使用，上传代码前提交本地git，防止覆盖远程代码，默认false
        "submit_git_msg": "", // 提交git的message配置，默认空。submit_git_before_upload为true时，不填写会弹出提示框手动填写
        // "build": "yarn build:test", // (非必填) 构建执行的命令 如果是前端项目则打开此项
        "compress": true, //  是否压缩上传，并远程解压（账号需要支持ssh登录，系统会自动检测是否支持，不支持，则不会压缩上传），默认false
        "distPath": [], // (非必填) 本地需要上传的目录，支持字符串或数组，默认上传根目录
        "deleteRemote": false, // 上传前是否删除远程distPath配置目录，一般用于清理前端部署代码， 默认false
        "remotePath": "/www/wwwtest/test", // (必填)上传服务器地址  
        "excludePath": [] // (非必填) 当前环境排除的上传文件及目录，会和插件配置excludePath合并，插件配置使用gitignore的时候，会和.gitignore配置文件合并
    },
    "online": { //正式环境
        "host": "0.0.0.0",  
        "port": 22, 
        "username": "username", 
        "password": "password",
        // "privateKeyPath": "/your_path/id_rsa", 
        "upload_on_save": false, 
        "watch": true, 
        "submit_git_before_upload": true, 
        "submit_git_msg": "", 
        // "build": "yarn build:online",  
        "compress": true, 
        "deleteRemote": false, 
        "distPath": [], 
        "remotePath": "/www/wwwtest/online",  
        "excludePath": []
    }
}
```

## 上传演示
实时上传
![](https://cdn.jsdelivr.net/gh/oorzc/public_img@main/img/2023%2F10%2F07%2F20231007165139.gif)

只上传变动数据
![](https://cdn.jsdelivr.net/gh/oorzc/public_img@main/img/2023%2F10%2F07%2F20231007164843.gif)


## BUG反馈

请附上相关代码片段

[Github](https://github.com/oorzc/ssh-tools/issues)
