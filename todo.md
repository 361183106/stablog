1.  ❌ 输出 epub 电子书, 而非 pdf
    1.  测试 epub 在多看上的效果
    2.  寻找 epub 生成库(大概率找不到)
    3.  寻找 epub3.2 规范
        1.  https://dpublishing.github.io/epub-specs-tc/epub32/epub-spec.html
    4.  编写基于 epub3.2 规范的生成库
    5.  多看不支持现代 css, 因此不能生成对应电子书. 手机端
2.  ✅ 移除赞助入口
3.  ✅ 体积优化-> 将体积优化到 100mb 以内
4.  ✅ 允许备份他人微博
5.  ✅ 优化 html 文件样式, 调整为 octoman 备份出的样式
6.  ❌ 导出关注人 uid 列表[不建议做]
    1.  没意义, 不如新起一个项目
7.  ✅ 解决用户名折行问题[https://github.com/YaoZeyuan/stablog/issues/33]
8.  ❌ 测试微博新版 api 有没有防爬虫功能.
    1.  看起来可以尝试 => https://weibo.com/ajax/statuses/mymblog?uid=1764741287&page=9&feature=0
    2.  经测试, 新版 api 一样有反爬虫功能, 10s 一次爬取也会被拦截.
    3.  对用户来说, 等待 1 小时才能完成和等 3 小时才能完成是等效的, 所以不浪费时间切新 API 了(还需要适配微博生成格式, 不值得)
9.  ✅ 使用 mozjpeg-js 压缩 jpg 图片
10. ✅ pdf 中支持目录, 方便跳转
11. ✅ 将封面字体改为阿里巴巴普惠体. 看起来正经一点
12. ✅ 将 pdf 首页文字居中
13. ✅ 增加接口, 通过微博新 api, 为微博记录增加创建时间
14. ✅ 测试图片渲染效果
15. 测试微博文章的渲染效果
16. 测试付费微博文章的渲染效果
17. ✅ 规范图片生成地址
18. ❌ 在抓取微博数据期间, 闲着也是闲着, 把渲染图片的工作干了(以微博 id 为 key)
    1.  不进行预渲染了
    2.  抓取失败后, 应重新尝试抓取, 尝试 3 次, 而非直接跳过
19. ✅ 生成一张图片耗时 1s, 估算时间时要把这个加上
20. ✅ 图片只生成一次, 增加重置图片选项
21. ❌ 检查 1_13, 周鸿祎的祎显示为乱码的问题
    1.  原数据如此, 该问题无解
22. 编写使用说明, 说明两种情况
    1.  页面抓取过程中停顿
    2.  页面生成过程中停顿
    3.  登陆时无法输入验证码
23. 升级 Electron 版本
    1.  Electron 升级到 12 后 sqlite3 需要手工安装, 对应命令为`npm install sqlite3 --build-from-source --runtime=electron --target=12.0.0 --dist-url=https://electronjs.org/headers`
24. ✅jspdf 有这个限制. A page in a PDF can not be wider or taller than 14400 userUnit. jsPDF limits the width/height to 14400
25. ✅ 分卷标题需要改正 tombkeeper -第 2／5 卷 2012-12-01~2015-03-31
26. ✅jspdf 最大只能输出 500mb 体积的 pdf, 原因为 content.join 的时候字符串体积超出了 js 引擎最大限制. 两个办法,1. 修复 bug. 2. 限制每本电子书最多只能有 5000 条微博
27. ✅jspdf 的最大页宽只有 14400, 也需要改正. 考虑把 js 代码嵌入到项目中, 单独使用
28. 手上没有 mac 机器, 只能用 github-action 构建, 需要保证可以在 mac 上编译出可用的 sqlite3 版本, 而 sqlite 最高只支持到 8.x, 所以选用可用的 Electron 的最高版本
29. ✅ 替换 jspdf 库, 支持输出大体积 pdf 文件
30. ✅ 输出 pdf 文件时, 添加不可见文本, 以方便搜索
31. ✅ 测试微博文章渲染效果
32. ✅ 支持渲染微博视频封面
33. ✅ 编写数据库管理工具
    1.  选择日期
    2.  展示微博记录
    3.  读取数据库时显示 loading
34. ✅ 支持选择导出原创微博/全部微博
    1.  ✅ 需修改数据库表结构, 增加以下字段
        1.  ✅ 是否原创
        2.  ✅ 是否微博文章
35. ✅ 解除 jspdf 最大图片 14400 的限制, 解除 jspdf 生成 pdf 最大 2gb 的体积限制
36. ✅ 生成日级别书签, 而非只是月级别
37. 测试
38. ✅ 添加按年分卷功能
39. ✅ 页面 title 要按年月日生成
    1.  ✅ 废除指定分页功能, 统一按`年-月-日`生成, 模板上可以加`下一天`标签
    2.  ✅ 需要支持自动分卷, 按年自动分卷或者按微博数自定义分卷
        1.  ✅ 添加 splitBy 配置, 支持按 single, year, month, count 进行配置, 支持按年分卷
40. ✅ 生成 html 时, 要提供下一页按钮, 且固定在底部
41. 输出 pdf 时, 会因为内存不足 outofmemory
    1.  对于 node 进程, 需要加上 --max-old-space-size=8192 flag, 将最大内存限制开到 8GB
    2.  但是对于 electron, 还不清楚该如何处理
        1.  添加`app.commandLine.appendSwitch('js-flags', '--max-old-space-size=10240');`, 解除 Node.js 的体积限制
        2.  经尝试, 似乎未能解决问题.
    3.  原因不明
42. 添加图片到 pdf 时, 添加速度太快, 会导致页面卡死
43. 在说明中加上原理说明
    1.  模拟浏览 m.weibo.com
    2.  所以, 如果没有对应微博浏览权限, 也会出现看不到微博的情况(被拉黑/微博仅粉丝可见/微博需付费)
44. ✅ 解决 umi 在 build 之后, Electron 界面白屏问题
45. 目前没有办法在 Electron 中修改 node 内存上限, 似乎只能通过命令行参数的形式完成修改. 需要在考虑以下
    1.  一个已验证可行的方案: Windows 上创建快捷方式时, 手工带上参数 `C:\Users\yao\AppData\Local\Programs\stablog\稳部落.exe --js-flags="--max-old-space-size=8192"`
46. ✅ 1w 条以上强制分卷, 不支持单卷输出太多电子书
47. 更新说明文档, 提供明确的使用说明
48. 优化配置
49. 解决 mac 上无法打开的问题
50. 支持导入/导出功能
51. ✅ 解决由于微博更换接口, account 识别失败问题
52. 调整 readme 编写思路
    1.  普通用户 => 一路下一步, 然后等待出 pdf 即可
    2.  高级用户 => 预期需要仔细浏览说明文档, 然后才能调整配置, 输出 pdf
