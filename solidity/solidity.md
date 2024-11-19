# Solidity

## 部署
```


```

```

# default values
uint public ui; //0
int public i; // 0
bool public b; // false
address public addr; // 0x0000000000000000000000000000000000000000
bytes32 public by; // 0x0000000000000000000000000000000000000000000000000000000000000000

# array
uint[] public nums = [1,2,3];
uint[3] public fixedNums = [4,5,6];
uint[] memory arr = new uint[](4);

# mapping
mapping(address => uint) public balances;
balances[address(0)] = 1;

# constant
address public constant MY_ADDR =  address(0);

# enum
enum OrderStatus {None, Pending, Shipped, Completed, Rejected, Cancelled }

# event
event Transfer(address indexed from, address indexed to, uint256 value);
emit Transfer(address(0), address(0), 1);

# constructor
contract ConstructorTest {
    address public owner;
    uint public ui;
    constructor(uint _ui) {
        owner = msg.sender;
        ui = _ui;
    }
}

# immutable
address public immutable owner;

```
##### error
```
contract ErrorTest {
    uint public ui = 1;
    error MyErr(address addr, uint i);
    function testRequire(uint i) external pure  {
        require(i <= 5, "i greater than 5");
    }
    function testRevert(uint i) external pure  {
        if (i > 5) {
            revert("i greater than 5");
        }
    }
    function testCustomError(uint i) external view  {
        if (i > 5) {
            revert MyErr(msg.sender, i);
        }
    }
    function testAssert() external view {
        assert(ui == 1);
    }
    function testChangeStateVar() external  {
        ui += 1;
    }
}
```

##### struct
```
contract StructTest {
    struct Vehicle{
        string make;
        uint year;
        address owner;
    }
    function test() public  {
        Vehicle memory v1 = Vehicle("a", 1, address(1));
        Vehicle memory v2 = Vehicle({year: 2, make: "b", owner: address(2)});
        Vehicle memory v3 ;
        v3.make = "c";
        v3.year = 3;
        v3.owner = address(3);
    }
```

##### visibility
private 私有
public 外部和内部均可调用
internal 内部和子类
external 外部
```
contract Base {
    uint private pri;
    uint public pub;
    uint internal inter;
    
    function privateFunc() private view  {
        pri+pub+inter;
    }
    function publicFunc() public view {
        pri+pub+inter;
    }
    function externalFunc () external view {
        pri+pub+inter;
    }
    function internalFunc() internal view {
        pri+pub+inter;
    }
    function testBase() public view {
        privateFunc();
        publicFunc();
        // gas 高 禁止这么做
        // this.externalFunc();
        internalFunc();
    }
}
contract Child is Base {
    function test() public view {
        super.publicFunc();
        super.internalFunc();
        pub+inter;
    }
}
```

##### inheritance, parent constructor
```
contract S {
    string public name;
    event LogS(string message);
    constructor(string memory _name) {
        emit LogS("S");
        name = _name;
    }
}
contract T {
    string public text;
    event LogT(string message);
    constructor(string memory _text) {
        emit LogT("T");
        text = _text;
    }
}
contract U is S,T {
    constructor(string memory _name, string memory _text) S(_name) T(_text) {}
}
contract BB is S("s"),T {
    constructor(string memory _text) T(_text){}
}
contract B0 is S, T {
    constructor(string memory _name, string memory _text) S(_name) T(_text) { }
}
contract B2 is T, S {
    constructor(string memory _name, string memory _text) S(_name) T(_text) {}
}
```
##### parent function
```
contract A {
    event Log(string message);
    function foo() public  virtual  {
        emit Log("A.foo");
    }
    function bar() public  virtual  {
        emit Log("A.bar");
    }
}
contract B is A {
    function foo() public override virtual  {
        emit Log("B.foo");
        A.foo();
    }
    function bar() public override  virtual  {
        emit Log("B.bar");
        super.bar();
    }
}
```

##### modifier
```
contract MyOwnable {
    address public owner;
    uint public count;
    constructor() {
        owner = msg.sender;
    }
    modifier onlyOwner() {
        require(msg.sender == owner, "not owner");
        _;
    }
    function transferOwnership(address newOwner) external onlyOwner {
        require(newOwner != address(0), "invalid owner");
        owner = newOwner;
    }
}
```
##### pure and view 

##### function output
```
contract FunctionOutputs {
    uint public ui;
    bool public b;
    string public str;
    function returnMultiple() public pure returns(uint, bool, string memory) {
        return (1, true, "test");
    }
    function captureOutputs() external {
        (ui, b, str) = returnMultiple();
    }
}
```

##### storage memory calldata
```
contract StorageMemoryCalldata {
    struct Demo{
        uint[]  arr;
        string str;
    }
    mapping(address => Demo) myMap;

    function updateDemo(uint[] calldata carr) external   {
        uint[] memory arr = new uint[](1);
        arr[0] = 1;
        Demo memory demo = Demo(arr, "test");
        myMap[msg.sender] = demo;
        modifyStr("ok");
        inter(carr);
        assert(keccak256(abi.encodePacked(myMap[msg.sender].str)) == keccak256(abi.encodePacked("ok")));
    }
    function modifyStr(string memory _s) private  {
        Demo storage demo = myMap[msg.sender];
        demo.str = _s;
    }
    function inter(uint[] calldata _arr) public pure returns(uint[] calldata) {
       return _arr;
    }
}
```
##### call other contract
```
contract MyCallerContract {
    function setTargetX(MyTargetContract _c, uint _x) external  {
        _c.setX(_x);
    }
    function setTargetX2(address _addr, uint _x) external  {
        MyTargetContract(_addr).setX(_x);
    }
    function setXWithEther(MyTargetContract _c, uint _x) external payable  {
        _c.setXAndReceiveEther{value: msg.value}(_x);
    }
}
contract MyTargetContract {
    uint public x;
    uint public value;
    function setX(uint _x) public  {
        x = _x;
    }
    function setXAndReceiveEther(uint _x) public payable  {
        x = _x;
        value = msg.value;
    }
}

```

