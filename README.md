[toc]

***

### CoFiX Hedge program

#### Background
CoFiX作为一种可计算的金融交易模型的实现，需要做市商角色提供资金流动性，做市商通过承担一定的价格波动风险，来获取交易过程中得到的收益。CoFiX中定义的做市、赎回、兑换交易，都有可能会影响CoFiX资金池的资金比例，这是价格波动风险的来源。
对于价格波动风险，做市商可以通过在场外进行反向交易对冲来消除，基本思路是根据资金池中资金的结构和自己的份额比例，实时的计算出自己可以分得的部分，与自己选定的参考点进行比较，消除负增量，从而保证在任何价格下，总资产都是处于增长状态。

CoFiX is the implemetation of a computable financial transaction model. It requires the role of a market maker to provide liquidity, and the market maker takes a certain risk of price fluctuations, on the same time to earn a margin on each trade. The market making subscriptions, market making redemptions, and trading transactions in CoFiX may affect the proportion of funds in the asset pool, it is the source of price fluctuation risks.

For the risk of price fluctuations, market makers can eliminate the risk through hedging. The basic idea is to calculate the asset they are entilted to in real time based on proportion of funds in the asset pool and their own share amount, and choose a reference point to eliminate negative increments, to ensure that the total assets are growing at any price.

#### 说明
根据前面的描述，具体的对冲策略可以有多种，本对冲程序按照前面描述的基本思路，实现了一种策略，来进行自动化对冲，具体逻辑如下：
1. 程序定义了一个资产结构参考状态，然后轮询检测状态变更，得到状态变更增量。
2. 当一种资产的增量小于0，且绝对值超过一个设定的阈值时，就通过卖出另外一种资产，来将负增长的资产补齐（由于CoFiX交易机制，可以确保做市商需要卖出的资产数量小于其增量，从而实现盈利）
3. 完成2中描述的对冲操作后，将新状态更新为参考状态。
4. 程序运行时，将第一次获取到的状态作为参考状态。

#### 准备

1. 做市商账号地址：主要用来查询个人份额。
2. 以太坊节点URL：可通过 https://infura.io 免费申请。

#### 运行启动

1. 运行项目：windows:双击项目路径下run.bat文件(Linux/MacOS:执行./run.sh)，运行项目，会弹出窗口，请勿关闭，可在窗口查看日志信息，也可以在logs文件夹下查看历史日志信息。
2. 登录：
   * 浏览器输入http://127.0.0.1，会进入登录页面，默认用户名cofix，密码&UJM6yhn。
   * 如需修改密码，可修改co-fi-x-hedging/Hedging/src/main/resourcesapplication.properties中的cofix.user.name（用户名）、confix.user.password（密码）。
3. 如自行打包，需先运行 lib文件夹下的 install-huobi-jar.bar或者install-huobi-jar.sh 文件。


#### 相关设置

1. 必须优先设置节点地址（必填）。
2. 设置做市商账户地址（必填）。
3. 设置网络代理ip地址和端口（非必填）。
4. 设置火币API-KEY和API-SECRET（必填）,交易所对冲必须填写API-KEY和API-SECRET。 
5. 设置资产对冲轮询时间间隔（非必填，默认10秒）;
6. 设置对冲阈值，根据需要自行设置。
7. 开启对冲，以上配置完成后，点击 Hedging 可开启对冲，如需关闭，再点击一次即可。


#### 核心代码

[核心代码说明](./Hedging/README.md)

[toc]

***

### CoFiX Hedge program

#### 背景
CoFiX作为一种可计算的金融交易模型的实现，需要做市商角色提供资金流动性，做市商通过承担一定的价格波动风险，来获取交易过程中得到的收益。CoFiX中定义的做市、赎回、兑换交易，都有可能会影响CoFiX资金池的资金比例，这是价格波动风险的来源。
对于价格波动风险，做市商可以通过在场外进行反向交易对冲来消除，基本思路是根据资金池中资金的结构和自己的份额比例，实时的计算出自己可以分得的部分，与自己选定的参考点进行比较，消除负增量，从而保证在任何价格下，总资产都是处于增长状态。

#### 说明
根据前面的描述，具体的对冲策略可以有多种，本对冲程序按照前面描述的基本思路，实现了一种策略，来进行自动化对冲，具体逻辑如下：
1. 程序定义了一个资产结构参考状态，然后轮询检测状态变更，得到状态变更增量。
2. 当一种资产的增量小于0，且绝对值超过一个设定的阈值时，就通过卖出另外一种资产，来将负增长的资产补齐（由于CoFiX交易机制，可以确保做市商需要卖出的资产数量小于其增量，从而实现盈利）
3. 完成2中描述的对冲操作后，将新状态更新为参考状态。
4. 程序运行时，将第一次获取到的状态作为参考状态。

#### 准备

1. 做市商账号地址：主要用来查询个人份额。
2. 以太坊节点URL：可通过 https://infura.io 免费申请。

#### 运行启动

1. 运行项目：windows:双击项目路径下run.bat文件(Linux/MacOS:执行./run.sh)，运行项目，会弹出窗口，请勿关闭，可在窗口查看日志信息，也可以在logs文件夹下查看历史日志信息。
2. 登录：
   * 浏览器输入http://127.0.0.1，会进入登录页面，默认用户名cofix，密码&UJM6yhn。
   * 如需修改密码，可修改co-fi-x-hedging/Hedging/src/main/resourcesapplication.properties中的cofix.user.name（用户名）、confix.user.password（密码）。
3. 如自行打包，需先运行 lib文件夹下的 install-huobi-jar.bar或者install-huobi-jar.sh 文件。


#### 相关设置

1. 必须优先设置节点地址（必填）。
2. 设置做市商账户地址（必填）。
3. 设置网络代理ip地址和端口（非必填）。
4. 设置火币API-KEY和API-SECRET（必填）,交易所对冲必须填写API-KEY和API-SECRET。 
5. 设置资产对冲轮询时间间隔（非必填，默认10秒）;
6. 设置对冲阈值，根据需要自行设置。
7. 开启对冲，以上配置完成后，点击 Hedging 可开启对冲，如需关闭，再点击一次即可。


#### 核心代码

[核心代码说明](./Hedging/README.md)
