## MarketRouter Contract: Current market core transactions related

### 1. increasePosition: Increases the size of a position on a market with the specified inputs
```
const { ethers } = require("ethers");
const sleep = (delay) => new Promise((resolve) => setTimeout(resolve, delay))
const url = ""
const provider = new ethers.providers.JsonRpcProvider(url);
const signer = await provider.getSigner()

function addDecimals(num, decimals) {
  num = String(num);
  const zeros = ethers.utils.parseUnits("1", decimals); //_price
  if (num.indexOf(".") < 0) {
    return BN.from(num).mul(zeros);
  }
  const [left, right, ...rest] = num.split(".");
  const num1 = BN.from(left).mul(zeros);
  const right_de = decimals - right?.length;
  const zeros2 = ethers.utils.parseUnits("1", right_de);
  const num2 = BN.from(right).mul(zeros2);
  return num1.add(num2);
}

async function testincreasePosition() {
    const marketRouterABI = []
    const marketRouterAddress = "0x6FEca459A8D57F6782fA46A9B56547101E984cc8"
    const marketAddress = ""

    const marketRouter = new ethers.Contract(marketRouterAddress, marketRouterABI, signer);

    let inputs = {
        _market : marketAddress,
        _isLong : true,
        _oraclePrice : 0,
        isOpen : true,
        _account : signer.getAddress(),
        _sizeDelta : 1000000,
        _price : addDecimals(40000+'',30),
        _slippage : 30,
        _isExec : false,
        liqState : 0,
        _fromOrder : "order id",
        _refCode : ethers.utils.formatBytes32String("As123456"),
        collateralDelta : 1000000,
        execNum : 0,
        inputs : [0,0,0] //0: tp, isKeepLev; 1: sl
    }
    let tx = await marketRouter.increasePosition(inputs)
    await tx.wait()
}
```
```
    /**
     * @notice Increases the size of a position on a market with the specified inputs
     * @param _inputs Inputs for updating the position
     *        _inputs._market Address of the market
     *        _inputs._isLong Whether the position is long (true) or short (false)
     *        _inputs._oraclePrice Price of the oracle for the market
     *        _inputs.isOpen Whether the position is open (true) or closed (false)
     *        _inputs._account Address of the account to increase position for
     *        _inputs._sizeDelta Amount to increase the size of the position by
     *        _inputs._price Price at which to increase the position
     *        _inputs._slippage Maximum amount of slippage allowed in the price
     *        _inputs._isExec Whether this is an execution of a previous order or not
     *        _inputs.liqState Liquidation state of the position
     *        _inputs._fromOrder ID of the order from which the position was executed
     *        _inputs._refCode Reference code for the position
     *        _inputs.collateralDelta Amount of collateral to add or remove from the position
     *        _inputs.execNum Execution number of the position
     *        _inputs.inputs Additional inputs for updating the position
     */
    function increasePosition(
        MarketDataTypes.UpdatePositionInputs memory _inputs
    ) public nonReentrant
    
    struct UpdatePositionInputs {
        address _market;
        bool _isLong;
        uint256 _oraclePrice;
        bool isOpen;
        address _account;
        uint256 _sizeDelta;
        uint256 _price;
        uint256 _slippage;
        bool _isExec;
        uint8 liqState;
        uint64 _fromOrder;
        bytes32 _refCode;
        uint256 collateralDelta;
        uint8 execNum;
        uint256[] inputs;
    }
```
### 2. decreasePosition: Function to decrease the position in the market
```
const { ethers } = require("ethers");
const sleep = (delay) => new Promise((resolve) => setTimeout(resolve, delay))
const url = ""
const provider = new ethers.providers.JsonRpcProvider(url);
const signer = await provider.getSigner()

function addDecimals(num, decimals) {
  num = String(num);
  const zeros = ethers.utils.parseUnits("1", decimals); //_price
  if (num.indexOf(".") < 0) {
    return BN.from(num).mul(zeros);
  }
  const [left, right, ...rest] = num.split(".");
  const num1 = BN.from(left).mul(zeros);
  const right_de = decimals - right?.length;
  const zeros2 = ethers.utils.parseUnits("1", right_de);
  const num2 = BN.from(right).mul(zeros2);
  return num1.add(num2);
}

async function testDecreasePosition() {
    const marketRouterABI = []
    const marketRouterAddress = "0x6FEca459A8D57F6782fA46A9B56547101E984cc8"
    const marketAddress = ""

    const marketRouter = new ethers.Contract(marketRouterAddress, marketRouterABI, signer);

    let inputs = {
        _market : marketAddress,
        _isLong : true,
        _oraclePrice : 0,
        isOpen : true,
        _account : signer.getAddress(),
        _sizeDelta : 1000000,
        _price : addDecimals(40000+'',30),
        _slippage : 30,
        _isExec : false,
        liqState : 0,
        _fromOrder : "order id",
        _refCode : ethers.utils.formatBytes32String("As123456"),
        collateralDelta : 1000000,
        execNum : 0,
        inputs : [0,0,0] //0: tp, isKeepLev; 1: sl
    }
    let tx = await marketRouter.decreasePosition(inputs)
    await tx.wait()
}
```
```
    /**
     * @dev Function to decrease the position in the market
     * @param _vars Struct containing the inputs to update the position
     *  _vars._market Address of the market
     *  _vars._isLong Boolean indicating the direction of the position
     *  _vars._oraclePrice Price of the oracle used for the market
     *  _vars.isOpen Boolean indicating if the position is open or not
     *  _vars._account Address of the account associated with the position
     *  _vars._sizeDelta Change in size of the position
     *  _vars._price Price of the position
     *  _vars._slippage Maximum price slippage allowed
     *  _vars._isExec Boolean indicating if the order has been executed
     *  _vars.liqState Liquidation state of the position
     *  _vars._fromOrder Order ID from which the position is being decreased
     *  _vars._refCode Reference code associated with the position
     *  _vars.collateralDelta Change in the collateral associated with the position
     *  _vars.execNum Number of times the order has been executed
     *  _vars.inputs Array of additional inputs
     */
    function decreasePosition(
        MarketDataTypes.UpdatePositionInputs memory _vars
    ) external nonReentrant
    
    struct UpdatePositionInputs {
        address _market;
        bool _isLong;
        uint256 _oraclePrice;
        bool isOpen;
        address _account;
        uint256 _sizeDelta;
        uint256 _price;
        uint256 _slippage;
        bool _isExec;
        uint8 liqState;
        uint64 _fromOrder;
        bytes32 _refCode;
        uint256 collateralDelta;
        uint8 execNum;
        uint256[] inputs;
    }
```
### 3. updateOrder: Create/Updates an order in a market.
```
    /**
     * @dev Create/Updates an order in a market.
     * @param _vars MarketDataTypes.UpdateOrderInputs memory containing the inputs required to update the order
     * _vars._market Address of the market
     * _vars._isLong Boolean indicating if the order is long
     * _vars._oraclePrice Price of the oracle
     * _vars.isOpen Boolean indicating if the order is open
     * _vars.isCreate Boolean indicating if the order is being created
     * _vars._order Order.Props containing the properties of the order to be updated
     * _vars.inputs Array of additional inputs required to update the order
     */
    function updateOrder(
        MarketDataTypes.UpdateOrderInputs memory _vars
    ) external nonReentrant
    
    struct UpdateOrderInputs {
        address _market;
        bool _isLong;
        uint256 _oraclePrice;
        bool isOpen;
        bool isCreate;
        Order.Props _order;
        uint256[] inputs; // uint256 pay; bool isFromMarket; uint256 _slippage;
    }
```
### 4. cancelOrderList: Function to cancel a list of orders in a market
```
    /**
     * @dev Function to cancel a list of orders in a market
     * @param _markets Addresses of the market
     * @param _isIncreaseList Array of boolean values indicating if the orders are increase orders or not
     * @param _orderIDList Array of order IDs to be canceled
     * @param _isLongList Array of boolean values indicating the direction of the orders
     */
    function cancelOrderList(
        address[] memory _markets,
        bool[] memory _isIncreaseList,
        uint256[] memory _orderIDList,
        bool[] memory _isLongList
    ) external nonReentrant
```