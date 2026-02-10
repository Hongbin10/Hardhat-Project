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

Return 20 accounts 

Open the Hardhat console (new terminal)
Opens an interactive console connected to the local blockchain.
```shell
npx hardhat console --network localhost
```
![open-console.png](pics/open-console.png)

Get a test account (Hardhat console)
Retrieves the first test account to deploy and send transactions.
```shell
const [owner] = await ethers.getSigners()
```
![get-test-account.png](pics/get-test-account.png) 
Returning undefined is a feature of assignment statements; in fact, the owner variable is already ready.
![owner.png](pics/owner.png)

![block-chain-test-account.png](pics/block-chain-test-account.png)
block chain log proof：eth_accounts asks the node "which accounts are there", hardhat_metadata checks the detailed information and finds the metadata of 20 accounts

Set an unlock time
Creates a timestamp 60 seconds in the future.
```shell
const unlockTime = Math.floor(Date.now() / 1000) + 60
```
![set-unlock-time.png](pics/set-unlock-time.png)


Loads the compiled Lock contract.
```shell
const Lock = await ethers.getContractFactory("Lock")
```
![create-contract-factory.png](pics/create-contract-factory.png)
This step is telling Hardhat: "I want to deploy the Lock contract. Please prepare the ABI, Bytecode and Signer information."

![block-chain-contract-factory.png](pics/block-chain-contract-factory.png)
Blockchain log: Check the node to obtain Signer information, including address, public key, balance, etc.

Deploy the contract and send Ether
Deploys the contract and sends 1 ETH to it.
```shell
const lock = await Lock.deploy(unlockTime, { value: ethers.parseEther("1") })
```

![deploy-contract.png](pics/deploy-contract.png)
The deployment transaction has been submitted, but the contract instance is not fully ready.

![block-chain-contract.png](pics/block-chain-contract.png)
Blockchain log proof: The complete execution record of deploying the transaction, proving that the contract has been successfully created and put on the chain.

```shell
await lock.waitForDeployment()
```
![等待部署.png](pics/等待部署.png)
Return the contract instance, allowing users to continue calling the contract's functions, such as querying the contract owner, querying the unlock time, etc.

![确认交易上链.png](pics/确认交易上链.png)
Blockchain log proof: Return the one-time receipt for this transaction.

Read contract state
Calls read-only functions to check stored values.
```shell
await lock.owner()
```
![查合约所有者.png](pics/查合约所有者.png)
Query the current contract owner and return the address when the contract was deployed.

![节点日志.png](pics/节点日志.png)

```shell
await lock.unlockTime()
```
![下一次的解锁时间戳.png](pics/下一次的解锁时间戳.png)

Query the next unlock time and return the timestamp when the contract was deployed.

![区块链日志.png](pics/区块链日志.png)

Withdraw funds
Withdraws funds after the unlock time has passed.
```shell
await lock.withdraw()
```
![取款.png](pics/取款.png)
Withdraw the locked funds to the contract owner's address.

![取款日志.png](pics/取款日志.png)
Withdrawal log: Check the node to obtain the transaction record of the withdrawal.

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

