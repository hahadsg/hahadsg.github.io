## env

```bash
// list envs
conda info --envs
conda env list

// activate env
activate myenv
```

## uninstall anaconda

```bash
conda install anaconda-clean
anaconda-clean --yes
rm -rf ~/anaconda3
rm -rf ~/.anaconda_backup  
```

## 使用清华的源

```bash
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes
```