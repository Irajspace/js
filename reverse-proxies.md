# Nginx
-![alt text](reverse-proxies-images/image-28.png)
- Layer 4 and Layer 7 processing in NGINX
- THE OSI MODEL
```
layer - 7 application layer
layer -6 tls layer, encryption
layer -5 - establish sessio id
layer -4 - transport layer- breaks into segments - divide into port no 
         - tcp/udp
layer -3 - network layer-the destination ip and source ip address attached 
layer-2 - data link layer - it breaks down into packets- adds target mac address
layer -1- phsyical layer - bits -0101010

```
![alt text](reverse-proxies-images/image-29.png)
![alt text](reverse-proxies-images/image-30.png)
![alt text](reverse-proxies-images/image-31.png)
```
using stream context it becomes layer 4 proxy
using http context it becomes layer 7 proxy


in layer -4 we only know the ip adress and port
after identifying the correct server it changes the port no using network address translation

```
![alt text](reverse-proxies-images/image-32.png)
![alt text](reverse-proxies-images/image-33.png)

## tcp config-haproxy
![alt text](reverse-proxies-images/image-34.png)
![alt text](reverse-proxies-images/image-35.png)

## layer-7 http
![alt text](reverse-proxies-images/image-36.png)
![alt text](reverse-proxies-images/image-37.png)


## nginx webserver
```
http{
    server{
        listen:8080;
    }
}
events{

}
you can serve contents of a directory file

http {
    server{
        listen:8080
        root: users/path
    }
}
events{

}

how to restrat the nginx
1) stop nginx and start nginx
2) nginx -s reload


location /reverse-proxies-images/images{
    root /Users/Hussein Nasser 
}
```
![alt text](reverse-proxies-images/image-38.png)
![alt text](reverse-proxies-images/image-39.png)

## if someone wishes to go to 8888 proxy it to 8080
![alt text](reverse-proxies-images/image-40.png)

## layer 7 proxy
- Here all the servers will go round-robin
![alt text](reverse-proxies-images/image-41.png)
-ip_hash
-here with ip will go to same backend. so stikcy hash
![alt text](reverse-proxies-images/image-42.png)

## layer 4 proxy
