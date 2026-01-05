# OXEC Immigration Static Frontend

此仓库包含 OXEC Immigration 网站的静态版本，并提供了使用 Docker 部署的简单方式。仓库内的页面已经增加了统一的中文友好字体及排版设置，便于在本地或服务器上快速启动浏览。

## 部署要求
- 已安装 [Docker](https://docs.docker.com/get-docker/)
- 可选：如果需要以不同端口运行，请确保对应端口未被占用

## 构建镜像
在仓库根目录运行：

```bash
docker build -t oxecimm-frontend .
```

该命令会基于 `nginx:alpine` 创建镜像，并将当前目录的静态文件复制到镜像内的 `/usr/share/nginx/html`。

## 启动容器
构建完成后，使用以下命令启动站点（示例使用本地 8080 端口）：

```bash
docker run -d --name oxecimm-frontend -p 8080:80 oxecimm-frontend
```

容器运行后，浏览器访问 <http://localhost:8080> 即可看到页面。

## 更新内容后重新部署
1. 修改或新增静态文件（如 HTML、CSS、图片等）。
2. 重新执行镜像构建命令：
   ```bash
   docker build -t oxecimm-frontend .
   ```
3. 重启容器以加载最新资源：
   ```bash
   docker stop oxecimm-frontend && docker rm oxecimm-frontend
   docker run -d --name oxecimm-frontend -p 8080:80 oxecimm-frontend
   ```

## 关于字体与排版
仓库新增的 `custom.css` 会在所有页面中统一应用中文无衬线字体（Noto Sans SC）、标题加粗、正文行距增大以及主体内容区域的左右留白，使页面内容在桌面端和移动端都更加整齐、易读。
