

Run Command:-

docker run -v /home/ubuntu/ashok/:/var/www/html/ --privileged -it --name mycentos -d -v /sys/fs/cgroup:/sys/fs/cgroup:ro -p 80:80 -p 8080:8080 centos:c7-systemd-httpd

Launch Application Using Below URL:-

http://IP:80 <Ip Address Of Docker Host machine>