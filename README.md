<!-- # 🪙 Token -->

[//]: # (<img alt="workshop/token" width="1412" src="../.resources/token.png">)
## The Second Task From The Workshop

Leo is a functional, statically typed programming language built for writing private applications. Leo is a high-level programming language that compiles down to low-level Aleo Instructions.

first i ran 
```
leo example token 
```
Creates a token project, we can then mint tokens to send to receiver
Then cd into ``` token ```

Then i ran 
```
leo account new
```

Generates a struct output that contains:

``` 
 {
  owner: aleo19pu64fuk0pgmkxzl2s8mwz9dcex6g4tdh4pmehd9fh9wdz9xdcgshprdr4,
  amount: 10u64,
  _nonce: 710947497959521588541978475371274797290179560223644761302029085270296751312group
}
```

## Minting token

I then ran command
```
leo run mint_private aleo1dmzle074dsf34m8q8x0gepg0hr5jtqdptn47ump0n6hk7atue59q3s5meu 10u64
```
This command mints 10 Token as specified 10u64


I changed the transfer function input in the token.in file by adding this:
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

Using this command to send 3 tokens to receiver address
```
leo run transfer_private
```
Changed the private key in the env file.

Also created a transition trasnfer_private_all function in the main file

```
   //This function `transfer_private_all` sends the total amount of the token to the receiver from the specified token record.
  transition transfer_private_all(sender: token, receiver: address) -> (token, token) {
        
        let total_funds: u64 = sender.amount;

        // Produce a token record with the change amount for the sender.
        let remaining: token = token {
            owner: sender.owner,
            amount: 0u64,
        };

        // Produce a token record for the specified receiver.
        let transferred: token = token {
            owner: receiver,
            amount: total_funds,
        };

        // Output the sender's change record and the receiver's record.
        return (remaining, transferred);
    }

```

Finally, I added the input in the token.in file
```
[transfer_private_all]
sender: token = token {
 owner: aleo19pu64fuk0pgmkxzl2s8mwz9dcex6g4tdh4pmehd9fh9wdz9xdcgshprdr4,
 amount: 10u64,
 _nonce: 710947497959521588541978475371274797290179560223644761302029085270296751312group
};

receiver: address = aleo14f6r8ee728arw8u2mgqfv37xk7lputxk5yman56krp2gn84a8urqfwnkkf;
```
then run 
```
leo run transfer_private_all
```
