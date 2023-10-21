# SSH Tools Code Rapid Upload Tool

[中文文档](https://github.com/oorzc/ssh-tools/blob/main/README.zh-CN.md)

[DOWNLOAD](https://marketplace.visualstudio.com/items?itemName=oorzc.ssh-tools)


## ✨ Plugin Features

1. Supports custom configuration of multiple development environments.
2. Supports real-time code synchronization.
3. Supports tracking code changes and manually uploading code.
4. Supports automatic building and packaging of front-end projects.
5. Supports code compression and upload.
6. Supports checking if the uploaded code is the latest in Git, suitable for team collaboration.
7. Supports custom upload directories and exclusion directories.

## 📖 User Guide

1. Plugin Configuration:
   * By default, it ignores the following files and folders: .git, .svn, .DS_Store, Thumbs.db, .idea, node_modules, runtime. You can add more exclusions as needed.
   * If a .gitignore configuration file exists, it will be used by default to exclude files from upload.
   ![Plugin Configuration](https://cdn.jsdelivr.net/gh/oorzc/public_img@main/img/2023%2F10%2F07%2F20231007154405.png)

2. Adding Project Configuration:
   ![Adding Project Configuration](https://cdn.jsdelivr.net/gh/oorzc/public_img@main/img/2023%2F10%2F20%2F20231020152319.gif)

Sample Project Configuration:

```jsonc
{
    // Environment name, supports custom names
    "test": { // Test environment
        "host": "0.0.0.0", // (Required) Server address
        "port": 22, // (Optional) Port number, default is 22
        "username": "username", // (Required) Login username
        "password": "password", // Login password (either password or privateKeyPath should be provided)
        // "privateKeyPath": "/your_path/id_rsa", // Private key path (either password or privateKeyPath should be provided). Note: It is recommended not to place the key in the code root directory.
        "upload_on_save": false, // Real-time submission after saving. Recommended for single-person development. When upload_on_save is set to true, watch, submit_git_before_upload, compress, deleteRemote are ignored. Default is false.
        "watch": true, // Listen for file changes in the upload directory. Default is true.
        "submit_git_before_upload": true, // For team development, submit local Git changes before uploading code to prevent overwriting remote code. Default is false.
        "submit_git_msg": "", // Git commit message configuration. Default is empty. If submit_git_before_upload is true and this field is not filled, a prompt will be displayed to manually enter the message.
        // "build": "yarn build:test", // (Optional) Build command to execute. Uncomment this line if it is a front-end project.
        "compress": true, // Compress the code before uploading and decompress it remotely (the account needs to support SSH login, the system will automatically check if it is supported, and if not, it will not compress the code). Default is false.
        "distPath": [], // (Optional) Local directories to upload, supports strings or arrays. Default is the root directory.
        "deleteRemote": false, // Whether to delete the remote distPath directory before uploading. Generally used to clean up front-end deployment code. Default is false.
        "remotePath": "/www/wwwtest/test", // (Required) Server upload path
        "excludePath": [] // (Optional) Files and directories to exclude for the current environment. This will be merged with the plugin's excludePath configuration. If the plugin is using a .gitignore file, it will be merged with the .gitignore configuration.
    },
    "online": { // Production environment
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

## Upload Demonstration

Real-time Upload:
![Real-time Upload](https://cdn.jsdelivr.net/gh/oorzc/public_img@main/img/2023%2F10%2F07%2F20231007165139.gif)

Upload Only Changed Data:
![Upload Only Changed Data](https://cdn.jsdelivr.net/gh/oorzc/public_img@main/img/2023%2F10%2F07%2F20231007164843.gif)

## Bug Reporting

[Github](https://github.com/oorzc/ssh-tools/issues)
