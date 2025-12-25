# Create Users & Configure Groups

## Create Users
```bash
sudo useradd -m -G [group] -s /bin/bash [username]
# set group to wheel for sudo access
```

## Configuring Wheel Group
```bash
su -
visudo
# uncomment to give wheel sudo privilege
```
