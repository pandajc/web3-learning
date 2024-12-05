
##### npm配置国内镜像
```
npm config set registry https://registry.npmmirror.com
```

##### 创建next.js工程
新建nextjs工程
```
npx create-next-app@latest
```
安装nextjs和react
```
npm install next@latest react@latest react-dom@latest
```
启动
pnpm dev
```
dev: runs next dev to start Next.js in development mode.
build: runs next build to build the application for production usage.
start: runs next start to start a Next.js production server.
lint: runs next lint to set up Next.js' built-in ESLint configuration.
```
##### npx 与 npm 有什么区别？

1.npx 是 npm 中的一部分，主要用于解决本地安装的包中 cli 命令，能在本地运行，无需再手动配置环境变量。它运行本地命令的原理：a.本地安装的包中的 cli 命令都统一加入到 node_modules 中的.bin 目录中。b.使用 npx 运行命令时，会从.bin 目录中查找。对于不存在的指令，npx 支持临时下载包到内存中临时使用此包中的指令，使用完则会释放内存。(总结：npx 用于运行本地安装包中的指令的)

2.npm 是对包进行管理的，进行包的下载、删除、更新、查询等操作的。npm 主要由两部分组成，一部分就是 npmregistry，另一部分 npmcli。npmregistry 存储着几乎所有的包，npmcli 是管理包的方式。再就是 npm 官网。npm 支持全局安装以及本地安装。全局安装的包，可以直接运行包中的命令行指令，因为 npm 在安装时默认配置了环境变量。

##### 清理依赖
清除node_modules
```
npx npkill
```
安装所有依赖
```
npm install
```