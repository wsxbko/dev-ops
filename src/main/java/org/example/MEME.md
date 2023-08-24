//把nginx在docker里的配置文件拷贝到项目文件中
docker container cp nginx:/etc/nginx/nginx.conf E:\work\demo\ChatGPT\dev-ops\nginx\conf
docker container cp nginx:/etc/nginx/conf.d/default.conf E:\work\demo\ChatGPT\dev-ops\nginx\conf\conf.d\default.conf
docker container cp nginx:/usr/share/nginx/html/index.html E:\work\demo\ChatGPT\dev-ops\nginx\

//重新创建容器将映射文件目录 映射到项目文件目录
docker run \
--name nginx \
-p 11180:80 \
-v E:\work\demo\ChatGPT\dev-ops\nginx\logs:/var/log/nginx \
-v E:\work\demo\ChatGPT\dev-ops\nginx\html:/usr/share/nginx/html \
-v E:\work\demo\ChatGPT\dev-ops\nginx\conf\nginx.conf:/etc/nginx/nginx.conf \
-v E:\work\demo\ChatGPT\dev-ops\nginx\conf\conf.d:/etc/nginx/conf.d \
-v E:\work\demo\ChatGPT\dev-ops\nginx\ssl:/etc/nginx/ssl/ \
--privileged=true -d --restart=always nginx
//上面的\错了，用下面的
docker run --name nginx -p 11180:80 nginx:1.24.0 -v E:/work/demo/ChatGPT/dev-ops/nginx/logs:/var/log/nginx -v E:/work/demo/ChatGPT/dev-ops/nginx/html:/usr/share/nginx/html -v E:/work/demo/ChatGPT/dev-ops/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -v E:/work/demo/ChatGPT/dev-ops/nginx/conf/conf.d:/etc/nginx/conf.d -v E:/work/demo/ChatGPT/dev-ops/nginx/ssl:/etc/nginx/ssl/ --privileged=true -d --restart=always nginx