问题记录：
1、express-session deprecated undefined resave option; provide resave option app.js:17:9
express-session deprecated undefined saveUninitialized option; provide saveUninitialized option app.js:17:9

解决办法：新增两个参数，如下
app.use(session({
    resave: true,  // 新增
    saveUninitialized: true,  // 新增
    secret: settings.cookieSecret,
    key: settings.db,//cookie name
    cookie: {maxAge: 1000 * 60 * 60 * 24 * 30},//30 days
    store: new MongoStore({
        db: settings.db,
        host: settings.host,
        port: settings.port
    })
}));

2、Error setting TTL index on collection : sessions报错

解决办法：将mongodb和connect-mongo都跟新到最新版本
在package.json修改
"mongodb"：“2.0.42”，
“connect-mongo”:“0.8.2”

3、每次我们更新代码后，都需要手动停止并重启应用，使用 supervisor 模块可以解决这个问题，每当我们保存修改的文件时，supervisor 都会自动帮我们重启应用

运行：supervisor bin/www

4、倒计时解决办法html
<!DOCTYPE html>
<html>

	<head>
		<meta charset="utf-8">
		<meta name="author" content="http://www.softwhy.com/" />
		<title>jQuery 60秒倒计时精确到毫秒 | jQuery特效|手机微信网站特效| 网页特效库</title>
<meta name="keywords" content="SVG特效, 手机微信网站特效, css3动画, html5特效, 网页特效" />
<meta name="description" content="网页特效库-专注于HTML5、CSS3、js、jQuery、手机移动端等网页特效的手机与分享。特效库始终坚持：无会员、无积分、无限制的“三无原则”，所有的资源都免费提供广大童鞋下载学习和使用。" />
		<script type="text/javascript" src="http://www.5iweb.com.cn/statics/js/jquery.1.7.1.min.js"></script>
		<script type="text/javascript">
		    function getTime() {
			   var times = 60 * 100; // 60秒
				countTime = setInterval(function() {
					times = --times < 0 ? 0 : times;
					var ms = Math.floor(times / 100).toString();

					if(ms.length <= 1) {
						ms = "0" + ms;
					}
					if(times == 0) {
						alert("下一期开始");
						times = 60 * 100

						clearInterval(countTime);
					}
					// 获取分钟、毫秒数
					$(".a").html(ms);
				}, 10);
			}
		</script>
		<style>
			.warp{
				width: 100%;
				height: 100px;
				line-height: 100px;
				text-align: center;
				font-size: 40px;
				font-family: "微软雅黑";
			}
			.warp strong{
				width: 100px;
				display: inline-block;
				text-align: center;
				font-family: georgia;
				color: #C9302C;
			}
		</style>
	</head>

	<body>
		<div class="warp">
			<button onclick="getTime()">开始</button><strong class="a">60</strong>秒
		</div>
	</body>

</html>
