# set up new user on Server

```bash
# create user and home dir
sudo adduser USER

# add new user to sudo group
sudo usermod -aG sudo USER

# create .ssh dir and authorized_keys
sudo mkdir /home/USER/.ssh
sudo touch /home/USER/.ssh/authorized_keys

# add this dir and file to the right user and group
sudo chown USER:USER /home/USER/.ssh/
sudo chown USER:USER /home/USER/.ssh/authorized_keys

# copy over public key to authorized_keys file
sudo vim /home/USER/.ssh/authorized_keys
```
