## jupyter

https://docs.aws.amazon.com/zh_cn/dlami/latest/devguide/setup-jupyter-config.html?shortFooter=true

* 错误1

ValueError: '' does not appear to be an IPv4 or IPv6 address

https://github.com/jupyter/notebook/issues/3946#issuecomment-423169943

`c.NotebookApp.ip = '*'`改成`c.NotebookApp.ip = '0.0.0.0'`