```vi
:w xx.log # 保存为xx.log
:w !{command} # 在vi中执行command 注意w !中间有空格
:w !sudo tee % # sudo保存当前文件
```

* replace

http://vim.wikia.com/wiki/Search_and_replace