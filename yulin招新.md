## ***\             *梦开始的地方（basic）\****

#### ***\*第一题：编码\****

***\*考察各种编码的特征，从第一个开始，在网上找工具解码\****

***\*①014380f217e124ad3213bcbf3cb794f4为md5编码\****

***\*②%53%65%63%7b%77%65%5f%6d%75%35%74%5f%6b%6e%30%77为url\****

***\*③X2MwbW0wbg==为base64编码\****

***\*④_enc0d1ngs}为unicode编码\****

***\*解完即得到flag\****

 

#### ***\*第二题：calc-1\****

***\*6\*11=66  直接输入，发现第二个6打不上去，于是F12，打开查看器，发现\****

![img](file:///C:\Users\17078\AppData\Local\Temp\ksohtml21024\wps1.jpg) 

***\*Maxlength=1，直接在上面修改为2，输入66即得到flag\****

***\*YulinSec{The_front_1s_n0t_saf3}  前端的限制并不安全\****

 

#### ***\*第三题：calc-2\****

***\*F12查看器，发现以JavaScript编写了一段语句，大意是\****

![img](file:///C:\Users\17078\AppData\Local\Temp\ksohtml21024\wps2.jpg) 

***\*判断上传内容，然后禁止上传并弹出弹出弹窗\****

***\*直接修改难度不小(我还没学会)，既然说了method=POST，直接POST一个result=666即可\****

***\*（用hackbar就行）\****

***\*得到flag：YulinSec{JavaScr1pt_1s_not_saf3}   javascript并不安全\****

 

#### ***\*第四题：calc-3\****

***\*学完网页的一些基础知识后，开始学习“伴随整个安全生涯的工具 python”\****

***\*要求更快的计算，尝试用python脚本完成\****

***\*这是我写的脚本（其实是B站上搬运的）\****

[***\*calc-3.py\****](../附件/calc-3.py)

***\*引用这几个模块就可以达到提取文字，自动计算并提交的功能\****

***\*import requests\*******\*
\*******\*from bs4 import BeautifulSoup\*******\*
\*******\*import re\*******\*
\*******\*import time\****

***\*Bs4模块好像要先去解释器中下载才能用\****

![img](file:///C:\Users\17078\AppData\Local\Temp\ksohtml21024\wps3.jpg) 

***\*得到flag：YulinSec{py_py_G00d_gOOd}\****

 

#### ***\*第五题：HTTP\****

***\*初学，先用burp suite熟悉一下HTTP报文的格式，不建议使用hackbar（主要是用起来太无脑了，学不到什么东西）\****

***\*1：网站后缀添加/?key1=YulinSec即以get方式发送key1=YulinSec\****

***\*2：使用POST提交方法和GET类似，将GET改为POST，在末尾添加，此时记得添加Content-Type: application/x-www-form-urlencoded\****

***\*3：更改Referer值为YulinSec://127.0.0.1\****

***\*4:你必须是管理员，注意右一栏，set-cookie里面的元素:admin，因此我们添加cookie，令admin=1发送请求就得到了flag\****

***\*YulinSec{kNoW_h77p_wEll!}\****

 

#### ***\*第六题：302\****

***\*抓包，发到重发器里，发现响应包里有个叫302.php的东西\****

***\*GET后面加上它，重新发送得到flag\****

![img](file:///C:\Users\17078\AppData\Local\Temp\ksohtml21024\wps4.jpg) 

***\*YulinSec{302_can_be_1ntercepted\*******\*}\****

 

#### ***\*第七题：method\****

***\*抓包，使用OPTIONS方法进行连接得到flag\****

***\*Flag: YulinSec{Meth0ds_include_PUT_Delet4_hEAd_TRA\*******\*CE\*******\*}\****

 

#### ***\*第八题：HTTPS\****

***\*必须是管理员\****

***\*同样抓包，放到重发器里，发现发来了一个cookie\****

 

![img](file:///C:\Users\17078\AppData\Local\Temp\ksohtml21024\wps5.jpg) 

***\*=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZG1pbiI6IjAiLCJpYXQiOjE3MjkwNTcwNTQsImV4cCI6MTcyOTA2NDI1NCwianRpIjoiZmE0ZWU0YzhkOTNmOWExNGViMzlmYzM5MTdjN2IxYmYifQ.W8n0gO28vrf2gvPGwZCW7swcKNH09kJN6Bi8H4dIxfI\****

***\*尝试base64解码\****

***\*发现只有前半部分可以解码，后面都是乱码\****

***\*就是直接删掉后面的，再把admin=0改成admin=1也不行\****

***\*学一学什么是JWT，终于知道怎么做\****

[***\*https://blog.csdn.net/solitudi/article/details/112525267\****](https://blog.csdn.net/solitudi/article/details/112525267)

***\*jwt伪造，爆破密钥，admin的值改为1\****

![img](file:///C:\Users\17078\AppData\Local\Temp\ksohtml21024\wps6.jpg) 

***\*拿下flag:YulinSec{Js0n_w3b_t0ken_de_secret_Yao_SheZhi_complicated_yidian}\****

 

 

***\*至此，basic被AK\****