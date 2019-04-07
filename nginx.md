# 正向代理、反向代理、负载均衡
(link)[http://www.jikexueyuan.com/course/2163.html]
1. 正向代理：隧道，当你访问google不能正常访问，你通过另一台服务器访问，这台服务器就是正向代理
1. 反向代理：当你访问baidu的时候，百度后面有成千上万的服务器,中间有一台服务器作为分发资源，这个就是反向代理
1. 负载均衡：

#  docker 

1. docker 安装 nginx:   docker pull  nginx
2. docker 运行 nginx： docker run -p 80:80 --name mynginx -v $PWD/www:/www -v $PWD/conf/nginx.conf:/etc/nginx/nginx.conf -v $PWD/logs:/wwwlogs  -d nginx 
3. 访问  localhost/index.html

# nginx 配置文件

1. nginx.conf

   ``` text
   user       www www;  ## Default: nobody
   worker_processes  5;  ## Default: 1
   error_log  logs/error.log;
   pid        logs/nginx.pid;
   worker_rlimit_nofile 8192;
   
   events {
     worker_connections  4096;  ## Default: 1024
   }
   
   http {
   
     upstream big_server_com {
       server 220.181.57.216; ## baidu for test
       server 203.119.216.238; ##alibaba.com
       server 106.11.62.15; ##taobao.com
     }
   
     server { # simple load balancing
       listen          80;
       access_log      logs/big.server.access.log main;
   
       location / {
         proxy_pass      http://big_server_com;
         # 这里的 big_server_com 没什么作用这是和 upstream相同，并从upstream中进行寻找
       }
     }
   }
   ```
   
2. docker 删除第一个container  commitid

   ```shell
   docker rm $(docker ps -a|head -n 2 | grep -v CONTAINER |awk '{print $1}')
   ```

3. docker 启动的服务

    ``` shell
    docker ps #显示所有正常的container
    docker ps -a #显示所有container(包含不正常退出的)
    docker logs commitid #为什么不正常退出
    ```

4. docker nginx 错误

   ```text
   2019/04/07 09:23:14 [emerg] 1#1: getpwnam("pang") failed in /etc/nginx/nginx.conf:1
   nginx: [emerg] getpwnam("pang") failed in /etc/nginx/nginx.conf:1
   nginx.conf用户名 用户组不对 改成 
   user  nobody nogroup;
   ```
5. docker 启动

   ```shell
   docker run -p 80:80 --name my -v $PWD/config/nginx.conf:/etc/nginx/nginx.conf:ro  -d nginx
   ```