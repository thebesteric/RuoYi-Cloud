FROM nginx
LABEL maintainer=eric

# 复制html文件到路径
COPY ./dist /usr/share/nginx/html/
COPY ./nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
