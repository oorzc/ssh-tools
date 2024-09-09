# SSH Tools Code Rapid Upload Tool

[中文文档](https://github.com/oorzc/ssh-tools/blob/main/README.zh-CN.md)

[DOWNLOAD](https://marketplace.visualstudio.com/items?itemName=oorzc.ssh-tools)

## ✨ Features

1. Supports custom configuration for multiple development environments.
2. Supports real-time code synchronization.
3. Supports recording and manually uploading changed code.
4. Supports automatic building and packaging of front-end projects.
5. Supports compressed code upload.
6. Supports checking if the code is up-to-date with git before uploading, suitable for teams.
7. Supports custom upload directories and exclusion of certain directories.
8. Supports downloading remote files.
9. Support for proxy settings

## 📖 Usage Instructions

1. Plugin Configuration
   * By default, ignores files and folders like `.git`, `.svn`, `.DS_Store`, `Thumbs.db`, `.idea`, `node_modules`, `ssh_tools.jsonc`, and `runtime`. Add others as needed.
   * If a `.gitignore` configuration file exists, the plugin will use it to determine ignored upload content.
   ![](https://cdn.jsdelivr.net/gh/oorzc/public_img@main/img/2023%2F10%2F07%2F20231007154405.png)

2. Adding Project Configuration
    ![](https://cdn.jsdelivr.net/gh/oorzc/public_img@main/img/2023%2F10%2F20%2F20231020152143.gif)

3. Proxy settings, you need to set proxy = true in the following project configuration to enable it
   ![](https://cdn.jsdelivr.net/gh/oorzc/public_img@main/img/2024%2F09%2F01%2Fcd35fdaffd774dd03249f63a5ca5b20c.png)


Sample project configuration:

```jsonc
{
    // Environment name, customizable
    "test": { // Test environment
        "host": "0.0.0.0", // (Required) Server address
        "port": 22, // (Optional) Port number, default is 22
        "username": "username", // (Required) Login username  
        "password": "password", // Login password (or private key path, choose one)
        // "privateKeyPath": "/your_path/id_rsa", // Private key path (or login password, choose one). Note: it's best not to place the key in the root directory of the code.
        "proxy": false, // Whether to use proxy, default false
        "upload_on_save": false, // Real-time submission after saving, recommended for single-person development. If set to true, watch, submit_git_before_upload, compress, and deleteRemote are ineffective. Default is false.
        "watch": true, // Watch for file changes in the upload directory, default is true. If upload_on_save is true, this is ineffective. If distPath is configured, only changes in distPath are watched.
        "submit_git_before_upload": true, // For team development, commits local git before uploading to prevent overwriting remote code, default is false.
        "submit_git_msg": "", // Git commit message configuration, default is empty. If submit_git_before_upload is true and this is not filled, a prompt will appear to manually enter it.
        // "build": "yarn build:test", // (Optional) Build command to execute, typically for front-end projects.
        "compress": true, // Whether to compress and upload, then extract remotely (account needs SSH login support, system will auto-detect). Default is false.
        //"remote_unpacked": true, // Whether to decompress the compressed file remotely after uploading, default true
        //"delete_remote_compress": true, // Whether to delete the zip file after uploading, default true
        //"delete_local_compress": true, // Whether to delete the local compressed file after uploading the compressed file, the default is true
        "distPath": [], // (Optional) Local directories to upload, supports string or array. Default is the root directory.
        "upload_to_root": false, // If there is only one distPath configuration directory, it is uploaded to the remotePath root directory. It is generally used to deploy front-end code. The default value is false
        "deleteRemote": false, // Whether to delete the remote distPath directory before uploading. Generally used for clearing front-end deployment code. Default is false.
        "remotePath": "/www/wwwtest/test", // (Required) Remote server address for uploading.
        "excludePath": [] // (Optional) Files and directories to exclude from upload in the current environment. Merged with the plugin's excludePath. If using .gitignore, merges with .gitignore configuration.
    },
    "online": { // Production environment
        "host": "0.0.0.0",  
        "port": 22, 
        "proxy": true, 
        "username": "username", 
        "password": "password",
        // "privateKeyPath": "/your_path/id_rsa", 
        "upload_on_save": false, 
        "watch": true, 
        "submit_git_before_upload": true, 
        "submit_git_msg": "", 
        // "build": "yarn build:online",  
        "compress": true, 
        // "remote_unpacked": true, 
        // "delete_remote_compress": true, 
        // "delete_local_compress": true, 
        "upload_to_root": false, 
        "deleteRemote": false, 
        "distPath": [], 
        "remotePath": "/www/wwwtest/online",  
        "excludePath": []
    }
}
```

## Upload Demonstrations

Real-time upload
![](https://cdn.jsdelivr.net/gh/oorzc/public_img@main/img/2023%2F10%2F07%2F20231007165139.gif)

Upload only changed data
![](https://cdn.jsdelivr.net/gh/oorzc/public_img@main/img/2023%2F10%2F07%2F20231007164843.gif)

