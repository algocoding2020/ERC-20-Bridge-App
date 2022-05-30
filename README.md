# ERC-20-Bridge-App

Why do we even need a bridge?
On the smart contract of erc20 tokens, there is a function called transfer that allows you to transfer your tokens to any other address right and since Binance and smart contract is based on Ethereum, its addresses also respect the format of Ethereum so can't we just call the transfer function of a token with the address of the the recipient on the Binance smart chain and it would work.
No, it wouldn't work if you do this, it would transfer the token to the recipient address but on the Ethereum blockchain even though Ethereum and Binance smart contracts share the same technology there are two separate networks completely independent smart contracts and Ethereum can only interact with the Ethereum blockchain and smart contract on Binance smart chain can only interact with the  Binance smart contact so we will need another approach.

How:
we cannot do a real transfer of tokens from one chain to another, however, we could create the same token
on the other chain and have a system, when you want to do a transfer, you destroy a token on
one chain and recreate the same token on the other chain. we use the terms burn and mint
instead of creating and destroying. Economically this would be correct the same value that is destroyed
is recreated nothing is lost nothing is added

Architecture:
we are going to have two bridge smart contracts one on Ethereum and one on Binance smart chain.
we also going to have a bridge API that runs script 24X7. so let's say that someone with tokens
on Ethereum wants to transfer his tokens to the Binance smart chain. first, the sender sends his token to the
bridge smart contract on Ethereum which burns the token an event is emitted with the detail of the transfer
including the recipient address on the Binance smart chain and the amount transferred.
then our bridge API received the transfer event and send a transaction to the other bridge smart contract on
Binance smart chain mint the same quantity of token that was destroyed on Ethereum and sends it to the recipient address. this is for transfers from Ethereum to the Binance smart chain and of course, you can also do transfers in the other direction, for that in the bridge API you will need to run a second process
to listen to the transfer events from the Binance smart chain.

![image](https://user-images.githubusercontent.com/69389020/170999693-7213dd3b-95e4-4532-928a-7a9de5e84cad.png)
