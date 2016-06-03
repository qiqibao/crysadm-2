#迅雷云监工源代码
#我只是搬运工，从seatom来的，添加支持docker的Dockerfile文件
***

##用法
进入系统后先升级源，输入命令<br>
`sudo apt-get update` <br>
等一会自动下载，输入命令 <br>
`sudo apt-get install -y git` <br>
如果出现`bash: sudo: command not found`错误，说明没有安装这个程序，直接输入命令<br>
`apt-get install -y sudo git`<br>
用 `cd` 命令进入任意可写权限文件夹，输入命令<br>
`sudo git clone https://github.com/seatom/crysadm.git`<br>
等待下载完成，输入命令<br>
`cd crysadm  && sudo chmod +x setup.sh && ./setup.sh`<br>
此时等待安装，完成后会自动启动云监工。<br>
***
##PS:<br>
***
run.sh是运行脚本，down.sh是停止脚本，setup.sh是安装环境脚本。
***
***


***   
- 默认端口：4000
- 第一次获得密码方法：浏览器打开【IP:4000/install】
-更新到最新版方法：cd crysadm进入程序根目录; sudo git reset --hard HEAD ; sudo git pull即可

###====================2016-5-27===================
login.py						修改登录接口解决登陆问题
templates/login.html			首页添加了站长统计和显示矿机统计
templates/base.html				登陆后页面底部能够显示矿机统计

###====================2016-5-10===================
crysadm_helper.py				收益报告和矿机异常报告现在将能自动重发(仅当邮件发送失败)。修复了数据统计中7日矿机收益统计不准确的问题、30日产量的统计不准确的问题（即日起生效，过往记录不补），修复了宝箱收益和矿场收益之和不等于今日总收益的BUG（账户越多效应越显著）。修复了矿机异常报告的换行问题，改用监工的账户信息页面的邮件地址作为收件地址
user.py							整合了明日的注册邮箱既用户名的逻辑
admin.py						移除了提醒邮件地址设置的后台支持
templates/dashboard.html		调整了收益柱子下的时间段提示文字，调整了面板的提示文字
templates/profile.html			移除了设置提醒邮件地址按钮，该功能改由 云监工设置->账户 下的邮件地址设置提供
templates/register.html			整合了明日的注册邮箱既用户名的逻辑

###====================2016-5-9===================
crysadm_helper.py				修复了矿机状态反复记录日志及不发邮件的问题，现在能一次发送多个同时异常的矿机状态了，添加了收益报告中的时间戳
web_common.py					修复了面板不显示速度收益的问题
user.py							添加了删除筛选后的日志的功能，优化了日志筛选功能的用户体验（不要求点击顺序，时间改为自然日区间，原为回滚X个24小时）。
admin.py						整合了明日的删除垃圾用户的逻辑
templates/base.html				修改以配合新的日志参数
templates/log.html				添加删除筛选结果按钮
templates/dashboard.html		使用默认统计时，不再显示打开速度曲线的按钮
templates/admin_user.html		整合了明日的删除垃圾用户的几个按钮

###====================2016-5-8===================
crysadm_helper.py				调整了矿机状态监测逻辑，修复了自动报告功能不发邮件的BUG(对于0点之后被自动重启的监工)。宝箱转盘改为迅雷的统计方案
api.py							添加了收益记录接口
web_common.py 					调整了宝箱转盘统计的后台逻辑，今日收益不再包括宝箱转盘收益

###====================2016-5-7===================
admin.py  						测试邮件的发送地址添加了验证
crysadm_helper.py  				添加了自动报告任务(每天凌晨自动报告昨日收益到邮箱)，修复了缓存变动的BUG，修复了丢失矿机数据的BUG，修复了迅雷统计数据不准确的BUG
mailsand.py  					添加了验证邮件地址的函数
user.py     					添加了自动报告开关的支持
templates/profile.html 			添加了自动报告开关

