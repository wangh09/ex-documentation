# Wallet Model

The wallet can be divded into exchange part and wallet part, and the balances in the exchange and on the blockchain addresses are separated.

The wallet is all about withdrawing and depositing. When depositing, the wallet only knows 'address', while the exchange will assign each deposit to specific user; When withdrawing, the wallet will pick up a proper address for sending out money, and it doesn't care if the address is the deposit address of the user. In other words, the wallet is a big token pool. The exchange will be in possession of the tokens deposited, while the shares of each user are recorded in the database of the exchange.

![](/assets/wallet_model.jpg)



