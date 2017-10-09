---
title: "Maszyny wirtualne aaaAzure planowania i wdrażania dla programu SAP NetWeaver | Dokumentacja firmy Microsoft"
description: "Azure maszyn wirtualnych, planowania i wdrażania dla programu SAP NetWeaver"
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: d7c59cc1-b2d0-4d90-9126-628f9c7a5538
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d1e9fa13d847e4d8abb3c34fd352d1f4ece3717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-planning-and-implementation-for-sap-netweaver"></a>Azure maszyn wirtualnych, planowania i wdrażania dla programu SAP NetWeaver
[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258]:https://launchpad.support.sap.com/#/notes/1814258
[1882376]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555]:https://launchpad.support.sap.com/#/notes/1922555
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2069760]:https://launchpad.support.sap.com/#/notes/2069760
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:dbms-guide.md
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:deployment-guide.md
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md  
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

[planning-guide-figure-100]:media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/planning-monitoring-overview-2502.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-2901]:media/virtual-machines-shared-sap-planning-guide/2901-azure-ha-sap-ha-md.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-3201]:media/virtual-machines-shared-sap-planning-guide/3201-sap-ha-with-sql-md.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/common/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/common/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/common/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/common/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../../storage/common/storage-premium-storage.md
[storage-redundancy]:../../../storage/common/storage-redundancy.md
[storage-scalability-targets]:../../../storage/common/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/common/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-windows-capture-image-resource-manager]:../../windows/capture-image.md
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-create-upload-vhd-oracle]:../../linux/oracle-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes-linux]:../../linux/sizes.md
[virtual-machines-sizes-windows]:../../windows/sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./../../windows/sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./../../windows/sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./../../windows/sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics-windows]:../../windows/multiple-nics.md
[virtual-networks-multiple-nics-linux]:../../linux/multiple-nics.md
[virtual-networks-nsg]:../../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-site-to-site-create.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md
[capture-image-linux-step-2-create-vm-image]:../../linux/capture-image.md#step-2-create-vm-image

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Microsoft Azure umożliwia zasoby obliczeniowe i magazynujące tooacquire firmy w czasie minimalnego bez cykle nabywania długie. Maszyny wirtualne platformy Azure umożliwiają aplikacjom klasycznego toodeploy, firm, takich jak SAP NetWeaver na podstawie aplikacji na platformie Azure i rozszerzyć ich niezawodności i dostępności bez konieczności dalszego zasoby dostępne lokalnie. Usługi platformy Azure na maszynie wirtualnej obsługuje również łączności między lokalizacjami, w których tooactively firm umożliwia integrację ich domenami lokalnymi ich chmur prywatnych i ich pozioma systemu SAP maszynach wirtualnych platformy Azure.
Ten dokument w tym artykule opisano podstawy hello Azure maszyny wirtualnej platformy Microsoft i zawiera omówienie zagadnienia dotyczące planowania i wdrażania dla instalacji programu SAP NetWeaver na platformie Azure i jako taki powinny być tooread dokumentu hello przed rozpoczęciem rzeczywiste wdrożenia SAP NetWeaver na platformie Azure.
Hello papieru uzupełnia hello SAP instalacji dokumentacji i notatki SAP reprezentują hello głównej zasobów dla instalacji i wdrożenia oprogramowania SAP na podane platform.

## <a name="summary"></a>Podsumowanie
Chmura obliczeniowa warunek powszechnie używany jest uzyskanie coraz więcej znaczenia w ramach hello branży IT z małych firm się toolarge i wielonarodowych firmy.

Microsoft Azure to hello platformy usług w chmurze firmy Microsoft, która oferuje szeroką gamę nowe możliwości. Obecnie klienci są toorapidly może udostępnić i usuwanie aplikacji jako usługa w chmurze hello, więc nie są ograniczone tootechnical lub ograniczeń budżetowych. Zamiast inwestowanie czas i pieniądze na infrastrukturę sprzętu, firmy mogą skupić się na aplikacji hello, procesy biznesowe i korzyści dla klientów i użytkowników.

Wraz z usługami Microsoft Azure Virtual Machines firma Microsoft oferuje kompleksową platformę typu infrastruktura jako usługa (IaaS). Aplikacje oparte na oprogramowaniu SAP NetWeaver są obsługiwane w usłudze Azure Virtual Machines (IaaS). Ten dokument zawiera opis jak tooplan i wdrożenie SAP NetWeaver na aplikacje w systemie Microsoft Azure jako platformę hello wyboru.

Witaj papieru, sam koncentruje się na dwóch aspektach:

* Pierwsza część Hello opisano dwa wzorce wdrożenia obsługiwany dla aplikacji programu SAP NetWeaver oparte na platformie Azure. Omówiono także ogólne Obsługa platformy Azure z wdrożenia SAP pamiętać.
* Hello Implementowanie hello dwóch różnych scenariuszy opisanych w pierwszej części hello drugi szczegóły części.

Dodatkowe zasoby można znaleźć w rozdziale [zasobów] [ planning-guide-1.2] w tym dokumencie.

### <a name="definitions-upfront"></a>Definicje z wyprzedzeniem
W dokumencie hello używamy hello następujące warunki:

* IaaS: Infrastruktura jako usługa
* PaaS: Platforma jako usługa
* SaaS: Oprogramowanie jako usługa
* ARM: Usługa Azure Resource Manager
* Składnik programu SAP: poszczególnych SAP aplikację taką jak ECC, BW, Menedżer rozwiązania lub EP.  Składniki programu SAP może bazować na tradycyjnych technologii ABAP lub Java lub aplikacji z systemem innym niż NetWeaver na podstawie takich jak obiektów biznesowych.
* Środowisko SAP: jeden lub więcej składników programu SAP pogrupowane logicznie tooperform funkcji biznesowych programowanie, QAS, szkolenia, odzyskiwania po awarii lub produkcji.
* Poziomo SAP: Odnosi się toohello cały SAP zasobów klienta IT w orientacji poziomej. Witaj pozioma SAP obejmuje wszystkie produkcyjnych i środowiskach nieprodukcyjnych.
* Systemu SAP: hello kombinację DBMS i warstwy aplikacji programu, na przykład programistycznej SAP ERP, programu SAP BW testu systemu SAP CRM produkcji systemu, itp. W przypadku wdrożeń platformy Azure, nie jest obsługiwane toodivide te dwie warstwy między lokalną i platformą Azure. To oznacza, że systemu SAP jest wdrożona lokalnie lub jest wdrożony na platformie Azure. Jednak można wdrożyć hello systemów pozioma SAP do platformy Azure lub lokalnie. Można na przykład wdrożyć hello systemów programowania i testowania SAP CRM na platformie Azure, ale hello SAP CRM produkcji systemu lokalnego.
* Wdrożenie tylko w chmurze: wdrożenia, którym hello subskrypcji platformy Azure nie jest połączony za pośrednictwem lokacji do lokacji lub ExpressRoute połączenia toohello lokalną infrastrukturę sieci. Wspólne dokumentacji platformy Azure rodzaju wdrożeń opisano również jako "Tylko do chmury" wdrożeń. Maszyny wirtualne wdrażane z tej metody są dostępne za pośrednictwem hello internet i publiczny adres IP i/lub w publicznym systemie DNS nazw maszyn wirtualnych przypisanych toohello na platformie Azure. Systemu Microsoft Windows hello lokalnymi Active Directory (AD) i DNS nie zostanie rozszerzony tooAzure w tych typach wdrożeń. Dlatego hello maszyny wirtualne nie są częścią hello lokalnej usługi Active Directory. Dotyczy to także implementacji systemu Linux przy użyciu, na przykład OpenLDAP + protokołu Kerberos.

> [!NOTE]
> Tylko w chmurze wdrożenia w tym dokumencie jest zdefiniowany jako pełną krajobrazów SAP działają wyłącznie na platformie Azure, bez rozszerzenia usługi Active Directory / OpenLDAP lub rozpoznawania nazw z lokalnymi do chmury publicznej. Konfiguracje tylko w chmurze nie są obsługiwane dla systemów produkcyjnych SAP lub konfiguracje, których SAP STMS lub innymi zasobami lokalnymi musi toobe używany podczas komunikacji między systemami SAP hostowane na platformie Azure i zasobów znajdującej się na lokalnym.
>
>

* Między lokalizacjami: w tym artykule opisano scenariusz, w którym maszyny wirtualne są wdrożone tooan subskrypcji Azure, która lokacja lokacja, obejmujący wiele lokacji lub połączenia ExpressRoute między datacenter(s) lokalne powitania i Azure. Dokumentacja wspólnych Azure rodzaju wdrożenia również są opisane jako scenariusze między lokalizacjami. Powodem Hello połączenia hello jest tooextend lokalnej domeny Active Directory/OpenLDAP lokalnymi i lokalnymi DNS na platformie Azure. Hello pozioma lokalnymi jest rozszerzona toohello zasobów Azure hello subskrypcji. Występuje to rozszerzenie, hello maszyn wirtualnych może być częścią domeny lokalne powitania. Użytkownicy domeny hello lokalnej domeny można uzyskać dostępu do serwerów hello i usługi można uruchamiać na tych maszynach wirtualnych (takie jak usługi systemu DBMS). Możliwe jest komunikacji i rozpoznawania nazw między maszyn wirtualnych wdrożonych lokalnie i wdrożone maszyny wirtualne platformy Azure. Jest to hello oczekuje się, że większość toobe zasoby SAP wdrożone w scenariuszu. Aby uzyskać więcej informacji, zobacz [to] [ vpn-gateway-cross-premises-options] artykułu i [to][vpn-gateway-site-to-site-create].

> [!NOTE]
> Między różnymi lokalizacjami wdrożeń systemów SAP, gdzie systemami SAP maszynach wirtualnych platformy Azure są członkami domeny lokalnej są obsługiwane dla systemów produkcyjnych SAP. Konfiguracje między lokalizacjami są obsługiwane w przypadku wdrażania części lub zakończyć krajobrazów SAP do platformy Azure. Nawet działają hello pełną SAP w orientacji poziomej na platformie Azure wymaga o te maszyny wirtualne są częścią domeny lokalnej i REKLAM/OpenLDAP. Wcześniejsze wersje hello dokumentacji możemy omówiono scenariuszy hybrydowych IT, gdzie hello termin "Hybrydowe" jest ścieżką do katalogu głównego w hello fakt, że istnieje łączność między lokalizacjami, między lokalną i platformą Azure. Ponadto hello fakt, że hello maszyn wirtualnych na platformie Azure są częścią hello lokalnej usługi Active Directory / OpenLDAP.
>
>

Niektóre dokumentacji firmy Microsoft opisano scenariusze między lokalizacjami nieco inaczej, szczególnie w przypadku konfiguracji HA systemu DBMS. W przypadku hello dokumentów związanych z SAP hello scenariuszu obejmującym różne pomieszczenia hello rozpoczęcia wrzenia dół toohaving lokacja lokacja lub prywatnej (ExpressRoute) łączności i hello fakt czy poziomo SAP hello jest rozdzielona między lokalną i platformą Azure.  

### <a name="e55d1e22-c2c8-460b-9897-64622a34fdff"></a>Zasoby
Witaj następujące dodatkowe przewodniki są dostępne dla tematu hello wdrożenia SAP na platformie Azure:

* [Azure maszyn wirtualnych, planowania i wdrażania dla programu SAP NetWeaver (w tym dokumencie)][planning-guide]
* [Maszyny wirtualne Azure wdrożenia SAP NetWeaver][deployment-guide]
* [Azure wdrożenia SAP NetWeaver DBMS maszyny wirtualne][dbms-guide]

