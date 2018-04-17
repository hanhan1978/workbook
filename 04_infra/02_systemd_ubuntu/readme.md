
vagrant up


apt update


systemctl list-unit-files -t service | grep enabled

systemctl list-units -t service

systemctl -t service   //同じ

# check each type

systemctl -t swap
systemctl -t mount
systemctl -t device

