# Deploy

| Name         | CPU (cores) | Mem (GB) | Number | Description    |
|--------------|-------------|----------|--------|----------------|
| config       | 1           | 1        | 1      |                |
| api          | 4           | 8        | 2      |                |
| sequence     | 1           | 2        | 2      |                |
| match        | 4           | 8        | 2      |                |
| ui           | 2           | 4        | 2      |                |
| manage       | 1           | 2        | 1      | VPN accessonly |
| notification | 1           | 4        | 2~4    | websocket      |
| nginx        | 2           | 4        | 2      | load balancer  |
| rocketmq     | 2           | 4        | 2      | 1M-1S-Sync     |

所有主机必须启动NTP时间同步，保证时间无误。

所有服务均以supervisor启动，启动后用户切换为www-data（或其他低权限用户）。

强烈建议启用内网DNS服务，例如：api.cryptoexchange.local。
