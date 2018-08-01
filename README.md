# autoindex
autoindex for Nginx
美化 Nginx 默认的目录文件 索引页

------

### 配置方法：

1. 复制 .autoindex 目录至 D:\websites\fulicat\
ps: D:\websites\fulicat\\.autoindex
  

2. 修改 nginx.conf 文件

```
# fulicat.bz
server {
    listen          80;
    server_name     fulicat.bz;
    root            D:\websites\fulicat;

    location / {
        index index.html index.htm index.php;
    }

    # autoindex for nginx 
    #如果请求为apk/ipd/zip之类的静态文件，且命中此location,则会导致文件格式损坏.建议使用body_filter_by_lua，并加入mime类型判断
    location ~ ^(.*)/$ {
        autoindex       on;
        autoindex_localtime on;
        autoindex_exact_size off;

        #add_before_body /.autoindex/header.html;
        add_after_body /.autoindex/footer.html;
    }

    location ~ \.php$ {
        fastcgi_pass        127.0.0.1:9000;
        fastcgi_index       index.php;
        fastcgi_param       SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include             fastcgi_params;
    }
}
```

------


# Screenshots:

### before:
![before](https://raw.githubusercontent.com/fulicat/autoindex/master/autoindex_before.png)

### after:
![after](https://raw.githubusercontent.com/fulicat/autoindex/master/autoindex_after.png)
