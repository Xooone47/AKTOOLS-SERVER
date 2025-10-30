# AKTOOLS SERVER

More detail about AKTOOLS: https://github.com/akfamily/aktools?tab=readme-ov-file

## Usage

### 方式一：本地运行

```bash
# If need
python -m venv venv

source venv/bin/activate

pip install -r requirements.txt

python -m aktools


# Exit
deactivate

```

Server running on: http://127.0.0.1:8080/

### 方式二：Docker运行

#### 构建镜像

```bash
docker build -t aktools-server:latest .
```

#### 运行容器

```bash
# 基本运行
docker run -d -p 8080:8080 --name aktools-server aktools-server:latest

# 查看日志
docker logs -f aktools-server

# 停止容器
docker stop aktools-server

# 删除容器
docker rm aktools-server
```

Server running on: http://127.0.0.1:8080/
