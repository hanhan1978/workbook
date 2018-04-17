
docker run --rm -it -p 80:80 ubuntu:18.04 bash


apt update

apt install -y systemd apache2


systemctl list-unit-files -t service

systemctl list-units -t service

systemctl -t service   //同じ


systemctl -t swap
systemctl -t mount
systemctl -t device

