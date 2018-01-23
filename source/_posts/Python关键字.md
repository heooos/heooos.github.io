---
title: Python关键字
date: 2018-01-23 22:56:38
tags: Python
categories: [基础,关键字]
---

Python2.7环境中，关键字共有31个。

可以通过

```shell
>>> import keyword
>>> print keyword.kwlist
```

进行查看。

```
and
as
assert
break
class
continue
def
del
elif
else
except
exec
finally
for
from
global
if
import
in
is
lambda
not
or
pass
print
raise
return
try
while
with
yield
```

**需要注意，在变量命名的时候 防止使用到关键字！**