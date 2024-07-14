# AVALAMCHEX:-HyperAvalanche

This project makes use of HyperSDK, which enables the creation of unique virtual machines and gives users total control over unique blockchains. We can construct a personalized blockchain that is suited to the unique requirements of your firm by using the HyperSDK, which gives us complete control over the functionality and regulations of your chain. 

## Description 
`consts/consts.go` contains the constants that is accessible across the hyperVM. The HRP, Name, and Symbol constants define information about the TokenVM, including its Human-Readable Part (HRP), name, and symbol.These constants play a crucial role in defining the characteristics and identity of the TokenVM within the hyperVM environment. They help users easily identify and interact with different tokens by providing key information such as the token's name and symbol. 

```js
const (
	// TODO: choose a human-readable part for your hyperchain
	HRP = "DRIFT"
	// TODO: choose a name for your hyperchain
	Name = "YORU"
	// TODO: choose a token symbol
	Symbol = "YU"
)
```

This code is added in the `consts/consts.go.`

`registry/registry.go` contains the action that will be performed in the terminal during interaction.his action can include commands to navigate directories, manipulate files, or run programs. It is executed by typing the command followed by any necessary arguments or options. 
```js
// TODO: register action: actions.CreateAsset
consts.ActionRegistry.Register(&actions.CreateAsset{}, actions.UnmarshalCreateAsset, false),
// TODO: register action: actions.MintAsset
consts.ActionRegistry.Register(&actions.MintAsset{}, actions.UnmarshalMintAsset, false),
```

This code is added in `registry/registry.go`


## Steps of Execution
This project is execute on WSl on windows and GO installed inside `wsl`.<br>
1) run git clone `https://github.com/ashutoshsharan2003/AVAX-PROOF--Avalanche-HyperSDK/tree/main`
2) run cd `AVAX-PROOF--Avalanche-HyperSDK `
3) Github is not allowing us  to upload the files due to large no of files so I decided to upload the files in Compress Zip Files.
4) Extract the `AVAX PROOF_Avalanche HyperSDK`
5) cd `'.\AVAX PROOF_Avalanche HyperSDK\' `
6) In terminal run command `MODE="run-single" ./scripts/run.sh` and this will start our machine with 1 subnet and for 2 subnet run `./scripts/run.sh.` after this command output will look like.

```js
Ran 4 of 4 Specs in 78.399 seconds
SUCCESS! -- 4 Passed | 0 Failed | 0 Pending | 0 Skipped
PASS
cluster is ready!
avalanche-network-runner is running in the background...

use the following command to terminate:

killall avalanche-network-runner
```

7) To start interaction run ./scripts/build.sh. output will be :
```js
/scripts/build.sh
Building tokenvm in ./build/tHBYNu8ikqo4MWMHehC9iKB9mR5tB3DWzbkYmTfe9buWQ5GZ8
Building token-cli in ./build/token-cli
```
This command will put the compiled CLI in ./build/token-cli. 
<b>NOTE- default address is   `token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp`

8) Lastly, we'll need to add the chains we created and the default key to the token-cli. run command:
```javascript
./build/token-cli key import demo.pk
./build/token-cli chain import-anr
```
Chain import-anr connects to the Avalanche Network Runner server running in the background and pulls the URIs of all nodes tracking each chain you created.

## Creation and Minting process
### Step:-1 Asset Creation
To create an assest run the command:
```javascript
./build/token-cli action create-asset
```
Enter the metadata (eg:`Etherium`) and confirm
output looks like:

```js
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: Wo124aKBGugeXe1oigshKyzqNoYaMYmoDGCAWi2vWgNZUKgR
metadata (can be changed later): Etherium
continue (y/n): y
✅ txID: 2DQsP1Q3h6Zyqr5R6HNq1wdN9BqPML9niYqGkAuRdh1DYjECXM
```
<b>NOTE - txID is the assetID of your new asset.</b>

### Step:-2 Minting of asset
To mint the created assest run command:
```javascript
./build/token-cli action mint-asset
```
enter the assetID then enter the receipient then enter the amount and continue.
It would be look like this:-
```js
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: Wo124aKBGugeXe1oigshKyzqNoYaMYmoDGCAWi2vWgNZUKgR
assetID: 2DQsP1Q3h6Zyqr5R6HNq1wdN9BqPML9niYqGkAuRdh1DYjECXM
metadata: Etherium supply: 0
recipient: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
✔ amount: 100█
continue (y/n): y
✅ txID: 2Pr2Pdmpe8qCas7fxgPFq6VQZJmyiVZabJfwP7CCgeYMJNXcX7
```
### Step:-3 check balance
run the command:
```javascript
./build/token-cli key balance
```
and enter the assetID of the token and output will be like:
```js
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: Wo124aKBGugeXe1oigshKyzqNoYaMYmoDGCAWi2vWgNZUKgR
assetID (use TKN for native token): 2Pr2Pdmpe8qCas7fxgPFq6VQZJmyiVZabJfwP7CCgeYMJNXcX7
✔ assetID (use TKN for native token): 2Pr2Pdmpe8qCas7fxgPFq6VQZJmyiVZabJfwP7CCgeYMJNXcX7
uri: `http://127.0.0.1:29638/ext/bc/Wo124aKBGugeXe1oigshKyzqNoYaMYmoDGCAWi2vWgNZUKgR`
metadata: Etherium  supply: 100 warp: false
balance: 100 2Pr2Pdmpe8qCas7fxgPFq6VQZJmyiVZabJfwP7CCgeYMJNXcX7
```
### Transfer assets
spilt terminal and in 1st run the command 
```javascript
./build/token-cli chain watch
```
enter 0 and execute it
in second terminal run
```javascript
./build/token-cli action transfer
```
then enter the assetID which we earlier created and enter the recepient address in this case we are don't have other address so we will transfer to ourself and see the transaction in first terminal. enter the amount and continue.


### Closing 
run the command 
```javascript
killall avalanche-network-runner
```
This will close the blockchain we just deployed.

##### Author 
Ashutosh Sharan
`(https://www.linkedin.com/in/ashutosh-sharan-177630249/)`