> [!IMPORTANT]
> Wszędzie tam, gdzie jest używane możliwe toohello łącza, odwoływanie SAP w podręczniku instalacji (odwołanie InstGuide-01, zobacz <http://service.sap.com/instguides>). Jeśli chodzi toohello warunki wstępne i proces instalacji, hello SAP NetWeaver instalacji przewodniki powinna być zawsze przeczytaj uważnie, ponieważ w tym dokumencie opisano tylko określonych zadań dla systemów SAP NetWeaver w maszynie wirtualnej Microsoft Azure.
>
>

Hello następujące uwagi SAP są powiązane toohello tematu SAP na platformie Azure:

| Numer | Tytuł |
| --- | --- |
| [1928533] |Aplikacje SAP na platformie Azure: obsługiwane produktów i zmiana rozmiaru |
| [2015553] |SAP na platformie Microsoft Azure: obsługuje wymagania wstępne |
| [1999351] |Rozwiązywanie problemów z rozszerzonego monitorowania Azure dla programu SAP |
| [2178632] |Klucz monitorowania metryki dla SAP na platformie Microsoft Azure |
| [1409604] |Wirtualizacji w systemie Windows: rozszerzonego monitorowania |
| [2191498] |SAP w systemie Linux przy użyciu platformy Azure: rozszerzonego monitorowania |
| [2243692] |Linux w systemie Microsoft Azure (IaaS) maszyny Wirtualnej: problemów licencji SAP |
| [1984787] |Systemu SUSE LINUX Enterprise Server 12: Informacje o instalacji |
| [2002167] |Red Hat Enterprise Linux 7.x: instalacji i uaktualniania |
| [2069760] |Oracle Linux 7.x SAP instalacji i uaktualniania |
| [1597355] |Zalecenie obszaru wymiany w systemie Linux |

Również przeczytanie hello [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) zawierający wszystkie notatki SAP dla systemu Linux.

Ograniczenia ogólne domyślne i maksymalnego ograniczenia subskrypcji platformy Azure można znaleźć w [w tym artykule][azure-subscription-service-limits-subscription].

## <a name="possible-scenarios"></a>Możliwe scenariusze
SAP jest często postrzegane jako jedną z kluczowych aplikacji hello w przedsiębiorstwach. Architektura Hello i operacje te aplikacje przede wszystkim jest bardzo skomplikowane i ważne jest zapewnienie, że spełniają wymagania dotyczące wydajności i dostępności.

W związku z tym przedsiębiorstwach istnieją toothink dokładnie o tym, które aplikacje mogą być uruchamiane w środowisku chmury publicznej, niezależnie od dostawcy usług w chmurze hello wybrany.

Typy systemu możliwych do wdrożenia SAP NetWeaver na podstawie aplikacji w obrębie chmur publicznych, środowisk są wymienione poniżej:

1. Systemy średniej wielkości produkcji
2. Programowanie systemów
3. Testowanie systemów
4. Systemy prototypu
5. Learning / pokaz systemów

W kolejności toosuccessfully wdrażanie systemów SAP do platformy Azure IaaS lub IaaS ogólnie rzecz biorąc, jest ważne toounderstand hello istotnych różnic między ofert hello tradycyjnych uzyskanie programu lub dostawcy usług hostingowych i oferty IaaS. Dostawcy usług hostingowych tradycyjnych hello lub dostawców dostosowuje infrastruktury (typ sieci, magazynu i serwer) toohello obciążenia odbiorca chce otrzymywać toohost, zamiast tego jest powitania klienta odpowiedzialność toochoose hello prawo obciążenia w przypadku wdrożeń IaaS.

Pierwszym krokiem klienci muszą hello tooverify następujące elementy:

* Witaj SAP obsługiwane typy maszyny Wirtualnej platformy Azure
* Witaj SAP obsługiwane produkty/wersjach na platformie Azure
* Hello obsługiwane wersje systemu operacyjnego i DBMS dla powitalne określonych SAP zwalnia na platformie Azure
* Protokoły SAP przepływności udostępniane przez różne jednostki magazynowe Azure

Witaj toothese odpowiedzi na pytania mogą być odczytywane w Uwaga SAP [1928533].

Jako drugi etap Azure ograniczenia zasobów i przepustowości muszą zużycie zasobów tooactual toobe w porównaniu z systemów lokalnych. W związku z tym klienci muszą toobe znasz możliwości różnych hello hello Azure typy, które są obsługiwane z programu SAP w obszarze hello:

* Zasoby Procesora i pamięci o różnych typach maszyn wirtualnych i
* Przepustowość IOPS o różnych typach maszyn wirtualnych i
* Możliwości różnych typach maszyn wirtualnych w sieci.

Większość tych danych można znaleźć [(Linux) w tym miejscu] [ virtual-machines-sizes-linux] i [tutaj (system Windows)][virtual-machines-sizes-windows].

Należy pamiętać, że hello limity na liście powyżej łącze hello są górne limity. Nie oznacza to, że hello limity dla dowolnych zasobów hello, na przykład IOPS można podać we wszystkich okolicznościach. Wyjątki Hello są jednak hello zasobów Procesora i pamięci wybranego typu maszyny Wirtualnej. Witaj typy maszyn wirtualnych obsługiwanych przez SAP hello zasobów Procesora i pamięci są zarezerwowane i jako taki dostępna w dowolnym momencie w czasie do użycia w ramach hello maszyny Wirtualnej.

Platforma Microsoft Azure Hello jak innych platform IaaS jest wielodostępnej. Oznacza to, że magazynu, sieci i inne zasoby są współużytkowane przez dzierżawców. Inteligentnego logiki ograniczania przepustowości i przydziału jest używane tooprevent jednej dzierżawy z wpływ na wydajność hello innej dzierżawy (zakłócenia sąsiada) w sposób radykalne. Chociaż logiki w usłudze Azure próbuje tookeep wariancje przepustowości wystąpił mały, wysokiej udostępnionego platformy często toointroduce większych wariancje dostępności zasobów/przepustowość niż wielu klientów są używane tooin wdrożeń lokalnych. W związku z tym mogą wystąpić różne poziomy przepustowości dotyczących sieci lub magazynu we/wy (hello woluminu także opóźnienia) toominute minuty. prawdopodobieństwo Hello systemu SAP na platformie Azure mogą wystąpić różnice większych niż w systemie lokalnym musi toobe brana pod uwagę.

Ostatnim krokiem jest tooevaluate wymagań dotyczących dostępności. Może się zdarzyć, tym hello podstawowej infrastruktury platformy Azure wymaga tooget aktualizacji oraz hello hostach z systemem toobe maszyn wirtualnych ponowny rozruch. W takich przypadkach maszyny wirtualne na tych hostach może być zamknięte i ponownie uruchomione również. czas Hello takiej obsługi odbywa się w godzinach pracy z systemem innym niż rdzeni w określonym regionie, ale hello okna potencjalnych kilka godzin, podczas którego nastąpi ponowne uruchomienie jest stosunkowo szeroki. Istnieją różne technologie w hello platformy Azure, które można skonfigurować toomitigate niektóre lub wszystkie hello wpływu tych aktualizacji. Przyszłe ulepszenia z hello platformy Azure, bazami danych, i SAP aplikacji są zaprojektowane toominimize hello skutków takiego ponownego uruchomienia.

W kolejności toosuccessfully wdrożenia systemu SAP do platformy Azure, hello lokalnej SAP systemy System operacyjny, baza danych, i aplikacje SAP musi występować w hello Azure SAP zapewniają macierz obsługi, mieszczą się hello hello zasobów infrastruktury platformy Azure i które może współpracować z powitalne zapewnia dostępność SLA Microsoft Azure. Określone systemy należy toodecide na jednym z hello następujące dwa scenariusze wdrażania.

### <a name="1625df66-4cc6-4d60-9202-de8a0b77f803"></a>Tylko w chmurze — wdrożenia maszyny wirtualnej na platformie Azure bez zależności na powitania lokalnej sieci klienta
![Jednej maszyny Wirtualnej z pokaz SAP lub scenariusza szkolenia wdrożona na platformie Azure][planning-guide-figure-100]

Ten scenariusz jest typowy szkolenia lub pokaz systemów, którym są zainstalowane wszystkie składniki hello SAP i oprogramowania z systemem innym niż SAP w jednej maszynie Wirtualnej. Systemów produkcyjnych SAP nie są obsługiwane w tym scenariuszu wdrażania. Ogólnie rzecz biorąc w tym scenariuszu spełnia hello następujące wymagania:

* maszyny wirtualne Hello, same są dostępne za pośrednictwem sieci publicznej hello. Łączność z siecią bezpośrednie dla aplikacji hello działających w ramach hello toohello maszyn wirtualnych sieci albo firmy hello będący właścicielem zawartości pokazy lub szkolenia hello lokalnymi lub powitania klienta nie jest konieczne.
* W przypadku reprezentujący szkolenia hello lub scenariusza pokaz wielu maszyn wirtualnych sieci łączności i rozpoznawania nazw musi toowork między maszynami wirtualnymi hello. Jednak komunikacji między hello zestaw maszyn wirtualnych muszą toobe samodzielnie, tak aby kilka zestawów maszyn wirtualnych można wdrożyć obok siebie bez zakłóceń.  
* Połączenie z Internetem jest wymagany dla hello użytkownika końcowego tooremote logowania do toohello maszyn wirtualnych hostowana na platformie Azure. W zależności od system operacyjny gościa hello, służy usług terminalowych usług pulpitu zdalnego lub VNC/ssh tooaccess hello wirtualna tooeither spełnienia hello szkolenia zadań lub wykonywać pokazy hello. Jeśli SAP porty takich jak 3200, 3300 & 3600 może również być widoczne wystąpienia aplikacji hello SAP można uzyskać z dowolnego pulpitu połączonych Internet.
* Witaj systemy SAP (i reprezentują VM(s)) scenariusza autonomiczny na platformie Azure, który tylko wymaga łączności z Internetem publicznego dostępu użytkownika końcowego i nie wymaga połączenia tooother maszyn wirtualnych na platformie Azure.
* SAPGUI i przeglądarką są zainstalowane i uruchomić bezpośrednio na powitania maszyny Wirtualnej.
* Wymagana jest szybkie zresetowanie oryginalny stan toohello maszyny Wirtualnej i ponownie nowego wdrożenia tego oryginalnego stanu.
* W przypadku hello demo i scenariusze szkoleniowe, które są realizowane w wielu maszyn wirtualnych, usługi Active Directory / OpenLDAP i/lub DNS usługa jest wymagana dla każdego zestawu maszyn wirtualnych.

![Grupa maszyny Wirtualnej reprezentuje jeden pokaz lub szkolenia scenariusz usługi w chmurze platformy Azure][planning-guide-figure-200]

Ważne tookeep pamiętać, że hello wirtualne w każdym hello ustawia toobe należy wdrożyć równolegle, gdzie hello nazw maszyn wirtualnych w każdym zestawu hello są takie same hello jest.

### <a name="f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10"></a>Między różnymi lokalizacjami - wdrażania jednego lub wielu SAP maszyn wirtualnych na platformie Azure za pomocą wymóg hello jest w pełni zintegrowany hello sieci lokalnej
![Sieć VPN z połączeniem lokacja-lokacja (między lokalizacjami)][planning-guide-figure-300]

Ten scenariusz jest scenariusza między lokalizacjami z wielu wzorców możliwe wdrożenie rozwiązania. Może być tylko opisany jako działających na platformie Azure niektórych części hello SAP pozioma lokalnego i innymi częściami pakietu hello pozioma SAP. Wszystkie aspekty hello fakt, że część hello SAP składniki są uruchomione na platformie Azure powinna być niewidoczny dla użytkowników końcowych. Dlatego hello SAP transportu korekty systemu (STMS), komunikacja RFC drukowanie, zabezpieczeń (na przykład SSO), itp. współpracuje systemu SAP hello działających na platformie Azure. Ale scenariuszu obejmującym różne pomieszczenia hello również opisano scenariusz, w którym hello pełną SAP w orientacji poziomej działa na platformie Azure z domeną powitania klienta i rozszerzone DNS na platformie Azure.

> [!NOTE]
> Jest to hello scenariusz wdrażania, która jest obsługiwana w przypadku produktywności systemami SAP.
>
>

Odczyt [w tym artykule] [ vpn-gateway-create-site-to-site-rm-powershell] Aby uzyskać więcej informacji na temat tooconnect tooMicrosoft Azure sieci lokalnej

> [!IMPORTANT]
> Gdy firma Microsoft mówimy więc o scenariuszach między lokalizacjami między wdrożeniami klienta usługi Azure i lokalnymi, czekamy na powitania szczegółowości całego systemu SAP. Scenariusze, które są *nieobsługiwane* między lokalizacjami scenariusze są:
>
> * Uruchamianie różnych warstw aplikacje SAP w różne metody wdrażania. Na przykład uruchomiony hello DBMS warstwy lokalnej, ale warstwy aplikacji hello SAP w maszyn wirtualnych wdrożonych jako maszynach wirtualnych platformy Azure lub na odwrót.
> * Niektóre składniki warstwy SAP w Azure i niektórych lokalnych. Na przykład podzielić wystąpienia warstwy aplikacji SAP hello między lokalnymi i maszyn wirtualnych platformy Azure.
> * Rozkład maszyn wirtualnych uruchomionych wystąpień SAP jednego systemu w wielu regionach platformy Azure nie jest obsługiwane.
>
> Powodem Hello te ograniczenia jest wymaganie hello bardzo małych opóźnień sieci wysokiej wydajności w ramach jednego systemu SAP, szczególnie między wystąpieniami aplikacji hello i warstwy DBMS hello systemu SAP.
>
>

### <a name="supported-os-and-database-releases"></a>Obsługiwane systemu operacyjnego i wersji bazy danych
* Obsługiwane w przypadku usług maszyny wirtualnej platformy Azure to wymienione w tym artykule oprogramowanie serwera firmy Microsoft: <http://support.microsoft.com/kb/2721672>.
* Obsługiwane wersje systemu operacyjnego, obsługiwany na usługi na maszynie wirtualnej platformy Azure w połączeniu z oprogramowania SAP wydaniach systemu bazy danych są udokumentowane w artykule Uwaga SAP [1928533].
* Aplikacje SAP i wersje obsługiwane na usługi na maszynie wirtualnej Azure opisano w Uwaga SAP [1928533].
* Tylko 64-bitowych obrazów są obsługiwane toorun jako maszyny wirtualne gości na platformie Azure w scenariuszach SAP. Oznacza to również, że obsługiwane są tylko aplikacje SAP 64-bitowe i baz danych.

## <a name="microsoft-azure-virtual-machine-services"></a>Usługi Microsoft Azure na maszynie wirtualnej
Platforma Microsoft Azure Hello to internet skali w chmurze platformy usług hostowanych i zarządzane w danych firmy Microsoft centrów. Platforma Hello obejmuje usług hello Microsoft Azure maszyny wirtualnej (infrastruktura jako usługa lub IaaS) oraz zestaw zaawansowanych platformy jako usługa (PaaS) możliwości.

Hello platformy Azure ogranicza potrzebę hello początkowych technologii i zakupów infrastruktury. Takie rozwiązanie upraszcza utrzymania i działających aplikacji zapewniając toohost obliczeniowych i przestrzeni dyskowej na żądanie skalowania oraz zarządzanie nim połączonych aplikacji i aplikacji sieci web. Zarządzanie infrastrukturą jest zautomatyzowane przy użyciu platformy, które zaprojektowano pod kątem wysokiej dostępności i dynamiczne skalowanie toomatch potrzeby użycia z opcją hello z modelu cenowego.

![Pozycjonowanie usługi na maszynie wirtualnej platformy Microsoft Azure][planning-guide-figure-400]

Za pomocą usług Azure maszyny wirtualnej firmy Microsoft jest umożliwiając toodeploy serwera niestandardowe obrazy tooAzure jako wystąpień IaaS (patrz rysunek 4). Hello maszynach wirtualnych platformy Azure są oparte na funkcji Hyper-V wirtualnych dysków twardych (VHD) i są możliwe toorun różnych systemów operacyjnych jako systemu operacyjnego gościa.

Z perspektywy operacyjnej powitalne usługa maszyny wirtualnej Azure oferuje podobne napotyka jako maszyn wirtualnych wdrożonych lokalnie. Ma jednak hello postęp niepotrzebnych tooprocure, Administruj i Zarządzaj hello infrastruktury. Deweloperzy i Administratorzy mają pełną kontrolę nad hello obrazu systemu operacyjnego w ramach tych maszyn wirtualnych. Administratorzy mogą zdalnie zalogować się w toothose maszyn wirtualnych tooperform konserwację i rozwiązywanie problemów z zadaniami, jak również zadania wdrażania oprogramowania. W toodeployment uwzględniając ograniczenia tylko hello są hello rozmiary i możliwości maszyn wirtualnych platformy Azure. To może nie być poprawnie jako szczegółowe w konfiguracji, można to zrobić lokalnie. Brak wyboru stanową kombinację typów maszyny Wirtualnej:

* Liczba Vcpu,
* Pamięci,
* Liczba wirtualnych dysków twardych, które można dołączyć,
* Przepustowości sieci i magazynu.

rozmiar Hello i ograniczenia o różnych rozmiarach różnych maszyn wirtualnych oferowanych są widoczne w tabeli w [w tym artykule (Linux)] [ virtual-machines-sizes-linux] i [w tym artykule (system Windows)] [ virtual-machines-sizes-windows].

Jak można zrealizować, istnieją różnych rodzin lub serii maszyn wirtualnych. Można rozróżnić powitania po rodzin maszyn wirtualnych:

* Maszyna wirtualna a0 A7 typów: nie wszystkie te są certyfikowane dla SAP. Pierwszy serii maszyny Wirtualnej, która Azure IaaS otrzymano wprowadzone w systemie.
* Maszyna wirtualna a8 A11 typy: Wysoka wydajność przetwarzania danych wystąpienia. Uruchomione na różnych lepsze wykonywanie obliczeń hostów od innych maszyn wirtualnych, A-series.
* Typy Dv2-D-Series maszyny Wirtualnej: wykonywanie lepiej niż A0 A7. Nie wszystkie typy wirtualna hello certyfikowanych SAP.
* Typy serii DS/DSv2 maszyny Wirtualnej: podobne tooD/Dv2-series, ale są możliwe tooconnect tooAzure magazyn w warstwie Premium (zobacz rozdział [Azure Premium Storage] [ planning-guide-3.3.2] tego dokumentu). Ponownie certyfikowanych nie wszystkie typy maszyny Wirtualnej z programu SAP.
* Typy wirtualna serii G: typach maszyn wirtualnych o wysokiej pamięci.
* Typy serii GS maszyny Wirtualnej: jak serii G, ale tym toouse opcji hello Azure Premium Storage (zobacz rozdział [Azure Premium Storage] [ planning-guide-3.3.2] tego dokumentu). Korzystając z maszyn wirtualnych GS-Series jako serwery baz danych, jest obowiązkowe toouse magazyn w warstwie Premium dla pliki dziennika bazy danych i transakcji

Może się okazać hello takie same konfiguracje Procesora i pamięci w innej serii maszyn wirtualnych. Niemniej jednak gdy wyszukiwanie hello przepustowość tych maszyn wirtualnych z innej serii hello może różnią się one znacznie. Pomimo o hello sama konfiguracja procesora CPU i pamięci. Przyczyną jest to, że sprzętu hello do serwera źródłowego hosta na wprowadzenie hello hello różnych typów maszyny Wirtualnej ma parametry przepływności różne.  Zazwyczaj różnica hello pokazano przepustowość jest odzwierciedlenie w hello ceny hello różnych maszyn wirtualnych.

Nie wszystkie innej serii maszyn wirtualnych może być oferowana w każdej z nich hello regiony platformy Azure (dla następnego rozdziału Zobacz regiony platformy Azure). Wziąć pod uwagę, że nie wszystkie maszyny wirtualne lub serii maszyn wirtualnych są certyfikowane dla programu SAP.

> [!IMPORTANT]
> Użytku hello SAP NetWeaver na podstawie aplikacji tylko podzbioru hello typach maszyn wirtualnych i konfiguracji na liście Uwaga SAP [1928533] są obsługiwane.
>
>

### <a name="be80d1b9-a463-4845-bd35-f4cebdb5424a"></a>Regiony platformy Azure
Microsoft umożliwia toodeploy maszyn wirtualnych do tak zwany "regiony platformy Azure". Region platformy Azure może być jeden lub wiele centrów danych, które znajdują się w pobliżu. Dla większości hello geograficznymi regionów Witaj świecie Microsoft ma co najmniej dwóch regionach platformy Azure. Na przykład w Europie istnieje Region platformy Azure "Europa Północna" i jednym "Europa". Tych dwóch regionach platformy Azure w obrębie regionu geograficznymi są oddzielone odległość tyle istotne, aby awarii naturalnych i technicznych nie wpływają na obu regionów platformy Azure w hello tego samego regionu geograficznymi. Ponieważ Microsoft stopniowo buduje się nowych regionów platformy Azure w różnych regionach geograficznymi globalnie, hello liczba tych regionów stopniowo rośnie i począwszy od grudnia 2015 maksymalną hello liczbę 20 regiony platformy Azure z regionami dodatkowe ogłoszenia już. Klientów można wdrożyć systemy SAP do tych regionów, w tym hello dwa regiony platformy Azure w Chinach. Tę witrynę sieci Web dla bieżącego aktualne informacje na temat regiony platformy Azure: <https://azure.microsoft.com/regions/>

### <a name="8d8ad4b8-6093-4b91-ac36-ea56d80dbf77"></a>Witaj koncepcji programu Microsoft Azure maszyny wirtualnej
Microsoft Azure oferuje infrastrukturę jako toohost rozwiązania usługi (IaaS) maszyn wirtualnych z podobne funkcje jako rozwiązania do wirtualizacji lokalnymi. Jesteś stanie toocreate maszyn wirtualnych w ramach hello portalu Azure, programu PowerShell lub interfejsu wiersza polecenia, które oferują także wdrażania i możliwości zarządzania.

Usługa Azure Resource Manager umożliwia tooprovision aplikacji przy użyciu szablonu deklaracyjnego. Pojedynczy szablon umożliwia wdrożenie wielu usług wraz z ich zależnościami. Użyj hello tego samego szablonu toorepeatedly wdrożenia aplikacji podczas każdego etapu cyklu życia aplikacji hello.

Więcej informacji na temat przy użyciu szablonów usługi Resource Manager można znaleźć tutaj:

* [Wdrażania i zarządzania maszynami wirtualnymi przy użyciu szablonów usługi Azure Resource Manager i hello Azure CLI] [.. /.. / linux/create-ssh-secured-vm-from-template.md]
* [Zarządzanie maszynami wirtualnymi przy użyciu usługi Azure Resource Manager i programu PowerShell][virtual-machines-deploy-rmtemplates-powershell]
* <https://Azure.microsoft.com/Documentation/Templates/>

Inna funkcja interesujące jest hello możliwości toocreate obrazów z maszyn wirtualnych, co pozwala tooprepare pewność, że repozytoriów, z których mogą tooquickly można wdrożyć wystąpień maszyn wirtualnych, które spełniają wymagania.

Więcej informacji na temat tworzenia obrazów z maszyn wirtualnych można znaleźć w [w tym artykule (Linux)] [ virtual-machines-linux-capture-image-resource-manager] i [w tym artykule (system Windows)][virtual-machines-windows-capture-image-resource-manager].

#### <a name="df49dc09-141b-4f34-a4a2-990913b30358"></a>Domen błędów
Domen błędów reprezentują fizyczną jednostkę awarii, bardzo ściśle powiązane toohello infrastruktury fizycznej zawarte w centrach danych i gdy bloku fizycznego lub stojak jest uznawana za domeny błędów, nie istnieje żadne bezpośrednie mapowanie jeden do jednego między hello dwa.

Podczas wdrażania wielu maszyn wirtualnych w ramach jednego systemu SAP w usług Microsoft Azure maszyny wirtualnej, można określić toodeploy Kontroler sieci szkieletowej Azure hello aplikacji do różnych domen błędów, w tym samym spełniając wymagania hello hello Umowy SLA platformy Microsoft Azure. Jednak hello dystrybucji domen błędów przez jednostkę skalowania Azure (kolekcja setki węzłów obliczeniowych lub węzłów magazynu i sieci) lub przypisanie hello tooa maszyn wirtualnych jest określonej domeny błędów coś, w którym nie ma bezpośredni formantu. W kolejności toodirect hello sieci szkieletowej Azure kontrolera toodeploy zestaw maszyn wirtualnych w różnych domenach awarii należy tooassign toohello zestawu dostępności Azure maszyn wirtualnych w czasie wdrażania. Aby uzyskać więcej informacji dotyczących zestawami dostępności Azure, zobacz rozdział [zestawami dostępności Azure] [ planning-guide-3.2.3] w tym dokumencie.

#### <a name="fc1ac8b2-e54a-487c-8581-d3cc6625e560"></a>Domen uaktualnienia
Domen uaktualnienia reprezentują jednostki logicznej, która pomocy toodetermine sposób aktualizowania maszyny Wirtualnej w ramach systemu SAP, składający się z wystąpień SAP w wielu maszyn wirtualnych. W przypadku uaktualnienia Microsoft Azure przechodzi przez proces hello aktualizacji tych domen uaktualnienia pojedynczo. Dzięki rozproszeniu maszyn wirtualnych w czasie wdrażania w różnych domenach uaktualnienia, można chronić systemu SAP częściowo z potencjalny Przestój. W kolejności tooforce Azure toodeploy VMs hello systemu SAP zlokalizowane w różnych domenach uaktualnienia, należy tooset określony atrybut w czasie wdrażania każdej maszyny wirtualnej. Podobnych tooFault domen, jednostki skalowania Azure jest podzielony na wiele domen uaktualnienia. W kolejności toodirect hello sieci szkieletowej Azure kontrolera toodeploy zestaw maszyn wirtualnych w różnych domenach uaktualnienia należy tooassign toohello zestawu dostępności Azure maszyn wirtualnych w czasie wdrażania. Aby uzyskać więcej informacji dotyczących zestawami dostępności Azure, zobacz rozdział [zestawami dostępności Azure] [ planning-guide-3.2.3] poniżej.

#### <a name="18810088-f9be-4c97-958a-27996255c665"></a>Zestawy dostępności Azure
Maszyny wirtualne platformy Azure w ramach jednego zestawu dostępności Azure są dystrybuowane przy hello Kontroler sieci szkieletowej Azure za pośrednictwem różnych usterek i domen uaktualnienia. Celem Hello hello dystrybucji za pośrednictwem różnych awarii i uaktualniania domen jest tooprevent zamknięcia się wszystkich maszyn wirtualnych systemu SAP będą pracowały w przypadku hello konserwacja infrastruktury lub błąd w obrębie jednej domeny błędów. Domyślnie maszyny wirtualne nie są częścią zestawu dostępności. udział Hello maszyny wirtualnej w zestawie dostępności jest zdefiniowany w czasie wdrażania lub nowszego przez zmianę konfiguracji i ponownego wdrażania maszyny wirtualnej.

pojęcie hello toounderstand zestawami dostępności Azure i hello sposób zestawów dostępności odnoszą się tooFault i domen uaktualnienia, przeczytaj [w tym artykule][virtual-machines-manage-availability]

Zobacz toodefine zbiór dostępności dla ARM przy użyciu szablonu json [hello specyfikacji interfejsu api rest](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2015-06-15/swagger/compute.json) i wyszukaj "availability".

### <a name="a72afa26-4bf4-4a25-8cf7-855d6032157f"></a>Pamięć: Usługi Microsoft Azure Storage i dysków z danymi
Maszyny wirtualne Microsoft Azure korzystać z różnymi typami magazynów. Podczas implementowania SAP na usługi na maszynie wirtualnej Azure, jest ważne toounderstand hello różnice między tymi dwoma rodzajami głównego magazynu:

* Inne niż stałe i nietrwałe magazynu.
* Magazynu trwałego.

Magazyn nietrwałe Hello jest podłączonego bezpośrednio toohello uruchomionych maszyn wirtualnych i znajduje się na powitania obliczeń w poszczególnych węzłach — Witaj lokalne wystąpienie magazynu tymczasowego. rozmiar Hello zależy od rozmiaru hello hello maszyny wirtualnej podczas uruchamiania wdrożenia hello. Ten typ magazynu jest nietrwała i w związku z tym hello dysk został zainicjowany po ponownym uruchomieniu wystąpienia maszyny wirtualnej. Zazwyczaj plik stronicowania hello hello systemu operacyjnego znajduje się na tym dysku tymczasowym.

- - -
> ![Windows][Logo_Windows] Windows
>
> Na maszynach wirtualnych Windows hello tymczasowego dysk jest zainstalowany jako dysku D:\ w wdrożonej maszyny Wirtualnej.
>
> ![Linux][Logo_Linux] Linux
>
> Na maszynach wirtualnych systemu Linux jest zainstalowany jako /mnt/resource lub katalogu/mnt. Dowiedz się więcej tutaj:
>
> * [Jak tooAttach tooa dysku danych maszyny wirtualnej systemu Linux][virtual-machines-linux-how-to-attach-disk]
> * <https://docs.microsoft.com/Azure/Storage/Storage-About-Disks-and-vhds-Linux#Temporary-Disk>
>
>

- - -
dysku Hello jest nietrwałe, ponieważ jest wprowadzenie przechowywane na serwerze hosta hello sam. Jeśli przenoszona hello maszyny Wirtualnej w przypadku ponownego wdrażania (na przykład z powodu toomaintenance na hoście hello lub zamknięcia i ponownego uruchomienia) zawartości hello hello dysku zostaną utracone. W związku z tym nie jest opcja toostore wszystkich ważnych danych na tym dysku. Witaj typ nośnika użytego dla tego typu magazynu różni się od innej serii maszyn wirtualnych z bardzo różnych charakterystyki, których począwszy od czerwca 2015 wygląda jak:

* A5 A7: Bardzo ograniczony wydajności. Nie jest zalecane dla wszystkich elementów poza pliku stronicowania
* A8 A11: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > 1GB/s przepustowości.
* D-Series: Charakterystyki wydajności bardzo dobre z niektórych, a następnie tysięcy IOPS i > 1GB/s przepustowości.
* Seria DS: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > 1GB/s przepustowości.
* Seria G: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > 1GB/s przepustowości.
* GS-Series: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > 1GB/s przepustowości.

Instrukcje powyżej jest stosowane toohello wirtualna typy, które są certyfikowane z programu SAP. Hello serii maszyn wirtualnych z doskonałym IOPS i przepływności kwalifikować się do korzystanie przez niektóre funkcje systemu DBMS. Aby uzyskać więcej informacji, zobacz hello [DBMS Deployment Guide][dbms-guide].

Microsoft Azure Storage zapewnia utrwalonego magazynu i hello typowe poziomy ochrony i nadmiarowość widoczne w magazynie SAN. Dyski oparte na usłudze Azure Storage to wirtualny dysk twardy (VHD) znajduje się w usług magazynu Azure hello. Hello lokalny dysk systemu operacyjnego (Windows C:\, Linux/dev/sda1) znajduje się na powitania usługi Azure Storage i dodatkowych woluminów/dysków zainstalowanych toohello maszyny Wirtualnej pobrać przechowywane, za.

Jest możliwe tooupload istniejącego dysku VHD z lokalnymi lub utworzyć pusty, które były w obrębie platformy Azure i Dołącz te toodeployed maszyn wirtualnych.

Po utworzeniu lub przekazywanie wirtualnego dysku twardego do usługi Azure Storage, jest możliwe toomount i Dołącz te tooan istniejącej maszyny wirtualnej i toocopy istniejącego wirtualnego dysku twardego (odinstalowane).

W tych wirtualne dyski twarde są trwałe, danych i zmiany w tych są bezpieczne podczas ponownego uruchamiania i ponowne utworzenie wystąpienia maszyny wirtualnej. Nawet, jeśli wystąpienie zostanie usunięty, te wirtualne dyski twarde bezpieczeństwo i może zostać wdrożone lub w przypadku dysków z systemem innym niż systemu operacyjnego może być zainstalowany tooother maszyn wirtualnych.

W ramach hello można skonfigurować sieci poziomy różnych nadmiarowość magazynu Azure:

* Minimalny poziom, który można wybrać jest "nadmiarowość lokalnego", który jest równoważne toothree repliki danych hello hello tym samym centrum danych z regionu platformy Azure (zobacz rozdział [regiony platformy Azure][planning-guide-3.1]).
* Strefy nadmiarowego magazynu, które obrazy hello trzech widzące w różnych centrach danych w ramach hello tym samym regionie Azure.
* Domyślny poziom nadmiarowości jest nadmiarowości geograficznej, które asynchronicznie replikuje hello zawartości do innego trzy obrazy hello danych w innym regionie Azure, która jest hostowana w hello tego samego regionu geograficznymi.

Zobacz też hello tabeli u góry tego artykułu dotyczącej hello nadmiarowość różne opcje: <https://azure.microsoft.com/pricing/details/storage/>

Więcej informacji na temat usługi Azure Storage można znaleźć tutaj:

* <https://Azure.microsoft.com/Documentation/Services/Storage/>
* <https://Azure.microsoft.com/Services/Site-Recovery>
* <https://docs.microsoft.com/REST/API/storageservices/Understanding-Block-Blobs--append-Blobs--and-Page-Blobs>
* <https://blogs.msdn.com/b/azuresecurity/Archive/2015/11/17/Azure-Disk-Encryption-for-Linux-and-Windows-Virtual-Machines-Public-Preview.aspx>

#### <a name="azure-standard-storage"></a>Azure Standard Storage
Azure Standard storage był hello typu miejsca do magazynowania IaaS platformy Azure został zwolniony. Znaleziono IOPS limitami na jednym dysku. Opóźnienie wystąpił nie hello sama klasa urządzenia SAN/NAS zazwyczaj wdrażana wysokiej klasy systemów SAP obsługiwanego lokalnie. Niemniej jednak hello usługi Azure Standard Storage potwierdza, że wystarczające do kilkuset wiele systemów SAP, w tym samym czasie wdrożona na platformie Azure.

Dyski, które są przechowywane na standardowe konta magazynu Azure są naliczane na podstawie hello rzeczywistych danych przechowywanych, wielkość hello transakcji magazynowych, transfer danych wychodzących i nadmiarowość opcja wybrana. Można tworzyć wiele dysków na powitania maksymalną 1 TB, rozmiar, ale tak długo, jak te pozostać pusta nie bez dodatkowych opłat. Jeśli następnie uzupełnij jeden wirtualny dysk twardy z 100GB, naliczane są opłaty do przechowywania 100GB, a nie hello nominalny hello, które utworzono z wirtualnego dysku twardego.

#### <a name="ff5ad0f9-f7f4-4022-9102-af07aef3bc92"></a>Magazyn w warstwie Premium systemu Azure
W kwietnia 2015 r. Firma Microsoft wprowadziła Azure Premium Storage. Magazyn w warstwie Premium otrzymano wprowadzone w systemie tooprovide celem hello:

* Lepsze opóźnienia we/wy.
* Większa przepustowość.
* Mniejsza zmienność, opóźnienia we/wy.

W tym celu wiele zmian zostały wprowadzone, które Witaj dwie najważniejsze są:

* Użycie dysków SSD w hello węzłów magazynu Azure
* Nowe odczytu pamięci podręcznej, która nie jest obsługiwana przez hello lokalny dysk SSD węzła obliczeń platformy Azure

W przeciwnym magazynu tooStandard gdzie możliwości nie został zmieniony zależny od rozmiaru hello hello dysku (lub dysku VHD), Magazyn w warstwie Premium obecnie ma trzy kategorie inny dysk, które są wyświetlane w tym artykule: <https://azure.microsoft.com/ Cennik/szczegóły / / niezarządzany dysków w magazynie />

Zobacz, czy IOPS/dysku i przepływności/dysku są zależne od kategorii rozmiar hello hello dysków

Podstawa kosztu w przypadku hello magazyn w warstwie Premium nie jest woluminem danych rzeczywistych hello przechowywanych w tych dysków, ale kategorii rozmiar hello takiego dysku, niezależnie od ilości hello hello dane przechowywane na dysku hello.

Można również tworzyć dyski na magazyn w warstwie Premium nie są bezpośrednio mapowania na powitania rozmiar kategorie wyświetlane. Może to być przypadku hello, szczególnie w przypadku kopiowania dysków z magazynu w warstwie standardowa do magazyn w warstwie Premium. W takich przypadkach mapowania toohello dalej największy Premium dysku opcji magazynu jest wykonywane.

Należy pamiętać, że niektóre serii maszyn wirtualnych mogą korzystać z hello Azure Premium Storage. Począwszy od grudnia 2015 r. są hello i GS-serii DS. Hello serii DS jest zasadniczo hello takie same jak maszyn wirtualnych na podstawie D-series, z wyjątkiem hello czy serii DS ma toomount możliwości hello magazyn w warstwie Premium Ponadto toodisks, które są obsługiwane przez usługi Azure Standard Storage. Samo jest prawidłowa dla serii tooGS G-series porównywane.

Jeśli jest wyewidencjonowywany hello części maszyn wirtualnych hello serii DS w [w tym artykule (Linux)] [ virtual-machines-sizes-linux] i [w tym artykule (system Windows)][virtual-machines-sizes-windows], można zrealizować które istnieją dyski magazynu danych woluminu ograniczenia tooPremium na poziom szczegółowości hello hello poziom maszyny Wirtualnej. Innej serii DS lub GS-series maszyn wirtualnych także mieć różne ograniczenia w zakresie toohello liczba dysków z danymi, które można zainstalować. Ograniczenia te są udokumentowane w artykule hello również wymienionych powyżej. Jednak w zasadzie oznacza to, że jeśli, na przykład zainstalować 32 tooa dysków x P30 pojedyncze maszyny DS14 nie Ci 32 x hello maksymalną przepływność dysku P30. Zamiast tego hello maksymalną przepustowość na poziomie maszyny Wirtualnej zgodnie z opisem w hello artykułu limity przepustowość.

Więcej informacji na temat magazyn w warstwie Premium można znaleźć tutaj: <http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2>

#### <a name="c55b2c6e-3ca1-4476-be16-16c81927550f"></a>Dyski zarządzane
Dyski zarządzane są nowego typu zasobu w usłudze Azure Resource Manager używany zamiast wirtualne dyski twarde, które są przechowywane na kontach magazynu Azure. Dyski zarządzane automatycznie wyrównuje z hello zestawu dostępności maszyny wirtualnej hello, są one dołączone tooand w związku z tym wzrost hello dostępności maszyny wirtualnej i hello usług, które są uruchomione na maszynie wirtualnej hello. Aby uzyskać więcej informacji, przeczytaj hello [artykuł z omówieniem](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview).

Firma Microsoft zaleca użycie tooyou dysk zarządzany, ponieważ uprościć ich hello wdrażania i zarządzania maszyn wirtualnych.
SAP aktualnie obsługuje tylko dysków zarządzanych w warstwie Premium. Aby uzyskać więcej informacji, przeczytaj Uwaga SAP [1928533].

#### <a name="azure-storage-accounts"></a>Konta usługi Azure Storage
W przypadku wdrażania usług lub maszynami wirtualnymi na platformie Azure, wdrożenie wirtualne dyski twarde i obrazów maszyn wirtualnych można organizować w jednostki o nazwie konta magazynu Azure. Podczas planowania wdrożenia usługi Azure, należy toocarefully należy wziąć pod uwagę ograniczenia hello Azure. Po jednej stronie powitania istnieje ograniczona liczba kont magazynu dla subskrypcji platformy Azure. Mimo że każdego konta magazynu Azure może zawierać dużą liczbę plików VHD, na powitania jest stały limit łączna liczba IOPS dla konta magazynu. W przypadku wdrażania setki SAP maszyn wirtualnych z systemami DBMS tworzenia znaczących wywołań we/wy, jest zalecane toodistribute wysokiej maszyn wirtualnych systemu DBMS IOPS między wieloma kontami magazynu Azure. Należy zachować ostrożność nie tooexceed hello bieżący limit kont magazynu Azure dla subskrypcji. Ponieważ Magazyn jest to ważna część hello wdrażania bazy danych systemu SAP, to pojęcie omówiono bardziej szczegółowo w hello już odwołanie [DBMS Deployment Guide][dbms-guide].

Więcej informacji o kontach magazynu Azure można znaleźć w [w tym artykule][storage-scalability-targets]. Odczyt w tym artykule, okazuje się, czy ma różnic w ograniczenia hello standardowe konta magazynu Azure i kont magazynu w warstwie Premium. Najważniejsze różnice są hello ilość danych, które mogą być przechowywane w ramach konta magazynu. W magazynie standardowe hello wolumin jest wielkości większy niż z magazyn w warstwie Premium. Na powitania drugiej stronie powitania standardowe konto magazynu jest znacznie ograniczone IOPS (zobacz kolumnę "Całkowita liczba żądań"), takie ograniczenie nie ma hello konta magazynu Azure Premium. Omówimy szczegóły oraz wyniki tych różnic w opisach wdrożenia hello systemów SAP, zwłaszcza na serwerach systemu DBMS hello.

W ramach konta magazynu masz hello możliwości toocreate różnych kontenerów hello w celu organizowania i klasyfikacji różnych wirtualne dyski twarde. Kontenery są zwykle używane do, na przykład oddzielnych wirtualne dyski twarde różnych maszyn wirtualnych. Nie ma wpływu na wydajność przy użyciu kontenera tylko jednego lub wielu kontenerów poniżej jedno konto magazynu Azure.

W systemie Azure Nazwa wirtualnego dysku twardego następujące powitania po nazewnictwa połączenie, które musi tooprovide unikatową nazwę hello wirtualnego dysku twardego w obrębie platformy Azure:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Jako ciąg hello wymienionych powyżej toouniquely musi zidentyfikować hello wirtualnego dysku twardego, który jest przechowywany w magazynie Azure.

### <a name="61678387-8868-435d-9f8c-450b2424f5bd"></a>Sieć platformy Microsoft Azure
Microsoft Azure udostępnia infrastrukturę sieci, dzięki czemu hello mapowanie wszystkie scenariusze, które chcemy toorealize przy użyciu oprogramowania SAP. możliwości Hello są:

* Dostęp z hello poza bezpośrednio toohello maszyn wirtualnych za pomocą usług terminalowych systemu Windows lub ssh/VNC
* Tooservices dostępu i określone porty używane przez aplikacje w hello maszyny wirtualne
* Wewnętrznej komunikacji i rozpoznawanie nazw między grupą maszyn wirtualnych wdrożonych jako maszynach wirtualnych platformy Azure
* Łączność między lokalizacjami sieci lokalnej klienta i hello sieć platformy Azure
* Krzyżowe regionu Azure lub łączności centrum danych między lokacjami systemu Azure

Więcej informacji można znaleźć tutaj: <https://azure.microsoft.com/documentation/services/virtual-network/>

Istnieje wiele różnych możliwości tooconfigure nazwy i rozpoznawania adresu IP na platformie Azure. W tym dokumencie scenariusze tylko w chmurze korzystają z domyślną hello przy użyciu usługi Azure DNS (w toodefining kontrastu własne usługi DNS). Istnieje również nową usługę Azure DNS, którego można użyć zamiast konfigurowania serwera DNS. Więcej informacji można znaleźć w [w tym artykule] [ virtual-networks-manage-dns-in-vnet] i na [tej strony](https://azure.microsoft.com/services/dns/).

W scenariuszach między różnymi lokalizacjami, możemy zależne fakt hello tego hello lokalnymi DNS-AD/OpenLDAP został rozszerzony za pośrednictwem sieci VPN lub tooAzure prywatną. Dla niektórych scenariuszy zgodnie z opisem w tym miejscu, może być konieczne toohave repliki AD/OpenLDAP zainstalowane na platformie Azure.

Ponieważ sieci i rozpoznawanie nazw jest to ważna część hello wdrażania bazy danych systemu SAP, to pojęcie omówiono bardziej szczegółowo w hello [DBMS Deployment Guide][dbms-guide].

##### <a name="azure-virtual-networks"></a>Sieci wirtualne platformy Azure
Przez tworzenie sieci wirtualnej platformy Azure, można określić zakres adresów hello hello przydzielonej przez funkcje protokołu DHCP Azure prywatnych adresów IP. W scenariuszach między różnymi lokalizacjami zakres adresów IP hello zdefiniowane wciąż jest przydzielony przy użyciu protokołu DHCP przez platformę Azure. Jednak rozpoznawania nazw domeny odbywa się lokalnie (przy założeniu, że maszyny wirtualne hello są częścią domeny lokalnej) i dlatego można rozwiązać adresów poza różnych usługach w chmurze Azure.

Każdej maszyny wirtualnej w toobe potrzeb Azure połączone tooa sieci wirtualnej.

Więcej informacji można znaleźć w [w tym artykule] [ resource-groups-networking] i na [tej strony](https://azure.microsoft.com/documentation/services/virtual-network/).

[comment]: <> (MShermannd TODO można znaleźć artykuł, w tym temacie OpenLDAP hello + ARM;)
[comment]: <> (MSSedusch < https://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL>)

> [!NOTE]
> Domyślnie po wdrożeniu maszyny Wirtualnej nie można zmienić hello konfiguracji sieci wirtualnej. ustawienia TCP/IP Hello musi pozostać toohello serwera Azure DHCP. Domyślnym zachowaniem jest przypisanie dynamicznego adresu IP.
>
>

adres MAC karty sieci wirtualnej hello Hello mogą ulec zmianie, na przykład po zmiany rozmiaru i systemu Windows hello lub system operacyjny gościa Linux przejmuje hello nowej karty sieciowej i automatycznie używa w tym przypadku DHCP tooassign hello adresów IP i DNS.

##### <a name="static-ip-assignment"></a>Przypisanie statycznego adresu IP
Jest to możliwe tooassign stałej lub zarezerwowane adresy IP tooVMs w ramach sieci wirtualnej platformy Azure. Działających maszyn wirtualnych hello w sieci wirtualnej platformy Azure otwiera tooleverage doskonałe możliwości tej funkcji, jeśli wymagane lub wymagane w przypadku niektórych scenariuszy. Przypisanie IP Hello pozostaje ważny w całym hello istnienie hello maszyny Wirtualnej, niezależnie od czy hello maszyna wirtualna jest uruchomiona lub zamknięcie. W związku z tym należy tootake hello ogólną liczbę maszyn wirtualnych (maszyny Wirtualne uruchomione i zatrzymane) pod uwagę podczas definiowania hello zakres adresów IP dla hello sieci wirtualnej. adres IP Hello jest przypisana do momentu usunięcia hello maszyny Wirtualnej i jej interfejsu sieciowego lub dopóki adres IP hello cofnąć pobiera ponownie przypisany. Aby uzyskać więcej informacji, przeczytaj [w tym artykule][virtual-networks-static-private-ip-arm-pportal].

##### <a name="multiple-nics-per-vm"></a>Wiele kart sieciowych dla maszyny Wirtualnej
Można zdefiniować wiele karty interfejsu sieci wirtualnej (vNIC) dla maszyny wirtualnej platformy Azure. Toohave możliwości hello wielu vNICs można rozpocząć tooset się rozdzielenie ruchu sieci where, na przykład klienta ruch jest kierowany przez jeden vNIC i zaplecza, ruch jest kierowany przez vNIC drugiego. W zależności od typu hello maszyny wirtualnej są różne ograniczenia w odniesieniu do liczby toohello vNICs. Dokładne szczegóły, funkcje i ograniczenia można znaleźć w następujących artykułach:

* [Tworzenie maszyny Wirtualnej systemu Windows z wieloma kartami sieciowymi][virtual-networks-multiple-nics-windows]
* [Utwórz Maszynę wirtualną systemu Linux z wieloma kartami sieciowymi][virtual-networks-multiple-nics-linux]
* [Wdrażanie maszyn wirtualnych kart Sieciowych multi przy użyciu szablonu][virtual-network-deploy-multinic-arm-template]
* [Wdrażanie maszyn wirtualnych kart Sieciowych multi przy użyciu programu PowerShell][virtual-network-deploy-multinic-arm-ps]
* [Wdrażanie maszyn wirtualnych kart Sieciowych multi przy użyciu hello Azure CLI][virtual-network-deploy-multinic-arm-cli]

#### <a name="site-to-site-connectivity"></a>Połączenie lokacja lokacja
Między lokalizacjami jest maszynach wirtualnych platformy Azure i lokalnymi połączone przejrzyste i trwałe połączenie sieci VPN. Jest oczekiwany toobecome hello najczęściej SAP wzorca wdrażania na platformie Azure. Witaj zakłada się, że procedury działania i procesy z wystąpieniem SAP na platformie Azure powinny działać przezroczysty. Oznacza to, możesz powinny być możliwe tooprint poza tymi systemami, a także użyć powitalne tootransport System zarządzania transportu SAP (TMS) zmieni się z systemu Programowanie w systemie testu Azure tooa, w którym jest wdrożony na lokalnym. Więcej dokumentacji wokół lokacja lokacja można znaleźć w [w tym artykule][vpn-gateway-create-site-to-site-rm-powershell]

##### <a name="vpn-tunnel-device"></a>Urządzenia tunel sieci VPN
W kolejności toocreate połączenie lokacja lokacja (lokalnego Centrum tooAzure danych centrum danych), należy tooeither uzyskać i skonfiguruj urządzenie sieci VPN lub użyj usługi Routing i dostęp zdalny (RRAS), która została wprowadzona jako składnik oprogramowania w systemie Windows Server 2012.

* [Tworzenie sieci wirtualnej za pomocą połączenia sieci VPN lokacja lokacja za pomocą programu PowerShell][vpn-gateway-create-site-to-site-rm-powershell]
* [O urządzeniach sieci VPN dla połączenia bramy sieci VPN typu lokacja-lokacja][vpn-gateway-about-vpn-devices]
* [Brama sieci VPN — często zadawane pytania][vpn-gateway-vpn-faq]

![Połączenie lokacja lokacja między lokalną i platformą Azure][planning-guide-figure-600]

Hello powyższej ilustracji przedstawiono dwie subskrypcji platformy Azure ma podzakresów adres IP zarezerwowany do użycia w sieciach wirtualnych platformy Azure. Witaj łączności z hello w lokalnym tooAzure sieci jest nawiązywane za pośrednictwem sieci VPN.

#### <a name="point-to-site-vpn"></a>Sieć VPN punkt lokacja
Sieć VPN punkt lokacja wymaga tooconnect maszyny każdego klienta z własną siecią VPN na platformie Azure. Scenariusze SAP hello czekamy na połączenie punkt lokacja nie jest praktyczne. W związku z tym nie dalsze odwołania są podane połączenie z siecią VPN toopoint do lokacji.

Więcej informacji można znaleźć tutaj
* [Skonfiguruj tooa połączenie punkt-lokacja sieci wirtualnej przy użyciu hello portalu Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
* [Skonfiguruj tooa połączenie punkt-lokacja sieci wirtualnej przy użyciu programu PowerShell](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

#### <a name="multi-site-vpn"></a>Obejmujący wiele lokacji sieci VPN
System Azure oferuje również dzisiaj hello możliwości toocreate obejmujący wiele lokacji połączenie z siecią VPN dla jedną subskrypcją platformy Azure. Wcześniej jednej subskrypcji został połączenia sieci VPN lokacja lokacja tooone ograniczone. To ograniczenie zostało usunięte z połączenia sieci VPN z wieloma lokacjami dla jednej subskrypcji. Dzięki temu możliwe tooleverage więcej niż jeden Region platformy Azure dla określonej subskrypcji za pomocą konfiguracji między lokalizacjami.

Więcej informacji dotyczących dokumentacji, zobacz [w tym artykule][vpn-gateway-create-site-to-site-rm-powershell]

[comment]: <> (MShermannd TODO nie znaleziono żadnego łącza doku ARM)

#### <a name="vnet-toovnet-connection"></a>Sieć wirtualna tooVNet połączenia
Przy użyciu sieci VPN w wielu lokacjach, należy tooconfigure oddzielnej sieci wirtualnych Azure w regionach hello. Należy jednak bardzo często wymaganie hello, które składniki oprogramowania hello w różnych regionach hello skontaktować się ze sobą. Najlepszym rozwiązaniem tej komunikacji powinny być kierowane z jednego regionu Azure tooon lokalnych i występują toohello inny Region platformy Azure. tooshortcut, system Azure oferuje hello tooconfigure możliwość połączenia z jedną sieć wirtualną platformy Azure w jednym tooanother regionu Azure Virtual Network hostowana w innym regionie. Ta funkcja jest wywoływana połączenia do wirtualnymi. Więcej informacji na temat tej funkcji można znaleźć tutaj: <https://azure.microsoft.com/documentation/articles/vpn-gateway-vnet-vnet-rm-ps/>.

#### <a name="private-connection-tooazure--expressroute"></a>Prywatne tooAzure połączenia — ExpressRoute
Microsoft Azure ExpressRoute umożliwia tworzenie hello prywatnych połączeń między centrach danych platformy Azure i infrastruktury lokalnej klienta albo hello lub w środowisku wspólnej lokalizacji. ExpressRoute jest oferowanych przez różnych MPLS dostawców sieci VPN (przełączaniem pakietów) lub innych dostawców usług sieciowych. Połączenia ExpressRoute nie został przekroczony hello publicznej sieci Internet. Połączenia ExpressRoute oferują wyższy poziom zabezpieczeń, niezawodności więcej za pomocą wielu równoległych obwodów, szybkości szybsze i opóźnienia niższa niż typowe połączenia za pośrednictwem hello Internet.

Znajdź więcej informacji na temat usługi Azure ExpressRoute i ofert tutaj:

* <https://Azure.microsoft.com/Documentation/Services/expressroute/>
* <https://Azure.microsoft.com/pricing/details/expressroute/>
* <https://Azure.microsoft.com/Documentation/articles/expressroute-FAQs/>

Usługi Express Route umożliwia wielu subskrypcji platformy Azure za pośrednictwem jednego obwodu ExpressRoute, zgodnie z opisem w tym miejscu

* <https://Azure.microsoft.com/Documentation/articles/expressroute-howto-linkvnet-ARM/>
* <https://Azure.microsoft.com/Documentation/articles/expressroute-howto-Circuit-ARM/>

#### <a name="forced-tunneling-in-case-of-cross-premises"></a>Wymuszone tunelowanie w przypadku między lokalizacjami
Dla maszyn wirtualnych, przyłączanie do domeny lokalnej za pośrednictwem lokacja lokacja, punkt lokacja lub ExpressRoute należy się, że ustawienia serwera proxy Internet hello są pobierania wdrożony dla wszystkich użytkowników hello na tych maszynach wirtualnych oraz toomake. Domyślnie oprogramowania uruchomionego w tych maszyn wirtualnych lub użytkowników korzystających z przeglądarki hello tooaccess internet nie przejdzie za pośrednictwem serwera proxy firmy hello, ale będzie łączyć się bezpośrednio za pośrednictwem Azure toohello przez internet. Ale ustawienie serwera proxy hello nawet nie jest rozwiązanie 100% toodirect hello ruchu za pośrednictwem serwera proxy firmy hello, ponieważ jest odpowiedzialny za toocheck oprogramowania i usług na powitania serwera proxy. Jeśli oprogramowanie uruchomione w hello maszyny Wirtualnej nie jest operacją lub administrator zmienia ustawienia hello, toohello ruchu internetowego można ponownie detoured bezpośrednio za pomocą usługi Azure toohello Internet.

To zamówienie tooavoid, tunelowanie wymuszone można skonfigurować połączenia lokacja lokacja między lokalną i platformą Azure. Witaj szczegółowy opis funkcji tunelowania wymuszonego hello zostanie opublikowana tutaj <https://azure.microsoft.com/documentation/articles/vpn-gateway-forced-tunneling-rm/>

Tunelowanie wymuszone z ExpressRoute jest włączana przez klientów anonsuje trasę domyślną za pośrednictwem hello BGP usługi ExpressRoute sesje komunikacji równorzędnej.

#### <a name="summary-of-azure-networking"></a>Podsumowanie sieci platformy Azure
Ten rozdział zawiera wiele ważne kwestie dotyczące sieci platformy Azure. Poniżej przedstawiono podsumowanie głównych punktów hello:

* Sieci wirtualnych platformy Azure umożliwia tooset sieć hello zgodnie z tooyour własnych potrzeb
* Można tooVMs zakresów adresów IP wykorzystywana tooassign lub przypisać stałym tooVMs adresów IP sieci wirtualnych platformy Azure
* tooset lokacja-lokacja lub połączenia punkt-lokacja należy najpierw toocreate sieci wirtualnej platformy Azure
* Po wdrożeniu maszyny wirtualnej nie jest już możliwe toochange powitalne sieci wirtualnej przypisane toohello maszyny Wirtualnej

### <a name="quotas-in-azure-virtual-machine-services"></a>Przydziały w usługach Azure maszyny wirtualnej
Firma Microsoft muszą toobe wyczyść o fakt hello hello magazynu i infrastruktury sieci jest współużytkowana przez maszyny wirtualne z systemami wielu usług w hello infrastruktury platformy Azure. I tak jak w przypadku centrów danych przez klienta hello, przerostu niektórych zasobów infrastruktury hello Przełącz miejsce tooa stopnia. Witaj platformy Microsoft Azure korzysta z dysku, Procesora, sieci i innych zużycie zasobów hello toolimit przydziały i toopreserve spójne i deterministyczna wydajności.  Witaj różnych typach maszyn wirtualnych (A5, A6 itp.) mają różne przydziały hello liczbę dysków, Procesora, pamięci RAM i sieci.

> [!NOTE]
> Zasoby Procesora i pamięci hello wirtualna typów obsługiwanych w SAP są wstępnie przydzielić na węzłach hostów hello. Oznacza to, że po wdrożeniu maszyny Wirtualnej hello hello na hoście hello dostępnych zasobów zgodnie z definicją hello typu maszyny Wirtualnej.
>
>

Należy uwzględnić podczas planowania i zmiany rozmiaru SAP rozwiązania Azure hello przydziały dla każdego rozmiaru maszyny wirtualnej. przydziały wirtualna Hello są opisane [(Linux) w tym miejscu] [ virtual-machines-sizes-linux] i [tutaj (system Windows)][virtual-machines-sizes-windows].

przydziały Hello opisane reprezentują hello teoretycznego maksymalne wartości.  limit Hello iops dla każdego dysku może zostać osiągnięty przy małych IOs (8kb), ale prawdopodobnie nie może zostać osiągnięty przy dużych IOs (1Mb).  Hello IOPS limit są wymuszane na poziom szczegółowości hello jednego dysku.

Jako toodecide drzewa decyzyjnego nierównej czy systemu SAP dopasowuje się do usług Azure maszyny wirtualnej i jej możliwości, lub czy istniejący system wymaga toobe inaczej skonfigurowana w kolejności toodeploy hello systemu Azure, drzewa decyzyjnego hello poniżej można:

![Decyzja drzewa toodecide możliwości toodeploy SAP na platformie Azure][planning-guide-figure-700]

**Krok 1**: hello najważniejszych informacji toostart z jest hello protokoły SAP wymagane dla danego systemu SAP. Protokoły SAP Hello wymagania potrzeby toobe dzielony hello DBMS i część hello SAP aplikacji, nawet jeśli hello systemu SAP jest już wdrożona lokalnie w konfiguracji warstwy 2. Istniejących systemów hello protokoły SAP związane z toohello sprzętu często można ustalić lub szacowany na podstawie istniejących testów porównawczych SAP. wyniki Hello można znaleźć tutaj: <http://global.sap.com/campaigns/benchmark/index.epx>.
W nowo wdrożonym systemach SAP powinien przejściu ćwiczeniu zmiany rozmiaru powinien ustalić wymagania protokoły SAP hello hello systemu.
Zobacz też ten blog i dołączonego dokumentu dla programu SAP rozmiaru na platformie Azure: <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

**Krok 2**: istniejących systemów hello We/Wy woluminu i powinno być mierzone na operacje We/Wy na sekundę na powitania serwera systemu DBMS. Dla nowo planowane systemów hello zmiany rozmiaru wykonywania do nowego systemu hello również nadać nierównej pomysły hello wymagań operacji We/Wy na powitania po stronie systemu DBMS. Jeśli nie wiesz, należy po pewnym czasie tooconduct Weryfikacja koncepcji.

**Krok 3**: wymaganie protokoły SAP hello Porównaj hello zapewniają bazami danych serwera z hello protokoły SAP hello wirtualna różnego rodzaju Azure. informacje Hello na protokoły SAP hello różnych typów maszyny Wirtualnej platformy Azure jest udokumentowany uwagi SAP [1928533]. Hello należy się skoncentrować na powitania maszyny Wirtualnej systemu DBMS najpierw ponieważ hello Warstwa bazy danych to warstwa hello w systemie SAP NetWeaver, która nie skalować w poziomie w hello większości wdrożeń. Z kolei warstwy aplikacji hello SAP może być skalowana w poziomie. Jeśli żaden z hello SAP obsługiwane typy maszyn wirtualnych Azure zapewnia protokoły SAP hello wymagane, hello obciążenie systemu SAP hello planowane nie można uruchomić na platformie Azure. Należy albo toodeploy hello systemu lokalnego lub należy toochange hello obciążenia woluminu systemu hello.

**Krok 4**: zgodnie z opisem [(Linux) w tym miejscu] [ virtual-machines-sizes-linux] i [tutaj (system Windows)][virtual-machines-sizes-windows], Azure wymusza przydziału IOPS dla każdego dysku niezależne, czy używać magazynu w warstwie standardowa lub Premium Storage. Zależne od hello typu maszyny Wirtualnej, hello liczba dysków danych, które można zainstalować zależy. W związku z tym można obliczyć maksymalną liczbę IOPS, który może zostać osiągnięty przy każdej hello różnych typach maszyn wirtualnych. Zależne od układ pliku hello bazy danych, można paskowych dysków toobecome jednego woluminu w system operacyjny gościa hello. Jednak jeśli hello bieżącego woluminu IOPS wdrożonego systemu SAP przekracza limity hello obliczana typu hello największy maszyny Wirtualnej systemu Azure i jeśli nie ma żadnych toocompensate szansy więcej pamięci, obciążenie hello hello systemu SAP może to dotyczyć poważnie. W takich przypadkach można trafiony punkt, w których nie należy wdrażać hello systemu Azure.

**Krok 5**: szczególnie w systemach SAP, które są wdrożone lokalnie w konfiguracji warstwy 2, hello prawdopodobnie czy hello systemu może być konieczne toobe skonfigurowane na platformie Azure w konfiguracji warstwy 3. W tym kroku należy toocheck czy składnik hello SAP aplikacji warstwy, która nie może być skalowana w poziomie, a nie mieści się który w hello procesora CPU i pamięci zasobów hello inną ofertę typów maszyny Wirtualnej platformy Azure. Jeśli w rzeczywistości jest takich składników, systemu SAP hello i jego obciążenie nie można wdrożyć na platformie Azure. Ale jeśli można skalować w poziomie składników aplikacji hello SAP do wielu maszyn wirtualnych platformy Azure, hello system można wdrożyć na platformie Azure.

**Krok 6**: Jeśli hello DBMS i składników warstwy aplikacji SAP mogą być uruchamiane na maszynach wirtualnych Azure, hello należy toobe zdefiniowane w odniesieniu do:

* Liczba maszyn wirtualnych platformy Azure
* Typy maszyn wirtualnych dla poszczególnych składników hello
* Liczba wirtualnych dysków twardych w tooprovide maszyny Wirtualnej systemu DBMS wystarczającej liczby IOPS

## <a name="managing-azure-assets"></a>Zarządzanie zasobami Azure
### <a name="azure-portal"></a>Azure Portal
Witaj portalu Azure jest jednym z trzech wdrożenia maszyny Wirtualnej Azure toomanage interfejsów. Hello zadania podstawowe możliwości zarządzania, takich jak wdrażanie maszyn wirtualnych z obrazów, można wykonać za pomocą hello portalu Azure. Ponadto hello tworzenie kont magazynu, sieci wirtualnych i inne składniki platformy Azure są również zadania hello portalu Azure może obsługiwać bardzo dobrze. Jednak funkcji takich jak przekazywanie wirtualne dyski twarde z lokalnymi tooAzure lub kopiowanie dysku VHD w obrębie platformy Azure są zadania, które wymagają narzędzi innych firm lub administrowanie przy użyciu programu PowerShell lub interfejsu wiersza polecenia.

![Portal Microsoft Azure — omówienie maszyny wirtualnej][planning-guide-figure-800]

[comment]: <> (MSSedusch * < https://azure.microsoft.com/documentation/articles/virtual-networks-create-vnet-arm-pportal/>)
[comment]: <> (MSSedusch * < https://azure.microsoft.com/documentation/articles/virtual-machines-windows-tutorial/>)

Zadania zarządzania i konfiguracji dla wystąpienia maszyny wirtualnej hello są możliwe z wewnątrz hello portalu Azure.

Oprócz ponowne uruchamianie i zamykanie maszyny wirtualnej można również dołączyć, odłączyć i tworzyć dyski danych dla wystąpienia maszyny wirtualnej hello wystąpienia hello toocapture przygotowania obrazu i skonfiguruj rozmiar hello hello wystąpienie maszyny wirtualnej.

Hello Azure portal udostępnia podstawowe funkcje toodeploy i konfigurowanie maszyn wirtualnych i wiele innych usług Azure. Jednak nie wszystkie dostępne funkcje jest objęta hello portalu Azure. W portalu Azure hello nie jest możliwe tooperform zadania, takie jak:

* Przekazywanie tooAzure wirtualne dyski twarde
* Kopiowanie maszyn wirtualnych

[comment]: <> (MShermannd TODO co temat automatyzacji usługi dla maszyn wirtualnych SAP?)
[comment]: <> (MSSedusch wdrażania wielu maszyn wirtualnych systemu operacyjnego w tym samym czasie możliwe)
[comment]: <> (MSSedusch również dowolnego typu automatyzacji dotyczące wdrożenia nie jest możliwe z hello portalu Azure. Zadania, takie jak inicjowanych przez skrypty wdrażania wielu maszyn wirtualnych nie jest możliwe za pośrednictwem hello portalu Azure.)

### <a name="management-via-microsoft-azure-powershell-cmdlets"></a>Zarządzanie za pomocą poleceń cmdlet programu PowerShell usługi Microsoft Azure
Windows PowerShell to zaawansowany i rozszerzalny platforma, która ma zostały powszechnie zaakceptowany przez klientów wdrażanie większej liczby systemów na platformie Azure. Po zakończeniu instalacji hello poleceń cmdlet programu PowerShell na pulpitu, laptopów i dedykowanych stację można zdalnie uruchamiać hello poleceń cmdlet programu PowerShell.

Witaj tooenable proces lokalny pulpitu/laptop hello użycia poleceń cmdlet programu Azure PowerShell i jak tooconfigure hello dotyczące użycia za pomocą hello Azure subskrypcji jest opisany w [w tym artykule][powershell-install-configure].

Bardziej szczegółowy opis kroków w sposób tooinstall, aktualizacji i skonfiguruj poleceń cmdlet programu Azure PowerShell hello można znaleźć w [ten rozdział hello Deployment Guide][deployment-guide-4.1].

Obsługi klienta do tej pory została środowiska PowerShell (PS) czy na pewno hello bardziej zaawansowanych narzędzi toodeploy maszyn wirtualnych i toocreate niestandardowych kroków hello podczas wdrażania maszyn wirtualnych. Wszyscy klienci hello uruchomione wystąpienia programu SAP na platformie Azure używają PS poleceń cmdlet toosupplement zadań zarządzania w portalu Azure hello lub nawet przy użyciu poleceń cmdlet środowiska PS wyłącznie toomanage wdrożeń na platformie Azure. Ponieważ hello Azure dotyczące polecenia cmdlet udziału hello sam konwencji nazewnictwa jak hello ponad 2000 polecenia cmdlet związane z systemem Windows, jest łatwe zadań systemu Windows administratorów tooleverage tych poleceń cmdlet.

Zobacz przykład tutaj: <http://blogs.technet.com/b/keithmayer/archive/2015/07/07/18-steps-for-end-to-end-iaas-provisioning-in-the-cloud-with-azure-resource-manager-arm-powershell-and-desired-state-configuration-dsc.aspx>

[comment]: <> (MShermannd TODO opisano nowe polecenia interfejsu wiersza polecenia podczas testowania)
Wdrożenie hello Azure rozszerzenie monitorowania dla programu SAP (zobacz rozdział [rozwiązanie monitorowanie Azure dla programu SAP] [ planning-guide-9.1] w tym dokumencie) jest możliwe tylko za pomocą programu PowerShell lub interfejsu wiersza polecenia. W związku z tym jest obowiązkowy tooset w górę i konfigurowanie programu PowerShell lub interfejsu wiersza polecenia podczas wdrażania i administrowania systemem SAP NetWeaver na platformie Azure.  

Jako platforma Azure oferuje więcej funkcji, nowe polecenia cmdlet PS będą toobe dodać, który wymaga aktualizacji hello poleceń cmdlet. W związku z tym ułatwia wykrywanie toocheck hello Azure Pobierz lokacji co najmniej raz na miesiąc hello <https://azure.microsoft.com/downloads/> nowej wersji hello poleceń cmdlet. Nowa wersja Hello zostanie zainstalowana na powitania starszej wersji.

Listę ogólne dotyczące usługi Azure PowerShell polecenia Sprawdź tutaj: <https://docs.microsoft.com/powershell/azure/overview>.

### <a name="management-via-microsoft-azure-cli-commands"></a>Zarządzanie za pomocą polecenia interfejsu wiersza polecenia programu Microsoft Azure
Dla klientów, którzy używać Linux a toomanage Azure zasoby programu Powershell nie mogą być opcję. Firma Microsoft oferuje wiersza polecenia platformy Azure jako alternatywę.
Hello wiersza polecenia platformy Azure oferuje zestaw typu open source, obsługujący wiele platform polecenia dotyczące pracy z hello platformy Azure. Witaj interfejsu wiersza polecenia Azure udostępniają hello tę samą funkcjonalność znalezione w hello portalu Azure.

Informacje o instalacji, konfiguracji i jak toouse CLI polecenia tooaccomplish Zobacz zadań Azure

* [Zainstaluj hello wiersza polecenia platformy Azure][xplat-cli]
* [Wdrażania i zarządzania maszynami wirtualnymi przy użyciu szablonów usługi Azure Resource Manager i hello Azure CLI] [.. /.. / linux/create-ssh-secured-vm-from-template.md]
* [Użyj hello Azure CLI for Mac, Linux i Windows za pomocą Menedżera zasobów Azure][xplat-cli-azure-resource-manager]

Również przeczytanie rozdziału [wiersza polecenia platformy Azure dla maszyn wirtualnych systemu Linux] [ deployment-guide-4.5.2] w hello [Deployment Guide] [ planning-guide] w sposób toodeploy interfejsu wiersza polecenia Azure toouse hello monitorowania Azure Rozszerzenie dla SAP.

## <a name="different-ways-toodeploy-vms-for-sap-in-azure"></a>Różne sposoby toodeploy maszyn wirtualnych dla programu SAP na platformie Azure
W tym rozdziale dowiesz się toodeploy różne sposoby hello Maszynę wirtualną na platformie Azure. W tym rozdziale opisano procedury dodatkowych przygotowań, a także obsługę wirtualnych dysków twardych i maszyny wirtualne na platformie Azure.

### <a name="deployment-of-vms-for-sap"></a>Wdrażanie maszyn wirtualnych dla programu SAP
Microsoft Azure oferuje wiele sposobów toodeploy maszyn wirtualnych i skojarzone dyski. W związku z tym jest bardzo ważne toounderstand hello różnice od przygotowania hello maszyn wirtualnych może się różnić w zależności od metody hello wdrożenia. Ogólnie rzecz biorąc możemy Spójrz na powitania następujące scenariusze:

#### <a name="4d175f1b-7353-4137-9d2f-817683c26e53"></a>Przenoszenie maszyny Wirtualnej z tooAzure lokalnego przy użyciu dysku z systemem innym niż uogólniony
Planujesz toomove określonego systemu SAP z lokalnymi tooAzure. Można przekazać hello wirtualnego dysku twardego, który zawiera hello systemu operacyjnego, hello SAP pliki binarne i plików binarnych systemu DBMS plus hello wirtualne dyski twarde z plików danych i dziennika hello hello DBMS tooAzure. Z kolei zbyt[scenariusza #2 poniżej][planning-guide-5.1.2], Zachowaj hello nazwa hosta, SAP SID i kont użytkowników SAP w hello maszyny Wirtualnej platformy Azure, ponieważ zostały one skonfigurowane w środowisku lokalne powitania. W związku z tym uogólnianie hello obrazu nie jest konieczne. Patrz rozdział [przygotowania do przenoszenia maszyny Wirtualnej z tooAzure lokalnego przy użyciu dysku z systemem innym niż uogólniony] [ planning-guide-5.2.1] tego dokumentu procedury przygotowania lokalnych i przekazywania-uogólniony tooAzure maszyn wirtualnych lub wirtualne dyski twarde. Rozdział odczytu [Scenariusz 3: przenoszenie maszyny Wirtualnej z lokalnymi przy użyciu-uogólniony wirtualny dysk twardy Azure z SAP] [ deployment-guide-3.4] w hello [Deployment Guide] [ deployment-guide] Aby uzyskać szczegółowy opis kroków wdrażania obrazu na platformie Azure.

#### <a name="e18f7839-c0e2-4385-b1e6-4538453a285c"></a>Wdrażanie maszyny Wirtualnej z obrazu właściwe dla klienta
Powodu toospecific wymagania dotyczące tej wersji systemu operacyjnego lub DBMS obrazy hello podane w portalu Azure Marketplace hello może nie odpowiadają potrzebom. W związku z tym może być konieczne toocreate Maszynę wirtualną przy użyciu własnego "private" obrazu systemu operacyjnego/DBMS maszyny Wirtualnej, można wdrożyć kilka razy później. tooprepare "private" obrazu do duplikacji hello następujące elementy są toobe traktowane jako:

- - -
> ![Windows][Logo_Windows] Windows
>
> Dowiedz się więcej tutaj: <https://docs.microsoft.com/azure/virtual-machines/windows/upload-generalized-managed> ustawienia systemu Windows hello (takich jak Windows SID i nazwy hosta) musi być pobieranej/uogólniony na lokalne powitania Maszyna wirtualna za pomocą polecenia sysprep hello.
>
>
> ![Linux][Logo_Linux] Linux
>
> Wykonaj kroki hello opisane w tych artykułach dla [SUSE][virtual-machines-linux-create-upload-vhd-suse], [Red Hat][virtual-machines-linux-redhat-create-upload-vhd], lub [Oracle Linux] [ virtual-machines-linux-create-upload-vhd-oracle], tooAzure przekazać tooprepare toobe wirtualnego dysku twardego.
>
>

- - -
Jeśli zainstalowano już SAP zawartości w lokalnej maszyny Wirtualnej (szczególnie w przypadku systemów warstwy 2), można dostosować ustawienia systemu SAP powitania po wdrożenie hello hello maszyny Wirtualnej platformy Azure za pomocą wystąpienia hello nazwy procedury obsługiwane przez hello rozbudowy oprogramowania SAP Menedżer (Uwaga SAP [1619720]). Patrz rozdział [przygotowania do wdrożenia maszyny Wirtualnej z obrazu specyficzne dla programu SAP] [ planning-guide-5.2.2] i [przekazywanie wirtualnego dysku twardego z lokalnymi tooAzure] [ planning-guide-5.3.2]tego dokumentu procedury przygotowania lokalnych i przekazywania ogólnych tooAzure maszyny Wirtualnej. Rozdział odczytu [Scenariusz 2: Wdrażanie maszyny Wirtualnej z obrazu niestandardowego dla SAP] [ deployment-guide-3.3] w hello [Deployment Guide] [ deployment-guide] szczegółowy opis kroków wdrażania taki obraz na platformie Azure.

#### <a name="deploying-a-vm-out-of-hello-azure-marketplace"></a>Wdrażanie maszyny Wirtualnej poza hello Azure Marketplace
Chcesz toouse firmy Microsoft lub innych firm podane obrazu maszyny Wirtualnej z hello Azure Marketplace toodeploy maszyny Wirtualnej. Po wdrożeniu maszyny Wirtualnej na platformie Azure, wykonaj hello tych samych wskazówek i narzędzia tooinstall hello oprogramowania SAP i/lub DBMS wewnątrz maszyny Wirtualnej w sposób jak w środowisku lokalnym. Aby uzyskać bardziej szczegółowe opis wdrożenia, zobacz rozdział [scenariusz 1: Wdrażanie maszyny Wirtualnej poza hello Azure Marketplace w celu SAP] [ deployment-guide-3.2] w hello [Deployment Guide] [ deployment-guide].

### <a name="6ffb9f41-a292-40bf-9e70-8204448559e7"></a>Przygotowywanie maszyn wirtualnych z programu SAP do platformy Azure
Przed przekazaniem maszyn wirtualnych na platformie Azure należy toomake się, że hello maszyny wirtualne i wirtualne dyski twarde spełnienia określonych wymagań. Istnieją niewielkie różnice w zależności od metody wdrażania hello jest używany.

#### <a name="1b287330-944b-495d-9ea7-94b83aff73ef"></a>Przygotowanie do przenoszenia maszyny Wirtualnej z tooAzure lokalnego przy użyciu dysku z systemem innym niż uogólniony
Częstą metodą wdrażania jest toomove istniejącej maszyny Wirtualnej, w którym jest uruchomiona systemie SAP z lokalnymi tooAzure. Maszyny Wirtualnej i hello systemu SAP w hello maszyny Wirtualnej należy uruchomić za pomocą usługi Azure hello tej samej nazwy hosta i najprawdopodobniej hello sam identyfikator SID SAP. W takim przypadku gościa hello systemu operacyjnego maszyny Wirtualnej nie można uogólnić dla wielu wdrożeń. Jeśli sieć lokalną hello został rozszerzony na platformie Azure (zobacz rozdział [między lokalizacjami - wdrażania jednego lub wielu SAP maszyn wirtualnych na platformie Azure za pomocą wymóg hello jest w pełni zintegrowany sieci lokalne powitania] [ planning-guide-2.2] w tym dokumencie), następnie nawet hello tego samego konta domeny może być używana w hello maszyny Wirtualnej, ponieważ zostały one wykorzystywane przed lokalnymi.

Wymagania dotyczące podczas przygotowywania własne dysku maszyny Wirtualnej Azure są:

* Pierwotnie hello dysku VHD zawierającego system operacyjny hello może mieć maksymalny rozmiar 127GB tylko. To ograniczenie został wyeliminowany na końcu hello marca 2015 roku. Teraz hello dysku VHD zawierającego system operacyjny hello można się too1TB rozmiar jako również inne usługi Azure Storage hostowanej wirtualnego dysku twardego.
* Musi on toobe w hello stały format wirtualnego dysku twardego. Dynamicznych wirtualnych dysków twardych lub wirtualnych dysków twardych w formacie VHDx nie są jeszcze obsługiwane na platformie Azure. Dynamiczne pliki VHD można wirtualne dyski twarde przekonwertowanego toostatic podczas przekazywania hello wirtualnego dysku twardego z apletów poleceń programu PowerShell lub interfejsu wiersza polecenia
* Wirtualne dyski twarde, które są zainstalowane toohello maszyny Wirtualnej i ma być instalowana, w toobe potrzeby maszyny Wirtualnej Azure toohello również stały format wirtualnego dysku twardego. Przeczytaj [w tym artykule (Linux)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux) i [w tym artykule (system Windows)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows) limitów rozmiaru dysków danych. Dynamiczne pliki VHD można wirtualne dyski twarde przekonwertowanego toostatic podczas przekazywania hello wirtualnego dysku twardego z apletów poleceń programu PowerShell lub interfejsu wiersza polecenia
* Dodawanie innego lokalnego konta z uprawnieniami administratora, które mogą być używane przez pomocy technicznej firmy Microsoft lub które do hello wdrożonej maszyny Wirtualnej można przypisać jako kontekst dla toorun usługi i aplikacje w i bardziej odpowiednie użytkowników może zostać użyty.
* Scenariusz wdrożenia tylko na chmurze przypadku hello (zobacz rozdział [tylko w chmurze — wdrożenia maszyny wirtualnej na platformie Azure bez zależności na powitania lokalnej sieci klienta] [ planning-guide-2.1] tego dokument) w połączeniu z tej metody wdrażania, domeny, konta mogą nie działać po wdrożeniu hello Azure dysku na platformie Azure. Jest to szczególnie ważne dla konta, które są używane toorun usług takich jak hello DBMS lub SAP aplikacji. Dlatego należy tooreplace takiego konta domeny z kontami lokalnymi maszyny Wirtualnej i usuwania kont domeny lokalne powitania w hello maszyny Wirtualnej. Zachowania użytkowników domeny lokalnej w obrazie maszyny Wirtualnej hello nie jest problemem, gdy maszyna wirtualna jest wdrożona w hello hello między lokalizacjami scenariusz zgodnie z opisem w rozdziale [między lokalizacjami - wdrażania jednego lub wielu SAP maszyn wirtualnych na platformie Azure za pomocą wymóg hello w pełni zintegrowany sieci lokalne powitania] [ planning-guide-2.2] w tym dokumencie.
* Jeśli użyto konta domeny jako nazwy logowania systemu DBMS lub użytkowników podczas uruchamiania hello systemu lokalnego i tych maszyn wirtualnych powinny toobe wdrożone w scenariuszach tylko w chmurze, użytkownicy domeny hello muszą toobe usunięte. Należy toomake się, że administrator lokalny hello plus innego użytkownika lokalnego maszyny Wirtualnej jest dodany jako logowania/użytkownika do hello DBMS jako administratorzy.
* Dodać inne konta lokalnego, jak te mogą być wymagane dla scenariusza wdrażania hello.

- - -
> ![Windows][Logo_Windows] Windows
>
> W tym scenariuszu nie Generalizacja (sysprep) hello maszyny Wirtualnej jest wymagana tooupload i wdrożyć hello maszyny Wirtualnej na platformie Azure.
> Upewnij się, tego dysku D:\ nie jest używana.
> Ustaw automatycznej instalacji dysków dołączonych dysków, zgodnie z opisem w rozdziale [ustawienie automatycznej instalacji dla dołączone dyski] [ planning-guide-5.5.3] w tym dokumencie.
>
> ![Linux][Logo_Linux] Linux
>
> W tym scenariuszu nie Generalizacja (agenta waagent-deprovision) hello maszyny Wirtualnej jest wymagana tooupload i wdrożyć hello maszyny Wirtualnej na platformie Azure.
> Upewnij się, czy/mnt/zasobu nie jest używany i czy wszystkie dyski są instalowane za pomocą identyfikatora uuid. Dla dysku systemu operacyjnego hello upewnij się, że wpis programu inicjującego hello również odzwierciedla hello na podstawie identyfikatora uuid instalacji.
>
>

- - -
#### <a name="57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3"></a>Przygotowanie do wdrożenia maszyny Wirtualnej z obrazu specyficzne dla programu SAP
Pliki VHD, które zawierają uogólniony systemu operacyjnego są przechowywane w kontenery na kontach magazynu Azure lub jako obrazy dysku zarządzanego. Można wdrożyć nową maszynę Wirtualną z takich obrazu za pomocą odwołań do obrazu wirtualnego dysku twardego lub dysk zarządzane hello jako źródło w plikach szablonu wdrożenia, zgodnie z opisem w rozdziale [Scenariusz 2: Wdrażanie maszyny Wirtualnej z obrazu niestandardowego dla SAP] [ deployment-guide-3.3]z hello [Deployment Guide][deployment-guide].

Wymagania dotyczące podczas przygotowywania własny obraz maszyny Wirtualnej platformy Azure są:

* Pierwotnie hello dysku VHD zawierającego system operacyjny hello może mieć maksymalny rozmiar 127GB tylko. To ograniczenie został wyeliminowany na końcu hello marca 2015 roku. Teraz hello dysku VHD zawierającego system operacyjny hello można się too1TB rozmiar jako również inne usługi Azure Storage hostowanej wirtualnego dysku twardego.
* Musi on toobe w hello stały format wirtualnego dysku twardego. Dynamicznych wirtualnych dysków twardych lub wirtualnych dysków twardych w formacie VHDx nie są jeszcze obsługiwane na platformie Azure. Dynamiczne pliki VHD można wirtualne dyski twarde przekonwertowanego toostatic podczas przekazywania hello wirtualnego dysku twardego z apletów poleceń programu PowerShell lub interfejsu wiersza polecenia
* Wirtualne dyski twarde, które są zainstalowane toohello maszyny Wirtualnej i ma być instalowana, w toobe potrzeby maszyny Wirtualnej Azure toohello również stały format wirtualnego dysku twardego. Przeczytaj [w tym artykule (Linux)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux) i [w tym artykule (system Windows)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows) limitów rozmiaru dysków danych. Dynamiczne pliki VHD można wirtualne dyski twarde przekonwertowanego toostatic podczas przekazywania hello wirtualnego dysku twardego z apletów poleceń programu PowerShell lub interfejsu wiersza polecenia
* Ponieważ wszystkie hello użytkowników domeny w zarejestrowany jako użytkowników w hello maszyna wirtualna nie będzie istnieć w scenariuszu tylko w chmurze (zobacz rozdział [tylko w chmurze — wdrożenia maszyny wirtualnej na platformie Azure bez zależności na powitania lokalnej sieci klienta] [ planning-guide-2.1] tego dokumentu), usługi przy użyciu takiej domeny konta mogą nie działać po wdrożeniu hello obrazu na platformie Azure. Jest to szczególnie ważne dla konta, które są używane toorun usług, takich jak aplikacje systemu DBMS lub SAP. Dlatego należy tooreplace takiego konta domeny z kontami lokalnymi maszyny Wirtualnej i usuwania kont domeny lokalne powitania w hello maszyny Wirtualnej. Utrzymywanie lokalnych użytkowników domeny w obrazie maszyny Wirtualnej hello może być problem podczas hello maszyna wirtualna jest wdrożona w hello między lokalizacjami scenariusz zgodnie z opisem w rozdziale [między lokalizacjami - wdrażania jednego lub wielu SAP maszyn wirtualnych na platformie Azure za pomocą hello wymagania jest w pełni zintegrowany sieci lokalne powitania] [ planning-guide-2.2] w tym dokumencie.
* Dodawanie innego lokalnego konta z uprawnieniami administratora, które mogą być używane przez pomocy technicznej firmy Microsoft w dochodzenia problem lub które do hello wdrożonej maszyny Wirtualnej można przypisać jako kontekst dla toorun usługi i aplikacje w i bardziej odpowiednie użytkowników może zostać użyty.
* Wdrożenia tylko w chmurze i gdzie kont domeny były używane jako nazwy logowania systemu DBMS lub użytkowników podczas uruchamiania hello systemu lokalnego należy je usunąć hello użytkownicy domeny. Należy toomake się, że administrator lokalny hello plus innego użytkownika lokalnego maszyny Wirtualnej jest dodany jako logowania/użytkownika hello DBMS jako administratorzy.
* Dodać inne konta lokalnego, jak te mogą być wymagane dla scenariusza wdrażania hello.
* Jeśli obraz powitania zawiera instalację programu SAP NetWeaver i prawdopodobnie zmianę nazwy hosta hello z oryginalną nazwą hello w punkcie hello hello wdrożenia usługi Azure, jest zalecane toocopy hello najnowsze wersje hello oprogramowania SAP inicjowania obsługi administracyjnej Menedżera DVD do Szablon Hello. Pozwoli to tooeasily Użyj hello SAP wprowadzone zmiany nazwy funkcji tooadapt hello zmienić nazwę hosta i/lub zmień hello SID hello systemu SAP w hello wdrożyć obraz maszyny Wirtualnej zaraz po uruchomieniu nowej kopii.

- - -
> ![Windows][Logo_Windows] Windows
>
> Upewnij się, że dysku D:\ nie jest używany zestaw automatycznej instalacji z dysku dołączonych dysków, zgodnie z opisem w rozdziale [ustawienie automatycznej instalacji dla dołączone dyski] [ planning-guide-5.5.3] w tym dokumencie.
>
> ![Linux][Logo_Linux] Linux
>
> Upewnij się, czy/mnt/zasobu nie jest używany i czy wszystkie dyski są instalowane za pomocą identyfikatora uuid. Dla dysku systemu operacyjnego hello upewnij się, że wpis programu inicjującego hello również odzwierciedla hello na podstawie identyfikatora uuid instalacji.
>
>

- - -
* SAP graficznego interfejsu użytkownika (dla administracyjne i ustawienia celów) można zainstalować wstępnie takie szablonu.
* Inne oprogramowanie hello toorun niezbędne, można ją zainstalować maszyn wirtualnych pomyślnie w scenariuszach między różnymi lokalizacjami, tak długo, jak to oprogramowanie może współpracować z hello Zmień nazwę elementu hello maszyny Wirtualnej.

Hello maszyna wirtualna jest wystarczająco przygotowany toobe ogólnego i ostatecznie niezależnie od kont użytkowników/nie jest dostępna w hello docelowe scenariusz wdrażania platformy Azure, hello ostatni krok przygotowania programu uogólnianie taki obraz jest przeprowadzane.

##### <a name="generalizing-a-vm"></a>Uogólnianie maszyny Wirtualnej
- - -
> ![Windows][Logo_Windows] Windows
>
> ostatni krok Hello jest toolog w tooa maszyny Wirtualnej przy użyciu konta administratora. Otwórz okno poleceń programu Windows "Administrator". Przejdź too%windir%\windows\system32\sysprep i wykonać sysprep.exe.
> Zostanie wyświetlone okno mała. Jest opcja "Generalize" hello ważne toocheck (domyślna hello jest wyczyszczone) i zmienić domyślne too'Shutdown "Ponowny rozruch" hello opcja zamknięcia systemu ". W tej procedurze założono, że proces programu sysprep hello jest wykonywane lokalnie w hello systemu operacyjnego gościa maszyny wirtualnej.
> Procedury hello tooperform z maszyny Wirtualnej już uruchomione na platformie Azure, należy wykonać hello procedury opisanej w [w tym artykule](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/capture-image-resource).
>
> ![Linux][Logo_Linux] Linux
>
> [Jak toocapture toouse maszyny wirtualnej systemu Linux jako szablon Menedżera zasobów][capture-image-linux-step-2-create-vm-image]
>
>

- - -
### <a name="transferring-vms-and-vhds-between-on-premises-tooazure"></a>Przenoszenie między lokalnymi tooAzure maszyny wirtualne i wirtualne dyski twarde
Ponieważ przekazywania tooAzure obrazy i dyski maszyny Wirtualnej nie jest możliwe za pośrednictwem hello portalu Azure, należy poleceń cmdlet programu Azure PowerShell toouse lub interfejsu wiersza polecenia. Inną możliwością jest użycie hello hello narzędzia "Narzędzie AzCopy". Narzędzie Hello można skopiować wirtualne dyski twarde między lokalną i platformą Azure (w obu kierunkach). On również skopiować wirtualne dyski twarde między regiony platformy Azure. Przejrzyj [tej dokumentacji] [ storage-use-azcopy] do pobrania i użycia programu AzCopy.

W trzecim alternatywnych byłoby toouse różnych narzędzi zorientowane na graficznego interfejsu użytkownika innych firm. Jednakże upewnij się, że te narzędzia są obsługiwane Azure stronicowych obiektów blob. Do przechowywania naszych celów potrzebujemy toouse Azure stronicowych obiektów Blob (w tym miejscu opisano różnice hello: <https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>). Witaj narzędzi dostępnych w programie Azure są również bardzo wydajny w kompresowania hello maszyny wirtualne i wirtualne dyski twarde, które należy przekazać toobe. Jest to ważne, ponieważ takie zwiększenie efektywności Kompresja zmniejsza czas przekazywania hello (które mimo to zmienia się w zależności od toohello łącze przekazywania hello internet z hello lokalnie, jak i regionu Azure wdrożenia hello docelowe). Jest odpowiedni założenie, że przekazywanie maszyny Wirtualnej lub wirtualnego dysku twardego z Europejskiego lokalizacji toohello amerykańskiej danych Azure, które centrów będzie trwać dłużej niż przekazywanie hello tych samych centrach danych Azure Europejskiego toohello maszyny wirtualne/VHD.

#### <a name="a43e40e6-1acc-4633-9816-8f095d5a7b6a"></a>Przekazywanie wirtualnego dysku twardego z lokalnymi tooAzure
tooupload istniejącej maszyny Wirtualnej lub wirtualnego dysku twardego z hello lokalnej sieci maszyny Wirtualnej lub wirtualnego dysku twardego musi toomeet hello wymagań wymienionych w rozdziale [przygotowania do przenoszenia maszyny Wirtualnej z tooAzure lokalnego przy użyciu dysku z systemem innym niż uogólniony] [ planning-guide-5.2.1] tego dokumentu.

Maszyna wirtualna nie jest konieczne toobe uogólniony i mogą być przekazywane w stanie hello i kształt, który ma po zamykania na powitania po stronie lokalnymi. Witaj dotyczy to także dodatkowe wirtualne dyski twarde, które nie mogą zawierać żadnego systemu operacyjnego.

##### <a name="uploading-a-vhd-and-making-it-an-azure-disk"></a>Przekazywanie wirtualnego dysku twardego i co dysku platformy Azure
W takim przypadku możemy mają tooupload dysku VHD, lub bez systemu operacyjnego i zainstalować go tooa maszyny Wirtualnej jako dysk z danymi lub używać go jako dysk systemu operacyjnego. Jest to proces wieloetapowych

**PowerShell**

* Zaloguj się za tooyour subskrypcji z *Login-AzureRmAccount*
* Ustaw hello subskrypcji kontekstu za pomocą *Set-AzureRmContext* i parametr identyfikator subskrypcji lub Nazwa subskrypcji — zobacz <https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* Przekaż hello wirtualny dysk twardy z *AzureRmVhd Dodaj* tooan konto magazynu platformy Azure — zobacz <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* (Opcjonalnie) Tworzenie dysku zarządzanego z hello wirtualnego dysku twardego z *AzureRmDisk nowy* — zobacz <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermdisk>
* Ustaw hello systemu operacyjnego z nowego toohello konfiguracji maszyny Wirtualnej wirtualny dysk twardy lub zarządzane dysku z *AzureRmVMOSDisk zestaw* — zobacz <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>
* Utwórz nową maszynę Wirtualną na podstawie hello konfiguracji maszyny Wirtualnej z *AzureRmVM nowy* — zobacz <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>
* Dodaj tooa dysku danych nowej maszyny Wirtualnej z *AzureRmVMDataDisk Dodaj* — zobacz <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk>

**Interfejs wiersza polecenia platformy Azure 2.0**

* Zaloguj się za tooyour subskrypcji z *az logowania*
* Wybierz subskrypcję z *skonfigurowane konto az — subskrypcji`<subscription name or id`>*
* Przekaż hello wirtualny dysk twardy z *az magazynu obiektów blob przekazywania* — zobacz [hello używanie interfejsu wiersza polecenia Azure z usługą Azure Storage][storage-azure-cli]
* (Opcjonalnie) Tworzenie dysku zarządzanego z hello wirtualnego dysku twardego z *Tworzenie dysku az* — Zobacz https://docs.microsoft.com/cli/azure/disk#create
* Tworzenie nowej maszyny Wirtualnej, określając hello przesłać wirtualnego dysku twardego lub dysk zarządzane jako dysk systemu operacyjnego z *tworzenia maszyny wirtualnej az* i parametru *--attach-os-disk*
* Dodaj tooa dysku danych nowej maszyny Wirtualnej z *dołączyć dysku maszyny wirtualnej az* i parametru *— nowy*

**Szablon**

* Przekaż hello wirtualny dysk twardy z programu Powershell lub interfejsu wiersza polecenia platformy Azure
* (Opcjonalnie) Tworzenie dysku zarządzanego z hello wirtualnego dysku twardego za pomocą programu Powershell, interfejsu wiersza polecenia Azure lub hello portalu Azure
* Wdrażanie hello maszyny Wirtualnej z szablonu JSON odwołujące się do hello wirtualnego dysku twardego, jak pokazano w [tego szablonu JSON przykład](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json) lub za pomocą dysków zarządzanych, jak pokazano w [tego szablonu JSON przykład](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-disk-md/azuredeploy.json).

#### <a name="deployment-of-a-vm-image"></a>Wdrożenie obrazu maszyny Wirtualnej
tooupload istniejącej maszyny Wirtualnej lub wirtualnego dysku twardego z hello lokalnej sieci w kolejności toouse go jako obraz maszyny Wirtualnej Azure maszyny Wirtualnej lub wirtualnego dysku twardego konieczne toomeet hello wymagania wymienione w rozdziale [przygotowania do wdrożenia maszyny Wirtualnej z obrazu specyficzne dla programu SAP] [ planning-guide-5.2.2] tego dokumentu.

* Użyj *sysprep* w systemie Windows lub *agenta waagent-deprovision* na systemie Linux toogeneralize maszyny Wirtualnej — zobacz [techniczne dotyczące narzędzia Sysprep](https://technet.microsoft.com/library/cc766049.aspx) dla systemu Windows lub [jak toocapture Toouse maszyny wirtualnej systemu Linux jako szablon Menedżera zasobów] [ capture-image-linux-step-2-create-vm-image] dla systemu Linux
* Zaloguj się za tooyour subskrypcji z *Login-AzureRmAccount*
* Ustaw hello subskrypcji kontekstu za pomocą *Set-AzureRmContext* i parametr identyfikator subskrypcji lub Nazwa subskrypcji — zobacz <https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* Przekaż hello wirtualny dysk twardy z *AzureRmVhd Dodaj* tooan konto magazynu platformy Azure — zobacz <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* (Opcjonalnie) Utwórz obraz dysku zarządzane na podstawie hello wirtualnego dysku twardego z *AzureRmImage nowy* — zobacz <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermimage>
* Ustaw hello dysku systemu operacyjnego nowy toothe konfiguracji maszyny Wirtualnej
  * Wirtualny dysk twardy z *Set AzureRmVMOSDisk - SourceImageUri fromImage - CreateOption* — zobacz <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>
  * Zarządzane obrazu dysku *AzureRmVMSourceImage zestaw* — zobacz <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage>
* Utwórz nową maszynę Wirtualną na podstawie hello konfiguracji maszyny Wirtualnej z *AzureRmVM nowy* — zobacz <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>

**Interfejs wiersza polecenia platformy Azure 2.0**

* Użyj *sysprep* w systemie Windows lub *agenta waagent-deprovision* na systemie Linux toogeneralize maszyny Wirtualnej — zobacz [techniczne dotyczące narzędzia Sysprep](https://technet.microsoft.com/library/cc766049.aspx) dla systemu Windows lub [jak toocapture Toouse maszyny wirtualnej systemu Linux jako szablon Menedżera zasobów] [ capture-image-linux-step-2-create-vm-image] dla systemu Linux
* Zaloguj się za tooyour subskrypcji z *az logowania*
* Wybierz subskrypcję z *skonfigurowane konto az — subskrypcji`<subscription name or id`>*
* Przekaż hello wirtualny dysk twardy z *az magazynu obiektów blob przekazywania* — zobacz [hello używanie interfejsu wiersza polecenia Azure z usługą Azure Storage][storage-azure-cli]
* (Opcjonalnie) Utwórz obraz dysku zarządzane na podstawie hello wirtualnego dysku twardego z *tworzenia obrazu az* — Zobacz https://docs.microsoft.com/cli/azure/image#create
* Tworzenie nowej maszyny Wirtualnej, określając hello przesłać wirtualnego dysku twardego lub obrazu dysku zarządzane jako dysk systemu operacyjnego z *tworzenia maszyny wirtualnej az* i parametru *--obrazu*

**Szablon**

* Użyj *sysprep* w systemie Windows lub *agenta waagent-deprovision* na systemie Linux toogeneralize maszyny Wirtualnej — zobacz [techniczne dotyczące narzędzia Sysprep](https://technet.microsoft.com/library/cc766049.aspx) dla systemu Windows lub [jak toocapture Toouse maszyny wirtualnej systemu Linux jako szablon Menedżera zasobów] [ capture-image-linux-step-2-create-vm-image] dla systemu Linux
* Przekaż hello wirtualny dysk twardy z programu Powershell lub interfejsu wiersza polecenia platformy Azure
* (Opcjonalnie) Tworzenie obrazu dysku zarządzane z hello wirtualnego dysku twardego za pomocą programu Powershell, interfejsu wiersza polecenia Azure lub hello portalu Azure
* Wdrażanie hello maszyny Wirtualnej z szablonu JSON odwołujące się do hello obrazu wirtualnego dysku twardego, jak pokazano w [tego szablonu JSON przykład](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-image/azuredeploy.json) lub przy użyciu hello zarządzanego obrazu dysku, jak pokazano w [tego szablonu JSON przykład](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).

#### <a name="downloading-vhds-or-managed-disks-tooon-premises"></a>Pobieranie dysków VHD lub zarządzane dysków lokalnych tooon
Azure infrastruktura jako usługa nie jest jednokierunkowa ulicy tylko ich stanie tooupload wirtualne dyski twarde i systemów SAP. Można przenieść SAP systemów z platformy Azure z powrotem do Witaj świecie lokalnych oraz.

Podczas hello hello hello pobierania dysków VHD lub dysków zarządzanych nie może być aktywne. Nawet w przypadku pobierania dysków, które są zainstalowane tooVMs hello maszyny Wirtualnej musi toobe zamknięte i alokację. Jeśli chcesz tylko toodownload hello bazy danych zawartości, następnie powinny być używane tooset nowy system lokalny. Jeśli i zaakceptować który podczas hello hello Pobierz hello instalacji nowego systemu hello który hello systemu na platformie Azure mogą nadal działać , można uniknąć długie przestoje, wykonując kopię zapasową skompresowanej bazy danych na dysk i wystarczy pobrać tego dysku zamiast również hello podstawowej maszyny Wirtualnej systemu operacyjnego.

#### <a name="powershell"></a>PowerShell

  * Pobieranie z dyskiem zarządzanym  
  Należy najpierw toohello dostępu tooget bazowy blob hello dysku zarządzanego. Następnie możesz skopiować hello podstawowej tooa nowego konta magazynu obiektów blob i pobrać hello obiektów blob z tego konta magazynu.

  ```powershell
  $access = Grant-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name> -Access Read -DurationInSecond 3600
  $key = (Get-AzureRmStorageAccountKey -ResourceGroupName <resource group> -Name <storage account name>)[0].Value
  $destContext = (New-AzureStorageContext -StorageAccountName <storage account name -StorageAccountKey $key)
  Start-AzureStorageBlobCopy -AbsoluteUri $access.AccessSAS -DestContainer <container name> -DestBlob <blob name> -DestContext $destContext
  # Wait for blob copy toofinish
  Get-AzureStorageBlobCopyState -Container <container name> -Blob <blob name> -Context $destContext
  Save-AzureRmVhd -SourceUri <blob in new storage account> -LocalFilePath <local file path> -StorageKey $key
  # Wait for download toofinish
  Revoke-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name>
  ```

  * Pobieranie wirtualnego dysku twardego  
  Po zatrzymaniu hello systemu SAP i hello maszyna wirtualna jest zamknięta, możesz użyć hello polecenia cmdlet programu PowerShell AzureRmVhd Zapisz na powitania lokalnych dysków VHD hello toodownload docelowych powrotem toohello świecie lokalnych. W kolejności toodo, że należy adres URL hello wirtualnego dysku twardego, który można znaleźć w hello magazynowania "w artykule" hello z hello portalu Azure (potrzeby toonavigate toohello konto magazynu i hello kontenera magazynu której hello wirtualny dysk twardy został utworzony) i potrzebujesz tooknow gdzie hello dysku VHD powinien być skopiowane do.

  Następnie można wykorzystać polecenie hello definiując po prostu parametru hello SourceUri jako adres URL hello hello toodownload wirtualnego dysku twardego i hello LocalFilePath jak fizyczną lokalizację hello hello wirtualnego dysku twardego (w tym swojej nazwy). polecenie Hello może wyglądać podobnie do:

  ```powerhell
  Save-AzureRmVhd -ResourceGroupName <resource group name of storage account> -SourceUri http://<storage account name>.blob.core.windows.net/<container name>/sapidedata.vhd -LocalFilePath E:\Azure_downloads\sapidesdata.vhd
  ```

  Więcej informacji o hello AzureRmVhd Zapisz polecenia cmdlet, sprawdź, czy w tym miejscu <https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvhd>.

#### <a name="cli-20"></a>Interfejs wiersza polecenia 2.0
  * Pobieranie z dyskiem zarządzanym  
  Należy najpierw toohello dostępu tooget bazowy blob hello dysku zarządzanego. Następnie możesz skopiować hello podstawowej tooa nowego konta magazynu obiektów blob i pobrać hello obiektów blob z tego konta magazynu.
  ```
  az disk grant-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --duration-in-seconds 3600
  az storage blob download --sas-token "<sas token>" --account-name <account name> --container-name <container name> --name <blob name> --file <local file>
  az disk revoke-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>"
  ```

  * Pobieranie wirtualnego dysku twardego   
  Po zatrzymaniu hello systemu SAP i hello maszyna wirtualna jest zamknięta, możesz użyć polecenia interfejsu wiersza polecenia Azure hello _pobieranie obiektu blob magazynu azure_ w celu lokalne powitania hello toodownload wirtualnego dysku twardego dyski world lokalnymi toohello Wstecz. W kolejności toodo, że z hello potrzebna nazwa hello i kontener hello hello wirtualnego dysku twardego, który można znaleźć w hello magazynowania "w artykule" portalu Azure (potrzeby toonavigate toohello konto magazynu i hello kontenera magazynu której hello wirtualny dysk twardy został utworzony) i potrzebujesz tooknow gdzie Witaj dysku VHD powinien zostać skopiowany do.

  Następnie można wykorzystać hello polecenia, po prostu definiując hello parametry blob i kontener hello toodownload wirtualnego dysku twardego i przeznaczenia hello jako lokalizację docelową fizycznych hello hello wirtualnego dysku twardego (w tym jego nazwa). polecenie Hello może wyglądać podobnie do:

  ```
  az storage blob download --name <name of hello VHD toodownload> --container-name <container of hello VHD toodownload> --account-name <storage account name of hello VHD toodownload> --account-key <storage account key> --file <destination of hello VHD toodownload>
  ```

### <a name="transferring-vms-and-disks-within-azure"></a>Przenoszenie maszyn wirtualnych i dyskami w systemie Azure
#### <a name="copying-sap-systems-within-azure"></a>Kopiowanie systemów SAP w obrębie platformy Azure
Systemu SAP lub nawet DBMS serwera dedykowanego obsługi warstwy aplikacji SAP będzie prawdopodobnie składają się z kilka dysków, które zawierają hello albo systemu operacyjnego przy użyciu plików binarnych hello lub hello danych oraz pliku lub plików bazy danych SAP hello dziennika. Hello Azure funkcji kopiowania dysków z użyciem ani hello Azure funkcji zapisywania dysków tooa dysku ma mechanizm synchronizacji, który spowoduje utworzenie migawki synchronicznie wiele dysków. Oznacza to, stan hello hello skopiowane i zapisane dysków, nawet jeśli te są zainstalowane przed hello tej samej maszyny Wirtualnej będzie inny. Oznacza to, że w przypadku konkretnych hello o różnych danych i logfile(s) zawarte w innych dyskach hello, bazy danych hello w celu hello byłoby niezgodne.

**Wniosek: W kolejności toocopy lub zapisać dysków, które są częścią konfiguracji systemu SAP muszą systemu SAP hello toostop, a także tooshut dół hello wdrożyć maszyny Wirtualnej. Tylko, a następnie możesz skopiować lub pobrać zestaw hello tooeither dyski należy utworzyć kopię hello systemu SAP w Azure lub lokalnie.**

Dyski danych mogą być przechowywane jako pliki wirtualnego dysku twardego na koncie magazynu Azure i może być podłączonego bezpośrednio tooa maszyny wirtualnej lub zostać użyty jako obraz. W takim przypadku hello wirtualnego dysku twardego jest lokalizacja skopiowanych tooanother zanim zostanie ono podłączone toohello maszyny wirtualnej. Pełna nazwa pliku wirtualnego dysku twardego hello na platformie Azure Hello musi być unikatowa w obrębie platformy Azure. Jak wspomniano wcześniej już, hello nazwa jest rodzaj trzyczęściowej wygląda następująco:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Dyski danych może być także zarządzane dysków. W takim przypadku hello dysku zarządzanego jest używane toocreate nowego zarządzanego dysku, zanim zostanie ono podłączone toohello maszyny wirtualnej. Nazwa Hello hello dysku zarządzanego musi być unikatowa w obrębie grupy zasobów.

##### <a name="powershell"></a>PowerShell
Można użyć toocopy poleceń cmdlet programu Azure PowerShell dysku VHD, jak pokazano w [w tym artykule][storage-powershell-guide-full-copy-vhd]. toocreate nowego dysku zarządzanego, użyj nowego AzureRmDiskConfig i AzureRmDisk nowy, jak pokazano hello poniższy przykład.

```powershell
$config = New-AzureRmDiskConfig -CreateOption Copy -SourceUri "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" -Location <location>
New-AzureRmDisk -ResourceGroupName <resource group name> -DiskName <disk name> -Disk $config
```

##### <a name="cli-20"></a>Interfejs wiersza polecenia 2.0
Można użyć interfejsu wiersza polecenia Azure toocopy dysku VHD, jak pokazano w [w tym artykule][storage-azure-cli-copy-blobs]. Użyj toocreate nowego dysku zarządzanego *Tworzenie dysku az* pokazane na powitania poniższy przykład.

```
az disk create --source "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --name <disk name> --resource-group <resource group name> --location <location>
```

##### <a name="azure-storage-tools"></a>Narzędzia do magazynu Azure
* <http://storageexplorer.com/>

Wersje Professional eksploratory usługi Azure Storage można znaleźć tutaj:

* <http://www.cerebrata.com/>
* <http://clumsyleaf.com/products/cloudxplorer>

Kopia Hello samego dysku VHD w ramach konta magazynu jest procesu, który zajmuje tylko kilka sekund (podobnego sprzętu tooSAN tworzenie migawek z opóźnieniem kopiowania i skopiuj podczas zapisu). Po utworzeniu kopii pliku wirtualnego dysku twardego hello można dołączyć maszyny wirtualnej tooa lub użyj go jako obraz tooattach kopiuje hello wirtualnego dysku twardego toovirtual maszyn.

##### <a name="powershell"></a>PowerShell
```powershell
# attach a vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <path toovhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -ManagedDiskId <managed disk id> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a copy of hello vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name <disk name> -VhdUri <new path of vhd> -SourceImageUri <path tooimage vhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption fromImage
$vm | Update-AzureRmVM

# attach a copy of hello managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$diskConfig = New-AzureRmDiskConfig -Location $vm.Location -CreateOption Copy -SourceUri <source managed disk id>
$disk = New-AzureRmDisk -DiskName <disk name> -Disk $diskConfig -ResourceGroupName <resource group name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Caching <caching option> -Lun <lun, for example 0> -CreateOption attach -ManagedDiskId $disk.Id
$vm | Update-AzureRmVM
```
##### <a name="cli-20"></a>Interfejs wiersza polecenia 2.0
```

# attach a vhd tooa vm
az vm unmanaged-disk attach --resource-group <resource group name> --vm-name <vm name> --vhd-uri <path toovhd>

# attach a managed disk tooa vm
az vm disk attach --resource-group <resource group name> --vm-name <vm name> --disk <managed disk id>

# attach a copy of hello vhd tooa vm
# this scenario is currently not possible with Azure CLI. A workaround is toomanually copy hello vhd toohello destination.

# attach a copy of a managed disk tooa vm
az disk create --name <new disk name> --resource-group <resource group name> --location <location of target virtual machine> --source <source managed disk id>
az vm disk attach --disk <new disk name or managed disk id> --resource-group <resource group name> --vm-name <vm name> --caching <caching option> --lun <lun, for example 0>
```

#### <a name="9789b076-2011-4afa-b2fe-b07a8aba58a1"></a>Kopiowanie dysków między kontami magazynu Azure
Nie można wykonać tego zadania na powitania portalu Azure. Można użyć poleceń cmdlet programu Azure PowerShell, interfejsu wiersza polecenia Azure lub przeglądarki magazynu innych firm. Witaj poleceń cmdlet programu PowerShell lub polecenia interfejsu wiersza polecenia można tworzyć i zarządzać obiektów blob, w tym hello możliwości tooasynchronously kopiowania blob wielu kont magazynu i w regionach w ramach hello subskrypcji platformy Azure.

##### <a name="powershell"></a>PowerShell
Można również skopiować wirtualne dyski twarde między subskrypcjami. Aby uzyskać więcej informacji, przeczytaj [w tym artykule][storage-powershell-guide-full-copy-vhd].

podstawowe przepływu Hello hello PS logiki polecenia cmdlet wygląda następująco:

* Tworzenie kontekstu konta magazynu hello **źródła** konta magazynu z *AzureStorageContext nowy* — zobacz <https://msdn.microsoft.com/library/dn806380.aspx>
* Tworzenie kontekstu konta magazynu hello **docelowej** konta magazynu z *AzureStorageContext nowy* — zobacz <https://msdn.microsoft.com/library/dn806380.aspx>
* Uruchom kopię hello z

```powershell
Start-AzureStorageBlobCopy -SrcBlob <source blob name> -SrcContainer <source container name> -SrcContext <variable containing context of source storage account> -DestBlob <target blob name> -DestContainer <target container name> -DestContext <variable containing context of target storage account>
```

* Sprawdź stan hello kopii hello w pętli z

```powershell
Get-AzureStorageBlobCopyState -Blob <target blob name> -Container <target container name> -Context <variable containing context of target storage account>
```

* Dołącz hello nowej wirtualnego dysku twardego tooa maszyny wirtualnej, zgodnie z powyższym opisem.

Przykłady można znaleźć [w tym artykule][storage-powershell-guide-full-copy-vhd].

##### <a name="cli-20"></a>Interfejs wiersza polecenia 2.0
* Uruchom kopię hello z

```
az storage blob copy start --source-blob <source blob name> --source-container <source container name> --source-account-name <source storage account name> --source-account-key <source storage account key> --destination-container <target container name> --destination-blob <target blob name> --account-name <target storage account name> --account-key <target storage account name>
```

* Sprawdź stan hello, jeśli hello kopiowania w pętli z

```
az storage blob show --name <target blob name> --container <target container name> --account-name <target storage account name> --account-key <target storage account name>
```

* Dołącz hello nowej wirtualnego dysku twardego tooa maszyny wirtualnej, zgodnie z powyższym opisem.

Przykłady można znaleźć [w tym artykule][storage-azure-cli-copy-blobs].

### <a name="disk-handling"></a>Obsługa dysku
#### <a name="4efec401-91e0-40c0-8e64-f2dceadff646"></a>Maszyna wirtualna lub dysk struktury wdrożenia SAP
W idealnym przypadku hello Obsługa struktury hello maszyny wirtualnej i hello skojarzone dyski powinny być bardzo proste. W przypadku instalacji lokalnych klientów opracowany struktury instalacji serwera na wiele sposobów.

* Jeden dysk podstawowy, który zawiera hello systemu operacyjnego i wszystkich hello pliki binarne hello DBMS i/lub SAP. Od marca 2015 ten dysk może być zapasowej too1TB rozmiar zamiast wcześniejszych ograniczenia, które go ograniczone too127GB.
* Jednego lub wielu dysków, które zawiera hello DBMS plik dziennika bazy danych SAP hello i pliku dziennika hello hello DBMS obszaru tymczasowego magazynu (jeśli hello DBMS obsługuje tę funkcję). Wymagania IOPS dziennika bazy danych hello są wysokie, należy najpierw toostripe wiele dysków w kolejności tooreach hello IOPS ilość wymaganą.
* Liczba dysków zawierających jeden lub dwa pliki bazy danych, bazy danych SAP hello hello DBMS dane tymczasowe również i plików (jeśli hello DBMS obsługuje tę funkcję).

![Odwołanie do konfiguracji IaaS maszyny Wirtualnej platformy Azure dla programu SAP][planning-guide-figure-1300]

[comment]: <> (MShermannd TODO opisania struktury systemu Linux)

- - -
> ![Windows][Logo_Windows] Windows
>
> Z wielu klientów widzieliśmy konfiguracje where, na przykład SAP i bazami danych binarnych nie zostały zainstalowane na dysku c:\ hello gdzie hello systemu operacyjnego został zainstalowany. Wystąpiły różne przyczyny to go, ale podczas ponownie poszliśmy toohello głównego, zwykle że dysków hello małe i uaktualnień systemu operacyjnego potrzebne dodatkowe miejsce, 10 – 15 lat temu. Oba te warunki nie są stosowane te zbyt często już dni. Dzisiaj dysku c:\ hello mogą być mapowane na dyskach duże lub maszyn wirtualnych. W przypadku wdrożeń tookeep kolejności proste w ich struktury, jest zalecane toofollow następującego wzorca wdrożenia SAP NetWeaver systemów na platformie Azure
>
> plik stronicowania systemu operacyjnego Windows Hello powinna znajdować się na powitania dysku D: (nietrwałe dysku)
>
> ![Linux][Logo_Linux] Linux
>
> Umieść swapfile Linux hello w katalogu/mnt/mnt/zasobu w systemie Linux, zgodnie z opisem w [w tym artykule][virtual-machines-linux-agent-user-guide]. plik wymiany Hello można skonfigurować w pliku konfiguracji hello hello /etc/waagent.conf agenta systemu Linux. Dodawanie lub zmienianie hello następujące ustawienia:
>
>

```
ResourceDisk.EnableSwap=y
ResourceDisk.SwapSizeMB=30720
```

tooactivate hello zmiany, należy toorestart hello agenta systemu Linux z

```
sudo service waagent restart
```

Przeczytaj uwagi SAP [1597355] więcej szczegółów na powitania zalecany rozmiar pliku wymiany

- - -
Witaj liczba dysków z hello DBMS danych plików i typ hello Azure Storage tych dysków znajdują się w powinna zostać określona przez wymagania IOPS hello i opóźnienia hello wymagane. Dokładne przydziały są opisane w [w tym artykule (Linux)] [ virtual-machines-sizes-linux] i [w tym artykule (system Windows)][virtual-machines-sizes-windows].

Środowisko wdrożenia SAP za pośrednictwem hello ostatnich 2 lat nauczanych nam niektórych — lekcje, które mogą być podsumowywane jako:

* Pliki danych toodifferent ruchu IOPS nie zawsze jest hello sam od istniejących systemów klienta może mieć inaczej o rozmiarze danych plików reprezentujący ich baz danych SAP. W związku z tym włączony limit toobe lepiej przy użyciu konfiguracji RAID przez wiele dysków tooplace hello danych plików jednostek LUN używać poza tymi. Znaleziono sytuacji, szczególnie gdy szybkość IOPS osiągnęła przydział hello pojedynczego dysku dla dziennika transakcji DBMS hello usługi Azure Standard Storage. W takich przypadkach zaleca się użycie hello magazyn w warstwie Premium lub też agregowanie wielu Standard Storage RAID dysków przy użyciu oprogramowania.

- - -
> ![Windows][Logo_Windows] Windows
>
> * [Wydajność najlepsze rozwiązania dotyczące programu SQL Server w maszynach wirtualnych platformy Azure][virtual-machines-sql-server-performance-best-practices]
>
> ![Linux][Logo_Linux] Linux
>
> * [Należy skonfigurować oprogramowanie RAID w systemie Linux][virtual-machines-linux-configure-raid]
> * [Skonfiguruj LVM na Maszynę wirtualną systemu Linux na platformie Azure][virtual-machines-linux-configure-lvm]
> * [Azure magazynu kluczy tajnych i optymalizacje We/Wy systemu Linux](http://blogs.msdn.com/b/igorpag/archive/2014/10/23/azure-storage-secrets-and-linux-i-o-optimizations.aspx)
>
>

- - -
* Magazyn w warstwie Premium jest pokazywany znaczących lepszą wydajność, szczególnie w przypadku zapisów dziennika transakcji krytyczne. Dla scenariuszy SAP, które są oczekiwane toodeliver produkcji, takich jak wydajność zdecydowanie zaleca toouse serii maszyn wirtualnych, które mogą korzystać z usługi Azure Premium Storage.

Należy pamiętać, ten dysk hello, który zawiera hello systemu operacyjnego i jak firma Microsoft zaleca, hello plików binarnych programu SAP i hello bazy danych (podstawowa maszyna wirtualna), również nie jest już ograniczona too127GB. Go teraz może zawierać maksymalnie too1TB rozmiar. Powinien to być tookeep za mało miejsca, wszystkie hello niezbędnego pliku w tym, na przykład, SAP partii z dziennikami zadań.

Dla więcej sugestie i bardziej szczegółowe informacje, w szczególności dla maszyn wirtualnych systemu DBMS, przejrzyj hello [DBMS Deployment Guide][dbms-guide]

#### <a name="disk-handling"></a>Obsługa dysku
W większości przypadków należy toocreate dodatkowych dysków w kolejności toodeploy hello SAP w bazie danych do hello maszyny Wirtualnej. Wspomnieliśmy o kwestiach związanych z hello liczby dysków w rozdziale [maszyna wirtualna lub dysk struktury wdrożenia SAP] [ planning-guide-5.5.1] tego dokumentu. Witaj portalu Azure umożliwia tooattach i odłączyć dysków, po wdrożeniu podstawowej maszyny Wirtualnej. Witaj dysków może być dołączony/odłączony podczas hello maszyny Wirtualnej jest uruchomiony i działa oraz gdy zostanie zatrzymana. Podczas podłączania na dysku, hello portalu Azure oferuje tooattach pusty dysk lub istniejącego dysku, który w tym momencie nie jest dołączony tooanother maszyny Wirtualnej.

**Uwaga**: dysków w danej chwili może być tylko dołączone tooone maszyny Wirtualnej.

![Dołączanie / odłączanie dysków przy użyciu usługi Azure Standard Storage][planning-guide-figure-1400]

Podczas wdrażania hello nowej maszyny wirtualnej można zdecydować, czy mają toouse zarządzane dysków, albo umieść dysków na kontach magazynu Azure. Jeśli chcesz toouse magazyn w warstwie Premium, zalecamy używanie dysków zarządzanych.

Następnie należy toodecide czy chcesz toocreate nowych i pusty dysk lub czy ma tooselect istniejącego dysku, który został wcześniej przekazany i powinien być dołączony teraz toohello maszyny Wirtualnej.

**WAŻNE**: możesz **nie** mają toouse buforowania hosta z usługi Azure Standard Storage. Należy pozostawić hello hosta pamięci podręcznej preferencji domyślną hello None. Usługa Azure Premium Storage należy włączyć buforowanie odczytu Jeśli cechy operacji We/Wy hello jest przede wszystkim odczytu, takich jak typowy ruch we/wy dla plików danych bazy danych. Buforowanie nie jest zalecane w przypadku pliku dziennika transakcji bazy danych.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Jak tooattach danych na dysku w hello portalu Azure][virtual-machines-linux-attach-disk-portal]
>
> Jeśli są dołączone dyski, należy toolog w toohello wirtualna tooopen hello Menedżera dysków systemu Windows. Jeśli nie włączono automatycznej instalacji, zgodnie z zaleceniami w rozdziale [ustawienie automatycznej instalacji dla dołączone dyski][planning-guide-5.5.3], hello nowo dołączona wolumin wymaga toobe podjęte w trybie online i zainicjować.
>
> ![Linux][Logo_Linux] Linux
>
> Jeśli są dołączone dyski, należy toolog w toohello maszyny Wirtualnej i zainicjuj dyski hello, zgodnie z opisem w [w tym artykule][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]
>
>

- - -
Nowy dysk hello jest pusty dysk, należy również tooformat hello dysku. Formatowania, szczególnie w przypadku systemu DBMS plików danych i dziennika hello zalecenia tej samej jak w przypadku wdrożenia bez systemu operacyjnego hello odnoszą się systemu DBMS.

Jak już wspomniano w rozdziale [hello Microsoft Azure maszyny wirtualnej koncepcji][planning-guide-3.2], konta usługi Azure Storage udostępnia nieskończone zasobów w postaci liczby operacji We/Wy woluminu, wolumin IOPS i danych. Zazwyczaj maszyn wirtualnych systemu DBMS najczęściej dotyczy to. Jeśli masz kilka wysokiej toodeploy maszyn wirtualnych woluminu we/wy w kolejności toostay w ramach limitu hello hello woluminu konta magazynu Azure może być najlepszym toouse oddzielne konto magazynu dla każdej maszyny Wirtualnej. W przeciwnym razie należy toosee jak umożliwiają równoważenie tych maszyn wirtualnych między różnymi kontami magazynu bez naciśnięcie limit hello każdego pojedynczego konta magazynu. Więcej szczegółów, omówiono w hello [DBMS Deployment Guide][dbms-guide]. Ograniczenia te powinny również należy pamiętać czysty aplikacji SAP serwera maszyn wirtualnych lub innych maszyn wirtualnych, które po pewnym czasie może wymagać dodatkowych dysków VHD. Ograniczenia te nie są stosowane, jeśli używasz dysku zarządzanego. Jeśli planujesz toouse magazyn w warstwie Premium, zalecamy użycie dysku zarządzanego.

Innym temacie, który ma zastosowanie w przypadku kont magazynu jest czy hello wirtualne dyski twarde na koncie magazynu jest pobierany z replikacją geograficzną. Replikacja geograficzna jest włączone lub wyłączone na powitania poziom konta magazynu, a nie na powitania poziom maszyny Wirtualnej. Jeśli jest włączona replikacja geograficzna, wirtualne dyski twarde hello w ramach konta magazynu może być replikowane do innego centrum danych Azure w ramach powitalne hello tego samego regionu. Przed podjęciem decyzji o tym, możesz pomyśleć o hello następujące ograniczenia:

Replikacja geograficzna Azure działa lokalnie na każdym dysku VHD na maszynie wirtualnej i nie jest replikowany IOs hello w kolejności chronologicznej w wielu dysków VHD na maszynie wirtualnej. W związku z tym hello wirtualnego dysku twardego czy reprezentuje hello podstawowej maszyny Wirtualnej, a także wszelkie dodatkowe toohello dołączonych dysków VHD maszyny Wirtualnej są replikowane od siebie niezależne. Oznacza to, że istnieje synchronizacja zmian hello hello różnych wirtualne dyski twarde. Witaj fakt, że hello IOs są replikowane niezależnie od hello kolejności, w którym są one zapisywane oznacza, czy replikacja geograficzna nie jest wartość dla serwerów baz danych, które mają swoje bazy danych rozproszone na wielu dysków VHD. W dodatku toohello DBMS również mogą istnieć inne aplikacje, gdzie procesy zapisu lub modyfikowania różnych wirtualne dyski twarde i jeśli jest to kolejność hello tookeep ważne zmiany danych. Jeśli jest to wymagane, nie można włączyć replikację geograficzną na platformie Azure. Zależne muszą czy mają — replikacja geograficzna zestaw maszyn wirtualnych, ale nie dla innego zestawu, można już przydzielić maszyn wirtualnych i ich powiązane wirtualne dyski twarde do różnych kont magazynu mające replikacja geograficzna włączone lub wyłączone.

#### <a name="17e0d543-7e8c-4160-a7da-dd7117a1ad9d"></a>Ustawienie automatycznej instalacji dołączonych dysków
- - -
> ![Windows][Logo_Windows] Windows
>
> Dla maszyn wirtualnych, które są tworzone na podstawie własnych obrazów lub dysków, jest konieczne toocheck i prawdopodobnie Ustaw parametr automatycznej instalacji hello. Ustawienie tego parametru umożliwi hello maszyny Wirtualnej, po ponownym uruchomieniu komputera lub ponownego wdrażania w hello Azure toomount dołączony/dysków zainstalowanych automatycznie ponownie.
> Parametr Hello jest ustawiony dla obrazów hello obsługiwane przez firmę Microsoft w hello Azure Marketplace.
>
> Kolejność tooset hello automatycznej instalacji można znaleźć w dokumentacji hello hello wiersza polecenia pliku wykonywalnego diskpart.exe tutaj:
>
> * [Opcje wiersza polecenia DiskPart](https://technet.microsoft.com/library/bb490893.aspx)
> * [Automatycznej instalacji](http://technet.microsoft.com/library/cc753703.aspx)
>
> okno wiersza polecenia systemu Windows Hello powinien zostać otwarty jako administrator.
>
> Jeśli są dołączone dyski, należy toolog w toohello wirtualna tooopen hello Menedżera dysków systemu Windows. Jeśli nie włączono automatycznej instalacji, zgodnie z zaleceniami w rozdziale [ustawienie automatycznej instalacji dla dołączone dyski][planning-guide-5.5.3], hello nowo dołączona woluminu > musi toobe podjęte w trybie online i zainicjować.
>
> ![Linux][Logo_Linux] Linux
>
> Należy tooinitialize nowo dołączona pusty dysk, zgodnie z opisem w [w tym artykule][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux].
> Należy również tooadd nowe dyski toohello /etc/fstab.
>
>

- - -
### <a name="final-deployment"></a>Końcowe wdrożenia
Witaj końcowego wdrożenia i kolejnych kroków, szczególnie w przypadku zakresie toohello wdrożenia SAP rozszerzone monitorowanie, można znaleźć w artykule toohello [Deployment Guide][deployment-guide].

## <a name="accessing-sap-systems-running-within-azure-vms"></a>Uzyskiwanie dostępu do systemów SAP uruchomionych w maszynach wirtualnych platformy Azure
W scenariuszach tylko w chmurze, może być systemów SAP toothose tooconnect między hello publicznego Internetu przy użyciu graficznego interfejsu użytkownika programu SAP. W tych przypadkach hello poniższych procedur należy toobe zastosowane.

W dalszej części dokumentu hello omówimy hello innych głównych scenariuszy, łączącego systemów tooSAP w wdrożeń między różnymi lokalizacjami, w których ma połączenie lokacja lokacja (tunel VPN) lub Azure ExpressRoute połączenia między lokalnymi hello i systemami Azure.

### <a name="remote-access-toosap-systems"></a>Systemy tooSAP dostępu zdalnego
Za pomocą Menedżera zasobów Azure w modelu klasycznego wcześniejsze hello są domyślne punkty końcowe nie już takie jak. Wszystkie porty maszyny Wirtualnej platformy Azure ARM są otwarte tak długo, jak:

1. Dla podsieci hello lub interfejs sieciowy hello zdefiniowano żadnej grupy zabezpieczeń sieci. TooAzure ruchu sieciowego maszyn wirtualnych może być zabezpieczone za pomocą tak zwane "grup zabezpieczeń sieci". Aby uzyskać więcej informacji, zobacz [co to jest grupa zabezpieczeń sieci (NSG)?][virtual-networks-nsg]
2. Brak usługi równoważenia obciążenia Azure jest zdefiniowany dla interfejsu sieciowego hello   

Zobacz hello architektura odstęp między klasycznego modelu ARM, zgodnie z opisem w [w tym artykule][virtual-machines-azure-resource-manager-architecture].

#### <a name="configuration-of-hello-sap-system-and-sap-gui-connectivity-for-cloud-only-scenario"></a>Konfiguracja hello łączności systemu SAP i SAP graficznego interfejsu użytkownika dla scenariusza tylko w chmurze
Zobacz ten artykuł opisujący szczegóły toothis tematu: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/06/24/sap-gui-connection-closed-when-connecting-to-sap-system-in-azure.aspx>

#### <a name="changing-firewall-settings-within-vm"></a>Zmiana ustawień zapory na maszynie wirtualnej
Może być konieczne tooconfigure hello zapory na tooallow sieci maszyn wirtualnych systemu SAP tooyour ruchu przychodzącego.

- - -
> ![Windows][Logo_Windows] Windows
>
> Domyślnie program hello zapory systemu Windows w maszynie Wirtualnej platformy Azure wdrożonej jest włączona. Teraz należy toobe portu SAP hello tooallow otwarty, w przeciwnym razie hello SAP graficznego interfejsu użytkownika nie będą mogli tooconnect.
> toodo to:
>
> * Otwórz panel sterowania\system i zabezpieczenia\zapora systemu Windows too'Advanced ustawienia.
> * Teraz kliknij prawym przyciskiem myszy reguły ruchu przychodzącego i wybierz opcję "Nową regułę".
> * W hello następującego kreatora wybierz toocreate nową regułę "Port".
> * W hello następnego kroku kreatora hello pozostaw ustawienie hello TCP i typ hello numer portu, który ma tooopen. Ponieważ identyfikator wystąpienia naszych SAP 00, wybraliśmy 3200. Jeśli wystąpienie ma numer innego wystąpienia, powinien zostać otwarty port hello, zdefiniowanych wcześniej według liczby wystąpień hello.
> * Hello następnej części hello kreatora należy tooleave hello elementu "Zezwalaj na połączenia" zaznaczone.
> * W następnym kroku kreatora hello hello należy toodefine czy hello reguła ma zastosowanie do domeny, prywatne i publiczne sieci. Dostosuj go jeśli niezbędne tooyour wymaga. Łączenie z graficznym interfejsem użytkownika SAP z hello poza za pośrednictwem sieci publicznej hello, jednak sieci publicznej toohello toohave hello reguły.
> * W hello ostatniego kroku kreatora hello nazwę hello reguły i zapisać, naciskając przycisk "Zakończ"
>
> Reguła Hello zaczyna obowiązywać natychmiast.
>
> ![Definicja reguły portu][planning-guide-figure-1600]
>
> ![Linux][Logo_Linux] Linux
>
> obrazy systemu Linux Hello w hello Azure Marketplace nie należy włączać zapory iptables hello domyślnie i systemu SAP tooyour połączenia hello powinny działać. Jeśli włączono iptables lub inna zapora, można znaleźć w dokumentacji toohello iptables lub hello używana Zapora tooallow przychodzący ruch tcp za 32xx portu (gdzie xx jest numer systemu hello systemu SAP).
>
>

- - -
#### <a name="security-recommendations"></a>Zalecenia dotyczące zabezpieczeń
Witaj SAP graficznego interfejsu użytkownika nie łączy się natychmiast tooany wystąpień SAP hello (port 32xx), które są uruchomione, ale najpierw łączy się za pomocą programu SAP toohello otworzyć port hello komunikat procesu serwera (port 36xx). W hello poza hello bardzo tego samego portu została użyta przez serwer wiadomość hello hello wewnętrznej komunikacji toohello aplikacji wystąpień. tooprevent lokalnych serwerów aplikacji z przypadkowo komunikację z serwerem komunikat w hello Azure wewnętrzny się, że porty komunikacyjne można zmienić. Zdecydowanie zaleca się toochange hello wewnętrznej komunikacji między serwerem komunikat SAP hello i jego aplikacji wystąpień tooa inny numer portu na komputerach został sklonowany z lokalnymi systemami, takimi jak klon rozwoju projektu testowania itp. Można to zrobić za pomocą parametru profil domyślny hello:

> rdisp/msserv_internal
>
>

zgodnie z opisem w [ustawienia zabezpieczeń dla hello SAP komunikatów serwera](https://help.sap.com/saphelp_nwpi71/helpdata/en/47/c56a6938fb2d65e10000000a42189c/content.htm)

## <a name="96a77628-a05e-475d-9df3-fb82217e8f14"></a>Pojęcia dotyczące tylko w chmurze wdrożenia SAP wystąpień
### <a name="3e9c3690-da67-421a-bc3f-12c520d99a30"></a>Pojedyncze maszyny z programem SAP NetWeaver pokaz/szkolenia scenariusza
![Z jednej systemami pokaz SAP maszyny Wirtualnej w programie hello takie same nazwy maszyny Wirtualnej, samodzielnie w usług Azure Cloud Services][planning-guide-figure-1700]

W tym scenariuszu (zobacz rozdział [tylko w chmurze] [ planning-guide-2.1] tego dokumentu) firma Microsoft wdrażania scenariusza systemu typowe szkolenia/pokaz, gdzie hello pełną szkolenia/pokaz scenariusza znajduje się w jednej maszyny Wirtualnej. Przyjęto założenie, że wdrożenie hello odbywa się za pośrednictwem szablony obrazu maszyny Wirtualnej. Ponadto przyjmujemy, wiele z tych pokaz/szkolenia toobe potrzeby maszyn wirtualnych z hello maszyn wirtualnych o hello tej samej nazwie.

założeń Hello jest utworzona z obrazu maszyny Wirtualnej, zgodnie z opisem w sekcjach rozdziału [przygotowywanie maszyn wirtualnych z programu SAP do platformy Azure] [ planning-guide-5.2] w tym dokumencie.

Witaj sekwencji zdarzeń tooimplement hello scenariusza wygląda następująco:

##### <a name="powershell"></a>PowerShell
* Utwórz nową grupę zasobów dla każdego pozioma szkolenia/pokaz

```powershell
$rgName = "SAPERPDemo1"
New-AzureRmResourceGroup -Name $rgName -Location "North Europe"
```
* Utwórz nowe konto magazynu, jeśli nie chcesz toouse zarządzane dysków

```powershell
$suffix = Get-Random -Minimum 100000 -Maximum 999999
$account = New-AzureRmStorageAccount -ResourceGroupName $rgName -Name "saperpdemo$suffix" -SkuName Standard_LRS -Kind "Storage" -Location "North Europe"
```

* Utwórz nową sieć wirtualną dla każdego szkolenia/pokaz pozioma tooenable hello użycia hello tej samej nazwy hosta i adresy IP. sieć wirtualna Hello jest chroniony przez sieciowej grupy zabezpieczeń, umożliwiający tylko ruch tooport 3389 tooenable pulpitu zdalnego dostępu i port 22 protokołu SSH.

```powershell
# Create a new Virtual Network
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGRDP -Protocol * -SourcePortRange * -DestinationPortRange 3389 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 100
$sshRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGSSH -Protocol * -SourcePortRange * -DestinationPortRange 22 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 101
$nsg = New-AzureRmNetworkSecurityGroup -Name SAPERPDemoNSG -ResourceGroupName $rgName -Location  "North Europe" -SecurityRules $rdpRule,$sshRule

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name Subnet1 -AddressPrefix  10.0.1.0/24 -NetworkSecurityGroup $nsg
$vnet = New-AzureRmVirtualNetwork -Name SAPERPDemoVNet -ResourceGroupName $rgName -Location "North Europe"  -AddressPrefix 10.0.1.0/24 -Subnet $subnetConfig
```

* Tworzenie nowego publicznego adresu IP, które mogą być używane tooaccess hello maszyny wirtualnej na podstawie hello internet

```powershell
# Create a public IP address with a DNS name
$pip = New-AzureRmPublicIpAddress -Name SAPERPDemoPIP -ResourceGroupName $rgName -Location "North Europe" -DomainNameLabel $rgName.ToLower() -AllocationMethod Dynamic
```

* Tworzenie nowego interfejsu sieciowego dla maszyny wirtualnej hello

```powershell
# Create a new Network Interface
$nic = New-AzureRmNetworkInterface -Name SAPERPDemoNIC -ResourceGroupName $rgName -Location "North Europe" -Subnet $vnet.Subnets[0] -PublicIpAddress $pip
```

* Utwórz maszynę wirtualną. W scenariuszu hello tylko w chmurze co maszyna wirtualna ma hello tej samej nazwy. Hello SAP identyfikator SID hello SAP NetWeaver wystąpień w tych maszyn wirtualnych będzie hello takie same jak również. W ramach hello grupy zasobów platformy Azure, nazwę hello hello maszyna wirtualna wymaga toobe unikatowy, ale w różnych grupach zasobów platformy Azure można uruchomić maszyny wirtualne z hello tej samej nazwy. Witaj domyślnego konta "Administrator" systemu Windows lub "główny" dla systemu Linux nie są prawidłowe. W związku z tym nową nazwę użytkownika administratora musi toobe zdefiniowany wraz z hasłem. rozmiar Hello hello maszyny Wirtualnej musi także toobe zdefiniowane.

```powershell
#####
# Create a new virtual machine with an official image from hello Azure Marketplace
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

# select image
$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" -Skus "2012-R2-Datacenter" -Version "latest"
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "SUSE" -Offer "SLES-SAP" -Skus "12-SP1" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "RedHat" -Offer "RHEL" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "Oracle" -Offer "Oracle-Linux" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="osfromimage"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"

$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Windows
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Linux
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a Managed Disk Image
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -Id <Id of Managed Disk Image>
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

* Opcjonalnie dodaj dodatkowe dyski i przywrócić wymaganej zawartości. Należy pamiętać, że wszystkie nazwy obiektów blob (BLOB toohello adresów URL) muszą być unikatowe w obrębie platformy Azure.

```powershell
# Optional: Attach additional VHD data disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
$dataDiskUri = $account.PrimaryEndpoints.Blob.ToString() + "vhds/datadisk.vhd"
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -VhdUri $dataDiskUri -DiskSizeInGB 1023 -CreateOption empty | Update-AzureRmVM

# Optional: Attach additional Managed Disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -DiskSizeInGB 1023 -CreateOption empty -Lun 0 | Update-AzureRmVM
```

##### <a name="cli"></a>Interfejs wiersza polecenia
Hello następującego przykładowego kodu można użyć w systemie Linux. W systemie Windows, albo użyj programu PowerShell zgodnie z powyższym opisem lub dostosowania hello przykład toouse % rgName % zamiast $rgName i ustaw zmienną środowiskową hello za pomocą polecenia Windows hello *ustawić*.

* Utwórz nową grupę zasobów dla każdego pozioma szkolenia/pokaz

```
rgName=SAPERPDemo1
rgNameLower=saperpdemo1
az group create --name $rgName --location "North Europe"
```

* Utwórz nowe konto magazynu

```
az storage account create --resource-group $rgName --location "North Europe" --kind Storage --sku Standard_LRS --name $rgNameLower
```

* Utwórz nową sieć wirtualną dla każdego szkolenia/pokaz pozioma tooenable hello użycia hello tej samej nazwy hosta i adresy IP. sieć wirtualna Hello jest chroniony przez sieciowej grupy zabezpieczeń, umożliwiający tylko ruch tooport 3389 tooenable pulpitu zdalnego dostępu i port 22 protokołu SSH.

```
az network nsg create --resource-group $rgName --location "North Europe" --name SAPERPDemoNSG
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGRDP --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 3389 --access Allow --priority 100 --direction Inbound
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGSSH --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 22 --access Allow --priority 101 --direction Inbound

az network vnet create --resource-group $rgName --name SAPERPDemoVNet --location "North Europe" --address-prefixes 10.0.1.0/24
az network vnet subnet create --resource-group $rgName --vnet-name SAPERPDemoVNet --name Subnet1 --address-prefix 10.0.1.0/24 --network-security-group SAPERPDemoNSG
```

* Tworzenie nowego publicznego adresu IP, które mogą być używane tooaccess hello maszyny wirtualnej na podstawie hello internet

```
az network public-ip create --resource-group $rgName --name SAPERPDemoPIP --location "North Europe" --dns-name $rgNameLower --allocation-method Dynamic
```

* Tworzenie nowego interfejsu sieciowego dla maszyny wirtualnej hello

```
az network nic create --resource-group $rgName --location "North Europe" --name SAPERPDemoNIC --public-ip-address SAPERPDemoPIP --subnet Subnet1 --vnet-name SAPERPDemoVNet
```

* Utwórz maszynę wirtualną. W scenariuszu hello tylko w chmurze co maszyna wirtualna ma hello tej samej nazwy. Hello SAP identyfikator SID hello SAP NetWeaver wystąpień w tych maszyn wirtualnych będzie hello takie same jak również. W ramach hello grupy zasobów platformy Azure, nazwę hello hello maszyna wirtualna wymaga toobe unikatowy, ale w różnych grupach zasobów platformy Azure można uruchomić maszyny wirtualne z hello tej samej nazwy. Witaj domyślnego konta "Administrator" systemu Windows lub "główny" dla systemu Linux nie są prawidłowe. W związku z tym nową nazwę użytkownika administratora musi toobe zdefiniowany wraz z hasłem. rozmiar Hello hello maszyny Wirtualnej musi także toobe zdefiniowane.

```
#####
# Create virtual machines using storage accounts
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password

#####
# Create virtual machines using Managed Disks
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
```

```
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Windows --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Linux --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd> --authentication-type password

#####
# Create a new virtual machine with a Managed Disk Image
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id> --authentication-type password
```

* Opcjonalnie dodaj dodatkowe dyski i przywrócić wymaganej zawartości. Należy pamiętać, że wszystkie nazwy obiektów blob (BLOB toohello adresów URL) muszą być unikatowe w obrębie platformy Azure.

```
# Optional: Attach additional VHD data disks
az vm unmanaged-disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --vhd-uri https://$rgNameLower.blob.core.windows.net/vhds/data.vhd  --new

# Optional: Attach additional Managed Disks
az vm disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --disk datadisk --new
```

##### <a name="template"></a>Szablon
Możesz użyć hello przykładowe szablony w repozytorium azure-Szybki Start — szablony hello w witrynie github.

* [Proste maszyny Wirtualnej systemu Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
* [Proste systemu Windows maszyny Wirtualnej](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
* [Maszyny Wirtualnej z obrazu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)

### <a name="implement-a-set-of-vms-which-need-toocommunicate-within-azure"></a>Implementuje zestaw maszyn wirtualnych, które należy toocommunicate w obrębie platformy Azure
Ten scenariusz tylko w chmurze jest typowy scenariusz do celów szkoleniowych i pokaz, w którym hello oprogramowania reprezentujący hello pokaz/szkolenia scenariusz jest rozłożona na wiele maszyn wirtualnych. Witaj różne składniki zainstalowane w hello różnych maszyn wirtualnych konieczność toocommunicate ze sobą. Ponownie w tym scenariuszu komunikacja sieciowa braku lokalnej lub scenariuszu obejmującym różne pomieszczenia jest wymagana.

Ten scenariusz jest rozszerzeniem instalacji hello w rozdziale opisano [jednej maszyny Wirtualnej z programem SAP NetWeaver pokaz/szkolenia scenariusza] [ planning-guide-7.1] tego dokumentu. W takim przypadku jedna maszyna wirtualna zostanie dodana tooan istniejącą grupę zasobów. W hello następujący przykład hello szkolenia pozioma składa się z programu SAP ASCS/SCS maszynę Wirtualną, maszyny Wirtualnej z systemem, system DBMS i wystąpienia serwera aplikacji SAP maszyny Wirtualnej.

Przed utworzeniem tego scenariusza należy toothink o podstawowych ustawień jak już wykonywane w scenariuszu hello przed.

#### <a name="resource-group-and-virtual-machine-naming"></a>Grupy zasobów i nazwy maszyny wirtualnej
Wszystkie nazwy grupy zasobów musi być unikatowa. Tworzenie własnych schemat nazewnictwa zasobów, takich jak `<rg-name`>-sufiks.

Nazwa maszyny wirtualnej Hello ma unikatowe w obrębie grupy zasobów hello toobe.

#### <a name="set-up-network-for-communication-between-hello-different-vms"></a>Konfigurowanie sieci dla komunikacji między hello różnych maszyn wirtualnych
![Zestaw maszyn wirtualnych w ramach sieci wirtualnej platformy Azure][planning-guide-figure-1900]

tooprevent nazewnictwa kolizji z klony hello tego samego krajobrazów szkolenia/demonstracyjnej, należy toocreate sieci wirtualnej platformy Azure dla każdego orientacji poziomej. Rozpoznawanie nazw DNS, które będą udostępniane przez usługi Azure lub skonfigurować własny serwer DNS poza Azure (opisane tutaj toobe). W tym scenariuszu firma Microsoft nie Konfiguruj własnej DNS. Dla wszystkich maszyn wirtualnych w jednej sieci wirtualnej platformy Azure komunikację za pomocą nazwy hostów zostaną włączone.

Witaj powodów, dla których tooseparate szkolenia lub pokaz krajobrazów sieci wirtualnych i nie tylko zasób może być grup:

* Witaj SAP poziomą ustanowionych potrzeb własną AD/OpenLDAP i serwer domeny musi toobe część każdego krajobrazów hello.  
* Witaj pozioma SAP — konfiguracja ma składników tego toowork potrzeby stałe adresy IP.

Więcej informacji o sieciach wirtualnych platformy Azure i sposobu toodefine ich znajdują się w [w tym artykule][virtual-networks-create-vnet-arm-pportal].

## <a name="deploying-sap-vms-with-corporate-network-connectivity-cross-premises"></a>Wdrażanie SAP maszyn wirtualnych z połączeniem w sieci firmowej (między lokalizacjami)
Uruchom pozioma SAP, a toodivide hello wdrażania od zera dla serwerów systemu DBMS wysokiej jakości, lokalnych zwirtualizowanych środowisk dla warstwy aplikacji i mniejszych warstwy 2 skonfigurowane SAP systemów i IaaS platformy Azure. podstawowe założenia Hello jest, systemów SAP w jednym pozioma SAP potrzeby toocommunicate ze sobą oraz z wielu innych składników oprogramowania wdrożone w firmie hello, niezależnie od ich formularza wdrożenia. Również powinno być żadnych różnic wprowadzonej przez formularz wdrożenia hello hello połączenie przy użyciu graficznego interfejsu użytkownika programu SAP lub innych interfejsów użytkownika. Te warunki można spełnić tylko, gdy będziemy mieć hello Active Directory/OpenLDAP lokalnymi i usługi DNS rozszerzony toohello systemów Azure za pośrednictwem połączenia lokacja do witryny/kilku lokalizacji lub połączeń prywatnych, takich jak usługa Azure ExpressRoute.

W kolejności tooget więcej w tle na powitania szczegóły implementacji SAP na platformie Azure, firma Microsoft zachęca rozdział tooread [pojęcia Cloud-Only wdrożenia SAP wystąpień] [ planning-guide-7] tego dokumentu, który wyjaśnia Tworzy niektóre podstawowe hello Azure oraz jak te używane aplikacje SAP Azure.

### <a name="scenario-of-an-sap-landscape"></a>Scenariusz pozioma SAP
Witaj scenariuszu obejmującym różne pomieszczenia można około opisana jak grafiki hello poniżej:

![Połączenie lokacja-lokacja między lokalnych i dostępnych zasobów platformy Azure][planning-guide-figure-2100]

Powyższy scenariusz Hello opisano scenariusz, w którym hello AD/OpenLDAP lokalnymi i DNS zostały rozszerzone tooAzure. Na stronie lokalne powitania określonego zakresu adresów IP jest zarezerwowany dla subskrypcji platformy Azure. zakres adresów IP Hello zostanie przypisany tooan sieci wirtualnej platformy Azure na powitania po stronie platformy Azure.

#### <a name="security-considerations"></a>Zagadnienia związane z zabezpieczeniami
Hello minimalna wymagana wartość to hello używanie protokołów bezpiecznej komunikacji, takie jak SSL/TLS, aby uzyskać dostęp za pomocą przeglądarki lub połączeniach sieci VPN dla systemu toohello Azure uzyskiwać dostęp do usług. jest założenie Hello firm różnie obsługi hello połączenia sieci VPN między siecią firmową i Azure. Niektóre firmy mogą otworzyć blankly wszystkie porty hello. Niektóre inne firmy może być toobe bardzo dokładne porty muszą tooopen itp.

W tabeli hello poniżej SAP typowe porty komunikacyjne są wyświetlane. Zasadniczo jest wystarczające hello tooopen portu bramą SAP.

| Usługa | Nazwa portu | Przykład `<nn`> = 01 | Domyślny zakres (maksymalna liczba min) | Komentarz |
| --- | --- | --- | --- | --- |
| Dyspozytor |sapdp`<nn>` zobacz * |3201 |3200 – 3299 |Dyspozytor SAP, używany przez SAP graficznego interfejsu użytkownika dla systemu Windows i języka Java |
| Serwer komunikatów |sapms`<sid`> zobacz ** |3600 |bezpłatne sapms`<anySID`> |Identyfikator SID = Identyfikatorem systemu SAP |
| Brama |sapgw`<nn`> zobacz * |3301 |W warstwie bezpłatna |Bramą SAP, używany do komunikacji CPIC i RFC |
| SAP router |sapdp99 |3299 |W warstwie bezpłatna |Tylko nazwy usługi CI (wystąpienia centralnej) może zostać przypisany /etc/services tooan dowolne wartości po zakończeniu instalacji. |

*) nn = liczby wystąpień programu SAP

*) identyfikatora sid = Identyfikatorem systemu SAP

Bardziej szczegółowe informacje dotyczące portów wymaganych przez różne produkty SAP lub usługi za pomocą produktów SAP można znaleźć tutaj <http://scn.sap.com/docs/DOC-17124>.
Z tego dokumentu należy stanie tooopen dedykowanego porty hello urządzenia sieci VPN jest niezbędne dla określonych produktów SAP i scenariuszy.

Mierzy innych zabezpieczeń podczas wdrażania maszyn wirtualnych w takiej sytuacji może być toocreate [sieciowej grupy zabezpieczeń] [ virtual-networks-nsg] toodefine reguły dostępu.

### <a name="dealing-with-different-virtual-machine-series"></a>Dotyczących różnych serii maszyny wirtualnej
W toku hello ostatnich 12 miesięcy firma Microsoft dodała wiele więcej typów maszyny Wirtualnej, które różnią się w liczba Vcpu, pamięci lub większe znaczenie na sprzęcie jest uruchomiona w. Nie wszystkie te maszyny wirtualne są obsługiwane z programu SAP (zobacz obsługiwane typy maszyny Wirtualnej w Uwaga SAP [1928533]). Uruchom niektóre z tych maszyn wirtualnych na inny host generacje sprzętu. W szczegółowości hello Azure skali-jednostki wdrożono uzyskiwania tych generacje sprzętu hosta. Przypadków oznacza, że może wystąpić, gdy hello różnych rozmiarów maszyn wirtualnych nie można uruchomić wybranego na hello tej samej jednostki skalowania. Zestawu dostępności jest ograniczony toospan możliwości hello, jednostki skalowania oparte na różnych sprzętu.  Na przykład hello toorun DBMS na maszynach wirtualnych A5 A11 i hello SAP warstwy aplikacji na maszynach wirtualnych G-Series, użytkownik będzie zmuszony toodeploy pojedynczego systemu SAP lub w innych systemach SAP w różnych zestawów dostępności.

#### <a name="printing-on-a-local-network-printer-from-sap-instance-in-azure"></a>Drukowania na drukarce lokalnej sieci z wystąpieniem SAP na platformie Azure
##### <a name="printing-over-tcpip-in-cross-premises-scenario"></a>Drukowanie za pośrednictwem protokołu TCP/IP w scenariuszu obejmującym różne pomieszczenia
Konfigurowanie drukarek sieciowych TCP/IP, na podstawie lokalnych w maszynie Wirtualnej platformy Azure jest ogólny hello mają takie same jak w sieci firmowej, wykonując tunelu VPN lokacja-lokacja lub nawiązano połączenie ExpressRoute.

- - -
> ![Windows][Logo_Windows] Windows
>
> toodo to:
>
> * Niektóre drukarki sieciowe dostarczane za pomocą Kreatora konfiguracji, co pozwala łatwo tooset się drukarki w maszynie Wirtualnej platformy Azure. Jeśli żadne oprogramowanie Kreator ma rozesłany drukarki hello "manual" jak tooset hello drukarka jest toocreate nowy port TCP/IP drukarki.
> * Otwórz Panel sterowania -> urządzenia i drukarki -> Dodaj drukarkę
> * Wybierz polecenie Dodaj drukarki za pomocą adresu TCP/IP lub nazwy hosta
> * Wpisz adres IP drukarki hello hello
> * Port drukarki 9100 standardowe
> * W razie potrzeby ręcznie zainstaluj hello odpowiedni sterownik drukarki.
>
> ![Linux][Logo_Linux] Linux
>
> * tak samo, jak dla systemu Windows po prostu wykonaj hello standardową procedurę tooinstall drukarki sieciowej
> * Wykonaj hello publicznego Linux przewodniki dotyczące [SUSE](https://www.suse.com/documentation/sles-12/book_sle_deployment/data/sec_y2_hw_print.html) lub [Red Hat i Oracle Linux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Printer_Configuration.html) na temat tooadd drukarki.
>
>

- - -
![Drukowanie w sieci][planning-guide-figure-2200]

##### <a name="host-based-printer-over-smb-shared-printer-in-cross-premises-scenario"></a>Drukarki oparta na hoście za pośrednictwem protokołu SMB (drukarki udostępnionej) w scenariuszu obejmującym różne pomieszczenia
Drukarki oparta na hoście nie są zgodne sieci zgodnie z projektem. Jednak drukarki oparta na hoście mogą być współużytkowane przez komputery w sieci, tak długo, jak drukarka hello jest połączonych tooa zasilania na komputerze. Połącz z firmowej sieci lokacja-lokacja lub ExpressRoute i udostępnianie drukarki lokalnej. Hello protokołu SMB używa NetBIOS zamiast DNS jako nazwa usługi. Nazwa hosta NetBIOS Hello może być inna niż nazwa hosta DNS hello. Standardowa przypadku Hello jest hello hosta NetBIOS i nazwę hosta DNS hello są identyczne. Witaj DNS domeny nie ma sensu w obszarze nazw NetBIOS hello. W związku z tym hello w pełni kwalifikowaną nazwę hosta DNS, składające się z nazwy hosta DNS hello i domeny DNS nie mogą być używane w obszarze nazw NetBIOS hello.

udziału drukarki Hello jest identyfikowane przez nazwę unikatową w sieci hello:

* Nazwę hosta hello SMB (zawsze wymagane).
* Nazwa udziału hello (zawsze wymagane).
* Nazwa domeny hello Jeśli udziału drukarki nie jest hello tej samej domenie co systemu SAP.
* Ponadto udziału drukarki hello tooaccess wymagane może być nazwa użytkownika i hasło.

Instrukcje:

- - -
> ![Windows][Logo_Windows] Windows
>
> Udostępnianie drukarki lokalnej.
> Hello maszyny Wirtualnej platformy Azure Otwórz Eksploratora Windows hello i wprowadź nazwę udziału hello hello drukarki.
> Kreator instalacji drukarki przeprowadzi Cię przez proces instalacji hello.
>
> ![Linux][Logo_Linux] Linux
>
> Oto kilka przykładów dokumentację dotyczącą konfigurowania drukarek sieciowych w systemie Linux lub w tym rozdziale dotyczące drukowania w systemie Linux. Będzie ona działać hello tak samo w Azure maszyny Wirtualnej systemu Linux tak długo, jak hello maszyna wirtualna jest częścią sieci VPN:
>
> * SLES <_Share_or_Windows_Share https://en.opensuse.org/SDB:Printing_via_SMB_ (Samba)>
> * RHEL lub Oracle Linux <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sec-Printer_Configuration.html#s1-printing-smb-printer>
>
>

- - -
##### <a name="usb-printer-printer-forwarding"></a>Drukarki USB (drukarki przekazywania)
Zdolności Azure hello hello usług pulpitu zdalnego tooprovide użytkownikom hello dostępu tootheir drukarki lokalnej urządzenia w sesji zdalnej jest niedostępna.

- - -
> ![Windows][Logo_Windows] Windows
>
> Więcej informacji dotyczących drukowania w systemie Windows można znaleźć tutaj: <http://technet.microsoft.com/library/jj590748.aspx>.
>
>

- - -
#### <a name="integration-of-sap-azure-systems-into-correction-and-transport-system-tms-in-cross-premises"></a>Integracja programu SAP Azure systemów do transportu systemu (TMS) w między lokalizacjami i korekty
Witaj tooexport toobe skonfigurowane potrzeb zmień SAP i System transportu (TMS) i zaimportuj żądania transportu we wszystkich systemach w orientacji poziomej hello. Przyjęto założenie, że hello programowanie wystąpień systemu SAP (deweloperów) znajdują się na platformie Azure hello jakości (QA) i systemów produkcyjnych (PRD) są lokalne. Ponadto przyjęto założenie, że istnieje transportu centralnego katalogu.

##### <a name="configuring-hello-transport-domain"></a>Konfigurowanie hello domeny transportu
Skonfiguruj domenę transportu w systemie Witaj wyznaczone jako hello transportu kontrolera domeny, zgodnie z opisem w [hello Konfigurowanie kontrolera domeny transportu](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm). Użytkownik systemowy, zostanie utworzony TMSADM i hello wymagane RFC docelowy zostanie wygenerowany. Można sprawdzić te połączenia RFC przy użyciu transakcji hello SM59. Rozpoznawanie nazwy hosta musi być włączony w Twojej domenie transportu.

Instrukcje:

* W naszym scenariuszu zdecydowaliśmy hello w lokalnym systemie QAS będzie kontroler domeny CTS hello. Wywołanie STMS transakcji. zostanie wyświetlone okno dialogowe TMS Hello. Wyświetlane jest okno dialogowe Konfigurowanie domeny transportu. (To okno dialogowe pojawia się tylko, jeśli nie skonfigurowano jeszcze domeny transportu.)
* Upewnij się, ten użytkownik hello tworzone jest autoryzowany TMSADM (SM59 -> ABAP połączenia -> TMSADM@E61.DOMAIN_E61 -> Utilities(M) -> Szczegóły -> Test autoryzacji). ekran początkowy Hello transakcji STMS powinny wskazywać, że tego systemu SAP będzie działać jako kontroler hello hello transportu domeny, jak pokazano poniżej:

![Ekran początkowy transakcji STMS na kontrolerze domeny hello][planning-guide-figure-2300]

#### <a name="including-sap-systems-in-hello-transport-domain"></a>W tym systemów SAP w hello domeny transportu
Sekwencja Hello, w tym systemie SAP w domenie transportu wygląda następująco:

* Na powitania deweloperów systemu Azure Przejdź system transportu toohello (klient 000) i wywołać STMS transakcji. Wybierz inne konfiguracji w oknie dialogowym hello i kontynuować obejmują systemu w domenie. Określ hello kontrolera domeny jako hosta docelowego ([w tym systemów SAP w hello domeny transportu](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0c17acc11d1899e0000e829fbbd/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)). Hello system jest teraz uwzględnione w domenie transportu hello toobe oczekiwania.
* Ze względów bezpieczeństwa można wybrać tooconfirm kontrolera domeny wstecz toohello toogo Twojego żądania. Wybierz Przegląd systemu i zatwierdź hello oczekiwania systemu. Następnie upewnij się, że konfiguracja wiersza i hello hello będą przesyłane.

Ten system SAP zawiera hello niezbędne informacje na temat wszystkich hello innych systemów SAP w domenie transportu hello. Na powitania sam czasu, adres hello, wysłania danych nowego systemu SAP hello tooall hello innych systemów SAP, a hello systemu SAP została wprowadzona w profilu transportu hello hello transportu kontroli programu. Sprawdź, czy działają dokumenty RFC i dostępu do katalogu transportu toohello hello domeny.

Kontynuuj hello konfiguracji systemu transportu w zwykły sposób zgodnie z opisem w dokumentacji hello [zmianami i System transportu](http://help.sap.com/saphelp_nw70ehp3/helpdata/en/48/c4300fca5d581ce10000000a42189c/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm).

Instrukcje:

* Upewnij się, że Twoje STMS lokalnie jest poprawnie skonfigurowany.
* Upewnij się, że nazwa hosta hello hello transportu kontrolera domeny można rozwiązać przez maszynę wirtualną na visa Azure i na.
* Wywołanie transakcji STMS -> inne konfiguracji -> obejmują systemu w domenie.
* Upewnij się, połączenie hello hello w lokalnym systemie TMS.
* Skonfiguruj trasy transportu, grup i warstw w zwykły sposób.

W lokacja lokacja połączenia między lokalizacjami scenariuszy, hello opóźnienia między lokalną i platformą Azure nadal może być istotne. Jeśli firma Microsoft wykonaj sekwencji hello transportu obiektów do prac deweloperskich i testowych tooproduction systemów lub pomyśleć o zastosowaniu transportów lub obsługi pakietów toohello różnych systemów, okazuje się, że zależny od lokalizacji hello hello transportu centralnego katalog, niektóre systemy hello wystąpi duże opóźnienie odczytu lub zapisu w katalogu centralnym transportu hello danych. sytuacja Hello jest podobnych konfiguracji pozioma tooSAP gdzie hello różnych systemów rozprzestrzenia się w różnych centrach danych z znacznej odległość między hello centrów danych.

W kolejności toowork wokół takie opóźnienia i systemy hello pracy fast w odczytu lub zapisu tooor z katalogu transportu hello, można skonfigurować dwie domeny transportu STMS (jeden na potrzeby lokalnego. i jeden z systemów hello w domenach transportu hello Azure i link Sprawdź, czy ta dokumentacja wyjaśniającego zasady hello za tę koncepcję w hello SAP TMS: <http://help.sap.com/saphelp_me60/helpdata/en/c4/6045377b52253de10000009b38f889/content.htm?frameset=/en/57/ 38dd924eb711d182bf0000e829fbfe/frameset.htm>.

Instrukcje:

* Konfigurowanie domeny transportu w każdej lokalizacji (lokalne i Azure) przy użyciu transakcji STMS <http://help.sap.com/saphelp_nw70ehp3/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm>
* Łącze hello domen z domeną link i Potwierdź hello łącze między dwiema domenami hello.
  <http://help.SAP.com/saphelp_nw73ehp1/helpdata/en/a3/139838280c4f18e10000009b38f8cf/Content.htm>
* Rozpowszechniać hello konfiguracji toohello połączony system.

#### <a name="rfc-traffic-between-sap-instances-located-in-azure-and-on-premises-cross-premises"></a>RFC ruchu między wystąpieniami programu SAP znajdujący się w usłudze Azure i lokalnego (między lokalizacjami)
RFC ruchu między systemami, które są lokalne i na platformie Azure wymaga toowork. tooset połączenia wywołać transakcji SM59 w systemie źródłowym wymagających toodefine połączenie RFC kierunku hello system docelowy. Konfiguracja Hello jest podobne toohello standardowe ustawienia połączenia RFC.

Przyjęto założenie, w scenariuszu obejmującym różne pomieszczenia hello hello maszyny wirtualne są wykonywania systemów SAP wymagające toocommunicate ze sobą w hello tej samej domenie. W związku z tym hello Instalatora RFC połączenia między systemami SAP nie różnią się od hello kroków instalacji i dane wejściowe w scenariuszach lokalnych.

#### <a name="accessing-local-fileshares-from-sap-instances-located-in-azure-or-vice-versa"></a>Podczas uzyskiwania dostępu do "local" fileshares z wystąpień SAP znajdującego się na platformie Azure lub na odwrót
SAP wystąpień znajdujących się na platformie Azure muszą tooaccess udziałów plików, które znajdują się w firmowych lokalne powitania. Ponadto lokalnego wystąpienia programu SAP konieczne tooaccess udziałów plików, które znajdują się na platformie Azure. należy skonfigurować uprawnienia hello i opcje udostępniania w systemie lokalnym hello udziałów plików hello tooenable. Upewnij się, że porty hello tooopen na powitania sieci VPN lub połączenia ExpressRoute platformy Azure i centrum danych.

## <a name="supportability"></a>Możliwości obsługi
### <a name="6f0a47f3-a289-4090-a053-2521618a28c3"></a>Azure monitorowania rozwiązania dla programu SAP
W kolejności tooenable hello monitorowania SAP znaczeniu krytycznym na Azure hello SAP narzędzi do monitorowania SAPOSCOL lub Agent hosta SAP Pobierz dane hello Azure maszyny wirtualnej usługi hosta za pośrednictwem rozszerzenia monitorowania Azure dla programu SAP. Wymagania hello przez SAP momentu tooSAP bardzo określonych aplikacji Microsoft postanowiła nie toogenerically wdrożenie hello wymaganych funkcji na platformie Azure, ale pozostawić ją dla klientów toodeploy hello niezbędne monitorowania składników i konfiguracje tootheir Maszyny wirtualne działające na platformie Azure. Jednak wdrożenia i cyklu życia zarządzania hello monitorowania składników będzie przede wszystkim zautomatyzowany przez platformę Azure.

#### <a name="solution-design"></a>Projekt rozwiązania
rozwiązanie Hello opracowany tooenable, który SAP monitorowania jest oparty na architekturze hello Agent maszyny Wirtualnej i środowiska rozszerzenia. pomysł Hello platformy Azure VM Agent i rozszerzenia hello jest tooallow instalacji aplikacji oprogramowania dostępne w galerii rozszerzeń maszyny Wirtualnej Azure hello w maszynie Wirtualnej. Witaj zasady ideą to pojęcie jest tooallow (w takich przypadkach hello Azure rozszerzenie monitorowania dla programu SAP), hello wdrożenia specjalnych funkcji w konfiguracji maszyny Wirtualnej i hello takiego oprogramowania w czasie wdrażania.

Witaj "Agent maszyny Wirtualnej" umożliwiającą obsługę określonych rozszerzeń maszyny Wirtualnej platformy Azure w ramach maszyny Wirtualnej jest wstrzykiwane do maszyn wirtualnych systemu Windows, domyślnie na tworzenie maszyny Wirtualnej w portalu Azure hello powitalne. W przypadku SUSE Red Hat lub Oracle Linux agent maszyny Wirtualnej hello jest już częścią obrazu portalu Azure Marketplace. W przypadku, gdy jeden czy przekazać Maszynę wirtualną systemu Linux z lokalnymi tooAzure hello VM agent ma toobe zainstalowany ręcznie.

Witaj podstawowe bloki konstrukcyjne hello monitorowanie rozwiązania na platformie Azure dla programu SAP wygląda następująco:

![Składniki Microsoft Azure rozszerzenia][planning-guide-figure-2400]

Jak pokazano na powyższym diagramie bloku hello, jednej części hello monitorowania rozwiązania dla programu SAP znajduje się w hello obrazu maszyny Wirtualnej platformy Azure i galerii rozszerzeń Azure, który jest replikowany globalnie repozytorium, który jest zarządzany przez operacje Azure. Jest odpowiedzialny za hello hello wspólnego SAP/MS zespół pracujący nad hello Azure wdrożenia SAP toowork operacji Azure toopublish nowe wersje hello Azure rozszerzenie monitorowania dla programu SAP.

Podczas wdrażania nowej maszyny Wirtualnej systemu Windows hello "Agent maszyny Wirtualnej" jest automatycznie dodawany do hello maszyny Wirtualnej. Funkcja Hello tego agenta jest hello toocoordinate ładowania i konfiguracji hello Azure rozszerzeń monitorowania SAP NetWeaver systemów. Dla maszyn wirtualnych systemu Linux hello Agent maszyny Wirtualnej jest już częścią hello Azure Marketplace OS obrazu.

Jednak jest to nadal wymaga toobe wykonywane przez powitania klienta. Jest to hello aktywacji i konfiguracji hello zbieranie danych wydajności. proces Hello powiązanych toohello "Konfiguracja" jest automatycznie przez skrypt programu PowerShell lub polecenia interfejsu wiersza polecenia. Witaj skrypt programu PowerShell można pobrać w Microsoft Azure Script Center hello zgodnie z opisem w hello [Deployment Guide][deployment-guide].

Witaj ogólna architektura hello Azure monitorowania rozwiązania dla programu SAP wygląda następująco:

![Monitorowanie rozwiązania dla programu SAP NetWeaver Azure][planning-guide-figure-2500]

**Hello dokładne instrukcje tooand szczegółowy opis kroków przy użyciu tych poleceń cmdlet programu PowerShell lub polecenia interfejsu wiersza polecenia, podczas wdrażania, wykonaj hello instrukcje podane w hello [Deployment Guide][deployment-guide].**

### <a name="integration-of-azure-located-sap-instance-into-saprouter"></a>Integracja Azure znajduje się wystąpienie SAP do SAProuter
Wystąpienia SAP działające na platformie Azure muszą toobe dostępny z SAProuter również.

![Połączenie routera SAP][planning-guide-figure-2600]

SAProuter umożliwia hello TCP/IP komunikacji między systemami uczestniczących w przypadku braku bezpośredniego połączenia IP. Dzięki temu można korzystać hello, że żadne połączenie na trasie między partnerami komunikacji hello nie jest konieczne na poziomie sieci. Witaj SAProuter nasłuchuje na porcie 3299 domyślnie.
wystąpienia tooconnect SAP poprzez SAProuter należy hello toogive ciąg SAProuter i nazwy hosta z tooconnect wszelkie próby.

## <a name="sap-netweaver-as-java"></a>SAP NetWeaver AS Java
Do tej pory hello fokus hello dokumentu została SAP NetWeaver ogólnie lub hello SAP NetWeaver ABAP stosu. W tej sekcji małych szczególne zagadnienia dotyczące stosu SAP Java hello są wyświetlane. Jednym z najważniejszych SAP NetWeaver Java wyłącznie na podstawie aplikacji hello jest hello SAP Enterprise Portal. Inne SAP NetWeaver aplikacji opartych na jak SAP PI i Menedżera rozwiązania SAP zarówno hello SAP NetWeaver ABAP i stosy Java. W związku z tym Oczywiście istnieje potrzeba tooconsider aspektów pokrewne toohello SAP NetWeaver Java stosu również.

### <a name="sap-enterprise-portal"></a>SAP Enterprise Portal
Instalator Hello portalu SAP w maszynie wirtualnej platformy Azure różnią się od instalacji na lokalnym, jeśli są wdrażane w scenariuszach między lokalizacjami. Ponieważ powitalne DNS jest realizowane przez lokalną hello ustawienia portów dla poszczególnych wystąpień hello może zostać wykonane jako skonfigurowanego lokalnymi. Hello zalecenia i ograniczenia wymienione w tym dokumencie wykonanej do tej pory się ogólnie dla aplikacji, takie jak SAP Enterprise Portal lub hello SAP NetWeaver Java stosu.

![Portal narażonych SAP][planning-guide-figure-2700]

Scenariusz wdrożenia specjalnych niektórych klientów jest hello bezpośredniego ujawnienia hello SAP Enterprise Portal toohello Internet podczas hello maszyny wirtualnej host jest połączony toohello firmową siecią za pośrednictwem tunelu VPN lokacja lokacja lub ExpressRoute. Takiej sytuacji należy toomake się, że określone porty są otwarte i nie jest blokowany przez zaporę lub w sieci grupy zabezpieczeń. Witaj mechanika tego samego potrzebny toobe stosowane, gdy chcesz tooconnect tooan SAP Java wystąpienie z lokalnymi w scenariuszu tylko w chmurze.

Hello portal początkowy identyfikator URI jest http (s):`<Portalserver`>: 5XX00/irj, gdzie portu hello jest tworzony przez 50000 plus (Systemnumber x 100). Hello portalu domyślny system identyfikatora URI SAP 00 jest `<dns name`>.`<azure region` >.Cloudapp.azure.com:PublicPort/irj. Aby uzyskać więcej informacji, należy mieć przyjrzeć się <http://help.sap.com/saphelp_nw70ehp1/helpdata/de/a2/f9d7fed2adc340ab462ae159d19509/frameset.htm>.

![Konfiguracja punktu końcowego][planning-guide-figure-2800]

Aby adres URL hello toocustomize i/lub porty programu SAP Enterprise Portal, sprawdź, czy w tej dokumentacji:

* [Zmień adres URL portalu](http://wiki.scn.sap.com/wiki/display/EP/Change+Portal+URL)
* [Zmienić domyślne numery portów, numery portów portalu](http://wiki.scn.sap.com/wiki/display/NWTech/Change+Default++port+numbers%2C+Portal+port+numbers)

## <a name="high-availability-ha-and-disaster-recovery-dr-for-sap-netweaver-running-on-azure-virtual-machines"></a>Wysokiej dostępności i odzyskiwania awaryjnego (DR) dla programu SAP NetWeaver uruchomione na maszynach wirtualnych platformy Azure
### <a name="definition-of-terminologies"></a>Definicja terminologii
termin Hello **wysokiej dostępności (HA)** jest zazwyczaj powiązane tooa zestawu technologii który minimalizuje zakłóceń IT, zapewniając ciągłość prowadzenia działalności biznesowej usługi IT za pośrednictwem nadmiarowe, odpornej na uszkodzenia lub pracy awaryjnej chronione składniki wewnątrz hello **tego samego** centrum danych. W tym przypadku w ramach jednego regionu Azure.

**Odzyskiwania awaryjnego (DR)** również jest docelowo zminimalizować zakłócenia usług IT i ich odzyskiwania ale wielu **różnych** centrów danych, które są zazwyczaj znajduje się setki kilometrów optymalizacji. W tym przypadku zwykle od różnych regionach platformy Azure w ramach hello tego samego regionu geograficznymi lub ustalonych przez użytkownika jako klient.

### <a name="overview-of-high-availability"></a>Przegląd informacji o wysokiej dostępności
Można oddzielić hello omówienie SAP wysokiej dostępności na platformie Azure na dwie części:

* **Wysoka dostępność infrastruktury platformy Azure**, na przykład wysokiej dostępności mocy obliczeniowej (maszyn wirtualnych), sieci, magazynu itp. oraz korzyści zwiększenia dostępności aplikacji SAP.
* **Wysoka dostępność aplikacji SAP**, na przykład HA programu SAP składników oprogramowania:
  * Serwery aplikacji SAP
  * Wystąpienie programu SAP ASCS/SCS
  * Serwer bazy danych

i jak można je łączyć z infrastrukturą systemu Azure wysokiej dostępności.

SAP wysokiej dostępności na platformie Azure ma pewne różnice w stosunku tooSAP wysokiej dostępności w lokalnym środowisku fizycznym lub wirtualnym. Witaj następujący dokument z programu SAP opisano konfiguracje standardowe SAP wysokiej dostępności w środowiskach wirtualnych w systemie Windows: <http://scn.sap.com/docs/DOC-44415>. Nie istnieje zintegrowane sapinst SAP-HA konfiguracja dla systemu Linux, takich jak istnieje dla systemu Windows. Dotyczące SAP HA lokalnymi dla systemu Linux informacje więcej tutaj: <http://scn.sap.com/docs/DOC-8541>.

### <a name="azure-infrastructure-high-availability"></a>Wysoka dostępność infrastruktury platformy Azure
Obecnie jest umowy SLA dla maszyn wirtualnych na jednym z wartością 99,9%. tooget pomysł, jak dostępności hello jednej maszyny wirtualnej może wyglądać tak, jak można po prostu utworzyć iloczyn hello hello różnych dostępnych umowy SLA platformy Azure: <https://azure.microsoft.com/support/legal/sla/>.

Podstawa Hello obliczania hello to 30 dni w miesiącu lub 43200 minut. W związku z tym przestoju 0,05% odpowiada too21.6 minut. W zwykły sposób dostępność hello hello różnych usług będzie pomnożyć w hello w następujący sposób:

(Usługa dostępności #1/100) * (dostępności usługi #2/100) * (dostępności usługi #3/100) *...

Na przykład:

(99,95/100) * (99,9/100) * (99,9/100) = 0.9975 lub ogólnej dostępności 99.75%.

#### <a name="virtual-machine-vm-high-availability"></a>Wysoka dostępność maszyn wirtualnych (VM)
Istnieją dwa typy zdarzeń platformy Azure, które mogą wpłynąć na dostępność maszyn wirtualnych hello: planowanych konserwacji i nieplanowanych konserwacji.

* Okresowe aktualizacje wprowadzone przez Microsoft toohello bazowy tooimprove platformy Azure są zdarzeń planowanych konserwacji ogólną niezawodność, wydajność i bezpieczeństwo infrastruktury platformy hello, które są uruchamiane maszyny wirtualne.
* Nieplanowana konserwacja zdarzenia wystąpić, gdy sprzęt hello lub infrastruktury fizycznej podstawowej maszyny wirtualnej wystąpił błąd w określony sposób. Mogą być to awarie sieci lokalnej, błędy na dysku lokalnym lub inne awarie na poziomie regału. W przypadku wykrycia takiej awarii hello platformy Azure automatycznie migracji maszyny wirtualnej z hello złej kondycji serwera fizycznego obsługującego maszyny wirtualnej tooa dobrej kondycji serwera fizycznego. Takie zdarzenia występują rzadko, ale może również spowodować tooreboot Twojej maszyny wirtualnej.

Więcej szczegółów można znaleźć w tej dokumentacji: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="azure-storage-redundancy"></a>Nadmiarowość magazynu Azure
Witaj danych na koncie magazynu Microsoft Azure jest zawsze replikowane tooensure trwałości i wysokiej dostępności, spotkania hello umowy SLA magazynu platformy Azure, nawet w powierzchnię hello przejściowych awarii sprzętu.

Ponieważ Magazyn Azure może być utrzymywanie trzy obrazy danych hello domyślnie, RAID5 lub RAID1 na wielu dyskach platformy Azure nie jest konieczne.

Więcej informacji można znaleźć w tym artykule: <http://azure.microsoft.com/documentation/articles/storage-redundancy/>

#### <a name="utilizing-azure-infrastructure-vm-restart-tooachieve-higher-availability-of-sap-applications"></a>Przy użyciu ponownego uruchomienia maszyny Wirtualnej infrastruktury Azure tooAchieve "Wyższej dostępności" aplikacje SAP
Jeśli zdecydujesz się nie toouse funkcje takie jak Windows Server Failover Clustering (WSFC) lub rozrusznik w systemie Linux (obecnie obsługiwana tylko dla SLES 12 lub nowszym), ponowne uruchomienie maszyny Wirtualnej Azure jest używane tooprotect systemu SAP przed planowanych lub nieplanowanych przestojów z hello Infrastruktura Azure serwera fizycznego i ogólnej podstawowej platformy Azure.

> [!NOTE]
> Jest ważne toomention czy głównie ponownego uruchomienia maszyny Wirtualnej Azure chroni maszyny wirtualne i nie aplikacje. Ponowne uruchomienie maszyny Wirtualnej nie zapewnia wysoką dostępność aplikacji SAP, ale oferuje pewien poziom dostępności infrastruktury i w związku z tym pośrednio "wyższej dostępności" systemów SAP. Dostępna jest również nie SLA hello czasu potrwa toorestart maszyny Wirtualnej po awarii hosta planowane lub nieplanowane. W związku z tym ta metoda "wysokiej dostępności" nie jest odpowiedni dla krytycznych składników systemu SAP, takich jak (A) SCS lub systemu DBMS.
>
>

Inny element ważne infrastruktury wysokiej dostępności jest magazynu. Na przykład umowy SLA magazynu platformy Azure jest 99,9% dostępności. Jeśli jeden wdraża wszystkich maszyn wirtualnych z jego dysków do jednego konta magazynu Azure, potencjalne magazynu Azure niedostępności spowoduje niedostępność wszystkich maszyn wirtualnych, które są umieszczone na tym koncie magazynu Azure, a także wszystkie SAP składniki działają w ramach tych maszyn wirtualnych.  

Zamiast wprowadzania wszystkich maszyn wirtualnych do konta magazynu Azure pojedynczego, umożliwia także dedykowanych dla magazynu kont dla każdej maszyny Wirtualnej i w ten sposób zwiększenia ogólnej dostępności maszyny Wirtualnej i SAP aplikacji przy użyciu wielu niezależnych konta magazynu Azure.

Zarządzane dysku systemu Azure automatycznie są umieszczane w hello domeny błędów hello maszyny wirtualnej, które są dołączone. Jeśli dwie maszyny wirtualne w dostępności ustawić i dysków zarządzanych, platformy hello zajmie się dystrybucji hello dysków zarządzanych w różnych domenach awarii również. Jeśli planujesz toouse magazyn w warstwie Premium, zdecydowanie zaleca się również za pomocą zarządzania dyskami.

Przykładowa architektura systemu SAP NetWeaver, który używa konta wysokiej dostępności i magazynu infrastruktury platformy Azure może wyglądać następująco:

![Przy użyciu infrastruktury platformy Azure dostępności "wyżej" HA tooachieve SAP aplikacji][planning-guide-figure-2900]

Przykładowa architektura systemu SAP NetWeaver, który korzysta z infrastrukturą systemu Azure wysokiej dostępności i zarządzane dysków może wyglądać następująco:

![Przy użyciu infrastruktury platformy Azure dostępności "wyżej" HA tooachieve SAP aplikacji][planning-guide-figure-2901]

Krytycznych składników SAP firma Microsoft uzyskuje hello wykonanej do tej pory następujące:

* Wysoką dostępność serwerów aplikacji SAP (AS)

  Wystąpień serwera aplikacji SAP są działanie elementów nadmiarowych. Każdy SAP, ponieważ wystąpienie jest wdrażana na jego własnej maszynie Wirtualnej, działającej w innej Azure usterek i domeny uaktualnienia (zobacz rozdział [domen błędów] [ planning-guide-3.2.1] i [domen uaktualnienia][planning-guide-3.2.2]). To jest zapewniana przez przy użyciu zestawów dostępności Azure (zobacz rozdział [zestawami dostępności Azure][planning-guide-3.2.3]). Potencjalne niedostępności planowane lub nieplanowane Azure awarii lub uaktualnienia domeny spowoduje niedostępność ograniczonej liczby maszyn wirtualnych z ich jako SAP wystąpień.

  Każdy SAP, jak wystąpienie znajduje się w jego własnej konta usługi Azure Storage — potencjalnych niedostępność jedno konto magazynu Azure niedostępności tylko jednej maszyny wirtualnej spowoduje, że z jego SAP wystąpienia. Należy jednak pamiętać, że istnieje limit kont magazynu Azure w ramach jednej subskrypcji platformy Azure. automatyczne uruchamianie tooensure () SCS wystąpienia po ponowny rozruch hello maszyny Wirtualnej, upewnij się, tooset hello Autostart parametr wystąpienia () SCS start profil w rozdziale opisano [przy użyciu Autostart dla wystąpień SAP] [ planning-guide-11.5].
  Przeczytaj również rozdział [wysokiej dostępności dla serwerów aplikacji SAP] [ planning-guide-11.4.1] więcej szczegółów.

  Nawet jeśli w przypadku używania dysków zarządzanych tych dysków są także przechowywane informacje o koncie magazynu Azure i mogą być niedostępne w przypadku awarii magazynu.

* *Wyższy* wystąpienia SCS dostępności SAP (A)

  W tym miejscu możemy wykorzystywać ponownego uruchomienia maszyny Wirtualnej Azure hello tooprotect maszyny Wirtualnej z zainstalowane wystąpienie SCS SAP (A). W hello przypadku planowane lub nieplanowane przestoje Azure serwery, maszyny wirtualne zostanie uruchomiona ponownie na innym serwerze dostępne. Jak wspomniano wcześniej, przede wszystkim ponownego uruchomienia maszyny Wirtualnej Azure chroni maszyny wirtualne i nie aplikacje, w tym przypadku hello wystąpienia SCS, (). Za pomocą hello ponownego uruchomienia maszyny Wirtualnej będziemy pośrednio "wyższej dostępności" wystąpienia SCS SAP (A). automatyczne uruchamianie tooinsure () SCS wystąpienia po ponowny rozruch hello maszyny Wirtualnej, upewnij się, parametr Autostart tooset w wystąpieniu () SCS start profil w rozdziale opisano [przy użyciu Autostart dla wystąpień SAP][planning-guide-11.5]. Oznacza to, że hello (A) SCS wystąpienie jako pojedynczy punkt awarii (SPOF) w jednej maszyny Wirtualnej będzie hello współczynnik dominującego hello dostępność hello całego poziomej SAP.

* *Wyższy* dostępności serwera z bazami danych

  W tym miejscu przypadek użycia podobnych toohello SCS SAP (A) wystąpienia, możemy korzystać z ponownego uruchomienia maszyny Wirtualnej Azure tooprotect hello maszyny Wirtualnej z zainstalowanego oprogramowania systemu DBMS i firma Microsoft zapewnienia "wyższej dostępności" DBMS oprogramowania przez ponowne uruchomienie maszyny Wirtualnej.
  DBMS uruchomionych w jednej maszyny Wirtualnej jest również SPOF i jest współczynnik dominującego hello hello dostępność hello całego poziomej SAP.

### <a name="sap-application-high-availability-on-azure-iaas"></a>SAP wysoką dostępność aplikacji na IaaS platformy Azure
tooachieve pełne SAP systemu wysokiej dostępności, potrzebujemy tooprotect wszystkich krytycznych składników systemu SAP, na przykład nadmiarowe SAP serwerów aplikacji, a unikatowy składników (na przykład pojedynczy punkt awarii), takich jak wystąpienie SCS SAP (A) i systemu DBMS.

#### <a name="5d9d36f9-9058-435d-8367-5ad05f00de77"></a>Wysoka dostępność dla serwerów aplikacji SAP
Dla wystąpień serwerów/okno aplikacji SAP hello nie jest konieczne toothink o rozwiązaniu określonego wysokiej dostępności. Wysoka dostępność po prostu odbywa się przez nadmiarowości i tym samym mających wystarczającą ilość je w różnych maszyn wirtualnych. One wszystkich należy umieścić w hello tego samego zestawu dostępności Azure tooavoid, który hello maszyny wirtualne mogły zostać zaktualizowane na powitania jednocześnie podczas zaplanowanej konserwacji przestoju. podstawowe funkcje Hello, która opiera się na różnych uaktualnienie i domen błędów w ramach jednostki skalowania Azure już została wprowadzona w rozdziale [domen uaktualnienia][planning-guide-3.2.2]. Zestawy dostępności Azure były widoczne w rozdziale [zestawami dostępności Azure] [ planning-guide-3.2.3] tego dokumentu.

Brak nie nieograniczoną liczbę usterek i domen uaktualnienia, używanego przez Azure zestawu dostępności w ramach jednostki skalowania Azure. Oznacza to, że wprowadzenia liczby maszyn wirtualnych do jednego zestawu dostępności, wcześniej lub później więcej niż jedna maszyna wirtualna kończy się w hello błędów tego samego lub do domeny uaktualnienia.

Wdrażanie serwera aplikacji SAP kilka wystąpień w ich dedykowanych maszyn wirtualnych i przy założeniu, że dotarliśmy pięć domen uaktualnienia hello poniższej ilustracji pojawia się na końcu hello. Hello rzeczywiste maksymalna liczba domen błędów i aktualizacji w ramach zestawu dostępności może zmieniać w przyszłości hello:

![HA SAP serwerów aplikacji na platformie Azure][planning-guide-figure-3000]

Więcej szczegółów można znaleźć w tej dokumentacji: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="high-availability-for-hello-sap-ascs-instance-on-windows"></a>Wysoka dostępność dla hello wystąpienia SCS SAP (A) w systemie Windows
Windows Server Failover Cluster (WSFC) jest wystąpieniem SAP (A) SCS hello tooprotect często używane rozwiązanie. On również jest zintegrowany sapinst w postaci "Instalacja HA". W tym momencie hello infrastruktury platformy Azure nie jest możliwe tooprovide hello funkcji tooset się hello wymagane klastra pracy awaryjnej systemu Windows Server hello sam sposób, jak jest wykonywane lokalnie.

Począwszy od stycznia 2016 platformy w chmurze Azure hello systemem operacyjnym Windows hello nie zapewnia możliwości hello na dysku współużytkowane dwóch maszyn wirtualnych platformy Azure przy użyciu udostępnionego woluminu klastra.

Gdy prawidłowym rozwiązaniem jest użycie hello 3rd firm, co zapewnia udostępniony wolumin za pomocą replikacji synchroniczne i przezroczysty dysku, który może zostać zintegrowane usługi WSFC. Tej metody oznacza, że tylko hello aktywnego węzła klastra jest możliwe tooaccess jeden dysk hello kopiuje w punkcie w czasie. Począwszy od stycznia 2016 HA tej konfiguracji jest obsługiwanych tooprotect hello SCS SAP (A) wystąpieniem na Windows System operacyjny gościa na maszynach wirtualnych Azure w połączeniu z 3rd firm SIOS DataKeeper.

Hello SIOS DataKeeper rozwiązanie zapewnia udostępniony dysk tooWindows zasobów klastra klastrów trybu Failover dzięki użyciu:

* Dodatkowe VHD Azure dołączony tooeach maszyn wirtualnych hello (VM), które znajdują się w konfiguracji klastra systemu Windows
* SIOS DataKeeper Cluster Edition uruchomione w obu węzłach maszyny Wirtualnej
* O SIOS DataKeeper Cluster Edition skonfigurowane w taki sposób, że synchronicznie odzwierciedla zawartość hello hello dodatkowe VHD dołączony woluminu z źródła maszyn wirtualnych tooadditional wirtualny dysk twardy dołączony woluminu docelowego maszyny Wirtualnej.
* SIOS DataKeeper abstrakcyjność hello źródłowa i docelowa woluminy lokalne i przedstawiające ich tooWindows klastra pracy awaryjnej jako pojedynczy udostępniony dysk.

Wszystkie szczegółowe informacje można znaleźć na temat tooinstall klastra pracy awaryjnej systemu Windows z SIOS DataKeeper i SAP w hello [klastrowanie SAP ASCS wystąpienia przy użyciu klastra trybu Failover systemu Windows Server na platformie Azure za pomocą SIOS DataKeeper] [ ha-guide-classic]oficjalny dokument.

#### <a name="high-availability-for-hello-sap-ascs-instance-on-linux"></a>Wysoka dostępność dla hello wystąpienia SCS SAP (A) w systemie Linux
Począwszy od grudnia 2015 jest również dysku tooshared równoważne usługi WSFC dla maszyn wirtualnych systemu Linux na platformie Azure. Alternatywne rozwiązania z wykorzystaniem 3rd firm, takich jak SIOS dla systemu Windows nie są weryfikowane jeszcze uruchamiania SAP w systemie Linux na platformie Azure.

#### <a name="high-availability-for-hello-sap-database-instance"></a>Wysoka dostępność dla wystąpienia bazy danych SAP hello
Witaj SAP DBMS HA instalacji standardowej opiera się na dwóch DBMS maszyn wirtualnych, gdy jest używana funkcja wysokiej dostępności systemu DBMS tooreplicate danych z hello active DBMS wystąpienia toohello drugie maszyny Wirtualnej do pasywnej wystąpienia systemu DBMS.

Wysoka dostępność i odzyskiwaniem po awarii funkcji odzyskiwania systemu DBMS w ogólne, jak również określonego systemu DBMS opisanym w hello [DBMS Deployment Guide][dbms-guide].

#### <a name="end-to-end-high-availability-for-hello-complete-sap-system"></a>Wysoka dostępność na trasie dla hello całego systemu SAP
Poniżej przedstawiono dwa przykłady pełną SAP NetWeaver HA architektury na platformie Azure — jeden dla systemu Windows i jeden dla systemu Linux.

Niezarządzane tylko dysków: hello pojęcia opisane poniżej może być konieczne toobe naruszony nieco podczas wdrażania wielu systemów SAP hello liczba wdrożonych maszyn wirtualnych są przekracza limit maksymalnej hello kont magazynu dla subskrypcji. W takich przypadkach wirtualne dyski twarde maszyny wirtualne muszą toobe łączyć w jedno konto magazynu. Zwykle będzie to nie łącząc warstwy aplikacji wirtualnych dysków twardych SAP maszyn wirtualnych różnych systemów SAP.  Możemy również łączyć różnych wirtualne dyski twarde różnych DBMS maszyn wirtualnych w różnych systemów SAP w jedno konto magazynu Azure. Dzięki temu pamiętając o hello limity liczby kont magazynu Azure (<https://azure.microsoft.com/documentation/articles/storage-scalability-targets>)


##### <a name="windowslogowindows-ha-on-windows"></a>![Windows][Logo_Windows] HA w systemie Windows
![Architektura HA SAP NetWeaver aplikacji z programem SQL Server w IaaS platformy Azure][planning-guide-figure-3200]

po konstrukcji Azure Hello są używane systemu SAP NetWeaver hello, toominimize wpływ na infrastrukturę problemy i stosowanie poprawek hosta:

* Witaj całego systemu jest wdrażana na platformie Azure (wymagane — system DBMS warstwy, () wystąpienia SCS i kompletna aplikacja warstwy potrzeby toorun w tej samej lokalizacji hello).
* Witaj całego systemu jest uruchamiany w ramach jednej subskrypcji platformy Azure (wymagane).
* Witaj całego systemu jest uruchamiany w ramach jednej sieci wirtualnej platformy Azure (wymagane).
* nawet w przypadku wszystkich hello maszyn wirtualnych należących toohello jest możliwe oddzielenie Hello hello maszyn wirtualnych z jednego systemu SAP do trzech zestawów dostępności tej samej sieci wirtualnej.
* Wszystkich maszyn wirtualnych uruchomionych wystąpień systemu DBMS jednego systemu SAP znajdują się w jednym zestawie dostępności. Przyjęto założenie, że istnieje więcej niż jedna maszyna wirtualna uruchomionych wystąpień systemu DBMS na system od macierzystego systemu DBMS wysokiej dostępności, które są używane funkcje, takie jak AlwaysOn programu SQL Server i Oracle Data Guard.
* Wszystkich maszyn wirtualnych uruchomionych wystąpień systemu DBMS użyć własnych konta magazynu. System DBMS plików danych i dziennika są replikowane z jednego konta tooanother magazynu konto magazynu przy użyciu systemu DBMS wysokiej dostępności funkcji, które synchronizują dane hello. Niedostępność jedno konto magazynu spowoduje niedostępność jednego węzła klastra systemu Windows SQL, ale hello całej usługi SQL Server.
* Wszystkie maszyny wirtualne uruchomione wystąpienie jednego systemu SAP () SCS są w jednym zestawie dostępności. Windows Server Failover Cluster (WSFC) jest skonfigurowany w ramach tych maszyn wirtualnych tooprotect hello (A) SCS wystąpienia.
* Wszystkie maszyny wirtualne uruchomione wystąpienia () SCS Użyj własne konta magazynu. (A) SCS wystąpienia pliki i foldery globalne SAP są replikowane z jednego konta tooanother magazynu konto magazynu przy użyciu replikacji SIOS DataKeeper. Niedostępność jedno konto magazynu spowoduje, że niedostępności jednego (A) systemu Windows SCS węźle klastra, ale nie hello całego () SCS usługi.
* WSZYSTKIE VMs hello reprezentujący warstwa serwera aplikacji SAP hello znajdują się w trzecim zestawu dostępności.
* WSZYSTKICH serwerów aplikacji SAP uruchomionych maszyn wirtualnych hello użyć własnych konta magazynu. Niedostępność jedno konto magazynu spowoduje niedostępność serwera aplikacji SAP, gdy inne AS SAP kontynuować toorun.

następujące Hello rysunek ilustrowane hello, które same poziomą, za pomocą zarządzania dyskami.

![Architektura HA SAP NetWeaver aplikacji z programem SQL Server w IaaS platformy Azure][planning-guide-figure-3201]

##### <a name="linuxlogolinux-ha-on-linux"></a>![Linux][Logo_Linux] HA w systemie Linux
Architektura powitania dla SAP HA w systemie Linux na platformie Azure jest zasadniczo hello takie same jak w przypadku systemu Windows, jak opisano powyżej. Od stycznia 2016 nie będzie żadnych SAP (A) SCS HA rozwiązania jeszcze obsługiwane w systemie Linux na platformie Azure

W rezultacie zgodnie ze stycznia 2016 roku systemu SAP Linux Azure nie można osiągnąć hello tym samym dostępności jako systemu SAP systemu Windows Azure z powodu brakującego wysokiej dostępności dla wystąpienia SCS hello (A) i hello bazy danych SAP ASE jednego wystąpienia.

### <a name="4e165b58-74ca-474f-a7f4-5e695a93204f"></a>Przy użyciu Autostart dla wystąpień SAP
SAP oferowane funkcji hello wystąpień SAP toostart natychmiast po hello początku hello systemu operacyjnego w ramach hello maszyny Wirtualnej. Witaj kolejnych kroków zostały udokumentowane w artykule bazy wiedzy SAP [1909114]. Jednak SAP jest nie rekomendowania toouse hello ustawienia ponieważ nie istnieje bez formantu w kolejności hello ponownego uruchamiania wystąpienie, zakładając, że otrzymano wpływ na więcej niż jedną maszynę Wirtualną lub uruchomienia wielu wystąpień dla maszyny Wirtualnej. Zakładając, że typowy scenariusz Azure jednego wystąpienia serwera aplikacji SAP w przypadku maszyny Wirtualnej i hello jednej maszyny wirtualnej po pewnym czasie ponownie uruchomić pobieranie, hello Autostart nie są naprawdę ważne i można ją włączyć przez dodanie tego parametru:

    Autostart = 1

Do hello start profilu hello wystąpienia SAP ABAP i/lub Java.

> [!NOTE]
> Parametr Autostart Hello może mieć także niektóre downfalls. Bardziej szczegółowo wyzwalaczy parametru hello hello początku wystąpienia SAP ABAP lub Java, czy hello związane z usługi systemu Windows i Linux wystąpienia hello jest uruchomiona. Czy na pewno sytuacja hello systemu operacyjnego hello jest uruchamiany. Jednak ponowne uruchomienie usługi SAP są również wspólnej operacją dla zarządzania cyklem życia oprogramowania SAP funkcji, takich jak SUM lub innych aktualizacji lub uaktualnienia. Te funkcje nie są oczekiwane toobe wystąpienia automatycznie uruchomiona ponownie na wszystkie. W związku z tym parametru Autostart hello powinno zostać wyłączone przed uruchomieniem takie zadania. Parametr Autostart Hello powinien nie również w wystąpieniach programu SAP, które są klastrowane, takich jak ASCS/SCS/CI.
>
>

Można znaleźć dodatkowe informacje na temat autostart dla SAP wystąpień w tym miejscu:

* [Uruchomienie/zatrzymanie SAP wraz z systemem Unix serwera uruchamiania/zatrzymywania](http://scn.sap.com/community/unix/blog/2012/08/07/startstop-sap-along-with-your-unix-server-startstop)
* [Uruchamianie i zatrzymywanie SAP NetWeaver zarządzania agentami](https://help.sap.com/saphelp_nwpi711/helpdata/en/49/9a15525b20423ee10000000a421938/content.htm)
* [Jak tooenable auto-Start elementu HANA bazy danych](http://www.freehanatutorials.com/2012/10/how-to-enable-auto-start-of-hana.html)

### <a name="larger-3-tier-sap-systems"></a>Większe systemów SAP 3-warstwowej
Aspekty wysokiej dostępności konfiguracje SAP 3-warstwowej otrzymano omówione już we wcześniejszych sekcjach. Ale co o systemach, w którym wymagania dotyczące serwera DBMS hello są zbyt duże toohave ten znajduje się na platformie Azure, ale warstwy aplikacji hello SAP można ją wdrożyć na platformie Azure?

#### <a name="location-of-3-tier-sap-configurations"></a>Lokalizacja 3-warstwowej SAP konfiguracji
Nie jest warstwy aplikacji hello obsługiwanych toosplit się lub aplikacja hello i warstwy DBMS między lokalną i platformą Azure. Systemu SAP jest całkowicie wdrożonych lokalnie lub na platformie Azure. Nie jest również obsługiwany toohave niektóre serwery aplikacji hello Uruchamianie lokalne i inne na platformie Azure. To hello dyskusji hello punktu początkowego. Możemy również nie są obsługiwane toohave hello DBMS składniki systemu SAP i hello warstwa serwera aplikacji SAP wdrożone w dwóch różnych regionach platformy Azure. Na przykład DBMS w warstwie aplikacji zachodnie stany USA i SAP w środkowe stany USA. Przyczyna nie obsługuje takiej konfiguracji jest czułość opóźnienia hello hello SAP NetWeaver architektury.

Za pośrednictwem przebiegu hello danych w ciągu ostatniego roku partnerów center opracowany regionów tooAzure wspólnej lokalizacji. Wspólnej często są to następujące lokalizacje w sąsiedztwie bardzo toohello fizycznych usługi Azure data centrów w obrębie regionu Azure. połączenia trwałe z hello wspólnej lokalizacji za pośrednictwem usługi na platformie Azure i niedaleko Hello może spowodować opóźnienia, które jest mniejszy niż 2 ms. W takich przypadkach możliwe jest toolocate hello DBMS warstwy (łącznie z magazynem sieci SAN/NAS) w taki wspólnej lokalizacji i warstwy aplikacji SAP hello na platformie Azure. Począwszy od grudnia 2015 r. nie mamy żadnych wdrożeń tak jak. Ale różnych klientów z wdrożenia aplikacji z systemem innym niż SAP korzystają z takiego podejścia już.

### <a name="offline-backup-of-sap-systems"></a>Systemy kopii zapasowej SAP w trybie offline
Zależne od hello SAP Konfiguracja wybierze (warstwy 2 lub 3-warstwowej) może być tooback muszą się. zawartość Hello hello samej maszyny Wirtualnej oraz toohave kopię zapasową bazy danych hello. Witaj związane z bazami danych kopie zapasowe są oczekiwane toobe odbywa się za pomocą metody bazy danych. Szczegółowy opis hello różnych baz danych, można znaleźć w [przewodnik DBMS][dbms-guide]. Na hello drugiej strony, hello danych SAP kopię zapasową można w sposób w trybie offline (w tym również hello bazy danych zawartości) zgodnie z opisem w tej sekcji lub w trybie online zgodnie z opisem w następnej sekcji hello.

Kopia zapasowa offline Hello zasadniczo wymagają wyłączenia maszyny Wirtualnej za pośrednictwem portalu Azure hello hello i kopii dysku podstawowego VM hello oraz wszystkich dołączonych dysków toohello maszyny Wirtualnej. Czy to zachowanie punktu w czasie obraz powitania maszyny Wirtualnej i jej skojarzone dyski. Kopie zapasowe"toocopy hello" zaleca się do innego konta magazynu Azure. Dlatego hello procedury opisanej w rozdziale [kopiowanie dysków między kontami magazynu Azure] [ planning-guide-5.4.2] tego dokumentu będą miały zastosowania.
Oprócz zamknięcia hello przy użyciu hello Azure portal, co także zrobić to za pomocą programu Powershell lub interfejsu wiersza polecenia zgodnie z opisem w tym miejscu: <https://azure.microsoft.com/documentation/articles/virtual-machines-deploy-rmtemplates-powershell/>

Przywracanie tego stanu może składać się usunięcia hello podstawowej maszyny Wirtualnej oraz jak hello oryginalnych dysków hello podstawowej maszyny Wirtualnej i zapisane dysków toohello oryginalnego konta magazynu lub grupę zasobów zarządzanych dysków i ponowne wdrożenie systemu hello hello dysków zainstalowanych kopiowanie ponownie.
W tym artykule przedstawiono przykład sposobu tooscript tego procesu w programie Powershell: <http://www.westerndevs.com/azure-snapshots/>

Upewnij się, że tooinstall nowej licencji SAP przywracanie kopii zapasowej maszyny Wirtualnej, zgodnie z powyższym opisem tworzy nowy klucz sprzętu.

### <a name="online-backup-of-an-sap-system"></a>Kopii zapasowych online systemu SAP
Tworzenie kopii zapasowych zgodnie z opisem w hello DBMS odbywa się za pomocą metod specyficznych dla systemu DBMS hello [przewodnik DBMS][dbms-guide].

Innych maszyn wirtualnych w systemie SAP hello utworzeniem kopii zapasowej za pomocą funkcji Kopia zapasowa maszyny wirtualnej Azure. Kopia zapasowa maszyny wirtualnej platformy Azure został wprowadzony na początku 2015 i w tym samym czasie jest tooback standardowe metody zapasowej pełną maszyny Wirtualnej na platformie Azure. Kopia zapasowa Azure przechowuje kopie zapasowe hello na platformie Azure i pozwala ponownie przywracania maszyny wirtualnej.

> [!NOTE]
> Począwszy od grudnia 2015 przy użyciu kopii zapasowej maszyny Wirtualnej nie przechowuje hello Unikatowy identyfikator maszyny Wirtualnej używanej do SAP licencjonowania. Oznacza to, że przywracanie z kopii zapasowej maszyny Wirtualnej wymaga instalacji klucza licencji SAP as hello przywrócić maszyny Wirtualnej jest uznawany za toobe nowej maszyny Wirtualnej i nie może zastąpić ten wcześniejsze, który został zapisany.
>
> ![Windows][Logo_Windows] Windows
>
> Teoretycznie maszyn wirtualnych, które wykonywania może być kopie zapasowe baz danych w sposób ciągły, a także jeśli hello DBMS system obsługuje usługi VSS systemu Windows hello (usługi kopiowania woluminów w tle <https://msdn.microsoft.com/library/windows/desktop/bb968832 (v=vs.85).aspx >), na przykład program SQL Server wykonuje.
> Należy jednak pamiętać, który oparty na wykonywanie kopii zapasowych maszyny Wirtualnej platformy Azure, które przywraca w momencie baz danych nie są możliwe. Dlatego zaleca się tooperform kopie zapasowe baz danych z funkcjami systemu DBMS zdejmując to zadanie kopii zapasowej maszyny Wirtualnej Azure.
>
> tooget zapoznać się z kopii zapasowej maszyny wirtualnej platformy Azure Uruchom tutaj: <https://docs.microsoft.com/azure/backup/backup-azure-vms>.
>
> Inne możliwości są toouse kombinacji programu Microsoft Data Protection Manager zainstalowane na maszynie Wirtualnej platformy Azure i kopia zapasowa Azure do wykonywania kopii zapasowej i przywracania bazy danych. Więcej informacji można znaleźć tutaj: <https://docs.microsoft.com/azure/backup/backup-azure-dpm-introduction>.  
>
> ![Linux][Logo_Linux] Linux
>
> Nie ma żadnych równoważne tooWindows VSS w systemie Linux. W związku z tym tylko plik spójne kopie zapasowe są możliwe, ale nie spójnych z aplikacją kopii zapasowych. Witaj kopii zapasowej systemu DBMS SAP ma się odbywać za pomocą funkcji systemu DBMS. Witaj systemu plików, w tym dane dotyczące SAP hello może zostać zapisany, na przykład za pomocą tar zgodnie z opisem w tym miejscu: <http://help.sap.com/saphelp_nw70ehp2/helpdata/en/d3/c0da3ccbb04d35b186041ba6ac301f/content.htm>
>
>

### <a name="azure-as-dr-site-for-production-sap-landscapes"></a>Azure jako lokacja DR dla krajobrazów SAP produkcji
Ponieważ Mid 2014 rozszerzenia toovarious składników funkcji Hyper-V, programu System Center i Azure Włącz użycie hello Azure jako lokacja DR dla maszyny wirtualne z systemami lokalnymi oparte na funkcji Hyper-V.

Blog, opisujące, jak toodeploy to rozwiązanie jest opisanych tutaj: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/11/19/protecting-sap-solutions-with-azure-site-recovery.aspx>.

## <a name="summary"></a>Podsumowanie
Witaj klucz wskazuje wysokiej dostępności dla systemów SAP na platformie Azure są:

* W tym momencie hello SAP pojedynczego punktu awarii nie można dokładnie zabezpieczyć hello sam sposób, jak można zrobić w przypadku wdrożeń lokalnych. Hello przyczyn jest to, że klastry udostępnionych dysków nie jeszcze można utworzyć na platformie Azure bez użycia hello 3 firmy.
* Dla warstwy DBMS hello należy toouse DBMS funkcje, które nie bazuje na technologii klastra udostępnionego dysku. Szczegółowe informacje są udokumentowane w hello [przewodnik DBMS][dbms-guide].
* wpływ hello toominimize problemów w obrębie domen błędów w hello Azure konserwacja infrastruktury lub hosta, należy korzystać z zestawami dostępności Azure:
  * Zalecane jest toohave jeden zbiór dostępności dla warstwy aplikacji hello SAP.
  * Zalecane jest toohave zbiór oddzielne dostępności dla warstwy SAP DBMS hello.
  * NIE jest zalecane hello tooapply, ustawione w tym samym dostępności dla maszyn wirtualnych różnych systemów SAP.
  * Zalecane jest toouse dysków zarządzanych w warstwie Premium.
* Do celów tworzenia kopii zapasowej hello SAP DBMS warstwy, sprawdź, czy hello [przewodnik DBMS][dbms-guide].
* Tworzenie kopii zapasowej wystąpienia okna dialogowego SAP sens małego ponieważ jest zwykle szybsze tooredeploy prostego okna dialogowego wystąpień.
* Tworzeniu kopii zapasowych hello maszyny Wirtualnej zawierający katalogu globalnego hello hello systemu SAP i z nią wszystkie profile hello różnych wystąpień hello, sensu i powinny być wykonywane przy użyciu kopii zapasowej systemu Windows lub, na przykład tar w systemie Linux. Ponieważ ma różnic systemu Windows Server 2008 (R2) i Windows Server 2012 (R2), które stał się łatwiejsze tooback przy użyciu hello zwalnia nowszą systemu Windows Server, zaleca się toorun systemu Windows Server 2012 (R2) jako systemu operacyjnego gościa.
