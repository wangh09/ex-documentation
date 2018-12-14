## Buissness deploy processuer

1. Create kubernetes namespace.
2. Create mysql redis rocketmq basic instrument service.
3. Create gitlab configuration projects, mainly to modify mysql and redis password. and there is no password for redis service
4. Create secret.yml ，modify git related content. including git-uri \(Ex. [http://xxx.xxx/xx.git\](http://xxx.xxx/xx.git%29\). git-username and git-password. and remember to encode by base64
5. Gernate kubernetes dockerconfig  secret for pulling image. 
6. Deploy by sequece for crypt-config  、crypto-api、wallet-signing、wallet-siging module.
7. Configure aws storageClass and its' PVC，then configure and startup  match  module
8. Deploy others module by sequnece for crypto-sequence、crypto-clearing、crypto-quotation and crypto-notification module

---

## TODO

* There's no password for redis service supplied by AWS. so need to annotate  redis password line by gitlab configuration.
* 


