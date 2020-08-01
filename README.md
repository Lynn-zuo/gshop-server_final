## 说明
1.后台项目说明
    1). 这是硅谷外卖项目的后台应用
    2). 默认短信验证码只能向此手机号发送验证码: 13716962779 (可以通过后台打印查看验证码, 也是可以使用的)
    3). 如果想修改需要根据视频讲解步骤修改
        a. 注册并登陆容联云通信的账号
        b. 添加测试号码为你的手机号
        c. 修改util/sms_util.js中的账号相关信息为你的信息
            var ACCOUNT_SID = '8aaf070855b647ab0155b9f80994058a'; // 可以改成自己的
            var AUTH_TOKEN = 'aa8aa679414e49df8908ea5b3d043c24'; // 可以改成自己的
            var Rest_URL = 'https://app.cloopen.com:8883';
            var AppID = '8aaf070855b647ab0155b9f809f90590'; // 可以改成自己的

2. 项目开发与部署
    1). 跨域后端配置---部署在服务器端
    nginx反向代理--nginx服务器配置
    server
    {
        listen 80; // 前台项目端口号
        server_name 140.143.133.253; // 前台项目ip或域名
        index index.html index.htm index.php;
        root  /www/wwwroot/lynn_z.com/dist; // 前台项目根目录
        
        location /api {
          proxy_pass http://140.143.133.253:4000; // 后端域名或IP
          rewrite ^/api/(.*)$ /$1 break; // 重写URL
          proxy_cookie_domain 140.143.133.253:4000 140.143.133.253:81; // 修改cookie中域名
          add_header Access-Control-Allow-Origin 140.143.133.253:80;
          add_header Access-Control-Allow-Credentials true;

        }
    }