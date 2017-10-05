---
title: "SAP NetWeaver na maszynach wirtualnych Azure — przewodnik wdrażania DBMS | Dokumentacja firmy Microsoft"
description: "SAP NetWeaver na maszynach wirtualnych Azure (maszyny wirtualne) — przewodnik wdrażania DBMS"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: e0e05b5e-47aa-4c1e-bf83-0d62ee8f614e
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cc7c85382d8f8183ef3eb3cc7496b012808148e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--dbms-deployment-guide"></a>SAP NetWeaver na maszynach wirtualnych Azure Windows (VM) — przewodnik wdrażania DBMS
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
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md 
[dbms-guide-2.1]:#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:#c8e566f9-21b7-4457-9f7f-126036971a91 
[dbms-guide-2.3]:#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:#f9071eff-9d72-4f47-9da4-1852d782087b 
[dbms-guide-5.6]:#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 
[dbms-guide-5.8]:#9053f720-6f3b-4483-904d-15dc54141e30 
[dbms-guide-5]:#3264829e-075e-4d25-966e-a49dad878737 
[dbms-guide-8.4.1]:#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:#23c78d3b-ca5a-4e72-8a24-645d141a3f5d 
[dbms-guide-8.4.3]:#77cd2fbb-307e-4cbf-a65f-745553f72d2c 
[dbms-guide-8.4.4]:#f77c1436-9ad8-44fb-a331-8671342de818 
[dbms-guide-900-sap-cache-server-on-premises]:#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md 
[deployment-guide-2.2]:sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 
[deployment-guide-3.1.2]:sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab 
[deployment-guide-3.2]:sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 
[deployment-guide-3.3]:sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 
[deployment-guide-3.4]:sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e 
[deployment-guide-4.1]:sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 
[deployment-guide-4.2]:sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc 
[deployment-guide-4.4.2]:sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 
[deployment-guide-4.4]:sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d 
[deployment-guide-4.5.1]:sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 
[deployment-guide-4.5.2]:sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f 
[deployment-guide-4.5]:sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca 
[deployment-guide-5.1]:sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 
[deployment-guide-5.2]:sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 
[deployment-guide-5.3]:sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 

[deployment-guide-configure-monitoring-scenario-1]:sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b 
[deployment-guide-configure-proxy]:sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d 
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b 

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md  
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f 
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a 
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c 
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef 
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a 
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d 
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 

[planning-guide-figure-100]:./media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:./media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:./media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:./media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:./media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:./media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:./media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:./media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:./media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:./media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:./media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:./media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:./media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:./media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:./media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:./media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:./media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:./media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:./media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:./media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:./media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:./media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:./media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd 
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f 

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam 
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../storage/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../storage/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../storage/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../storage/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../storage/storage-premium-storage.md
[storage-redundancy]:../../storage/storage-redundancy.md
[storage-scalability-targets]:../../storage/storage-scalability-targets.md
[storage-use-azcopy]:../../storage/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:../../resource-manager-deployment-model.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-linux-configure-lvm]:../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../linux/update-agent.md
[virtual-machines-manage-availability]:../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:classic/ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:classic/ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:upload-image.md
[virtual-machines-windows-tutorial]:../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../xplat-cli-azure-resource-manager.md

Ten przewodnik jest częścią dokumentacji na wdrażanie i wdrażanie oprogramowania SAP w systemie Microsoft Azure. Przed przeczytaniem tego przewodnika, przeczytaj [implementacji przewodnik planowania i][planning-guide]. W tym dokumencie opisano wdrażanie różnych systemów zarządzania relacyjnej bazy danych (RDBMS) oraz pokrewnych produktów w połączeniu z SAP w Microsoft Azure maszynach wirtualnych (VM) jako możliwości usługi (IaaS) przy użyciu infrastruktury usługi Azure.

Uzupełnia papieru SAP instalacji dokumentacji i uwagi SAP, reprezentujące głównej zasobów dla instalacji i wdrożenia oprogramowania SAP na podany platformy

## <a name="general-considerations"></a>Zagadnienia ogólne
W tym rozdziale zagadnienia dotyczące uruchamiania SAP powiązanych wprowadzono systemów DBMS w maszynach wirtualnych platformy Azure. Istnieje kilka odwołań do konkretnych systemów DBMS w tym rozdziale. Zamiast tego w po tym rozdziale konkretnych systemów DBMS są obsługiwane w tym dokumencie.

### <a name="definitions-upfront"></a>Definicje z wyprzedzeniem
W całym dokumencie użyjemy następujące warunki:

* IaaS: Infrastruktura jako usługa.
* PaaS: Platforma jako usługa.
* SaaS: Oprogramowanie jako usługa.
* Składnik programu SAP: poszczególnych SAP aplikację taką jak ECC, BW, Menedżer rozwiązania lub EP.  Składniki programu SAP może bazować na tradycyjnych technologii ABAP lub Java lub aplikacji z systemem innym niż NetWeaver na podstawie takich jak obiektów biznesowych.
* Środowisko SAP: jeden lub więcej składników programu SAP logicznie pogrupowane funkcji biznesowych, takich jak projektowanie, QAS, szkolenia, odzyskiwania po awarii lub produkcji.
* Poziomo SAP: Odnosi się do całego zasoby SAP w klienta IT w orientacji poziomej. Poziomo SAP obejmuje wszystkie produkcyjnych i środowiskach nieprodukcyjnych.
* Systemu SAP: Kombinacja systemu DBMS i warstwy aplikacji, np. SAP ERP programistycznej system testowy programu SAP BW, SAP CRM produkcji systemu, itp. W przypadku wdrożeń Azure nie jest obsługiwane dzielenia te dwie warstwy między lokalną i platformą Azure. To oznacza, że systemu SAP jest wdrożona lokalnie lub jest wdrożony na platformie Azure. Jednak można wdrożyć różnych systemów pozioma SAP w Azure lub lokalnie. Na przykład możesz wdrożyć programowanie SAP CRM i systemy testowe w Azure, ale SAP CRM produkcji systemu lokalnego.
* Wdrożenie tylko w chmurze: wdrożenia, w którym subskrypcji platformy Azure nie jest połączony za pośrednictwem lokacja lokacja lub połączenia ExpressRoute do infrastruktury sieci lokalnej. Wspólne dokumentacji platformy Azure rodzaju wdrożeń opisano również jako "Tylko do chmury" wdrożeń. Maszyny wirtualne wdrażane z tej metody są dostępne za pośrednictwem Internetu i publiczny Internet punkty końcowe przypisane do maszyn wirtualnych na platformie Azure. Lokalnej usługi Active Directory (AD) i DNS nie zostanie rozszerzony na platformie Azure w tych typach wdrożeń. Dlatego maszyn wirtualnych nie są częścią lokalnej usługi Active Directory. Uwaga: Tylko w chmurze wdrożeń, w tym dokumencie są definiowane jako zakończenie krajobrazów SAP, które jest uruchamiane wyłącznie na platformie Azure, bez rozszerzenia usługi Active Directory lub rozpoznawania nazw lokalnych do chmury publicznej. Konfiguracje tylko w chmurze nie są obsługiwane dla systemów produkcyjnych SAP lub konfiguracje, których SAP STMS lub innymi zasobami lokalnymi trzeba używać między systemami SAP hostowane na platformie Azure i zasobów znajdującej się na lokalnym.
* Między lokalizacjami: Opisano scenariusz wdrożonym maszyn wirtualnych z subskrypcją platformy Azure, lokacja lokacja, obejmujący wiele lokacji lub połączenia ExpressRoute między datacenter(s) lokalną i platformą Azure. Dokumentacja wspólnych Azure rodzaju wdrożenia również są opisane jako scenariusze między lokalizacjami. Przyczyna połączenia jest rozszerzenie domenami lokalnymi, lokalnej usługi Active Directory i lokalnymi DNS na platformie Azure. Pozioma lokalnej jest rozszerzony do platformy Azure zasobów subskrypcji. Występuje to rozszerzenie, maszyn wirtualnych może być częścią domeny lokalnej. Użytkownicy domeny w domenie lokalnej mogą uzyskiwać dostęp do serwerów i usługi można uruchamiać na tych maszynach wirtualnych (takie jak usługi systemu DBMS). Komunikację i rozpoznawania nazw między maszynami wirtualnymi wdrożone lokalnie i maszyn wirtualnych wdrożonych na platformie Azure jest możliwe. Oczekuje się najbardziej typowy scenariusz wdrażania SAP zasobów na platformie Azure. Zobacz [to] [ vpn-gateway-cross-premises-options] artykułu i [to] [ vpn-gateway-site-to-site-create] Aby uzyskać więcej informacji.

> [!NOTE]
> Między różnymi lokalizacjami wdrożeń systemów SAP, gdzie systemami SAP maszynach wirtualnych platformy Azure są członkami domeny lokalnej są obsługiwane dla systemów produkcyjnych SAP. Konfiguracje między lokalizacjami są obsługiwane w przypadku wdrażania części lub zakończyć krajobrazów SAP do platformy Azure. Nawet działające na platformie Azure pełną pozioma SAP wymaga o te maszyny wirtualne są częścią domeny lokalnej i REKLAM. W poprzednich wersjach dokumentacji zajmowaliśmy scenariuszy hybrydowych IT, których termin "Hybrydowe" jest ścieżką do katalogu głównego z faktu, że istnieje łączność między lokalizacjami, między lokalną i platformą Azure. W takim przypadku "Hybrydowe" oznacza również, czy maszyny wirtualne na platformie Azure są częścią lokalnej usługi Active Directory.
>
>

Niektóre dokumentacji firmy Microsoft opisano scenariusze między lokalizacjami nieco inaczej, szczególnie w przypadku konfiguracji HA systemu DBMS. W przypadku SAP powiązanych dokumentów, w scenariuszu obejmującym różne pomieszczenia tylko wrzenia w dół o łączności (ExpressRoute) do lokacji lub prywatnych oraz na fakt, że pozioma SAP jest rozdzielona między lokalną i platformą Azure.

### <a name="resources"></a>Zasoby
Temat wdrożenia SAP na platformie Azure dostępne są następujące przewodniki:

* [SAP NetWeaver na maszynach wirtualnych Azure (maszyny wirtualne) — planowanie i przewodnik wdrażania][planning-guide]
* [SAP NetWeaver na maszynach wirtualnych Azure (maszyny wirtualne) — przewodnik wdrażania][deployment-guide]
* [SAP NetWeaver na maszynach wirtualnych platformy Azure (maszyny wirtualne) — DBMS Deployment Guide (w tym dokumencie)][dbms-guide]
* [SAP NetWeaver na maszynach wirtualnych Azure (maszyny wirtualne) — przewodnik wdrażania wysokiej dostępności][ha-guide]

Poniższe uwagi SAP są związane z tym tematem SAP na platformie Azure:

| Numer | Tytuł |
| --- | --- |
| [1928533] |Aplikacje SAP na platformie Azure: typy obsługiwanych produktów i maszyny Wirtualnej Azure |
| [2015553] |SAP na platformie Microsoft Azure: obsługuje wymagania wstępne |
| [1999351] |Rozwiązywanie problemów z rozszerzonego monitorowania Azure dla programu SAP |
| [2178632] |Klucz monitorowania metryki dla SAP na platformie Microsoft Azure |
| [1409604] |Wirtualizacji w systemie Windows: rozszerzonego monitorowania |
| [2191498] |SAP w systemie Linux przy użyciu platformy Azure: rozszerzonego monitorowania |
| [2039619] |Aplikacje SAP w systemie Microsoft Azure przy użyciu bazy danych Oracle: obsługiwane produktów i wersji |
| [2233094] |DB6: Aplikacje SAP na platformie Azure przy użyciu programu IBM DB2 dla systemu Linux, UNIX i systemu Windows — informacje dodatkowe |
| [2243692] |Linux w systemie Microsoft Azure (IaaS) maszyny Wirtualnej: problemów licencji SAP |
| [1984787] |Systemu SUSE LINUX Enterprise Server 12: Informacje o instalacji |
| [2002167] |Red Hat Enterprise Linux 7.x: instalacji i uaktualniania |

Należy również zapoznać [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) zawierający wszystkie notatki SAP dla systemu Linux.

Należy mieć praktyczną wiedzę o architekturze Microsoft Azure oraz jak wdrożyć i obsługiwane maszyny wirtualne Microsoft Azure. W tym miejscu więcej informacji można znaleźć <https://azure.microsoft.com/documentation/>

> [!NOTE]
> Możemy **nie** dyskutować platformy Microsoft Azure jako usługa (PaaS) ofert platformy Microsoft Azure. Ten dokument jest o uruchamianiu systemu zarządzania bazami (danych DBMS) w Microsoft Azure maszyn wirtualnych (IaaS) tak samo, jak systemu DBMS może działać w środowisku lokalnym. Funkcje bazy danych i funkcji między te dwie oferty bardzo różnią się i nie może być mieszane ze sobą. Zobacz też: <https://azure.microsoft.com/services/sql-database/>
>
>

Ponieważ firma Microsoft dyskusji IaaS, ogólnie instalacji systemu Windows, Linux i bazami danych i konfiguracji są zasadniczo takie same jak dowolnej maszyny wirtualnej lub systemu od zera kompletnego stanu maszyny będą instalowane lokalnie. Istnieją jednak niektóre architekturę i system zarządzania implementacji decyzji, które będzie różna w przypadku używania IaaS. Ten dokument ma na celu wyjaśnienia dotyczące architektury i systemu zarządzania różnice, które muszą być przygotowane, dla przy użyciu IaaS.

Ogólnie rzecz biorąc ogólną obszarów różnicą, że zostaną omówione w tym dokumencie są:

* Planowanie prawidłowego układu maszyny Wirtualnej/VHD systemów SAP, aby upewnić się, że masz odpowiednie dane pliku układu i można osiągnąć za mało IOPS dla obciążenia.
* Zagadnienia dotyczące sieci przy użyciu IaaS.
* Funkcje określonej bazy danych do użycia w celu zoptymalizowania układu bazy danych.
* Zagadnienia i przywracania kopii zapasowej w IaaS.
* Przy użyciu różnych typów obrazów na potrzeby wdrożenia.
* Wysoka dostępność IaaS platformy Azure.

## <a name="65fa79d6-a85f-47ee-890b-22e794f51a64"></a>Struktura RDBMS wdrożenia
W kolejności należy wykonać w tym rozdziale, konieczne jest zrozumieć, co przedstawiono w [to] [ deployment-guide-3] rozdziału [Deployment Guide][deployment-guide]. Wiedzy o innej serii maszyn wirtualnych i ich różnic oraz różnice Azure standardowe i Magazyn w warstwie Premium powinien rozumieć i znane przed przeczytaniem tego rozdziału.

