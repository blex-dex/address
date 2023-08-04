## VaultReward Contract: Buy/sell BLP in Rewards page; view, receive rewards and other feature contracts

### 1. getAPR: get annual interest rate
```
function getAPR() external view returns (uint256)
```
### 2. priceDecimals: This function retrieves the number of decimal places used for price values by calling the priceDecimals function of the vaultRouter contract.
```
    /**
     * @dev This function retrieves the number of decimal places used for price values by calling the priceDecimals function of the vaultRouter contract.
     * It does not take any parameters.
     * @return decimals The number of decimal places used for price values.
     */
    function priceDecimals() public view returns (uint256)
```
### 3. getLPPrice: retrieve the current price of LP tokens in the current market.
```
    /**
     * @dev This function allows anyone to retrieve the current price of LP tokens in the current market.
     * The function calls the `getLPPrice` function of the `vaultRouter` contract, passing in the address of the `coreVault` contract.
     * The `getLPPrice` function returns the current price of LP tokens in the market, which is then returned by this function as a `uint256`.
     * @return The current price of LP tokens in the market as a `uint256`.
     */
    function getLPPrice() public view returns (uint256)
```
### 4. getAUM: retrieve the current assets under management (AUM) of the market.
```
    /**
     * @dev This function allows anyone to retrieve the current assets under management (AUM) of the market.
     * The function calls the `getAUM` function of the `vaultRouter` contract, which returns the current AUM of the market as a `uint256`.
     * The AUM represents the total value of assets held in the market, including both the LP tokens and any other tokens held by the market.
     * @return The current AUM of the market as a `uint256`.
     */
    function getAUM() public view returns (uint256)
```
### 5. getLPReward: This function allows an LP (liquidity provider) to view the amount of rewards they have earned in the current market.
```
    /**
     * @dev This function allows an LP (liquidity provider) to view the amount of rewards they have earned in the current market.
     * The function uses the `msg.sender` parameter to look up the earned rewards for the calling account in the `lpEarnedRewards` mapping.
     * The function returns the amount of rewards earned by the calling account as a `uint256`.
     * @return The amount of rewards earned by the calling account as a `uint256`.
     */
    function getLPReward() public view returns (uint256)
```
### 6. getUSDBalance: retrieves the USD balance of the contract calling the function, by calling the getUSDBalance function of the vaultRouter contract.
```
    /**
     * @dev This function retrieves the USD balance of the contract calling the function, by calling the getUSDBalance function of the vaultRouter contract.
     * It does not take any parameters.
     * @return balance The USD balance of the contract calling the function.
     */
    function getUSDBalance() public view returns (uint256)
```
### 7. buyLpFee: retrieve the fee required to buy LP tokens in a market.
```
    /**
     * @dev This function is part of an interface and is used to retrieve the fee required to buy LP tokens in a market.
     * The function takes in a `CoreVault` parameter representing the CoreVault contract of the market being queried.
     * The function calls the `buyLpFee` function of the `vault` parameter, which returns the fee required to buy LP tokens in the market as a `uint256`.
     * @param vault The `CoreVault` contract of the market being queried.
     * @return The fee required to buy LP tokens in the market as a `uint256`.
     */
    function buyLpFee(ICoreVault vault) public view returns (uint256)
```
### 8. sellLpFee: retrieves the sell LP fee of a CoreVault contract, by calling the sellLpFee function of the specified CoreVault contract passed as a parameter.
```
    /**
     * @dev This function retrieves the sell LP fee of a CoreVault contract, by calling the sellLpFee function of the specified CoreVault contract passed as a parameter.
     * @param vault The CoreVault contract from which the sell LP fee is retrieved.
     * @return fee The sell LP fee of the specified CoreVault contract.
     */
    function sellLpFee(ICoreVault vault) public view returns (uint256) {
        return vault.sellLpFee();
    }
```
### 9. previewDeposit: When buying a BLP, the contract calculates how much BLP you get when the value of the Pay USDC input box changes
```
    /** @dev See {IERC4626-previewDeposit}. */
    function previewDeposit(uint256 assets) external view returns (uint256)
```
### 10. previewMint: When you buy a BLP, the contract calculates how much USDC you get when the Receive BLP input field changes
```
 /** @dev See {IERC4626-previewMint}. */
    function previewMint(uint256 shares) external view returns (uint256)
```
### 11. previewWithdraw: When a BLP is sold, the contract calculates how much USDC you get when the Receive BLP input field changes
```
/** @dev See {IERC4626-previewWithdraw}. */
    function previewWithdraw(uint256 assets) external view returns (uint256)
```
### 12. previewRedeem: When selling BLP, the contract calculates how much BLP you get when the value of the Pay USDC input box changes
```
/** @dev See {IERC4626-previewRedeem}. */
    function previewRedeem(uint256 shares) external view returns (uint256)
```
### 13. coreVault: get coreVault contract address
```
function coreVault() public view
```
----------------------------------------------------------------
### 14. buy: used to buy shares in a vault using an ERC20 asset as payment.
```
const { ethers } = require("ethers");
const sleep = (delay) => new Promise((resolve) => setTimeout(resolve, delay))
const url = ""
const provider = new ethers.providers.JsonRpcProvider(url);
const signer = await provider.getSigner()

async function testVaultReward() {
    const erc20ABI = [];
    const vaultRewardABI = []
    const vaultAddress = "0x2ACc5adB8584EAcbFe133142BDc31480b7B6a311"
    const vaultRewardAddress = "0x6FEca459A8D57F6782fA46A9B56547101E984cc8"
    const erc20Address = "0x4811Bc0598f1ff7C3E92a8a26ff50Ab450a6d64B"

    const erc20 = new ethers.Contract(erc20Address, erc20ABI, signer);
    const vaultReward = new ethers.Contract(vaultRewardAddress, vaultRewardABI, signer);

    let tx = await erc20.approve(vaultRewardAddress, ethers.utils.parseUnits(100000000+'', 18))
    await tx.wait()

    tx = await vaultReward.buy(vaultAddress, signer.getAddress(), ethers.utils.parseUnits(1000000+'',18), 0)
    await tx.wait()
}
```
```
    /**
     * @dev This function is used to buy shares in a vault using an ERC20 asset as payment.
     * @param vault The address of the vault.
     * @param to The address where the purchased shares will be sent.
     * @param amount The amount of ERC20 tokens to use for purchasing the shares.
     * @param minSharesOut The minimum number of shares that the buyer expects to receive for their payment.
     * @return sharesOut The actual number of shares purchased by the buyer.
     */
    function buy(
        IERC4626 vault,
        address to,
        uint256 amount,
        uint256 minSharesOut
    ) public nonReentrant returns (uint256 sharesOut)
```
### 15. sell: sells a specified amount of shares in a given vault on behalf of the caller using the `vaultReward` contract.
```
const { ethers } = require("ethers");
const sleep = (delay) => new Promise((resolve) => setTimeout(resolve, delay))
const url = ""
const provider = new ethers.providers.JsonRpcProvider(url);
const signer = await provider.getSigner()

async function testVaultReward() {
    const erc20ABI = [];
    const vaultRewardABI = []
    const vaultAddress = "0x2ACc5adB8584EAcbFe133142BDc31480b7B6a311"
    const vaultRewardAddress = "0x6FEca459A8D57F6782fA46A9B56547101E984cc8"
    const erc20Address = "0x4811Bc0598f1ff7C3E92a8a26ff50Ab450a6d64B"

    const erc20 = new ethers.Contract(erc20Address, erc20ABI, signer);
    const vaultReward = new ethers.Contract(vaultRewardAddress, vaultRewardABI, signer);

    let tx = await erc20.approve(vaultRewardAddress, ethers.utils.parseUnits(100000000+'', 18))
    await tx.wait()

    tx = await vaultReward.buy(vaultAddress, signer.getAddress(), ethers.utils.parseUnits(1000000+'',18), 0)
    await tx.wait()

    await sleep(20 * 60)  //wait 20 minutes

    tx = await vaultReward.sell(vaultAddress, signer.getAddress(), ethers.utils.parseUnits(1000000+'',18), 0)
    await tx.wait()

}
```
```
    /**
     * @dev This function sells a specified amount of shares in a given vault on behalf of the caller using the `vaultReward` contract.
     * The `to` address receives the resulting assets of the sale.
     * @param vault The address of the vault to sell assets from.
     * @param to The address that receives the resulting shares of the sale.
     * @param shares The amount of shares to sell.
     * @param minAssetsOut The minimum amount of assets the caller expects to receive from the sale.
     * @return assetOut The resulting number of shares received by the `to` address.
     */
    function sell(
        IERC4626 vault,
        address to,
        uint256 shares,
        uint256 minAssetsOut
    ) public nonReentrant returns (uint256 assetOut)
```
### 16. claimLPReward: This function allows an LP (liquidity provider) to claim their rewards in the current market
```
const { ethers } = require("ethers");
const sleep = (delay) => new Promise((resolve) => setTimeout(resolve, delay))
const url = ""
const provider = new ethers.providers.JsonRpcProvider(url);
const signer = await provider.getSigner()

async function testclaimLPReward() {
    const erc20ABI = [];
    const vaultRewardABI = []
    const vaultAddress = "0x2ACc5adB8584EAcbFe133142BDc31480b7B6a311"
    const vaultRewardAddress = "0x6FEca459A8D57F6782fA46A9B56547101E984cc8"
    const erc20Address = "0x4811Bc0598f1ff7C3E92a8a26ff50Ab450a6d64B"

    const erc20 = new ethers.Contract(erc20Address, erc20ABI, signer);
    const vaultReward = new ethers.Contract(vaultRewardAddress, vaultRewardABI, signer);

    let tx = await erc20.approve(vaultRewardAddress, ethers.utils.parseUnits(100000000+'', 18))
    await tx.wait()

    tx = await vaultReward.buy(vaultAddress, signer.getAddress(), ethers.utils.parseUnits(1000000+'',18), 0)
    await tx.wait()

    tx = await vaultReward.claimLPReward()
    await tx.wait()
}
```
```
    /**
     * @dev This function allows an LP (liquidity provider) to claim their rewards in the current market.
     * The function first checks that the LP has a non-zero balance in the CoreVault contract.
     * If the LP has a non-zero balance, the function calls the `pendingRewards` function to calculate the amount of
     * rewards the LP is entitled to. The LP's earned rewards are then stored in the `lpEarnedRewards` mapping.
     * Finally, the `transferFromVault` function of the `vaultRouter` contract is called to transfer the rewards
     * from the market's vault to the LP's account.
     */
    function claimLPReward() public nonReentrant
```