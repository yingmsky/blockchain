---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 创建受管通道 

**注意：**在使用 {{site.data.keyword.blockchainfull}} 产品之前，请阅读[免责声明](/docs/services/blockchain/needtoknow.html)一节中的技术和支持信息。  
{:shortdesc}

在某些用例中（例如，高度管制的外汇市场），可能需要让一个值得信赖的第三方负责管理通道上的角色，这些通道通常由各种操作员或成员负责处理。 

供应此类网络的过程类似于创建任何网络。主要差别在于为成员分配他们如何在通道内进行事务处理的许可权。  

以下是用于创建网络和邀请成员的步骤：[管理网络](/docs/services/blockchain/get_start.html#creating-a-network)。 

**注**：在现实世界示例中，此类网络的操作员可能会使用策略编辑器在“创建网络”阶段期间安装定制链代码，但出于本示例的需要，我们假定您的网络配置为标准配置。 

## 创建通道

在您已具有网络并且邀请的成员已完成上线程序后，请浏览至工具栏中的**通道**。 

单击**新建通道**。此时将显示一个屏幕，您可以在其中向您的通道提供名称和描述（描述是可选的）。 

单击**下一步**后，您将进入屏幕，在该屏幕中邀请成员访问通道并管理其许可权。为了配合本示例，假设您是在两家银行之间的外汇兑换中充当值得信赖的第三方。您是值得信赖的第三方，让您自己成为通道的唯一“操作员”，并将其他两家银行分配为“作者”。这将为您赋予唯一的编辑通道的权限（例如，在其上实例化链代码，稍后将详细说明），同时仍使两家银行能够调用事务处理。您的屏幕应该看起来如下： 

  ![选择成员角色](images/selectmemberroles.png "选择成员角色")
*其中“JoeCo”是您，即值得信赖的第三方，“IBM”和“Chris”是两家银行（这显然只是一个示例）。* 

分配正确的许可权后，单击**下一步**。 

这将带您转至通道策略更新屏幕。由于此通道上只有一个操作员（您），因此请选择创建通道所需的成员数为“1”。然后单击**提交请求**。 

注：即使您是此通道的唯一操作员，这仍然只是一个请求；您仍然必须浏览到正确的屏幕，以核准并提交请求来创建通道。 

系统会向您邀请的成员发送电子邮件，并提示他们加入通道。但是，他们仅具有“写入”特权，您负责完成通道创建过程。请浏览至“网络监视器”中的“通知”屏幕，其中会显示创建创建的警报。在“全部”或“暂挂”子选项卡中，找到要处理的请求。单击**复查请求**以显示通道详细信息，然后单击**核准**。然后单击**提交请求**。 

恭喜您！您刚创建了一个受管通道。 

在具有 15 个成员（14 家银行和您（值得信赖的第三方））的网络中，您可能会看到数十种这样的通道。银行 A 和 B 在通道上。银行 B 和 F 在通道上。银行可能会为它们交易的每种货币类型选择单独的通道。但是，在每个案例中，值得信赖的第三方会创建通道、支持事务处理并充当唯一的操作员。 

# 实例化链代码

您的通道已成功创建，但仍需要附加链代码。在专用于外币兑换的通道中，此链代码可能需要通道的所有三个成员（涉及的两家银行和您（值得信赖的第三方））来支持**每笔**事务处理。还可以编写此链代码，以将此事务处理的*结果*记录发送到网络中每个成员组成的受管“只读”通道（稍后将详细说明）。但是，在可以实例化任何链代码之前，必须先将其安装在成员的同级上。一旦完成，即可由通道操作员（您）对其进行实例化。  

安装和实例化此类链代码的实际过程与任何链代码没有什么不同（除了核准实例化所需的操作员数之外），因此请遵循此处的指示信息：[安装和实例化链代码](install_instantiate_chaincode.html.html)。

# 受管只读通道

要继续使用本用例，外汇市场的金融法规可能要求在网络中有一个通道，该通道上的每家银行都处于被动“只读”方式，从而允许跟踪这些货币事务处理的**结果**。这是为了确保（举例来说）在与银行 B 的“押注”中损失了数百万美元的银行 A（超过一段时间内货币涨幅或降幅的价值），不会出现无法支持本事务处理的情况，从而能够将数百万美元转给银行 B。 

要创建此类通道，请遵循之前遵循的相同通道创建过程，这次不是仅邀请两家银行，使它们成为“作者”（您自己是唯一的操作员），而是邀请**每家**银行，并使它们都成为“读者”。然后，执行安装和实例化链代码的相同过程。 

## {{site.data.keyword.IBM_notm}} 支持 

{{site.data.keyword.IBM_notm}} 提供 {{site.data.keyword.IBM_notm}} 实施的 {{site.data.keyword.blockchain}} 解决方案的支持。通过 [{{site.data.keyword.blockchainfull_notm}} DockerHub ![外部链接图标](images/external_link.svg "外部链接图标")](https://hub.docker.com/u/ibmblockchain/) 访问 {{site.data.keyword.blockchainfull_notm}} 支持详细信息，并探索可用的支持合作项目。

有关所有 Hyperledger Fabric V1.0 特性和功能的完整详细信息，请参阅 [Hyperledger Fabric 文档 ![外部链接图标](images/external_link.svg "外部链接图标")](http://hyperledger-fabric.readthedocs.io/en/latest/)。
