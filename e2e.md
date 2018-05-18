# e2e 练习

### Quick Start
##### 目的：检查自己的环境，了解什么是e2e 的测试
##### 练习
1. 浏览器打开 https://github.com/dwyl/learn-nightwatch
2. 按照 README.md 中的 Quick Start 开始.

  **注意：提前需要安装java，详细阅读 Installation (in detail)** 
### todo-list 的e2e测试

+ run起todo-list的base
```
git clone https://github.com/IonicaBizau/react-todo-app/
cd react-todo-app
npm i
npm run start:dev
open localhost:8080
```
如果修改了todo-list 中的源代码，需要代码生效，执行下面的命令：
```
npm run bundle
```
+ 创建文件``` nightwatch.conf.BASIC.js``` ，文件的内容是：
https://github.com/dwyl/learn-nightwatch/blob/master/nightwatch.conf.BASIC.js中的内容

+  Run config  file ：
```
node nightwatch.conf.BASIC.js
``` 

+ 修改pakeage.json 中的Script：
```
 "scripts": { 
 "e2e": "nightwatch --config nightwatch.conf.BASIC.js"
 }
```
+ 创建文件夹 ``` /test/e2e```，创建测试文件 ``` todo.js```,文件的内容是：

```
var conf = require('../../nightwatch.conf.BASIC.js')

module.exports = {
  'Demo test todo-list': function (browser) {
    browser
      .url('http://localhost:8080')   // visit the url
      .waitForElementVisible('body') // wait for the body to be rendered
      .pause(1000)
      .setValue('#task', 'first  todo !')
      .click('#add')
      .setValue('#task', 'second  todo !')
      .click('#add')
      .assert.containsText('.total-items', '共有2个')

      .pause(1000)
      .click('tbody:first-child .edit-btn')
      .setValue('tbody:first-child form input', 'edit')
      .click('tbody:first-child .save-btn')
      .pause(2000)
      .assert.containsText('.total-items', '共有2个')
      .pause(1000)
      .click('tbody:first-child .delete-btn')
      .assert.containsText('.total-items', '共有1个')
      .end()
  }
}

```

+ 使用下面的命令运行测试
```
npm test
```




