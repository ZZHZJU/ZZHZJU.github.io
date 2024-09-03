# 主页

<body>
<font color="#B9B9B9">
  <p style="text-align: left; ">
      <span>本站已经运行</span>
      <span id='box1'></span>
</p>
  <div id="box1"></div>
  <script>
    function timingTime(){
      let start = '2024-2-26 00:00:00'
      let startTime = new Date(start).getTime()
      let currentTime = new Date().getTime()
      let difference = currentTime - startTime
      let m =  Math.floor(difference / (1000))
      let mm = m % 60  // 秒
      let f = Math.floor(m / 60)
      let ff = f % 60 // 分钟
      let s = Math.floor(f/ 60) // 小时
      let ss = s % 24
      let day = Math.floor(s  / 24 ) // 天数
      return day + "天" + ss + "时" + ff + "分" + mm +'秒'
    }
    setInterval(()=>{
      document.getElementById('box1').innerHTML = timingTime()
    },1000)
  </script>
  </font>
</body>

<font color="purple" size="6" class="clear-text">Welcome to Nana's Notebook !</font>

<font color=#608DBD size="4" >每日诗词：</font>

<font  color= #608DBD size=4>
<span id="jinrishici-sentence">正在加载今日诗词....</span>
<script src="https://sdk.jinrishici.com/v2/browser/jinrishici.js" charset="utf-8"></script>
</font>


## 关于我
来自四川成都，ZJU软件工程在读，欢迎来看我的博客~

## 我想要在这里分享的一些东西
!!!note
    * 技术积累(<del>CS 主要靠自学</del>)
    * ZJU 部分课程的笔记和经验
    * 一些杂谈，我的一些碎碎念

***

## 一些有用的链接
!!!note
    * [CS自学指南](https://csdiy.wiki/) 
    * [ZJU-CS-ALL-IN-ONE](https://isshikihugh.github.io/zju-cs-asio/)
    * [在线编译器](https://onecompiler.com/)
    * [cppperference](https://zh.cppreference.com/w/%E9%A6%96%E9%A1%B5)
    * [Latex数学符号表](https://oi-wiki.org/intro/symbol/)

## 个人的学习计划
- [ ] C++项目练习 [aut courseworks](https://github.com/courseworks) & [project-based-learning](https://github.com/practical-tutorials/project-based-learning?tab=readme-ov-file)
- [ ] 结合深度学习模型和静态分析结果来进行软件成分分析相关论文阅读
- [ ] 线性代数补充学习 MIT Linear Algebra
- [ ] ads learning & 算法刷题


<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>

        浏览量：<span id="busuanzi_value_site_pv"><i class="fa fa-spinner fa-spin"></i></span>| 访客数：<span id="busuanzi_value_site_uv"><i class="fa fa-spinner fa-spin"></i></span>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class="giscus"></div>
   <script src="https://giscus.app/client.js"
        data-repo="ZZHZJU/ZZHZJU.github.io"
        data-repo-id="R_kgDOLzHvOg"
        data-category="General"
        data-category-id="DIC_kwDOLzHvOs4ChnMd"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="preferred_color_scheme"
        data-lang="zh-CN"
        crossorigin="anonymous"
        async>
</script>
</body>
</html>