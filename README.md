## 项目名称：中国企业招聘教育岗位数据分析
谁能分得国内企业教育岗位的一杯羹？通过对中国猎聘网爬取的数据分析国内应聘教育岗位的市场环境及对于应聘能力的研究，为有意向从事教育岗位或者正在从事教育岗位的人员提供参考。
* [项目pythonanywhere部署报告](http://littlelucaszy.pythonanywhere.com/)

## 问题表述：
### 1.项目为啥要做？
随着国家发展对于教育的越发重视，企业中教育岗位的也正更新发展，在这样的大环境发展下，人才市场对于从事企业中的教育岗位有了更为强烈的需求。
### 2.是谁有需要解决的问题？
想要应聘国内教育岗位的人、需要了解国内企业教育岗位数据趋向的人（用户画像）
### 3.用户需求：
* 使用场景：高校师范类应届毕业生需要找第一份正式工作，希望能得到一份可靠的教育岗位分析数据
* 任务：快速得到一份国内企业应聘教育岗位的分析报告
* 痛点：网络相关讯息众多复杂，缺少了一份清晰简洁又专业的报告书
* 增长/益点：找到个城市教育岗位的数据情况、应聘要求
### 4.用户画像
![](https://github.com/ZengWenYan/PythonCourseProject/blob/master/%E7%94%A8%E6%88%B7%E7%94%BB%E5%83%8F.png)

## 解决方案表述
### 1.项目如何做分析？
* 先通过[中国猎聘网](https://www.liepin.com/city-gz/zhaopin/?init=1)收集相关的国内企业教育岗位的信息，并且收集到的数据做好数据清洗
* 首先从全局观出发做出大的教育岗位数量分布地区图，然后再通过同样的办法做出教育岗位相关的要求对比图，例如：学历要求、经验要求、语言要求、具体的职位要求。
* 最后结合数据呈现结果，综合从总体到局部去进行分析国内环境下应聘教育岗位的要求
### 2.项目结果解决了谁的问题？
解决了想要应聘国内教育岗位环境的人或者需要了解国内企业教育岗位人才需求数据趋向的人的问题
### 3.项目结果的设计思维部分：
* 商业可行性：企业/投资者可以为教育岗位市场与教育人才市场的关系进行战略调整；应聘者可以通过这一份数据进行自我未来规划和应聘策略。
* 技术可行性：利用中国猎聘网给予的开放数据进行挖掘后，可利用panadas、pyecharts完成数据清洗和图表制作。
* 用户可欲性：能够帮助该类用户解决实际应聘需求、招聘市场分析的考察。 

## 数据分析思路及方法
* 读出“猎聘教育相关岗位详情页.xlsx”表格

![](https://github.com/ZengWenYan/PythonCourseProject/blob/master/%E8%AF%BB%E8%A1%A81.png)

* 清洗数据（工作城市栏位处理：筛选出包含下级区域城市-生成列表准备处理-利用for循环处理数据-数据原表替换-数据更新-进行分进合击）

![](https://github.com/ZengWenYan/PythonCourseProject/blob/master/%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90%E5%9B%BE.png)

## 数据分析流程及成果
* 在分进合击之后，为了让求职者直观地了解到公司主要在哪些城市招聘，也可以了解到哪些城市缺乏教育的人才，同时也能查看到里边是否有自己的心仪的城市，甚至也能知道在教育这方面竞争的激烈程度制作了地图可视化。
![](https://github.com/ZengWenYan/PythonCourseProject/blob/master/%E6%95%88%E6%9E%9C%E5%9B%BE1.png)
* 在了解大环境后，为了让用户了解到不同因素（学历、经验、语言）对于国内应聘教育岗位的影响，分别制作了饼状图、玫瑰图、水滴图。
![]https://github.com/ZengWenYan/PythonCourseProject/blob/master/%E6%95%88%E6%9E%9C%E5%9B%BE2.png)
* 最后为了让用户对于应聘要求有更细节的了解，就运用主题建模的方式对其做了主题建模可视化。
![](https://github.com/ZengWenYan/PythonCourseProject/blob/master/%E6%95%88%E6%9E%9C%E5%9B%BE3.png)

## 三个文档描述
### Web App动作描述：
1. "/": 响应GET请求，返回 GDP per person.csv 文件内容数据并在界面展示
2. "/hurun": 响应POST请求，读取 pregrant.csv、literacy.csv、GDP per person.csv、literacy.csv 文件内容并生成 柱状图、折线图、Map图数据返回页面
							
### Python 函数介绍:
1. getCsvData: 通过传入不同文件名称，并返回pandas数据对象
2. readCsvData: 通过传入不同文件名称，返回pandas数据对象
3. bar_gdp：接入传输数据 并将数据生成柱状图 展示人均GDP年增长率
4. grid_mutil_yaxis：将数据通过 bar line方法 生成折线图与柱状图并展示生育率与GDP增长率对比图
5. map_data：根据参数生成 识字率&生育率 Map图信息
6. hu_run_2019() 通过flask "/"路由，指定GET请求方法，读取GDP per person.csv 文件数据内容 并以results2.html文件作为模板以响应返回 
7. hu_run_select() 通过 "/hurun"路由，指定POST请求方式， 调用gbar_gdp、 grid_mutil_yaxis、 map_data函数将结果返回web界面
8. logger封装 日志模块 记录日志信息 并将日志数据存储；log文件夹下
9. 使用if、elif的条件判断语句以打开不同的图表文件功能
10. 使用for循环，遍历含有复杂数据的嵌套列表，并返回一个表格
11. 使用with语句和open()函数以打开图表文件
12. 使用csv模块并利用csv.reader()函数读取csv文件，利用.readlines()函数读取html文件
13. 使用python内置函数list()使csv文件转化为嵌套列表
14. 使用flask模块的request.form()接受前端页面传来的表单数据，render_template()函数返回一个HTML页面和页面标题、表格数据
15. 引用了pandas、pyecharts、PIL、matplotlib、numpy、time、json、logging第三方模块
16. 利用''.join()函数把列表转化为字符串
17. 使用try、except异常处理
18. 使用下拉框功能可以实现在同一个url下查看不同的表
	
### HTML文档：
1. html使用jinjia2 模板语言+html+JavaScript制作。其中模板语言主要使用了循环和判断，用于自动生成表格和翻页按钮。
2. 页面中使用了 echart 库进行绘制，echart是JavaScript的一个第三方库。除此之外还通过html的<select>标签的onchange属性配合。
3. JavaScript函数实现了页面刷新，通过<button>标签的onclick熟悉配合JavaScript实现翻页功能。
3. JavaScript函数实现了页面刷新，通过<button>标签的onclick熟悉配合JavaScript实现翻页功能。
4. HTML新语义元素使用。
5. 利用HTMl5优点，在<a>标签中放入多个元素。
6. 利用css3实现响应式网页。
7. 使用了boostrap前端框架的按钮、网格系统、导航栏下拉框和轮播图。
8. 在index.html页面使用了多个<form>标签，发送表单数据到python后端。	
***
## 学习/实践心得总结及感谢
通过本次python语言课程的学习以及项目的实践，我意识到了对科学思维培养的重要性，并且学习到了有关python语言的一些基本运用。在此由衷感谢许智超老师的教学与指导；感谢中国猎聘网提供的数据；感谢jupyter notebook提供的技术平台支持。
