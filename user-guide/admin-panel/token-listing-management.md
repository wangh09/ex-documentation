#### 上币管理

* **币对管理**

  * 功能：查询币对列表、开启/关闭币对展示功能、查看操作记录、查看币对、增加币对

  * 查询参数：

    * 状态：全部、上线、开启交易、下线

  * 查询结果：以数据表格形式展示

  * 操作：

    * 点击**全部/上线/开启交易/下线**按钮进行查询

    * 增加币对：点击**添加**按钮，除了开始时间和结束时间之外都是必填项，填写完成之后，然后点击**确认**按钮

    * 开启/关闭币对展示：点击**开启/关闭展示**后，点击**立即开启/关闭**或者是**稍后开启/关闭**\(需选择时间\)按钮，然后点击**确定**。

    * 查看币对：点击**查看**按钮查看币对

    * 操作记录：点击**操作记录**按钮

* **币种管理**

  * 功能：查询币种列表、开启/关闭币种展示功能、开启/关闭币种充值功能、查看操作记录、编辑币种、增加币种

  * 查询参数：

    * 状态：全部、全部开启、只开启充值、只开启提现

  * 查询结果：以数据表格形式展示

  * 操作:

    * 点击**全部/全部开启/只开启充值/只开启提现**按钮进行查询

    * 开启/关闭币种展示：点击**开启/关闭展示**后，点击**立即开启/关闭**或者是**稍后开启/关闭**\(需选择时间\)按钮，然后点击**确定**。

    * 开启/关闭币种充值：点击**开启/关闭充值**后，点击**立即开启/关闭**或者是**稍后开启/关闭**\(需选择时间\)按钮，然后点击**确定**。

    * 增加币种：点击**添加Token**按钮，所有显示出来的字段必须填写，然后点击**确认**按钮\(全部填写正确后确认按钮可点击\)

    * 编辑币种:点击**编辑**按钮，然后点击**确认**按钮\(目前底层只支持编辑币种图片和名称\)

    * 查看币种操作记录：点击**操作记录**按钮

* **充币规则**

  * 功能：增加、编辑、删除充币规则

  * 操作：

    * 增加提币规则：点击**增加**按钮，按规则填入，然后点击**提交**按钮

    * 编辑提币规则：点击**编辑**按钮，按规则填入，然后点击**提交**按钮

    * 删除提币规则：点击**删除**按钮，确认无误后，点击**确定删除**。

    ```
    每个币种添加的第一个充币规则，数量必须为0，且不可删除
    ```

* **提币规则**

  * 功能：开启/关闭提币功能，增加、编辑、查看提币规则
  * 操作：

    * 开启/关闭提币：点击开启/关闭提币后，点击**立即开启/关闭**或者是**稍后开启/关闭**\(需选择时间\)按钮，然后点击**确定**。

    * 编辑提币规则：点击**编辑**按钮，按规则填入，然后点击**提交**按钮

      * 编辑时，币种不可改变；**最小手续费小于最大手续费**

    * 查看提币规则：点击**查看**按钮

* **交易手续费**

  * **user**

    * 功能：查看特殊用户的手续费，添加和删除特殊用户的手续费。

    * 查询参数： UID，手机号，邮箱

    * 查询结果：以数据表格形式展示

    * 操作：

      * 添加用户手续费：需要输入用户的邮箱、挂单手续费、吃单手续费以及生效时间且都是必填项。

      * 删除用户手续费：点击**删除**按钮，确认无误后，点击**确定删除**。

  * **symbol**

    * 功能：查看、添加币对手续费，切换币对且展示当前币对手续费记录。

    * 操作：

      * 添加币对手续费：添加当前币对手续费，需要输入挂单手续费、吃单手续费以及生效时间且都是必填项。

      * 删除币对手续费：点击**删除**按钮，确认无误后，点击**确定删除**。



