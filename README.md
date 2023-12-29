<!-- # 🪙 Token -->

[//]: # (<img alt="workshop/token" width="1412" src="../.resources/token.png">)
## The Second Task From The Workshop

Leo is a functional, statically typed programming language built for writing private applications. Leo is a high-level programming language that compiles down to low-level Aleo Instructions.
I changed the transfer function input in the token.in file."

I added this:
```
[transfer_private]
sender: token = token {
  owner: aleo19pu64fuk0pgmkxzl2s8mwz9dcex6g4tdh4pmehd9fh9wdz9xdcgshprdr4,
  amount: 10u64,
  _nonce: 710947497959521588541978475371274797290179560223644761302029085270296751312group
};

receiver: address = aleo14f6r8ee728arw8u2mgqfv37xk7lputxk5yman56krp2gn84a8urqfwnkkf;
amount: u64 = 3u64;
```

Using this command
```
leo run transfer_private
```
Changed the private key in the env file.

Also added a transition trasnfer_private_all function in the main file

```
   //This function `transfer_all` sends the total amount of the token to the receiver from the specified token record.
   transition transfer_all(sender: token, receiver: address) -> (token, token) {
       // Produce a token record with the change amount for the sender.
       let owned: token = token {
           owner: sender.owner,
           amount: 0u64,
       };

       // Produce a token record for the specified receiver.
       let transferred: token = token {
           owner: receiver,
           amount: sender.amount,
       };

        // Output the sender's change record and the receiver's record.
       return (owned, transferred);
   }
```

Finally, I added the input in the token.in file
```
[transfer_all]
sender: token = token {
 owner: aleo19pu64fuk0pgmkxzl2s8mwz9dcex6g4tdh4pmehd9fh9wdz9xdcgshprdr4,
 amount: 7u64,
 _nonce: 710947497959521588541978475371274797290179560223644761302029085270296751312group
};

receiver: address = aleo14f6r8ee728arw8u2mgqfv37xk7lputxk5yman56krp2gn84a8urqfwnkkf;
```
then run 
```
leo run transfer_private_all
```