##### encode and decode data
```
contract AbiDecode {
    struct MyStruct{
        string name;
        uint[2] numbers;
    }
    function encodeData(uint x, address addr, uint[] calldata arr, MyStruct calldata myStruct) external pure returns(bytes memory) {
        return abi.encode(x, addr, arr,  myStruct);
    }
    function decodeData(bytes calldata data) external pure returns(uint x, address addr, uint[] memory arr, MyStruct memory myStruct) {
        (x, addr, arr, myStruct) = abi.decode(data, (uint, address, uint[], MyStruct));
    }
}
```

##### function selector
msg.data = selector + param1 + param2
data前4字节为function selector，即前8位16进制
function selector 计算方式如下，调用示例 getSelector("transfer(address,uint256)");
```
contract FunctionSelector {
    function getSelector(string calldata _func) external pure returns (bytes4) {
        return bytes4(keccak256(bytes(_func)));
    }
}
contract Reciever {
    event Log(bytes data);
    function transfer(address _to, uint amount) external {
        emit Log(msg.data);
    }

}
```
##### 3 ways to encode function data

```
interface IERC20 {
    function transfer(address to, uint amount) external;
}
contract Token is IERC20{
    function transfer(address to, uint amount) external  {}
}
contract EncodeData {
    function test(address _contract, bytes calldata _data) external returns (bool ok) {
        ( ok, ) = _contract.call(_data);
        require(ok, "call failed");
    }
    function encodeWithSignature(address to, uint256 amount) external pure returns (bytes memory) {
        return abi.encodeWithSignature("transfer(address,uint256)", to, amount);
    }
    function encodeWithSelector(address to, uint256 amount) external pure returns (bytes memory)  {
        return abi.encodeWithSelector(IERC20.transfer.selector, to, amount);
    }
    function encodeCall(address to, uint256 amount) external pure returns (bytes memory)  {
        return abi.encodeCall(IERC20.transfer, (to,amount));
    }
}

```

##### send ether
1. to.send(123)
2. to.transfer(123)
3. to.call{value: 123}("")
```
contract SendEther {
    constructor() payable{}
    receive() external payable { }
    function sendByTransfer(address payable _to) external payable  {
        _to.transfer(123);
    }
    // 用的少
    function sendBySend(address payable _to) external payable  {
        bool res = _to.send(123);
        require(res, "send failed");
    }
    function sendByCall(address payable _to) external payable  {
        (bool res,) = _to.call{value: 123}("");
        require(res, "call failed");
    }
}
contract EthReciever {
    event Log(uint amount, uint gas);
    receive() external payable {
        emit Log(msg.value, gasleft());
    }
}
```
##### call
```
contract TestContract {
    string public  message;
    uint public num;
    event Log(string msg);
    function foo(string memory _msg, uint256 _num) external returns(bool, uint){
        message = _msg;
        num = _num;
        return (true, 555);
    }

    receive() external payable { }
    fallback() external  payable {
        emit Log("Fallback was called");
    }
}

contract Caller {
    bytes public data;
    function callFoo(address _testContract, string memory _msg, uint256 _num) external payable  {
        // encodeWithSignature 方法签名参数逗号分隔不能有空格，uint必须写为uint256
        (bool res, bytes memory _data) = _testContract.call{value: msg.value, gas: 20000}(abi.encodeWithSignature("foo(string,uint256)", _msg, _num));
        require(res, "call failed");
        data = _data;
        (bool b, uint ui) = abi.decode(data, (bool, uint256));
        assert(b);
        assert(ui == 555);
    }
    function callNonExistentFunction(address _testContract) external  {
        (bool res,) = _testContract.call(abi.encodeWithSignature("afunc()"));
        require(res, "call failed");
    }
}

```
##### delegatecall
```
contract Callee {
    uint public num;
    // 与caller变量定义和顺序一致，如果添加caller不需要的变量，只能在后面添加
    function setNum(uint _num) public payable  {
        num = _num;
    }
}
contract Caller {
    uint public num;
    function deleteCall(address _callee, uint _num) public  {
        // (bool res, ) = _callee.call{value: msg.value}(abi.encodeWithSignature("setNum(uint256)", _num));
        (bool suc, ) = _callee.delegatecall(abi.encodeWithSelector(Callee.setNum.selector, _num));
        require(suc, "delegatecall failed");
    }
}
```
##### fallback and recieve
```
//              Ether
//       is msg.data empty?
//        Yes/          \ No
// receive() exists?      fallback()
//      Yes/ \ No
// receive()   fallback()

```

##### decimals convert

为了在 LlamaPay 合约中统一处理代币，我们需要将所有代币的精度标准化为 20 位。这可以通过以下公式实现：
DECIMALS_DIVISOR = 10**(20 - tokenDecimals);
DECIMALS_DIVISOR 是一个用于处理代币小数位数的除数。通过以上计算，我们可以将代币的小数位数转换为 20 位的精度，使得在合约中处理不同精度的代币变得更加简单和一致。例如，如果代币有 18 位小数，这意味着我们将代币的最小单位乘以 100，使得其精度达到 20 位，同样地，如果代币有 6 位小数，则乘以 10^14：
// ETH‘s decimal is 18
DECIMALS_DIVISOR = 10**(20 - 18) = 10^2 = 100;

// USDC's decimal is 6
DECIMALS_DIVISOR = 10**(20 - 6) = 10^14;

