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


