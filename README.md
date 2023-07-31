# Description: Includes the ABI and address description of each file

## fantom_4002.json: fantom contract's addresses
```
{
    "ETH": "0x62CAe0FA2da220f43a51F86Db2EDb36DcA9A5A08",            //ETH address
    "BTC": "0x6550bc2301936011c1334555e62A87705A81C12C",            //BTC address
    "LINK": "0xC112E008e88CE6c35a9afebaA31cd6706d06E36A",           //LINK address
    "GmxPriceFeed": "0x",                                           
    "BTCPriceFeed": "0x65E8d79f3e8e36fE48eC31A2ae935e92F5bBF529",   //BTCPriceFeed address
    "ETHPriceFeed": "0xB8C458C957a6e6ca7Cc53eD95bEA548c52AFaA24",   //ETHPriceFeed address
    "USDT": "0x4811Bc0598f1ff7C3E92a8a26ff50Ab450a6d64B",           //USDT contract address
    "USDC": "0x4811Bc0598f1ff7C3E92a8a26ff50Ab450a6d64B",           //USDC contract address
    "----------": "-------------------",
    "GlobalValid": "0xE1Ede12e794bDf4991d826d48F18aFEbc65A57bA",    //GlobalValid address
    "GlobalValid_block": 18698166,
    "CoreVault": "0x2ACc5adB8584EAcbFe133142BDc31480b7B6a311",      //CoreVault address
    "CoreVaultImpl": "0x7038EcE4F69db25E52d12fce6e028446674Dc2e0",  //CoreVaultImpl address
    "CoreVault_block": 18698174,
    "VaultRouter": "0xea6764Cd9B2bCa7CCf07F4942D18351293070F38",    //VaultRouter address
    "VaultRouterImpl": "0x4145bE5F42FbDb5F45e0a35c65f83E069A98E6eC",//VaultRouterImpl address
    "VaultRouter_block": 18698181,
    "VaultReward": "0x6FEca459A8D57F6782fA46A9B56547101E984cc8",    //VaultReward
    "VaultRewardImpl": "0x59F652d2844a698Bd7D5C2b5a5108e18E9050AAf",//VaultRewardImpl address
    "VaultReward_block": 18698192,
    "RewardDistributor": "0x73b836C9bC17A93F9088D9e56483FfC572f69752",//RewardDistributor address
    "RewardDistributor_block": 18698194,
    "MarketFactory": "0x3aE8Bb55CBC8f6Ca06A9eb6192c3F2A7E554A887",   //MarketFactory address
    "MarketFactory_block": 18698202,
    "MarketRouter": "0x7B934d8d5b61E9F08aE1e09Ae4464f42eA380feb",    //MarketRouter address
    "MarketRouterImpl": "0xCfE822a4E702b7f74800C3EFf8d7172B69401dA3",//MarketRouterImpl address
    "MarketRouter_block": 18698223,
    "MarketReader": "0x509D21fCe01DcC272980E167EA9FB6594F2d65a5",    //MarketReader address
    "MarketReader_block": 18698229,
    "PositionAddMgr": "0xa241Cff91C5bd40C3f1B2eDF425b7375AB16d196",  //PositionAddMgr address
    "PositionAddMgr_block": 18698237,
    "PositionSubMgr": "0x3FD0Bc669f2F3395942D21dE5c41a1cAe54E3A27",  //PositionSubMgr address
    "PositionSubMgr_block": 18698247,
    "OrderMgr": "0x9d62C6869Ce96A723bBD1A96c84b0d4306584D0c",        //OrderMgr address
    "OrderMgr_block": 18698257,
    "FeeVault": "0x9F05E8E83B887634434eeB5bB35Bc16837005FEF",        //FeeVault address
    "FeeVault_block": 18698264,
    "FundFee": "0x9348BDf5fbA1b5c56ba0214efAF35a1CF1F4E27A",         //FundFee address
    "FundFee_block": 18698273,
    "FeeRouter": "0x9a4BB7ED7e8A0557e98baB025C1e3E0bAD96ff1f",       //FeeRouter address
    "FeeRouter_block": 18698279,
    "ChainPriceFeed": "0x1Fdc21af4E87483650454F97781498de84204D94",  //ChainPriceFeed address
    "ChainPriceFeed_block": 18698316,
    "FastPriceFeed": "0xAa98Bd4996beF30772B080c4e9Fa78a414E56968",   //FastPriceFeed address
    "FastPriceFeed_block": 18698325,
    "Price": "0xd584c8bF0664E643fd7e1bDaeAe5891A587A672d",           //Price address
    "Price_block": 18698332,
    "Referral": "0x8A31e1068ddac6b5dD44794fbC41dC9Dc92EdDF0",        //Referral address
    "Referral_block": 18698434,
    "AutoManager": "0x7A8e25202F7c3d50415AA51CbEc25EEC01B120F0",     //AutoManager address
    "AutoManager_block": 18698440
}
```

