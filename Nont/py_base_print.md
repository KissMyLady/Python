Print妙用  
====

```Python
for i in range(100):
	time.sleep(0.5)
	print('\r','precentage is{}%'.format(i), end="", flush=True)
```


```Python
for i in tqdm(range(100)):
	print('\r',i, end='', flush=True)
	time.sleep(0.5)
```
![ScreenShot-00280](https://github.com/KissMyLady/Python/blob/master/Img/Python/ScreenShot-00280.jpg)  


```
from progressbar import *
pr = ProgressBar()
for i in pr(range(100)):
	print(i)
	time.sleep(0.5)
```
![ScreenShot-00281](https://github.com/KissMyLady/Python/blob/master/Img/Python/ScreenShot-00281.jpg)  
