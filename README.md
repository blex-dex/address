![blex_image](./resource/blex_image.png "blex_image")
# BLEX
## Overview
BLEX is index price-feed based Decentralized Perpetual Exchange.It was born to enable users to deploy trading strategies without permission on the basis of controlling their funds and achieving low loss and high efficiency. At the same time, it also reduces redundant games and losses among users, and builds a decentralized trading network where all users focus on their respective fields…

## Items
| FileName         | Description                                          | Link                                   |
|------------------|------------------------------------------------------|----------------------------------------|
| fantom_4002.json | Fantom chain contract's addresses(chainName_chainId) |                                        |
| FeeRouter.json   | FeeRouter contract's ABI file                        |                                        |
| Referral.json    | Referral contract's ABI file                         |                                        |
| MarketReader.json| MarketReader contract's ABI file                     | [MarketReader](./docs/MarketReader.md) |
| MarketRouter.json| MarketRouter contract's ABI file                     | [MarketRouter](./docs/MarketRouter.md) |
| VaultReward.json | VaultReward contract's ABI file                      | [VaultReward](./docs/VaultReward.md)   |

- ### fantom_4002.json: Records the addresses of all contracts in the fantom chain(chainName_chainId)
- ### FeeRouter.json: FeeVault's external encapsulation is primarily used to participate in business calculations
- ### Referral.json: To improve the performance of the contract, the invitation code adopts the Hex structure and needs to be processed by the encapsulation functions encodeReferralCode and decodeReferralCode
- ### MarketReader.json: Get market information related
- ### MarketRouter.json: Current market core transactions related
- ### VaultReward.json: Buy/sell BLP in Rewards page; view, receive rewards and other feature contracts

## Demo
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