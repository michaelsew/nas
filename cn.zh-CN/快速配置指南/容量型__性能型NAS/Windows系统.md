# Windows系统 {#task_944060 .task}

本文档介绍如何快速创建文件系统，并将其挂载至云服务器ECS（Windows系统）。

1.  已注册阿里云账号，并完成实名认证。

    如果没有，请先注册阿里云账号，详情请参见[../../../../dita-oss-bucket/SP\_89/DNEIP11875793/ZH-CN\_TP\_12832\_V1.md\#](../../../../intl.zh-CN/.md#)。

2.  已开通NAS服务。

    首次登录[NAS控制台](https://nas.console.aliyun.com/)时，根据页面提示开通NAS服务。

3.  在需要创建文件系统的地域，已有可用的云服务器ECS。

    如果没有，请购买云服务器ECS，详情请参见[../../../../dita-oss-bucket/SP\_2/DNA0011854887/ZH-CN\_TP\_9601\_V14.md\#](../../../../intl.zh-CN/个人版快速入门/创建ECS实例.md#)。

4.  确保Windows系统服务中的Workstation服务和TCP/IP NetBIOS Helper服务均已启动。详情请参见[ZH-CN\_TP\_21209\_V8.md\#](intl.zh-CN/快速配置指南/挂载文件系统/手动挂载SMB文件系统.md#)。

    **说明：** 

    1.  如果您要使用RAM账户操作NAS，详情请参见[../../../../dita-oss-bucket/SP\_111/DNnas1882233/ZH-CN\_TP\_776283\_V1.md\#](../../../../intl.zh-CN/用户指南/权限管理/RAM用户访问控制.md#)。
    2.  开通NAS服务后，默认的计费方式是按量付费。如果您想使用更优惠的套餐，可购买存储包，详情请参见[../../../../dita-oss-bucket/SP\_111/DNnas1862918/ZH-CN\_TP\_18686\_V2.md\#](../../../../intl.zh-CN/计费方式/预付费/购买存储包.md#)。
    3.  如果要创建专有网络类型的挂载点，还需在创建文件系统的地域上创建专有网络VPC，并将已创建的云服务器ECS归属到此专有网络VPC下，详情请参见[创建专有网络和交换机](创建专有网络和交换机../../SP_22/DNVPC11885991/ZH-CN_TP_2434_V13.dita#concept_isl_ghv_rdb/section_ufw_rhv_rdb) 。

## 步骤一：创建文件系统 {#section_ycr_jeb_8o0 .section}

1.  登录[NAS控制台](https://nas.console.aliyun.com/)。
2.  选择**NAS** \> **文件系统列表**，单击**创建文件系统**。
3.  在创建文件系统页面，配置相关信息。

    |参数|说明|
    |--|--|
    |地域| 选择要创建文件系统的地域。

**说明：** 

    -   不同地域的文件系统与云服务器ECS不互通。
    -   地域不同，文件系统支持的存储类型、协议类型不同，更多详情请参见 [NAS 所在地域与存储类型、协议类型的对应关系](../../../../intl.zh-CN/常见问题/一般性问题/NAS 地域与支持的存储类型和协议类型.md#)。
    -   每个账号在单个地域内最多可以创建20个文件系统。
 |
    |存储类型| 包括**SSD性能型**或**容量型**。

**说明：** 性能型文件系统容量上限为1PB，容量型文件系统容量上限为10PB。按实际使用量付费。

 |
    |协议类型|选择**SMB（2.1及以上）**。 NFS适合Linux ECS文件共享， SMB适合Windows ECS文件共享。

 |
    |可用区| 可用区是指在同一地域内，电力和网络互相独立的物理区域。

 单击下拉框选择可用区，建议和云服务器ECS在同一可用分区。

**说明：** 同一地域不同可用区之间的文件系统与云服务器ECS互通。

 |
    |存储包| 存储包为可选项，是在按量付费的基础上推出的更加优惠的计费方式。如果不购买存储包，系统将默认按量计费，更多详情请参见[计量项和计费说明](../../../../intl.zh-CN/计费方式/计量项和计费说明.md#)。

 |

4.  配置完成后，单击**确定**。

## 步骤二：添加挂载点 {#section_kkl_dpm_swq .section}

在文件存储NAS中，需要通过挂载点将文件系统挂载至云服务器ECS。文件存储NAS支持专有网络类型和经典网络两种挂载点，它们的创建方式不同，具体操作如下所示。

**说明：** 每个文件系统最多可添加两个挂载点。

1.  选择**NAS** \> **文件系统列表**。
2.  找到目标文件系统，单击**添加挂载点**。
3.  在**添加挂载点**页面，配置相关参数。

    **挂载点类型**：包括专有网络和经典网络。

    -   如果您要添加专有网络类型的挂载点，请配置以下参数。

        |参数|说明|
        |--|--|
        |VPC网络| 选择已创建的VPC网络。如果还未创建 ，请单击[点击前往VPC控制创建VPC网络](https://vpc.console.aliyun.com/)进行创建。

**说明：** 必须与云服务器ECS选择一样的VPC网络和交换机。

 |
        |交换机| 选择VPC网络下创建的交换机。

 |
        |权限组| 选择**VPC 默认权限组（全部允许）**或已创建的权限组。

**说明：** 初始情况下，每个账号都会自动生成一个VPC默认权限组，允许同一VPC环境下的任何IP地址都可以通过该挂载点访问文件系统。如果你要创建权限组，详情请参见[../../../../dita-oss-bucket/SP\_111/DNnas1882233/ZH-CN\_TP\_18697\_V7.md\#](../../../../intl.zh-CN/用户指南/管理权限组.md#)。

 |

    -   如果您要添加经典网络类型的挂载点，请配置以下参数。

        |参数|说明|
        |--|--|
        |权限组| 选择已创建的权限组。如果还未创建，单击[点击管理/创建权限组](https://nas.console.aliyun.com/#/accessGroup/list)进行创建。

**说明：** 

        -   目前不支持境外地域添加经典网络挂载点。
        -   目前经典网络类型挂载点仅支持ECS实例挂载。
        -   出于安全原因，NAS没有提供经典网络类型的默认权限组。因此初次使用时，您需要在权限组页面创建一个经典网络类型权限组，并向权限组添加合适的规则。有关权限组的操作，请参见[../../../../dita-oss-bucket/SP\_111/DNnas1882233/ZH-CN\_TP\_630045\_V1.md\#](../../../../intl.zh-CN/.md#)。
        -   首次创建经典网络挂载点时，系统会要求您通过RAM授权NAS访问您的ECS实例查询接口，请按照指引完成授权操作后重新尝试创建经典网络挂载点。详细操作请参见[../../../../dita-oss-bucket/SP\_111/DNnas1843949/ZH-CN\_TP\_18736\_V1.md\#](../../../../intl.zh-CN/常见问题/一般性问题/创建经典网络挂载点时为什么需要RAM授权？.md#)。
 |

4.  单击**确定**，创建挂载点。

## 步骤三：挂载文件系统 {#section_c6i_oxv_mra .section}

执行以下步骤挂载SMB文件系统至云服务器ECS。

1.  登录[云服务器ECS](https://ecs.console.aliyun.com/)。
2.  打开命令行窗口，执行以下命令挂载文件系统。

    ``` {#codeblock_7b8_l26_nq2}
    net use D: \\file-system-id.region.nas.aliyuncs.com\myshare
    ```

    挂载命令格式：`net use <挂载目标盘符> \\<挂载点域名>\myshare`。

    -   挂载目标盘符：指当前Windows系统上要挂载的目标盘符。
    -   挂载点域名：指创建文件系统挂载点时，自动生成的挂载点域名。挂载点详情请参见[../../../../dita-oss-bucket/SP\_111/DNnas1882233/ZH-CN\_TP\_18694\_V7.md\#](../../../../intl.zh-CN/用户指南/管理挂载点.md#)。
    -   myshare： SMB的share名称，不允许变更。
    **说明：** 

    目标盘符不能和本地盘符重名。

    如果执行挂载命令报错，可参见[../../../../dita-oss-bucket/SP\_111/DNnas1843949/ZH-CN\_TP\_149028\_V4.md\#](../../../../intl.zh-CN/常见问题/SMB FAQ/SMB 挂载失败的原因分析.md#)进行排查。

3.  执行`net use`命令，检查挂载结果。

    如果回显包含如下类似信息，说明挂载成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156264047449545_zh-CN.png)