###====================2016-5-6===================
admin.py                                添加了测试邮件发送功能，修复了设置参数跳转到其它标签的BUG
crysadm_helper.py                       添加了安全参数阈值，所有低于15秒的自动任务间隔都将强制解释为15秒。整合了爱转角的BUG修复：自动任务有时不生效。
user.py                                 修复了设置参数跳转到其它标签的BUG
web_common.py                           整合了爱转角的BUG修复：用户不存在时后台报告500
templates/profile.html                  修复了设置参数跳转到其它标签的BUG
templates/admin_settings.html           添加了测试邮件发送功能，修复了设置参数跳转到其它标签的BUG

###====================2016-5-5===================
crysadm_helper.py                       修改所有的自动任务时间单位为秒，请先在前台改成较大的参数之后再升级
template/profile.html                   提示文字更新
template/admin_settings.html            提示文字更新
web_common.py                           整合了码神的修复不显示图表的问题的方案(移除对默认统计的速度曲线的支持)。
template/dashboard.html                 添加了切换迅雷统计、速度曲线、宝箱转盘统计区间的按钮
user.py                                 添加了对切换按钮的支持

###====================2016-5-4 晚上===================
web_common.py                           修复了新用户统计不显示图表的问题

###====================2016-5-4===================
admin.py                                添加了系统参数配置页面
templates/admin_settings.html           添加了系统参数配置页面
crysadm_helper.py                       修改邮件发送逻辑，修改自动任务逻辑，添加了矿机状态自动监测任务
user.py                                 自动任务显示动态提示文字,整合爱转角的邮件邀请逻辑
templates/register.html                 爱转角的邮件邀请前端页面
mailsand.py                             爱转角的邮件发送逻辑
templates/login.html                    修复注册账号的按钮为邀请码输入页面(原来为公开邀请码获取页面)
templates/profile.html                  自动任务显示更详细的提示文字
                                        
###====================2016-5-2 晚上===================
web_common.py                           修复了从未切换过显示速度曲线的用户的异常显示问题
crysadm_helper.py                       修复了从未设置过提现和取现水晶下限的用户的不执行问题
templates/profile.html                  调整了邮箱地址按钮的文字

###==========2016-5-2==========
新增邮件提醒功能
新增状态日志
新增水晶收取下限、邮件地址设置

###==========2016-5-1==========
优化了主界面排版
添加了三态开关用户切换宝箱统计区间
新增了缓存变动日志和矿机状态改变日志

###==========2016-4-30 晚上==========

优化了主界面排版
添加了显示/隐藏速度曲线、本周宝箱/挖矿收益切换开关

###==========2016-4-30 下午==========

添加了速度显示、别名/账户名切换开关

优化了主界面排版、设置页面排版



###==========2016-4-30 上午==========

修复了清空日志报错的BUG

添加了自动只保留31天内日志的功能

##以上为 @独影凭栏 更新

###  2016.04.14 更新 v4.1401 
新增站点监控分页
新增邀请记录页面
新增公开邀请页面
新增公开邀请获取
更改首页注册链接
注意：部分功能依赖反向代理

###  2016.04.12 更新 v4.1201 
新增关于页面
新增站长交流页面
新增站点记录页面

###  2016.04.11 更新 v4.1101 
修复监控中心速度换算判断
修复数据中心数据有效判断
修复Install 账号日记错误
修复本周收益不正常问题

###  2016.04.10 更新 v4.1001 
删除无用接口
添加双重登陆接口
更新部分接口参数
添加迅雷账号全部启用函数
添加迅雷账号全部停用函数
添加迅雷账号全部启用按钮
添加迅雷账号全部停用按钮

###  2016.04.05 更新 v4.0501 
添加秘银复仇接口
添加秘银复仇函数
添加秘银复仇按钮

###  2016.04.03 更新 v4.0301 
添加用户管理登陆时间显示
添加用户管理登陆状态显示

###  2016.04.02 更新 v4.0201 
修复运行日记显示登陆时不刷新问题
修复部分用户登陆失败出现502错误
注意：需重新登陆

