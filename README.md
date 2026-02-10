# Sample Hardhat Project

This project demonstrates a basic Hardhat use case. It comes with a sample contract, a test for that contract, and a script that deploys that contract.

Try running some of the following tasks:

```shell
npx hardhat help
npx hardhat test
REPORT_GAS=true npx hardhat test
npx hardhat node
npx hardhat run scripts/deploy.js
```
# Example commands

Initialize the Hardhat project
Creates the project structure, sample contract, and configuration file.
```shell
npx hardhat
```
Compile the smart contracts
Compiles all Solidity files in the contracts folder.
```shell
npx hardhat compile
```
Start a local blockchain
Starts a local Ethereum network with pre-funded test accounts.
```shell
npx hardhat node
``` 
![hardhat-node.png](pics/hardhat-node.png)

Open the Hardhat console (new terminal)
Opens an interactive console connected to the local blockchain.
```shell
npx hardhat console --network localhost
```
![hardhat-console.png](pics/hardhat-console.png)

Get a test account (Hardhat console)
Retrieves the first test account to deploy and send transactions.
```shell
const [owner] = await ethers.getSigners()
```
![get-test-account.png](pics/get-test-account.png)
![block-chain-test-account.png](pics/block-chain-test-account.png)   

Set an unlock time
Creates a timestamp 60 seconds in the future.
```shell
const unlockTime = Math.floor(Date.now() / 1000) + 60
```
![set-unlock-time.png](pics/set-unlock-time.png)

Create contract factory
Loads the compiled Lock contract.
```shell
const Lock = await ethers.getContractFactory("Lock")
```
![create-contract-factory.png](pics/create-contract-factory.png)
![block-chain-contract-factory.png](pics/block-chain-contract-factory.png)

Deploy the contract and send Ether
Deploys the contract and sends 1 ETH to it.
```shell
const lock = await Lock.deploy(unlockTime, { value: ethers.parseEther("1") })
```
![deploy-contract.png](pics/deploy-contract.png)
![block-chain-deploy-and-send.png](pics/block-chain-deploy-and-send.png)

Read contract state
Calls read-only functions to check stored values.
```shell
await lock.owner()
await lock.unlockTime()
```
Withdraw funds
Withdraws funds after the unlock time has passed.
```shell
await lock.withdraw()
```
Exit the Hardhat console
Leaves the Hardhat interactive console.
```shell
.exit
```
Stop the local blockchain
Stops the local Hardhat network.
```shell
Ctrl + C
```