## FeeRouter.json:
### 1.Get feeVault contract address
```
function feeVault() external view returns ( //Get feeVault contract address
    address //feeVault contract address
    );
```
### 2.Get fundFee contract address
```
function fundFee() external view returns (
    address //fundFee contract address
    );
```
### 3.Get FEE RATE PRECISION
```
function FEE_RATE_PRECISION() external view returns (
    uint256 //FEE_RATE_PRECISION
    );
```
### 4.Get market's feeRate and fee
```
function feeAndRates(
        address market, //market address
        uint8 kind      //kind
    ) external view returns (
    uint256 //market's feeRate and fee
    );
```
### 5.set market fee and rates
```
function setFeeAndRates(
    address market,         //market address
    uint256[] memory rates  //market rates
    ) external;
```
### 6.FeeVault withdraw
```
function withdraw(
    address token,  //token address
    address to,     //receiver
    uint256 amount  //amount
    ) external;
```
### 7.Get Exec Fee
```
function getExecFee(
    address market              //market address
    ) external view returns (
    uint256                     //fee amount
    );
```
### 8.getAccountFees
```
function getAccountFees(
    address account             //user account address
    ) external view returns (
    uint256                     //fees
    );
```
### 9.getFundingRate
```
function getFundingRate(
        address market,
        uint256 longSize,
        uint256 shortSize,
        bool isLong
    ) external view returns (
    int256
    );
```
### 10.cumulativeFundingRates
```
function cumulativeFundingRates(
        address market,     //market address
        bool isLong         //long or not
    ) external view returns (
    int256                  //rates
    );
```
### 11.updateCumulativeFundingRate
```
function updateCumulativeFundingRate(
        address market,         //market address
        uint256 longSize,       //longSize
        uint256 shortSize       //shortSize
    ) external;
```
### 12.getOrderFees
```
function getOrderFees(
        MarketDataTypes.UpdateOrderInputs memory params
    ) external view returns (int256 fees);
```
```
struct UpdateOrderInputs {
        address _market;        //market address
        bool _isLong;           //long or not
        uint256 _oraclePrice;   //oraclePrice
        bool isOpen;            //open or not
        bool isCreate;          //create or not
        //===========
        Order.Props _order;     //order
        uint256[] inputs; // uint256 pay; bool isFromMarket; uint256 _slippage;
}

struct Props {
        uint8 version;
        uint32 updatedAtBlock;  
        uint8 triggerAbove;
        address account;
        uint48 extra3; // close: isKeepLev
        uint128 collateral;
        // open:pay; close:collateralDelta

        uint128 size;
        uint128 price;
        uint128 extra1; // open:tp
        uint64 orderID;
        uint64 extra2; //close: order to order id
        // 
        uint128 extra0; // open:sl; close:from order  
        bytes32 refCode; //160
        //96 todo uint96 extra4;
}
```
### 13.getFees
```
function getFees(
        MarketDataTypes.UpdatePositionInputs memory params,
        Position.Props memory position
    ) external view returns (int256[] memory);
```
```
struct UpdatePositionInputs {
        address _market;        //market address
        bool _isLong;           //long or not
        uint256 _oraclePrice;
        bool isOpen;
        //===========
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
        uint256[] inputs; //0: tp, isKeepLev; 1: sl
    }

struct Props {
        address market;
        bool isLong;
        uint32 lastTime;
        uint216 extra3;
        uint256 size;
        uint256 collateral;
        uint256 averagePrice;
        int256 entryFundingRate;
        int256 realisedPnl;
        uint256 extra0;
        uint256 extra1;
        uint256 extra2;
    }
```
### 14.collectFees
```
function collectFees(
        address account,        //user account
        address token,          //token address
        int256[] memory fees    //fees array
    ) external;
```
### 15.getGlobalFees
```
function getGlobalFees() external view returns (
    int256 total        //fees
);
```

