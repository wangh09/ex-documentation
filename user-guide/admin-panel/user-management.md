#### 用户管理

* **实名认证\(KYC\)**

  * 功能：查询用户KYC信息，详情页可对**已提交C1及以上**的用户审核**通过或拒绝**。
  * 查询参数
    * KYC状态：全部、待审核、已通过、未通过、未提交、C1、C2、C3
    * UID，邮箱，手机号
    * KYC信息提交时间
  * 查询结果：以数据表格形式展示
  * 操作：

    * UID、邮箱、手机号及提交时间查询为精确查询，仅可在全部下查询，且互斥
    * **用户提交C1信息后，可通过点击列表行进入相应用户KYC详情页**

    * 详情页：

      * 默认表格： 展示用户C1的提交信息及C1认证状态
      * | 用户C1提交信息国家名 | 是否开启阿里云第三方服务 | C1详情列表 | C2详情列表 |
        | :--- | :--- | :--- | :--- |
        | 中国 | 是 | 显示采集数据信息 | 显示采集数据信息 |
        |  | 否 | 列表为空 | 列表为空 |
        | 非中国 | \ | 不显示 | 不显示 |
      * C2证件正反面及手持证件照及手动审核**通过/拒绝**，调用OSS服务，**拒绝后会自动删除图片信息，且只能操作一次**

      * C3为提交申请后，手动审核**通过/拒绝，且只能操作一次**

* **用户列表**

  * 功能：查询用户列表、激活/冻结登录、激活/冻结交易、激活/冻结提现、查看用户详细信息。

  * 查询参数：

    * 状态：全部、待审核、注册最早

    * UID、邮箱、手机号

    * 用户注册时间

  * 查询结果：以数据表格形式展示

  * 操作：

    * 激活\(冻结\)登录：点击**登录正常/登录冻结**按钮，确认无误后，点击**确定冻结/激活登录**

    * 激活\(冻结\)提现：点击**提现正常/提现冻结**按钮，确认无误后，点击**确定冻结/激活提现（如果该用户没有底层id，该按钮不可以点击）**

    * 激活\(冻结\)交易：点击**交易正常/交易冻结**按钮，确认无误后，点击**确定冻结/激活交易（如果该用户没有底层id，该按钮不可以点击\)**

    * 查看用户详细信息：可通过点击**列表行**进入相应用户详细信息

    * UID、邮箱、手机号及注册时间查询为精确查询，仅可在全部下查询，且为互斥关系。



