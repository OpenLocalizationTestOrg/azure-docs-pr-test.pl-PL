---
title: "aaaSAP NetWeaver na maszynach wirtualnych Azure — przewodnik wdrażania DBMS | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: a56b8f6b3b26fa10e01a25a251a3e4a7bfc77e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sap-netweaver-on-azure-windows-virtual-machines-vms--dbms-deployment-guide"></a>SAP NetWeaver na maszynach wirtualnych Azure Windows (VM) — przewodnik wdrażania DBMS
[767598 ]:https://launchpad.support.sap.com/#/notes/767598
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
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
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

Ten przewodnik jest częścią dokumentacji hello na wdrażanie i wdrażanie oprogramowania SAP hello w systemie Microsoft Azure. Przed przeczytaniem tego przewodnika, przeczytaj hello [implementacji przewodnik planowania i][planning-guide]. W tym dokumencie opisano wdrażania hello różnych systemów zarządzania relacyjnej bazy danych (RDBMS) oraz pokrewnych produktów w połączeniu z SAP w Microsoft Azure maszynach wirtualnych (VM) przy użyciu hello infrastruktury platformy Azure jako możliwości usługi (IaaS).

Hello papieru uzupełnia hello SAP instalacji dokumentacji i notatki SAP, reprezentujące hello głównej zasobów dla instalacji i wdrożenia oprogramowania SAP na podane platformy

## <a name="general-considerations"></a>Zagadnienia ogólne
W tym rozdziale zagadnienia dotyczące uruchamiania SAP powiązanych wprowadzono systemów DBMS w maszynach wirtualnych platformy Azure. Istnieje kilka odwołań do systemów DBMS toospecific w tym rozdziale. Zamiast tego konkretnych systemów DBMS hello są obsługiwane w tym dokumencie, po tym rozdziale.

### <a name="definitions-upfront"></a>Definicje z wyprzedzeniem
W dokumencie hello używamy hello następujące warunki:

* IaaS: Infrastruktura jako usługa.
* PaaS: Platforma jako usługa.
* SaaS: Oprogramowanie jako usługa.
* Składnik programu SAP: poszczególnych SAP aplikację taką jak ECC, BW, Menedżer rozwiązania lub EP.  Składniki programu SAP może bazować na tradycyjnych technologii ABAP lub Java lub aplikacji z systemem innym niż NetWeaver na podstawie takich jak obiektów biznesowych.
* Środowisko SAP: jeden lub więcej składników programu SAP pogrupowane logicznie tooperform funkcji biznesowych programowanie, QAS, szkolenia, odzyskiwania po awarii lub produkcji.
* Poziomo SAP: Odnosi się toohello cały SAP zasobów klienta IT w orientacji poziomej. Witaj pozioma SAP obejmuje wszystkie produkcyjnych i środowiskach nieprodukcyjnych.
* Systemu SAP: hello kombinację DBMS i warstwy aplikacji, np. SAP ERP programistycznej system testowy programu SAP BW, SAP CRM produkcji systemu, itp. Azure wdrożenia, który nie jest obsługiwane w toodivide te dwie warstwy między lokalną i platformą Azure. To oznacza, że systemu SAP jest wdrożona lokalnie lub jest wdrożony na platformie Azure. Jednak można wdrożyć hello systemów pozioma SAP w Azure lub lokalnie. Można na przykład wdrożyć hello systemów programowania i testowania SAP CRM na platformie Azure, ale hello SAP CRM produkcji systemu lokalnego.
* Wdrożenie tylko w chmurze: wdrożenia, którym hello subskrypcji platformy Azure nie jest połączony za pośrednictwem lokacji do lokacji lub ExpressRoute połączenia toohello lokalną infrastrukturę sieci. Wspólne dokumentacji platformy Azure rodzaju wdrożeń opisano również jako "Tylko do chmury" wdrożeń. Maszyn wirtualnych wdrożonych w ramach tej metody są dostępne za pośrednictwem hello Internet i publiczny Internet punkty końcowe przypisanych maszyn wirtualnych toohello na platformie Azure. Witaj lokalnej usługi Active Directory (AD) i DNS nie zostanie rozszerzony tooAzure w tych typach wdrożeń. Dlatego hello maszyny wirtualne nie są częścią hello lokalnej usługi Active Directory. Uwaga: Tylko w chmurze wdrożeń, w tym dokumencie są definiowane jako zakończenie krajobrazów SAP, które jest uruchamiane wyłącznie na platformie Azure, bez rozszerzenia usługi Active Directory lub rozpoznawania nazw lokalnych do chmury publicznej. Konfiguracje tylko w chmurze nie są obsługiwane dla systemów produkcyjnych SAP lub konfiguracje, których SAP STMS lub innymi zasobami lokalnymi musi toobe używany podczas komunikacji między systemami SAP hostowane na platformie Azure i zasobów znajdującej się na lokalnym.
* Między lokalizacjami: w tym artykule opisano scenariusz, w którym maszyny wirtualne są wdrożone tooan subskrypcji Azure, która ma lokacja lokacja, obejmujący wiele lokacji lub połączenia ExpressRoute między datacenter(s) lokalne powitania i Azure. Dokumentacja wspólnych Azure rodzaju wdrożenia również są opisane jako scenariusze między lokalizacjami. Witaj połączenia hello są tooextend domenami lokalnymi, lokalnej usługi Active Directory i lokalne DNS na platformie Azure. Hello pozioma lokalnymi jest rozszerzona toohello zasobów Azure hello subskrypcji. Występuje to rozszerzenie, hello maszyn wirtualnych może być częścią domeny lokalne powitania. Użytkownicy domeny hello lokalnej domeny można uzyskać dostępu do serwerów hello i usługi można uruchamiać na tych maszynach wirtualnych (takie jak usługi systemu DBMS). Komunikację i rozpoznawania nazw między maszynami wirtualnymi wdrożone lokalnie i maszyn wirtualnych wdrożonych na platformie Azure jest możliwe. Oczekuje się tym toobe hello najczęściej scenariusza wdrażania SAP zasobów na platformie Azure. Zobacz [to] [ vpn-gateway-cross-premises-options] artykułu i [to] [ vpn-gateway-site-to-site-create] Aby uzyskać więcej informacji.

> [!NOTE]
> Między różnymi lokalizacjami wdrożeń systemów SAP, gdzie systemami SAP maszynach wirtualnych platformy Azure są członkami domeny lokalnej są obsługiwane dla systemów produkcyjnych SAP. Konfiguracje między lokalizacjami są obsługiwane w przypadku wdrażania części lub zakończyć krajobrazów SAP do platformy Azure. Nawet działają hello pełną SAP w orientacji poziomej na platformie Azure wymaga o te maszyny wirtualne są częścią domeny lokalnej i REKLAM. W wcześniejsze wersje dokumentacji hello zajmowaliśmy scenariuszy hybrydowych IT, gdzie hello termin "Hybrydowe" jest ścieżką do katalogu głównego w hello fakt, że istnieje łączność między lokalizacjami, między lokalną i platformą Azure. W tym przypadku "Hybrydowe" również oznacza, że maszyny wirtualne hello na platformie Azure są częścią hello lokalnej usługi Active Directory.
>
>

Niektóre dokumentacji firmy Microsoft opisano scenariusze między lokalizacjami nieco inaczej, szczególnie w przypadku konfiguracji HA systemu DBMS. W hello przypadku hello SAP związane z dokumentów, scenariusz hello między lokalizacjami rozpoczęcia wrzenia dół toohaving lokacja lokacja lub prywatnej (ExpressRoute) łączności i toohello fakt czy poziomo SAP hello jest rozdzielona między lokalną i platformą Azure.

### <a name="resources"></a>Zasoby
Hello są dostępne dla tematu hello wdrożenia SAP na platformie Azure następujące przewodniki:

* [SAP NetWeaver na maszynach wirtualnych Azure (maszyny wirtualne) — planowanie i przewodnik wdrażania][planning-guide]
* [SAP NetWeaver na maszynach wirtualnych Azure (maszyny wirtualne) — przewodnik wdrażania][deployment-guide]
* [SAP NetWeaver na maszynach wirtualnych platformy Azure (maszyny wirtualne) — DBMS Deployment Guide (w tym dokumencie)][dbms-guide]
* [SAP NetWeaver na maszynach wirtualnych Azure (maszyny wirtualne) — przewodnik wdrażania wysokiej dostępności][ha-guide]

Hello następujące uwagi SAP są powiązane toohello tematu SAP na platformie Azure:

| Numer | Tytuł |
| --- | --- |
| [1928533] |Aplikacje SAP na platformie Azure: typy obsługiwanych produktów i maszyny Wirtualnej Azure |
| [2015553] |SAP na platformie Microsoft Azure: obsługuje wymagania wstępne |
| [1999351] |Rozwiązywanie problemów z rozszerzonego monitorowania Azure dla programu SAP |
| [2178632] |Klucz monitorowania metryki dla SAP na platformie Microsoft Azure |
| [1409604] |Wirtualizacji w systemie Windows: rozszerzonego monitorowania |
| [2191498] |SAP w systemie Linux przy użyciu platformy Azure: rozszerzonego monitorowania |
| [2039619] |Baza danych Oracle hello aplikacje SAP przy użyciu Microsoft Azure: obsługiwane produktów i wersji |
| [2233094] |DB6: Aplikacje SAP na platformie Azure przy użyciu programu IBM DB2 dla systemu Linux, UNIX i systemu Windows — informacje dodatkowe |
| [2243692] |Linux w systemie Microsoft Azure (IaaS) maszyny Wirtualnej: problemów licencji SAP |
| [1984787] |Systemu SUSE LINUX Enterprise Server 12: Informacje o instalacji |
| [2002167] |Red Hat Enterprise Linux 7.x: instalacji i uaktualniania |

Przeczytaj również hello [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) zawierający wszystkie notatki SAP dla systemu Linux.

Należy mieć praktyczną wiedzę o hello architektury Microsoft Azure oraz jak wdrożyć i obsługiwane maszyny wirtualne Microsoft Azure. W tym miejscu więcej informacji można znaleźć <https://azure.microsoft.com/documentation/>

> [!NOTE]
> Możemy **nie** dyskutować platformy Microsoft Azure jako usługa (PaaS) oferty hello platformy Microsoft Azure. Ten dokument jest o uruchamianiu systemu zarządzania bazami (danych DBMS) w Microsoft Azure maszyn wirtualnych (IaaS) tak samo, jak hello DBMS może działać w środowisku lokalnym. Funkcje bazy danych i funkcji między te dwie oferty bardzo różnią się i nie może być mieszane ze sobą. Zobacz też: <https://azure.microsoft.com/services/sql-database/>
>
>

Ponieważ firma Microsoft dyskusji IaaS, ogólnie hello systemu Windows, Linux i DBMS instalacji i konfiguracji są zasadniczo hello taki sam jak dowolnej maszyny wirtualnej lub systemu od zera kompletnego stanu maszyny będą instalowane lokalnie. Istnieją jednak niektóre architekturę i system zarządzania implementacji decyzji, które będzie różna w przypadku używania IaaS. Witaj celem niniejszego dokumentu jest tooexplain hello określonej architektury i system zarządzania różnice, które muszą być przygotowane, dla przy użyciu IaaS.

Ogólnie rzecz biorąc hello ogólną różnicy, która będzie omawiać w tym dokumencie kwestie:

* Planowanie hello prawidłowego maszyny Wirtualnej/VHD układ tooensure systemów SAP ma hello odpowiednie dane pliku układu i można osiągnąć za mało IOPS dla obciążenia.
* Zagadnienia dotyczące sieci przy użyciu IaaS.
* Toouse funkcji określonej bazy danych w kolejności toooptimize hello bazy danych układu.
* Zagadnienia i przywracania kopii zapasowej w IaaS.
* Przy użyciu różnych typów obrazów na potrzeby wdrożenia.
* Wysoka dostępność IaaS platformy Azure.

## <a name="65fa79d6-a85f-47ee-890b-22e794f51a64"></a>Struktura RDBMS wdrożenia
W kolejności należy wykonać w tym rozdziale, jest konieczne toounderstand co został przedstawiony w [to] [ deployment-guide-3] rozdział hello [Deployment Guide][deployment-guide]. Wiedza na temat hello innej serii maszyn wirtualnych i ich różnice i różnice Azure standardowe i Magazyn w warstwie Premium powinien rozumieć i znane przed przeczytaniem tego rozdziału.