## MarketReader.json: MarketReader contract's ABI file
### 1.Get market related configurations and parameters (trade pair details)
```
function getMarket( address marketAddr)
```
### Data definition
```
struct ValidOuts {
    uint256 minSlippage; // return 1
    uint256 maxSlippage; // return 300
    uint256 slippageDigits;//The denominator of the slippage
    uint256 minLev;//return 2
    uint256 maxLev;//return 100
    uint256 minCollateral;//rturn 5 * 10^tokenDigits
    uint256 maxTradeAmount;//return 10 * 10^tokenDigits
    bool allowOpen;
    bool allowClose;
}

struct MarketOuts {
    uint256 tokenDigits; // return 18
    uint256 liquidationFeeUsd;//The unit is US dollars.
    uint256 spread;//Unit is up in the air
    address indexToken;
    address collateralToken;
    address vault;
    address marketAddressesProvider;
    address orderBookLong;
    address orderBookShort;
    address positionBook;
}
struct FeeOuts{
    uint256 closeFeeRate; // It's in billions, parts per billion x, with an accuracy of 10^8
    uint256 openFeeRate; // same
    uint256 execFee; // x * 10^tokenDigits
    uint256 liquidateFee; // x * 10^tokendits
    uint256 precision; // 10^8
}

```
### return value
```
returns (ValidOuts memory validOuts, MarketOuts memory mktOuts)
```

### 2.Get the Funds rate (in the MarketReader contract)
```
function getFundingRate(address marketAddress, bool isLong)
 return {
    int256, // Current capital rate
    int256  // Overall total fund rate
    } 
```

### 3.Get the funds fee for the corresponding position (in the MarketReader contract)
```
function getFundingFee(
    address account,
    address market,
    bool isLong
)  
return {
    int256
}
```

### 4.Get user expense statistics
```
function getUserFee(
  address _mkt,// Market address
  address _user//User wallet address
) 
returns (
  UserFeeOuts memory _outs
);
```
```
struct UserFeeOuts {
  uint256 openFee;//Users accumulated opening/adding warehouse charges
  uint256 closeFee;//User accumulated closing/reducing expenses
  int256 fundFee;//Users pay cumulative capital charges (plus or minus, possibly negative, i.e. users receive money, not pay)
  uint256 liquidateFee;//User accumulated clearing costs
  uint256 execFee;//User accumulated execution costs
}
```

### 5.Gets the maximum position size that a user can open in a given market (in a MarketReader contract)

```
    function availableLiquidity(
        address _market,  // markt address
        address _account, // user address
        bool _isLong      // Long/short
    ) external view returns (uint256) // Returns the maximum position size that can be opened
```

### 6.Get positions
```
function getPositions(
    address account,
    address market
)
return [{
    isLong // Long or not
    size, // size
    collateral, // collateral
    averagePrice, // Average open position price
    fundingFee, // Fund rate at the time of entry (with symbol)
    realisedPnl, // Realized profit or loss (unsigned)
    hasProfit, // Whether there is profit (Boolean value)
    position.lastTime // Last modified time
}]
```

