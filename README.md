### Create HALAL Masternode

- Step 1: Collateral your 1000 HALAL on your Desktop wallet.
    - Your collateral address is where you will be storing your `1000 HLL`.
    - You can create the collateral address in two ways: using the Receive tab, OR in the Debug Window.
        - Receive tab:
            - Click on the Receive tab. 
            - Enter a label for your collateral address in the Label field and click on Request Payment.
            - A window should pop up with a HLL address.
        - Debug Window:
            - Go to Help > Debug Window > Console and type in
            ```javascript 
            getnewaddress
            ```
    - In one single transaction, send exactly `1000 HLL` into the masternode collateral address that you created.
        ##### Note : Do not send 500 and then another 500. It has to be in one single transaction. Do not tick subtract fee from amount.
    - It is not recommended to send it direct from an exchange as they might deduct certain withdrawal fees resulting in less than `1000 HLL` in that transfer.
    - Wait `1 confirmation` for this transaction to be valid as your masternode collateral.
    - When done correctly, the `transaction id` and `transaction index` will appear when you execute this command in the Debug Console:
    ```javascript
    evoznode outputs
    ```

- Step 2: Creating ownerAddress, payoutAddress, feeSourceAddress and operatorKey/operatorPubKey
    - ownerAddress
        - Proof that you own the masternode. Must be in the same wallet as collateral. 
        #### DO NOT USE THE COLLATERAL ADDRESS AS OWNER ADDRESS.
        #### DO NOT SEND COINS TO THE OWNER ADDRESS.  
        #### DO NOT USE IT AS PAYOUT ADDRESS. 
        #### DO NOT USE THIS ADDRESS FOR ANY OTHER PURPOSE.
    - payoutAddress
        - Address the masternode will pay out to. Can be inside the same wallet or an external address.
    - feeSourceAddress
        - An address with funds to pay the transaction fee for registering your masternode. To get a list of addresses with funds, enter the following command in the Debug Window:
        ```javascript
        listaddressbalances 0.01
        ```
        ##### If you do not have any, you can create an address and send some HALAL there. You can then use the address as feeSourceAddress.
    - operatorKey/operatorPubKey
        - In Debug Console, enter `bls generate`. The output will be similar to this:
        ```javascript
        {
            "secret": "2e551176c4cd5a2e26f3a1c61f151487e013f7095ffbc0f62b5c2b251e7bd84c",
            "public": "89d395bc75e99527e80d3bbd408a5b41bbf37e7e1e26c5924da734008d1aa4a3f5e42a968bef541cb1c9a0899280d29b"
        }
        ```
        - secret: This is your operatorKey (for protx) and also the znodeblsprivkey.
        - public: This is your operatorPubKey (for protx)
        ### NOTE : You cannot regenerate the same pair of keys, but you can generate the public key from the secret key if you lose the public key.

- Step 3: Registering your masternode
    - Replace value in below command & Run it for start your Masternode
    ```javascript
    protx register collateralHash collateralIndex ipAndPort ownerAddress operatorPubKey votingAddress operatorReward payoutAddress feeSourceAddress
    ```
    - where
    ```javascript
    collateralHash: transaction ID of your 1000 HALAL collateral (from "evoznode outputs")
    collateralIndex: transaction index of your 1000 HALAL collateral (from "evoznode outputs")
    ipAndPort: the IP address and port of your masternode
    ownerAddress: the ownerAddress, generated in Step 2
    operatorPubKey: the "public" part of the "bls generate" output, generated in Step 2
    votingAddress: "" (defaults to ownerAddress)
    operatorReward: 0
    payoutAddress: A valid HALAL address for your masternode payouts, generated in Step 2
    feeSourceAddress: A valid HALAL address with funds in it to fund the masternode registration, from Step 2
    ```
    #### Example
    ```javascript
    protx register 4950f88867b69760d3cd7c1f53531340f6723eb8f7d7f00730abfa12c5fe10e0 0 207.148.122.12:4502 HRRDAxJwaZYFfmty4aTeKCByz1jbMq8Jy4 995b3e1e2a65ce960a8cc7d305c5914b7f60e888c338c1f3317efbdcac58e82ecc110315ce03f49d9d387ff35c2796ad "" 0 HEZ8E8Fgp8h4HvUjXtjz3krYraRtySiXdw HWGmCxUQlK2xKGYNyeqGdSYQqfEAB2hjtd

    ```
    - where Details:
    ```javascript
    collateralHash: 4950f88867b69760d3cd7c1f53531340f6723eb8f7d7f00730abfa12c5fe10e0 
    collateralIndex: 0 
    ipAndPort: 207.148.122.12:4502 
    ownerAddress: HRRDAxJwaZYFfmty4aTeKCByz1jbMq8Jy4 
    operatorPubKey: 995b3e1e2a65ce960a8cc7d305c5914b7f60e888c338c1f3317efbdcac58e82ecc110315ce03f49d9d387ff35c2796ad 
    votingAddress: "" 
    operatorReward: 0 
    payoutAddress: HEZ8E8Fgp8h4HvUjXtjz3krYraRtySiXdw 
    feeSourceAddress: HWGmCxUQlK2xKGYNyeqGdSYQqfEAB2hjtd
    ```

	Сongratulations you did it!
