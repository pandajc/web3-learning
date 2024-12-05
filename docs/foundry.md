
##### 初始化
forge init hello_foundry

##### 编译
forge build

##### 测试
forge test

##### 安装
forge install transmissions11/solmate Openzeppelin/openzeppelin-contracts

##### 查看文件树
tree . -d -L 2


##### 部署
export PRIVATE_KEY=????
forge create NFT --rpc-url=$RPC_URL --private-key=$PRIVATE_KEY --constructor-args <name> <symbol>

forge create --rpc-url <your_rpc_url> \
    --constructor-args "ForgeUSD" "FUSD" 18 1000000000000000000000 \
    --private-key <your_private_key> \
    --etherscan-api-key <your_etherscan_api_key> \
    --verify \
    src/MyToken.sol:MyToken


##### 调用合约
cast send --rpc-url=$RPC_URL <contractAddress>  "mintTo(address)" <mintAddress> --private-key=$PRIVATE_KEY

cast call 模拟调用

##### 分叉
anvil --fork-url YOUR_ENDPOINT_URL --fork-block-number 19000000

##### 启动本地节点
anvil


##### 脚本
```
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

import {Script} from "forge-std/Script.sol";
import {NFT} from "../src/NFT.sol";

contract MyScript is Script {
    function run() external {
        uint256 deployerPrivateKey = vm.envUint("PRIVATE_KEY");
        vm.startBroadcast(deployerPrivateKey);

        NFT nft = new NFT("NFT_tutorial", "TUT", "baseUri");

        vm.stopBroadcast();
    }
}

```
##### 部署脚本
```
# To load the variables in the .env file
source .env

# To deploy and verify our contract
forge script --chain sepolia script/NFT.s.sol:MyScript --rpc-url $SEPOLIA_RPC_URL --broadcast --verify -vvvv

```


##### vscode配置
```
1. Remappings
run forge remappings > remappings.txt.
2. Dependencies
add the following to your .vscode/settings.json for the extension to find your dependencies:
{
  "solidity.packageDefaultDependenciesContractsDirectory": "src",
  "solidity.packageDefaultDependenciesDirectory": "lib"
}

3. Formatter
To enable the built-in formatter that comes with Foundry to automatically format your code on save, you can add the following settings to your .vscode/settings.json:

{
  "editor.formatOnSave": true,
  "[solidity]": {
    "editor.defaultFormatter": "JuanBlanco.solidity" 
  },
  "solidity.formatter": "forge",
  "solidity.monoRepoSupport": false
}

4. Solc Version
Finally, it is recommended to specify a Solidity compiler version:

"solidity.compileUsingRemoteVersion": "v0.8.17"
To get Foundry in line with the chosen version, add the following to your default profile in foundry.toml.

solc = "0.8.17"
```
