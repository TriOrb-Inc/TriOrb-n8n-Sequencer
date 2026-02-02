# Docker & Docker Compose セットアップ手順（Ubuntu）

このドキュメントでは、Ubuntu環境でDockerおよびDocker Composeをインストールし、ユーザーをdockerグループに追加する手順をまとめています。

---

## 1. 事前準備

```bash
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release
```

## 2. Docker公式GPG鍵の取得

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

## 3. Dockerリポジトリの追加

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## 4. Docker Engineのインストール

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin
```

## 5. Docker Composeプラグインのインストール

```bash
sudo apt install docker-compose-plugin
```

## 6. dockerグループへのユーザー追加

```bash
sudo usermod -aG docker $USER
```

※ 反映のため一度ログアウトし、再度ログインしてください。

## 7. 動作確認

```bash
docker --version
docker compose version
```

---

以上でDockerおよびDocker Composeのセットアップは完了です。