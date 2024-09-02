#Home-Projects #LocalVos
# What is Immich
---
_Immich_ is an image server. Running this service locally could allow for a full replacement of _Google Photos_. If you need any more help in regards to installing _Immich_ you can always go to [their documentation](https://immich.app/docs/install/requirements)

# My GitHub setup
---
```bash
git clone https://github.com/LocalVos/My-Immich-Setup.git
cd My-Immich-Setup
sudo docker compse up -d
```
# Docker Compose
---
>An automatic installer script exist but as of writing this it is not recommended yet.

I will go over [the documentation of Immich](https://immich.app/docs/install/requirements).

```sh
cd
mkdir ./immich-app
cd ./immich-app

wget -O docker-compose.yml https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml

wget -O .env https://github.com/immich-app/immich/releases/latest/download/example.env

wget -O hwaccel.transcoding.yml https://github.com/immich-app/immich/releases/latest/download/hwaccel.transcoding.yml

wget -O hwaccel.ml.yml https://github.com/immich-app/immich/releases/latest/download/hwaccel.ml.yml

```

If you want you can populate the .env file with custom values like setting a different `UPLOAD_LOCALTION` or changing the `DB_PASSWORD`

> Postgres is not publicly exposed, so this password is only used for local authentication. To avoid issues with Docker Parsing this values it is best to use only the characters `A-Za-z0-9`.

Next you can run:
```bash
sudo docker compose up -d
```

# Updating Immich
---
Updating Immich is easy. All you have to do is run:
```bash
docker compose pull && docker compose up -d
```

>Immich is currently under heavy development, which means you can expect breaking changes and bugs. Therefore, we recommend reading the release notes prior to updating and to take special care when using automated tools like Watchtower.

# Error handling

>If you get an error `unknown shorthand flag: 'd' in -d`, you are probably running the wrong Docker version. (This happens, for example, with the docker.io package in Ubuntu 22.04.3 LTS.) You can correct the problem by `apt remove`ing Ubuntu's docker.io package and installing docker and docker-compose via [Docker's official repository](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository).

```bash
sudo apt remove docker
sudo apt remove docker-compose
```

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

```bash
# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

