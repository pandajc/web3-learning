##### 官网
https://hardhat.org/

# hardhat
```
npm init
npm install --save-dev hardhat

npx hardhat init
npx hardhat compile
npx hardhat test
npx hardhat ignition deploy ./ignition/modules/Lock.ts
npx hardhat node
npx hardhat ignition deploy ./ignition/modules/Lock.ts --network localhost
npx hardhat ignition deploy ignition/modules/Apollo.ts --network localhost --reset

npm install -g ts-node
npm install --save-dev ts-node
ts-node --files

-g 全局安装
--save 等价于 -S，项目上线以后也需要用到的
--save-dev 等价于 -D ，只在开发阶段使用

以上两种方式都会在npm install 执行时把信息写入package.json中，--save会把依赖名称及版本号写入dependencies的属性下，--save-dev会写入devDependencies下
dependencies：运行时依赖
devDependencies：开发时依赖




#  get a list of all the deployment IDs that exist in the current project
npx hardhat ignition deployments

# check on the current status of a deployment,
npx hardhat ignition status chain-31337

npx hardhat ignition wipe deploymentId futureId


```