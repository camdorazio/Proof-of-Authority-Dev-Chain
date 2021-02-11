# POA-Development-Chain

Set-up process:
- Create a new enviornment for ethereum blockchain
- Install necessary packages using this guide [Blockchain Installation Guides](https://github.com/camdorazio/POA-Development-Chain/blob/main/blockchain-install-guide.md)
- Bu sure you have MyCrypto app installed as we will need it to send a tranbsaction with our newly created ETH blockchain.

# Creating a Blockchain 
1. Open an instance of Git Bash. 
2. Activate you enverionment you created in the Set-up process. (refer to [Blockchain Installation Guides](https://github.com/camdorazio/POA-Development-Chain/blob/main/blockchain-install-guide.md))
3. Navigate to the directory where you created the "Blockchain-Tools" folder (the directory would have been created when you installed GoEtherum Tools - refer to [Blockchain Installation Guides](https://github.com/camdorazio/POA-Development-Chain/blob/main/blockchain-install-guide.md))
4. Activate puppeth using the following command:
 - $ ./puppeth

## Creating the Genesis State
1. Next will we set a genesis state. This esentially starts a clean network with 0's for your hashes. This will be a new blockchain network that will be run locally.
2. Start by giving your network a name. In this case I will use: ethtest
3. Next you will receive a series of prompts to create the genesis state. You will select the following options:
 - option 2. Configure new genesis
 - option 1. Create new genesis from scratch
 - optoin 2. Clique - proof-of-authority
 - "How many seconds should blocks take? *for this example I have used the defaul of 15 seconds.*
 - Which accounts are allowed to seal? *This is where you enter your node 1 and node 2 wallet addresses (i.e. 0x......). You will need to do the Creating the "Nodes for Validation" section below and come back to to fill in the address (IMPORTANT: Do not close this GitBash window!).*
 - - Which accounts should be pre-funded? *This is where you enter your node 1 and node 2 wallet addresses (i.e. 0x......). You will need to do the Creating the "Nodes for Validation" section below and come back to to fill in the address (IMPORTANT: Do not close this GitBash window!).*
 - Should the precompile-addresses be pre-funded with 1 wei? no
 - Specify your chain/network ID if you want an explicit one. *for this example I will leave the default=random. You don't want to run into an issue where you create a chain ID you may have previously created or is being used for an existing network (i.e. 1=ETH and therefore you cannot use a chain/network ID of 1.*

CONGRATULATIONS!! You have just created your genesis. 

*NOTE*: You need to save your genesis information, please choose the following:
- option 2. Manage existing genesis 
- optoin 2. Export genesis configurations

*This will create .json files in your existing directory with the genesis information. You will need one of these files to unlock your wallet in the MyCrypto app so you can do the test transaction at the end.*

## Creating the Nodes for Validation
1. Open a new Git Bash window. *(It's important that you do not close the previous GitBash window with the genesis information as you need some information when creating the nodes to finalize your genesis.)*
2. Activate your blockchain enviorment that you created and navigate to the directory where you created the "Blockchain-Tools" folder.
3. Next we create a new account using the following command:
 - $ ./geth account new -datadir node1
4. Enter and re-enter a password to access node1. *NOTE: You can use the following command in paranthesis to view the directory tree in Git Bash. ($ tree.com //a)*
5. Copy your Public address of the key and Path of the secret key file (I recommend into Notepad) as we will need this information to finish creating the genesis and again later to activate the nodes.
6. To create additional nodes, you will need to open separate Git Bash windows for each additional node. For this example, I will create another node called node2 following the same process described above using the same command but replacing node1 with node2. Don't forget to copy your Public address of the key and Path of the secret key file for each node that you create. *NOTE: You need at least 2 nodes to run a blockchain.*

## Initializing the Blockchain State for each Node
1. We need to initalize our genesis state using the following command:
 - $ ./geth init "GENESIS_NAME".json -datadir node1
*The GENESIS_NAME in this case is "ethtest". You will see the .json files in your directory.*

*NOTE: Check your directory tree to ensure your node directory and chaindata and lightchain data sub-directories have been created for each node. This will be important as you will need to access these files later to complete your blockchain set-up and testing.*

 - $ ./geth init ethereumking"GENESIS_NAME".json -datadir node2

# Blockchain Mining
## Let's start mining some ETH!

1. Run the nodes in separate terminal windows with the commands:

    - ./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
    - ./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock --ipcdisable

  *NOTE: SEALER_ONE_ADDRESS is the Public Address of the Key for Node 1. SEALER_TWO_ADDRESS is the Public Address of the Key for Node 2. SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303 is the enode address of node 1 which can be located n GitBash when you initialze node 1.*  

2. Make sure you enter the passwords when prompted in GitBash for each node and confirm that the nodes have been unlocked. Once both nodes are unlocked, you should see that there is at least 1 peer connected to each node.

Congratulatons! You are now mining some ETH!

# Test your newly created ETH blockchain network
1. We will now connect to the newly created ETH blockchain network and send a transaction. Follow these instructions [My Crypto - Network Set-up and Transactions](https://github.com/camdorazio/POA-Development-Chain/blob/main/MyCrypto-network.md)).
*NOTE: The Chain/Network ID can be found in the "GENESIS_NAME".json file in your "Blockchain-Tools" folder.*

2. Please be patient once you have successfully sent a transaction and it's in "PENDING" state. Average time for the transaction to be confirmed and "SUCCESSFUL". As a baseline, for this test case, it took over 3 hours for my transaction to be "SUCCESSFUL". You need to leave the Git Bash windows for all the nodes running, in mining mode, for the transaction to be confirmed and completed.

# CONGATULATOINS ON SETTNG UP YOUR OWN PERSONAL ETH BLOCKCHAIN NETWROK!







