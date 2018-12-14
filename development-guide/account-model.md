# Exchange Model

## Account

### Account types

There are two account types: _SPOT\_AVAILABLE, SPOT\_FROZEN_. There will be different accounts for each balance.

### User types

The related classes: _users_, _spot\_accounts, spot\_accounts_\__flow, api\_key\_auths._

The exchange user has only necessary data needed for running, id, canTrade, canWithdraw, level, etc.

There are several user types:

| user type | amount | account type | function |
| :--- | :--- | :--- | :--- |
| MANAGER, UI, WALLET | 1 | no account | no use, placeholder for api\_key. |
| ASSET | 1 | SPOT\_AVAILABLE | the exchange account, represents the asset of the exchange. will always be zero if everything works correctly, but is useful in creating account flows. |
| DEBT | 1 | SPOT\_AVAILABLE | the exchange debt account, denotes how much tokens were actually in the exchange. DEBT always &lt; 0 |
| WITHDRAW\_FEE | 1 | SPOT\_AVAILABLE | fee collected from users when they withdraw, exchange income. |
| WITHDRAW\_COST | 1 | SPOT\_AVAILABLE | actually spent in broadcasting TXs in blockchain network. |
| TRADE\_FEE | many | SPOT\_AVAILABLE | fee collected from users when they trade, exchange income. |
| TRADER | many | SPOT\_AVAILABLE                 SPOT\_FROZEN | the user account |
| MINING | many | SPOT\_AVAILABLE |  |

### Account flow

The wallet service will create account flows through exchange-api, and the balances for the wallet \(in the actual blockchain addresses\) are separated from that in the exchange.

#### 1. Deposit

When a deposit is confirmed, an account flow from DEBT to ASSET will be created.

Then the system will find out whom this deposit belongs to, and create an ASSET to TRADER flow to actually send to the user.

DEBT -&gt; ASSET

ASSET -&gt; TRADER

#### 2. Withdraw

When a withdraw is submitted, USER/AVAILABLE -&gt; USER/FROZEN.

When the withdraw is broadcasted.

USER/FROZEN -&gt; ASSET

USER/FROZEN -&gt; WITHDRAW\_FEE

ASSET-&gt; DEBT

If the withdraw failed, a reverse flow will be created.

When the withdraw is packaged in the block and confirmed,

WITHDRAW\_FEE -&gt; WITHDRAW\_COST

#### 3. Trade

When an order is placed,

USERA/AVAILABLE -&gt; USER/FROZEN

USERB/AVAILABLE -&gt; USER/FROZEN

When an order pair is matched,

USERA/FROZEN -&gt; USERB/AVAILABLE

USERA/FROZEN -&gt; FEE

USERB/FROZEN -&gt; USERA/AVAILABLE

USERB/FROZEN -&gt; FEE

## Trade

_orders, order\_sequences, clearing\_records, clearing\_results, ext\_order\_fee\_refunds, level\_fee\_rates, match\_message\_store, bars, ticks_



