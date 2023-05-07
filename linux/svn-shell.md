* rm所有!文件

 ```bash
 svn status | grep '!' | awk '{print "'\''"substr($0, 9)"'\''"}' | xargs svn rm
 ```
 
 ```bash
 svn status | awk '$1=="?" {printf "'\''%s'\''\n", $2}' |  xargs rm
 ```
 
* add所有?文件
```bash
svn status | grep '?' | awk '{print "'\''"substr($0, 9)"'\''"}' | xargs svn add
```

* rm changelist中所有文件

 ```
 svn changelist --remove --recursive --cl [cl_name] [path]
 ```


