 
 * @Descripttion: common vs setting 
 * @version: 1.0
 * @Author: hangjie.zhu
 * @LastEditors: hangjie.zhu
 * @Date: 2019-04-04 15:46:23
 * @LastEditTime: 2019-04-04 16:02:48 

> tip:ctrl+p(quick open)

> plugin for vscode

1.  `Document This`  
    desc: quick doc for function.  
    setting: null  
    how to use: `Ctrl+Alt+D` and again `Ctrl+Alt+D`  

2. `KoroFileHeader`   
   desc: quick doc for file and finction.   
   setting: ctrl+p input 'setting', add content as follow:            
```js
  //文件头部注释
  "fileheader.customMade": {
      "Descripttion":"",
      "version":"",
      "Author":"your name like hangjie.zhu",
      "Date":"Do not edit",
      "LastEditors":"your name like hangjie.zhu",
      "LastEditTime":"Do not Edit"
  },
  //函数注释
  "fileheader.cursorMode": {
      "name":"", 
      "msg":"",
      "param":"",
      "return":""
  }
```
* how to use:   
    + file header doc:     `crtl+alt+i` (window), `ctrl+cmd+t` (mac)  
    + function header doc: `ctrl+alt+t` (window), `ctrl+alt+t` (mac)  

3. `Vue 2 Snippets`   
    desc: code helper for Vue2.  
    setting: null  
    how to use: null


