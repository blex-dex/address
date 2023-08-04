## MarketReader: Get market information related

### 1. getMarket: Retrieves information about a market, including its validation parameters, market parameters, and fee parameters.
```
     /**
     * @dev Retrieves information about a market, including its validation parameters, market parameters, and fee parameters.
     * @param _marketAddr Address of the market to retrieve information about.
     * @return validOuts Struct containing the validation parameters for the market.
     * @return mktOuts Struct containing the market parameters, such as token digits, fee rates, and order book and position book addresses.
     * @return feeOuts Struct containing the fee parameters, such as fee rates and fee precision.
     */
    function getMarket(
        address _marketAddr
    )
        external
        view
        returns (
            ValidOuts memory validOuts,
            MarketOuts memory mktOuts,
            FeeOuts memory feeOuts
        )
        
    struct ValidOuts {
        uint256 minSlippage;            //minimum slippage
        uint256 maxSlippage;            //maximum slippage
        uint256 slippageDigits;         //slippage digits
        uint256 minLev;                 //minimum Lev
        uint256 maxLev;                 //maximum Lev
        uint256 minCollateral;          //minimum collateral
        uint256 maxTradeAmount;         //maximum trade amount
        bool allowOpen;                 //allow open or not    
        bool allowClose;                //allow close or not
    }

    struct MarketOuts {
        uint256 tokenDigits;            //token digits
        uint256 closeFeeRate;           //close fee rate
        uint256 openFeeRate;            //open fee rate
        uint256 liquidationFeeUsd;      //liquidation of fee in usd
        uint256 spread;                 //spread
        address indexToken;             //token index
        address collateralToken;        //collateral token address
        address orderBookLong;          //long order book addrss
        address orderBookShort;         //short order book address
        address positionBook;           //position book address
    }

    struct FeeOuts {
        uint256 closeFeeRate;           //fee rate when close
        uint256 openFeeRate;            //fee rate when open
        uint256 execFee;                //fee of exec
        uint256 liquidateFee;           //fee of liquidate
        uint256 digits;                 //digits
    }
```
### 2. getMarkets: Get a list of supported markets
```
    /**
    * @dev This function returns an array of market information, including the market name, address, and whether the market allows opening and closing positions.
    * @return _outs An array of structures containing information about each market, including the name, address, and whether opening and closing positions are allowed.
    */
    function getMarkets()
        external
        view
        returns (IMarketFactory.Outs[] memory _outs)

    struct Outs {
        string name;                    //market name
        address addr;                   //market address
        bool allowOpen;                 //allow to open or not
        bool allowClose;                //allow to close or not
    }
```
### 3. getFundingRate: This function returns the current and cumulative funding rates of a market for a specified type of position.
```
    /**
     * @dev This function returns the current and cumulative funding rates of a market for a specified type of position.
     * @param _market The address of the market for which to retrieve the funding rates.
     * @param _isLong A boolean flag indicating whether the position type for which to retrieve the funding rates is a long position.
     * @return A tuple containing two int256 values: `nowRate` and `totalRate`.
     * `nowRate` is the current funding rate of the market for the specified position type, calculated using the formula provided by the `getFundingRate()` function of the associated `IFeeRouter` contract.
     * `totalRate` is the cumulative funding rate of the market for the specified position type, calculated using the cumulativeFundingRates() function of the associated `IFeeRouter` contract.
     */
    function getFundingRate(
        address _market,
        bool _isLong
    ) external view returns (int256, int256)
```
### 4. getFundingFee: This function retrieves the funding fee for a specific account's position in a given market.
```
    /**
     * @dev This function retrieves the funding fee for a specific account's position in a given market.
     * @param account The address of the account whose position the funding fee is being retrieved for.
     * @param market The address of the market in which the position exists.
     * @param isLong A boolean indicating whether the position is a long position.
     * @return The funding fee associated with the specified position.
     */
    function getFundingFee(
        address account,
        address market,
        bool isLong
    ) external view returns (int256)
```
### 5. getPositions: This function retrieves the positions of a given account in a market or in all markets if market address is not provided
```
    /**
     * @dev This function retrieves the positions of a given account in a market or in all markets if market address is not provided
     * @param account Address of the account whose positions are to be retrieved
     * @param market Optional address of the market. If provided, retrieves the positions in the specified market. If not provided, retrieves the positions in all markets
     * @return _positions Array of `Position.Props` structures representing the positions of the account in the specified market or in all markets
     */
    function getPositions(
        address account,
        address market
    ) external view returns (Position.Props[] memory _positions)

    struct Props {
        address market;                 //market address
        bool isLong;                    //long or short
        uint32 lastTime;                //the last time
        uint216 extra3;                 
        uint256 size;
        uint256 collateral;             //collateral token address
        uint256 averagePrice;           //the average price
        int256 entryFundingRate;        //funding rate
        int256 realisedPnl;             //the realised pnl
        uint256 extra0;
        uint256 extra1;
        uint256 extra2;
    }
```
### 6. availableLiquidity: This function calculates the available liquidity for a given account in a market.
```
    /**
     * @dev This function calculates the available liquidity for a given account in a market.
     * @param market Address of the market
     * @param account Address of the account for which the available liquidity is to be calculated
     * @param isLong Boolean indicating if the position to be calculated is long or short
     * @return The amount of available liquidity in the market denominated in the collateral token of the market
     */
    function availableLiquidity(
        address market,
        address account,
        bool isLong
    ) external view returns (uint256)
```