## MarketRouter.json: MarketRouter contract's ABI file

### 1.update PositionBook address
```
function updatePositionBook(
    address newA        //new address
    ) external;
```
### 2.Get vaultRouter contract address
```
function vaultRouter() external view returns (address);
```
### 3.getGlobalSize
```
function getGlobalSize()
        external
        view
        returns (
            uint256 sizesLong, //long size
            uint256 sizesShort //short size
        );
```
### 4.get account's size
```
function getAccountSize(
        address account         //account address
    ) external view returns (
        uint256 sizesL,         //long size
        uint256 sizesS          //short size
    );

```
### 5.add market
```
function addMarket(
    address         //market address
    ) external;
```
### 6.remove market
```
function removeMarket(
    address         //market address
) external;
```
### 7.validateIncreasePosition
```
function validateIncreasePosition(
        MarketDataTypes.UpdatePositionInputs memory _inputs
    ) external view;
```
```
struct UpdatePositionInputs {
        address _market;         //market address
        bool _isLong;            //long or not
        uint256 _oraclePrice;
        bool isOpen;
        //===========
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
        uint256[] inputs; //0: tp, isKeepLev; 1: sl
    }
```

## Referral.json: Referral contract's ABI file

### 1.Get code's owners
```
function codeOwners(
    bytes32 _code       //referral code
) external view returns (
    address             //code's owner address
);
```
### 2.Get trader Referral Codes
```
function traderReferralCodes(
        address _account           //account address
    ) external view returns (
    bytes32                         //codes
    );
```
### 3.Get referrer Discount Shares
```
function referrerDiscountShares(
        address _account        //account address
    ) external view returns (
    uint256                     //shares
    );
```
### 4.Get referrer Tiers
```
 function referrerTiers(
    address _account    //account address
 ) external view returns (
    uint256             //tiers
 );
```
### 5.get Trader Referral code and referrer
```
function getTraderReferralInfo(
        address _account      //account address
    ) external view returns (
        bytes32,              //code
        address               //referrer address
    );
```
### 6.set Trader Referral Code
```
function setTraderReferralCode(
    address _account,   //account address
    bytes32 _code       //code
) external;
```
### 7.set tier
```
function setTier(
        uint256 _tierId,
        uint256 _totalRebate,
        uint256 _discountShare
    ) external;

```
### 8.set Referrer Tier
```
function setReferrerTier(
    address _referrer,  //referrer address
    uint256 _tierId     //tierId
) external;
```
### 9.Set code owner by gov
```
function govSetCodeOwner(
    bytes32 _code, 
    address _newAccount
) external;
```

## VaultReward.json: VaultReward contract's ABI file

### 1.update Rewards
```
function updateRewards() external;
```
### 2.buy
```
function buy(
        IERC4626 vault, //vault contract address
        address to,     //receiver
        uint256 amount, //amount
        uint256 minSharesOut 
    ) external returns (uint256); //out amount 
```
### 3.sell
```
function sell(
        IERC4626 vault,  //vault contract address
        address to,      //receiver
        uint256 amount,
        uint256 minAssetsOut
    ) external returns (uint256); //out amount
```
### 4.calim LP Reward
```
function calimLPReward() external;
```
### 5.get APR
```
function getAPR() external returns (uint256);
```
### 6.get AUM
```
function getAUM() external returns (uint256);
```
### 7.get LP Reward
```
function getLPReward() external returns (uint256);
```
### 8.pending Rewards
```
function pendingRewards() external returns (uint256);
```
### 9.Get price Decimals
```
function priceDecimals() external returns (uint256);
```
### 10.cacul buy Lp Fee
```
function buyLpFee(
    ICoreVault vault        //vault contract address
) external view returns (
    uint256                 //fee
);
```
### 11.cacul sell Lp fee
```
function sellLpFee(
    ICoreVault vault        //vault contract address
) external view returns (
    uint256                 //feee
    );
```