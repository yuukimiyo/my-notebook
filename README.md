# compose.yml for Jupyter notebook

# 注意点

利用には./dataフォルダが必要。

Jupyter notebookからの書き込み用に次のユーザ/グループを作成し、自ユーザおよび./dataフォルダを所属させる。
必要な場合、UID/GIDをオリジナルのDockerfileで確認する。

https://github.com/jupyter/docker-stacks/blob/main/docker-stacks-foundation/Dockerfile

```
sudo groupadd -g 100099 docker-group
sudo useradd -g docker-group -u 100999 docker-user

sudo usermod -aG docker-group yuuki
sudo chgrp docker-group data
```

