Although the matching engine has its own user system, this user only care about the coin accounts, trades, deposits and withdraws. In this way, the matching engine can be separated with other complex business functions. One may be curious that how to integrate it with the user system of the app. This is achieved by binding the matching engine userId \(matId\) to the business userId, so that the app can use the matId to access the resources in the matching engine.

Each API call made to the matching engine need to be encrypted. There are two types of API Keys in the matching engine: Token and Key. Tokens are used to access order APIs, and is used for API trading; Keys are used to access other APIs of finance \(deposit & withdraw\), user \(balance, freeze & unfreeze, etc\) modules. The systems in the whole exchange system will have several tokens and keys, which are listed in the following chart.

|  | Token | Key |
| :--- | :--- | :--- |
| App | UIToken | UIInternalKey |
| Admin Panel | UIToken | ManageKey |
| Wallet | - | WalletKey |
| User | API Trading Token \(API KEY\) | - |

App is the foreground system of the exchange. The App will delegate every user accessing the exchange frontends \(web, app\) to send APIs to the matching engine. But if the user want to trade by automatic strategies then he \(she\) will need to request an API Trading Token to access the trading APIs \(only\). The difference between this API Trading Token and the UIToken that owned by the App is that UIToken has the access to all the user data while API Trading Token only has the access to the single user's.

