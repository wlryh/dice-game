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
