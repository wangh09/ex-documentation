## Prerequirements

* Basic instruments: Mysql 、Redis、Rocketmq、Gitlab、Docker Registry and Kubernetes cluster

* Somethings generated from cold wallet. 
  * config\_hd.js will be applied for wallet-signing service.
  * xpub.keys data should be imported to mysql.

## Configurations for config.ini

```
[config]
# Order of kubectl apply to run. it reprsents directory now
order = namespace secrets storage resources wallet config api match notification quotation clearing sequence 

namespace = ex
appenv = test

[secrets]
# dockerCfg is applied for imagePullSecrets. and its content is from ~/.docker/config.json
dockerCfg = {"auths": {"544322597768.dkr.ecr.us-west-2.amazonaws.com": {"auth": "QVdTOmV5SndZWGxzYjJGa0lqb2lRamRCTkZoNmJtNU1lRkpPVFVKcmNFSnpTVmxKVVdKU1pWRlFXbU5XV21Wc2QyNXpMMjR2Ukc5WVZWSkRSMEppUVhsTVpHWk9iMlJFYjBGUWJXWlNVMHd4YTFWQlNXUTFVemt4V0dwNlZqYzNXbEZNVTFGUlMwZHpUVGhzVlZSU09IRmtXbkZtUmtoT01FTkxTRGRMUTJGbWMxTnhjWFJOWWxKc1F6ZFVZbXhxTVVSMU9UZDFjUzlPVFdoelNuRTBjRmhLWkZobFZuSTFZMFZ4YWtSaGFTdG5iakI2Y2xvckwwTjZaSEZMTjJGemRtTXJTVGRtV1M5SWNuTmFkRWxKYVVwdlpsbDBNVWx5U25BeE5FdFNUa2M1ZGxOQ2FuUkxiUzlJYzB0a2VYbFBLeTlJWnpVNVIxUkVkVlIwTTNSMVl6Qm5WVll6VDJoR1RDOVdSV1kwTDJzMGNIZEllRzlyUmxkTU1rZHpiRkpETlhKS05HbDJlRnBvU0hrMU9UbFVaa3g2Y3pVNWNqTk1OM0ZsVTB4S05YWlplR1Z5UW10aFIzSllSazlTUkhCRWNIbDNObGRqYWk5a2QyTnJaMFJNVUM4ME1XeFlTV3hzYTA5VFNYaHBVM0I2UVVGUGRIUm9NVXM0WVhWelJXRklkMjFHVFNzMVNGTTJZM3BpUVZkelpYaEpNV1Z4VUdFMU1YSm9PVVZXVldWNGJYbzBUVmhWVWtVMWFFWm9UR1U1VWsxclJWZEJiVWhFYTNOMU9GZG5VMjVTYmxWaWVFNXRTVFYxUjB4T1dUSTRhbEpWVVU5NVNXdFRTRzlOVDNNeWJscDZjVmMxU1ZSVU1GUnhaM3ByVlRGUGQzQjNkRnBvWmt4UGVWSXJSRUpZV1ZaUk1XVjJkWFJqVERWeFRHbEplbVJIVWtZdk0ydHlWVUZDZW1OQlMwMDFhbmxzUVdSYVVrNXZNRkF2Y1hSSFNuSkdhVTF3YUV0VWJIVjJiVmxrTTJsQlFXWm9OR3BLTTJGYVJWTm1lR1EwT1Roc1ZqSm9lbnBOT1hCR2RuUmtia3BsYnpobE9UbG9NQ3RrZDFoVmN6QktLM1JCY0doaGRHWkhhRFV5VUU0ek1uWkpkV2w2WlZKSUsydHBXV2RJTlZOcVNXc3ZMM0pCU0VKSlZIQjRhMUJtZVZGSk1XUm1Wa3RxT1RKWGQxcG5OV3h6ZURoQ1RXVTBja2h1TVhndmJGcG9URVJSUlRGMmRFOXFXbVJKZUM5TVV6UlpiSFZKVjJacFVtNWxNR05KUkhoeVFtOUNTVzl3VFV0UlVUbG5kRkF2YUZOWlYzVkthalZVVEVscU4yMVhhVEJCUTBGeUx5dE5Za1JtTW5GS1ltRmlNWHBpWkVSWldEZzNRa1JLTlRSU2R6QnFWMlpCTm5wWFJXOUVMM0ZvVmtkd1EwaEJXRWgyVVUxQ1RXdFBXVXNyZEZjek5FTldUMGhwVEU1Qk5HNXRUMmx4Tlc5NFFrTnBlWFZvV25kS2JsVkdjMUF4VURkeFNFb3hPVmhPWlV4bFExY3pUVmRsU1hWUE1qTmxOazA0T1hRM01HY3JWVE5RUW5OdEwwOXhSRXR0TW5GWVpVbHhSa2xSV1ZSRE5HUnFMelJoZUZReFlWSlRSa05qVldVMVdHbHJTbWRvWWxwaVJrVnFlbVZKUTI5d1dqWjFZbEJRV1U1b1JrNXpWVWwxU0V4aVFUUnpjRWhsWW1GYVoyeGlVWGRTTjFWSVVYSmhSelJSYzFGQ1lreFFkWFZQTlU1RlZrazFWRFV4VVRWUGMydDJlamRvUjBkdFZVbDVXR1Z1WjNsTE5WSjVOVVJrZFZkUlZHZzVZMmRhV2tGemNWSlZSbWN2UkdKdVNGTlVhbGRuTTJOSFkwTXZjWGhWTTI1MFJGbG9jRWhhTDJ0SlFrTnBRVU5RWlZobk1XVm5MeXR3T0hCelEwSmFZekk0VUhZdmNIcE5OR2M5UFNJc0ltUmhkR0ZyWlhraU9pSkJVVVZDUVVocU5teGpORmhKU25jdk4yeHVNRWhqTURCRVRXVnJOa2RGZUVoRFlsazBVa2x3VkUxRFNUVTRTVzVWZDBGQlFVZzBkMlpCV1VwTGIxcEphSFpqVGtGUlkwZHZSemgzWWxGSlFrRkVRbTlDWjJ0eGFHdHBSemwzTUVKQ2QwVjNTR2RaU2xsSldrbEJWMVZFUWtGRmRVMUNSVVZFVHpaWlNYcHRZVVV4UlV0dVUyaFNXV2RKUWtWSlFUYzJLM2hGZFRsWVJEQlZkalZLYXpGUVFrZEZha0ZsZVdOWWR6WnBObUZ6VUVoUmNFNTFkMU4xTlhGRmQxTmpkR3BsYTNSVlVIbGxTSE15YkhnNGJqVm1URkZLU0dvNGVXSTFZWFZvT0ZWVlBTSXNJblpsY25OcGIyNGlPaUl5SWl3aWRIbHdaU0k2SWtSQlZFRmZTMFZaSWl3aVpYaHdhWEpoZEdsdmJpSTZNVFV6TmpjNE9ERTNNWDA9"}}}
# git related somethings
gitUri = http://gitlab.awsexeks.com/ink/k8s-ex-config.git
gitUsername = ink
gitPassword = lR4Mu8hD1bnEppK0
registryKey = test-key
configHdJs = ./templates/wallet/keys/config_hd.js 

[mysql]
# Mysql instance domain
mysqlDomain = inkex-test.cik6ew4qk1ib.us-west-2.rds.amazonaws.com

[redis]
# Redis instance domain
redisDomain = inkex-test.vsjn8j.0001.usw2.cache.amazonaws.com

[rocketmq]
# Rocketmq server IP and Port
rocketmqIp = 192.168.219.216
rocketmqPort = 9876

[apps]
# Images uri
walletSigningJs = 544322597768.dkr.ecr.us-west-2.amazonaws.com/wallet-signing
walletSendingJar = 544322597768.dkr.ecr.us-west-2.amazonaws.com/wallet-sending
cryptoConfigJarImage = 544322597768.dkr.ecr.us-west-2.amazonaws.com/crypto-config
cryptoApiJarImage = 544322597768.dkr.ecr.us-west-2.amazonaws.com/crypto-api
cryptoClearingJarImage = 544322597768.dkr.ecr.us-west-2.amazonaws.com/crypto-clearing
cryptoSequenceJarImage = 544322597768.dkr.ecr.us-west-2.amazonaws.com/crypto-sequence
cryptoNotificationJarImage = 544322597768.dkr.ecr.us-west-2.amazonaws.com/crypto-notification
cryptoQuotationJarImage = 544322597768.dkr.ecr.us-west-2.amazonaws.com/crypto-quotation
cryptoMatchJarImage = 544322597768.dkr.ecr.us-west-2.amazonaws.com/crypto-match
```

## Run the script

1. Instructions
   * Git location for building up the services  : [http://gitlab.ziggurat.cn/ink-assets/devops-scripts/tree/master/k8s-deployment/matching](http://gitlab.ziggurat.cn/ink-assets/devops-scripts/tree/master/k8s-deployment/matching)
2. How to run

   * Get help   ./apply.py -h  or ./apply.py --help.

   * The command "./apply.py \[parmeters\] " just generages yaml files

   * The command "./apply.py \[prameters\] run " will generates yaml files and apply these yaml files to kubernetes clusters.



