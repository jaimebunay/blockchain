# Blockchain

## Proof of Authority Development Chain

In this project, we set up a private testnet that can be used to explore potentials for blockchain. By using testnet, we have the freedom to experiment with blockchain because there is no real money involved. In order to set up this testnet, we will use the following skills/tools:

* Puppeth, to generate and manage new genesis block

* Geth, a command-line tool, to create, initialize, and connect the nodes together

* The Clique Proof of Authority algorithm

## Create a Genesis Block

1. Download a stable version of Geth&Tools and decompress in the project directory. Rename the folder to the desired name.

2. Open Git Bash and cd to the decompressed and renamed folder.

3. Execute the following commands to create accounts for two nodes for the network:

			`./geth account new --datadir node1`
		   `./geth account new --datadir node2`

	Note: Copy the public key from each account to a temporary file. You will need both keys to create the genesis.


4. Run Puppeth, and name your network. Type/select the following for each prompt:

	* Configure new genesis

	* Create new genesis from scratch

	* Clique - proof-of-authority

	* Use 15 seconds default for block time. Length of time it takes to validate a new block into the blockchain network

	* Paste both public key addresses from step 3 for accounts to seal

	* Paste both public key addresses again in the list to pre-fund the accounts

	* Type yes to pre-fund account with 1 wei

	* Specify number to use as the Chain/network ID. This enables Ethereum nodes to connect and sign different transactions. You will need this number to create a custom node in MyCrypto app.

	* Select manage existing network

	* Export existing genesis

	* Type cntrl+c to stop puppeth

## Start the Nodes and Bring the Blockchain to Life

1. Execute the following command to run node1. Include --miner to enable mining of new blocks. Unlock the account with --unlock. The --minerthreads parameter CPU usage during mining.

	`./geth --datadir node1 --mine --minerthreads 1 --unlock "node1_public_key"`

	Note: Save the "enode://...." address in the temporary file.

2. Open a new Git Bash window and cd to the same working directory.

3. Start node2 and include the following parameters: --port 30304 since node1 is already using port 30303. This enables communication. --RPC port opens communication with MyCrypto app. Since the RPC port will be exposed by HTTP communication, we need to --allow-insecure-unlock in order to --unlock the second account. --bootnode directs node2 to talk to node1.

	`./geth --datadir node2 --port 30304 --rpc --bootnodes "enode: PASTE ENODE FROM PREVIOUS STEP" --ipcdisable --mine --allow-insecure-unlock --unlock "node_2_public_key"`

## Connect MyCrypto to Custom Private Network

1. Open MyCrypto app and create a custom node. Type the same Chain/network ID that was created earlier.

2. Switch to the custom network. Open node1 account via its private key. Import private key from ../node1/keystore and type the account password.

3. Transfer funds to the second account.
