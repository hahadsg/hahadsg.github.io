### 快捷键

跳转到定义 `alt+command+down`

跳转到上一次位置`ctrl+-`

光标出现在每一行`command+shift+L`

### 在服务器上编辑文本

https://stackoverflow.com/questions/37458814/how-to-open-remote-files-in-sublime-text-3

### My Preferences.sublime-settings(User)

```
{
    // translate tabs to spaces
    "translate_tabs_to_spaces": true,
    "font_size": 12,
    "ignored_packages":
    [
        "Vintage"
    ],
    "vintage_ctrl_keys": true
}
```

# 问题

### package control不能安装

https://blog.csdn.net/zr15829039341/article/details/73136319

https://github.com/HBLong/channel_v3_daily

# Scala
-----

## Enisme

http://ensime.github.io/build_tools/sbt/

### 常用快捷键

  ```
  Command + Space 补全
  Command + Click 跳转定义
  Shift + Click 类型显示
 
  Ctrl + Click 菜单
  Alt + Command + E 错误原因显示
  ```

### 常见错误

* 出现[error] (*:coursierProject)

  plugins.sbt在ensime之前加上这个

  ```
  addSbtPlugin("com.dwijnand" % "sbt-compat" % "1.2.6")
  ```
 
* 创建了scala_2.11而不是使用scala文件夹
    https://stackoverflow.com/questions/41070767/ensimeconfig-creates-directories-java-and-scala-2-11-which-i-dont-need
    
* You have a different version of scala for ENSIME (2.10.7) and root (2.11.12)

  在build.sbt加上
  
  ```
  ensimeScalaVersion in ThisBuild := "2.11.12"
  ```