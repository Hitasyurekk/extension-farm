# extension-farm

## Sanal sunucumuza docker kurulumu ile başlıyoruz. 

```
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Docker version check
docker --version

```

## Docker kurulumundan sonra sunucumuzun Saat dilimini öğreniyoruz burası önemli.

```
realpath --relative-to /usr/share/zoneinfo /etc/localtime
```

## Chromium kurulumu

**İlk önce chromium için sunucuda yer hazırlıyoruz**

```
mkdir chromium
cd chromium
```

**Docker compose dosyası oluşturuyoruz**

```
nano docker-compose.yaml
```

```
---
services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined #optional
    environment:
      - CUSTOM_USER=     #Replace username
      - PASSWORD=    #Replace password
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - CHROME_CLI=https://github.com/hitasyurekk #optional
    volumes:
      - /root/chromium/config:/config
    ports:
      - 3010:3000   #Change 3010 to your favorite port if needed
      - 3011:3001   #Change 3011 to your favorite port if needed
    shm_size: "1gb"
    restart: unless-stopped
 ```

   <code> Ctrl+X+Y+Enter </code> **İşlemleri ile dosyadı kaydedip çıkıyoruz.**

   ## Son adım Chromium çalıştırma 

```
   cd $HOME && cd chromium

docker compose up -d
```

## Artık hazırsınız , şimdi yapmanız gereken şey kendi bilgisayarınızdan sunucuya bağlanmak ve eklentileri kurmak
```
http://Sunucu_IP:3010/
https://Sunucu_IP:3011/
```


# Adım 2 eklentileri kurmak!

**Öncelikle tavsiyem bu sunucularda yeni hesap oluşturmanız isteyen kendi hesabınıda kullanabilir ama ne olur ne olmaz yeni hesap kurmak daha sağlıklı olur.**

[Nodepay](https://app.nodepay.ai/register?ref=OcK6UeIDXtTJaBN)

[UpNetwork](https://points.upnetwork.xyz/?request=122473)

[Gradient](https://app.gradient.network/signup?code=OKZ66P)

[Block mesh](https://app.blockmesh.xyz/register?invite_code=rove)

[Teneo](https://teneo.pro/community-node) **Giriş kodu : GRRqs**