Do marca 2015 r. maksymalnie 127 GB rozmiar zostały Azure wirtualne dyski twarde, które zawierają system operacyjny. To ograniczenie otrzymano zniesienia w marca 2015 roku (Aby uzyskać więcej informacji Sprawdź <https://azure.microsoft.com/blog/2015/03/25/azure-vm-os-drive-limit-octupled/> ). Z tego miejsca na dyskach VHD zawierającego system operacyjny może mieć taki sam rozmiar jak inne wirtualnego dysku twardego. Niemniej jednak firma Microsoft nadal preferowane jest strukturą wdrożenia, których system operacyjny, system DBMS i ostatecznego SAP pliki binarne są niezależne od pliki bazy danych. W związku z tym oczekujemy SAP systemami w maszynach wirtualnych platformy Azure będzie mieć podstawowej maszyny Wirtualnej (lub VHD) zainstalowanych z systemem operacyjnym, bazy danych zarządzania system plików wykonywalnych i plików wykonywalnych SAP. System DBMS plików danych i dziennika będą przechowywane w usłudze Azure Storage (Standard lub Premium Storage) w oddzielnych plików VHD i dołączone jako dyski logiczne do oryginalnego obrazu systemu operacyjnego Azure maszyny Wirtualnej.

W zależności od korzystania z usługi Azure Standard lub Premium Storage (np. przy użyciu serii DS lub GS-series maszyn wirtualnych) są inne przydziały na platformie Azure, które są udokumentowane [tutaj][virtual-machines-sizes]. Podczas planowania Azure dyski VHD, należy znaleźć równowagę przydziały dla następujących elementów:

* Liczba plików danych.
* Liczba wirtualnych dysków twardych, które zawierają pliki.
* Przydziały IOPS jednego wirtualnego dysku twardego.
* Przepustowość danych na dysku VHD.
* Liczba dodatkowych możliwości wirtualne dyski twarde na rozmiar maszyny Wirtualnej.
* Ogólną przepustowość magazynowania zapewniają maszyny Wirtualnej.

Azure będzie wymuszać limit przydziału IOPS na dysku VHD. Te przydziały są różne dla wirtualne dyski twarde hostowane na usługi Azure Standard Storage i Magazyn w warstwie Premium. Czasy oczekiwania operacji We/Wy jest bardzo różnią się między tymi dwoma typami magazynów z magazyn w warstwie Premium dostarczania czynniki lepsze opóźnienia we/wy. Każdego innego typu maszyny Wirtualnej mają ograniczoną liczbę wirtualnych dysków twardych, które można dołączyć. Ograniczenie innego jest, że niektórych typów maszyny Wirtualnej mogą korzystać z usługi Azure Premium Storage. Oznacza to, że decyzja dla określonego typu maszyny Wirtualnej może nie tylko być regulowane przez wymagania Procesora i pamięci, ale również przez IOPS, opóźnienia i dysku wymagania przepływności, które zwykle są skalowane liczba wirtualnych dysków twardych lub typ dysków magazyn w warstwie Premium. Szczególnie w przypadku magazyn w warstwie Premium rozmiar wirtualnego dysku twardego również mogą być definiowane liczbę IOPS i przepływność, którą trzeba osiągnąć, każdy z nich.

Fakt, że liczba wirtualnych dysków twardych zainstalowanych ogólną szybkość IOPS, a rozmiar maszyny wirtualnej są wszystkie powiązane ze sobą, może spowodować konfiguracji platformy Azure systemu SAP może być inny niż jego lokalnego wdrożenia. Limity liczby operacji na jednostce LUN są zwykle konfigurowane w przypadku wdrożeń lokalnych. Z usługą Azure Storage te limity są stałe, lub tak jak magazyn w warstwie Premium w zależności od typu dysku. Dlatego z wdrożeń lokalnych widzimy konfiguracji klienta, serwerów baz danych, które korzystają z wielu różnych woluminach dla specjalnych plików wykonywalnych, takie jak SAP i DBMS lub woluminów specjalnych tymczasowej bazy danych lub tabel. Po przeniesieniu systemu lokalnego do platformy Azure może prowadzić do niepotrzebnego potencjalne IOPS przepustowości przez marnować dla plików wykonywalnych lub baz danych, których nie należy wykonywać dowolne albo nie partii iops wirtualnego dysku twardego. W związku z tym na maszynach wirtualnych Azure zaleca się pliki wykonywalne systemu DBMS i SAP zainstalowania na dysk systemu operacyjnego, jeśli to możliwe.

Umieszczanie plików bazy danych i plików dziennika i typ magazynu Azure używana, powinien być zdefiniowany przez wymagania dotyczące przepływności, opóźnienia i IOPS. Aby przypisać wystarczającej liczby IOPS dla dziennika transakcji, może wymusić Aby korzystać z wielu dysków VHD dla pliku dziennika transakcji lub użyj większy dysk magazyn w warstwie Premium. W takim wypadku jednego czy po prostu kompilacji oprogramowania RAID (np. Windows puli magazynu dla Windows lub MDADM i LVM (Menedżer woluminów logicznych) dla systemu Linux) z wirtualne dyski twarde zawierające dziennika transakcji.

- - -
> ![Windows][Logo_Windows] Windows
>
> Dysku D:\ w maszynie Wirtualnej platformy Azure jest nieutrwaloną dysku, który nie jest obsługiwana przez niektóre dyski lokalne w węźle obliczeń platformy Azure. Ponieważ jest nieutrwaloną, oznacza to, że wszelkie zmiany wprowadzone do zawartości na dysku D:\ ma utracone po ponownym uruchomieniu maszyny Wirtualnej. "Wszystkie zmiany" Firma Microsoft oznacza zapisane pliki, katalogi utworzone, zainstalowane aplikacje itd.
>
> ![Linux][Logo_Linux] Linux
>
> Maszyny wirtualne systemu Linux platformy Azure automatycznie zainstalować dysk w /mnt/resource, który jest dyskiem-utrwalony obsługiwana przez dyski lokalne w węźle obliczeń platformy Azure. Nietrwałe, dlatego oznacza to, że wszelkie zmiany wprowadzone do zawartości w /mnt/resource jest tracona po ponownym uruchomieniu maszyny Wirtualnej. Wszelkie zmiany firma Microsoft oznacza zapisywane pliki, katalogi utworzone, zainstalowane aplikacje itd.
>
>

- - -
Zależne od Azure serii maszyn wirtualnych, dyski lokalne w węźle obliczeń Pokaż różne działania, które mogą zostać podzielone, takich jak:

* A0 A7: Bardzo ograniczony wydajności. Nie można używać do wszelkich innych niż plik stronicowania systemu windows
* A8 A11: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > przepustowości 1GB/s
* D-Series: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > przepustowości 1GB/s
* Seria DS: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > przepustowości 1GB/s
* Seria G: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > przepustowości 1GB/s
* GS-Series: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > przepustowości 1GB/s

Instrukcje powyżej jest stosowane do typów maszyny Wirtualnej, które są certyfikowane z SAP. Seria maszyn wirtualnych z doskonałym IOPS i przepływności kwalifikować się do korzystanie przez niektóre funkcje systemu DBMS, takie jak bazy danych tempdb lub miejsce tabeli tymczasowej.

### <a name="c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f"></a>Buforowanie maszyny wirtualne i wirtualne dyski twarde
Tworząc tych dysków/dysków VHD za pośrednictwem portalu lub możemy zainstalować przekazane wirtualne dyski twarde do maszyn wirtualnych, możemy można wybrać, czy ruch we-wy między maszyny Wirtualnej, a te wirtualne dyski twarde znajduje się w magazynie Azure są buforowane. Azure Standard i Premium Storage należy użyć dwóch różnych technologii dla tego typu pamięci podręcznej. W obu przypadkach samej pamięci podręcznej dysku kopie na tym samym dysków używanych przez dysku tymczasowym (D:\ w systemie Windows) lub /mnt/resource w systemie Linux maszyny wirtualnej.

Dla usługi Azure Standard Storage pamięci podręcznej możliwe typy to:

* Bez buforowania
* Buforowania zapisu
* Odczyt i zapis buforowanie

Aby uzyskać spójny i deterministyczna wydajności, należy ustawić buforowanie na usługi Azure Standard Storage dla wszystkich dysków VHD zawierającego **DBMS powiązanych plików danych, plików dziennika i obszaru tabel do "NONE"**. Buforowanie maszyny Wirtualnej może pozostać przy użyciu domyślnego.

Dla usługi Azure Premium Storage istnieją następujące opcje buforowania:

* Bez buforowania
* Buforowania zapisu

Dla usługi Azure Premium Storage zaleca się wykorzystać **buforowanie plików danych do odczytu** bazy danych SAP i wybrać **bez buforowania VHD(s) plików dziennika**.

### <a name="c8e566f9-21b7-4457-9f7f-126036971a91"></a>Oprogramowaniem RAID
Jak już wspomniano, konieczne będzie saldo liczbę IOPS wymagany dla plików bazy danych dla liczby dysków VHD, można skonfigurować, a następnie wpisz maksymalną wartość IOPS dla każdego dysku wirtualnego dysku twardego lub magazyn w warstwie Premium zapewnia maszynie Wirtualnej platformy Azure. Najprostszym sposobem postępowania w przypadku obciążenia IOPS za pośrednictwem wirtualnych dysków twardych jest kompilacja oprogramowania RAID w różnych dysków VHD. Następnie umieszczenie liczby plików danych w systemie SAP DBMS na jednostkach LUN, używać poza oprogramowaniem RAID. Zależne od wymagania, warto rozważyć użycie magazyn w warstwie Premium, jak również od dwie z trzech różnych dyski magazyn w warstwie Premium zapewniają wyższy przydziału IOPS niż dyski VHD w oparciu magazynu w warstwie standardowa. Oprócz znaczne opóźnienia we/wy lepsze udostępniane przez usługi Azure Premium Storage.

Dziennik transakcji w różnych systemach DBMS samo dotyczy. Z dużą ilością je tylko dodanie większej liczby plików Tlog pomaga od systemów DBMS zapis do jednego z plików tylko w czasie. Razie IOPS większe niż jeden Standard magazynu oparte na zapewnia wirtualnego dysku twardego, można paskowych za pośrednictwem wielu dysków VHD standardowe magazynu lub można użyć typu większy dysk magazyn w warstwie Premium, oferującym poza większe IOPS również czynniki mniejsze opóźnienia dla zapisu operacji We/Wy w dzienniku transakcji.

Sytuacje wystąpił we wdrożeniach systemu Azure, które favor, przy użyciu oprogramowania są RAID:

* Dziennik transakcji dziennika/ponów wymagają IOPS więcej niż platforma Azure oferuje dla pojedynczego dysku VHD. Jak napisano powyżej, to będzie możliwe tworzenie jednostki LUN za pośrednictwem wielu dysków VHD za pomocą oprogramowania RAID.
* Nierówna we/wy rozkład obciążenia za pośrednictwem plików danych bazy danych SAP. W takich przypadkach jedną występować jeden plik danych zamiast często naciśnięcie limit przydziału. Podczas gdy inne pliki danych nie otrzymują nawet możliwości wykorzystania przydziału IOPS jednego wirtualnego dysku twardego. W takich przypadkach najlepszym rozwiązaniem jest kompilacja jednej jednostki LUN w wielu dysków VHD za pomocą oprogramowania RAID.
* Nie można ustalić dokładną obciążenia We/Wy na plik danych, a czego tylko około zna ogólną obciążenia IOPS względem systemu DBMS. Najłatwiej wykonać jest kompilacji dla jednej jednostki LUN za pomocą oprogramowania RAID. Suma kwot wielu dysków VHD za tej jednostki LUN następnie należy spełnić znane szybkość IOPS.

- - -
> ![Windows][Logo_Windows] Windows
>
> Zalecane jest użycie systemu Windows Server 2012 lub nowszej miejsca do magazynowania, ponieważ jest bardziej efektywne niż rozkładanie systemu Windows starszych wersji systemu Windows. Należy pamiętać, że może być konieczne tworzenie Windows pul magazynów i miejsc do magazynowania za pomocą poleceń programu PowerShell, korzystając z systemu Windows Server 2012 jako systemu operacyjnego. Polecenia programu PowerShell można znaleźć tutaj <https://technet.microsoft.com/library/jj851254.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> Do tworzenia oprogramowania RAID w systemie Linux są obsługiwane tylko MDADM i LVM (Menedżer woluminów logicznych). Aby uzyskać więcej informacji przeczytaj następujące artykuły:
>
> * [Należy skonfigurować oprogramowanie RAID w systemie Linux] [ virtual-machines-linux-configure-raid] (dla MDADM)
> * [Skonfiguruj LVM na Maszynę wirtualną systemu Linux na platformie Azure][virtual-machines-linux-configure-lvm]
>
>

- - -
Uwagi dotyczące korzystania z serii maszyn wirtualnych, które są w stanie do pracy z usługą Azure Premium Storage zazwyczaj są:

* Wymagania dla opóźnienia we/wy, znajdujących się w pobliżu urządzenia SAN/NAS dostarczania.
* Żądanie dla czynniki lepsze opóźnienia we/wy niż zapewnia usługi Azure Standard Storage.
* Wyższa wartość IOPS dla maszyny Wirtualnej niż to, co może zostać osiągnięty przy wielu standardowe magazynu wirtualnych dysków twardych dla określonego typu maszyny Wirtualnej.

Ponieważ źródłowy magazyn Azure replikuje każdy z nich do co najmniej trzech węzłów magazynu, prosty RAID 0 rozkładanie mogą być używane. Nie istnieje potrzeba do zaimplementowania RAID5 lub RAID1.

### <a name="10b041ef-c177-498a-93ed-44b3441ab152"></a>Magazyn Microsoft Azure
Microsoft Azure Storage będzie przechowywać podstawowej maszyny Wirtualnej (z systemem operacyjnym) i wirtualnych dysków twardych lub obiekty BLOB do co najmniej 3 węzłów oddzielne magazynu. Podczas tworzenia konta magazynu, istnieje możliwość wyboru ochrony w sposób pokazany poniżej:

![Replikacja geograficzna włączone dla konta magazynu Azure][dbms-guide-figure-100]

Replikacja usługi Azure Storage lokalnego (magazyn lokalnie nadmiarowy) zapewnia poziom ochrony przed utratą danych z powodu błędu infrastruktury, który kilku klientów może pozwolić sobie do wdrożenia. Jak pokazano powyżej, że istnieją różne opcje 4 piąty jest odmianą jednego z trzech pierwszy. Wyszukiwanie bliżej ich firma Microsoft może odróżnić:

* **Premium lokalnie nadmiarowego magazynu (LRS)**: Usługa Azure Premium Storage oferuje obsługę wysokiej wydajności i małych opóźnieniach dysku dla maszyn wirtualnych uruchomionych/O wykonujących obciążeń. Istnieją 3 repliki danych w ramach tego samego centrum danych Azure regionu platformy Azure. Kopie będą znajdować się w różnych usterek i domen uaktualnienia (pojęć można znaleźć [to] [ planning-guide-3.2] rozdziału w [Planning Guide][planning-guide]). W przypadku repliki danych wychodzących z usługi z powodu awarii węzła magazynu lub awarii dysku nowej repliki jest generowany automatycznie.
* **Lokalnie nadmiarowego magazynu (LRS)**: W tym przypadku istnieją 3 repliki danych w ramach tego samego centrum danych Azure regionu platformy Azure. Kopie będą znajdować się w różnych usterek i domen uaktualnienia (pojęć można znaleźć [to] [ planning-guide-3.2] rozdziału w [Planning Guide][planning-guide]). W przypadku repliki danych wychodzących z usługi z powodu awarii węzła magazynu lub awarii dysku nowej repliki jest generowany automatycznie.
* **Z magazynu geograficznie nadmiarowego magazynu (GRS)**: W tym przypadku jest asynchroniczne replikacji, który będzie dostarczyć dodatkowe 3 repliki danych w innym regionie Azure, który znajduje się w większości przypadków w tym samym regionie geograficznym (takich jak i Europa Północna, Europa). To spowoduje 3 dodatkowych replik, pozwoli to 6 replik w sumie. Odmiana to jest dodanie gdzie danych w regionie Azure zreplikowanych geograficznie może służyć do celów odczytu (dostęp do odczytu z magazynu geograficznie nadmiarowego).
* **Magazyn geograficznie nadmiarowy (ZRS) strefy**: W tym przypadku 3 replik danych pozostają w tym samym regionie Azure. Zgodnie z objaśnieniem w [to] [ planning-guide-3.1] rozdziału [Planning Guide] [ planning-guide] region platformy Azure może być liczbą centrów danych w pobliżu. W przypadku LRS repliki może być rozłożone w różnych centrach danych, że jeden region platformy Azure.

Więcej informacji można znaleźć [tutaj][storage-redundancy].

> [!NOTE]
> W przypadku wdrożeń systemu DBMS nie zaleca się użycie magazynu geograficznie nadmiarowego magazynu
>
> Azure magazynu — replikacja geograficzna jest asynchroniczne. Replikacja poszczególnych wirtualnych dysków twardych, które są zainstalowane do jednej maszyny Wirtualnej nie są zsynchronizowane w kroku blokady. W związku z tym nie jest odpowiedni replikację plików bazami danych, które są dystrybuowane za pośrednictwem różnych dysków VHD lub wdrożyć przed oprogramowaniem RAID oparte na wielu dysków VHD. Oprogramowanie systemu DBMS wymaga, że magazyn dyskowy trwałe dokładnie synchronizację różnych jednostek LUN i podstawowych dysków/wirtualne dyski twarde/jednostkami. Oprogramowanie system DBMS korzysta z różnych mechanizmów działania zapisu We/Wy sekwencji i DBMS zgłasza, że magazyn dyskowy celem replikacji jest uszkodzony, jeśli różnią się one nawet przez kilka milisekund. Dlatego jeśli jeden naprawdę oczekuje, że baza danych konfiguracji z bazą danych rozciągnięty w wielu dysków VHD replikacją geograficzną, takie replikacji musi odbywać się przy użyciu środków bazy danych i funkcji. Jeden nie polegać na platformie Azure magazynu — replikacja geograficzna do wykonania tego zadania.
>
> Problem jest najprostszym sposobem opisano przykład systemu. Załóżmy, że masz systemu SAP przekazany do platformy Azure, którego 8 wirtualne dyski twarde zawierające dane pliki systemu DBMS plus jeden wirtualny dysk twardy z plikiem dziennika transakcji. Każdej z nich te 9 wirtualne dyski twarde mają dane zapisane w spójny sposób zgodnie z bazami danych, czy dane są zapisywane w plikach dziennika danych lub transakcji.
>
> W celu prawidłowo replikacja geograficzna danych i obsługa obraz spójnej bazy danych zawartości wszystkich dziewięć dysków VHD musi być replikacją geograficzną dokładnie w takiej kolejności operacji We/Wy zostały wykonane na dziewięć różnych dysków VHD. Replikacja geograficzna usługi Azure Storage, nie zezwala na zadeklarować zależności między wirtualne dyski twarde. Oznacza to, że replikacja geograficzna usługi Magazyn Microsoft Azure nie może ustalić o tym, że zawartość tych dziewięć różne dyski VHD są ze sobą powiązane i zmiany danych są zgodne tylko wtedy, gdy replikacja w kolejności operacji We/Wy wystąpił we wszystkich wirtualne dyski twarde 9.
>
> Oprócz ryzyko jest wysoka, że obrazy replikacją geograficzną, w tym scenariuszu nie zapewniają obrazu spójności bazy danych również jest zmniejszenie wydajności pokazywany z geograficznie nadmiarowego magazynu, która może znacznie wpłynąć na wydajność. W podsumowaniu nie należy używać tego typu nadmiarowość magazynu dla obciążeń typu systemu DBMS.
>
>

#### <a name="mapping-vhds-into-azure-virtual-machine-service-storage-accounts"></a>Mapowanie wirtualne dyski twarde do kont magazynu usługi Azure maszyny wirtualnej
Konto magazynu platformy Azure jest nie tylko konstrukcję administracyjne, ale również temat ograniczenia. Podczas gdy ograniczenia różnią się od tego, czy omawianiu standardowe konto magazynu platformy Azure lub konta usługi Azure Premium Storage. Podano dokładne możliwości i ograniczeń [tutaj][storage-scalability-targets]

Dlatego dla usługi Azure Standard Storage należy zwrócić uwagę na IOPS na konto magazynu jest ograniczona do (wiersz zawierający "Całkowita liczba żądań" w [artykuł][storage-scalability-targets]). Ponadto jest początkowej limit 100 kont magazynu dla subskrypcji platformy Azure (lub nowszym lipca 2015). Dlatego zaleca się saldo IOPS maszyn wirtualnych między wiele kont magazynu przy użyciu usługi Azure Standard Storage. Podczas gdy jeden maszyna wirtualna używa najlepiej jedno konto magazynu, jeśli to możliwe. Dlatego jeśli omawianiu DBMS wdrożeń, gdzie każdego wirtualnego dysku twardego, który znajduje się na usługi Azure Standard Storage można osiągnąć limitu przydziału należy wdrażać tylko 30-40 wirtualne dyski twarde na konto magazynu Azure, która używa usługi Azure Standard Storage. Z drugiej strony Jeśli korzystać z usługi Azure Premium Storage i mają być przechowywane bazy danych dużych woluminów, może być poprawnie pod względem IOPS. Jednak konto magazynu Azure Premium jest sposób bardziej restrykcyjne w woluminie danych niż standardowe konta magazynu platformy Azure. W związku z tym można wdrażać tylko w ograniczonej liczby wirtualnych dysków twardych w ramach konta usługi Azure Premium Storage przed szukaniem limit woluminów danych. W Pomyśl zakończenia jako "Wirtualną sieć SAN", który ma ograniczone możliwości w IOPS i/lub pojemności konta magazynu Azure. W związku z tym zadanie pozostanie, tak jak wdrożeń lokalnych do definiowania układu dysków VHD różnych systemów SAP za pomocą różnych "urojony SAN urządzenia" lub konta magazynu Azure.

Dla usługi Azure Standard Storage nie zaleca się zaprezentowanie magazynu z różnych kont magazynu dla jednej maszyny Wirtualnej, jeśli to możliwe.

Natomiast przy użyciu DS lub GS-serii maszyn wirtualnych platformy Azure istnieje możliwość instalacji wirtualne dyski twarde poza standardowe konta magazynu Azure i kont magazynu w warstwie Premium. Przypadki użycia, takie jak zapisywanie kopii zapasowych do magazynu w warstwie standardowa kopie wirtualne dyski twarde, natomiast o DBMS danych i pliki dziennika na magazyn w warstwie Premium wyniknąć którym takie magazyn heterogeniczny można skorzystać.

Na podstawie wdrożeń klienta i testowania około 30-40 wirtualne dyski twarde zawierające pliki danych bazy danych i pliki dziennika można udostępnić w jednej Azure standardowe konto magazynu z akceptowalną wydajność. Jak wspomniano wcześniej, ograniczenie konto magazynu Azure Premium będzie prawdopodobnie możliwości danych, które może przechowywać go i nie IOPS.

Jako z sieci SAN urządzeniami lokalnymi, udostępnianie wymaga pewne aspekty monitorowania w celu wykrycia ostatecznie wąskie gardła na konto magazynu platformy Azure. Rozszerzenie monitorowania Azure SAP i portalu Azure są narzędzia, które mogą służyć do wykrywania zajęty kontach magazynu Azure, która może być dostarczanie nieoptymalne wydajność We/Wy.  Jeśli ta sytuacja jest wykrył, że zalecane jest aby przenieść zajęty maszyn wirtualnych do innego konta magazynu Azure. Zapoznaj się z [Deployment Guide] [ deployment-guide] dla szczegółowe informacje na temat aktywowania SAP hosta możliwości monitorowania.

Inny artykuł podsumowania najlepsze rozwiązania dotyczące usługi Azure Standard Storage i standardowe konta magazynu Azure można znaleźć tutaj <https://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx>

#### <a name="moving-deployed-dbms-vms-from-azure-standard-storage-to-azure-premium-storage"></a>Przenoszenie wdrożonych maszyn wirtualnych systemu DBMS z usługi Azure Standard Storage do magazynu Azure w warstwie Premium
Firma Microsoft wystąpi jakiś scenariuszy, w którym jako klienta chcesz przenieść wdrożonej maszyny Wirtualnej z usługi Azure Standard Storage w usłudze Azure Premium Storage. Nie jest to możliwe bez fizycznie przeniesienie danych. Istnieje kilka sposobów, aby osiągnąć:

* Wszystkie wirtualne dyski twarde, podstawowy dysk VHD jak wirtualne dyski twarde danych można po prostu skopiuj do nowego konta magazynu Azure Premium. Bardzo często wybranej liczba wirtualnych dysków twardych w ramach usługi Azure Standard Storage nie ze względu na fakt, że potrzebne ilość danych. Jednak potrzebne tak wielu wirtualnych dysków twardych z powodu IOPS. Teraz Przenieś do usługi Azure Premium Storage należy można przejść sposób mniej wirtualne dyski twarde do osiągnięcia niektórych przepływności IOPS. Podane fakt, że w usłudze Azure Storage standardowy opłacać używanych danych i nie rozmiar dysku nominalnego, liczba wirtualnych dysków twardych naprawdę niezależnie od tego, pod względem kosztów. Usługa Azure Premium Storage będzie płatności dla rozmiaru nominalnego dysku. W związku z tym większość klienta należy próbować zachować liczba wirtualnych dysków twardych Azure w magazynie Premium pod numerem niezbędnych do osiągnięcia przepływności IOPS niezbędne. Tak większość klientów decyzję przed sposób prosty 1:1 kopiowania.
* Jeśli nie został jeszcze zainstalowany, w przypadku zainstalowania jednego wirtualnego dysku twardego, zawierające kopii zapasowej bazy danych SAP bazy danych. Po utworzeniu kopii zapasowej Odinstaluj wszystkie dyski VHD, w tym wirtualny dysk twardy zawierający kopię zapasową i skopiuj podstawowy dysk VHD i wirtualny dysk twardy z kopią zapasową do konta usługi Azure Premium Storage. Następnie będzie wdrożenie oparte na podstawowy dysk VHD maszyny Wirtualnej i zainstalować dysk VHD z kopią zapasową. Teraz utworzyć dodatkowe pustych dysków w warstwie Premium magazynu służące do przywracania bazy danych do maszyny wirtualnej. Przy założeniu, że systemu DBMS umożliwia zmianę ścieżki do plików danych i dziennika w ramach procesu przywracania.
* Inną możliwością jest odmianą poprzedniego procesu, którym tylko kopia zapasowa dysku VHD w usłudze Azure Premium Storage i dołącz je przed Maszynami wirtualnymi, nowo wdrożone i zainstalowana.
* Możliwość czwarty należy wybrać po potrzebę się, aby zmienić liczbę plików danych bazy danych. W takim przypadku przeprowadza się przy użyciu eksportu/importu kopii jednorodnego systemu SAP. Te pliki eksportu do wirtualnego dysku twardego, który jest kopiowany do konta usługi Azure Premium Storage i dołączenie go do maszyny Wirtualnej, którego używasz do uruchamiania procesów importu PUT. Klienci używać tej możliwości głównie w przypadku, gdy chcą, aby zmniejszyć liczbę plików danych.

### <a name="deployment-of-vms-for-sap-in-azure"></a>Wdrażanie maszyn wirtualnych dla programu SAP na platformie Azure
Microsoft Azure oferuje wiele sposobów wdrażania maszyn wirtualnych i skojarzone dyski. Co jest bardzo ważne poznać różnice, od przygotowania maszyn wirtualnych może się różnić zależy od sposobu wdrożenia. Ogólnie rzecz biorąc szukamy do opisanych w poniższych rozdziałach scenariuszy.

#### <a name="deploying-a-vm-from-the-azure-marketplace"></a>Wdrażanie maszyny Wirtualnej z poziomu portalu Azure Marketplace
Chcesz przełączyć firmy Microsoft lub strona 3 podać obrazu z portalu Azure Marketplace do wdrożenia maszyny Wirtualnej. Po wdrożeniu maszyny Wirtualnej na platformie Azure, wykonaj te same wskazówki i narzędzia do zainstalowania oprogramowania SAP wewnątrz maszyny Wirtualnej, jak w środowisku lokalnym. Dotyczących instalowania oprogramowania SAP wewnątrz maszyny Wirtualnej Azure, SAP i Microsoft zaleca przekazywanie i przechowywać nośnika instalacyjnego programu SAP w Azure wirtualnych dysków twardych lub do utworzenia maszyny Wirtualnej platformy Azure działa jako "serwera plików", który zawiera wszystkie niezbędne nośnik instalacyjny programu SAP.

#### <a name="deploying-a-vm-with-a-customer-specific-generalized-image"></a>Wdrażanie maszyny Wirtualnej z uogólniony obraz określonego klienta
Z powodu szczególne wymagania dotyczące w odniesieniu do używanej wersji systemu operacyjnego lub DBMS podane obrazów w portalu Azure Marketplace może nie odpowiadają potrzebom. W związku z tym konieczne może utworzyć Maszynę wirtualną za pomocą własnych "private" obrazu systemu operacyjnego/DBMS maszyny Wirtualnej, który można wdrożyć kilka razy później. Aby przygotować obraz "private" do duplikacji, system operacyjny musi być uogólniony na lokalnej maszynie Wirtualnej. Zapoznaj się z [Deployment Guide] [ deployment-guide] szczegółowe informacje na temat sposobu generalize maszyny Wirtualnej.

Jeśli zainstalowano już SAP zawartości w lokalnej maszyny Wirtualnej (szczególnie w przypadku systemów warstwy 2), można dostosować ustawienia systemu SAP po wdrożenia maszyny Wirtualnej platformy Azure za pomocą wystąpienia nazwy procedury obsługiwana przez Menedżera inicjowania obsługi oprogramowania SAP (Uwaga SAP [1619720]). W przeciwnym razie można zainstalować oprogramowania SAP później po wdrożeniu maszyny wirtualnej Azure.

Począwszy od bazy danych zawartości używana przez aplikację SAP możesz albo wygenerować zawartość świeżo przez instalację programu SAP lub można zaimportować zawartość na platformie Azure przy użyciu wirtualnego dysku twardego z kopii zapasowej bazy danych systemu DBMS lub dzięki wykorzystaniu funkcji systemu DBMS, aby bezpośrednio kopii zapasowej do Magazyn Microsoft Azure. W takim przypadku można również przygotować dyski VHD z systemu DBMS danych i dziennika plików lokalnej, a następnie zaimportowanie tych dysków na platformie Azure. Jednak transferu danych systemu DBMS, który jest ładowany z lokalnego do platformy Azure może działać przez dysków VHD, które muszą być przygotowane na lokalnym.

#### <a name="moving-a-vm-from-on-premises-to-azure-with-a-non-generalized-disk"></a>Przenoszenie maszyny Wirtualnej z lokalnej na platformie Azure przy użyciu dysku z systemem innym niż uogólniony
Ma zostać przeniesiona do określonego systemu SAP z lokalnego do platformy Azure (przyrostu i shift). Można to zrobić, przekazując wirtualny dysk twardy zawierający system operacyjny, pliki binarne programu SAP i ostatecznego plików binarnych systemu DBMS i dyski VHD z plików danych i dziennika z bazami danych na platformie Azure. W przeciwnym Scenariusz #2 powyżej, zachowanie nazwy hosta, identyfikator SID SAP i SAP kont użytkowników w Maszynie wirtualnej Azure, jak zostały one skonfigurowane w środowisku lokalnym. W związku z tym uogólnianie obrazu nie jest konieczne. Ten przypadek przede wszystkim zostanie zastosowana dla scenariuszy między różnymi lokalizacjami, gdzie część pozioma SAP jest uruchomiona lokalnie i w częściach na platformie Azure.

## <a name="871dfc27-e509-4222-9370-ab1de77021c3"></a>Wysoka dostępność i odzyskiwanie po awarii z maszynami wirtualnymi platformy Azure
Platforma Azure oferuje następujące funkcje wysokiej dostępności i odzyskiwania awaryjnego (DR), które dotyczą różnych składników, których używamy dla wdrożenia SAP i bazami danych

### <a name="vms-deployed-on-azure-nodes"></a>Maszyn wirtualnych wdrożonych w węzłach Azure
Dla wdrożonych maszyn wirtualnych platformy Azure nie oferuje funkcje, takie jak migracja na żywo. Oznacza to, jeśli w klastrze serwerów, na którym wdrożono Maszynę wirtualną niezbędne jest konserwacji, maszyny Wirtualnej musi pobrać zatrzymana i uruchomiona ponownie. Na platformie Azure jest wykonywana konserwacja przy użyciu tak zwane domen uaktualnienia w ramach klastrów serwerów. Obsługiwane jest tylko jedną domenę uaktualnienia naraz. Podczas ponownego uruchamiania będzie przerwy w świadczeniu usług maszyna wirtualna jest zamknięta, gdy jest wykonywana Konserwacja i ponownego uruchomienia maszyny Wirtualnej. Większość dostawców DBMS jednak zapewnić wysoką dostępność i odzyskiwanie po awarii funkcje, których szybko uruchomi usług systemu DBMS w innym węźle, jeśli węzeł podstawowy jest niedostępny. Platforma Azure oferuje funkcje do dystrybucji maszyn wirtualnych, magazynu i innymi usługami Azure w domenach uaktualnienia, aby upewnić się, że zaplanowanej konserwacji lub infrastruktury błędów czy tylko wpływ małego podzbioru maszyn wirtualnych lub usług.  Staranne planowanie jest możliwe uzyskanie poziomy dostępności porównywalne z infrastruktury lokalnej.

Logiczne grupowanie maszyn wirtualnych są zestawami dostępności usługi Microsoft Azure lub usługi, które zapewnia maszyn wirtualnych i inne usługi są dystrybuowane do różnych usterek i domen uaktualnienia w ramach klastra taki sposób, że może istnieć tylko jeden zamknięcia węzła w każdym punkcie w czasie (odczyt [to] [ virtual-machines-manage-availability] artykułu, aby uzyskać więcej informacji).

Musi zostać skonfigurowana w celu wdrażania maszyn wirtualnych, jak pokazano poniżej:

![Definicja zestawu dostępności dla systemu DBMS HA konfiguracji][dbms-guide-figure-200]

Jeśli chcemy, aby utworzyć wysokiej dostępności konfiguracje wdrożeń systemu DBMS (niezależnie od poszczególnych DBMS HA funkcji używanych), maszynach wirtualnych systemu DBMS należy:

* Dodawanie maszyn wirtualnych do tej samej sieci wirtualnej platformy Azure (<https://azure.microsoft.com/documentation/services/virtual-network/>)
* Maszyny wirtualne w konfiguracji wysokiej dostępności należy się również w tej samej podsieci. Rozpoznawanie nazw między różne podsieci nie jest możliwe w przypadku wdrożeń tylko w chmurze, będzie działać tylko rozpoznawania adresu IP. Przy użyciu lokacja lokacja lub połączenia ExpressRoute, w przypadku wdrożeń między różnymi lokalizacjami, sieci z co najmniej jedną podsieć zostanie już nawiązane. Rozpoznawanie nazw, które zostaną wykonane zgodnie z lokalną infrastrukturę AD zasad i sieci.

[comment]: <> (MSSedusch TODO testu, jeśli nadal ma wartość true w usłudze ARM)

#### <a name="ip-addresses"></a>Adresy IP
Zdecydowanie zaleca się można skonfigurować w taki sposób, elastyczne maszyn wirtualnych w konfiguracji wysokiej dostępności. Polegania na adresy IP w celu rozwiązania partnerów wysokiej dostępności w konfiguracji wysokiej dostępności nie jest niezawodne na platformie Azure, chyba że statyczne adresy IP są używane. Istnieją dwa pojęcia "Zamknij", na platformie Azure:

* Zamknij za pomocą portalu Azure lub programu Azure PowerShell polecenia cmdlet Stop-AzureRmVM: W tym przypadku maszyny wirtualnej pobiera zamykania i zwalnia przydzielone. Konto platformy Azure nie jest już będzie obciążana dla tej maszyny Wirtualnej, są tylko opłaty, które będzie powodowało użycie magazynu. Jednak jeśli nie statycznego prywatnego adresu IP interfejsu sieciowego, adres IP zostanie zwolniony i nie gwarantuje, że interfejs sieciowy pobiera stary adres IP przypisany ponownie po ponownym uruchomieniu maszyny wirtualnej. Wykonywanie zamykania w dół za pośrednictwem portalu Azure lub przez wywołanie metody Stop-AzureRmVM automatycznie spowoduje dezaktywowanie alokacji. Jeśli nie chcesz deallocat Użyj maszyny Stop AzureRmVM - StayProvisioned
* Wyłączenie maszyny Wirtualnej z poziomu systemu operacyjnego maszyny Wirtualnej pobiera zamknięta i nie zwalnia przydzielony. Jednak w takim przypadku konta platformy Azure będzie nadal obciążana dla maszyny Wirtualnej, mimo że jest zamknięcie. W takim przypadku przypisanie adresu IP do zatrzymania maszyny Wirtualnej pozostaną nienaruszone. Zamykanie maszyny Wirtualnej z wewnątrz nie automatycznie wymusi dezaktywowanie alokacji.

Nawet w przypadku scenariuszy między różnymi lokalizacjami domyślnie zamykania i dezaktywowanie alokacji oznaczają do przypisywania adresów IP z maszyny Wirtualnej, nawet jeśli zasad lokalnych w ustawieniach DHCP są różne.

* Jeśli jeden przypisuje statycznego adresu IP do karty sieciowej jako opisano wyjątek [tutaj][virtual-networks-reserved-private-ip].
* W takim przypadku adres IP nie zmienia się tak długo, jak interfejs sieciowy nie zostanie usunięta.

> [!IMPORTANT]
> Aby zachować całego wdrożenia proste i łatwą w obsłudze, wyczyść zaleca się instalacji maszyn wirtualnych partnerstwo w DBMS HA lub konfiguracji odzyskiwania po awarii w obrębie platformy Azure w sposób, który istnieje działa rozpoznawanie nazw między różnych maszyn wirtualnych związane.
>
>

## <a name="deployment-of-host-monitoring"></a>Wdrożenie hosta monitorowania
Wydajność użycia aplikacje SAP w maszynach wirtualnych platformy Azure SAP wymaga możliwości uzyskać hosta monitorowania danych z hostów fizycznych z uruchomionymi maszynach wirtualnych platformy Azure. Określony poziom poprawki SAP HostAgent będzie wymagane, umożliwia tę funkcję w SAPOSCOL i SAP HostAgent. Poziom poprawki dokładne jest udokumentowany uwagi SAP [1409604].

Aby uzyskać szczegółowe informacje dotyczące wdrażania składników dostarczających SAPOSCOL i SAPHostAgent dane hostów i zarządzanie cyklem życia tych składników, zobacz [przewodnik wdrażania][deployment-guide]

## <a name="3264829e-075e-4d25-966e-a49dad878737"></a>Szczegóły programu Microsoft SQL Server
### <a name="sql-server-iaas"></a>SQL Server IaaS
Począwszy od programu Microsoft Azure, można łatwo migracji istniejącej aplikacji SQL Server oparty na platformie systemu Windows Server na maszynach wirtualnych platformy Azure. Program SQL Server w maszynie wirtualnej pozwala zmniejszyć całkowity koszt posiadania wdrażania, zarządzania i konserwacji aplikacji szerokość przedsiębiorstwa za pomocą łatwo migracji te aplikacje do systemu Microsoft Azure. Z programem SQL Server w maszynie wirtualnej platformy Azure Administratorzy i deweloperzy mogą nadal używać tej samej opracowywania i narzędzia administracyjne, które są dostępne na lokalnym.

> [!IMPORTANT]
> Należy pamiętać, że firma Microsoft nie dyskusji Microsoft usługi Azure SQL Database, który to platforma jako ofertę usługi platformy Microsoft Azure. Omówienie w tym dokumencie jest uruchomiony produktu SQL Server, ponieważ jest ona znana wdrożeń lokalnych w maszynach wirtualnych platformy Azure, wykorzystanie infrastruktury jako możliwości usługi Azure. Funkcje bazy danych i funkcji między te dwie oferty są różne, a nie może być mieszane ze sobą. Zobacz też: <https://azure.microsoft.com/services/sql-database/>
>
>

Zdecydowanie zaleca się przegląd [to] [ virtual-machines-sql-server-infrastructure-services] dokumentacji, przed kontynuowaniem.

W poniższych sekcjach części części dokumentacji w ramach powyższego łącza zostaną zagregowane i wymienione. Szczegóły wokół SAP są wymienione także i niektóre pojęcia są opisane bardziej szczegółowo. Jednak zdecydowanie zalecane jest do pracy z dokumentacją powyżej pierwszej przed odczytaniem szczegółowej dokumentacji programu SQL Server.

Brak niektórych programu SQL Server w IaaS określone informacje, których należy wiedzieć przed kontynuowaniem:

* **Umowa SLA maszyny wirtualnej**: Brak umowy SLA dla maszyn wirtualnych działających na platformie Azure, w którym można znaleźć tutaj: <https://azure.microsoft.com/support/legal/sla/>  
* **Obsługa wersji programu SQL**: w przypadku klientów SAP, firma Microsoft obsługuje program SQL Server 2008 R2 lub nowszy na maszyny wirtualne Microsoft Azure. Starszych wersji nie są obsługiwane. Przejrzyj ogólnego [oświadczenie pomocy technicznej](https://support.microsoft.com/kb/956893) więcej szczegółów. Należy pamiętać, że ogólnie programu SQL Server 2008 jest obsługiwane przez firmę Microsoft oraz. Jednak ze względu na najważniejsze funkcje SAP, którą wprowadzono w programie SQL Server 2008 R2, SQL Server 2008 R2 jest minimalna wersja programu SAP. Należy pamiętać, że programu SQL Server 2012 i 2014 został rozszerzony za pomocą lepszą integrację scenariusz IaaS (takich jak tworzenie kopii zapasowej bezpośrednio w usłudze Azure Storage). W związku z tym stosujemy ograniczenia, w tym dokumencie do programu SQL Server 2012 i 2014 z poziomu najnowsze poprawki dla platformy Azure.
* **Obsługa funkcji SQL**: funkcje najbardziej programu SQL Server są obsługiwane w programie Microsoft Azure Virtual Machines z kilkoma wyjątkami. **SQL Server Failover Clustering przy użyciu udostępnionych dysków nie jest obsługiwane**.  Rozproszone technologii, takich jak dublowania bazy danych, zawsze włączonych grup dostępności, replikacji, aby wysyłanie dziennika i brokera usług, które są obsługiwane w pojedynczym regionie Azure. Program SQL Server AlwaysOn również są obsługiwane między różnych regionach platformy Azure zgodnie z opisem w tym miejscu: <https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.  Przegląd [oświadczenie pomocy technicznej](https://support.microsoft.com/kb/956893) więcej szczegółów. Przykład wdrażania konfiguracji funkcji AlwaysOn znajduje się w [to] [ virtual-machines-workload-template-sql-alwayson] artykułu. Sprawdź również, najlepsze rozwiązania udokumentowane [tutaj][virtual-machines-sql-server-infrastructure-services]
* **Wydajność SQL**: pracujemy pewność, że Microsoft Azure hostowanej maszyny wirtualnej będzie wykonywać bardzo dobrze w odróżnieniu od innych ofert wirtualizacji chmury publicznej, ale wyniki poszczególnych może się różnić. Zapoznaj się z [to] [ virtual-machines-sql-server-performance-best-practices] artykułu.
* **Przy użyciu obrazów z portalu Azure Marketplace**: jest to najszybszy sposób wdrażania nowej maszyny Wirtualnej Microsoft Azure można użyć obrazu z portalu Azure Marketplace. Brak obrazów w portalu Azure Marketplace, które zawierają programu SQL Server. Obrazy SQL Server już zainstalowanym nie można natychmiast SAP NetWeaver aplikacji. Przyczyną jest to domyślne ustawienie sortowania programu SQL Server jest zainstalowane w ramach tych obrazów i nie wymaganych przez systemy SAP NetWeaver sortowania. Aby można było używać tych obrazów, sprawdź, czy czynności opisanych w rozdziale [obrazów za pomocą programu SQL Server z witryny Microsoft Azure Marketplace][dbms-guide-5.6].
* Zapoznaj się z [szczegóły cennika](https://azure.microsoft.com/pricing/) Aby uzyskać więcej informacji. [Podręcznik licencjonowania programu SQL Server 2012](https://download.microsoft.com/download/7/3/C/73CAD4E0-D0B5-4BE5-AB49-D5B886A5AE00/SQL_Server_2012_Licensing_Reference_Guide.pdf) i [Podręcznik licencjonowania programu SQL Server 2014](https://download.microsoft.com/download/B/4/E/B4E604D9-9D38-4BBA-A927-56E4C872E41C/SQL_Server_2014_Licensing_Guide.pdf) są również ważnych zasobów.

### <a name="sql-server-configuration-guidelines-for-sap-related-sql-server-installations-in-azure-vms"></a>Wskazówki dotyczące konfigurowania programu SQL Server dla programu SAP związane z instalacji programu SQL Server na maszynach wirtualnych Azure
#### <a name="recommendations-on-vmvhd-structure-for-sap-related-sql-server-deployments"></a>Zalecenia dotyczące maszyny Wirtualnej/VHD struktury dla programu SAP dotyczące wdrożenia programu SQL Server
Zgodnie z ogólny opis plików wykonywalnych programu SQL Server powinny być znajduje się lub zainstalowany na dysku systemowym podstawowy dysk VHD maszyny Wirtualnej (dysk C:\).  Zazwyczaj większość systemowych baz danych programu SQL Server nie są używane na wysokim poziomie przez SAP NetWeaver obciążenie. Dlatego systemowych baz danych programu SQL Server (master, msdb i modelu) może pozostać na tym dysku C:\. Wystąpił wyjątek może być bazy danych tempdb, co w przypadku niektórych ERP SAP i wszystkich BW obciążeń, może wymagać większą ilość danych lub woluminu operacji We/Wy, który nie mieści się w oryginalnej maszyny Wirtualnej. Dla tych systemów można wykonać następujące czynności:

* Przenieś pliki danych głównej bazy danych tempdb na tym samym dysku logicznego pliki danych podstawowych bazy danych SAP.
* Dodaj wszystkie pliki danych tempdb dodatkowe do wszystkich innych dysków logicznych zawierający plik danych bazy danych SAP.
* Dodaj plik dziennika bazy danych tempdb na dysk logiczny, który zawiera plik dziennika bazy danych użytkownika.
* **Wyłącznie do typów maszyny Wirtualnej, które używają lokalnych dysków SSD** danych tempdb węzła obliczeń i dziennika plików może być umieszczone na dysku D:\. Niemniej jednak może zalecane do korzystania z wielu plików danych bazy danych tempdb. Należy pamiętać, że woluminy dysku D:\ są różne na podstawie typu maszyny Wirtualnej.

Te konfiguracje Włącz tempdb korzystać więcej miejsca niż dysk systemowy jest zapewnienie. W celu określenia rozmiaru odpowiednie bazy danych tempdb, jeden Sprawdź rozmiar bazy danych tempdb na istniejących systemów, które lokalnie. Ponadto taka konfiguracja umożliwia liczb IOPS względem bazy danych tempdb, którego nie można podać z dysku systemowego. Ponownie systemów, które są uruchamiane lokalnie może służyć do monitorowania obciążenia We/Wy względem bazy danych tempdb, dzięki czemu mogą pochodzić liczby IOPS, które powinny być widoczne w Twojej bazie danych tempdb.

Konfiguracja maszyny Wirtualnej, w którym działa program SQL Server z bazą danych SAP i rozmieszczenie danych tempdb i bazy danych tempdb pliku dziennika na dysku D:\ wyglądałyby tak jak:

![Odwołanie do konfiguracji IaaS maszyny Wirtualnej platformy Azure dla programu SAP][dbms-guide-figure-300]

Należy pamiętać, że na dysku D:\ ma różne rozmiary, zależy od typu maszyny Wirtualnej. Zależy od rozmiaru wynoszącego tempdb użytkownik może można wymusić pary plików danych i dziennika bazy danych tempdb z SAP bazy danych plików danych i dziennika w przypadku gdy dysku D:\ jest za mały.

#### <a name="formatting-the-vhds"></a>Formatowanie dysków VHD
Dla programu SQL Server NTFS rozmiaru bloku dla wirtualne dyski twarde zawierające dane programu SQL Server i pliki dziennika powinien być 64 KB. Nie istnieje potrzeba do sformatowania dysku D:\. Ten dysk jest wstępnie sformatowane.

Aby upewnić się, że przywracania lub tworzenie baz danych nie inicjuje pliki danych poprzez wyzerowanie zawartości plików, co upewnij się, że uruchomiono usługi SQL Server w kontekście użytkownika ma określone uprawnienia. Zwykle użytkowników do grupy Administratorzy systemu Windows mają te uprawnienia. W kontekście użytkownika użytkownik bez uprawnień administratora na systemu Windows jest uruchomiona usługa SQL Server, należy przypisać użytkownika prawa użytkownika "Wykonaj zadania konserwacji woluminu".  Zobacz szczegółowe informacje w tym artykule bazy wiedzy firmy Microsoft: <https://support.microsoft.com/kb/2574695>

#### <a name="impact-of-database-compression"></a>Wpływ kompresji bazy danych
W konfiguracji, gdy przepustowość operacji We/Wy mogą stać się czynnikiem ograniczającym co miar, co zmniejsza liczbę IOPS może przyczynić się do rozciągania obciążenie jednego, mogą uruchamiać w scenariuszu IaaS, takich jak Azure. W związku z tym jeśli nie została jeszcze zrobione, zastosowanie kompresji strony serwera SQL zdecydowanie zalecane jest zarówno SAP, jak i Microsoft przed przekazywania SAP istniejących baz danych na platformie Azure.

Zalecenie, aby wykonać kompresji bazy danych przed przekazaniem Azure znajduje się z dwóch powodów:

* Ilość danych do przekazania jest niższa.
* Czas realizacji kompresji jest krótszy, przy założeniu, że jeden służy silniejszych sprzętu z więcej procesorów ani większą przepustowość operacji We/Wy lub mniej we/wy opóźnienia lokalnymi.
* Mniejsze rozmiary bazy danych może prowadzić do mniejsze koszty przydział dysku

Kompresja bazy danych działa również w maszynach wirtualnych platformy Azure, jak lokalnie. Aby uzyskać więcej informacji na temat sposobu Kompresuj istniejącego serwera SQL SAP bazy danych można znaleźć tutaj: <https://blogs.msdn.com/b/saponsqlserver/archive/2010/10/08/compressing-an-sap-database-using-report-msscompress.aspx>

### <a name="sql-server-2014--storing-database-files-directly-on-azure-blog-storage"></a>Program SQL Server 2014 — przechowywanie bazy danych plików bezpośrednio na blogu magazynu Azure
SQL Server 2014 otwiera możliwość przechowywania plików bazy danych bezpośrednio w magazynie obiektów Blob Azure bez "otokę" wokół nich wirtualnego dysku twardego. Szczególnie w przypadku przy użyciu usługi Azure Standard Storage lub typów mniejszych maszyny Wirtualnej dzięki temu scenariuszy, w którym można rozwiązać, limity iops może zostać wymuszone przez ograniczona liczba wirtualnych dysków twardych, które można zainstalować do niektórych typów mniejszych maszyny Wirtualnej. Działa to w przypadku baz danych użytkowników, ale nie dla systemowych baz danych programu SQL Server. Działa także dla plików danych i dziennika programu SQL Server. Jeśli chcesz wdrożyć bazę danych programu SQL Server SAP w ten sposób zamiast "zawijania" go do wirtualnych dysków twardych, pamiętaj o następujących pamiętać:

* Konto magazynu używane musi być w tym samym regionie Azure, jako taki, który jest używany do wdrożenia maszyny Wirtualnej programu SQL Server jest uruchomiony w.
* Wymienione wcześniej w odniesieniu do rozpowszechniania wirtualne dyski twarde w różnych kontach magazynu Azure kwestie dla tej metody, a także wdrożeń. Oznacza, że liczba operacji We/Wy limitów konta magazynu Azure.

[comment]: <> (MSSedusch TODO, ale zostaną użyte przepustowość sieci i nie przepustowość magazynu nie go?)

Szczegółowe informacje o tym typie wdrożenia są wyświetlane tutaj: <https://msdn.microsoft.com/library/dn385720.aspx>

Aby przechowywać pliki danych programu SQL Server bezpośrednio w usłudze Azure Premium Storage, musisz mieć minimalnej wersji poprawki programu SQL Server 2014, który opisano w tym miejscu: <https://support.microsoft.com/kb/3063054>. Przechowywanie plików danych programu SQL Server na usługi Azure Standard Storage działa z wydanej wersji programu SQL Server 2014. Jednak tej samej poprawki zawierają innej serii poprawki, które powodują, że bardziej niezawodny bezpośredniego użycia magazynu obiektów Blob Azure do tworzenia kopii zapasowych i plików danych programu SQL Server. Dlatego zaleca się używania poprawki te na ogół.

### <a name="sql-server-2014-buffer-pool-extension"></a>Rozszerzenie puli buforów programu SQL Server 2014
SQL Server 2014 wprowadzono nową funkcję, która jest wywoływana rozszerzenia puli buforów. Ta funkcja stanowi rozszerzenie puli buforów programu SQL Server, który jest przechowywany w pamięci z drugiego poziomu pamięci podręcznej, która nie jest obsługiwana przez lokalne dyski SSD serwera lub maszyny Wirtualnej. Dzięki temu do przechowywania danych większy zestaw roboczy "w pamięci". W porównaniu do uzyskiwania dostępu do usługi Azure Standard Storage dostęp do rozszerzenia puli buforów, który jest przechowywany na lokalnych dyskach SSD maszyny wirtualnej Azure jest wiele czynników szybciej.  W związku z tym wykorzystanie dysku D:\ typy maszyn wirtualnych, które mają znakomity IOPS i przepływność może być bardzo rozsądnego sposobu zmniejszenia obciążenia IOPS w usłudze Azure Storage i znacznie skrócić czas odpowiedzi zapytań. Dotyczy to zwłaszcza w przypadku, gdy nie używa magazyn w warstwie Premium. W przypadku magazyn w warstwie Premium i użycie pamięci podręcznej odczytu Azure Premium w węźle obliczeń zgodnie z zaleceniami plików danych, nie duże różnice nie oczekiwano. Przyczyną jest to, że oba pamięci podręcznych (rozszerzenie puli buforów serwera SQL i pamięci podręcznej odczytu magazynu Premium) używają dyski lokalne węzłów obliczeniowych.
Aby uzyskać więcej informacji na temat tej funkcji, sprawdź, czy w tej dokumentacji: <https://msdn.microsoft.com/library/dn133176.aspx>

### <a name="backuprecovery-considerations-for-sql-server"></a>Uwagi dotyczące tworzenia kopii zapasowej i odzyskiwania dla programu SQL Server
W przypadku wdrażania serwera SQL na platformie Azure z kopii zapasowej metodologii musi przejrzeć. Nawet jeśli system nie jest systemów produkcyjnych, bazy danych SAP obsługiwanych przez program SQL Server musi zapasową okresowo. Ponieważ usługa Azure Storage chroni trzy obrazy, kopia zapasowa jest teraz mniej ważne w odniesieniu do kompensowanie awarii magazynu. Powodem priorytet utrzymania właściwego planu tworzenia kopii zapasowych i odzyskiwania jest więcej, który można kompensowane błędy logiczne/ręczny, zapewniając punktu w czasie możliwości odzyskiwania. Dlatego celem jest albo użyj kopii zapasowych, aby przywrócić bazy danych niektórych punktu w czasie lub umożliwia tworzenie kopii zapasowych w usłudze Azure inicjatora innego systemu przez skopiowanie istniejącej bazy danych. Na przykład można przeniesiesz z konfiguracji SAP warstwy 2 do 3-warstwowej systemu BIOS tego samego systemu przez Przywracanie kopii zapasowej.

Istnieją trzy różne sposoby tworzenia kopii zapasowych programu SQL Server do usługi Azure Storage:

1. SQL Server 2012 CU4 i wyższe może natywnie kopii zapasowej baz danych do adresu URL. To jest szczegółowo opisane w blogu [nowych funkcji w programie SQL Server 2014 — część 5 – Backup/Restore ulepszenia](https://blogs.msdn.com/b/saponsqlserver/archive/2014/02/15/new-functionality-in-sql-server-2014-part-5-backup-restore-enhancements.aspx). Patrz rozdział [programu SQL Server 2012 SP1 CU4 lub nowszy][dbms-guide-5.5.1].
2. Wersje programu SQL Server przed SQL 2012 CU4 służy funkcji przekierowania do kopii zapasowej na dysku VHD i zasadniczo przejścia strumień zapisu do lokalizacji magazynu Azure, który został skonfigurowany. Patrz rozdział [programu SQL Server 2012 z dodatkiem SP1 CU3 i wcześniejszych wersjach][dbms-guide-5.5.2].
3. Ostatnia metoda jest wykonanie konwencjonalnych kopii zapasowej programu SQL Server do polecenia dysku na dysk VHD.  To jest identyczny z wzorcem wdrożenia lokalnego i nie jest omówiona szczegółowo w tym dokumencie.

#### <a name="0fef0e79-d3fe-4ae2-85af-73666a6f7268"></a>SQL Server 2012 SP1 CU4 lub nowszy
Ta funkcja umożliwia bezpośrednio kopii zapasowych do magazynu obiektów BLOB Azure. Bez tej metody można kopie zapasowe innych wirtualne dyski twarde Azure, która będzie używać pojemność wirtualnego dysku twardego i IOPS. Koncepcja jest zasadniczo to:

 ![Przy użyciu kopii zapasowej programu SQL Server 2012 do platformy Microsoft Azure magazynu obiektów BLOB][dbms-guide-figure-400]

Zaletą jest w tym przypadku jeden nie musi przeznaczać wirtualne dyski twarde do przechowywania kopii zapasowych programu SQL Server na. Tak ma mniejszą liczbę dysków VHD przydzielone i całą przepustowość iops wirtualnego dysku twardego może służyć do plików danych i dziennika. Należy pamiętać, że maksymalny rozmiar kopii zapasowej jest ograniczone do maksymalnie 1 TB, zgodnie z opisem w sekcji "Ograniczenia" w tym artykule: <https://msdn.microsoft.com/library/dn435916.aspx#limitations>. Jeśli rozmiar kopii zapasowej, pomimo przy użyciu kopii zapasowej serwera SQL kompresji spowoduje przekroczenie 1 TB, rozmiar, funkcje opisane w rozdziale [programu SQL Server 2012 z dodatkiem SP1 CU3 i wcześniejszych wersjach] [ dbms-guide-5.5.2] w tym dokumencie musi być używane.

[Dokumentację pokrewną](https://msdn.microsoft.com/library/dn449492.aspx) opisujące przywracania bazy danych z kopii zapasowej na magazyn obiektów Blob Azure zaleca nie, aby przywrócić bezpośrednio z magazynu obiektów BLOB platformy Azure, jeśli kopie zapasowe > 25 GB. Zalecenia w tym artykule jest po prostu oparta na zagadnienia dotyczące wydajności i nie ze względu na ograniczenia funkcjonalności. W związku z tym inne warunki mogą stosować na podstawie przypadku.

Można znaleźć w dokumentacji w sposób ustawiania i wykorzystać ten typ kopii zapasowej [to](https://msdn.microsoft.com/library/dn466438.aspx) samouczka

Przykład sekwencji kroki mogą być odczytywane [tutaj](https://msdn.microsoft.com/library/dn435916.aspx).

Automatyzacja tworzenia kopii zapasowych, jest najwyższym znaczenie upewnij się, że inne nazwy obiektów blob dla każdej kopii zapasowej. W przeciwnym razie zostaną zastąpione i łańcuch restore został przerwany.

Aby nie łączyć się elementy między 3 różne typy kopii zapasowych zaleca się tworzenia różnych kontenerów poniżej konto magazynu używane dla kopii zapasowych. Kontenery można przez maszynę Wirtualną lub przez typ maszyny Wirtualnej i tworzenia kopii zapasowej tylko. Schemat może wyglądać jak:

 ![Za pomocą programu SQL Server 2012 wykonywanie kopii zapasowej na obiektu BLOB magazynu Azure Microsoft — różne kontenery w ramach oddzielnego konta magazynu][dbms-guide-figure-500]

W powyższym przykładzie do tego samego konta magazynu, w których są wdrożone maszyny wirtualne nie jest wykonywane kopie zapasowe. Byłoby nowe konto magazynu, w szczególności na kopie zapasowe. W ramach konta magazynu będzie różnych kontenerów utworzone za pomocą macierzy typu kopii zapasowej oraz nazwę maszyny Wirtualnej. Takie segmentacji ułatwi administrowanie kopii zapasowych różnych maszyn wirtualnych.

Obiekty BLOB jedną bezpośrednio zapisuje kopie zapasowe do, nie można dodać do liczby dysków VHD maszyny wirtualnej. Dlatego jedną można zwiększyć maksymalną liczbę wirtualnych dysków twardych zainstalowanych z określonej jednostki SKU maszyny Wirtualnej dla danych i transakcji plik dziennika i nadal wykonywać kopii zapasowej przed kontenera magazynu.

#### <a name="f9071eff-9d72-4f47-9da4-1852d782087b"></a>SQL Server 2012 z dodatkiem SP1 CU3 i wcześniejszych wersjach
Pierwszy krok należy wykonać w celu uzyskania kopii zapasowej bezpośrednio w usłudze Azure Storage byłoby Pobierz plik msi, które jest połączone z [to](https://www.microsoft.com/download/details.aspx?id=40740) KBA artykułu.

Plik instalacyjny pobierania x64 i dokumentację. Plik zostanie zainstalowany program o nazwie: "Microsoft SQL Server kopii zapasowej do narzędzia Microsoft Azure". Dokładnie zapoznaj się z dokumentacją produktu.  Narzędzie zasadniczo działa w następujący sposób:

* Ze strony programu SQL Server określono lokalizację dysku do utworzenia kopii zapasowej programu SQL Server (nie używaj dysku D:\ w tym).
* Narzędzie będzie umożliwiają definiowanie zasad, które mogą służyć do kierowania poszczególnych typów kopii zapasowych do różnych kontenerów. Magazyn Azure.
* Gdy zasady są stosowane, narzędzie przekieruje strumień zapisu kopii zapasowej do jednego z dysków VHD/dysków do lokalizacji magazynu Azure, który został wcześniej zdefiniowany.
* Narzędzie pozostawi pliku niewielkie kilka rozmiaru KB na dysk VHD/dysku, który został zdefiniowany dla programu SQL Server kopii zapasowej. **Ten plik należy pozostawić go w lokalizacji magazynu jest wymagane do przywrócenia ponownie z usługi Magazyn Azure.**
  * Jeśli wybrano opcję Tworzenie kopii zapasowych na koncie usługi Magazyn Microsoft Azure możesz utracić plik szczątkowy (np. poprzez utraty nośników, który zawiera plik szczątkowy), pobierając je z s może odzyskać plik szczątkowy za pośrednictwem usługi Magazyn Microsoft Azure kontener torage, w którym została wprowadzona. Następnie należy umieścić plik szczątkowy do folderu na komputerze lokalnym, w którym narzędzie jest skonfigurowane do wykrywania i przekazać do tego samego kontenera, używając tego samego hasła szyfrowania, jeśli szyfrowanie została użyta z oryginalnej reguły.

Oznacza to, że schemat zgodnie z powyższym opisem dla nowszej wersji programu SQL Server mogą być przełączane w miejscu, jak również dla wersji programu SQL Server, które nie zezwalają na bezpośredni adres lokalizacji magazynu Azure.

Ta metoda nie powinna być używana z nowszej wersji programu SQL Server, które obsługuje wykonywania kopii zapasowych natywnie w usłudze Azure Storage. Wyjątki są, gdzie ograniczenia natywnego wykonywania kopii zapasowych na platformie Azure blokują natywnego wykonywania kopii zapasowej na platformie Azure.

#### <a name="other-possibilities-to-backup-sql-server-databases"></a>Inne możliwości tworzenia kopii zapasowych baz danych serwera SQL
Dołącz dodatkowe pliki VHD do maszyny Wirtualnej, którego używasz do przechowywania kopii zapasowych na jest innych możliwości tworzenia kopii zapasowej bazy danych. W takim przypadku należy się upewnić, że wirtualne dyski twarde nie są uruchomione pełna. Jeśli tak jest, należy odinstalować dysku VHD, a więc do speak "archiwizować" i zastąp go nowy pusty dysk VHD. Jeśli ta ścieżka jest przerywane, chcesz zachować te wirtualne dyski twarde w osobnych kont magazynu Azure niż które wirtualne dyski twarde z plikami bazy danych.

Druga możliwość polega na dużej maszynie Wirtualnej, która może mieć wiele wirtualnych dysków twardych, które są dołączone. Na przykład D14 z 32VHDs. Używać funkcji miejsca do magazynowania do tworzenia elastyczne środowisko, gdzie można zbudować udziałów, które są następnie używane jako obiekty docelowe kopii zapasowej dla różnych serwerów systemu DBMS.

Najlepsze rozwiązania został udokumentowany [tutaj](https://blogs.msdn.com/b/sqlcat/archive/2015/02/26/large-sql-server-database-backup-on-an-azure-vm-and-archiving.aspx) również.

#### <a name="performance-considerations-for-backupsrestores"></a>Zagadnienia dotyczące wydajności dla kopii zapasowych/przywracania
Jak wdrożenia bez systemu operacyjnego wydajności tworzenia kopii zapasowej i przywracania jest zależna od mogą być odczytywane jak wiele woluminów równolegle i co można przepływność tych woluminów. Ponadto zużycie procesora CPU używanych przez kompresję kopii zapasowych może odtworzyć istotną rolę na maszynach wirtualnych z właśnie maksymalnie 8 wątków Procesora. W związku z tym co można założyć:

* Mniejsza liczba dysków VHD używana do przechowywania danych plików, mniejszych ogólną przepustowość podczas odczytywania.
* Im mniejsza liczba CPU wątki w maszynie Wirtualnej, bardziej rygorystycznych wpływ kompresja kopii zapasowej.
* Mniejszej liczby celów (obiekty BLOB lub wirtualne dyski twarde) można zapisać kopii zapasowej do mniejszej przepływności.
* Mniejsze maszyny Wirtualnej rozmiar, im mniejsza przepływności przydział magazynowania zapisu i odczytu z magazynu Azure. Niezależnie od tego, czy kopie zapasowe są przechowywane bezpośrednio na obiektów Blob platformy Azure lub czy są przechowywane w plikach VHD, które ponownie są przechowywane w obiektach blob Azure.

Korzystając z obiektu BLOB magazynu Azure Microsoft jako miejsce docelowe kopii zapasowej w nowszej wersji, jest ograniczony do wyznaczania tylko jeden obiekt docelowy adresu URL dla każdej kopii zapasowej.

Ale korzystając "Microsoft SQL Server kopia zapasowa narzędzia Microsoft Azure" w starszych wersjach, można zdefiniować więcej niż jeden element docelowy pliku. Z więcej niż jeden element docelowy tworzenie kopii zapasowej można skalować i przepływności kopii zapasowej jest wyższy. To spowoduje następnie wielu plików, jak również na koncie magazynu Azure. Podczas testów przy użyciu wielu plików miejsc docelowych, co ostatecznie osiągnięcia przepływności, której jeden można osiągnąć z rozszerzeniami kopii zapasowej zaimplementowana w z programu SQL Server 2012 SP1 CU4 na. Możesz również nie są blokowane przez limit 1TB, tak jak natywnego wykonywania kopii zapasowych na platformie Azure.

Należy jednak pamiętać, przepływność również jest zależny od lokalizacji konta magazynu Azure, możesz użyć do tworzenia kopii zapasowej. Rozwiązaniem może być można zlokalizować konta magazynu w regionie innym niż maszyny wirtualne są uruchomione. Na przykład Czy uruchomić konfiguracji maszyny Wirtualnej w Europie Zachodnia, ale zawiesić konto magazynu, który umożliwia tworzenie kopii zapasowej przed w Europa Północna. Czy na pewno będą miały wpływ na wydajność tworzenia kopii zapasowej i prawdopodobnie nie można wygenerować przepustowości 150MB/s, jak wygląda na to możliwe w przypadku, gdy docelowy magazyn i maszyny wirtualne są uruchomione w tym samym regionalne centrum danych.

#### <a name="managing-backup-blobs"></a>Zarządzanie obiekty BLOB kopii zapasowej
Istnieje konieczność zarządzania kopiami zapasowymi samodzielnie. Ponieważ oczekuje się, że wiele obiektów blob zostaną utworzone, wykonując kopie zapasowe dziennika transakcji częste, administracja tych obiektów blob można łatwo przeciążać portalu Azure. W związku z tym jest recommendable wykorzystać Eksploratora magazynu Azure. Istnieje kilka dobrej dostępnymi, które ułatwiają zarządzanie kontem magazynu platformy Azure

* Microsoft Visual Studio z zestawem Azure SDK zainstalowany (<https://azure.microsoft.com/downloads/>)
* Eksplorator usługi Storage platformy Microsoft Azure (<https://azure.microsoft.com/downloads/>)
* 3 narzędzi

[comment]: <> (Nie jest jeszcze obsługiwane na ARM)
[comment]: <> (### Azure kopii zapasowej maszyny Wirtualnej)
[comment]: <> (Maszyny wirtualne w ramach systemu SAP utworzeniem kopii zapasowej za pomocą funkcji Kopia zapasowa maszyny wirtualnej Azure. Azure kopii zapasowej maszyny wirtualnej został wprowadzony na początku roku 2015 i tym samym czasie jest standardowe metody kopii zapasowej pełnej maszyny Wirtualnej na platformie Azure. Kopia zapasowa Azure przechowuje kopie zapasowe na platformie Azure i pozwala ponownie przywracania maszyny wirtualnej.)
[comment]: <> (Maszyny wirtualne, które wykonywania może być kopie zapasowe baz danych w sposób ciągły, jak również w przypadku systemów DBMS obsługuje usługi VSS kopii tle woluminu programu Windows < jest https://msdn.microsoft.com/library/windows/desktop/bb968832.aspx> jako programu SQL Server. Przy użyciu kopii zapasowej maszyny Wirtualnej Azure może być sposobem uzyskania umożliwiająca przywrócenie kopii zapasowej bazy danych SAP. Należy jednak pamiętać, który oparty na wykonywanie kopii zapasowych maszyny Wirtualnej platformy Azure, które przywraca w momencie baz danych nie jest możliwe. Dlatego zaleca się wykonywanie kopii zapasowych baz danych z funkcjami systemu DBMS zdejmując to zadanie kopii zapasowej maszyny Wirtualnej Azure.)
[comment]: <> (Aby zapoznać się z kopii zapasowej maszyny wirtualnej platformy Azure Uruchom tutaj < https://azure.microsoft.com/documentation/services/backup/>)

### <a name="1b353e38-21b3-4310-aeb6-a77e7c8e81c8"></a>Przy użyciu obrazów programu SQL Server z witryny Microsoft Azure Marketplace
Firma Microsoft oferuje maszyn wirtualnych w portalu Azure Marketplace, które już zawierają wersjach programu SQL Server. SAP klientów, którzy wymagają licencji programu SQL Server i Windows może to być możliwość zasadniczo pokrycia potrzebę licencji Obracająca się maszyn wirtualnych z programem SQL Server już zainstalowana. Aby użyć takich obrazów dla SAP, należy wykonać następujące kwestie:

* Wersje programu SQL Server z systemem innym niż oceny uzyskać wyższe koszty niż tylko "Tylko do systemu Windows" maszyny Wirtualnej wdrożone z portalu Azure Marketplace. Zobacz następujące artykuły, aby porównać ceny: <https://azure.microsoft.com/pricing/details/virtual-machines/> i <https://azure.microsoft.com/pricing/details/virtual-machines/#Sql>.
* Można używać tylko wersji programu SQL Server, które są obsługiwane przez SAP, takich jak SQL Server 2012.
* Sortowania wystąpienia programu SQL Server, który jest instalowany na maszynach wirtualnych, w portalu Azure Marketplace nie jest sortowania SAP NetWeaver wymaga, aby uruchomić wystąpienie programu SQL Server. Chociaż z instrukcjami w poniższej sekcji, można zmienić sortowania.

#### <a name="changing-the-sql-server-collation-of-a-microsoft-windowssql-server-vm"></a>Zmienianie sortowania serwera SQL programu Microsoft Windows/SQL maszyny Wirtualnej
Ponieważ obrazów programu SQL Server w portalu Azure Marketplace nie są skonfigurowane do korzystania z sortowania, co jest wymagane przez aplikacje SAP NetWeaver, trzeba zmienić natychmiast po wdrożeniu. Dla programu SQL Server 2012 można to zrobić z następujących kroków natychmiast po wdrożeniu maszyny Wirtualnej i administratora jest w stanie zalogować się do wdrożonej maszyny Wirtualnej:

* Otwórz okno poleceń programu Windows "Administrator".
* Zmień katalog C:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012.
* Uruchom polecenie: Setup.exe/quiet/Action = / InstanceName REBUILDDATABASE = parametr/SQLSYSADMINACCOUNTS MSSQLSERVER =`<local_admin_account_name`> /SQLCOLLATION = SQL_Latin1_General_Cp850_BIN2   
  * `<local_admin_account_name`> to konto, która została zdefiniowana jako konto administratora podczas wdrażania maszyny Wirtualnej po raz pierwszy za pomocą galerii.

Proces tylko powinien zająć kilka minut. Aby upewnić się, czy krok ostatecznie otrzymano prawidłowego wyniku, należy wykonać następujące czynności:

* Otwórz program SQL Server Management Studio.
* Otwórz okno zapytania.
* Wykonanie polecenia sp_helpsort w bazie danych master programu SQL Server.

Oczekiwany wynik powinien wyglądać podobnie jak:

    Latin1-General, binary code point comparison sort for Unicode Data, SQL Server Sort Order 40 on Code Page 850 for non-Unicode Data

Jeśli nie jest to wynik, Zatrzymaj wdrożenie SAP i zbadać, dlaczego polecenia Instalatora nie działać zgodnie z oczekiwaniami. Wdrażanie aplikacji programu SAP NetWeaver na wystąpienie programu SQL Server z innego serwera SQL strony kodowe niż wymienione powyżej jest **nie** obsługiwane.

### <a name="sql-server-high-availability-for-sap-in-azure"></a>SQL Server wysokiej dostępności dla programu SAP na platformie Azure
Jak wspomniano wcześniej w tym dokumencie, nie było możliwości do utworzenia magazynu udostępnionego, który jest konieczny do użycia najstarsze funkcji wysokiej dostępności programu SQL Server. Ta funkcja zainstalować dwóch lub więcej wystąpień programu SQL Server w Windows Server Failover Cluster (WSFC) za pomocą udostępnionego dysku dla bazy danych użytkowników (i ostatecznie tempdb). Jest to metoda standardowe wysokiej dostępności długi czas, który także jest obsługiwany przez SAP. Ponieważ Azure nie obsługuje magazynu udostępnionego, nie zrealizowane konfiguracji o wysokiej dostępności programu SQL Server z konfiguracji klastra udostępnionego dysku. Inne metody wysoka dostępność jest jednak nadal możliwe i są opisane w poniższych sekcjach.

[comment]: <> (Artykuł nadal odwołuje się do funkcji ASM)
[comment]: <> (Przed przeczytaniem można używać technologii różnych określonych wysoką dostępność dla programu SQL Server na platformie Azure, jest bardzo dobre dokumentu, który zapewnia bardziej szczegółowe informacje i wskaźniki [[[[tutaj] Virtual-Machines-SQL-Server-High-Availability-and-Disaster-Recovery-Solutions])

#### <a name="sql-server-log-shipping"></a>Wysyłanie dziennika programu SQL Server
Jest jedną z metod wysokiej dostępności (HA), wysyłania dzienników serwera SQL. Jeśli działa rozpoznawanie nazw maszyn wirtualnych uczestniczących w konfiguracji wysokiej dostępności, problem nie występuje i ustawienia na platformie Azure będzie różnią się od żadnej konfiguracji, które jest wykonywane lokalnie. Nie zaleca się ufać tylko rozpoznawania adresu IP. W odniesieniu do konfigurowania wysyłania dzienników i zasadami wokół wysyłania dziennika Sprawdź, czy w tej dokumentacji:

<https://technet.microsoft.com/library/ms187103.aspx>

Aby osiągnąć naprawdę wysokiej dostępności, należy wdrożyć maszyn wirtualnych, które znajdują się w takiej wysyłania dziennika konfiguracji się w obrębie tego samego zestawu dostępności Azure.

#### <a name="database-mirroring"></a>Funkcja dublowania baz danych
Funkcja dublowania bazy danych, obsługiwana przez SAP (patrz Uwaga SAP [965908]) polega na definiowanie serwer partnerski trybu failover w parametrach połączenia SAP. Dla przypadków między różnymi lokalizacjami przyjęto założenie, że dwie maszyny wirtualne są w tej samej domenie i że kontekstu użytkownika dwa wystąpienia programu SQL Server, są uruchomione w są również użytkownikami domeny i mają wystarczające uprawnienia w dwóch wystąpień programu SQL Server związane. W związku z tym Konfigurowanie funkcji dublowania baz danych na platformie Azure nie różnią się lokalnej typowe ustawienia/konfiguracji.

Począwszy od wdrożenia tylko na chmurze najprostszą ma mieć inny Instalator domeny na platformie Azure mają tych maszyn wirtualnych systemu DBMS (i najlepiej dedykowanych SAP maszyn wirtualnych) w jednej domenie.

Jeśli domeny nie jest możliwe, co można także używać certyfikatów dublowania punktów końcowych, zgodnie z opisem w tym miejscu baz danych: <https://technet.microsoft.com/library/ms191477.aspx>

Samouczek do konfiguracji dublowania bazy danych na platformie Azure można znaleźć tutaj: <https://technet.microsoft.com/library/ms189852.aspx>

#### <a name="alwayson"></a>Zawsze włączone
Jak AlwaysOn jest obsługiwany dla lokalnego programu SAP (patrz Uwaga SAP [1772688]), można używać w połączeniu z SAP na platformie Azure jest obsługiwane. Fakt, że nie jest możliwe do utworzenia udostępnionych dysków na platformie Azure nie oznacza, że jeden nie można utworzyć konfiguracji AlwaysOn Windows Server Failover Cluster (WSFC), między różnych maszyn wirtualnych. Oznacza jedynie, że nie ma możliwości użycia udostępnionego dysku jako kworum w konfiguracji klastra. Dlatego możesz skompilować konfiguracji usługi WSFC (AlwaysOn) na platformie Azure i po prostu nie wybierz typ kworum, który wykorzystuje udostępniony dysk. W środowisku platformy Azure te maszyny wirtualne są wdrażane w powinien resolve maszyny wirtualne według nazwy i maszyn wirtualnych powinna być w tej samej domenie. Dotyczy to tylko Azure i wdrożeń między lokalizacjami. Istnieją pewne uwagi dotyczące wdrażania odbiornika grupy dostępności programu SQL Server (nie należy mylić jej z zestawu dostępności Azure) ponieważ Azure w tym momencie nie zezwalają na po prostu utworzyć obiektu AD/serwera DNS, jak to możliwe lokalnymi. Dlatego niektóre kroki instalacji różnych są niezbędne w celu wyeliminowania określone zachowanie systemu Azure.

Niektóre kwestie wymagające rozważenia przy użyciu odbiornika grupy dostępności są:

* Przy użyciu odbiornika grupy dostępności jest możliwe tylko z systemu Windows Server 2012 lub Windows Server 2012 R2 jako system operacyjny gościa maszyny wirtualnej. Dla systemu Windows Server 2012 należy się upewnić, że ta poprawka jest stosowana: <https://support.microsoft.com/kb/2854082>
* Dla systemu Windows Server 2008 R2 ta poprawka nie istnieje i można używać w taki sam sposób jak dublowania bazy danych, określając serwer partnerski trybu failover w parametrach połączenia musi zawsze włączone (zrobić za pomocą default.pfl parametru bazami danych/mss/serwerem SAP — patrz Uwaga SAP [965908]).
* Przy użyciu odbiornika grupy dostępności, maszyn wirtualnych do bazy danych powinny być połączone z dedykowanym równoważenia obciążenia. Rozpoznawanie nazw w przypadku wdrożeń tylko w chmurze albo wymagają wszystkich maszyn wirtualnych systemu SAP (serwerów aplikacji, bazami danych serwera i serwera (sieci) SCS) znajdują się w tej samej sieci wirtualnej lub wymaga z warstwy aplikacji SAP konserwacji etc\host pliku do Pobierz nazw maszyn wirtualnych maszyn wirtualnych serwera SQL, które zostały rozwiązane. W celu uniknięcia czy Azure przypisuje nowe adresy IP w przypadku gdy obie maszyny wirtualne są okazjonalnie zamknięcia, jeden należy przypisywać statyczne adresy IP do interfejsów sieciowych maszyn wirtualnych w konfiguracji funkcji AlwaysOn (Definiowanie statycznego adresu IP jest opisane w [to] [ virtual-networks-reserved-private-ip] artykuł)

[comment]: <> (Stary blogi)
[comment]: <> (< https://blogs.msdn.com/b/alwaysonpro/archive/2014/08/29/recommendations-and-best-practices-when-deploying-sql-server-alwayson-availability-groups-in-windows-azure-iaas.aspx>, < https://blogs.technet.com/b/rmilne/ Archive/2015/07/27/How-to-set-static-IP-on-Azure-VM.aspx >)
* Istnieją specjalne kroki wymagane podczas kompilowania konfiguracji klastra usługi WSFC, gdy klaster musi specjalne adres IP przypisany, ponieważ Azure z jego bieżącej funkcji przypisywanej nazwy klastra ten sam adres IP jako węzeł klastra jest tworzony na. Oznacza to, że należy wykonać to krok wykonywany ręcznie, aby przypisać inny adres IP do klastra.
* Odbiornik grupy dostępności, będzie można utworzyć na platformie Azure z punktami końcowymi protokołu TCP/IP, które są przypisane do maszyn wirtualnych z podstawowych i pomocniczych replik grupy dostępności.
* Może być potrzebne do zabezpieczania te punkty końcowe z listy ACL.

[comment]: <> (Blog starego TODO)
[comment]: <> (Szczegółowe instrukcje i artykuły pierwszej potrzeby zainstalować konfiguracji funkcji AlwaysOn na platformie Azure są najlepiej wystąpił podczas Instruktaż dostępny samouczek [here][virtual-machines-windows-classic-ps-sql-alwayson-availability-groups])
[comment]: <> (Wstępnie konfiguracji funkcji AlwaysOn za pomocą galerii Azure < https://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx>)
[comment]: <> (Tworzenie odbiornika grupy dostępności jest najlepiej opisane w samouczku [this][virtual-machines-windows-classic-ps-sql-int-listener])
[comment]: <> (Zabezpieczanie punktów końcowych sieci z listy ACL są omówione najlepiej:)
[comment]: <> (* < https://michaelwasham.com/windows-azure-powershell-reference-guide/network-access-control-list-capability-in-windows-azure-powershell/>)
[comment]: <> (* < https://blogs.technet.com/b/heyscriptingguy/archive/2013/08/31/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-1-of-2.aspx>)
[comment]: <> (* < https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/01/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-2-of-2.aspx>)  
[comment]: <> (* < https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/18/creating-acls-for-windows-azure-endpoints.aspx>)

Istnieje możliwość wdrożenia grupy dostępności AlwaysOn programu SQL Server w różnych regionach platformy Azure oraz. Ta funkcja będzie korzystać z łączności Azure do wirtualnymi ([szczegółowe][virtual-networks-configure-vnet-to-vnet-connection]).

[comment]: <> (Blog starego TODO)
[comment]: <> (Konfigurowanie grup dostępności AlwaysOn programu SQL Server w takiej sytuacji opisanej tutaj: < https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.)

#### <a name="summary-on-sql-server-high-availability-in-azure"></a>Podsumowanie na wysokiej dostępności serwera SQL na platformie Azure
Biorąc pod uwagę fakt, że usługi Azure Storage chroni zawartość, jest mniej powodem wymagania obrazu stałej gotowości. Oznacza to, że danego scenariusza wysokiej dostępności należy chronić tylko względem następujących przypadkach:

* Niedostępność maszyny wirtualnej jako całość z powodu konserwacji w klastrze serwerów w usłudze Azure lub z innych powodów
* Problemy z oprogramowaniem w wystąpieniu programu SQL Server
* Ochrona przed ręczne błąd, gdzie danych zostaje usunięta, a w momencie odzyskiwania jest wymagana

Spojrzenie na zgodną technologii, których jedną można argumentowało czy dwóch pierwszych przypadkach może być objętych przez dublowania bazy danych lub funkcji AlwaysOn, natomiast trzeci przypadku tylko może być objętych przez wysyłanie dziennika.

Konieczne będzie saldo bardziej złożonych konfiguracji funkcji AlwaysOn, w porównaniu do funkcji dublowania baz danych, z zalet funkcji AlwaysOn. Może być wymieniona te korzyści, takich jak:

* Do odczytu replikach pomocniczych.
* Tworzenie kopii zapasowych z replik pomocniczych.
* Lepszą skalowalność.
* Więcej niż jednej repliki pomocniczej.

### <a name="9053f720-6f3b-4483-904d-15dc54141e30"></a>Ogólne programu SQL Server dla programu SAP w podsumowaniu Azure
Istnieje wiele zaleceń w tym przewodniku, i zaleca się, że można go odczytać więcej niż raz przed Planowanie wdrożenia usługi Azure. Ogólnie rzecz biorąc jednak należy postępować zgodnie top dziesięć DBMS ogólne w określonych punktach Azure:

[comment]: <> (2.3 przepływności wyższy niż co? Niż jeden wirtualny dysk twardy?)
1. Użyj najnowszej wersji systemu DBMS, takich jak SQL Server 2014 z większości korzyści w systemie Azure. Dla programu SQL Server to SQL Server 2012 SP1 CU4 obejmujące funkcję zapasowego sprzętu magazynu Azure. Jednak w połączeniu z SAP zalecamy co najmniej pakietu CU1 programu SQL Server 2014 z dodatkiem SP1 lub SQL Server 2012 z dodatkiem SP2 i najnowszej aktualizacji zbiorczej.
2. Starannie zaplanować Twojej pozioma systemu SAP na platformie Azure w celu zrównoważenia ograniczenia Azure i układ pliku danych:
   * Nie ma zbyt wiele wirtualnych dysków twardych, ale aby upewnić się, że może nawiązać połączenie z wymagane IOPS.
   * Należy pamiętać, że IOPS są również ograniczone na konto magazynu Azure i czy kont magazynu są ograniczone w ramach każdej subskrypcji platformy Azure ([szczegółowe][azure-subscription-service-limits]).
   * Tylko rozłożonej na wirtualne dyski twarde, jeśli w celu osiągnięcia wyższej przepustowości.
3. Nigdy nie instaluj oprogramowania lub umieść wszystkie pliki, które wymaga trwałości na dysku D:\, jest niestałych i wszystko na tym dysku zostaną utracone podczas rozruchu systemu Windows.
4. Nie używaj buforowania Azure wirtualnego dysku twardego dla usługi Azure Standard Storage.
5. Nie należy używać konta magazynu Azure replikacją geograficzną.  Magazyn lokalnie nadmiarowy Użyj dla obciążeń systemu DBMS.
6. Rozwiązania wysokiej dostępności i odzyskiwania po awarii z dostawcą systemu DBMS umożliwia replikowanie danych w bazie danych.
7. Zawsze używaj rozpoznawania nazw, nie należy polegać na adresy IP.
8. Użyj najwyższy możliwy kompresji bazy danych. Dla programu SQL Server jest kompresji strony.
9. Należy zachować ostrożność, przy użyciu obrazów programu SQL Server w witrynie Azure Marketplace. Jeśli używasz programu SQL Server, co należy zmienić sortowania wystąpienia przed zainstalowaniem dowolnego systemu SAP NetWeaver na nim.
10. Instalowanie i konfigurowanie monitorowania SAP hosta dla platformy Azure, zgodnie z opisem w [Deployment Guide][deployment-guide].

## <a name="specifics-to-sap-ase-on-windows"></a>Szczegóły ASE SAP w systemie Windows
Począwszy od programu Microsoft Azure, można łatwo migrować istniejące aplikacje SAP ASE na maszynach wirtualnych platformy Azure. SAP ASE na maszynie wirtualnej pozwala zmniejszyć całkowity koszt posiadania wdrażania, zarządzania i konserwacji aplikacji szerokość przedsiębiorstwa za pomocą łatwo migracji te aplikacje do systemu Microsoft Azure. Z programu SAP ASE w maszynie wirtualnej platformy Azure Administratorzy i deweloperzy można nadal używać tej samej opracowywania i narzędzia administracyjne, które są dostępne w lokalnym.

Brak umowy SLA dla maszyn wirtualnych platformy Azure, które można znaleźć tutaj: <https://azure.microsoft.com/support/legal/sla>

Firma Microsoft upewnieniu się, że Microsoft Azure hostowanej maszyny wirtualnej będzie wykonywać bardzo dobrze w odróżnieniu od innych ofert wirtualizacji chmury publicznej, ale wyniki poszczególnych może się różnić. Zmiany rozmiaru protokoły SAP liczby różnych SAP SAP certyfikowane jednostki SKU wirtualna znajdzie się w oddzielnych Uwaga SAP [1928533].

Instrukcje i zalecenia dotyczące użycia usługi Azure Storage, wdrożenia SAP maszyn wirtualnych lub SAP monitorowania dotyczą wdrożenia SAP ASE w połączeniu z aplikacje SAP w już wspomniano w całym pierwsze cztery rozdziałach tego dokumentu.

### <a name="sap-ase-version-support"></a>Obsługa wersji ASE SAP
SAP obecnie obsługuje ASE SAP wersji 16.0 do użycia z programem SAP Business pakiet produktów. Wszystkie aktualizacje serwera SAP ASE lub sterowniki JDBC i ODBC do użycia z produktami SAP Business pakietu znajdują się wyłącznie za pośrednictwem portalu Marketplace usługi SAP w: <https://support.sap.com/swdc>.

Podobnie jak w przypadku instalacji lokalnej bez pobierania aktualizacji dla serwera SAP ASE lub sterowniki JDBC i ODBC bezpośrednio z witryny sieci Web programu Sybase. Szczegółowe informacje na temat aktualizacji, które są obsługiwane w przypadku użycia z programu SAP Business pakiet produktów lokalnych i w maszynach wirtualnych platformy Azure, zobacz poniższe uwagi SAP:

* [1590719]
* [1973241]

Ogólne informacje o systemie SAP Business Suite SAP ASE można znaleźć w [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Wskazówki dotyczące konfigurowania ASE SAP dla SAP powiązane SAP ASE instalacje w maszynach wirtualnych platformy Azure
#### <a name="structure-of-the-sap-ase-deployment"></a>Struktura wdrożenia SAP ASE
Zgodnie z ogólny opis pliki wykonywalne SAP ASE powinna być znajduje się lub zainstalowany na dysku systemowym podstawowy dysk VHD maszyny Wirtualnej (dysk c:\). Zazwyczaj większość SAP ASE systemu i narzędzi baz danych są nie naprawdę wykorzystywane twardego przez SAP NetWeaver obciążenia. Dlatego system i narzędzi baz danych (master, model, saptools, sybmgmtdb, sybsystemdb) może pozostawać na C:\drive również.

Wystąpił wyjątek może być tymczasowa baza danych zawierająca wszystkie tabele pracy i tabel tymczasowych utworzonych przez ASE SAP, które w przypadku niektórych ERP SAP i wszystkich obciążeń BW może wymagać większą ilość danych lub woluminu operacji We/Wy, który nie mieści się w oryginalnej maszyny Wirtualnej podstawowy wirtualny dysk twardy (dysk c:\).

W zależności od wersji SAPInst/SWPM używane do instalowania systemu może zawierać bazy danych:

* Pojedynczy tempdb SAP ASE, która jest tworzona podczas instalowania programu SAP ASE
* Bazy danych tempdb SAP ASE utworzone przez zainstalowanie SAP ASE i dodatkowe saptempdb utworzone przez procedurę instalacji SAP
* Bazy danych tempdb SAP ASE utworzone przez zainstalowanie SAP ASE i dodatkowych danych tempdb, który został utworzony ręcznie (np. po Uwaga SAP [1752266]) do określonej bazy danych tempdb ERP/BW wymagań

W przypadku ERP określonych lub wszystkich obciążeń BW warto, w zakresie wydajności, aby urządzenia tempdb Ponadto utworzonej bazy danych tempdb (przez SWPM lub ręcznie) na dysku innym niż C:\. Jeśli nie dodatkowe tempdb istnieje on zaleca się utworzenie (Uwaga SAP [1752266]).

W takich systemach Ponadto utworzonej bazy danych tempdb należy przeprowadzić następujące kroki:

* Przenieś pierwszego urządzenia tempdb jako pierwsze urządzenie bazy danych SAP
* Dodaj urządzenia tempdb wszystkie wirtualne dyski twarde zawierające urządzenia bazy danych SAP

Ta konfiguracja umożliwia tempdb albo korzystać więcej miejsca niż dysk systemowy jest zapewnienie. Jako odwołanie jedną Sprawdź rozmiary urządzenia bazy danych tempdb na istniejących systemów, które lokalnie. Lub taka konfiguracja umożliwia liczb IOPS względem bazy danych tempdb, którego nie można podać z dysku systemowego. Ponownie systemów, które są uruchamiane lokalnie może służyć do monitorowania obciążenia We/Wy względem bazy danych tempdb.

Nie wolno umieszczać żadnych urządzeń SAP ASE na dysku D:\ maszyny wirtualnej. Dotyczy to również tempdb, nawet jeśli są tylko tymczasowe obiekty przechowywane w bazie danych tempdb.

#### <a name="impact-of-database-compression"></a>Wpływ kompresji bazy danych
W konfiguracji, gdy przepustowość operacji We/Wy mogą stać się czynnikiem ograniczającym co miar, co zmniejsza liczbę IOPS może przyczynić się do rozciągania obciążenie jednego, mogą uruchamiać w scenariuszu IaaS, takich jak Azure. W związku z tym zdecydowanie zaleca się upewnić, że używa kompresji SAP ASE przed przekazaniem istniejącej bazy danych SAP do platformy Azure.

Zalecenie, aby wykonać kompresji przed przekazaniem do platformy Azure, jeśli nie jest zaimplementowana znajduje się z kilku powodów:

* Jest mniejsza ilość danych do przekazania do platformy Azure
* Czas realizacji kompresji jest krótszy, przy założeniu, że jeden służy silniejszych sprzętu z więcej procesorów ani większą przepustowość operacji We/Wy lub mniej we/wy opóźnień lokalnego
* Mniejsze rozmiary bazy danych może prowadzić do mniejsze koszty przydział dysku

Kompresji danych i obiektów LOB działa na maszynie wirtualnej hostowanej w maszynach wirtualnych platformy Azure, jak ma lokalnego. Więcej informacji na temat sposobu Sprawdź, czy kompresja jest już w użyć w istniejącej bazy danych SAP ASE Sprawdź, czy Uwaga SAP [1750510].

#### <a name="using-dbacockpit-to-monitor-database-instances"></a>Aby monitorować wystąpienia bazy danych przy użyciu DBACockpit
Dla systemów SAP, które korzystają z programu SAP ASE jako bazy danych platformy DBACockpit jest dostępny jako okna przeglądarki osadzony w transakcji DBACockpit lub Webdynpro. Jednak wszystkie funkcje monitorowania i administrowania bazy danych jest dostępna w implementacji Webdynpro DBACockpit tylko.

Jako z systemami lokalnymi kilka czynności umożliwiające wszystkie funkcje programu SAP NetWeaver używane przez implementację Webdynpro DBACockpit. Wykonaj Uwaga SAP [1245200] Aby włączyć użycie webdynpros i generować wymagane te. Gdy zgodnie z instrukcjami zawartymi w powyższych informacji zostanie również skonfigurować Menedżera komunikacji internetowych (icm) oraz porty, które mają być używane dla połączeń http i https. Ustawieniem domyślnym dla protokołu http wygląda następująco:

> ICM/server_port_0 = ochronę = HTTP, PORT = 8000, PROCTIMEOUT = 600, limit czasu = 600
>
> ICM/server_port_1 = ochronę = HTTPS i portu 443$ $, PROCTIMEOUT = = 600, limit czasu = 600
>
>

i linki generowane w transakcji DBACockpit będzie wyglądać podobnie do poniższego:

> https://`<fullyqualifiedhostname`>: 44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://`<fullyqualifiedhostname`>: 8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

W zależności od czy i jak hosting systemu SAP maszyny wirtualnej Azure jest połączony za pośrednictwem lokacja lokacja, obejmujący wiele lokacji lub ExpressRoute (wdrożenie między lokalizacjami), należy się upewnić, że ICM używa pełni kwalifikowaną nazwę hosta, który można rozwiązać ten problem na komputerze gdzie Próbujesz otworzyć DBACockpit z. Zobacz Uwaga SAP [773830] zrozumieć, jak ICM Określa nazwę FQDN hosta w zależności od parametrów profilu i ustaw parametr icm/host_name_full jawnie w razie potrzeby.

Jeśli wdrożono maszynę Wirtualną w scenariuszu tylko w chmurze bez łączności między lokalizacjami między lokalną i platformą Azure, musisz zdefiniować publiczny adres IP i domainlabel. Format publicznej nazwy DNS maszyny wirtualnej zostanie następnie wyglądać następująco:

> `<custom domainlabel`>. `<azure region`>. cloudapp.azure.com
>
>

Można znaleźć więcej szczegółów dotyczących nazwy DNS [tutaj][virtual-machines-azurerm-versus-azuresm].

Ustawienie parametru profilu icm/host_name_full SAP nazwę DNS maszyny Wirtualnej Azure link może wyglądać podobnie do:

> https://mydomainlabel.westeurope.cloudapp.NET:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://mydomainlabel.westeurope.cloudapp.NET:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

W takim przypadku należy koniecznie:

* Dodaj do grupy zabezpieczeń sieci w portalu Azure, aby porty TCP/IP używane do komunikacji z ICM reguł ruchu przychodzącego
* Dodaj do konfiguracji zapory systemu Windows dla portów TCP/IP używany do komunikacji z ICM reguł ruchu przychodzącego

Do automatycznego zaimportowane wszystkie dostępne poprawek zalecane jest okresowo zastosować kolekcji korekty Uwaga SAP mające zastosowanie do używanej wersji programu SAP:

* [1558958]
* [1619967]
* [1882376]

Więcej informacji na temat panelu sterowania DBA SAP ASE można znaleźć w uwagach SAP do następujących:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Uwagi dotyczące tworzenia kopii zapasowej i odzyskiwania dla programu SAP ASE
W przypadku wdrażania SAP ASE do platformy Azure z kopii zapasowej metodologii musi przejrzeć. Nawet jeśli system nie jest systemów produkcyjnych, bazy danych SAP, obsługiwanej przez SAP ASE musi zapasową okresowo. Ponieważ usługa Azure Storage chroni trzy obrazy, kopia zapasowa jest teraz mniej ważne w odniesieniu do kompensowanie awarii magazynu. Główną przyczyną utrzymania właściwego planu tworzenia kopii zapasowej i przywracania jest większa, który można kompensowane błędy logiczne/ręczny, zapewniając punktu w czasie odzyskiwania funkcji. Dlatego celem jest albo użyj kopii zapasowych, aby przywrócić bazy danych niektórych punktu w czasie lub umożliwia tworzenie kopii zapasowych w usłudze Azure inicjatora innego systemu przez skopiowanie istniejącej bazy danych. Na przykład można przeniesiesz z konfiguracji SAP warstwy 2 do 3-warstwowej systemu BIOS tego samego systemu przez Przywracanie kopii zapasowej.

Wykonywanie kopii zapasowych i przywracanie bazy danych na platformie Azure działa tak samo jak lokalnie. Zobacz uwagi SAP:

* [1588316]
* [1585981]

Aby uzyskać więcej informacji na temat tworzenia zrzutu konfiguracji i planowania kopii zapasowych. W zależności od Twoich potrzeb, które można skonfigurować i strategii bazy danych i dziennika zrzuty na dysku na jeden z istniejących dysków VHD lub dodać dodatkowe wirtualnego dysku twardego dla kopii zapasowej.  Aby ograniczyć ryzyko utraty danych w przypadku błędu zaleca się użyć dysku VHD, w którym znajduje się żadnego urządzenia bazy danych.

Oprócz danych i obiektów LOB kompresji SAP ASE oferuje również kompresja kopii zapasowej. Zajmuje mniej miejsca z bazy danych i dziennika zrzuty zaleca kompresja kopii zapasowej. Zobacz Uwaga SAP [1588316] Aby uzyskać więcej informacji. Kompresja kopii zapasowej jest również istotne zmniejszyć ilość danych do przeniesienia, jeśli planujesz do pobrania kopii zapasowych lub wirtualne dyski twarde zawierające zrzuty kopii zapasowej z maszyny wirtualnej platformy Azure do środowiska lokalnego.

Nie należy używać dysku D:\ jako miejsce docelowe zrzutu bazy danych lub dziennika.

#### <a name="performance-considerations-for-backupsrestores"></a>Zagadnienia dotyczące wydajności dla kopii zapasowych/przywracania
Jak wdrożenia bez systemu operacyjnego wydajności tworzenia kopii zapasowej i przywracania jest zależna od mogą być odczytywane jak wiele woluminów równolegle i co można przepływność tych woluminów. Ponadto zużycie procesora CPU używanych przez kompresję kopii zapasowych może odtworzyć istotną rolę na maszynach wirtualnych z właśnie maksymalnie 8 wątków Procesora. W związku z tym co można założyć:

* Mniejsza liczba wirtualnych dysków twardych używany do przechowywania urządzenia bazy danych mniejsza ogólną przepustowość podczas odczytywania
* Im mniejsza liczba CPU wątki w maszynie Wirtualnej, bardziej rygorystycznych wpływ kompresja kopii zapasowej
* Mniej elementy docelowe (Stripe katalogów, wirtualne dyski twarde) można zapisać kopii zapasowej do mniejszej przepływności

Aby zwiększyć liczbę elementów docelowych do zapisu się, że istnieją dwa opcje, które mogą być używane/łączone w zależności od potrzeb:

* Stosowanie wolumin docelowy kopii zapasowej za pośrednictwem wielu wirtualnych dysków twardych zainstalowanych w celu poprawienia przepływności IOPS na tym woluminie rozłożonego
* Tworzenie zrzutu konfiguracji na poziomie SAP ASE, który używa więcej niż jeden katalog docelowy można zapisać zrzutu do

Stosowanie woluminu przez kilka zainstalowanych dysków VHD został omówiony we wcześniejszej części tego przewodnika. Aby uzyskać więcej informacji na temat używania wielu katalogów w konfiguracji zrzutu SAP ASE zapoznaj się dokumentacją na sp_config_dump procedury składowanej, który jest używany do tworzenia konfiguracji zrzutu na [Centrum informacyjne Sybase](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Odzyskiwanie po awarii z maszynami wirtualnymi platformy Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Replikacja danych z serwerem replikacji programu Sybase SAP
W ramach ASE SAP SAP Sybase replikacji serwera (SRS) zapewnia ciepłych rozwiązania rezerwy asynchronicznego przesyłania transakcji bazy danych do lokalizacji odległej.

Instalacji i działania SRS działa również funkcjonalnie hostowane w usługach maszyny wirtualnej Azure, jak lokalnej maszyny Wirtualnej.

HADR ASE za pośrednictwem serwera replikacji SAP jest zaplanowane z przyszłych wersji. Zostanie ono przetestowana i wydane dla platformy Microsoft Azure, jak jest dostępny.

## <a name="specifics-to-sap-ase-on-linux"></a>Szczegóły ASE SAP w systemie Linux
Począwszy od programu Microsoft Azure, można łatwo migrować istniejące aplikacje SAP ASE na maszynach wirtualnych platformy Azure. SAP ASE na maszynie wirtualnej pozwala zmniejszyć całkowity koszt posiadania wdrażania, zarządzania i konserwacji aplikacji szerokość przedsiębiorstwa za pomocą łatwo migracji te aplikacje do systemu Microsoft Azure. Z programu SAP ASE w maszynie wirtualnej platformy Azure Administratorzy i deweloperzy można nadal używać tej samej opracowywania i narzędzia administracyjne, które są dostępne w lokalnym.

Do wdrażania maszyn wirtualnych platformy Azure jest musisz znać oficjalnego umów SLA, które można znaleźć tutaj: <https://azure.microsoft.com/support/legal/sla>

Informacje dotyczące zmiany rozmiaru SAP oraz listę SAP certyfikowane jednostki SKU maszyny Wirtualnej zostanie podany w Uwaga SAP [1928533]. Dodatkowe SAP zmiany rozmiaru dokumentów dla maszyn wirtualnych Azure można znaleźć tutaj <http://blogs.msdn.com/b/saponsqlserver/archive/2015/06/19/how-to-size-sap-systems-running-on-azure-vms.aspx> i tutaj <http : //blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

Instrukcje i zalecenia dotyczące użycia usługi Azure Storage, wdrożenia SAP maszyn wirtualnych lub SAP monitorowania dotyczą wdrożenia SAP ASE w połączeniu z aplikacje SAP w już wspomniano w całym pierwsze cztery rozdziałach tego dokumentu.

Dwa poniższe uwagi SAP zawierają ogólne informacje o ASE w systemie Linux i ASE w chmurze:

* [2134316]
* [1941500]

### <a name="sap-ase-version-support"></a>Obsługa wersji ASE SAP
SAP obecnie obsługuje ASE SAP wersji 16.0 do użycia z programem SAP Business pakiet produktów. Wszystkie aktualizacje serwera SAP ASE lub sterowniki JDBC i ODBC do użycia z produktami SAP Business pakietu znajdują się wyłącznie za pośrednictwem portalu Marketplace usługi SAP w: <https://support.sap.com/swdc>.

Podobnie jak w przypadku instalacji lokalnej bez pobierania aktualizacji dla serwera SAP ASE lub sterowniki JDBC i ODBC bezpośrednio z witryny sieci Web programu Sybase. Szczegółowe informacje na temat aktualizacji, które są obsługiwane w przypadku użycia z programu SAP Business pakiet produktów lokalnych i w maszynach wirtualnych platformy Azure, zobacz poniższe uwagi SAP:

* [1590719]
* [1973241]

Ogólne informacje o systemie SAP Business Suite SAP ASE można znaleźć w [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Wskazówki dotyczące konfigurowania ASE SAP dla SAP powiązane SAP ASE instalacje w maszynach wirtualnych platformy Azure
#### <a name="structure-of-the-sap-ase-deployment"></a>Struktura wdrożenia SAP ASE
Zgodnie z ogólny opis pliki wykonywalne SAP ASE powinien znajduje się lub zainstalowane w głównym systemie plików maszyny wirtualnej (/sybase). Zazwyczaj większość SAP ASE systemu i narzędzi baz danych są nie naprawdę wykorzystywane twardego przez SAP NetWeaver obciążenia. Dlatego system i narzędzi baz danych (master, model, saptools, sybmgmtdb, sybsystemdb) może pozostawać w głównym systemie plików również.

Wystąpił wyjątek może być tymczasowa baza danych zawierająca wszystkie tabele pracy i tabel tymczasowych utworzonych przez ASE SAP, które w przypadku niektórych ERP SAP i wszystkich obciążeń BW może wymagać większą ilość danych lub woluminu operacji We/Wy, który nie pasuje do oryginalna maszyna wirtualna systemu operacyjnego dysk.

W zależności od wersji SAPInst/SWPM używane do instalowania systemu może zawierać bazy danych:

* Pojedynczy tempdb SAP ASE, która jest tworzona podczas instalowania programu SAP ASE
* Bazy danych tempdb SAP ASE utworzone przez zainstalowanie SAP ASE i dodatkowe saptempdb utworzone przez procedurę instalacji SAP
* Bazy danych tempdb SAP ASE utworzone przez zainstalowanie SAP ASE i dodatkowych danych tempdb, który został utworzony ręcznie (np. po Uwaga SAP [1752266]) do określonej bazy danych tempdb ERP/BW wymagań

W przypadku ERP określonych lub wszystkich obciążeń BW warto, w zakresie wydajności, tempdb urządzeniach dodatkowo utworzonej bazy danych tempdb (przez SWPM lub ręcznie) w systemie oddzielny plik, który może być reprezentowany przez dysk pojedynczy danych Azure lub RAID Linux spanning m l dysków danych Azure. Jeśli nie dodatkowe tempdb istnieje on zaleca się utworzenie (Uwaga SAP [1752266]).

W takich systemach Ponadto utworzonej bazy danych tempdb należy przeprowadzić następujące kroki:

* Przenieś pierwszy katalog bazy danych tempdb na pierwszy system plików bazy danych SAP
* Dodaj bazy danych tempdb katalogi na każdym z dysków VHD zawierającego system plików bazy danych SAP

Ta konfiguracja umożliwia tempdb albo korzystać więcej miejsca niż dysk systemowy jest zapewnienie. Jako odwołanie jedną Sprawdź rozmiary katalogu bazy danych tempdb na istniejących systemów, które lokalnie. Lub taka konfiguracja umożliwia liczb IOPS względem bazy danych tempdb, którego nie można podać z dysku systemowego. Ponownie systemów, które są uruchamiane lokalnie może służyć do monitorowania obciążenia We/Wy względem bazy danych tempdb.

Nie wolno umieszczać wszelkich katalogów SAP ASE do katalogu/mnt lub /mnt/resource maszyny wirtualnej. Dotyczy to również tempdb, nawet jeśli obiekty przechowywane w bazie danych tempdb są tylko tymczasowego, ponieważ katalogu/mnt lub /mnt/resource jest domyślna maszyny Wirtualnej Azure tymczasowego miejsca, który nie jest trwały. Więcej informacji na temat miejsca tymczasowego maszyny Wirtualnej platformy Azure można znaleźć w [w tym artykule][virtual-machines-linux-how-to-attach-disk]

#### <a name="impact-of-database-compression"></a>Wpływ kompresji bazy danych
W konfiguracji, gdy przepustowość operacji We/Wy mogą stać się czynnikiem ograniczającym co miar, co zmniejsza liczbę IOPS może przyczynić się do rozciągania obciążenie jednego, mogą uruchamiać w scenariuszu IaaS, takich jak Azure. W związku z tym zdecydowanie zaleca się upewnić, że używa kompresji SAP ASE przed przekazaniem istniejącej bazy danych SAP do platformy Azure.

Zalecenie, aby wykonać kompresji przed przekazaniem do platformy Azure, jeśli nie jest zaimplementowana znajduje się z kilku powodów:

* Jest mniejsza ilość danych do przekazania do platformy Azure
* Czas realizacji kompresji jest krótszy, przy założeniu, że jeden służy silniejszych sprzętu z więcej procesorów ani większą przepustowość operacji We/Wy lub mniej we/wy opóźnień lokalnego
* Mniejsze rozmiary bazy danych może prowadzić do mniejsze koszty przydział dysku

Kompresji danych i obiektów LOB działa na maszynie wirtualnej hostowanej w maszynach wirtualnych platformy Azure, jak ma lokalnego. Więcej informacji na temat sposobu Sprawdź, czy kompresja jest już w użyć w istniejącej bazy danych SAP ASE Sprawdź, czy Uwaga SAP [1750510]. Zobacz też Uwaga SAP [2121797] Aby uzyskać dodatkowe informacje dotyczące kompresji bazy danych.

#### <a name="using-dbacockpit-to-monitor-database-instances"></a>Aby monitorować wystąpienia bazy danych przy użyciu DBACockpit
Dla systemów SAP, które korzystają z programu SAP ASE jako bazy danych platformy DBACockpit jest dostępny jako okna przeglądarki osadzony w transakcji DBACockpit lub Webdynpro. Jednak wszystkie funkcje monitorowania i administrowania bazy danych jest dostępna w implementacji Webdynpro DBACockpit tylko.

Jako z systemami lokalnymi kilka czynności umożliwiające wszystkie funkcje programu SAP NetWeaver używane przez implementację Webdynpro DBACockpit. Wykonaj Uwaga SAP [1245200] Aby włączyć użycie webdynpros i generować wymagane te. Gdy zgodnie z instrukcjami zawartymi w powyższych informacji zostanie również skonfigurować Menedżera komunikacji internetowych (icm) oraz porty, które mają być używane dla połączeń http i https. Ustawieniem domyślnym dla protokołu http wygląda następująco:

> ICM/server_port_0 = ochronę = HTTP, PORT = 8000, PROCTIMEOUT = 600, limit czasu = 600
>
> ICM/server_port_1 = ochronę = HTTPS i portu 443$ $, PROCTIMEOUT = = 600, limit czasu = 600
>
>

i linki generowane w transakcji DBACockpit będzie wyglądać podobnie do poniższego:

> https://`<fullyqualifiedhostname`>: 44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://`<fullyqualifiedhostname`>: 8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

W zależności od czy i jak hosting systemu SAP maszyny wirtualnej Azure jest połączony za pośrednictwem lokacja lokacja, obejmujący wiele lokacji lub ExpressRoute (wdrożenie między lokalizacjami), należy się upewnić, że ICM używa pełni kwalifikowaną nazwę hosta, który można rozwiązać ten problem na komputerze gdzie Próbujesz otworzyć DBACockpit z. Zobacz Uwaga SAP [773830] zrozumieć, jak ICM Określa nazwę FQDN hosta w zależności od parametrów profilu i ustaw parametr icm/host_name_full jawnie w razie potrzeby.

Jeśli wdrożono maszynę Wirtualną w scenariuszu tylko w chmurze bez łączności między lokalizacjami między lokalną i platformą Azure, musisz zdefiniować publiczny adres IP i domainlabel. Format publicznej nazwy DNS maszyny wirtualnej zostanie następnie wyglądać następująco:

> `<custom domainlabel`>. `<azure region`>. cloudapp.azure.com
>
>

Można znaleźć więcej szczegółów dotyczących nazwy DNS [tutaj][virtual-machines-azurerm-versus-azuresm].

Ustawienie parametru profilu icm/host_name_full SAP nazwę DNS maszyny Wirtualnej Azure link może wyglądać podobnie do:

> https://mydomainlabel.westeurope.cloudapp.NET:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://mydomainlabel.westeurope.cloudapp.NET:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

W takim przypadku należy koniecznie:

* Dodaj do grupy zabezpieczeń sieci w portalu Azure, aby porty TCP/IP używane do komunikacji z ICM reguł ruchu przychodzącego
* Dodaj do konfiguracji zapory systemu Windows dla portów TCP/IP używany do komunikacji z ICM reguł ruchu przychodzącego

Do automatycznego zaimportowane wszystkie dostępne poprawek zalecane jest okresowo zastosować kolekcji korekty Uwaga SAP mające zastosowanie do używanej wersji programu SAP:

* [1558958]
* [1619967]
* [1882376]

Więcej informacji na temat panelu sterowania DBA SAP ASE można znaleźć w uwagach SAP do następujących:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Uwagi dotyczące tworzenia kopii zapasowej i odzyskiwania dla programu SAP ASE
W przypadku wdrażania SAP ASE do platformy Azure z kopii zapasowej metodologii musi przejrzeć. Nawet jeśli system nie jest systemów produkcyjnych, bazy danych SAP, obsługiwanej przez SAP ASE musi zapasową okresowo. Ponieważ usługa Azure Storage chroni trzy obrazy, kopia zapasowa jest teraz mniej ważne w odniesieniu do kompensowanie awarii magazynu. Główną przyczyną utrzymania właściwego planu tworzenia kopii zapasowej i przywracania jest większa, który można kompensowane błędy logiczne/ręczny, zapewniając punktu w czasie odzyskiwania funkcji. Dlatego celem jest albo użyj kopii zapasowych, aby przywrócić bazy danych niektórych punktu w czasie lub umożliwia tworzenie kopii zapasowych w usłudze Azure inicjatora innego systemu przez skopiowanie istniejącej bazy danych. Na przykład można przeniesiesz z konfiguracji SAP warstwy 2 do 3-warstwowej systemu BIOS tego samego systemu przez Przywracanie kopii zapasowej.

Wykonywanie kopii zapasowych i przywracanie bazy danych na platformie Azure działa tak samo jak lokalnie. Zobacz uwagi SAP:

* [1588316]
* [1585981]

Aby uzyskać więcej informacji na temat tworzenia zrzutu konfiguracji i planowania kopii zapasowych. W zależności od Twoich potrzeb, które można skonfigurować i strategii bazy danych i dziennika zrzuty na dysku na jeden z istniejących dysków VHD lub dodać dodatkowe wirtualnego dysku twardego dla kopii zapasowej.  Aby ograniczyć ryzyko utraty danych w przypadku błędu zaleca się użyć dysku VHD, w którym znajduje się nie bazy danych pliku lub katalogu.

Oprócz danych i obiektów LOB kompresji SAP ASE oferuje również kompresja kopii zapasowej. Zajmuje mniej miejsca z bazy danych i dziennika zrzuty zaleca kompresja kopii zapasowej. Zobacz Uwaga SAP [1588316] Aby uzyskać więcej informacji. Kompresja kopii zapasowej jest również istotne zmniejszyć ilość danych do przeniesienia, jeśli planujesz do pobrania kopii zapasowych lub wirtualne dyski twarde zawierające zrzuty kopii zapasowej z maszyny wirtualnej platformy Azure do środowiska lokalnego.

Nie należy używać maszyny Wirtualnej Azure miejsca tymczasowego katalogu/mnt lub /mnt/resource jako miejsce docelowe zrzutu bazy danych lub dziennika.

#### <a name="performance-considerations-for-backupsrestores"></a>Zagadnienia dotyczące wydajności dla kopii zapasowych/przywracania
Jak wdrożenia bez systemu operacyjnego wydajności tworzenia kopii zapasowej i przywracania jest zależna od mogą być odczytywane jak wiele woluminów równolegle i co można przepływność tych woluminów. Ponadto zużycie procesora CPU używanych przez kompresję kopii zapasowych może odtworzyć istotną rolę na maszynach wirtualnych z właśnie maksymalnie 8 wątków Procesora. W związku z tym co można założyć:

* Mniejsza liczba wirtualnych dysków twardych używany do przechowywania urządzenia bazy danych mniejsza ogólną przepustowość podczas odczytywania
* Im mniejsza liczba CPU wątki w maszynie Wirtualnej, bardziej rygorystycznych wpływ kompresja kopii zapasowej
* Mniej elementów docelowych (Linux oprogramowaniem RAID, wirtualne dyski twarde) można zapisać kopii zapasowej do mniejszej przepływności

Aby zwiększyć liczbę elementów docelowych do zapisu się, że istnieją dwa opcje, które mogą być używane/łączone w zależności od potrzeb:

* Stosowanie wolumin docelowy kopii zapasowej za pośrednictwem wielu wirtualnych dysków twardych zainstalowanych w celu poprawienia przepływności IOPS na tym woluminie rozłożonego
* Tworzenie zrzutu konfiguracji na poziomie SAP ASE, który używa więcej niż jeden katalog docelowy można zapisać zrzutu do

Stosowanie woluminu przez kilka zainstalowanych dysków VHD został omówiony we wcześniejszej części tego przewodnika. Aby uzyskać więcej informacji na temat używania wielu katalogów w konfiguracji zrzutu SAP ASE zapoznaj się dokumentacją na sp_config_dump procedury składowanej, który jest używany do tworzenia konfiguracji zrzutu na [Centrum informacyjne Sybase](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Odzyskiwanie po awarii z maszynami wirtualnymi platformy Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Replikacja danych z serwerem replikacji programu Sybase SAP
W ramach ASE SAP SAP Sybase replikacji serwera (SRS) zapewnia ciepłych rozwiązania rezerwy asynchronicznego przesyłania transakcji bazy danych do lokalizacji odległej.

Instalacji i działania SRS działa również funkcjonalnie hostowane w usługach maszyny wirtualnej Azure, jak lokalnej maszyny Wirtualnej.

HADR ASE za pośrednictwem SAP replikacji serwera nie jest obsługiwany w tym momencie. Może być przetestowana i wydane w przyszłości dla platformy Microsoft Azure.

## <a name="specifics-to-oracle-database-on-windows"></a>Szczegóły do bazy danych Oracle w systemie Windows
Ponieważ midyear 2013 oprogramowanie Oracle jest obsługiwana przez Oracle do uruchamiania w funkcji Hyper-V systemu Microsoft Windows i Azure. Przeczytaj ten artykuł, aby uzyskać więcej informacji dotyczących ogólnego obsługi funkcji Hyper-V systemu Windows i Azure przez firmę Oracle: <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces>

Następujące ogólne pomocy technicznej również jest obsługiwana danego scenariusza aplikacji SAP korzystania z bazy danych programu Oracle. Szczegółowe informacje są o nazwie w tej części dokumentu.

### <a name="oracle-version-support"></a>Obsługa wersji programu Oracle
Wszystkie szczegółowe informacje o wersji programu Oracle i odpowiednie wersje systemu operacyjnego, które są obsługiwane dla systemie SAP Oracle na maszynach wirtualnych platformy Azure można znaleźć w następujących Uwaga SAP [2039619]

Ogólne informacje o systemie SAP Business Suite Oracle można znaleźć w SCN: <https://scn.sap.com/community/oracle>

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Wskazówki dotyczące konfigurowania programu Oracle dla instalacji programu SAP w maszynach wirtualnych platformy Azure
#### <a name="storage-configuration"></a>Konfiguracja usługi Storage
Tylko jednego wystąpienia obsługiwany Oracle przy użyciu dysków sformatowanym w systemie NTFS. Wszystkie pliki bazy danych muszą być przechowywane w systemie plików NTFS, które są oparte na dyskach VHD. Te wirtualne dyski twarde są zainstalowane na maszynie Wirtualnej platformy Azure i są oparte na magazyn obiektów BLOB Azure strony (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Dowolny dyski sieciowe lub zdalnych udziałów, takich jak usługi Azure plików:

* <https://blogs.msdn.com/b/windowsazurestorage/Archive/2014/05/12/Introducing-Microsoft-Azure-File-Service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/Archive/2014/05/27/persisting-Connections-to-Microsoft-Azure-Files.aspx>

są **nie** obsługiwane dla plików bazy danych programu Oracle!

Za pomocą dysków VHD Azure oparte na magazyn obiektów BLOB Azure strony instrukcji zawartych w tym dokumencie w rozdziale [buforowanie maszyny wirtualne i wirtualne dyski twarde] [ dbms-guide-2.1] i [magazyn Microsoft Azure] [ dbms-guide-2.3] dotyczy wdrożeń z bazą danych programu Oracle również.

Jak opisano wcześniej w głównej części dokumentu, przydziały na przepływność IOPS dla wirtualnych dysków twardych Azure istnieje. Dokładne przydziały w zależności od typu maszyny Wirtualnej służą. Znajduje się lista typów maszyny Wirtualnej z przydziałami ich [tutaj][virtual-machines-sizes]

Aby zidentyfikować obsługiwanych typów maszyny Wirtualnej platformy Azure, zapoznaj się Uwaga SAP [1928533]

Tak długo, jak bieżący przydział IOPS dla każdego dysku spełnia wymagania, istnieje możliwość zapisywania wszystkich plików bazy danych na jeden pojedynczy zainstalowanego Azure dysku VHD.

Jeśli wymaganych jest więcej IOPS, zdecydowanie zalecane jest tworzenie jeden duży urządzenia logicznego w wielu dysków VHD zainstalowanych za pomocą okna pule magazynów (tylko dostępne w systemie Windows Server 2012 i nowsze) lub rozkładanie systemu Windows dla systemu Windows 2008 R2. Zobacz też rozdział [RAID oprogramowania] [ dbms-guide-2.2] tego dokumentu. Takie podejście upraszcza obciążenie administracyjne, aby zarządzać miejscem na dysku i pozwala uniknąć starań, aby ręcznie rozpowszechniają plików kilka zainstalowanych dysków wirtualnych.

#### <a name="backup--restore"></a>Wykonywanie kopii zapasowych i ich przywracanie
Do utworzenia kopii zapasowej / przywrócenia jej funkcjonalności, SAP BR * narzędzi dla programu Oracle są obsługiwane w taki sam sposób jak w standardowe systemów operacyjnych Windows Server i Hyper-V. Menedżer odzyskiwania Oracle (RMAN) jest również obsługiwana dla kopii zapasowych na dysk i przywracanie z dysku.

#### <a name="high-availability"></a>Wysoka dostępność
[comment]: <> (łącze odwołuje się do funkcji ASM)
Oracle Data Guard jest obsługiwana dla zapewnienia wysokiej dostępności i celów odzyskiwania po awarii. Szczegółowe informacje znajdują się w [to] [ virtual-machines-windows-classic-configure-oracle-data-guard] dokumentacji.

#### <a name="other"></a>Inne
Wszystkie inne tematy ogólne jak zestawami dostępności Azure lub SAP monitorowania stosowane zgodnie z opisem w pierwszych trzech rozdziałach tego dokumentu w przypadku wdrożeń maszyn wirtualnych z bazą danych programu Oracle również.

## <a name="specifics-for-the-sap-maxdb-database-on-windows"></a>Szczegóły dla bazy danych SAP MaxDB w systemie Windows
### <a name="sap-maxdb-version-support"></a>Obsługa wersji MaxDB SAP
SAP obecnie obsługuje MaxDB SAP wersji 7,9 do użycia z programem SAP NetWeaver na podstawie produktów na platformie Azure. Wszystkie aktualizacje serwera SAP MaxDB lub sterowniki JDBC i ODBC do użycia z produktów na podstawie SAP NetWeaver są realizowane wyłącznie za pośrednictwem portalu Marketplace usługi SAP w <https://support.sap.com/swdc>.
Ogólne informacje o systemie SAP NetWeaver SAP MaxDB można znaleźć w folderze <https://scn.sap.com/community/maxdb>.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-maxdb-dbms"></a>Obsługiwane typy wersji systemu Windows firmy Microsoft i maszyny Wirtualnej platformy Azure dla systemu DBMS MaxDB SAP
Aby znaleźć obsługiwanej wersji programu Microsoft Windows dla systemu DBMS MaxDB SAP na platformie Azure, zobacz:

* [Macierz dostępności produktu SAP (PAM)][sap-pam]
* Uwaga SAP [1928533]

Zdecydowanie zaleca się przy użyciu najnowszej wersji systemu operacyjnego Microsoft Windows, który jest Microsoft Windows 2012 R2.

### <a name="available-sap-maxdb-documentation"></a>Dokumentacja MaxDB dostępne SAP
Zaktualizowaną listę SAP MaxDB dokumentację można znaleźć w następujących Uwaga SAP [767598]

### <a name="sap-maxdb-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Wskazówki dotyczące konfigurowania MaxDB SAP SAP instalacji na maszynach wirtualnych platformy Azure
#### <a name="b48cfe3b-48e9-4f5b-a783-1d29155bd573"></a>Konfiguracja magazynu
Najlepsze rozwiązania magazynu Azure dla programu SAP MaxDB wykonaj ogólne zalecenia, o których wspomniano w rozdziale [struktury wdrożenia RDBMS][dbms-guide-2].

> [!IMPORTANT]
> Podobnie jak innych baz danych SAP MaxDB ma plików danych i dziennika. Jednak w terminologii SAP MaxDB poprawne określenie jest "wolumin" (nie "plik"). Na przykład istnieją SAP MaxDB woluminów danych i woluminy dziennika. Nie należy mylić tych woluminów dysku systemu operacyjnego.
>
>

Innymi słowy należy:

* Ustaw konto magazynu platformy Azure, które przechowuje woluminy danych i dziennika SAP MaxDB (np. pliki) **lokalny magazyn geograficznie nadmiarowy (LRS)** jak określono w rozdziale [magazyn Microsoft Azure] [ dbms-guide-2.3].
* Oddzielić ścieżkę We/Wy dla woluminów danych SAP MaxDB (np. plików) od ścieżkę We/Wy na woluminy dziennika (np. plików). To oznacza, że woluminy danych SAP MaxDB (np. pliki) muszą być zainstalowane na jednym dysku logicznego, a woluminy dziennika SAP MaxDB (np. pliki) musi być zainstalowany na innym dysku logicznego.
* Określanie prawidłowego pliku buforowania dla poszczególnych obiektów blob platformy Azure, w zależności od tego, czy używać go SAP MaxDB danych lub dziennika woluminów (np. plików) i używać usługi Azure Standard lub Premium usługi Azure Storage, zgodnie z opisem w rozdziale [buforowania dla maszyn wirtualnych] [ dbms-guide-2.1].
* Tak długo, jak bieżący przydział IOPS dla każdego dysku spełnia wymagania, użytkownik może przechowywać wszystkie woluminy danych w jednym zainstalowanego dysku VHD Azure, a także przechowywać wszystkie woluminy dziennika bazy danych na inny jednego zainstalowanego Azure dysku VHD.
* Jeśli wymaganych jest więcej IOPS i/lub miejsca, zdecydowanie zaleca się umożliwiają utworzenie jednego urządzenia logicznego dużych za pośrednictwem pul magazynów okna Microsoft (tylko dostępne w systemie Microsoft Windows Server 2012 i nowsze) lub rozkładanie Microsoft Windows dla systemu Microsoft Windows 2008 R2 wiele zainstalowanych dysków VHD. Zobacz też rozdział [RAID oprogramowania] [ dbms-guide-2.2] tego dokumentu. Takie podejście upraszcza obciążenie administracyjne, aby zarządzać miejscem na dysku i pozwala uniknąć wysiłku ręcznie dystrybucję plików kilka zainstalowanych dysków wirtualnych.
* Najwyższy IOPS wymagania w zakresie można użyć usługi Azure Premium Storage, który jest dostępny na serii DS i GS-series maszyn wirtualnych.

![Odwołanie do konfiguracji IaaS maszyny Wirtualnej platformy Azure dla systemu DBMS MaxDB SAP][dbms-guide-figure-600]

#### <a name="23c78d3b-ca5a-4e72-8a24-645d141a3f5d"></a>Kopia zapasowa i przywracanie
W przypadku wdrażania SAP MaxDB do platformy Azure, należy przejrzeć z metody tworzenia kopii zapasowej. Nawet jeśli system nie jest systemów produkcyjnych, bazy danych SAP obsługiwanych przez SAP MaxDB musi zapasową okresowo. Ponieważ usługa Azure Storage chroni trzy obrazy, kopia zapasowa jest teraz mniej ważne w zakresie ochrony systemu przed błąd magazynu i ważniejsze awariami operacyjne lub administracyjnych. Główną przyczyną utrzymywania odpowiednich kopii zapasowej i przywracania plan jest tak, aby można kompensowane błędy logiczne, czy ręcznie, zapewniając możliwości punktu w czasie odzyskiwania. Celem jest więc użyć kopii zapasowych do przywrócenia bazy danych do niektórych punktu w czasie lub na potrzeby kopii zapasowych w usłudze Azure inicjatora innego systemu przez skopiowanie istniejącej bazy danych. Na przykład można przeniesiesz z konfiguracji SAP warstwy 2 do 3-warstwowej systemu BIOS tego samego systemu przez Przywracanie kopii zapasowej.

Wykonywanie kopii zapasowych i przywracanie bazy danych na platformie Azure działa tak samo jak w przypadku systemów lokalnych, dzięki czemu można używać standardowych narzędzi wykonywania kopii zapasowej i przywracania SAP MaxDB, które zostały opisane w jednym z dokumentów dokumentacji SAP MaxDB SAP Uwaga na liście [767598].

#### <a name="77cd2fbb-307e-4cbf-a65f-745553f72d2c"></a>Zagadnienia dotyczące wydajności tworzenia kopii zapasowych i przywracania
Jak wdrożenia bez systemu operacyjnego wydajności tworzenia kopii zapasowej i przywracania jest zależna od liczby woluminy mogą być odczytywane w równolegle i przepływność tych woluminów. Ponadto zużycie procesora CPU kompresja kopii zapasowej można odtworzyć istotną rolę na maszynach wirtualnych z maksymalnie 8 wątków na Procesor. W związku z tym co można założyć:

* Mniejsza liczba wirtualnych dysków twardych używany do przechowywania urządzenia bazy danych, niższa ogólną przepustowość odczytu
* Im mniejsza liczba CPU wątki w maszynie Wirtualnej, bardziej rygorystycznych wpływ kompresja kopii zapasowej
* Mniej elementów docelowych (Stripe katalogów, wirtualne dyski twarde), można zapisać kopii zapasowej do niższej przepływności

Aby zwiększyć liczbę elementów docelowych do zapisu, istnieją dwie opcje, których można, prawdopodobnie w połączeniu, w zależności od potrzeb:

* Przypisywanie oddzielnych woluminach kopii zapasowej
* Stosowanie wolumin docelowy kopii zapasowej za pośrednictwem wielu wirtualnych dysków twardych zainstalowanych w celu poprawienia przepływności IOPS na wolumin na dysku rozłożonego
* O oddzielnych dedykowanych dysku logicznego urządzeń:
  * SAP MaxDB woluminach kopii zapasowej (tj. pliki)
  * SAP MaxDB woluminy danych (np. pliki)
  * SAP woluminy dziennika MaxDB (np. pliki)

Stosowanie woluminu przez kilka zainstalowanych dysków VHD został omówiony wcześniej w rozdziale [RAID oprogramowania] [ dbms-guide-2.2] tego dokumentu.

#### <a name="f77c1436-9ad8-44fb-a331-8671342de818"></a>Inne
Wszystkie inne tematy ogólne takich jak monitorowanie zestawami dostępności Azure lub SAP mają również zastosowanie, zgodnie z opisem w pierwszych trzech rozdziałach tego dokumentu w przypadku wdrożeń maszyn wirtualnych z bazy danych SAP MaxDB.
Inne ustawienia specyficzne dla programu SAP MaxDB są niewidoczne dla maszyn wirtualnych platformy Azure i są opisane w różnych dokumentach wymienionych w Uwaga SAP [767598] w te informacje SAP:

* [826037]
* [1139904]
* [1173395]

## <a name="specifics-for-sap-livecache-on-windows"></a>Charakterystyka liveCache SAP w systemie Windows
### <a name="sap-livecache-version-support"></a>LiveCache SAP Obsługa wersji
Minimalną wersję liveCache SAP obsługiwane w maszynach wirtualnych platformy Azure jest **SAP LC/LCAPPS 10.0 SP 25** tym **liveCache 7.9.08.31** i **25 Znajdowania kompilacji**, wydane dla **EhP 2 dla programu SAP SCM 7.0** i wyższych.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-livecache-dbms"></a>Obsługiwane typy wersji systemu Windows firmy Microsoft i maszyny Wirtualnej platformy Azure dla programu SAP liveCache DBMS
Aby znaleźć obsługiwanej wersji programu Microsoft Windows liveCache SAP na platformie Azure, zobacz:

* [Macierz dostępności produktu SAP (PAM)][sap-pam]
* Uwaga SAP [1928533]

Zdecydowanie zaleca się przy użyciu najnowszej wersji systemu operacyjnego Microsoft Windows, który jest Microsoft Windows 2012 R2.

### <a name="sap-livecache-configuration-guidelines-for-sap-installations-in-azure-vms"></a>LiveCache SAP wskazówki dotyczące konfigurowania dla instalacji programu SAP w maszynach wirtualnych platformy Azure
#### <a name="recommended-azure-vm-types"></a>Zalecane typy maszyna wirtualna platformy Azure
Jak SAP liveCache jest aplikacja, która wykonuje obliczenia ogromny, ilość i szybkość pamięci RAM i procesora CPU ma poważny wpływ na wydajność liveCache SAP.

Dla typów maszyny Wirtualnej platformy Azure obsługiwane przez SAP (Uwaga SAP [1928533]), wszystkie wirtualne zasobów procesora CPU przydzielonych do maszyny Wirtualnej bazują na dedykowany fizycznych zasobów procesora CPU funkcji hypervisor. Nie wymaga (i w związku z tym nie konkurowanie o zasoby procesora CPU) ma miejsce.

Podobnie dla wszystkich typów wystąpienie maszyny Wirtualnej platformy Azure obsługiwane przez SAP, pamięci maszyny Wirtualnej jest 100% mapowane w pamięci fizycznej — na przykład nadmiarowe Inicjowanie obsługi administracyjnej (nadmierne zobowiązania), nie jest używany.

Z tą perspektywą zaleca użycie nowego typu D-series lub maszyny Wirtualnej platformy Azure: seria DS (w połączeniu z usługą Azure Premium Storage), mają 60% procesory szybsze niż A-series. Dla najwyższej obciążenie Procesora i pamięci RAM służy serii G i GS-series (w połączeniu z usługą Azure Premium Storage), maszynach wirtualnych z najnowszą rodziny v3 E5 procesor Intel Xeon®, która ma dwa razy pamięci i cztery razy półprzewodnikowych dysku magazynu (SSD) D/DS-serii.

#### <a name="storage-configuration"></a>Konfiguracja magazynu
Jak SAP liveCache jest oparty na technologii SAP MaxDB, magazynu Azure najlepsze praktyki zaleceń wymienionych w rozdziale SAP MaxDB [konfiguracji magazynu] [ dbms-guide-8.4.1] również są prawidłowe dla SAP liveCache.

#### <a name="dedicated-azure-vm-for-livecache"></a>Dedykowane maszyny Wirtualnej platformy Azure dla liveCache
Jak SAP liveCache intensywnie korzysta z moc obliczeniową, do użytku produkcyjnego zaleca można wdrożyć na dedykowanych maszynie wirtualnej platformy Azure.

![Dedykowane maszyny Wirtualnej platformy Azure dla liveCache dla przypadek użycia produktywności][dbms-guide-figure-700]

#### <a name="backup-and-restore"></a>Wykonywanie kopii zapasowych i przywracanie
Kopia zapasowa i przywracanie zagadnienia dotyczące wydajności, w tym już zostały opisane w odpowiednich rozdziałów SAP MaxDB [i przywracania kopii zapasowych] [ dbms-guide-8.4.2] i [zagadnienia dotyczące wydajności dla kopii zapasowej i przywrócić][dbms-guide-8.4.3].

#### <a name="other"></a>Inne
Wszystkie tematy ogólne już zostały opisane w odpowiednich MaxDB SAP [to] [ dbms-guide-8.4.4] działu.

## <a name="specifics-for-the-sap-content-server-on-windows"></a>Szczegóły serwera SAP zawartości w systemie Windows
Serwer zawartości SAP jest oddzielnym, na serwerze składników do przechowywania zawartości takiej jak elektronicznych dokumentów w różnych formatach. Serwer zawartości SAP są dostarczane przez rozwoju technologii i ma być używane różne aplikacje aplikacje SAP. Jest instalowana w oddzielnym systemie. Typowy zawartość jest materiałów szkoleniowych i dokumentacji z magazynu wiedzy lub rysunki techniczne pochodzące z mySAP System zarządzania dokumentami elementu.

### <a name="sap-content-server-version-support"></a>Obsługa wersji zawartości serwera SAP
SAP obecnie obsługuje:

* **Serwer zawartości SAP** z wersją **6.50 (lub nowszy)**
* **MaxDB SAP wersji 7,9**
* **Microsoft IIS (Internet Information Server) w wersji 8.0 (i nowsze)**

Zdecydowanie zaleca się przy użyciu najnowszej wersji serwera zawartości SAP, które w momencie pisania tego dokumentu jest **6.50 SP4**oraz najnowszej wersji **Microsoft IIS 8.5**.

Sprawdź najnowsze obsługiwanych wersjach programu SAP serwera zawartości i Microsoft IIS w [SAP produktu dostępności macierzy (PAM)][sap-pam].

### <a name="supported-microsoft-windows-and-azure-vm-types-for-sap-content-server"></a>Obsługiwane typy Microsoft Windows i maszyny Wirtualnej platformy Azure dla serwera zawartości SAP
Aby dowiedzieć się, wersji systemu Windows dla serwera zawartości SAP na platformie Azure, zobacz:

* [Macierz dostępności produktu SAP (PAM)][sap-pam]
* Uwaga SAP [1928533]

Zdecydowanie zaleca się używać najnowszej wersji systemu Microsoft Windows, które w momencie pisania tego dokumentu jest **systemu Windows Server 2012 R2**.

### <a name="sap-content-server-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Wskazówki dotyczące konfigurowania serwera zawartości SAP SAP instalacji na maszynach wirtualnych platformy Azure
#### <a name="storage-configuration"></a>Konfiguracja magazynu
Jeśli skonfigurujesz serwer zawartości SAP do przechowywania plików w bazie danych SAP MaxDB wszystkie usługi Azure storage najlepszych rozwiązań zaleceń wymienionych w rozdziale SAP MaxDB [konfiguracji magazynu] [ dbms-guide-8.4.1] również są prawidłowe w scenariuszu SAP serwera zawartości.

Jeśli skonfigurujesz serwer zawartości SAP do przechowywania plików w systemie plików, zalecane jest Użyj dedykowanego dysku logicznego. Przy użyciu funkcji miejsca do magazynowania umożliwia także zwiększyć rozmiar dysku logicznego i przepływność IOPS, zgodnie z opisem w w rozdziale [RAID oprogramowania][dbms-guide-2.2].

#### <a name="sap-content-server-location"></a>Lokalizacja zawartości serwera SAP
Serwer zawartości SAP ma zostać wdrożony w tym samym regionie Azure i sieć Wirtualną Azure, w którym jest wdrażany SAP system. Mogą zdecydować, czy chcesz wdrożyć składniki serwera zawartości SAP na dedykowany maszyny Wirtualnej platformy Azure lub w tej samej maszyny Wirtualnej, którym jest uruchomiona systemie SAP.

![Maszyna wirtualna platformy Azure w wersji dedykowanej dla serwera zawartości SAP][dbms-guide-figure-800]

#### <a name="sap-cache-server-location"></a>Lokalizacja serwera SAP pamięci podręcznej
SAP serwera pamięci podręcznej jest dodatkowe składnikiem zapewnianie dostępu do dokumentów (buforowaną) lokalnie na serwerze. Serwer pamięci podręcznej SAP buforuje dokumenty SAP serwera zawartości. To optymalizacji ruchu sieciowego, jeśli dokumenty mają zostać pobrane więcej niż jeden raz z różnych lokalizacji. Ogólną zasadą jest, że serwera SAP pamięci podręcznej musi być fizycznie bliski klienta, który uzyskuje dostęp do serwera SAP pamięci podręcznej.

Poniżej dostępne są dwie opcje:

1. **Klient znajduje się w wewnętrznej bazie danych systemu SAP** Jeśli systemu SAP wewnętrznej bazy danych skonfigurowano na dostęp do zawartości serwera SAP, klient jest systemu SAP. Podczas wdrażania zarówno systemu SAP, jak i serwer zawartości SAP w tym samym regionie Azure — w tym samym centrum danych Azure — są fizycznie zbliża się wzajemnie. W związku z tym jest niepotrzebna dedykowanego serwera SAP pamięci podręcznej. Klienci SAP interfejsu użytkownika (SAP GUI lub przeglądarki sieci web) bezpośrednio uzyskać dostępu do systemu SAP, a systemu SAP pobiera dokumentów z serwera zawartości SAP.
2. **Klient jest przeglądarki sieci web lokalnie** SAP zawartości serwer można skonfigurować jako dostępne bezpośrednio z przeglądarki sieci web. W takim przypadku przeglądarki sieci web uruchomiony lokalnie — jest klient serwera zawartości SAP. W lokalnym centrum danych i centrum danych Azure są umieszczane w różnych lokalizacjach fizycznych (najlepiej blisko innych). Centrum danych lokalnych jest połączony z Azure za pomocą usługi Azure Site-to-Site VPN lub usługi ExpressRoute. Mimo że obie opcje oferują bezpiecznego połączenia sieci VPN na platformie Azure, połączenie lokacja lokacja nie oferuje SLA sieci przepustowości i opóźnień między lokalnego centrum danych i centrum danych Azure. Aby przyspieszyć dostęp do dokumentów, wykonaj jedną z następujących czynności:
   1. Zainstaluj lokalnym serwerem SAP pamięci podręcznej, Zamknij, aby przeglądarki sieci web na lokalnym (opcja [to] [ dbms-guide-900-sap-cache-server-on-premises] rysunek)
   2. Skonfiguruj Azure ExpressRoute, oferuje niezawodny i małych opóźnieniach dedykowane połączenie sieciowe między lokalnego centrum danych i centrum danych Azure.

![Możliwość zainstalowania SAP pamięci podręcznej serwera lokalnego][dbms-guide-figure-900]
<a name="642f746c-e4d4-489d-bf63-73e80177a0a8"></a>

#### <a name="backup--restore"></a>Wykonywanie kopii zapasowych i ich przywracanie
Jeśli skonfigurujesz serwer zawartości SAP do przechowywania plików w bazie danych SAP MaxDB zagadnienia dotyczące wydajności i procedury wykonywania kopii zapasowej i przywracania są już opisane w rozdziale SAP MaxDB [i przywracania kopii zapasowych] [ dbms-guide-8.4.2]i rozdział [zagadnienia dotyczące wydajności tworzenia kopii zapasowych i przywracania][dbms-guide-8.4.3].

Jeśli skonfigurujesz serwer zawartości SAP do przechowywania plików w systemie plików, jedną z opcji ma wykonać ręcznego wykonywania kopii zapasowej/przywracania struktury cały plik gdzie znajdują się dokumenty. Podobnie jak przywracania kopii zapasowej SAP MaxDB, zaleca się ma dedykowany wolumin w celu tworzenia kopii zapasowej.

#### <a name="other"></a>Inne
Inne ustawienia określonego serwera zawartości SAP są niewidoczne dla maszyn wirtualnych platformy Azure i są opisane w różnych dokumentach i SAP uwagi:

* <https://Service.SAP.com/contentserver>
* Uwaga SAP [1619726]  

## <a name="specifics-to-ibm-db2-for-luw-on-windows"></a>Szczegóły programu IBM DB2 LUW w systemie Windows
Przy użyciu systemu Microsoft Azure możesz łatwo przeprowadzić migrację istniejącej aplikacji SAP uruchomionego na IBM DB2 dla systemu Linux, UNIX i systemu Windows (LUW) do maszyn wirtualnych platformy Azure. Z programu SAP, IBM DB2 dla LUW Administratorzy i deweloperzy mogą nadal używać tej samej opracowywania i narzędzia administracyjne, które są dostępne na lokalnym.
Ogólne informacje o systemie SAP Business Suite IBM DB2 dla LUW można znaleźć w sieci społeczności SAP (SCN) na <https://scn.sap.com/community/db2-for-linux-unix-windows>.

Dodatkowe informacje i aktualizacji dotyczących SAP na bazy danych DB2 dla LUW na platformie Azure, zobacz Uwaga SAP [2233094].

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>IBM DB2 dla systemu Linux, UNIX i obsługa wersji systemu Windows
SAP na IBM DB2 dla LUW na usługi Microsoft Azure maszyny wirtualnej jest obsługiwane począwszy od wersji bazy danych DB2 10.5.

Informacje o obsługiwanych produktach SAP i typy maszyny Wirtualnej platformy Azure, można znaleźć w Uwaga SAP [1928533].

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>IBM DB2 dla systemu Linux, UNIX i wskazówki dotyczące konfigurowania systemu Windows dla programu SAP instalacji na maszynach wirtualnych platformy Azure
#### <a name="storage-configuration"></a>Konfiguracja magazynu
Wszystkie pliki bazy danych muszą być przechowywane w systemie plików NTFS, które są oparte na dyskach VHD. Te wirtualne dyski twarde są zainstalowane na maszynie Wirtualnej platformy Azure i są oparte na w magazynie obiektów BLOB Azure strony (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Dowolny dyski sieciowe lub zdalnych udziałów, takich jak następujących usług plików na platformę Azure **nie** obsługiwane dla plików bazy danych:

* <https://blogs.msdn.com/b/windowsazurestorage/Archive/2014/05/12/Introducing-Microsoft-Azure-File-Service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/Archive/2014/05/27/persisting-Connections-to-Microsoft-Azure-Files.aspx>

Jeśli używasz Azure wirtualne dyski twarde, oparte na magazyn obiektów BLOB Azure strony instrukcji zawartych w tym dokumencie w rozdziale [struktury wdrożenia RDBMS] [ dbms-guide-2] mają zastosowanie również do wdrożenia przy użyciu programu IBM DB2 LUW bazy danych.

Jak opisano wcześniej w głównej części dokumentu, przydziały na przepływność IOPS dla wirtualnych dysków twardych Azure istnieje. Dokładne przydziały są zależne od typu maszyny Wirtualnej, używane. Znajduje się lista typów maszyny Wirtualnej z przydziałami ich [tutaj][virtual-machines-sizes]

Tak długo, jak bieżący limit przydziału IOPS na dysku jest wystarczająca, istnieje możliwość zapisywania wszystkich plików bazy danych na jeden pojedynczy zainstalowanego Azure dysku VHD.

Wydajność zagadnienia również znajdują się w rozdziale "Danych bezpieczeństwa i wydajności uwagi dla bazy danych katalogi" w Przewodnikach instalacji SAP.

Alternatywnie można użyć pul magazynu systemu Windows (tylko dostępne w systemie Windows Server 2012 i nowsze) lub w rozdziale opisano rozkładanie systemu Windows dla systemu Windows 2008 R2 jako [RAID oprogramowania] [ dbms-guide-2.2] tego dokumentu Utwórz jedno urządzenie logiczne big przez wiele dysków zainstalowanych wirtualnego dysku twardego.
Dyski zawierające ścieżki magazynu bazy danych DB2 do katalogów sapdata i saptmp należy określić dysk fizyczny rozmiar sektora 512 KB. Gdy używane są pule magazynu systemu Windows, należy utworzyć pule magazynów ręcznie za pośrednictwem interfejsu wiersza polecenia za pomocą parametru "-LogicalSectorSizeDefault". Aby uzyskać więcej informacji, zobacz <https://technet.microsoft.com/library/hh848689.aspx>.

#### <a name="backuprestore"></a>Tworzenie i przywracanie kopii zapasowych
Funkcja Kopia zapasowa i przywracanie programu IBM DB2 dla LUW jest obsługiwana w taki sam sposób jak standardowe systemów operacyjnych Windows Server i funkcji Hyper-V.

Należy się upewnić, czy masz strategii tworzenia kopii zapasowej prawidłową bazę danych w miejscu.

Jak wdrożenia bez systemu operacyjnego wydajności tworzenia kopii zapasowej/przywracania zależy od mogą być odczytywane jak wiele woluminów równolegle i co można przepływność tych woluminów. Ponadto zużycie procesora CPU używanych przez kompresję kopii zapasowych może odtworzyć istotną rolę na maszynach wirtualnych z właśnie maksymalnie 8 wątków Procesora. W związku z tym co można założyć:

* Mniejsza liczba wirtualnych dysków twardych używany do przechowywania urządzenia bazy danych mniejsza ogólną przepustowość podczas odczytywania
* Im mniejsza liczba CPU wątki w maszynie Wirtualnej, bardziej rygorystycznych wpływ kompresja kopii zapasowej
* Mniej elementów docelowych (Stripe katalogów, wirtualne dyski twarde), można zapisać kopii zapasowej do niższej przepływności

Aby zwiększyć liczbę elementów docelowych do zapisu, dwie opcje można używać/łączone w zależności od potrzeb:

* Stosowanie wolumin docelowy kopii zapasowej za pośrednictwem wielu wirtualnych dysków twardych zainstalowanych w celu poprawienia przepływności IOPS na tym woluminie rozłożonego
* Przy użyciu więcej niż jeden katalog docelowy kopii zapasowej do zapisu

#### <a name="high-availability-and-disaster-recovery"></a>Wysoka dostępność i odzyskiwanie po awarii
Serwera klastrów firmy Microsoft (MSCS) nie jest obsługiwana.

Odzyskiwanie po awarii wysoką dostępność bazy danych DB2 (HADR) jest obsługiwane. Jeśli działa rozpoznawanie nazw maszyn wirtualnych w konfiguracji wysokiej dostępności, konfiguracji platformy Azure będzie różnią się od żadnej konfiguracji, które jest wykonywane lokalnie. Nie zaleca się ufać tylko rozpoznawania adresu IP.

Nie używaj replikacji geograficznej magazynu Azure. Więcej informacji można znaleźć w rozdziale [magazyn Microsoft Azure] [ dbms-guide-2.3] i rozdział [wysokiej dostępności i odzyskiwania po awarii z maszynami wirtualnymi Azure] [ dbms-guide-3].

#### <a name="other"></a>Inne
Wszystkie inne tematy ogólne jak zestawami dostępności Azure lub SAP monitorowania stosowane zgodnie z opisem w pierwszych trzech rozdziałach tego dokumentu w przypadku wdrożeń maszyn wirtualnych z programu IBM DB2 dla LUW również.

Należy także zapoznać się z rozdziałem [ogólne programu SQL Server dla programu SAP w podsumowaniu Azure][dbms-guide-5.8].
