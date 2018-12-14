# External Services

## 1. Git for configuration management

| resource name | access name | example value | Documentation |
| :--- | :--- | :--- | :--- |
| git repository for config | GIT\_URL | [https://github.com/ex/config.git](https://github.com/ex/config.git) | Git Setup |
|  | GIT\_USER | gitlab\_user |  |
|  | GIT\_PASS | Abcd1234 |  |

## 2. Mysql

The database url, username, and password are needed and should be filled in git config files.

| db name | group | service | access type |
| :--- | :--- | :--- | :--- |
| ex | matching engine | crypto-\* | ReadWrite & ReadOnly |
| hd | wallet | wallet-\* | ReadWrite |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

## 3. MQ

The nameserver address is needed. 

## 4. Redis

The redis host and port are needed, while the password is optional. The ex and the app all need redis, they can be the same one or saparatedly created.

## 5. Blockchains

Refer to Blockchain in Environment Setup for more information.

