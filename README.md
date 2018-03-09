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