Do marca 2015 Azure wirtualne dyski twarde, które zawierają system operacyjny były ograniczone too127 GB rozmiar. To ograniczenie otrzymano zniesienia w marca 2015 roku (Aby uzyskać więcej informacji Sprawdź <https://azure.microsoft.com/blog/2015/03/25/azure-vm-os-drive-limit-octupled/> ). Z tego miejsca na dyskach VHD zawierającego system operacyjny hello może mieć hello sam rozmiar jako dowolny dysk VHD. Niemniej jednak firma Microsoft nadal preferowane jest strukturą wdrożenia, którym hello systemu operacyjnego, system DBMS i ostatecznego SAP pliki binarne są niezależne od hello pliki bazy danych. W związku z tym oczekujemy SAP systemami w maszynach wirtualnych platformy Azure będzie mieć hello podstawowej maszyny Wirtualnej (lub dysku VHD) zainstalowanych z systemem operacyjnym hello bazy danych zarządzania system plików wykonywalnych i plików wykonywalnych SAP. Hello DBMS danych i pliki dziennika są przechowywane w usłudze Azure Storage (Standard lub Premium Storage) w oddzielnych plików VHD i dołączone jako dyski logiczne toohello oryginalnego Azure systemu operacyjnego obrazu maszyny Wirtualnej.

W zależności od korzystania z usługi Azure Standard lub Premium Storage (np. przy użyciu hello serii DS lub GS-series maszyn wirtualnych) są inne przydziały na platformie Azure, które są udokumentowane [tutaj][virtual-machines-sizes]. Podczas planowania Azure dyski VHD, należy toofind hello równowagę hello przydziałów dla następujących hello:

* Witaj liczby plików danych.
* Witaj liczba wirtualnych dysków twardych, które zawierają pliki hello.
* przydziały IOPS Hello pojedynczego wirtualnego dysku twardego.
* Witaj przepływność danych na dysku VHD.
* Liczba Hello dodatkowe możliwości wirtualne dyski twarde na rozmiar maszyny Wirtualnej.
* Witaj ogólne przepływności magazynu maszyny Wirtualnej może zapewnić.

Azure będzie wymuszać limit przydziału IOPS na dysku VHD. Te przydziały są różne dla wirtualne dyski twarde hostowane na usługi Azure Standard Storage i Magazyn w warstwie Premium. Czasy oczekiwania operacji We/Wy jest bardzo różnią się między dwoma typami magazynu hello z magazyn w warstwie Premium dostarczania czynniki lepsze opóźnienia we/wy. Każdego typu maszyny Wirtualnej z inną hello mają ograniczoną liczbę dysków VHD, czy stanie tooattach. Ograniczenie innego jest, że niektórych typów maszyny Wirtualnej mogą korzystać z usługi Azure Premium Storage. Oznacza to, że hello decyzja dla określonego typu maszyny Wirtualnej może nie tylko uzależniona hello Procesora i ilości pamięci, ale także hello IOPS, opóźnienia i dysku wymagania przepływności, które zwykle są skalowane hello liczby dysków VHD lub hello typu dysków Premium Storage. Szczególnie w przypadku magazyn w warstwie Premium hello rozmiar wirtualnego dysku twardego również mogą być definiowane hello liczbę IOPS i przepływność, którą musi toobe osiągnięte przez każdy z nich.

fakt Hello hello ogólną szybkość IOPS, hello liczba zainstalowanych, wirtualne dyski twarde i hello rozmiar hello maszyny Wirtualnej są wszystkie powiązane ze sobą, może spowodować konfiguracji platformy Azure toobe systemu SAP różni się od jego lokalnego wdrożenia. Hello limity liczby operacji na jednostce LUN są zwykle konfigurowane w przypadku wdrożeń lokalnych. Z usługą Azure Storage te limity są stałe, lub tak jak magazyn w warstwie Premium w zależności od typu dysku hello. Dlatego z wdrożeń lokalnych widzimy konfiguracji klienta, serwerów baz danych, które używają wielu różnych woluminach dla specjalnych plików wykonywalnych, takie jak SAP i hello DBMS lub woluminów specjalnych tymczasowej bazy danych lub tabel. Gdy system lokalny jest przeniesionego tooAzure go może prowadzić odpady tooa potencjalnych przepustowości IOPS przy tym jak zmarnowała dla plików wykonywalnych lub baz danych, których nie należy wykonywać dowolne albo nie partii iops wirtualnego dysku twardego. W związku z tym na maszynach wirtualnych Azure zaleca się tym hello system DBMS i SAP pliki wykonywalne zostanie zainstalowany na dysku hello systemu operacyjnego, jeśli to możliwe.

Witaj umieszczania hello pliki bazy danych i plików dziennika i typ hello Azure Storage używane, powinien być zdefiniowany przez wymagania dotyczące przepływności, opóźnienia i IOPS. W kolejności toohave wystarczającej liczby IOPS dla dziennika transakcji hello, może być wymuszone tooleverage wielu dysków VHD dla dziennika transakcji hello pliku lub użyj większy dysk magazyn w warstwie Premium. W takim wypadku jednego czy po prostu kompilacji z hello wirtualne dyski twarde zawierające dziennika transakcji hello oprogramowania RAID (np. Windows puli magazynu dla Windows lub MDADM i LVM (Menedżer woluminów logicznych) dla systemu Linux).

- - -
> ![Windows][Logo_Windows] Windows
>
> Dysku D:\ w maszynie Wirtualnej platformy Azure jest nieutrwaloną dysku, który nie jest obsługiwana przez niektóre dyski lokalne powitania węzła obliczeń platformy Azure. Ponieważ nietrwałe, oznacza to, że zawartości toohello wszelkie zmiany wprowadzone na dysku D:\ hello ma utracone po ponownym uruchomieniu hello maszyny Wirtualnej. "Wszystkie zmiany" Firma Microsoft oznacza zapisane pliki, katalogi utworzone, zainstalowane aplikacje itd.
>
> ![Linux][Logo_Linux] Linux
>
> Maszyny wirtualne systemu Linux platformy Azure automatycznie zainstalować dysk w /mnt/resource, która jest obsługiwana przez dyski lokalne w węźle obliczeń platformy Azure hello dysku nietrwałe. Nietrwałe, dlatego oznacza to, że toocontent wszelkie zmiany wprowadzone w /mnt/resource jest tracona po ponownym uruchomieniu hello maszyny Wirtualnej. Wszelkie zmiany firma Microsoft oznacza zapisywane pliki, katalogi utworzone, zainstalowane aplikacje itd.
>
>

- - -
Zależne od hello Azure serii maszyn wirtualnych, dyski lokalne powitania na powitania obliczeniowe węzła Pokaż różne działania, które mogą zostać podzielone, takich jak:

* A0 A7: Bardzo ograniczony wydajności. Nie można używać do wszelkich innych niż plik stronicowania systemu windows
* A8 A11: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > przepustowości 1GB/s
* D-Series: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > przepustowości 1GB/s
* Seria DS: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > przepustowości 1GB/s
* Seria G: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > przepustowości 1GB/s
* GS-Series: Charakterystyki wydajności bardzo dobre z niektórych IOPS dziesięć tysięcy i > przepustowości 1GB/s

Instrukcje powyżej jest stosowane toohello wirtualna typy, które są certyfikowane z programu SAP. Hello serii maszyn wirtualnych z doskonałym IOPS i przepływności kwalifikować się do korzystanie przez niektóre funkcje systemu DBMS, takie jak bazy danych tempdb lub miejsce tabeli tymczasowej.

### <a name="c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f"></a>Buforowanie maszyny wirtualne i wirtualne dyski twarde
Tworząc tych dysków/dysków VHD za pomocą portalu hello lub gdy firma Microsoft instalacji przekazane tooVMs wirtualne dyski twarde, firma Microsoft można wybrać, czy ruch hello We/Wy między hello maszyny Wirtualnej, a te wirtualne dyski twarde znajduje się w magazynie Azure są buforowane. Azure Standard i Premium Storage należy użyć dwóch różnych technologii dla tego typu pamięci podręcznej. W obu przypadkach hello pamięci podręcznej samego dysku kopie na powitania używać tego samego dysków przez hello tymczasowego dysku (D:\ w systemie Windows) lub /mnt/resource w systemie Linux hello maszyny Wirtualnej.

Dla usługi Azure Standard Storage hello pamięci podręcznej możliwe typy to:

* Bez buforowania
* Buforowania zapisu
* Odczyt i zapis buforowanie

Kolejność tooget spójne i deterministyczna wydajności, należy ustawić hello buforowanie na usługi Azure Standard Storage dla wszystkich dysków VHD zawierającego **DBMS powiązanych plików danych, plików dziennika i too'NONE miejsca tabeli '**. buforowanie Hello hello maszyny Wirtualnej może pozostać przy hello domyślnego.

Dla usługi Azure Premium Storage istnieje hello następujące opcje buforowania:

* Bez buforowania
* Buforowania zapisu

Zalecenia dotyczące usługi Azure Premium Storage jest tooleverage **buforowanie plików danych do odczytu** bazy danych SAP hello i wybrać **bez buforowania hello VHD(s) pliki dziennika**.

### <a name="c8e566f9-21b7-4457-9f7f-126036971a91"></a>Oprogramowaniem RAID
Jak już wspomniano powyżej konieczne będzie toobalance hello liczbę IOPS potrzebne hello plików bazy danych przez liczbę hello wirtualne dyski twarde można skonfigurować i hello maksymalna liczba IOPS dla wirtualnego dysku twardego lub magazyn w warstwie Premium zapewnia maszynie Wirtualnej platformy Azure typ dysku. Najprostszym sposobem toodeal z powitalne IOPS obciążenia za pośrednictwem wirtualnych dysków twardych jest toobuild oprogramowaniem RAID za pośrednictwem hello różnych wirtualne dyski twarde. Następnie należy umieścić liczbę plików danych hello SAP DBMS na powitalne jednostek LUN używać poza hello oprogramowaniem RAID. Zależne od wymagań hello tooconsider hello użycie magazyn w warstwie Premium również może być od dwóch hello trzy różne dyski magazyn w warstwie Premium zapewniają wyższy przydziału IOPS niż dyski VHD w oparciu magazynu w warstwie standardowa. Oprócz hello znaczących lepiej opóźnienia We/Wy są udostępniane przez usługi Azure Premium Storage.

Dotyczy to również dziennika transakcji toohello hello różnych systemów systemu DBMS. Z dużą ilością je tylko dodanie większej liczby plików Tlog nie pomocy, ponieważ systemy DBMS hello zapis do jednego z plików hello naraz tylko. Razie IOPS większe niż pojedynczy standardowy magazyn na podstawie wirtualnego dysku twardego można dostarczać, można paskowych za pośrednictwem wielu dysków VHD standardowe magazynu lub można użyć typu większy dysk magazyn w warstwie Premium, oferującym poza większe IOPS również czynniki mniejsze opóźnienia do zapisu hello I / System operacyjny na powitania dziennika transakcji.

Sytuacje wystąpił we wdrożeniach systemu Azure, które favor, przy użyciu oprogramowania są RAID:

* Dziennik transakcji dziennika/ponów wymagają IOPS więcej niż platforma Azure oferuje dla pojedynczego dysku VHD. Jak napisano powyżej, to będzie możliwe tworzenie jednostki LUN za pośrednictwem wielu dysków VHD za pomocą oprogramowania RAID.
* Nierówna we/wy rozkład obciążenia za pośrednictwem hello plików danych bazy danych SAP hello. W takich przypadkach jedną występować jeden plik danych zamiast często naciśnięcie hello przydziału. Podczas gdy inne pliki danych nie otrzymują nawet przydziału IOPS Zamknij toohello jednego wirtualnego dysku twardego. W takich przypadkach hello najlepszym rozwiązaniem jest toobuild jednej jednostki LUN za pośrednictwem wielu dysków VHD za pomocą oprogramowania RAID.
* Nie znasz dokładnego obciążenia We/Wy jakie hello na plik danych jest i tylko około wiedzieć, jaki hello ogólne IOPS obciążenie przed hello DBMS jest. Najprostszym toodo jest toobuild Pomoc dla jednej jednostki LUN z hello oprogramowania RAID. Suma Hello przydziały wielu dysków VHD za tej jednostki LUN należy następnie spełnienia hello znane IOPS szybkości.

- - -
> ![Windows][Logo_Windows] Windows
>
> Zalecane jest użycie systemu Windows Server 2012 lub nowszej miejsca do magazynowania, ponieważ jest bardziej efektywne niż rozkładanie systemu Windows starszych wersji systemu Windows. Należy pamiętać, że konieczne może hello toocreate Windows pul magazynów i miejsc do magazynowania za pomocą poleceń programu PowerShell w przypadku używania systemu Windows Server 2012 jako systemu operacyjnego. Witaj poleceń programu PowerShell można znaleźć tutaj <https://technet.microsoft.com/library/jj851254.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> Tylko MDADM i LVM (logiczne menedżera woluminu) są obsługiwane toobuild oprogramowania RAID w systemie Linux. Aby uzyskać więcej informacji przeczytaj hello następujące artykuły:
>
> * [Należy skonfigurować oprogramowanie RAID w systemie Linux] [ virtual-machines-linux-configure-raid] (dla MDADM)
> * [Skonfiguruj LVM na Maszynę wirtualną systemu Linux na platformie Azure][virtual-machines-linux-configure-lvm]
>
>

- - -
Uwagi dotyczące korzystania z serii maszyn wirtualnych, które są zazwyczaj stanie toowork usługa Azure Premium Storage są:

* Wymagania dla opóźnienia we/wy, które są Zamknij dostarczyć urządzenia SAN/NAS toowhat.
* Żądanie dla czynniki lepsze opóźnienia we/wy niż zapewnia usługi Azure Standard Storage.
* Wyższa wartość IOPS dla maszyny Wirtualnej niż to, co może zostać osiągnięty przy wielu standardowe magazynu wirtualnych dysków twardych dla określonego typu maszyny Wirtualnej.

Od hello podstawowej usługi Azure Storage replikuje poszczególnych węzłów magazynu wirtualnego dysku twardego tooat co najmniej trzy proste RAID 0, zastosowanie rozkładania mogą być używane. Nie ma żadnych tooimplement potrzeby RAID5 lub RAID1.

### <a name="10b041ef-c177-498a-93ed-44b3441ab152"></a>Magazyn Microsoft Azure
Microsoft, które będą przechowywać magazynu Azure hello podstawowej maszyny Wirtualnej (z systemem operacyjnym) i wirtualnych dysków twardych lub obiekty BLOB węzłów magazynu oddzielnych tooat co najmniej 3. Podczas tworzenia konta magazynu, istnieje możliwość wyboru ochrony w sposób pokazany poniżej:

![Replikacja geograficzna włączone dla konta magazynu Azure][dbms-guide-figure-100]

Replikacja usługi Azure Storage lokalnego (magazyn lokalnie nadmiarowy) zapewnia poziom ochrony przed utratą danych ze względu na błąd tooinfrastructure czy kilku klientów może pozwolić sobie toodeploy. Jak pokazano powyżej, że istnieją różne opcje 4 piąty jest odmianą jednego hello pierwsze trzy. Wyszukiwanie bliżej ich firma Microsoft może odróżnić:

* **Premium lokalnie nadmiarowego magazynu (LRS)**: Usługa Azure Premium Storage oferuje obsługę wysokiej wydajności i małych opóźnieniach dysku dla maszyn wirtualnych uruchomionych/O wykonujących obciążeń. Istnieją 3 repliki danych hello w hello centrum danych Azure tego samego regionu platformy Azure. Witaj kopie będą znajdować się w różnych usterek i domen uaktualnienia (pojęć można znaleźć [to] [ planning-guide-3.2] rozdziału w hello [Planning Guide][planning-guide]). W przypadku repliki hello danych wychodzących z usługi awarii węzła magazynu tooa lub awarii dysku nowej repliki jest generowany automatycznie.
* **Lokalnie nadmiarowego magazynu (LRS)**: W tym przypadku istnieją 3 repliki danych hello w hello centrum danych Azure tego samego regionu platformy Azure. Witaj kopie będą znajdować się w różnych usterek i domen uaktualnienia (pojęć można znaleźć [to] [ planning-guide-3.2] rozdziału w hello [Planning Guide][planning-guide]). W przypadku repliki hello danych wychodzących z usługi awarii węzła magazynu tooa lub awarii dysku nowej repliki jest generowany automatycznie.
* **Z magazynu geograficznie nadmiarowego magazynu (GRS)**: W tym przypadku jest asynchroniczne replikacji, który będzie dostarczyć dodatkowe 3 repliki hello danych w innym regionie Azure, która jest w większości przypadków hello w hello tym samym regionie geograficznym (na przykład, a Europa Północna, Europa Zachodnia Europa). To spowoduje 3 dodatkowych replik, pozwoli to 6 replik w sumie. Odmiana to jest dodanie gdzie hello danych w regionie Azure zreplikowanych geograficznie hello może służyć do celów odczytu (dostęp do odczytu z magazynu geograficznie nadmiarowego).
* **Magazyn geograficznie nadmiarowy (ZRS) strefy**: W tym przypadku repliki hello 3 hello dane pozostają w hello tym samym regionie Azure. Zgodnie z objaśnieniem w [to] [ planning-guide-3.1] rozdział hello [Planning Guide] [ planning-guide] region platformy Azure może być liczbą centrów danych w pobliżu. W przypadku hello LRS replik hello czy rozłożone hello różnych centrach danych, że jeden region platformy Azure.

Więcej informacji można znaleźć [tutaj][storage-redundancy].

> [!NOTE]
> W przypadku wdrożeń systemu DBMS hello użycie magazynu geograficznie nadmiarowego magazynu nie jest zalecane
>
> Azure magazynu — replikacja geograficzna jest asynchroniczne. Replikacja poszczególne wirtualne dyski twarde zainstalowanego tooa jednej maszyny Wirtualnej nie są zsynchronizowane w kroku blokady. W związku z tym nie jest odpowiedni tooreplicate DBMS pliki, które są dystrybuowane za pośrednictwem różnych dysków VHD lub wdrożyć przed oprogramowaniem RAID oparte na wielu dysków VHD. Oprogramowanie systemu DBMS wymaga, że magazyn dyskowy trwałe hello dokładnie synchronizację różnych jednostek LUN i podstawowych dysków/wirtualne dyski twarde/jednostkami. Oprogramowanie system DBMS używa różnych toosequence mechanizmów działania zapisu We/Wy i DBMS zgłasza, że magazyn dyskowy hello celem replikacji hello jest uszkodzony, jeśli różnią się one nawet przez kilka milisekund. Dlatego jeśli jedną naprawdę oczekuje, że baza danych konfiguracji z bazą danych rozciągnięty w wielu dysków VHD replikacją geograficzną, takie replikacji musi toobe przeprowadzane przy użyciu środków bazy danych i funkcji. Jeden nie miały tooperform replikacji geograficznej magazynu Azure to zadanie.
>
> Hello problem jest najprostsza tooexplain systemu przykład. Załóżmy, że masz systemu SAP przekazany do platformy Azure, którego 8 wirtualne dyski twarde zawierające pliki danych hello DBMS plus jeden wirtualny dysk twardy zawierający hello plik dziennika transakcji. Każdej z nich te 9 wirtualne dyski twarde mają danymi zapisywanymi toothem w spójny sposób zgodnie z toohello DBMS, czy dane hello są zapisywane pliki dziennika toohello danych lub transakcji.
>
> W kolejności tooproperly geograficznie replicate hello danych i obsługa obraz spójności bazy danych, zawartość hello wszystkich dysków VHD dziewięć będzie mieć toobe replikacją geograficzną w operacjach hello we/wy dokładnej kolejności hello zostały wykonane przed hello dziewięć różnych wirtualne dyski twarde. Jednak replikacja geograficzna usługi Azure Storage nie zezwala na toodeclare zależności między wirtualne dyski twarde. Oznacza to, że replikacja geograficzna usługi Magazyn Microsoft Azure nie ma informacji dotyczących hello na fakt, że zawartość hello w tych dziewięć różne dyski VHD są inne pokrewne tooeach i hello zmiany danych są zgodne tylko wtedy, gdy replikowanie w operacji We/Wy hello kolejności hello wystąpił we wszystkich hello 9 wirtualne dyski twarde.
>
> Oprócz jest wysoka, że hello replikacją geograficzną obrazów w scenariuszu hello nie udostępniają obrazu spójności bazy danych, również jest zmniejszenie wydajności pokazywany z geograficznie nadmiarowego magazynu, który może spowodować poważne ryzyko wpływ na wydajność. W podsumowaniu nie należy używać tego typu nadmiarowość magazynu dla obciążeń typu systemu DBMS.
>
>

#### <a name="mapping-vhds-into-azure-virtual-machine-service-storage-accounts"></a>Mapowanie wirtualne dyski twarde do kont magazynu usługi Azure maszyny wirtualnej
Konto magazynu platformy Azure jest nie tylko konstrukcję administracyjne, ale również temat ograniczenia. Podczas gdy ograniczenia hello różnią się od tego, czy omawianiu standardowe konto magazynu platformy Azure lub konta usługi Azure Premium Storage. wymieniono Hello dokładne możliwości i ograniczeń [tutaj][storage-scalability-targets]

Dlatego dla usługi Azure Standard Storage jest ważne toonote na powitania IOPS na konto magazynu istnieje limit (wiersz zawierający "Całkowita liczba żądań" w [artykułu hello][storage-scalability-targets]). Ponadto jest początkowej limit 100 kont magazynu dla subskrypcji platformy Azure (lub nowszym lipca 2015). W związku z tym zaleca toobalance IOPS maszyn wirtualnych między wiele kont magazynu przy użyciu usługi Azure Standard Storage. Podczas gdy jeden maszyna wirtualna używa najlepiej jedno konto magazynu, jeśli to możliwe. Dlatego jeśli omawianiu DBMS wdrożeń, gdzie każdego wirtualnego dysku twardego, który znajduje się na usługi Azure Standard Storage można osiągnąć limitu przydziału należy wdrażać tylko 30-40 wirtualne dyski twarde na konto magazynu Azure, która używa usługi Azure Standard Storage. Na powitania drugiej strony, jeśli korzystać z usługi Azure Premium Storage, a toostore bazy danych dużych woluminów, być może przeprowadzać pod względem IOPS. Jednak konto magazynu Azure Premium jest sposób bardziej restrykcyjne w woluminie danych niż standardowe konta magazynu platformy Azure. W związku z tym można wdrażać tylko w ograniczonej liczby wirtualnych dysków twardych w ramach konta usługi Azure Premium Storage przed szukaniem hello danych woluminu limit. Na powitania zakończenia Pomyśl o konta magazynu platformy Azure jako "Wirtualną sieć SAN", który ma ograniczone możliwości w IOPS i/lub pojemności. W związku z tym hello zadanie pozostanie, tak jak wdrożeń lokalnych, układ hello toodefine hello dysków VHD hello różnych systemów SAP za pośrednictwem hello różnych "urojony SAN urządzenia" lub konta magazynu Azure.

Dla usługi Azure Standard Storage nie jest zalecane toopresent magazynu z innego magazynu kont tooa pojedynczy maszyny Wirtualnej, jeśli to możliwe.

Przy użyciu hello DS lub GS-serii maszyn wirtualnych platformy Azure jest możliwe toomount wirtualne dyski twarde poza standardowe konta magazynu Azure i kont magazynu w warstwie Premium. Przypadki użycia, takie jak zapisywanie kopii zapasowych do magazynu w warstwie standardowa kopie wirtualne dyski twarde, natomiast o DBMS danych i pliki dziennika na magazyn w warstwie Premium pochodzić toomind którym takie magazyn heterogeniczny można skorzystać.

Na podstawie wdrożeń klienta i testowania too40 około 30, które wirtualne dyski twarde zawierające pliki danych bazy danych i pliki dziennika można udostępnić w jednej Azure standardowe konto magazynu z akceptowalną wydajność. Jak wspomniano wcześniej, ograniczenie hello konto magazynu Azure Premium jest prawdopodobnie toobe hello danych pojemności, które może przechowywać go i nie IOPS.

Z sieci SAN urządzeniami lokalnymi, udostępnianie wymaga monitorowania tooeventually kolejności wykrywania wąskich gardeł na konto magazynu platformy Azure. Hello Azure rozszerzenie monitorowania dla programu SAP i hello portalu Azure są narzędzia, które mogą być używane toodetect zajęty konta magazynu Azure, która może być dostarczanie nieoptymalne wydajność We/Wy.  Jeśli ta sytuacja jest wykrył, że zalecane jest zajęty toomove tooanother maszyn wirtualnych konta magazynu Azure. Zobacz toohello [Deployment Guide] [ deployment-guide] szczegółowe informacje na temat sposobu tooactivate hello SAP hosta możliwości monitorowania.

Inny artykuł podsumowania najlepsze rozwiązania dotyczące usługi Azure Standard Storage i standardowe konta magazynu Azure można znaleźć tutaj <https://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx>

#### <a name="moving-deployed-dbms-vms-from-azure-standard-storage-tooazure-premium-storage"></a>Przenoszenie wdrożone maszyny wirtualne systemu DBMS z usługi Azure Standard Storage tooAzure magazyn w warstwie Premium
Firma Microsoft wystąpić dość sytuacje, w którym jako klient ma toomove wdrożonej maszyny Wirtualnej z usługi Azure Standard Storage w usłudze Azure Premium Storage. Nie jest to możliwe bez fizycznie przeniesienie danych hello. Istnieje kilka sposobów tooachieve hello cel:

* Wszystkie wirtualne dyski twarde, podstawowy dysk VHD jak wirtualne dyski twarde danych można po prostu skopiuj do nowego konta magazynu Azure Premium. Bardzo często wybranej hello liczba wirtualnych dysków twardych w ramach usługi Azure Standard Storage nie ze względu na powitania fakt, że potrzebne hello ilość danych. Jednak potrzebne tak wielu wirtualnych dysków twardych z powodu hello IOPS. Teraz, gdy przeniesiesz magazyn w warstwie Premium można przejść z sposób tooAzure mniej tooachieve wirtualne dyski twarde hello przepływność niektórych IOPS. Biorąc pod uwagę fakt hello w usłudze Azure Storage standardowy opłacać hello użytą danych i nie rozmiar dysku nominalnego hello, hello liczba wirtualnych dysków twardych naprawdę niezależnie od tego, pod względem kosztów. Usługa Azure Premium Storage będzie płatności dla rozmiaru dysku nominalnego hello. W związku z tym większość powitania klienta spróbuj tookeep hello liczba Azure wirtualne dyski twarde w magazynie Premium na hello numer wymagane tooachieve hello IOPS przepływności niezbędne. Tak większość klientów decyzję przed hello sposób prosty 1:1 kopiowania.
* Jeśli nie został jeszcze zainstalowany, w przypadku zainstalowania jednego wirtualnego dysku twardego, zawierające kopii zapasowej bazy danych SAP bazy danych. Po utworzeniu kopii zapasowej hello Odinstaluj wszystkie wirtualne dyski twarde, łącznie z wirtualnego dysku twardego zawierającego hello hello w kopii zapasowej i kopii hello podstawowy dysk VHD i hello wirtualnego dysku twardego z kopii zapasowej hello do konta usługi Azure Premium Storage. Czy następnie wdrożyć maszyny Wirtualnej w oparciu hello podstawowy dysk VHD i instalacji hello wirtualnego dysku twardego z kopii zapasowej hello powitalne. Teraz możesz utworzyć dodatkowe puste dysków magazyn w warstwie Premium dla hello maszyny Wirtualnej, które są używane toorestore hello z bazy danych do. Przyjęto założenie, że ten hello DBMS pozwala toochange ścieżki toohello plików danych i dziennika w ramach procesu przywracania hello.
* Inną możliwością jest odmianą hello poprzedniego procesu, którym tylko kopia zapasowa hello wirtualnego dysku twardego w usłudze Azure Premium Storage i dołącz je przed Maszynami wirtualnymi, nowo wdrożone i zainstalowana.
* Witaj czwarty możliwość, że została wybrana, po osiągnięciu potrzebę toochange hello liczby plików danych bazy danych. W takim przypadku przeprowadza się przy użyciu eksportu/importu kopii jednorodnego systemu SAP. Umieść te pliki eksportu do wirtualnego dysku twardego, który jest kopiowany do konta magazynu Azure Premium i dołączenie go tooa użycie procesów importu hello toorun maszyny Wirtualnej. Klienci używać tej możliwości głównie w przypadku, gdy mają one toodecrease hello liczby plików danych.

### <a name="deployment-of-vms-for-sap-in-azure"></a>Wdrażanie maszyn wirtualnych dla programu SAP na platformie Azure
Microsoft Azure oferuje wiele sposobów toodeploy maszyn wirtualnych i skojarzone dyski. Co jest bardzo ważne toounderstand hello różnic od przygotowania hello maszyn wirtualnych może się różnić zależy sposób hello wdrożenia. Ogólnie rzecz biorąc szukamy do hello scenariuszy opisanych w powitania po rozdziałach.

#### <a name="deploying-a-vm-from-hello-azure-marketplace"></a>Wdrażanie maszyny Wirtualnej z hello Azure Marketplace
Chcesz tootake firmy Microsoft lub strona 3 podać obraz z hello Azure Marketplace toodeploy maszyny Wirtualnej. Po wdrożeniu maszyny Wirtualnej na platformie Azure, wykonaj hello tych samych wskazówek i narzędzia tooinstall hello oprogramowania SAP wewnątrz maszyny Wirtualnej w sposób jak w środowisku lokalnym. Dotyczących instalowania oprogramowania SAP hello wewnątrz hello maszyny Wirtualnej platformy Azure, SAP i Microsoft zaleca tooupload i Zapisz nośnika instalacyjnego programu SAP hello w Azure dysków VHD lub toocreate maszyny Wirtualnej platformy Azure działa jako "serwera plików", zawierający wszystkie nośnika instalacyjnego programu SAP niezbędne hello.

#### <a name="deploying-a-vm-with-a-customer-specific-generalized-image"></a>Wdrażanie maszyny Wirtualnej z uogólniony obraz określonego klienta
Powodu toospecific poprawki wymagania w zakresie tooyour systemu operacyjnego lub w wersji systemu DBMS obrazy hello podane w portalu Azure Marketplace hello może nie odpowiadają potrzebom. W związku z tym może być konieczne toocreate Maszynę wirtualną za pomocą własnych "private" obrazu systemu operacyjnego/DBMS maszyny Wirtualnej, który można wdrożyć kilka razy później. tooprepare "private" obraz do duplikacji, powitalne systemu operacyjnego musi być uogólniony na powitania lokalnej maszyny Wirtualnej. Zobacz toohello [Deployment Guide] [ deployment-guide] szczegółowe informacje na temat toogeneralize maszyny Wirtualnej.

Jeśli zainstalowano już SAP zawartości w lokalnej maszyny Wirtualnej (szczególnie w przypadku systemów warstwy 2), można dostosować ustawienia systemu SAP powitania po wdrożenie hello hello maszyny Wirtualnej platformy Azure za pomocą wystąpienia hello nazwy procedury obsługiwane przez hello rozbudowy oprogramowania SAP Menedżer (Uwaga SAP [1619720]). W przeciwnym razie można zainstalować oprogramowania SAP hello później po wdrożeniu hello hello maszyny Wirtualnej platformy Azure.

Począwszy od hello zawartości bazy danych używane przez hello SAP aplikacji możesz albo wygenerować zawartości hello świeżo przez instalację programu SAP lub można zaimportować zawartość na platformie Azure za pomocą dysku VHD z kopii zapasowej bazy danych systemu DBMS lub korzystania z możliwości hello DBMS toodirectly wykonywanie kopii zapasowej na magazyn Microsoft Azure. W takim przypadku można również przygotować dyski VHD z hello DBMS danych i dziennika lokalne pliki i zaimportować je jako dyski na platformie Azure. Ale hello transferu danych systemu DBMS, który jest ładowany z lokalnymi tooAzure będzie działać przez dysków VHD, które należy toobe przygotowane lokalnymi.

#### <a name="moving-a-vm-from-on-premises-tooazure-with-a-non-generalized-disk"></a>Przenoszenie maszyny Wirtualnej z tooAzure lokalnego przy użyciu dysku z systemem innym niż uogólniony
Planujesz toomove określonego systemu SAP z lokalnymi tooAzure (przyrostu i shift). Można przekazać hello wirtualnego dysku twardego, który zawiera hello systemu operacyjnego, hello SAP pliki binarne i ostatecznego plików binarnych systemu DBMS plus hello wirtualne dyski twarde z plików danych i dziennika hello hello DBMS tooAzure. W przeciwne tooscenario #2. powyżej zachowanie hello hostname, identyfikator SID SAP i SAP kont użytkowników w hello maszyny Wirtualnej platformy Azure, jak zostały one skonfigurowane w środowisku lokalne powitania. W związku z tym uogólnianie hello obrazu nie jest konieczne. Ten przypadek przede wszystkim zostanie zastosowana dla scenariuszy między różnymi lokalizacjami, gdzie część hello pozioma SAP jest uruchomiona lokalnie i w częściach na platformie Azure.

## <a name="871dfc27-e509-4222-9370-ab1de77021c3"></a>Wysoka dostępność i odzyskiwanie po awarii z maszynami wirtualnymi platformy Azure
Platforma Azure oferuje następujące funkcje wysokiej dostępności i odzyskiwania awaryjnego (DR), stosować toodifferent składników, których używamy dla wdrożenia SAP i DBMS hello

### <a name="vms-deployed-on-azure-nodes"></a>Maszyn wirtualnych wdrożonych w węzłach Azure
Hello platformy Azure oferuje funkcje, takie jak migracja na żywo dla wdrożonych maszyn wirtualnych. Oznacza to, czy w klastrze serwerów, na którym wdrożono Maszynę wirtualną niezbędne jest konserwacji, hello maszyna wirtualna wymaga tooget zatrzymana i uruchomiona ponownie. Na platformie Azure jest wykonywana konserwacja przy użyciu tak zwane domen uaktualnienia w ramach klastrów serwerów. Obsługiwane jest tylko jedną domenę uaktualnienia naraz. Podczas ponownego uruchamiania będzie przerwy w świadczeniu usług podczas hello zamknięcia maszyny Wirtualnej, jest wykonywana konserwacja oraz ponownego uruchomienia maszyny Wirtualnej. Większość dostawców DBMS jednak zapewnić wysoką dostępność i odzyskiwanie po awarii funkcje, których szybko uruchomi hello DBMS usług w innym węźle, jeśli węzeł podstawowy hello jest niedostępny. Witaj platformy Azure oferuje funkcje toodistribute maszyn wirtualnych, magazynu i innymi usługami Azure między tooensure domen uaktualnienia, który planowanych konserwacji lub infrastruktury błędów miałoby wpływ tylko mały podzbiór maszyn wirtualnych lub usług.  Należy dokładnie zaplanować jest możliwe tooachieve dostępności poziomy porównywalne tooon lokalnej infrastruktury.

Zestawy dostępności usługi Microsoft Azure są logiczne grupowanie maszyn wirtualnych lub usług, które zapewnia maszyn wirtualnych i innych usług rozproszonych toodifferent usterek i domen uaktualnienia w ramach klastra taki sposób, że może istnieć tylko jeden zamknięcia węzła w każdym punkcie w czasie (odczyt [to] [ virtual-machines-manage-availability] artykułu, aby uzyskać więcej informacji).

Musi on toobe skonfigurowany w celu wdrażania maszyn wirtualnych, jak pokazano poniżej:

![Definicja zestawu dostępności dla systemu DBMS HA konfiguracji][dbms-guide-figure-200]

Aby toocreate wysokiej dostępności konfiguracje wdrożeń systemu DBMS (niezależnie od hello poszczególnych DBMS HA funkcjonalność używaną), maszynach wirtualnych systemu DBMS hello musi:

* Dodaj hello toohello maszyny wirtualne Azure Virtual Network (<https://azure.microsoft.com/documentation/services/virtual-network/>)
* Witaj maszyn wirtualnych w konfiguracji wysokiej dostępności hello należy również hello tej samej podsieci. Rozpoznawanie nazw między hello różnych podsieci nie jest możliwe w przypadku wdrożeń tylko w chmurze, będzie działać tylko rozpoznawania adresu IP. Przy użyciu lokacja lokacja lub połączenia ExpressRoute, w przypadku wdrożeń między różnymi lokalizacjami, sieci z co najmniej jedną podsieć zostanie już nawiązane. Rozpoznawanie nazw zostanie wykonane zgodnie z toohello lokalne zasady AD i infrastruktury sieci.

[comment]: <> (MSSedusch TODO testu, jeśli nadal ma wartość true w usłudze ARM)

#### <a name="ip-addresses"></a>Adresy IP
Zdecydowanie zaleca toosetup hello maszyn wirtualnych wysokiej dostępności konfiguracji w taki sposób, elastyczne. Zależne od partnerów tooaddress adresy IP HA hello w konfiguracji wysokiej dostępności hello nie jest niezawodna na platformie Azure, chyba że statyczne adresy IP są używane. Istnieją dwa pojęcia "Zamknij", na platformie Azure:

* Zamknij za pomocą portalu Azure lub programu Azure PowerShell polecenia cmdlet Stop-AzureRmVM: W tym przypadku hello maszyny wirtualnej pobiera zamykania i zwalnia przydzielone. Konta platformy Azure nie zostanie obciążona dla tej maszyny Wirtualnej, umożliwia użycie magazynu hello opłat tylko hello, które będą naliczane. Jednak jeśli hello prywatnego adresu IP interfejsu sieciowego hello nie jest statyczny, zwolnieniu hello adresu IP i nie jest gwarantowana się, że ten interfejs sieciowy hello pobiera hello starego adresu IP przypisanego ponownie po ponownym uruchomieniu programu hello maszyny Wirtualnej. Wykonywanie hello wyłączony za pośrednictwem portalu Azure hello lub przez wywołanie metody Stop-AzureRmVM automatycznie spowoduje dezaktywowanie alokacji. Jeśli nie chcesz maszyna hello toodeallocat użyć Stop AzureRmVM - StayProvisioned
* Jeśli wyłączysz hello maszyny Wirtualnej z poziomu systemu operacyjnego hello maszyny Wirtualnej pobiera zamknięta i nie zwalnia przydzielony. Jednak w takim przypadku konta platformy Azure będzie nadal obciążony hello maszyny Wirtualnej, pomimo hello fakt, iż zamknięcia. W takim przypadku hello przypisania tooa adres IP hello zatrzymanej maszyny Wirtualnej pozostaną nienaruszone. Zamykanie hello maszyny Wirtualnej z wewnątrz nie automatycznie wymusi dezaktywowanie alokacji.

Nawet w przypadku scenariuszy między różnymi lokalizacjami domyślnie zamykania i dezaktywowanie alokacji oznaczają dezaktywowanie przypisanie hello adresów IP z hello maszyny Wirtualnej, nawet jeśli zasad lokalnych w ustawieniach DHCP są różne.

* Witaj wyjątek Jeśli przypisuje jeden statyczny adres IP tooa sieci interfejs jako opisano [tutaj][virtual-networks-reserved-private-ip].
* W takim przypadku hello adres IP nie zmienia się tak długo, jak hello interfejsu sieciowego nie jest usuwany.

> [!IMPORTANT]
> W kolejności tookeep hello całego wdrożenia proste i łatwą w obsłudze hello wyraźny wniosek: zalecane jest toosetup hello partnerstwo w konfiguracji DBMS HA lub odzyskiwanie po awarii w obrębie platformy Azure w taki sposób, który istnieje działa rozpoznawanie nazw między powitalne związane z różnych maszyn wirtualnych maszyn wirtualnych.
>
>

## <a name="deployment-of-host-monitoring"></a>Wdrożenie hosta monitorowania
W przypadku produktywności korzystania z aplikacji SAP w maszynach wirtualnych platformy Azure SAP wymaga hosta tooget możliwości hello dane monitorowania z hello hostów fizycznych z uruchomionymi hello maszynach wirtualnych platformy Azure. Określony poziom poprawki SAP HostAgent będzie wymagane, umożliwia tę funkcję w SAPOSCOL i SAP HostAgent. Poziom poprawki dokładne Hello jest udokumentowany uwagi SAP [1409604].

Witaj szczegóły dotyczące wdrażania składników, które dostarczają tooSAPOSCOL danych hosta i SAPHostAgent i hello Zarządzanie cyklem życia tych składników, zobacz toohello [przewodnik wdrażania][deployment-guide]

## <a name="3264829e-075e-4d25-966e-a49dad878737"></a>Szczegóły tooMicrosoft programu SQL Server
### <a name="sql-server-iaas"></a>SQL Server IaaS
W programie Microsoft Azure, można łatwo migracji istniejących aplikacji SQL Server w oparciu tooAzure platformy systemu Windows Server maszyn wirtualnych. Program SQL Server w maszynie wirtualnej umożliwia możesz tooreduce hello całkowity koszt posiadania wdrażania, zarządzania i konserwacji aplikacji szerokość przedsiębiorstwa za pomocą łatwo migracji tych tooMicrosoft aplikacji Azure. Z programem SQL Server w maszynie wirtualnej platformy Azure Administratorzy i deweloperzy mogą nadal używać hello tych samych narzędzi programowania i administracji, które są dostępne lokalnie.

> [!IMPORTANT]
> Należy pamiętać, że firma Microsoft nie dyskusji Microsoft usługi Azure SQL Database, który to platforma jako ofertę usługi hello platformy Microsoft Azure. Omówienie Hello w tym dokumencie jest uruchomiony hello produktu SQL Server, ponieważ jest ona znana wdrożeń lokalnych w maszynach wirtualnych platformy Azure, hello korzystanie z usług infrastruktury jako możliwości usługi Azure. Funkcje bazy danych i funkcji między te dwie oferty są różne, a nie może być mieszane ze sobą. Zobacz też: <https://azure.microsoft.com/services/sql-database/>
>
>

Zdecydowanie zaleca się tooreview [to] [ virtual-machines-sql-server-infrastructure-services] dokumentacji, przed kontynuowaniem.

W hello następujące sekcje części części dokumentacji hello w obszarze hello łącze powyżej zostaną zagregowane i wymienione. Szczegóły wokół SAP są wymienione także i niektóre pojęcia są opisane bardziej szczegółowo. Jednak zdecydowanie zalecane jest toowork za pośrednictwem dokumentacji hello powyżej pierwszej przed odczytaniem szczegółowej dokumentacji programu SQL Server hello.

Brak niektórych programu SQL Server w IaaS określone informacje, których należy wiedzieć przed kontynuowaniem:

* **Umowa SLA maszyny wirtualnej**: Brak umowy SLA dla maszyn wirtualnych działających na platformie Azure, w którym można znaleźć tutaj: <https://azure.microsoft.com/support/legal/sla/>  
* **Obsługa wersji programu SQL**: w przypadku klientów SAP, firma Microsoft obsługuje program SQL Server 2008 R2 lub nowszy na maszyny wirtualne Microsoft Azure. Starszych wersji nie są obsługiwane. Przejrzyj ogólnego [oświadczenie pomocy technicznej](https://support.microsoft.com/kb/956893) więcej szczegółów. Należy pamiętać, że ogólnie programu SQL Server 2008 jest obsługiwane przez firmę Microsoft oraz. Jednak powodu funkcji toosignificant SAP, którą wprowadzono w programie SQL Server 2008 R2, SQL Server 2008 R2 jest hello minimalnej wersji dla programu SAP. Należy pamiętać, że programu SQL Server 2012 i 2014 został rozszerzony za pomocą lepszą integrację hello scenariusz IaaS (takich jak tworzenie kopii zapasowej bezpośrednio w usłudze Azure Storage). W związku z tym stosujemy ograniczenia, to tooSQL papieru Server 2012 i 2014 z poziomu najnowsze poprawki dla platformy Azure.
* **Obsługa funkcji SQL**: funkcje najbardziej programu SQL Server są obsługiwane w programie Microsoft Azure Virtual Machines z kilkoma wyjątkami. **SQL Server Failover Clustering przy użyciu udostępnionych dysków nie jest obsługiwane**.  Rozproszone technologii, takich jak dublowania bazy danych, zawsze włączonych grup dostępności, replikacji, aby wysyłanie dziennika i brokera usług, które są obsługiwane w pojedynczym regionie Azure. Program SQL Server AlwaysOn również są obsługiwane między różnych regionach platformy Azure zgodnie z opisem w tym miejscu: <https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.  Przejrzyj hello [oświadczenie pomocy technicznej](https://support.microsoft.com/kb/956893) więcej szczegółów. Przykład sposobu toodeploy konfiguracji funkcji AlwaysOn jest wyświetlany w [to] [ virtual-machines-workload-template-sql-alwayson] artykułu. Sprawdź również, hello najlepsze rozwiązania w zakresie udokumentowane [tutaj][virtual-machines-sql-server-infrastructure-services]
* **Wydajność SQL**: pracujemy pewność, że Microsoft Azure hostowanej maszyny wirtualnej będzie wykonywać bardzo dobrze porównanie tooother chmury publicznej wirtualizacji oferty, ale wyniki poszczególnych może się różnić. Zapoznaj się z [to] [ virtual-machines-sql-server-performance-best-practices] artykułu.
* **Przy użyciu obrazów z portalu Azure Marketplace**: hello najszybszy sposób toodeploy nowej maszyny Wirtualnej Microsoft Azure jest toouse obrazu z hello Azure Marketplace. Brak obrazów w hello Azure Marketplace, które zawierają programu SQL Server. obrazy Hello programu SQL Server już zainstalowanym nie można użyć od razu SAP NetWeaver aplikacji. Przyczyna Hello jest hello domyślne sortowanie programu SQL Server jest zainstalowany w tych obrazów i nie sortowania hello wymaganych przez systemy SAP NetWeaver. W kolejności toouse takich obrazów, sprawdź, czy hello czynności opisanych w rozdziale [przy użyciu programu SQL Server obrazy poza hello Microsoft Azure Marketplace][dbms-guide-5.6].
* Zapoznaj się z [szczegóły cennika](https://azure.microsoft.com/pricing/) Aby uzyskać więcej informacji. Witaj [Podręcznik licencjonowania programu SQL Server 2012](https://download.microsoft.com/download/7/3/C/73CAD4E0-D0B5-4BE5-AB49-D5B886A5AE00/SQL_Server_2012_Licensing_Reference_Guide.pdf) i [Podręcznik licencjonowania programu SQL Server 2014](https://download.microsoft.com/download/B/4/E/B4E604D9-9D38-4BBA-A927-56E4C872E41C/SQL_Server_2014_Licensing_Guide.pdf) są również ważnych zasobów.

### <a name="sql-server-configuration-guidelines-for-sap-related-sql-server-installations-in-azure-vms"></a>Wskazówki dotyczące konfigurowania programu SQL Server dla programu SAP związane z instalacji programu SQL Server na maszynach wirtualnych Azure
#### <a name="recommendations-on-vmvhd-structure-for-sap-related-sql-server-deployments"></a>Zalecenia dotyczące maszyny Wirtualnej/VHD struktury dla programu SAP dotyczące wdrożenia programu SQL Server
Zgodnie z hello ogólny opis, plików wykonywalnych programu SQL Server powinny być znajduje się lub zainstalowany na dysku systemowym hello wirtualna hello podstawowy plik VHD (dysk C:\).  Zazwyczaj większość hello programu SQL Server systemowych baz danych nie są używane na wysokim poziomie przez SAP NetWeaver obciążenie. Dlatego hello systemowych baz danych programu SQL Server (master, msdb i modelu) może pozostawać na powitania również dysku C:\. Wystąpił wyjątek może być bazy danych tempdb, co w przypadku hello niektórych ERP SAP i wszystkich BW obciążeń, może wymagać większą ilość danych lub woluminu operacji We/Wy, który nie pasuje do hello oryginalna maszyna wirtualna. W tych systemach można wykonać hello następujące kroki:

* Przenieś toohello pliki danych tempdb głównej hello tym samym dysku logicznego hello danych podstawowych pliki bazy danych SAP hello.
* Dodaj wszelkie dodatkowe tempdb danych plików tooeach z hello innych dysków logicznych zawierający plik danych bazy danych użytkowników programu SAP hello.
* Dodaj hello tempdb logfile toohello dysku logicznego zawierającą hello użytkownika w pliku dziennika bazy danych.
* **Wyłącznie do typów maszyny Wirtualnej, które używają lokalnych dysków SSD** na powitania obliczeń węzła bazy danych tempdb danych i dziennika pliki może umieścić na dysku D:\ hello. Niemniej jednak, może być zalecane toouse wielu plikach danych tempdb. Należy pamiętać, że woluminy dysku D:\ są różne oparte na powitania typu maszyny Wirtualnej.

Te konfiguracje Włącz tempdb tooconsume więcej miejsca niż dysk systemowy hello jest tooprovide stanie. Kolejność toodetermine hello tempdb właściwego rozmiaru jedną Sprawdź hello rozmiary bazy danych tempdb na istniejących systemów, które lokalnie. Ponadto taka konfiguracja umożliwia liczb IOPS względem bazy danych tempdb, który nie może posiadać hello dysku systemowego. Ponownie systemów, które są uruchomione w siedzibie firmy może być obciążenie toomonitor używane we/wy względem bazy danych tempdb, dzięki czemu mogą pochodzić liczb IOPS hello spodziewać się toosee w przypadku bazy danych tempdb.

Konfiguracja maszyny Wirtualnej, w którym działa program SQL Server z bazą danych SAP i rozmieszczenie danych tempdb i bazy danych tempdb pliku dziennika na dysku D:\ hello wyglądałyby tak jak:

![Odwołanie do konfiguracji IaaS maszyny Wirtualnej platformy Azure dla programu SAP][dbms-guide-figure-300]

Należy pamiętać, że hello dysku D:\ ma różne rozmiary zależne hello typu maszyny Wirtualnej. Zależne od hello rozmiaru wynoszącego tempdb może być na wymuszone toopair danych tempdb i pliki dziennika z hello SAP dane z bazy danych i pliki dziennika w przypadku gdy dysku D:\ jest za mały.

#### <a name="formatting-hello-vhds"></a>Formatowanie hello wirtualne dyski twarde
Dla programu SQL Server hello rozmiar bloku systemu plików NTFS, które wirtualne dyski twarde zawierające dane programu SQL Server i dziennik pliki powinny być 64 KB. Nie konieczności tooformat hello dysku D:\ nie istnieje. Ten dysk jest wstępnie sformatowane.

W kolejności toomake się, że hello przywracania lub tworzenie baz danych nie inicjuje hello pliki danych poprzez wyzerowanie zawartości hello hello plików, należy upewnić się, że usługi SQL Server hello kontekstu użytkownika hello działa ma określone uprawnienia. Zazwyczaj użytkownicy w grupie administratora usługi Windows hello ma te uprawnienia. Jeżeli hello usługi SQL Server jest uruchamiany w kontekście użytkownika hello użytkownika bez uprawnień administratora na systemie Windows, należy tooassign hello tego użytkownika prawa użytkownika "Wykonaj zadania konserwacji woluminu".  Zobacz szczegóły hello w tym artykule bazy wiedzy firmy Microsoft: <https://support.microsoft.com/kb/2574695>

#### <a name="impact-of-database-compression"></a>Wpływ kompresji bazy danych
W konfiguracji, gdy przepustowość operacji We/Wy mogą stać się czynnikiem ograniczającym co miar, co zmniejsza liczbę IOPS mogą ułatwić toostretch hello obciążenie, co mogą uruchamiać w scenariuszu IaaS, takich jak Azure. W związku z tym jeśli nie została jeszcze zrobione, zastosowanie kompresji strony serwera SQL zdecydowanie zaleca się przez SAP i Microsoft przed przekazywania SAP istniejącego w bazach danych tooAzure.

Witaj zalecenie tooperform kompresji bazy danych przed przekazaniem tooAzure znajduje się z dwóch powodów:

* Witaj ilość danych toobe przekazać jest niższa.
* czas trwania Hello wykonywania kompresji hello jest krótszy, przy założeniu, że jeden służy silniejszych sprzętu z więcej procesorów ani większą przepustowość operacji We/Wy lub mniej we/wy opóźnienia lokalnymi.
* Mniejsze rozmiary bazy danych może prowadzić tooless kosztów przydział dysku

Kompresja bazy danych działa również w maszynach wirtualnych platformy Azure, jak lokalnie. Aby uzyskać więcej informacji na jak toocompress istniejącej bazy danych SAP programu SQL Server można znaleźć tutaj: <https://blogs.msdn.com/b/saponsqlserver/archive/2010/10/08/compressing-an-sap-database-using-report-msscompress.aspx>

### <a name="sql-server-2014--storing-database-files-directly-on-azure-blog-storage"></a>Program SQL Server 2014 — przechowywanie bazy danych plików bezpośrednio na blogu magazynu Azure
SQL Server 2014 otwiera pliki bazy danych toostore możliwość hello bezpośrednio w magazynie obiektów Blob Azure bez hello "otokę" wokół nich dysku VHD. Szczególnie w przypadku przy użyciu usługi Azure Standard Storage lub typów mniejszych maszyny Wirtualnej dzięki temu scenariuszy, w której można rozwiązać, limity hello iops może zostać wymuszone przez ograniczona liczba wirtualnych dysków twardych, które mogą być toosome zainstalowanego mniejszych typów maszyny Wirtualnej. Działa to w przypadku baz danych użytkowników, ale nie dla systemowych baz danych programu SQL Server. Działa także dla plików danych i dziennika programu SQL Server. Jeśli chcesz toodeploy programu SQL Server SAP bazy danych dzięki temu zamiast "pakowanie" go do dysków VHD, należy pamiętać hello następujących:

* toobe potrzeb konto magazynu używane Hello w hello tego samego regionu Azure, jak hello jest używane toodeploy powitalne maszyny Wirtualnej programu SQL Server jest uruchomiony w.
* Wymienione wcześniej w odniesieniu do toodistribute wirtualne dyski twarde za pośrednictwem różnych kontach magazynu Azure kwestie dla tej metody, a także wdrożeń. Oznacza, że hello liczby operacji We/Wy limitów hello hello konta magazynu Azure.

[comment]: <> (MSSedusch TODO, ale zostaną użyte przepustowość sieci i nie przepustowość magazynu nie go?)

Szczegółowe informacje o tym typie wdrożenia są wyświetlane tutaj: <https://msdn.microsoft.com/library/dn385720.aspx>

W kolejności toostore pliki programu SQL Server dane bezpośrednio w usłudze Azure Premium Storage, potrzebujesz wersji poprawki toohave minimalna programu SQL Server 2014, który jest opisanych tutaj: <https://support.microsoft.com/kb/3063054>. Przechowywanie plików danych programu SQL Server na usługi Azure Standard Storage działa z hello wydana wersja programu SQL Server 2014. Jednak poprawki tej samej hello zawierają innej serii poprawki, które powodują bardziej niezawodny hello bezpośredniego użycia magazynu obiektów Blob Azure do tworzenia kopii zapasowych i plików danych programu SQL Server. Dlatego zaleca się toouse poprawki te na ogół.

### <a name="sql-server-2014-buffer-pool-extension"></a>Rozszerzenie puli buforów programu SQL Server 2014
SQL Server 2014 wprowadzono nową funkcję, która jest wywoływana rozszerzenia puli buforów. Ta funkcja stanowi rozszerzenie puli buforów hello programu SQL Server, który jest przechowywany w pamięci z drugiego poziomu pamięci podręcznej, która nie jest obsługiwana przez lokalne dyski SSD serwera lub maszyny Wirtualnej. Dzięki temu tookeep większy zestaw roboczy danych "w pamięci". W porównaniu tooaccessing usługi Azure Standard Storage hello dostępu do hello rozszerzenia puli buforów hello, który jest przechowywany na lokalnych dyskach SSD maszyny wirtualnej Azure jest wiele czynników szybciej.  W związku z tym wykorzystaniu hello na lokalnym dysku D:\ hello maszyny Wirtualnej typów, które mają znakomity IOPS i przepływności może być bardzo rozsądnego sposobu hello tooreduce IOPS obciążenia w usłudze Azure Storage i znacznie skrócić czas odpowiedzi zapytań. Dotyczy to zwłaszcza w przypadku, gdy nie używa magazyn w warstwie Premium. W przypadku magazyn w warstwie Premium i użycie hello hello pamięci podręcznej odczytu Azure Premium w węźle obliczeń hello zalecanych do plików danych, nie duże różnice nie oczekiwano. Przyczyną jest to, że oba pamięci podręcznych (rozszerzenie puli buforów serwera SQL i pamięci podręcznej odczytu magazynu Premium) używają dyski lokalne powitania węzłów obliczeniowych hello.
Aby uzyskać więcej informacji na temat tej funkcji, sprawdź, czy w tej dokumentacji: <https://msdn.microsoft.com/library/dn133176.aspx>

### <a name="backuprecovery-considerations-for-sql-server"></a>Uwagi dotyczące tworzenia kopii zapasowej i odzyskiwania dla programu SQL Server
W przypadku wdrażania serwera SQL na platformie Azure z kopii zapasowej metodologii musi przejrzeć. Nawet jeśli hello systemu nie jest systemów produkcyjnych, hello SAP obsługiwanych przez program SQL Server musi być kopię zapasową bazy danych okresowo. Ponieważ Magazyn Azure przechowuje trzy obrazy, jest teraz mniej ważne w zakresie toocompensating awarii magazynu kopii zapasowej. Powodem priorytet Hello utrzymania właściwego planu tworzenia kopii zapasowych i odzyskiwania jest więcej, który można kompensowane błędy logiczne/ręczny, zapewniając punktu w czasie możliwości odzyskiwania. Dzięki hello celem jest tooeither użyj kopii zapasowych toorestore hello kopii bazy danych tooa niektórych punktu w czasie lub toouse kopie zapasowe hello w Azure tooseed innego systemu przez skopiowanie hello istniejącej bazy danych. Na przykład można zostaną przeniesione z warstwy 2 SAP tooa systemu 3-warstwowej ustawienia konfiguracji hello sam systemu przez Przywracanie kopii zapasowej.

Istnieją trzy różne sposoby toobackup programu SQL Server tooAzure magazynu:

1. SQL Server 2012 CU4 i wyższe może natywnie kopii zapasowej bazy danych tooa adresu URL. To jest szczegółowo opisane w blogu hello [nowych funkcji w programie SQL Server 2014 — część 5 – Backup/Restore ulepszenia](https://blogs.msdn.com/b/saponsqlserver/archive/2014/02/15/new-functionality-in-sql-server-2014-part-5-backup-restore-enhancements.aspx). Patrz rozdział [programu SQL Server 2012 SP1 CU4 lub nowszy][dbms-guide-5.5.1].
2. Wcześniejsze tooSQL wersjach programu SQL Server 2012 CU4 za pomocą przekierowania tooa toobackup funkcji wirtualnego dysku twardego i zasadniczo przejścia hello zapisu strumienia do lokalizacji magazynu Azure, który został skonfigurowany. Patrz rozdział [programu SQL Server 2012 z dodatkiem SP1 CU3 i wcześniejszych wersjach][dbms-guide-5.5.2].
3. Metoda końcowego Hello jest tooperform konwencjonalnych polecenia toodisk kopii zapasowych programu SQL Server na urządzeniu dysku VHD.  To jest identyczne toohello lokalnego wdrożenia wzorca i nie została omówiona szczegółowo w tym dokumencie.

#### <a name="0fef0e79-d3fe-4ae2-85af-73666a6f7268"></a>SQL Server 2012 SP1 CU4 lub nowszy
Ta funkcja umożliwia magazynu obiektów BLOB toodirectly tooAzure kopii zapasowej. Bez tej metody należy wykonać kopię zapasową tooother Azure wirtualne dyski twarde, która będzie używać pojemność wirtualnego dysku twardego i IOPS. pomysł Hello jest zasadniczo to:

 ![Za pomocą narzędzia Kopia zapasowa programu SQL Server 2012 tooMicrosoft obiektu BLOB magazynu Azure][dbms-guide-figure-400]

w takim przypadku Hello zaletą jest to, że nie należy toospend wirtualne dyski twarde toostore programu SQL Server z kopii zapasowych na. Tak ma mniejszą liczbę dysków VHD przydzielone i przepustowości całego hello iops wirtualnego dysku twardego może służyć do plików danych i dziennika. Należy pamiętać, że hello maksymalny rozmiar kopii zapasowej jest ograniczona tooa maksymalnie 1 TB, zgodnie z opisem w sekcji "Ograniczenia" hello, w tym artykule: <https://msdn.microsoft.com/library/dn435916.aspx#limitations>. Jeśli rozmiar kopii zapasowej hello, pomimo przy użyciu kopii zapasowej serwera SQL kompresji spowoduje przekroczenie 1 TB, rozmiar, hello funkcji opisanych w rozdziale [programu SQL Server 2012 z dodatkiem SP1 CU3 i wcześniejszych wersjach] [ dbms-guide-5.5.2] w tym dokumencie toobe używane.

[Dokumentację pokrewną](https://msdn.microsoft.com/library/dn449492.aspx) opisujące hello Przywracanie bazy danych z kopii zapasowej na magazyn obiektów Blob Azure zaleca nie toorestore bezpośrednio z magazynu obiektów BLOB platformy Azure, jeśli kopie zapasowe hello jest > 25 GB. zalecenie Hello w tym artykule po prostu opiera się na zagadnienia dotyczące wydajności i nie ze względu ograniczenia toofunctional. W związku z tym inne warunki mogą stosować na podstawie przypadku.

Można znaleźć w dokumentacji w sposób ustawiania i wykorzystać ten typ kopii zapasowej [to](https://msdn.microsoft.com/library/dn466438.aspx) samouczka

Przykład Witaj sekwencji kroki mogą być odczytywane [tutaj](https://msdn.microsoft.com/library/dn435916.aspx).

Automatyzacja tworzenia kopii zapasowych, jest najwyższym toomake znaczenie się, że inne nazwy obiektów blob powitania dla każdej kopii zapasowej. W przeciwnym razie zostaną one zastąpione i łańcuch przywracania hello został przerwany.

W celu nie toomix się rzeczy między hello 3 poszczególnych typów kopii zapasowych jest wskazane toocreate różnych kontenerów poniżej hello magazynu konto używane do tworzenia kopii zapasowych. kontenery Hello można przez maszynę Wirtualną lub przez typ maszyny Wirtualnej i tworzenia kopii zapasowej tylko. Schemat Hello może wyglądać jak:

 ![Za pomocą narzędzia Kopia zapasowa programu SQL Server 2012 tooMicrosoft obiektu BLOB magazynu Azure — różnych kontenerów w ramach oddzielnego konta magazynu][dbms-guide-figure-500]

W przykładzie hello powyżej hello się, że nie jest wykonywane kopie zapasowe do tego samego magazynu konta w przypadku gdy hello hello maszyny wirtualne są wdrażane. Byłoby nowe konto magazynu specjalnie z myślą o hello kopii zapasowych. W ramach kont magazynu hello będzie różnych kontenerów utworzone za pomocą macierzy hello typ kopii zapasowej i hello nazwę maszyny Wirtualnej. Takie segmentacji ułatwi łatwiejsze tooadministrate hello kopie zapasowe hello różnych maszyn wirtualnych.

obiekty BLOB Hello, który zapisuje jedną bezpośrednio hello kopii zapasowych, nie jest dodawany toohello liczba hello wirtualne dyski twarde maszyny wirtualnej. Dlatego jedną można zmaksymalizować hello maksymalna liczba wirtualnych dysków twardych zainstalowanych hello określonych SKU maszyny Wirtualnej dla danych hello i transakcji plik dziennika i nadal wykonywać względem kontenera magazynu kopii zapasowej.

#### <a name="f9071eff-9d72-4f47-9da4-1852d782087b"></a>SQL Server 2012 z dodatkiem SP1 CU3 i wcześniejszych wersjach
pierwszym krokiem Hello w kolejności tooachieve należy wykonać kopię zapasową bezpośrednio w usłudze Azure Storage będzie toodownload hello msi, który jest połączony za[to](https://www.microsoft.com/download/details.aspx?id=40740) KBA artykułu.

Pobierz plik instalacyjny hello x64 i hello dokumentacji. Plik Hello zainstaluje program o nazwie: "Kopia zapasowa programu Microsoft SQL Server tooMicrosoft narzędzie Azure". Dokładnie zapoznaj się dokumentacją hello hello produktu.  Narzędzie Hello zasadniczo działa w następujący sposób hello:

* Z powitania po stronie serwera SQL jest zdefiniowany lokalizację dysku do utworzenia kopii zapasowej hello programu SQL Server (nie używaj dysku D:\ hello to).
* Narzędzie Hello pozwoli toodefine reguł, które mogą być używane toodirect różne rodzaje kontenery magazynu Azure toodifferent kopii zapasowych.
* Po hello reguły są spełnione, narzędzie hello przekieruje strumień zapisu hello hello tooone kopii zapasowej z toohello wirtualne dyski twarde/dysków hello lokalizacji magazynu Azure, który został wcześniej zdefiniowany.
* Narzędzie Hello pozostawi pliku niewielkie kilka KB rozmiaru na powitania wirtualnego dysku twardego/dysku, który został zdefiniowany dla programu SQL Server hello kopii zapasowej. **Ten plik należy pozostawić w lokalizacji magazynu hello, ponieważ jest ono wymagane toorestore ponownie z usługi Magazyn Azure.**
  * Jeśli wybrano opcję hello tworzenia kopii zapasowych tooa konta usługi Magazyn Microsoft Azure utracić plik szczątkowy hello (np. poprzez utraty hello nośników, który zawiera plik szczątkowy hello), może odzyskać plik szczątkowy hello za pośrednictwem usługi Magazyn Microsoft Azure przez Trwa pobieranie jej z hello kontenera magazynu, w którym została umieszczona. Następnie należy umieścić plik szczątkowy hello do folderu na komputerze lokalnym hello hello narzędzia w przypadku skonfigurowanego toohello toodetect i przekazywanie tego samego kontenera z hello tego samego hasła szyfrowania, jeśli szyfrowanie została użyta z hello oryginalnej reguły.

Oznacza to, że schemat hello zgodnie z powyższym opisem dla nowszej wersji programu SQL Server mogą być przełączane w miejscu, jak również dla wersji programu SQL Server, które nie zezwalają na bezpośredni adres lokalizacji magazynu Azure.

Ta metoda nie powinna być używana z nowszej wersji programu SQL Server, które obsługuje wykonywania kopii zapasowych natywnie w usłudze Azure Storage. Wyjątki są, gdzie ograniczenia hello natywnego wykonywania kopii zapasowych na platformie Azure blokują natywnego wykonywania kopii zapasowej na platformie Azure.

#### <a name="other-possibilities-toobackup-sql-server-databases"></a>Innych baz danych programu SQL Server toobackup możliwości
Bazy danych innych możliwości toobackup jest tooattach dodatkowe tooa wirtualne dyski twarde maszyny Wirtualnej używanej toostore kopii zapasowych na. W takim przypadku należy toomake się, że ten hello wirtualne dyski twarde nie są uruchomione pełna. Jeśli jest przypadek hello, będzie potrzebny hello toounmount wirtualnego dysku twardego i dlatego toospeak "archiwizować" i zastąp go nowy pusty dysk VHD. Jeśli ta ścieżka jest przerywane, ma tookeep te wirtualne dyski twarde w osobnych kont magazynu Azure z hello te, które hello wirtualne dyski twarde z hello pliki bazy danych.

Druga możliwość jest toouse dużą maszynę Wirtualną, która może mieć wiele wirtualnych dysków twardych, które są dołączone. Na przykład D14 z 32VHDs. Użyj elastyczne środowisko, w którym rozwiązaniem jest utworzenie udziałów który służą następnie jako obiekty docelowe kopii zapasowej do różnych serwerów systemu DBMS hello toobuild miejsca do magazynowania.

Najlepsze rozwiązania został udokumentowany [tutaj](https://blogs.msdn.com/b/sqlcat/archive/2015/02/26/large-sql-server-database-backup-on-an-azure-vm-and-archiving.aspx) również.

#### <a name="performance-considerations-for-backupsrestores"></a>Zagadnienia dotyczące wydajności dla kopii zapasowych/przywracania
Jak wdrożenia bez systemu operacyjnego wydajności tworzenia kopii zapasowej i przywracania jest zależna od mogą być odczytywane jak wiele woluminów równolegle i jakie przepływności hello tych woluminów mogą być. Ponadto hello użycie procesora CPU używanych przez kompresję kopii zapasowych może odtworzyć istotną rolę na maszynach wirtualnych z właśnie too8 wątków procesora CPU. W związku z tym co można założyć:

* Witaj mniej hello liczba wirtualnych dysków twardych używanych toostore hello danych plików, hello mniejszych hello ogólną przepustowość podczas odczytywania.
* Witaj mniejszą liczbę hello wątków procesora CPU w hello maszyny Wirtualnej, hello poważniejsze wpływ hello kompresja kopii zapasowej.
* Hello mniej toowrite elementów docelowych (obiekty BLOB lub wirtualne dyski twarde) hello tworzenie kopii zapasowych, hello mniejszym hello przepływności.
* Witaj Witaj mniejszy rozmiar maszyny Wirtualnej, hello mniejszych hello przydział pamięci masowej przepływność zapisu i odczytu z magazynu Azure. Niezależnie od tego, czy hello są przechowywane kopie zapasowe bezpośrednio na obiektów Blob platformy Azure lub czy są przechowywane w plikach VHD, które ponownie są przechowywane w obiektach blob Azure.

Przy użyciu obiektu BLOB magazynu Azure Microsoft jako miejsce docelowe kopii zapasowej hello w nowszej wersji, są ograniczone toodesignating tylko jeden obiekt docelowy adresu URL dla każdej kopii zapasowej.

Ale korzystając z hello "Kopia zapasowa programu Microsoft SQL Server tooMicrosoft narzędzie Azure" w starszych wersjach, można zdefiniować więcej niż jeden element docelowy pliku. Z więcej niż jeden element docelowy hello kopii zapasowej można skalować i hello przepływności hello kopii zapasowej jest wyższy. To spowoduje następnie wielu plików, również w hello konta magazynu Azure. Podczas testów przy użyciu wielu plików miejsc docelowych, co ostatecznie osiągnąć przepływności hello, który jedną można osiągnąć z rozszerzeniami kopii zapasowej hello zaimplementowana w z programu SQL Server 2012 SP1 CU4 na. Możesz również nie są blokowane przez limit 1TB hello jak hello natywnego wykonywania kopii zapasowych na platformie Azure.

Należy jednak pamiętać, również przepływności hello jest zależna od lokalizacji hello hello użyć do utworzenia kopii zapasowej hello konta magazynu Azure. Rozwiązaniem może być konta magazynu hello toolocate w regionie innym niż hello maszyny wirtualne są uruchomione w. Na przykład Czy uruchomić hello konfiguracji maszyny Wirtualnej w Europa Zachodnia, ale put hello konta magazynu Użyj tooback się przed w Europie Północna. Czy na pewno będą miały wpływ na przepustowość kopii zapasowej hello i jest prawdopodobnie nie toogenerate 150MB/s przepustowości wydaje się toobe możliwe w przypadku gdy hello docelowy magazyn i hello maszyny wirtualne są uruchomione w hello samego regionalne centrum danych.

#### <a name="managing-backup-blobs"></a>Zarządzanie obiekty BLOB kopii zapasowej
Brak kopii zapasowych wymaganie toomanage hello samodzielnie. Ponieważ hello oczekuje się, że wiele obiektów blob zostaną utworzone, wykonując kopie zapasowe dziennika transakcji częste, administracja tych obiektów blob można łatwo przeciążać hello portalu Azure. W związku z tym jest recommendable tooleverage Eksploratora magazynu Azure. Istnieje kilka dobrej dostępnymi umożliwiające toomanage konta magazynu platformy Azure

* Microsoft Visual Studio z zestawem Azure SDK zainstalowany (<https://azure.microsoft.com/downloads/>)
* Eksplorator usługi Storage platformy Microsoft Azure (<https://azure.microsoft.com/downloads/>)
* 3 narzędzi

[comment]: <> (Nie jest jeszcze obsługiwane na ARM)
[comment]: <> (### Azure kopii zapasowej maszyny Wirtualnej)
[comment]: <> (Maszyny wirtualne w ramach hello systemu SAP utworzeniem kopii zapasowej za pomocą funkcji Kopia zapasowa maszyny wirtualnej Azure. Kopii zapasowej maszyny wirtualnej platformy Azure otrzymano wprowadzono na początku hello roku 2015 i w tym samym czasie jest toobackup standardowe metody ukończenia maszyny Wirtualnej na platformie Azure. Kopia zapasowa Azure przechowuje kopie zapasowe hello na platformie Azure i pozwala ponownie przywracania maszyny wirtualnej.)
[comment]: <> (Maszyny wirtualne, które wykonywania może być kopie zapasowe baz danych w sposób ciągły, a także jeśli obsługuje systemy DBMS hello hello usługi kopiowania w tle woluminu systemu Windows usługi VSS < jest https://msdn.microsoft.com/library/windows/desktop/bb968832.aspx> jako programu SQL Server. Dlatego przy użyciu kopii zapasowej maszyny Wirtualnej platformy Azure może być tooa tooget sposób umożliwiająca przywrócenie kopii zapasowej bazy danych SAP. Należy jednak pamiętać, który oparty na wykonywanie kopii zapasowych maszyny Wirtualnej platformy Azure, które przywraca w momencie baz danych nie jest możliwe. W związku z tym hello zaleca tooperform kopie zapasowe baz danych z funkcjami systemu DBMS zdejmując to zadanie kopii zapasowej maszyny Wirtualnej Azure.)
[comment]: <> (tooget zapoznać się z kopii zapasowej maszyny wirtualnej platformy Azure Uruchom tutaj < https://azure.microsoft.com/documentation/services/backup/>)

### <a name="1b353e38-21b3-4310-aeb6-a77e7c8e81c8"></a>Przy użyciu obrazów programu SQL Server, poza hello Microsoft Azure Marketplace
Firma Microsoft oferuje maszyn wirtualnych w hello Azure Marketplace, która już zawiera wersje programu SQL Server. SAP klientów, którzy wymagają licencji programu SQL Server i Windows może to być możliwości toobasically okładce hello potrzebę licencji według Obracająca się maszyn wirtualnych z programem SQL Server już zainstalowana. Toouse kolejności tych obrazów dla SAP, hello następujące zagadnienia dotyczące niezbędne toobe wprowadzone:

* wersje oceny z systemem innym niż SQL Server Hello uzyskać wyższe koszty niż tylko "Tylko do systemu Windows" maszyny Wirtualnej wdrożone z portalu Azure Marketplace. Zobacz artykuły ceny toocompare: <https://azure.microsoft.com/pricing/details/virtual-machines/> i <https://azure.microsoft.com/pricing/details/virtual-machines/#Sql>.
* Można używać tylko wersji programu SQL Server, które są obsługiwane przez SAP, takich jak SQL Server 2012.
* Sortowanie Hello hello wystąpienia programu SQL Server, który jest instalowany na maszynach wirtualnych hello oferowany hello Azure Marketplace jest sortowania hello SAP NetWeaver wymaga toorun wystąpienia programu SQL Server hello. Chociaż z instrukcjami hello hello następujących sekcji, można zmienić sortowania hello.

#### <a name="changing-hello-sql-server-collation-of-a-microsoft-windowssql-server-vm"></a>Zmiana hello sortowanie programu SQL Server maszyny wirtualnej programu Microsoft Windows/SQL Server
Ponieważ nie ustawiono hello obrazów programu SQL Server w portalu Azure Marketplace hello toouse hello sortowanie, co jest wymagane przez aplikacje SAP NetWeaver, musi zmienić natychmiast po wdrożeniu hello toobe. Dla programu SQL Server 2012, można to zrobić z hello następujące kroki natychmiast hello maszyna wirtualna została wdrożona, a administrator może toolog do hello wdrożyć maszyny Wirtualnej:

* Otwórz okno poleceń programu Windows "Administrator".
* Zmień hello katalogu tooC:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012.
* Wykonanie polecenia hello: Setup.exe/quiet/Action = / InstanceName REBUILDDATABASE = parametr/SQLSYSADMINACCOUNTS MSSQLSERVER =`<local_admin_account_name`> /SQLCOLLATION = SQL_Latin1_General_Cp850_BIN2   
  * `<local_admin_account_name`> to konto hello, który został zdefiniowany jako konto administratora hello, wdrażając hello maszyny Wirtualnej dla hello za pomocą galerii powitania po raz pierwszy.

proces Hello tylko powinien zająć kilka minut. W kolejności toomake się, czy krok hello ostatecznie otrzymano hello prawidłowego wyniku, należy wykonać hello następujące kroki:

* Otwórz program SQL Server Management Studio.
* Otwórz okno zapytania.
* Wykonanie sp_helpsort polecenia hello w bazie danych master programu SQL Server hello.

Witaj żądanego wyniku powinna wyglądać:

    Latin1-General, binary code point comparison sort for Unicode Data, SQL Server Sort Order 40 on Code Page 850 for non-Unicode Data

Jeśli nie jest to wynik hello Zatrzymaj wdrożenie SAP i zbadać, dlaczego polecenia Instalatora hello zakończyło się niepowodzeniem zgodnie z oczekiwaniami. Wdrożenia SAP NetWeaver aplikacje na wystąpienie programu SQL Server z innej strony kodowe programu SQL Server niż jeden wymienione powyżej hello jest **nie** obsługiwane.

### <a name="sql-server-high-availability-for-sap-in-azure"></a>SQL Server wysokiej dostępności dla programu SAP na platformie Azure
Jak wspomniano wcześniej w tym dokumencie, Brak Brak magazynu toocreate udostępnionych możliwości, który jest konieczny do użycia hello hello najstarsze funkcji wysokiej dostępności programu SQL Server. Ta funkcja zainstalować dwóch lub więcej wystąpień programu SQL Server w Windows Server Failover Cluster (WSFC) za pomocą udostępnionego dysku dla bazy danych użytkowników hello (i ostatecznie tempdb). Jest to hello długo standardowe wysoką dostępność metody, która jest obsługiwana przez SAP. Ponieważ Azure nie obsługuje magazynu udostępnionego, nie zrealizowane konfiguracji o wysokiej dostępności programu SQL Server z konfiguracji klastra udostępnionego dysku. Wiele metod wysokiej dostępności jest jednak nadal możliwe i są opisane w hello następujące sekcje.

[comment]: <> (Artykuł jest nadal tooASM odwołuje)
[comment]: <> (Przed przeczytaniem hello różnych wysoką dostępność określonych technologii można używać dla programu SQL Server na platformie Azure, jest bardzo dobre dokumentu, który zapewnia bardziej szczegółowe informacje i wskaźniki [[[[tutaj] Virtual-Machines-SQL-Server-High-Availability-and-Disaster-Recovery-Solutions])

#### <a name="sql-server-log-shipping"></a>Wysyłanie dziennika programu SQL Server
Jest jedną z metod hello wysokiej dostępności (HA), wysyłania dzienników serwera SQL. Jeśli maszyny wirtualne hello uczestniczących w konfiguracji wysokiej dostępności hello pracy rozpoznawania nazw, problem nie występuje i Instalator hello na platformie Azure zostaną różnią się od żadnej konfiguracji, które jest wykonywane lokalnie. Nie jest zalecane toorely na tylko rozpoznawania adresu IP. W odniesieniu do toosetting wysyłania dzienników i zasadami hello wokół wysyłania dziennika Sprawdź, czy w tej dokumentacji:

<https://technet.microsoft.com/library/ms187103.aspx>

W kolejności tooreally osiągnięcia wysokiej dostępności, co musi hello toodeploy maszyn wirtualnych, które są w tych wysyłania dziennika konfiguracji toobe w hello tego samego zestawu dostępności Azure.

#### <a name="database-mirroring"></a>Funkcja dublowania baz danych
Funkcja dublowania bazy danych, obsługiwana przez SAP (patrz Uwaga SAP [965908]) polega na definiowanie serwer partnerski trybu failover w hello SAP parametry połączenia. W przypadku hello między lokalizacjami przyjęto założenie, tym Witaj dwie maszyny wirtualne są w hello tej samej domeny i że wystąpień programu SQL Server hello dwa kontekstu użytkownika hello działają w ramach są również użytkowników domeny i odpowiednich uprawnień w wystąpieniach programu SQL Server hello dwa związane. W związku z tym hello Konfiguracja dublowania bazy danych na platformie Azure nie różnią się lokalnej typowe ustawienia/konfiguracji.

W przypadku wdrożenia tylko na chmurze najprostszą hello jest toohave innej domeny w ustawień Azure toohave tych maszyn wirtualnych systemu DBMS (i najlepiej dedykowanych SAP maszyn wirtualnych) w jednej domenie.

Jeśli domeny nie jest możliwe, co umożliwia także certyfikaty dla bazy danych hello dublowania punktów końcowych, zgodnie z opisem w tym miejscu: <https://technet.microsoft.com/library/ms191477.aspx>

Samouczek tooset up dublowania bazy danych na platformie Azure można znaleźć tutaj: <https://technet.microsoft.com/library/ms189852.aspx>

#### <a name="alwayson"></a>Zawsze włączone
Jak AlwaysOn jest obsługiwany dla lokalnego programu SAP (patrz Uwaga SAP [1772688]), jest obsługiwane toobe używane w połączeniu z SAP na platformie Azure. Hello fakt, że firma nie jest możliwe toocreate udostępnionych dysków na platformie Azure nie oznacza, że jeden nie można utworzyć konfiguracji AlwaysOn Windows Server Failover Cluster (WSFC), między różnych maszyn wirtualnych. Oznacza jedynie, że nie masz toouse możliwość hello udostępniony dysk jako kworum w konfiguracji klastra hello. Dlatego możesz skompilować konfiguracji usługi WSFC (AlwaysOn) na platformie Azure i nie wystarczy wybrać typ kworum hello korzystającego z udostępnionego dysku. Witaj środowiska platformy Azure te maszyny wirtualne są wdrażane w powinna być rozpoznawana hello maszyn wirtualnych o nazwie a hello maszyn wirtualnych powinny być hello tej samej domenie. Dotyczy to tylko Azure i wdrożeń między lokalizacjami. Istnieją pewne specjalne uwagi wokół wdrażanie hello odbiornika grupy dostępności programu SQL Server (nie toobe mylić jej z zestawu dostępności Azure hello) ponieważ Azure w tym momencie niedozwolone jest możliwe toosimply utworzyć obiektu AD/serwera DNS lokalny. Dlatego niektóre kroki instalacji różnych są niezbędne tooovercome hello określone zachowanie systemu Azure.

Niektóre kwestie wymagające rozważenia przy użyciu odbiornika grupy dostępności są:

* Przy użyciu odbiornika grupy dostępności jest możliwe tylko z systemu Windows Server 2012 lub Windows Server 2012 R2 jako system operacyjny gościa hello maszyny Wirtualnej. Dla systemu Windows Server 2012 należy się upewnić, że ta poprawka jest stosowana toomake: <https://support.microsoft.com/kb/2854082>
* Dla systemu Windows Server 2008 R2 ta poprawka nie istnieje, a musi zawsze włączonych toobe używane w hello takie same jak w przypadku dublowania bazy danych, określając serwer partnerski trybu failover w ciągu połączenia hello (za pomocą hello SAP default.pfl parametru baz danych i mss/serwerem — patrz Uwaga SAP [965908]).
* Jeśli przy użyciu odbiornika grupy dostępności, hello bazy danych z maszyn wirtualnych muszą toobe połączone tooa dedykowane modułu równoważenia obciążenia. Do rozpoznawania nazw w przypadku wdrożeń tylko w chmurze albo wymagają wszystkich maszyn wirtualnych systemu SAP (serwerów aplikacji, system DBMS serwer i () SCS) są w tej samej sieci wirtualnej hello lub wymaga z SAP aplikacji warstwy hello konserwacji hello etc\host pliku w kolejność tooget hello wirtualna nazwy hello maszynach wirtualnych serwera SQL rozwiązane. W kolejności tooavoid czy Azure przypisuje nowe adresy IP w przypadku gdy obie maszyny wirtualne są okazjonalnie zamknięcia powinien jedną Przypisz statyczne adresy IP interfejsów sieciowych toohello tych maszyn wirtualnych w konfiguracji funkcji AlwaysOn hello (Definiowanie statycznego adresu IP jest opisane w [to] [ virtual-networks-reserved-private-ip] artykuł)

[comment]: <> (Stary blogi)
[comment]: <> (< https://blogs.msdn.com/b/alwaysonpro/archive/2014/08/29/recommendations-and-best-practices-when-deploying-sql-server-alwayson-availability-groups-in-windows-azure-iaas.aspx>, < https://blogs.technet.com/b/rmilne/ Archive/2015/07/27/How-to-set-static-IP-on-Azure-VM.aspx >)
* Istnieją specjalne kroki wymagane podczas kompilowania konfiguracji klastra usługi WSFC hello których hello klastra wymaga specjalnych adres IP przypisany, ponieważ Azure z jego bieżącej funkcji przypisywanej hello nazwy klastra hello sam adres IP klastra hello węzła hello jest tworzona na. Oznacza to, że jest to krok wykonywany ręcznie musi być wykonywane tooassign innego klastra toohello adresów IP.
* Witaj odbiornika grupy dostępności będzie toobe utworzona na platformie Azure z punktów końcowych protokołu TCP/IP, które są przypisane do maszyn wirtualnych toohello systemem hello podstawowych i pomocniczych replik grupy dostępności hello.
* Mogą wystąpić toosecure potrzeby te punkty końcowe z listy kontroli dostępu.

[comment]: <> (Blog starego TODO)
[comment]: <> (Witaj szczegółowy opis kroków i artykuły pierwszej potrzeby zainstalować konfiguracji funkcji AlwaysOn na platformie Azure są najlepiej wystąpił podczas Instruktaż hello samouczek dostępne [here][virtual-machines-windows-classic-ps-sql-alwayson-availability-groups])
[comment]: <> (Wstępnie konfiguracji funkcji AlwaysOn za pośrednictwem hello Azure galerii < https://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx>)
[comment]: <> (Tworzenie odbiornika grupy dostępności jest najlepiej opisane w samouczku [this][virtual-machines-windows-classic-ps-sql-int-listener])
[comment]: <> (Zabezpieczanie punktów końcowych sieci z listy ACL są omówione najlepiej:)
[comment]: <> (* < https://michaelwasham.com/windows-azure-powershell-reference-guide/network-access-control-list-capability-in-windows-azure-powershell/>)
[comment]: <> (* < https://blogs.technet.com/b/heyscriptingguy/archive/2013/08/31/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-1-of-2.aspx>)
[comment]: <> (* < https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/01/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-2-of-2.aspx>)  
[comment]: <> (* < https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/18/creating-acls-for-windows-azure-endpoints.aspx>)

W różnych regionach platformy Azure oraz jest możliwe toodeploy grupy dostępności AlwaysOn programu SQL Server. Ta funkcja będzie korzystać z łączności hello Azure do wirtualnymi ([szczegółowe][virtual-networks-configure-vnet-to-vnet-connection]).

[comment]: <> (Blog starego TODO)
[comment]: <> (Hello ustawienia grup dostępności AlwaysOn programu SQL Server w takiej sytuacji jest opisane tutaj: < https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.)

#### <a name="summary-on-sql-server-high-availability-in-azure"></a>Podsumowanie na wysokiej dostępności serwera SQL na platformie Azure
Podana hello fakt, że usługi Azure Storage chroni zawartość hello, istnieje jeden mniej tooinsist Przyczyna w obrazie stałej gotowości. Oznacza to, że danego scenariusza wysokiej dostępności wymaga tooonly ochronę przed hello w następujących przypadkach:

* Niedostępność hello maszyny Wirtualnej jako całość powodu toomaintenance w klastrze serwerów hello na platformie Azure lub z innych powodów
* Problemy z oprogramowaniem w wystąpieniu programu SQL Server hello
* Ochrona przed ręczne błąd, gdzie danych zostaje usunięta, a w momencie odzyskiwania jest wymagana

Spojrzenie na zgodną technologii, których jedną można argumentowało czy hello dwóch pierwszych przypadkach może być objętych przez dublowania bazy danych lub funkcji AlwaysOn, przypadku trzeci hello tylko mogą być objęte wysyłania dziennika.

Konieczne będzie toobalance hello bardziej złożonych konfiguracji funkcji AlwaysOn, porównaniu tooDatabase dublowania z zalet hello AlwaysOn. Może być wymieniona te korzyści, takich jak:

* Do odczytu replikach pomocniczych.
* Tworzenie kopii zapasowych z replik pomocniczych.
* Lepszą skalowalność.
* Więcej niż jednej repliki pomocniczej.

### <a name="9053f720-6f3b-4483-904d-15dc54141e30"></a>Ogólne programu SQL Server dla programu SAP w podsumowaniu Azure
Istnieje wiele zaleceń w tym przewodniku, i zaleca się, że można go odczytać więcej niż raz przed Planowanie wdrożenia usługi Azure. Ogólnie rzecz biorąc jednak można się hello toofollow top dziesięć DBMS ogólne w określonych punktach Azure:

[comment]: <> (2.3 przepływności wyższy niż co? Niż jeden wirtualny dysk twardy?)
1. Użyj hello najnowsze DBMS zlecenia, takie jak SQL Server 2014, mający hello większości korzyści w usłudze Azure. Dla programu SQL Server to SQL Server 2012 SP1 CU4 obejmujące hello funkcji wykonywania kopii sprzętu magazynu Azure. Jednak w połączeniu z SAP zalecamy co najmniej pakietu CU1 programu SQL Server 2014 z dodatkiem SP1 lub SQL Server 2012 z dodatkiem SP2 i hello najnowszej aktualizacji zbiorczej.
2. Starannie zaplanować Twojej pozioma systemu SAP w układ pliku danych hello Azure toobalance i ograniczenia dotyczące platformy Azure:
   * Nie ma zbyt wiele wirtualnych dysków twardych, ale ma za mało tooensure może nawiązać połączenie z wymagane IOPS.
   * Należy pamiętać, że IOPS są również ograniczone na konto magazynu Azure i czy kont magazynu są ograniczone w ramach każdej subskrypcji platformy Azure ([szczegółowe][azure-subscription-service-limits]).
   * Tylko rozłożonej na wirtualne dyski twarde, jeśli potrzebujesz tooachieve wyższej przepustowości.
3. Nigdy nie instaluj oprogramowania lub umieść wszystkie pliki, które wymaga trwałości na dysku D:\ hello jest niestałych i wszystko na tym dysku zostaną utracone podczas rozruchu systemu Windows.
4. Nie używaj buforowania Azure wirtualnego dysku twardego dla usługi Azure Standard Storage.
5. Nie należy używać konta magazynu Azure replikacją geograficzną.  Magazyn lokalnie nadmiarowy Użyj dla obciążeń systemu DBMS.
6. Użyj dostawcą systemu DBMS wysokiej dostępności i odzyskiwania po awarii rozwiązania tooreplicate bazy danych.
7. Zawsze używaj rozpoznawania nazw, nie należy polegać na adresy IP.
8. Użyj hello najwyższy bazy danych kompresji możliwe. Dla programu SQL Server jest kompresji strony.
9. Należy zachować ostrożność, przy użyciu obrazów programu SQL Server z hello Azure Marketplace. Jeśli używasz hello programu SQL Server, co należy zmienić sortowania wystąpienia hello przed zainstalowaniem dowolnego systemu SAP NetWeaver na nim.
10. Instalowanie i konfigurowanie hello SAP hosta monitorowania dla platformy Azure, zgodnie z opisem w [Deployment Guide][deployment-guide].

## <a name="specifics-toosap-ase-on-windows"></a>Szczegóły tooSAP ASE w systemie Windows
Począwszy od programu Microsoft Azure, możesz łatwo przeprowadzić migrację z istniejącej aplikacji SAP ASE tooAzure maszyn wirtualnych. SAP ASE na maszynie wirtualnej umożliwia możesz tooreduce hello całkowity koszt posiadania wdrażania, zarządzania i konserwacji aplikacji szerokość przedsiębiorstwa za pomocą łatwo migracji tych tooMicrosoft aplikacji Azure. Z ASE SAP w maszynie wirtualnej platformy Azure Administratorzy i deweloperzy mogą nadal używać hello tych samych narzędzi programowania i administracji, które są dostępne lokalnie.

Brak umowy SLA dla hello maszynach wirtualnych platformy Azure, które można znaleźć tutaj: <https://azure.microsoft.com/support/legal/sla>

Firma Microsoft upewnieniu się, że Microsoft Azure hostowanej maszyny wirtualnej będzie wykonywać bardzo dobrze porównanie tooother chmury publicznej wirtualizacji oferty, ale wyniki poszczególnych może się różnić. Ustawianie rozmiaru protokoły SAP liczby hello certyfikat różnych SAP jednostki SKU wirtualna znajdzie się w oddzielnych Uwaga SAP SAP [1928533].

Instrukcje i zalecenia w zakresie toohello użycia usługi Azure Storage, wdrożenia SAP maszyn wirtualnych lub SAP monitorowania zastosować toodeployments SAP ASE w połączeniu z aplikacje SAP, jak wspomniano w całym hello pierwsze cztery rozdziałach tego dokumentu.

### <a name="sap-ase-version-support"></a>Obsługa wersji ASE SAP
SAP obecnie obsługuje ASE SAP wersji 16.0 do użycia z programem SAP Business pakiet produktów. Wszystkie aktualizacje serwera SAP ASE lub JDBC i ODBC toobe sterowników używane z SAP Business pakiet produktów są udostępniane wyłącznie przez hello Marketplace usługi SAP w: <https://support.sap.com/swdc>.

Podobnie jak w przypadku instalacji lokalnej bez pobierania aktualizacji dla serwera SAP ASE hello, lub hello JDBC i sterowników ODBC bezpośrednio z witryny sieci Web programu Sybase. Szczegółowe informacje na temat aktualizacji, które są obsługiwane w przypadku użycia z programu SAP Business pakiet produktów lokalnych i w maszynach wirtualnych platformy Azure, zobacz następujące uwagi SAP hello:

* [1590719]
* [1973241]

Ogólne informacje o systemie SAP Business Suite SAP ASE można znaleźć w hello [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Wskazówki dotyczące konfigurowania ASE SAP dla SAP powiązane SAP ASE instalacje w maszynach wirtualnych platformy Azure
#### <a name="structure-of-hello-sap-ase-deployment"></a>Struktura hello wdrożenia SAP ASE
Zgodnie z hello ogólny opis pliki wykonywalne SAP ASE powinna być znajduje się lub zainstalowany na dysku systemowym hello wirtualna hello podstawowy plik VHD (dysk c:\). Zazwyczaj większość hello SAP ASE systemu narzędzi baz danych i są nie naprawdę wykorzystywane twardego przez SAP NetWeaver obciążenia. Dlatego hello systemu i narzędzi baz danych, (master, model, saptools, sybmgmtdb, sybsystemdb) może pozostawać na powitania C:\drive również.

Wystąpił wyjątek może być tymczasowa baza danych hello zawierająca wszystkie tabele pracy i tabel tymczasowych utworzonych przez ASE SAP, które może wymagać większą ilość danych lub woluminu operacji We/Wy, który nie mieści się w oryginalnej hello w przypadku niektórych ERP SAP i wszystkich obciążeń BW Podstawowy dysk VHD maszyny Wirtualnej (dysk c:\).

W zależności od hello używana wersja SAPInst/SWPM tooinstall hello systemu, hello baza danych może zawierać:

* Pojedynczy tempdb SAP ASE, która jest tworzona podczas instalowania programu SAP ASE
* Bazy danych tempdb SAP ASE utworzone przez zainstalowanie SAP ASE i dodatkowe saptempdb utworzone przez hello procedury instalacyjnej SAP
* Bazy danych tempdb SAP ASE utworzone przez zainstalowanie SAP ASE i dodatkowych danych tempdb, który został utworzony ręcznie (np. po Uwaga SAP [1752266]) toomeet ERP/BW tempdb określonych wymagań

W przypadku ERP określonych lub wszystkich obciążeń BW warto, w zakresie tooperformance, urządzenia tempdb hello tookeep hello również utworzyć bazę danych tempdb (przez SWPM lub ręcznie) na dysku innym niż C:\. Jeśli nie dodatkowe tempdb istnieje on zaleca się toocreate jedną (Uwaga SAP [1752266]).

Dla takich systemów hello hello również utworzyć bazę danych tempdb należy przeprowadzić następujące czynności:

* Przenieś hello pierwszy tempdb urządzenia toohello pierwszego urządzenia bazy danych SAP hello
* Dodaj bazę danych tempdb tooeach urządzeń z hello wirtualne dyski twarde zawierające urządzenia bazy danych SAP hello

Ta konfiguracja umożliwia tempdb tooeither używać więcej miejsca niż dysk systemowy hello jest tooprovide stanie. Jako odwołanie jedną Sprawdź hello tempdb urządzenia rozmiary na istniejących systemów, które lokalnie. Lub taka konfiguracja umożliwia liczb IOPS względem bazy danych tempdb, który nie może posiadać hello dysku systemowego. Ponownie systemów, które są uruchomione w siedzibie firmy może być obciążenie toomonitor używane we/wy względem bazy danych tempdb.

Nie wolno umieszczać żadnych urządzeń SAP ASE na powitania dysku D:\ hello maszyny Wirtualnej. Dotyczy to również toohello bazy danych tempdb, nawet jeśli hello obiekty przechowywane w bazie danych tempdb hello są tylko tymczasowe.

#### <a name="impact-of-database-compression"></a>Wpływ kompresji bazy danych
W konfiguracji, gdy przepustowość operacji We/Wy mogą stać się czynnikiem ograniczającym co miar, co zmniejsza liczbę IOPS mogą ułatwić toostretch hello obciążenie, co mogą uruchamiać w scenariuszu IaaS, takich jak Azure. W związku z tym zdecydowanie zaleca się, że kompresja SAP ASE jest używana przed przekazaniem istniejących tooAzure bazy danych SAP toomake.

Kompresja tooperform zalecenie Hello przed przekazaniem tooAzure, jeśli nie jest zaimplementowana znajduje się z kilku powodów:

* Hello ilość danych toobe przekazać tooAzure jest niższa
* czas trwania Hello wykonywania kompresji hello jest krótszy, przy założeniu, że jeden służy silniejszych sprzętu z więcej procesorów ani większą przepustowość operacji We/Wy lub mniej we/wy opóźnień lokalnego
* Mniejsze rozmiary bazy danych może prowadzić tooless kosztów przydział dysku

Kompresji danych i obiektów LOB działa na maszynie wirtualnej hostowanej w maszynach wirtualnych platformy Azure, jak ma lokalnego. Aby uzyskać więcej informacji na temat sposobu używania toocheck, jeśli kompresja jest już w istniejących ASE SAP bazy danych sprawdź, czy Uwaga SAP [1750510].

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>Za pomocą wystąpień bazy danych toomonitor DBACockpit
Dla systemów SAP, które korzystają z programu SAP ASE jako bazy danych platformy hello DBACockpit jest dostępny jako okna przeglądarki osadzony w transakcji DBACockpit lub Webdynpro. Jednak hello pełną funkcjonalność monitorowania i administrowanie hello bazy danych jest dostępny w celu wykonania Webdynpro hello hello DBACockpit tylko.

Z lokalnymi systemów, które są kilka kroków wymaga tooenable wszystkie funkcje programu SAP NetWeaver używane przez implementację Webdynpro hello hello DBACockpit. Wykonaj Uwaga SAP [1245200] tooenable hello użycia webdynpros i generować hello wymagane te. Jeśli poniższe instrukcje hello w hello powyżej notatki, które będą również skonfigurować hello Internet Communication Manager (icm) wraz z programem hello toobe porty używane w przypadku połączeń http i https. ustawienie domyślne Hello http wygląda następująco:

> ICM/server_port_0 = ochronę = HTTP, PORT = 8000, PROCTIMEOUT = 600, limit czasu = 600
>
> ICM/server_port_1 = ochronę = HTTPS i portu 443$ $, PROCTIMEOUT = = 600, limit czasu = 600
>
>

i linki hello generowane w transakcji DBACockpit będzie wyglądać podobnie toothis:

> https://`<fullyqualifiedhostname`>: 44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://`<fullyqualifiedhostname`>: 8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

W zależności od czy i jak hello maszyny wirtualnej Azure hostingu hello systemu SAP jest połączony za pośrednictwem lokacja lokacja, obejmujący wiele lokacji lub ExpressRoute (wdrożenie między lokalizacjami) toomake należy się upewnić tego ICM używa pełni kwalifikowaną nazwę hosta, który można rozwiązać ten problem na powitania komputer, na którym próbujesz tooopen hello DBACockpit z. Zobacz Uwaga SAP [773830] toounderstand sposób określa ICM hello jawnie pełni kwalifikowana nazwa domeny w zależności od parametrów profilu i ustaw parametr icm/host_name_full, jeśli jest to wymagane.

Jeśli wdrożono hello maszyn wirtualnych w scenariuszu tylko w chmurze bez łączności między lokalizacjami między lokalną i platformą Azure, należy toodefine, publiczny adres IP i domainlabel. format Hello hello publicznej nazwy DNS hello maszyny Wirtualnej zostanie następnie wyglądać następująco:

> `<custom domainlabel`>. `<azure region`>. cloudapp.azure.com
>
>

Powiązane więcej szczegółów można znaleźć nazwy DNS toohello [tutaj][virtual-machines-azurerm-versus-azuresm].

Ustawienia systemu hello SAP profilu parametru icm/host_name_full toohello przez nazwę DNS hello Azure VM hello łącza mogą wyglądać podobnie do:

> https://mydomainlabel.westeurope.cloudapp.NET:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://mydomainlabel.westeurope.cloudapp.NET:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

W takim przypadku należy toomake się, że:

* Dodawanie reguł ruchu przychodzącego toohello sieciowej grupy zabezpieczeń w hello Azure Portal hello porty TCP/IP używane toocommunicate z ICM
* Dodawanie reguł ruchu przychodzącego toohello konfiguracji zapory systemu Windows hello TCP/IP używane porty toocommunicate z hello ICM

Dla automatycznego zaimportowane wszystkie dostępne poprawki, zalecane jest tooperiodically zastosować hello korekty kolekcji Uwaga SAP dotyczy tooyour SAP wersji:

* [1558958]
* [1619967]
* [1882376]

Więcej informacji na temat panelu sterowania DBA SAP ASE znajdują się w powitania po SAP uwagi:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Uwagi dotyczące tworzenia kopii zapasowej i odzyskiwania dla programu SAP ASE
W przypadku wdrażania SAP ASE do platformy Azure z kopii zapasowej metodologii musi przejrzeć. Nawet jeśli hello systemu nie jest systemów produkcyjnych, hello SAP obsługiwanych przez SAP ASE musi być kopię zapasową bazy danych okresowo. Ponieważ Magazyn Azure przechowuje trzy obrazy, jest teraz mniej ważne w zakresie toocompensating awarii magazynu kopii zapasowej. Hello główną przyczyną utrzymania właściwego planu tworzenia kopii zapasowej i przywracania jest więcej, który można kompensowane błędy logiczne/ręczny, zapewniając punktu w czasie możliwości odzyskiwania. Dzięki hello celem jest tooeither użyj kopii zapasowych toorestore hello kopii bazy danych tooa niektórych punktu w czasie lub toouse kopie zapasowe hello w Azure tooseed innego systemu przez skopiowanie hello istniejącej bazy danych. Na przykład można zostaną przeniesione z warstwy 2 SAP tooa systemu 3-warstwowej ustawienia konfiguracji hello sam systemu przez Przywracanie kopii zapasowej.

Wykonywanie kopii zapasowych i przywracanie bazy danych w programie Azure works hello sam sposób jak lokalnie. Zobacz uwagi SAP:

* [1588316]
* [1585981]

Aby uzyskać więcej informacji na temat tworzenia zrzutu konfiguracji i planowania kopii zapasowych. W zależności od Twoich potrzeb, które można skonfigurować i strategii bazy danych i dziennika zrzuty toodisk na jedną hello istniejące pliki VHD lub Dodaj dodatkowe VHD hello kopii zapasowej.  tooreduce hello ryzyka utraty danych w przypadku błędu jest zalecane toouse dysku VHD, w którym znajduje się żadnego urządzenia bazy danych.

Oprócz danych i obiektów LOB kompresji SAP ASE oferuje również kompresja kopii zapasowej. toooccupy mniej miejsca na powitania bazy danych i dziennika zrzuty go zaleca się toouse kompresja kopii zapasowej. Zobacz Uwaga SAP [1588316] Aby uzyskać więcej informacji. Kompresja kopii zapasowej hello jest również istotne tooreduce hello ilość toobe dane przesyłane, jeśli planujesz toodownload kopii zapasowych lub wirtualne dyski twarde zawierające zrzuty kopii zapasowej z hello tooon lokalnej maszyny wirtualnej platformy Azure.

Nie należy używać dysku D:\ jako miejsce docelowe zrzutu bazy danych lub dziennika.

#### <a name="performance-considerations-for-backupsrestores"></a>Zagadnienia dotyczące wydajności dla kopii zapasowych/przywracania
Jak wdrożenia bez systemu operacyjnego wydajności tworzenia kopii zapasowej i przywracania jest zależna od mogą być odczytywane jak wiele woluminów równolegle i jakie przepływności hello tych woluminów mogą być. Ponadto hello użycie procesora CPU używanych przez kompresję kopii zapasowych może odtworzyć istotną rolę na maszynach wirtualnych z właśnie too8 wątków procesora CPU. W związku z tym co można założyć:

* Witaj mniej hello liczba wirtualnych dysków twardych używanych toostore hello bazy danych urządzeń, hello mniejszych hello ogólną przepustowość podczas odczytywania
* Witaj mniejszą liczbę hello wątków procesora CPU w hello maszyny Wirtualnej, hello poważniejsze wpływ hello kompresja kopii zapasowej
* Witaj mniejszą liczbę elementów docelowych (Stripe katalogów, wirtualne dyski twarde) toowrite hello kopii zapasowej, hello mniejszym przepływności hello

tooincrease hello liczbę elementów docelowych toowrite toothere są dwie opcje, które mogą być używane/łączone w zależności od potrzeb:

* Stosowanie hello wolumin docelowy kopii zapasowej za pośrednictwem wielu wirtualnych dysków twardych zainstalowanych w kolejności tooimprove hello IOPS przepływności na tym woluminie rozłożonego
* Tworzenie zrzutu konfiguracji na poziomie SAP ASE, który używa więcej niż jeden docelowy katalogu toowrite hello zrzutu do

Stosowanie woluminu przez kilka zainstalowanych dysków VHD został omówiony we wcześniejszej części tego przewodnika. Aby uzyskać więcej informacji na temat używania wielu katalogów w hello SAP ASE zrzutu konfiguracji można znaleźć w dokumentacji toohello na sp_config_dump procedury składowanej, która jest używana toocreate hello zrzutu konfiguracji na powitania [Sybase Centrum informacyjne](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Odzyskiwanie po awarii z maszynami wirtualnymi platformy Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Replikacja danych z serwerem replikacji programu Sybase SAP
Z hello ASE SAP SAP Sybase replikacji serwera (SRS) umożliwia ciepłych rozwiązania rezerwy tootransfer bazy danych transakcji tooa oddalonych asynchronicznie.

Witaj instalacji i działania SRS działa również funkcjonalnie hostowane w usługach maszyny wirtualnej Azure, jak lokalnej maszyny Wirtualnej.

HADR ASE za pośrednictwem serwera replikacji SAP jest zaplanowane z przyszłych wersji. Zostanie ono przetestowana i wydane dla platformy Microsoft Azure, jak jest dostępny.

## <a name="specifics-toosap-ase-on-linux"></a>Szczegóły tooSAP ASE w systemie Linux
Począwszy od programu Microsoft Azure, możesz łatwo przeprowadzić migrację z istniejącej aplikacji SAP ASE tooAzure maszyn wirtualnych. SAP ASE na maszynie wirtualnej umożliwia możesz tooreduce hello całkowity koszt posiadania wdrażania, zarządzania i konserwacji aplikacji szerokość przedsiębiorstwa za pomocą łatwo migracji tych tooMicrosoft aplikacji Azure. Z ASE SAP w maszynie wirtualnej platformy Azure Administratorzy i deweloperzy mogą nadal używać hello tych samych narzędzi programowania i administracji, które są dostępne lokalnie.

Do wdrażania maszyn wirtualnych platformy Azure, jego ważne tooknow hello oficjalnego umów SLA, które można znaleźć tutaj: <https://azure.microsoft.com/support/legal/sla>

Informacje dotyczące zmiany rozmiaru SAP oraz listę SAP certyfikowane jednostki SKU maszyny Wirtualnej zostanie podany w Uwaga SAP [1928533]. Dodatkowe SAP zmiany rozmiaru dokumentów dla maszyn wirtualnych Azure można znaleźć tutaj <http://blogs.msdn.com/b/saponsqlserver/archive/2015/06/19/how-to-size-sap-systems-running-on-azure-vms.aspx> i tutaj <http : //blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>

Instrukcje i zalecenia w zakresie toohello użycia usługi Azure Storage, wdrożenia SAP maszyn wirtualnych lub SAP monitorowania zastosować toodeployments SAP ASE w połączeniu z aplikacje SAP, jak wspomniano w całym hello pierwsze cztery rozdziałach tego dokumentu.

Witaj następujące dwie notatki SAP zawierają ogólne informacje o ASE w systemie Linux i ASE w hello chmury:

* [2134316]
* [1941500]

### <a name="sap-ase-version-support"></a>Obsługa wersji ASE SAP
SAP obecnie obsługuje ASE SAP wersji 16.0 do użycia z programem SAP Business pakiet produktów. Wszystkie aktualizacje serwera SAP ASE lub JDBC i ODBC toobe sterowników używane z SAP Business pakiet produktów są udostępniane wyłącznie przez hello Marketplace usługi SAP w: <https://support.sap.com/swdc>.

Podobnie jak w przypadku instalacji lokalnej bez pobierania aktualizacji dla serwera SAP ASE hello, lub hello JDBC i sterowników ODBC bezpośrednio z witryny sieci Web programu Sybase. Szczegółowe informacje na temat aktualizacji, które są obsługiwane w przypadku użycia z programu SAP Business pakiet produktów lokalnych i w maszynach wirtualnych platformy Azure, zobacz następujące uwagi SAP hello:

* [1590719]
* [1973241]

Ogólne informacje o systemie SAP Business Suite SAP ASE można znaleźć w hello [SCN](https://scn.sap.com/community/ase)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Wskazówki dotyczące konfigurowania ASE SAP dla SAP powiązane SAP ASE instalacje w maszynach wirtualnych platformy Azure
#### <a name="structure-of-hello-sap-ase-deployment"></a>Struktura hello wdrożenia SAP ASE
Zgodnie z hello ogólny opis pliki wykonywalne SAP ASE powinien znajduje się lub zainstalowane w systemie plików głównego hello hello maszyny Wirtualnej (/sybase). Zazwyczaj większość hello SAP ASE systemu narzędzi baz danych i są nie naprawdę wykorzystywane twardego przez SAP NetWeaver obciążenia. Dlatego hello systemu i narzędzi baz danych, (master, model, saptools, sybmgmtdb, sybsystemdb) może pozostawać w systemie plików głównego hello również.

Wystąpił wyjątek może być tymczasowa baza danych hello zawierająca wszystkie tabele pracy i tabel tymczasowych utworzonych przez ASE SAP, które może wymagać większą ilość danych lub woluminu operacji We/Wy, który nie mieści się w oryginalnej hello w przypadku niektórych ERP SAP i wszystkich obciążeń BW Dysk systemu operacyjnego maszyny Wirtualnej.

W zależności od hello używana wersja SAPInst/SWPM tooinstall hello systemu, hello baza danych może zawierać:

* Pojedynczy tempdb SAP ASE, która jest tworzona podczas instalowania programu SAP ASE
* Bazy danych tempdb SAP ASE utworzone przez zainstalowanie SAP ASE i dodatkowe saptempdb utworzone przez hello procedury instalacyjnej SAP
* Bazy danych tempdb SAP ASE utworzone przez zainstalowanie SAP ASE i dodatkowych danych tempdb, który został utworzony ręcznie (np. po Uwaga SAP [1752266]) toomeet ERP/BW tempdb określonych wymagań

W przypadku ERP określonych lub wszystkich obciążeń BW warto, w zakresie tooperformance, urządzenia tempdb hello tookeep hello również utworzone bazy danych tempdb (przez SWPM lub ręcznie) w systemie oddzielny plik, który może być reprezentowany przez dysk pojedynczy danych platformy Azure lub RAID systemu Linux Rozciąganie na wiele dysków danych Azure. Jeśli nie dodatkowe tempdb istnieje on zaleca się toocreate jedną (Uwaga SAP [1752266]).

Dla takich systemów hello hello również utworzyć bazę danych tempdb należy przeprowadzić następujące czynności:

* Przenieś hello pierwszy tempdb katalogu toohello pierwszy system plików bazy danych SAP hello
* Dodaj bazę danych tempdb tooeach katalogi z dysków VHD zawierającego system plików bazy danych SAP hello hello

Ta konfiguracja umożliwia tempdb tooeither używać więcej miejsca niż dysk systemowy hello jest tooprovide stanie. Jako odwołanie jedną Sprawdź hello tempdb katalogu rozmiary na istniejących systemów, które lokalnie. Lub taka konfiguracja umożliwia liczb IOPS względem bazy danych tempdb, który nie może posiadać hello dysku systemowego. Ponownie systemów, które są uruchomione w siedzibie firmy może być obciążenie toomonitor używane we/wy względem bazy danych tempdb.

Nie wolno umieszczać wszelkich katalogów SAP ASE do katalogu/mnt lub /mnt/resource hello maszyny Wirtualnej. Dotyczy to również toohello bazy danych tempdb, nawet jeśli hello obiekty przechowywane w bazie danych tempdb hello są tylko tymczasowego, ponieważ katalogu/mnt lub /mnt/resource jest domyślna maszyny Wirtualnej Azure tymczasowego miejsca, który nie jest trwały. Więcej informacji na temat hello miejsca tymczasowego maszyny Wirtualnej platformy Azure można znaleźć w [w tym artykule][virtual-machines-linux-how-to-attach-disk]

#### <a name="impact-of-database-compression"></a>Wpływ kompresji bazy danych
W konfiguracji, gdy przepustowość operacji We/Wy mogą stać się czynnikiem ograniczającym co miar, co zmniejsza liczbę IOPS mogą ułatwić toostretch hello obciążenie, co mogą uruchamiać w scenariuszu IaaS, takich jak Azure. W związku z tym zdecydowanie zaleca się, że kompresja SAP ASE jest używana przed przekazaniem istniejących tooAzure bazy danych SAP toomake.

Kompresja tooperform zalecenie Hello przed przekazaniem tooAzure, jeśli nie jest zaimplementowana znajduje się z kilku powodów:

* Hello ilość danych toobe przekazać tooAzure jest niższa
* czas trwania Hello wykonywania kompresji hello jest krótszy, przy założeniu, że jeden służy silniejszych sprzętu z więcej procesorów ani większą przepustowość operacji We/Wy lub mniej we/wy opóźnień lokalnego
* Mniejsze rozmiary bazy danych może prowadzić tooless kosztów przydział dysku

Kompresji danych i obiektów LOB działa na maszynie wirtualnej hostowanej w maszynach wirtualnych platformy Azure, jak ma lokalnego. Aby uzyskać więcej informacji na temat sposobu używania toocheck, jeśli kompresja jest już w istniejących ASE SAP bazy danych sprawdź, czy Uwaga SAP [1750510]. Zobacz też Uwaga SAP [2121797] Aby uzyskać dodatkowe informacje dotyczące kompresji bazy danych.

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>Za pomocą wystąpień bazy danych toomonitor DBACockpit
Dla systemów SAP, które korzystają z programu SAP ASE jako bazy danych platformy hello DBACockpit jest dostępny jako okna przeglądarki osadzony w transakcji DBACockpit lub Webdynpro. Jednak hello pełną funkcjonalność monitorowania i administrowanie hello bazy danych jest dostępny w celu wykonania Webdynpro hello hello DBACockpit tylko.

Z lokalnymi systemów, które są kilka kroków wymaga tooenable wszystkie funkcje programu SAP NetWeaver używane przez implementację Webdynpro hello hello DBACockpit. Wykonaj Uwaga SAP [1245200] tooenable hello użycia webdynpros i generować hello wymagane te. Jeśli poniższe instrukcje hello w hello powyżej notatki, które będą również skonfigurować hello Internet Communication Manager (icm) wraz z programem hello toobe porty używane w przypadku połączeń http i https. ustawienie domyślne Hello http wygląda następująco:

> ICM/server_port_0 = ochronę = HTTP, PORT = 8000, PROCTIMEOUT = 600, limit czasu = 600
>
> ICM/server_port_1 = ochronę = HTTPS i portu 443$ $, PROCTIMEOUT = = 600, limit czasu = 600
>
>

i linki hello generowane w transakcji DBACockpit będzie wyglądać podobnie toothis:

> https://`<fullyqualifiedhostname`>: 44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://`<fullyqualifiedhostname`>: 8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

W zależności od czy i jak hello maszyny wirtualnej Azure hostingu hello systemu SAP jest połączony za pośrednictwem lokacja lokacja, obejmujący wiele lokacji lub ExpressRoute (wdrożenie między lokalizacjami) toomake należy się upewnić tego ICM używa pełni kwalifikowaną nazwę hosta, który można rozwiązać ten problem na powitania komputer, na którym próbujesz tooopen hello DBACockpit z. Zobacz Uwaga SAP [773830] toounderstand sposób określa ICM hello jawnie pełni kwalifikowana nazwa domeny w zależności od parametrów profilu i ustaw parametr icm/host_name_full, jeśli jest to wymagane.

Jeśli wdrożono hello maszyn wirtualnych w scenariuszu tylko w chmurze bez łączności między lokalizacjami między lokalną i platformą Azure, należy toodefine, publiczny adres IP i domainlabel. format Hello hello publicznej nazwy DNS hello maszyny Wirtualnej zostanie następnie wyglądać następująco:

> `<custom domainlabel`>. `<azure region`>. cloudapp.azure.com
>
>

Powiązane więcej szczegółów można znaleźć nazwy DNS toohello [tutaj][virtual-machines-azurerm-versus-azuresm].

Ustawienia systemu hello SAP profilu parametru icm/host_name_full toohello przez nazwę DNS hello Azure VM hello łącza mogą wyglądać podobnie do:

> https://mydomainlabel.westeurope.cloudapp.NET:44300/sap/bc/webdynpro/sap/dba_cockpit
>
> http://mydomainlabel.westeurope.cloudapp.NET:8000/sap/bc/webdynpro/sap/dba_cockpit
>
>

W takim przypadku należy toomake się, że:

* Dodawanie reguł ruchu przychodzącego toohello sieciowej grupy zabezpieczeń w hello Azure Portal hello porty TCP/IP używane toocommunicate z ICM
* Dodawanie reguł ruchu przychodzącego toohello konfiguracji zapory systemu Windows hello TCP/IP używane porty toocommunicate z hello ICM

Dla automatycznego zaimportowane wszystkie dostępne poprawki, zalecane jest tooperiodically zastosować hello korekty kolekcji Uwaga SAP dotyczy tooyour SAP wersji:

* [1558958]
* [1619967]
* [1882376]

Więcej informacji na temat panelu sterowania DBA SAP ASE znajdują się w powitania po SAP uwagi:

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Uwagi dotyczące tworzenia kopii zapasowej i odzyskiwania dla programu SAP ASE
W przypadku wdrażania SAP ASE do platformy Azure z kopii zapasowej metodologii musi przejrzeć. Nawet jeśli hello systemu nie jest systemów produkcyjnych, hello SAP obsługiwanych przez SAP ASE musi być kopię zapasową bazy danych okresowo. Ponieważ Magazyn Azure przechowuje trzy obrazy, jest teraz mniej ważne w zakresie toocompensating awarii magazynu kopii zapasowej. Hello główną przyczyną utrzymania właściwego planu tworzenia kopii zapasowej i przywracania jest więcej, który można kompensowane błędy logiczne/ręczny, zapewniając punktu w czasie możliwości odzyskiwania. Dzięki hello celem jest tooeither użyj kopii zapasowych toorestore hello kopii bazy danych tooa niektórych punktu w czasie lub toouse kopie zapasowe hello w Azure tooseed innego systemu przez skopiowanie hello istniejącej bazy danych. Na przykład można zostaną przeniesione z warstwy 2 SAP tooa systemu 3-warstwowej ustawienia konfiguracji hello sam systemu przez Przywracanie kopii zapasowej.

Wykonywanie kopii zapasowych i przywracanie bazy danych w programie Azure works hello sam sposób jak lokalnie. Zobacz uwagi SAP:

* [1588316]
* [1585981]

Aby uzyskać więcej informacji na temat tworzenia zrzutu konfiguracji i planowania kopii zapasowych. W zależności od Twoich potrzeb, które można skonfigurować i strategii bazy danych i dziennika zrzuty toodisk na jedną hello istniejące pliki VHD lub Dodaj dodatkowe VHD hello kopii zapasowej.  tooreduce hello ryzyka utraty danych w przypadku błędu jest zalecane toouse dysku VHD, w którym znajduje się nie bazy danych pliku lub katalogu.

Oprócz danych i obiektów LOB kompresji SAP ASE oferuje również kompresja kopii zapasowej. toooccupy mniej miejsca na powitania bazy danych i dziennika zrzuty go zaleca się toouse kompresja kopii zapasowej. Zobacz Uwaga SAP [1588316] Aby uzyskać więcej informacji. Kompresja kopii zapasowej hello jest również istotne tooreduce hello ilość toobe dane przesyłane, jeśli planujesz toodownload kopii zapasowych lub wirtualne dyski twarde zawierające zrzuty kopii zapasowej z hello tooon lokalnej maszyny wirtualnej platformy Azure.

Nie używaj hello Azure VM miejsca tymczasowego katalogu/mnt lub /mnt/resource jako miejsce docelowe zrzutu bazy danych lub dziennika.

#### <a name="performance-considerations-for-backupsrestores"></a>Zagadnienia dotyczące wydajności dla kopii zapasowych/przywracania
Jak wdrożenia bez systemu operacyjnego wydajności tworzenia kopii zapasowej i przywracania jest zależna od mogą być odczytywane jak wiele woluminów równolegle i jakie przepływności hello tych woluminów mogą być. Ponadto hello użycie procesora CPU używanych przez kompresję kopii zapasowych może odtworzyć istotną rolę na maszynach wirtualnych z właśnie too8 wątków procesora CPU. W związku z tym co można założyć:

* Witaj mniej hello liczba wirtualnych dysków twardych używanych toostore hello bazy danych urządzeń, hello mniejszych hello ogólną przepustowość podczas odczytywania
* Witaj mniejszą liczbę hello wątków procesora CPU w hello maszyny Wirtualnej, hello poważniejsze wpływ hello kompresja kopii zapasowej
* Hello mniej toowrite elementów docelowych (Linux oprogramowaniem RAID, wirtualne dyski twarde) hello tworzenie kopii zapasowych, hello mniejszym przepływności hello

tooincrease hello liczbę elementów docelowych toowrite toothere są dwie opcje, które mogą być używane/łączone w zależności od potrzeb:

* Stosowanie hello wolumin docelowy kopii zapasowej za pośrednictwem wielu wirtualnych dysków twardych zainstalowanych w kolejności tooimprove hello IOPS przepływności na tym woluminie rozłożonego
* Tworzenie zrzutu konfiguracji na poziomie SAP ASE, który używa więcej niż jeden docelowy katalogu toowrite hello zrzutu do

Stosowanie woluminu przez kilka zainstalowanych dysków VHD został omówiony we wcześniejszej części tego przewodnika. Aby uzyskać więcej informacji na temat używania wielu katalogów w hello SAP ASE zrzutu konfiguracji można znaleźć w dokumentacji toohello na sp_config_dump procedury składowanej, która jest używana toocreate hello zrzutu konfiguracji na powitania [Sybase Centrum informacyjne](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Odzyskiwanie po awarii z maszynami wirtualnymi platformy Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Replikacja danych z serwerem replikacji programu Sybase SAP
Z hello ASE SAP SAP Sybase replikacji serwera (SRS) umożliwia ciepłych rozwiązania rezerwy tootransfer bazy danych transakcji tooa oddalonych asynchronicznie.

Witaj instalacji i działania SRS działa również funkcjonalnie hostowane w usługach maszyny wirtualnej Azure, jak lokalnej maszyny Wirtualnej.

HADR ASE za pośrednictwem SAP replikacji serwera nie jest obsługiwany w tym momencie. Może być przetestowana i wydane dla platformy Microsoft Azure w przyszłości hello.

## <a name="specifics-toooracle-database-on-windows"></a>Szczegóły tooOracle bazy danych w systemie Windows
Ponieważ midyear 2013 oprogramowanie Oracle jest obsługiwana przez toorun Oracle w funkcji Hyper-V systemu Microsoft Windows i na platformie Azure. Przeczytaj ten artykuł tooget więcej informacji dotyczących obsługi ogólne hello funkcji Hyper-V systemu Windows i Azure przez firmę Oracle: <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces>

Następujące hello ogólną pomoc techniczną hello danego scenariusza aplikacji SAP wykorzystaniu Oracle — bazy danych jest obsługiwana także. Szczegółowe informacje są o nazwie w tej części hello dokumentu.

### <a name="oracle-version-support"></a>Obsługa wersji programu Oracle
Wszystkie szczegółowe informacje o wersji programu Oracle i odpowiednie wersje systemu operacyjnego, które są obsługiwane dla systemie SAP Oracle na maszynach wirtualnych platformy Azure można znaleźć w powitania po Uwaga SAP [2039619]

Ogólne informacje o systemie SAP Business Suite Oracle można znaleźć w SCN: <https://scn.sap.com/community/oracle>

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Wskazówki dotyczące konfigurowania programu Oracle dla instalacji programu SAP w maszynach wirtualnych platformy Azure
#### <a name="storage-configuration"></a>Konfiguracja usługi Storage
Tylko jednego wystąpienia obsługiwany Oracle przy użyciu dysków sformatowanym w systemie NTFS. Wszystkie pliki bazy danych muszą być przechowywane w systemie plików NTFS hello oparte na dyskach VHD. Te wirtualne dyski twarde są zainstalowane toohello maszyny Wirtualnej platformy Azure i są oparte na magazyn obiektów BLOB Azure strony (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Dowolny dyski sieciowe lub zdalnych udziałów, takich jak usługi Azure plików:

* <https://blogs.msdn.com/b/windowsazurestorage/Archive/2014/05/12/Introducing-Microsoft-Azure-File-Service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/Archive/2014/05/27/persisting-Connections-to-Microsoft-Azure-Files.aspx>

są **nie** obsługiwane dla plików bazy danych programu Oracle!

Za pomocą dysków VHD Azure oparte na magazyn obiektów BLOB Azure strony, hello instrukcji zawartych w tym dokumencie w rozdziale [buforowanie maszyny wirtualne i wirtualne dyski twarde] [ dbms-guide-2.1] i [magazyn Microsoft Azure] [ dbms-guide-2.3] Zastosuj toodeployments z również hello baz danych programu Oracle.

Jak opisano wcześniej w głównej części dokumentu hello hello, przydziały na przepływność IOPS dla wirtualnych dysków twardych Azure istnieje. dokładne przydziały Hello w zależności od typu maszyny Wirtualnej hello służą. Znajduje się lista typów maszyny Wirtualnej z przydziałami ich [tutaj][virtual-machines-sizes]

Witaj tooidentify obsługiwane typy maszyny Wirtualnej platformy Azure, zobacz Uwaga tooSAP [1928533]

Tak długo, jak hello limit przydziału IOPS dla każdego dysku spełnia wymogi hello, jest możliwe toostore wszystkie pliki hello bazy danych na jednym jeden zainstalowany Azure wirtualnego dysku twardego.

Jeśli wymaganych jest więcej IOPS, zdecydowanie zalecane jest toouse pule magazynów okna (tylko dostępne w systemie Windows Server 2012 i nowsze) lub stosowanie dla systemu Windows 2008 R2 toocreate jeden duży urządzenia logicznego przez wiele dysków VHD zainstalowanych z systemem Windows. Zobacz też rozdział [RAID oprogramowania] [ dbms-guide-2.2] tego dokumentu. Takie podejście upraszcza hello administracji narzutów toomanage hello miejsca i pozwala uniknąć nakładu hello toomanually rozpowszechniają wielu wirtualnych dysków twardych zainstalowanych plików.

#### <a name="backup--restore"></a>Wykonywanie kopii zapasowych i ich przywracanie
Do utworzenia kopii zapasowej / przywrócenia jej funkcjonalności, hello SAP BR * narzędzia Oracle są obsługiwane w hello sam sposób jak w standardowe systemów operacyjnych Windows Server i Hyper-V. Menedżer odzyskiwania Oracle (RMAN) jest również obsługiwane dla toodisk kopii zapasowych i przywracanie z dysku.

#### <a name="high-availability"></a>Wysoka dostępność
[comment]: <> (łącze tooASM)
Oracle Data Guard jest obsługiwana dla zapewnienia wysokiej dostępności i celów odzyskiwania po awarii. Szczegółowe informacje znajdują się w [to] [ virtual-machines-windows-classic-configure-oracle-data-guard] dokumentacji.

#### <a name="other"></a>Inne
Wszystkie inne tematy ogólne jak zestawami dostępności Azure lub SAP monitorowania stosowane zgodnie z opisem w hello pierwsze trzy rozdziałach tego dokumentu w przypadku wdrożeń maszyn wirtualnych z hello również bazą danych Oracle.

## <a name="specifics-for-hello-sap-maxdb-database-on-windows"></a>Charakterystyka hello SAP MaxDB z bazy danych w systemie Windows
### <a name="sap-maxdb-version-support"></a>Obsługa wersji MaxDB SAP
SAP obecnie obsługuje MaxDB SAP wersji 7,9 do użycia z programem SAP NetWeaver na podstawie produktów na platformie Azure. Wszystkie aktualizacje serwera SAP MaxDB lub JDBC i ODBC toobe sterowników używane z produktów na podstawie SAP NetWeaver są udostępniane wyłącznie przez hello Marketplace usługi SAP w <https://support.sap.com/swdc>.
Ogólne informacje o systemie SAP NetWeaver SAP MaxDB można znaleźć w folderze <https://scn.sap.com/community/maxdb>.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-maxdb-dbms"></a>Obsługiwane typy wersji systemu Windows firmy Microsoft i maszyny Wirtualnej platformy Azure dla systemu DBMS MaxDB SAP
wersja Microsoft Windows hello obsługiwane toofind dla systemu DBMS MaxDB SAP na platformie Azure, zobacz:

* [Macierz dostępności produktu SAP (PAM)][sap-pam]
* Uwaga SAP [1928533]

Zdecydowanie zaleca toouse hello najnowsza wersja hello systemu operacyjnego Microsoft Windows, który jest Microsoft Windows 2012 R2.

### <a name="available-sap-maxdb-documentation"></a>Dokumentacja MaxDB dostępne SAP
Hello zaktualizować listę dokumentacji SAP MaxDB można znaleźć w powitania po Uwaga SAP [767598 ]

### <a name="sap-maxdb-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Wskazówki dotyczące konfigurowania MaxDB SAP SAP instalacji na maszynach wirtualnych platformy Azure
#### <a name="b48cfe3b-48e9-4f5b-a783-1d29155bd573"></a>Konfiguracja magazynu
Najlepsze rozwiązania magazynu Azure dla programu SAP MaxDB wykonaj ogólne zalecenia hello wymienionych w rozdziale [struktury wdrożenia RDBMS][dbms-guide-2].

> [!IMPORTANT]
> Podobnie jak innych baz danych SAP MaxDB ma plików danych i dziennika. Jednak w terminologii SAP MaxDB termin poprawne hello jest "wolumin" (nie "plik"). Na przykład istnieją SAP MaxDB woluminów danych i woluminy dziennika. Nie należy mylić tych woluminów dysku systemu operacyjnego.
>
>

Innymi słowy należy:

* Ustaw konto magazynu Azure hello przechowujący hello SAP MaxDB danych i dziennika woluminów (np. pliki) zbyt**lokalny magazyn geograficznie nadmiarowy (LRS)** jak określono w rozdziale [magazyn Microsoft Azure] [ dbms-guide-2.3].
* Ścieżka we/wy oddzielne hello SAP MaxDB woluminy danych (np. pliki) ze ścieżki we/wy hello woluminy dziennika (np. plików). Oznacza to, że woluminy danych SAP MaxDB (np. pliki) mają toobe zainstalowane na jednym dysku logicznego, a woluminy dziennika SAP MaxDB (np. pliki) mają toobe zainstalowany na innym dysku logicznego.
* Ustawianie hello prawidłowego pliku buforowania dla poszczególnych obiektów blob platformy Azure, w zależności od tego, czy używać go SAP MaxDB danych lub dziennika woluminów (np. plików) i używać usługi Azure Standard lub Premium usługi Azure Storage, zgodnie z opisem w rozdziale [buforowania dla maszyn wirtualnych] [ dbms-guide-2.1].
* Tak długo, jak hello limit przydziału IOPS dla każdego dysku spełnia wymogi hello, jest możliwe toostore wszystkie woluminy danych hello na jednym zainstalowanego dysku VHD Azure, a także przechowywać wszystkie woluminy dziennika bazy danych na inny jednego zainstalowanego Azure dysku VHD.
* Jeśli wymaganych jest więcej IOPS i/lub miejsca, zalecane jest toouse Microsoft okna pule magazynów (tylko dostępne w systemie Microsoft Windows Server 2012 i nowsze) lub Microsoft Windows stosowanie dla systemu Microsoft Windows 2008 R2 toocreate jeden duży urządzenie logiczne przez wiele dysków zainstalowanych wirtualnego dysku twardego. Zobacz też rozdział [RAID oprogramowania] [ dbms-guide-2.2] tego dokumentu. Takie podejście upraszcza hello administracji narzutów toomanage hello miejsca i pozwala uniknąć wysiłku hello ręcznie dystrybucję plików kilka zainstalowanych dysków wirtualnych.
* Dla hello najwyższe wymagania IOPS można użyć usługi Azure Premium Storage, który jest dostępny na serii DS i GS-series maszyn wirtualnych.

![Odwołanie do konfiguracji IaaS maszyny Wirtualnej platformy Azure dla systemu DBMS MaxDB SAP][dbms-guide-figure-600]

#### <a name="23c78d3b-ca5a-4e72-8a24-645d141a3f5d"></a>Kopia zapasowa i przywracanie
W przypadku wdrażania SAP MaxDB do platformy Azure, należy przejrzeć z metody tworzenia kopii zapasowej. Nawet jeśli hello systemu nie jest systemów produkcyjnych, hello SAP obsługiwanych przez SAP MaxDB musi być kopię zapasową bazy danych okresowo. Ponieważ usługa Azure Storage chroni trzy obrazy, kopia zapasowa jest teraz mniej ważne w zakresie ochrony systemu przed błąd magazynu i ważniejsze awariami operacyjne lub administracyjnych. Witaj główną przyczyną utrzymywania odpowiednich kopii zapasowej i przywracania plan jest, aby można kompensowane błędy logiczne, czy ręcznie, zapewniając możliwości punktu w czasie odzyskiwania. Dzięki hello celem jest tooeither użyj kopii zapasowych toorestore hello bazy danych tooa niektórych punktu w czasie lub toouse kopie zapasowe hello w Azure tooseed innego systemu przez skopiowanie hello istniejącej bazy danych. Na przykład można zostaną przeniesione z warstwy 2 SAP tooa systemu 3-warstwowej ustawienia konfiguracji hello sam systemu przez Przywracanie kopii zapasowej.

Tworzenie kopii zapasowej i przywracanie bazy danych w hello Azure działa sam sposób jak w przypadku systemów lokalnych, dzięki czemu można używać standardowych MaxDB SAP kopii zapasowych/przywracania narzędzia, opisane w jednym hello SAP MaxDB dokumentacji dokumentów na liście Uwaga SAP [767598 ].

#### <a name="77cd2fbb-307e-4cbf-a65f-745553f72d2c"></a>Zagadnienia dotyczące wydajności tworzenia kopii zapasowych i przywracania
Jak wdrożenia bez systemu operacyjnego wydajności tworzenia kopii zapasowej i przywracania jest zależna od liczby woluminy mogą być odczytywane w równolegle i hello przepływności tych woluminów. Ponadto hello użycie procesora CPU używanych przez kompresja kopii zapasowej można odtworzyć istotną rolę na maszynach wirtualnych z too8 wątków procesora CPU. W związku z tym co można założyć:

* Witaj mniej hello liczbę dysków VHD używana toostore hello bazy danych urządzeń, hello niższe hello ogólną przepustowość do odczytu
* Witaj mniejszą liczbę hello wątków procesora CPU w hello maszyny Wirtualnej, hello poważniejsze wpływ hello kompresja kopii zapasowej
* Witaj mniejszą liczbę elementów docelowych (Stripe katalogów, wirtualne dyski twarde) toowrite hello kopii zapasowej, hello niższe hello przepływności

tooincrease hello liczbę elementów docelowych toowrite do, dostępne są dwie opcje, których można, prawdopodobnie w połączeniu, w zależności od potrzeb:

* Przypisywanie oddzielnych woluminach kopii zapasowej
* Stosowanie hello wolumin docelowy kopii zapasowej za pośrednictwem wielu wirtualnych dysków twardych zainstalowanych w kolejności tooimprove hello IOPS przepływności na wolumin na dysku rozłożonego
* O oddzielnych dedykowanych dysku logicznego urządzeń:
  * SAP MaxDB woluminach kopii zapasowej (tj. pliki)
  * SAP MaxDB woluminy danych (np. pliki)
  * SAP woluminy dziennika MaxDB (np. pliki)

Stosowanie woluminu przez kilka zainstalowanych dysków VHD został omówiony wcześniej w rozdziale [RAID oprogramowania] [ dbms-guide-2.2] tego dokumentu.

#### <a name="f77c1436-9ad8-44fb-a331-8671342de818"></a>Inne
Wszystkie inne tematy ogólne takich jak monitorowanie zestawami dostępności Azure lub SAP mają również zastosowanie, zgodnie z opisem w hello pierwsze trzy rozdziałach tego dokumentu w przypadku wdrożeń maszyn wirtualnych z bazy danych SAP MaxDB hello.
Inne ustawienia specyficzne dla programu SAP MaxDB przezroczysty tooAzure maszyn wirtualnych i są opisane w różnych dokumentach wymienionych w Uwaga SAP [767598 ] w te informacje SAP:

* [826037]
* [1139904]
* [1173395]

## <a name="specifics-for-sap-livecache-on-windows"></a>Charakterystyka liveCache SAP w systemie Windows
### <a name="sap-livecache-version-support"></a>LiveCache SAP Obsługa wersji
Minimalną wersję liveCache SAP obsługiwane w maszynach wirtualnych platformy Azure jest **SAP LC/LCAPPS 10.0 SP 25** tym **liveCache 7.9.08.31** i **25 Znajdowania kompilacji**, wydane dla **EhP 2 dla programu SAP SCM 7.0** i wyższych.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-livecache-dbms"></a>Obsługiwane typy wersji systemu Windows firmy Microsoft i maszyny Wirtualnej platformy Azure dla programu SAP liveCache DBMS
wersja Microsoft Windows hello obsługiwane toofind liveCache SAP na platformie Azure, zobacz:

* [Macierz dostępności produktu SAP (PAM)][sap-pam]
* Uwaga SAP [1928533]

Zdecydowanie zaleca toouse hello najnowsza wersja hello systemu operacyjnego Microsoft Windows, który jest Microsoft Windows 2012 R2.

### <a name="sap-livecache-configuration-guidelines-for-sap-installations-in-azure-vms"></a>LiveCache SAP wskazówki dotyczące konfigurowania dla instalacji programu SAP w maszynach wirtualnych platformy Azure
#### <a name="recommended-azure-vm-types"></a>Zalecane typy maszyna wirtualna platformy Azure
Jak SAP liveCache jest aplikacja, która wykonuje obliczenia ogromny, hello ilość i szybkość pamięci RAM i procesora CPU ma poważny wpływ na wydajność liveCache SAP.

Dla typów maszyny Wirtualnej Azure hello obsługiwane przez SAP (Uwaga SAP [1928533]), wszystkie zasoby Procesora wirtualnego przydzielone toohello wirtualna bazują na dedykowany fizycznych zasobów procesora CPU hello funkcji hypervisor. Nie wymaga (i w związku z tym nie konkurowanie o zasoby procesora CPU) ma miejsce.

Podobnie dla wszystkich typów wystąpienie maszyny Wirtualnej platformy Azure obsługiwane przez SAP, hello pamięci maszyny Wirtualnej jest 100% zamapować pamięci fizycznej toohello — nadmiarowe Inicjowanie obsługi administracyjnej (nadmierne zobowiązania), na przykład nie jest używany.

Z tą perspektywą zaleca toouse hello nowy D-series lub maszyny Wirtualnej platformy Azure: seria DS (w połączeniu z usługą Azure Premium Storage) typ, mają 60% procesory szybsze niż hello A-series. Witaj największa ilość pamięci RAM i procesora CPU obciążenia, można użyć serii G i maszyny wirtualne serii GS (w połączeniu z usługą Azure Premium Storage) z procesorem Intel Xeon® najnowsze hello E5 v3 rodziny, która ma dwa razy hello pamięci i cztery razy hello półprzewodnikowych dysku magazynu (SSD) hello D / Seria DS.

#### <a name="storage-configuration"></a>Konfiguracja magazynu
Jak SAP liveCache jest oparty na technologii SAP MaxDB, wszystkie hello magazynu Azure zalecenia wymienionych SAP MaxDB w rozdziale [konfiguracji magazynu] [ dbms-guide-8.4.1] również są prawidłowe dla SAP liveCache.

#### <a name="dedicated-azure-vm-for-livecache"></a>Dedykowane maszyny Wirtualnej platformy Azure dla liveCache
Jak SAP liveCache intensywnie korzysta z moc obliczeniową, do użytku produkcyjnego zaleca toodeploy na dedykowany maszynie wirtualnej platformy Azure.

![Dedykowane maszyny Wirtualnej platformy Azure dla liveCache dla przypadek użycia produktywności][dbms-guide-figure-700]

#### <a name="backup-and-restore"></a>Wykonywanie kopii zapasowych i przywracanie
Kopia zapasowa i przywracanie zagadnienia dotyczące wydajności, w tym już zostały opisane w odpowiednich rozdziałów SAP MaxDB hello [i przywracania kopii zapasowych] [ dbms-guide-8.4.2] i [zagadnienia dotyczące wydajności dla kopii zapasowej i przywrócić][dbms-guide-8.4.3].

#### <a name="other"></a>Inne
Wszystkie tematy ogólne już zostały opisane w hello odpowiednich MaxDB SAP [to] [ dbms-guide-8.4.4] działu.

## <a name="specifics-for-hello-sap-content-server-on-windows"></a>Charakterystyka hello SAP serwera zawartości w systemie Windows
powitania serwera zawartości SAP jest zawartość toostore oddzielnych, na serwerze składników, takich jak elektronicznych dokumentów w różnych formatach. Witaj SAP serwera zawartości są udostępniane przez rozwoju technologii i jest międzyaplikacyjnej toobe używane aplikacje SAP. Jest instalowana w oddzielnym systemie. Typowe zawartości jest szkolenie materiałów i dokumentów z magazynu wiedzy lub rysunki techniczne pochodzące z mySAP hello System zarządzania dokumentami elementu.

### <a name="sap-content-server-version-support"></a>Obsługa wersji zawartości serwera SAP
SAP obecnie obsługuje:

* **Serwer zawartości SAP** z wersją **6.50 (lub nowszy)**
* **MaxDB SAP wersji 7,9**
* **Microsoft IIS (Internet Information Server) w wersji 8.0 (i nowsze)**

Zdecydowanie zaleca się toouse hello najnowszą wersję serwera zawartości SAP, który w czasie hello pisania tego dokumentu jest **6.50 SP4**i hello najnowsza wersja **Microsoft IIS 8.5**.

Sprawdź hello najnowszych obsługiwane wersje SAP serwera zawartości i Microsoft IIS w hello [SAP produktu dostępności macierzy (PAM)][sap-pam].

### <a name="supported-microsoft-windows-and-azure-vm-types-for-sap-content-server"></a>Obsługiwane typy Microsoft Windows i maszyny Wirtualnej platformy Azure dla serwera zawartości SAP
toofind obsługiwanych wersji systemu Windows dla serwera zawartości SAP na platformie Azure, zobacz:

* [Macierz dostępności produktu SAP (PAM)][sap-pam]
* Uwaga SAP [1928533]

Zdecydowanie zaleca się toouse hello najnowszej wersji systemu Microsoft Windows, który w czasie hello pisania tego dokumentu jest **systemu Windows Server 2012 R2**.

### <a name="sap-content-server-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Wskazówki dotyczące konfigurowania serwera zawartości SAP SAP instalacji na maszynach wirtualnych platformy Azure
#### <a name="storage-configuration"></a>Konfiguracja magazynu
Jeśli skonfigurujesz serwer zawartości SAP toostore pliki w bazie danych SAP MaxDB hello wszystkie usługi Azure storage najlepszych rozwiązań zalecenie wymienionych SAP MaxDB w rozdziale [konfiguracji magazynu] [ dbms-guide-8.4.1] są również prawidłowe dla scenariusza zawartości serwera SAP hello.

Jeśli skonfigurujesz serwer zawartości SAP toostore plików w systemie plików hello jest zalecane toouse dedykowanych dysku logicznego. Używanie funkcji miejsca do magazynowania pozwala tooalso Zwiększ rozmiar dysku logicznego i przepływność IOPS, zgodnie z opisem w w rozdziale [RAID oprogramowania][dbms-guide-2.2].

#### <a name="sap-content-server-location"></a>Lokalizacja zawartości serwera SAP
Serwer zawartości SAP ma toobe wdrożone w hello tego samego regionu Azure i sieć wirtualna Azure wdrożonym hello systemu SAP. Jesteś toodecide wolnego, czy mają być toodeploy serwera zawartości SAP składników na dedykowanych maszyna wirtualna platformy Azure lub hello tej samej maszyny Wirtualnej, w którym jest uruchomiona hello systemu SAP.

![Maszyna wirtualna platformy Azure w wersji dedykowanej dla serwera zawartości SAP][dbms-guide-figure-800]

#### <a name="sap-cache-server-location"></a>Lokalizacja serwera SAP pamięci podręcznej
Witaj SAP serwera pamięci podręcznej jest dodatkowych składników serwerowych tooprovide dostępu too(cached) dokumenty lokalnie. powitania serwera pamięci podręcznej SAP buforuje dokumenty hello SAP serwera zawartości. Jest to toooptimize ruchu sieciowego w przypadku dokumentów toobe pobrać więcej niż jeden raz z różnych lokalizacji. ogólną zasadą Hello jest tego serwera pamięci podręcznej SAP hello ma toobe fizycznie Zamknij toohello klienta, który uzyskuje dostęp do powitania serwera pamięci podręcznej SAP.

Poniżej dostępne są dwie opcje:

1. **Klient znajduje się w wewnętrznej bazie danych systemu SAP** systemu SAP wewnętrznej bazy danych w przypadku skonfigurowanego tooaccess SAP serwera zawartości, klient jest systemu SAP. Podczas wdrażania zarówno systemu SAP, jak i serwer zawartości SAP w hello tego samego regionu Azure — w hello tego samego centrum danych Azure — były fizycznie tooeach innych. Dlatego nie jest toohave nie potrzeby dedykowanego serwera pamięci podręcznej SAP. Witaj dostępu klientów (SAP graficznego interfejsu użytkownika lub przeglądarki sieci web) SAP interfejsu użytkownika systemu SAP bezpośrednio i hello SAP system pobiera dokumentów z hello SAP serwera zawartości.
2. **Klient jest przeglądarki sieci web lokalnie** hello SAP serwera zawartości może być skonfigurowany toobe uzyskać dostępu bezpośrednio hello przeglądarki sieci web. W takim przypadku przeglądarki sieci web uruchomiony lokalnie — jest klientem hello SAP serwera zawartości. W lokalnym centrum danych i centrum danych Azure są umieszczane w różnych lokalizacjach fizycznych (najlepiej Zamknij tooeach innych). Centrum danych lokalnych jest tooAzure połączonych za pośrednictwem usługi Azure Site-to-Site VPN lub usługi ExpressRoute. Mimo że obie opcje oferują bezpiecznego tooAzure połączenia sieci VPN, połączenia lokacja lokacja nie oferuje SLA sieci przepustowości i opóźnień między hello lokalnego centrum danych i hello centrum danych Azure. toospeed się toodocuments dostępu, możesz wybrać jedną z następujących hello:
   1. Zainstaluj lokalnym serwerem SAP pamięci podręcznej, zamknij przeglądarkę sieci web lokalnie toohello (opcja [to] [ dbms-guide-900-sap-cache-server-on-premises] rysunek)
   2. Skonfiguruj Azure ExpressRoute, oferuje niezawodny i małych opóźnieniach dedykowane połączenie sieciowe między lokalnego centrum danych i centrum danych Azure.

![Opcja tooinstall SAP pamięci podręcznej serwera lokalnego][dbms-guide-figure-900]
<a name="642f746c-e4d4-489d-bf63-73e80177a0a8"></a>

#### <a name="backup--restore"></a>Wykonywanie kopii zapasowych i ich przywracanie
Jeśli skonfigurujesz powitania serwera zawartości SAP toostore pliki bazy danych SAP MaxDB hello zagadnienia procedury i wydajności kopii zapasowych/przywracania hello już w SAP MaxDB rozdziale opisano [i przywracania kopii zapasowych] [ dbms-guide-8.4.2] i rozdział [zagadnienia dotyczące wydajności tworzenia kopii zapasowych i przywracania][dbms-guide-8.4.3].

Jeśli skonfigurujesz powitania serwera zawartości SAP toostore plików w systemie plików hello jedną z opcji jest tooexecute ręcznego tworzenia kopii zapasowej/przywracania hello cały plik struktury którym dokumenty hello znajdują się. Podobne tooSAP MaxDB kopii zapasowej i przywracania jest zalecane toohave dedykowany wolumin w celu tworzenia kopii zapasowej.

#### <a name="other"></a>Inne
Inne ustawienia określonego serwera zawartości SAP przezroczysty tooAzure maszyn wirtualnych i są opisane w różnych dokumentach i SAP uwagi:

* <https://Service.SAP.com/contentserver>
* Uwaga SAP [1619726]  

## <a name="specifics-tooibm-db2-for-luw-on-windows"></a>Szczegóły tooIBM bazy danych DB2 dla LUW w systemie Windows
Przy użyciu systemu Microsoft Azure można łatwo przeprowadzić migrację istniejącej aplikacji SAP systemem IBM DB2 dla maszyn wirtualnych tooAzure Linux, UNIX i systemu Windows (LUW). Z programu SAP, IBM DB2 dla LUW Administratorzy i deweloperzy mogą nadal używać hello tych samych narzędzi programowania i administracji, które są dostępne lokalnie.
Ogólne informacje o systemie SAP Business Suite IBM DB2 dla LUW można znaleźć w hello SAP społeczności sieci (SCN) na <https://scn.sap.com/community/db2-for-linux-unix-windows>.

Dodatkowe informacje i aktualizacji dotyczących SAP na bazy danych DB2 dla LUW na platformie Azure, zobacz Uwaga SAP [2233094].

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>IBM DB2 dla systemu Linux, UNIX i obsługa wersji systemu Windows
SAP na IBM DB2 dla LUW na usługi Microsoft Azure maszyny wirtualnej jest obsługiwane począwszy od wersji bazy danych DB2 10.5.

Informacje o obsługiwanych produktach SAP i typy maszyny Wirtualnej platformy Azure, zobacz tooSAP Uwaga [1928533].

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>IBM DB2 dla systemu Linux, UNIX i wskazówki dotyczące konfigurowania systemu Windows dla programu SAP instalacji na maszynach wirtualnych platformy Azure
#### <a name="storage-configuration"></a>Konfiguracja magazynu
Wszystkie pliki bazy danych muszą być przechowywane w systemie plików NTFS hello oparte na dyskach VHD. Te wirtualne dyski twarde są zainstalowane toohello maszyny Wirtualnej platformy Azure i są oparte na w magazynie obiektów BLOB Azure strony (<https://msdn.microsoft.com/library/azure/ee691964.aspx>).
Dowolny dyski sieciowe lub zdalnych udziałów, takich jak hello następujących usług plików na platformę Azure są **nie** obsługiwane dla plików bazy danych:

* <https://blogs.msdn.com/b/windowsazurestorage/Archive/2014/05/12/Introducing-Microsoft-Azure-File-Service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/Archive/2014/05/27/persisting-Connections-to-Microsoft-Azure-Files.aspx>

Jeśli używasz Azure wirtualne dyski twarde, oparte na magazyn obiektów BLOB Azure strony hello instrukcji zawartych w tym dokumencie w rozdziale [struktury wdrożenia RDBMS] [ dbms-guide-2] również LUW poprosić toodeployments z hello IBM DB2 Baza danych.

Jak opisano wcześniej w głównej części dokumentu hello hello, przydziały na przepływność IOPS dla wirtualnych dysków twardych Azure istnieje. dokładne przydziały Hello są zależne od typu maszyny Wirtualnej hello używane. Znajduje się lista typów maszyny Wirtualnej z przydziałami ich [tutaj][virtual-machines-sizes]

Tak długo, jak bieżący przydział IOPS hello na dysku jest wystarczająca, jest możliwe toostore, którego wszystkie hello pliki bazy danych na jednym jednego zainstalowanego wirtualnego dysku twardego Azure.

Wydajność zagadnienia również można znaleźć toochapter "danych bezpieczeństwa i wydajności uwagi dla bazy danych katalogi" w Przewodnikach instalacji SAP.

Alternatywnie można użyć pul magazynu systemu Windows (tylko dostępne w systemie Windows Server 2012 i nowsze) lub w rozdziale opisano rozkładanie systemu Windows dla systemu Windows 2008 R2 jako [RAID oprogramowania] [ dbms-guide-2.2] tego dokumentu toocreate jeden duży urządzenia logicznego przez wiele dysków zainstalowanych wirtualnego dysku twardego.
Dla dysków hello zawierających hello bazy danych DB2 ścieżek magazynu do katalogów sapdata i saptmp należy określić dysk fizyczny rozmiar sektora 512 KB. Gdy używane są pule magazynu systemu Windows, należy utworzyć hello pule magazynów ręcznie za pośrednictwem interfejsu wiersza polecenia przy użyciu parametru hello "-LogicalSectorSizeDefault". Aby uzyskać więcej informacji, zobacz <https://technet.microsoft.com/library/hh848689.aspx>.

#### <a name="backuprestore"></a>Tworzenie i przywracanie kopii zapasowych
Hello funkcji wykonywania kopii zapasowej i przywracania programu IBM DB2 LUW jest obsługiwane w hello sam sposób jak w standardowe systemów operacyjnych Windows Server i Hyper-V.

Należy się upewnić, czy masz strategii tworzenia kopii zapasowej prawidłową bazę danych w miejscu.

Jak wdrożenia bez systemu operacyjnego wydajności tworzenia kopii zapasowej/przywracania zależy od mogą być odczytywane jak wiele woluminów równolegle i jakie przepływności hello tych woluminów mogą być. Ponadto hello użycie procesora CPU używanych przez kompresję kopii zapasowych może odtworzyć istotną rolę na maszynach wirtualnych z właśnie too8 wątków procesora CPU. W związku z tym co można założyć:

* Witaj mniej hello liczba wirtualnych dysków twardych używanych toostore hello bazy danych urządzeń, hello mniejszych hello ogólną przepustowość podczas odczytywania
* Witaj mniejszą liczbę hello wątków procesora CPU w hello maszyny Wirtualnej, hello poważniejsze wpływ hello kompresja kopii zapasowej
* Witaj mniejszą liczbę elementów docelowych (Stripe katalogów, wirtualne dyski twarde) toowrite hello kopii zapasowej, hello niższe hello przepływności

tooincrease hello liczba toowrite obiekty docelowe do, dwie opcje może być używany/łączone w zależności od potrzeb:

* Stosowanie hello wolumin docelowy kopii zapasowej za pośrednictwem wielu wirtualnych dysków twardych zainstalowanych w kolejności tooimprove hello IOPS przepływności na tym woluminie rozłożonego
* Przy użyciu więcej niż jeden docelowy katalogu toowrite hello kopii zapasowej

#### <a name="high-availability-and-disaster-recovery"></a>Wysoka dostępność i odzyskiwanie po awarii
Serwera klastrów firmy Microsoft (MSCS) nie jest obsługiwana.

Odzyskiwanie po awarii wysoką dostępność bazy danych DB2 (HADR) jest obsługiwane. Jeśli działa rozpoznawanie nazw maszyn wirtualnych hello hello HA konfiguracji, ustawienia hello na platformie Azure zostanie różnią się od żadnej konfiguracji, które jest wykonywane lokalnie. Nie jest zalecane toorely na tylko rozpoznawania adresu IP.

Nie używaj replikacji geograficznej magazynu Azure. Aby uzyskać więcej informacji, zobacz toochapter [magazyn Microsoft Azure] [ dbms-guide-2.3] i rozdział [wysokiej dostępności i odzyskiwania po awarii z maszynami wirtualnymi Azure] [ dbms-guide-3].

#### <a name="other"></a>Inne
Wszystkie inne tematy ogólne jak zestawami dostępności Azure lub SAP monitorowania stosowane zgodnie z opisem w hello pierwsze trzy rozdziałach tego dokumentu w przypadku wdrożeń maszyn wirtualnych z programu IBM DB2 dla LUW również.

Należy także zapoznać toochapter [ogólne programu SQL Server dla programu SAP w podsumowaniu Azure][dbms-guide-5.8].
