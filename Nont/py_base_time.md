```Python
import  datetime
#以当前时间作为起始点，days=-7向前偏移7天，days=7向后偏移7天
time_now = datetime.datetime.now()
print('time.now: ', time_now)
time = (time_now + datetime.timedelta(days=7)).strftime("%Y%m%d")
print(time)

# 安装dateutil库，注意不是pip install dateutil,而是pip install python-dateutil

import  datetime
from dateutil.relativedelta import relativedelta

#以当前时间作为起始点，days=-7向前偏移7天，days=7向后偏移7天
time_now = datetime.datetime.now()
time = (time_now + datetime.timedelta(days=7)).strftime("%Y%m%d")

print('偏移7天: ', time)
#以当前时间为起始点，偏移一个月
time_1=(time_now+relativedelta(months=-1)).strftime("%Y%m%d")
print('偏移一个月: ', time_1)

```
输出结果:  
```
time.now:  2020-01-24 17:34:08.942675
20200131
偏移7天:  20200131
偏移一个月:  20191224
```

