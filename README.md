# OXEC Immigration Static Site

本仓库包含傲赛移民网站的静态版本，可通过轻量化的 Docker 容器在端口 **666** 上部署。首页导航与快捷入口均指向本地的二级目录，便于登录后快速访问各板块。

## 本地预览
1. 在仓库根目录启动一个简易服务器：
   ```bash
   python -m http.server 8000
   ```
2. 浏览器访问 <http://localhost:8000> 即可预览首页和各二级目录。

## Docker 部署
1. 构建镜像：
   ```bash
   docker build -t oxecimm-site .
   ```
2. 运行容器（容器内外均使用端口 666）：
   ```bash
   docker run -d --name oxecimm-site -p 666:666 oxecimm-site
   ```
3. 部署完成后访问：<http://localhost:666>

### 目录结构说明
- `Dockerfile`：使用 `nginx:alpine` 构建的轻量化镜像，默认暴露端口 666。
- `docker/nginx.conf`：服务器配置，启用 `try_files` 以便直接访问二级目录。
- `.dockerignore`：忽略 Git 元数据等文件，保持镜像精简。

## 修改与发布
- 页面更新后重新构建镜像即可同步变更：
  ```bash
  docker build -t oxecimm-site . && docker run -d --rm -p 666:666 oxecimm-site
  ```
- 如果需要调整监听端口，可修改 `docker/nginx.conf` 中的 `listen` 配置并重新构建。
