## 使用ssh -i

```bash
rsync -rav -e 'ssh -i ~/.ssh/xxx.pem' \
--exclude='.git/*' \
from_xxx to_xxx
```