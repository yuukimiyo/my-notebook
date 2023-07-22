# compose.yml for Jupyter notebook

# 注意点

./dataフォルダが必要。

## Data folder

利用には./dataが必要。Jupyter notebookからの書き込み用に次のユーザ/グループを作成し、自ユーザおよび./dataフォルダを所属させる。必要な場合、UID/GIDをオリジナルのDockerfileで確認する。

https://github.com/jupyter/docker-stacks/blob/main/docker-stacks-foundation/Dockerfile

```
sudo groupadd -g 100099 docker-group
sudo useradd -g docker-group -u 100999 docker-user

sudo usermod -aG docker-group yuuki
sudo chgrp docker-group data
```

## Network

他のコンテナと通信するために独自ネットワークを作成しておく。

```
docker network create my-network
```

# その他

## root作業

rootユーザでの作業が必要な場合は次のコマンドでコンテナへログインする。

```
docker exec -it --user root {コンテナ名} /bin/bash
```

## jovyanユーザの設定

コンテナへrootユーザでログインして実施する。

```
# パスワードを付与
passwd jovyan

# ユーザのロックを解除
passwd -u jovyan

# パスワード無しsudo設定
echo "jovyan ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/jovyan
```
