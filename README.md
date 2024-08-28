# gpg-public-key

## Get gpg key from git
```
sudo curl -sSL https://github.com/saha-robotics/gpg-public-key/raw/main/saha-keyring.key -o /etc/apt/keyrings/saha-keyring.gpg
```

## Add Url to source list
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/saha-keyring.gpg] https://saha-apt.s3.eu-central-1.amazonaws.com $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/saha-robotics.list > /dev/null
```

## Arrange priorities
```
echo -e "Package: *\nPin: origin saha-apt.s3.eu-central-1.amazonaws.com\nPin-Priority: 1011" | sudo tee /etc/apt/preferences.d/saha
```

## Update repository list
```
sudo apt update
```

### update the repo (remote)
aptly publish update jammy s3:server:.


### get humble nav2 1.1.9 repos (lucky)

aptly mirror -ignore-signatures create TEST http://snapshots.ros.org/humble/2023-09-25/ubuntu/ jammy main

aptly mirror -ignore-signatures update TEST


#### create snapshot from mirror

aptly snapshot create ros-snapshot-20240828 from mirror TEST

#### get previous snapshot from repo

aptly snapshot create ros-v1-20240828 from repo saha-robotics

#### merge two snapshots into one

aptly snapshot merge ros-v2-20240828 ros-snapshot-20240828 ros-v1-2024082







#### publish merged snapshot

aptly publish snapshot ros2-v1-snapshot s3:server:.
