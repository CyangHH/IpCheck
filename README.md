**一个简单查看国内国外IPv4/v6的分流情况的页面**  

## PC端：  


![GitHub图像](/pc.jpg)  


## 手机端：  

![GitHub图像](/phone.jpg)  


演示网站：[ip.cyang.net](https://ip.cyang.net/)  


## 接口来源：  

### 以前用的：

 [Yinghualuo](https://v2ex.com/t/1149457) 

 [ipinfo.io](https://ipinfo.io/)   
 
 [纯真CZ88](https://www.cz88.net/)  

### 目前用的：

 [https://github.com/ljxi/GeoCN](https://github.com/ljxi/GeoCN) 
 
 #### 关于IPDB docker部署
 
 开启docker IPV6支持
 
 vim /etc/docker/daemon.json
  
{
  "ipv6": true,
  "fixed-cidr-v6": "fd00::/64",
  "log-driver": "none"
}

docker network create --ipv6 --subnet="fd00:1:2:3::/64" my-ipv6-network

-------------------------------------
 
  docker run -d -p 8000:80 netart/ipapi

  原作者的意思使用nginx反代用，让nginx负责把真实地址写入xff里面，这样用ipv4回源也可以查询IPV6
 
 ~~原作者的docker镜像，IPV6部分有问题，没有监听IPV6地址~~
 
 ~~请修改 update_and_restart.sh~~
 
 ~~在sleep 86400; 上面添加~~
 
 ~~nohup uvicorn main:app --host :: --port 8080 --no-server-header --proxy-headers &~~
 
 ~~再启动一个实例监听 IPV6地址。~~
 
 -----------------------------
 
 你也可以使用我修改的镜像，使用 Gunicorn替换uvicorn命令，以确保正确可靠的 IPv4/IPv6 双栈绑定，使用方法如下：
 
 docker run -d \
  --name checkip \
  --network my-ipv6-network \
  -p 0.0.0.0:8000:8080 -p [::]:8000:8080 cyang/checkip
 
 如果使用nginx反代，可以让该实例保持仅本机访问
 
 docker run -d \
  --name checkip \
  --network my-ipv6-network \
  -p 127.0.0.1:8000:8080 -p [::1]:8000:8080 cyang/checkip
  

  
  
  
  

 

 