###  2016.03.31 更新 v3.3101

添加运行日记

###  2016.03.27 更新 v3.2701

添加更多产量信息，修改进攻和转盘函数

###  2016.03.25 更新 v3.2501

添加炫酷首页；添加速度曲线

###  2016.03.24 更新 v3.2401

由@Tiramisu 提供更新：
增加“APP管理”按钮

由@Seatom 提供更新：
修改crysadm_helper.py，修复免费宝箱和收取水晶问题

###  2016.03.21 更新 v3.2101

如有任何疑问及Bug欢迎加入L.k群讨论
@爱转角遇到了谁 大力更新,请尊重作者
为了您的云监工安全,请立马修改config.py[SECRET_KEY] Key！请不要使用默认的

api.py更新日记:
更新用户提现接口	更新MINE信息接口  
新增免费宝箱接口	新增放弃宝箱接口  
新增秘银进攻接口	新增幸运转盘接口  

crysadm_helper.py更新日记:
删除老式矿机变量	    新增自动用户提现函数  
新增自动免费宝箱函数	新增自动秘银进攻函数  
新增自动幸运转盘函数

excavator.py更新日记:
添加设备升级函数	添加设备定位函数  
添加出厂设置函数	添加设备管理函数  
添加单个账号提现	添加单个账号进攻  
添加单个账号转盘	添加所有账号提现  
添加所有账号进攻	添加所以账号转盘  

admin.py更新日记:
添加自动用户提现变量	添加自动开免费宝箱变量  
添加自动秘银进攻变量	添加自动幸运转盘变量  
更改最高迅雷账号上限:100

ueer.py更新日记:
添加自动用户提现变量	添加自动开免费宝箱变量  
添加自动秘银进攻变量	添加自动幸运转盘变量  
更改注册后迅雷账号上限:20

web_common.py更新日记:
更换类型返回信息	删除老式矿机变量  

register.html更新日记:
添加注册成功提示框

excavator.html更新日记:
删除老式矿机信息	删除雇佣矿机信息  
添加秘银数量信息	添加今日产值信息  
添加设备升级按钮	添加设备定位按钮  
添加出厂设置按钮	添加设备管理按钮  
更换设备显示类型	添加设备固件版本显示  
添加设备端口映射显示	添加单个账号进攻按钮  
添加单个账号转盘按钮	添加所有账号进攻按钮  
添加所以账号转盘按钮

profile.html更新日记:
添加自动提醒开关	添加免费宝箱开关  
添加秘银进攻开关	添加幸运转盘开关  

user_management.html更新日记:
添加自动提醒开关	添加免费宝箱开关  
添加秘银进攻开关	添加幸运转盘开关  



***   

##  2016.03.18 更新

***   

感谢@爱转角遇见了谁 的源码，使监工又能用了，而且加了新功能

更新@爱转角遇见了谁 的源码，增加了自动转盘，自动进攻功能

***    
##2016.03.09 更新
***
更新user.py，解决登出其他用户直接到login页面问题
***
##2016.03.08 更新
***
感谢Dream.Fei的源代码  
更新开宝箱功能，说明进入crysadm文件夹看     

更改收水晶时间为6小时，迅雷帐号最大为200
***
##2016.03.04 14:30 更新
***
更新cron.sh脚本，实现每小时重启一次监工，分钟时间是随机一次
***
##2016.03.02 17:00 更新
***
更新README.MD文件
***
##2016.03.02 9:40更新
***
源代码降回提现功能版本<br>
开宝箱版有问题<br>
刷新数据改为15秒更新<br>
***
##2016.03.01 17:00更新
***
升级了开免费宝箱功能<br>
收水晶改为6小时收一次<br>
***
##以前更新
***
此版本增加了自动提现功能<br>
此版本加了环境安装脚本，安装脚本支持ubuntu 14.04，debian 8，kali 2.0，实测可用<br>
***

