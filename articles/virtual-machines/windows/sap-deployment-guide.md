---
title: "aaaAzure wdrożenia maszyny wirtualnej dla programu SAP w systemie Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak SAP toodeploy oprogramowanie na maszynach wirtualnych systemu Windows na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 22aaa98c-bb9f-472f-b546-0b294e033cda
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 121e317afc6498a896959e58ebfbdcbef9432ef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-on-windows-vms-in-azure"></a>Wdrażanie programu SAP na maszynach wirtualnych systemu Windows na platformie Azure
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
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP on Windows)
[dbms-guide-2.1]:sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from hello Azure Marketplace)
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics tooSQL Server RDBMS)
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
[dbms-guide-900-sap-cache-server-on-premises]:sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md (Azure Virtual Machines deployment for SAP on Windows)
[deployment-guide-2.2]:#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from hello Azure Marketplace for SAP)
[deployment-guide-3.3]:#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM tooan on-premises domain - Windows only)
[deployment-guide-4.4.2]:#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable hello Azure VM Agent)
[deployment-guide-4.5.1]:#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure hello Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for hello Azure monitoring infrastructure)
[deployment-guide-5.3]:#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:#baccae00-6f79-4307-ade4-40292ce4e02d (Configure hello proxy)
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:classic/virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:classic/virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-windows-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md (Azure Virtual Machines planning and implementation for SAP on Windows)
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on hello on-premises customer network)
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with hello on-premises network)
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises tooAzure)
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)

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
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
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
[virtual-machines-windows-attach-disk-portal]:../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../virtual-machines-windows-capture-image.md#capture-the-vm
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
[virtual-machines-windows-create-vm-specialized]:../virtual-machines-windows-create-vm-specialized.md
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

Maszyny wirtualne platformy Azure jest hello rozwiązania dla organizacji, które muszą zasobów obliczeniowych i magazynu, w czasie minimalnego i bez cykle nabywania długie. Maszyny wirtualne Azure toodeploy klasycznego aplikacje, takie jak SAP NetWeaver aplikacji, można użyć w systemie Azure. Rozszerzanie niezawodności i dostępności bez dodatkowych lokalnych zasobów aplikacji. Maszyny wirtualne platformy Azure obsługuje łączności między lokalizacjami, maszynach wirtualnych platformy Azure można zintegrować lokalnej domeny Twojej organizacji, chmur prywatnych i pozioma systemu SAP.

W tym artykule firma Microsoft obejmuje aplikacje SAP toodeploy kroki hello na maszynach wirtualnych systemu Windows (VM) na platformie Azure. W tym artykule opiera się na powitania informacji w [maszyny wirtualne Azure planowania i wdrażania dla SAP w systemie Windows][planning-guide]. Uzupełnia on również SAP instalacji dokumentacji i notatki SAP hello zasobów podstawowy instalacji i wdrażania oprogramowania SAP.

## <a name="prerequisites"></a>Wymagania wstępne
Konfigurowanie maszyny wirtualnej platformy Azure dla wdrożenia oprogramowania SAP obejmuje wiele kroków i zasobów. Przed rozpoczęciem upewnij się, że spełniają hello wymagań wstępnych instalacji oprogramowania SAP na maszynach wirtualnych systemu Windows na platformie Azure.

### <a name="local-computer"></a>Komputer lokalny
toomanage systemu Windows lub maszyn wirtualnych systemu Linux, można użyć skryptu programu PowerShell i hello portalu Azure. Dla obu narzędzia należy komputera lokalnego z systemem Windows 7 lub nowszej wersji systemu Windows. Jeśli chcesz toomanage tylko maszyn wirtualnych systemu Linux, a ma toouse komputera z systemem Linux dla tego zadania można użyć wiersza polecenia platformy Azure.

### <a name="internet-connection"></a>Połączenie internetowe
toodownload i hello uruchamiania narzędzia i skrypty, które są wymagane do wdrożenia oprogramowania SAP, musi być podłączony toohello Internet. Witaj maszyny Wirtualnej platformy Azure z systemem hello Azure ulepszone rozszerzenie monitorowania dla programu SAP musi także toohello dostęp do Internetu. Jeśli hello maszyny Wirtualnej platformy Azure jest częścią sieci wirtualnej platformy Azure lub lokalnymi domeny, upewnij się, że hello właściwych ustawień serwera proxy są ustawione, zgodnie z opisem w [skonfigurować serwer proxy hello][deployment-guide-configure-proxy].

### <a name="microsoft-azure-subscription"></a>Subskrypcja platformy Microsoft Azure
Potrzebne aktywne konto platformy Azure.

### <a name="topology-and-networking"></a>Topologia i sieci
Należy toodefine hello topologii i architektura hello wdrożenia SAP na platformie Azure:

* Używane toobe konta magazynu platformy Azure
* Gdzie chcesz systemu SAP hello toodeploy sieci wirtualnej
* Chcesz systemu SAP hello toodeploy toowhich grupy zasobów
* Region platformy Azure w miejscu systemu SAP hello toodeploy
* Konfiguracja programu SAP (dwuwarstwowa i trójwarstwowa)
* Rozmiary maszyn wirtualnych i hello liczba dodatkowych wirtualnych dysków twardych (VHD) toobe zainstalowane toohello maszyny wirtualne
* Konfiguracja korekty SAP i System transportu (CTS)

Tworzenie i konfigurowanie kont magazynu Azure lub sieci wirtualnych platformy Azure, przed rozpoczęciem procesu wdrażania oprogramowania SAP hello. Aby uzyskać informacje na temat toocreate oraz konfigurowania tych zasobów, zobacz [maszyny wirtualne Azure planowania i wdrażania dla SAP w systemie Windows][planning-guide].

### <a name="sap-sizing"></a>Zmiana rozmiaru SAP
Znajomość hello następujących informacji dla programu SAP rozmiaru:

* Przewidywane obciążenia SAP, na przykład za pomocą narzędzia Rozmiar symboli szybkie SAP hello i hello numer SAP aplikacji wydajności standardowe (protokoły SAP)
* Wymagany zasób i pamięci użycie Procesora hello systemu SAP
* Wymagane operacje wejścia/wyjścia (We/Wy), na sekundę
* Wymagana przepustowość sieci wynosi ostatecznego komunikacji między maszynami wirtualnymi na platformie Azure
* Przepustowość sieci wymagany między zasoby lokalne i hello systemu SAP wdrożone Azure

### <a name="resource-groups"></a>Grupy zasobów
W systemie Azure Resource Manager służy toomanage grup zasobów wszystkie zasoby aplikacji hello w Twojej subskrypcji platformy Azure. Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Resource Manager][resource-group-overview].

## <a name="resources"></a>Zasoby

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Zasoby SAP
Podczas konfigurowania wdrożenia oprogramowania SAP, potrzebne są następujące zasoby SAP hello:

* Uwaga SAP [1928533], który zawiera:
  * Lista rozmiarów maszyny Wirtualnej platformy Azure, które są obsługiwane dla hello wdrożenia oprogramowania SAP
  * Informacje o rozmiary maszyn wirtualnych Azure ważne pojemności
  * Obsługiwane oprogramowanie SAP i kombinacji bazy danych i systemu operacyjnego (OS)
  * Wymagana wersja jądra SAP dla systemu Windows i Linux w systemie Microsoft Azure

* Uwaga SAP [2015553] wymieniono wymagania wstępne dotyczące wdrażania oprogramowania SAP SAP, obsługiwane na platformie Azure.
* Uwaga SAP [2178632] zawiera szczegółowe informacje na temat wszystkie funkcje monitorowania metryki zgłoszone dla SAP na platformie Azure.
* Uwaga SAP [1409604] hello wymaga wersji agenta hosta SAP dla systemu Windows na platformie Azure.
* Uwaga SAP [2191498] hello wymaga wersji agenta hosta SAP dla systemu Linux na platformie Azure.
* Uwaga SAP [2243692] zawiera informacje o licencjonowaniu SAP w systemie Linux na platformie Azure.
* Uwaga SAP [1984787] zawiera ogólne informacje o systemie SUSE Linux Enterprise Server 12.
* Uwaga SAP [2002167] zawiera ogólne informacje na temat Red Hat Enterprise Linux 7.x.
* Uwaga SAP [1999351] zawiera dodatkowe informacje dotyczące rozwiązywania problemów hello Azure ulepszone rozszerzenie monitorowania dla programu SAP.
* [SAP społeczności WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) ma wszystkie wymagane informacje SAP dla systemu Linux.
* Polecenia cmdlet programu PowerShell specyficzne dla programu SAP, które są częścią [programu Azure PowerShell][azure-ps].
* Specyficzne dla programu SAP polecenia interfejsu wiersza polecenia Azure, które są częścią [interfejsu wiersza polecenia Azure][azure-cli].

[comment]: <> (Poziom poprawki MSSedusch TODO dodać ARM dla agenta hosta SAP w 1409604 Uwaga SAP)

### <a name="microsoft-resources"></a>Zasoby firmy Microsoft
Te artykuły Microsoft obejmuje wdrożenia SAP na platformie Azure:

* [Azure maszyn wirtualnych, planowania i wdrażania dla SAP w systemie Windows][planning-guide]
* [Maszyny wirtualne Azure wdrożenie SAP w systemie Windows (w tym artykule)][deployment-guide]
* [Azure maszyn wirtualnych systemu DBMS wdrożenie SAP w systemie Windows][dbms-guide]
* [Azure portal][azure-portal]

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Scenariusze wdrażania oprogramowania SAP na maszynach wirtualnych Azure
Istnieje wiele opcji wdrażania maszyn wirtualnych i skojarzone dyski na platformie Azure. Jest ważne toounderstand hello różnice między opcje wdrażania, ponieważ tooprepare inne czynności może potrwać maszyn wirtualnych do wdrożenia oparte na wybranego typu wdrożenia hello.

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Scenariusz 1: Wdrażanie maszyny Wirtualnej z hello Azure Marketplace w celu SAP
Możesz użyć obrazu obsługiwane przez firmę Microsoft lub strony trzeciej w hello Azure Marketplace toodeploy maszyny Wirtualnej. Witaj Marketplace udostępnia niektóre standardowe obrazów systemu operacyjnego Windows Server i różne dystrybucje systemu Linux. Również można wdrożyć obraz, który obejmuje zarządzanie bazą danych jednostki SKU systemu (danych DBMS), na przykład Microsoft SQL Server. Aby uzyskać więcej informacji o korzystaniu z obrazów z wersji systemu DBMS dotycząca produktu, zobacz [DBMS maszyny wirtualne Azure wdrożenie SAP w systemie Linux][dbms-guide].

Witaj poniższy schemat przedstawia hello specyficzne dla programu SAP sekwencji kroki w celu wdrożenia maszyny Wirtualnej z portalu Azure Marketplace hello:

![Schemat blokowy wdrożenia maszyny Wirtualnej dla systemów SAP przy użyciu obrazu maszyny Wirtualnej z hello Azure Marketplace][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Utwórz maszynę wirtualną za pomocą hello portalu Azure
Hello Najprostszym sposobem toocreate nowej maszyny wirtualnej z obrazu z hello Azure Marketplace jest przy użyciu hello portalu Azure.

1.  Przejdź za<https://portal.azure.com/#create>.  Lub hello menu portalu Azure, wybierz **+ nowy**.
2.  Wybierz **obliczeniowe**, a następnie wybierz typ hello ma toodeploy systemu operacyjnego. Na przykład Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) lub Red Hat Enterprise Linux 7.2 (RHEL 7.2). domyślny widok listy Hello nie są wyświetlane wszystkie obsługiwane systemy operacyjne. Wybierz **zobaczyć wszystkie** pełną listę. Aby uzyskać więcej informacji na temat obsługiwanych systemów operacyjnych dla wdrożenia oprogramowania SAP, patrz Uwaga SAP [1928533].
3.  Na następnej stronie powitania Przejrzyj warunki i postanowienia.
4.  W hello **wybierz model wdrożenia** wybierz **Resource Manager**.
5.  Wybierz pozycję **Utwórz**.

Hello Kreator przeprowadzi użytkownika przez ustawienie maszyny wirtualnej hello hello wymagane parametry toocreate, oprócz tooall wymaganych zasobów, takich jak interfejsów sieciowych i kont magazynu. Niektóre z tych parametrów, to:

1. **Podstawy**:
  * **Nazwa**: hello Nazwa zasobu hello (hello nazwę maszyny wirtualnej).
 * **Nazwa użytkownika i hasło** lub **klucz publiczny SSH**: Wprowadź hello nazwę użytkownika i hasło użytkownika hello, który jest tworzony podczas inicjowania obsługi hello. Dla maszyny wirtualnej systemu Linux można wprowadzić hello Secure Shell (SSH) klucz publiczny Użyj toosign toohello maszyny.
 * **Subskrypcja**: Wybierz subskrypcję hello, które mają toouse tooprovision hello nowej maszyny wirtualnej.
 * **Grupa zasobów**: hello nazwę grupy zasobów hello hello maszyny Wirtualnej. Można wprowadzić nazwę hello albo zasób grupy lub hello nazwę nowej grupy zasobów, która już istnieje.
 * **Lokalizacja**: gdzie toodeploy hello nowej maszyny wirtualnej. Jeśli chcesz, aby sieć lokalną tooyour tooconnect hello maszyny wirtualnej, upewnij się, że możesz wybrać lokalizację hello hello sieci wirtualnej, które łączy sieć lokalną Azure tooyour. Aby uzyskać więcej informacji, zobacz [sieci Microsoft Azure] [ planning-guide-microsoft-azure-networking] w [maszyny wirtualne Azure planowania i wdrażania dla SAP w systemie Linux][planning-guide].
2. **Rozmiar**:

     Aby uzyskać listę obsługiwanych typów maszyny Wirtualnej, zobacz Uwaga SAP [1928533]. Upewnij się, że wybierz hello poprawnego typu maszyny Wirtualnej, jeśli chcesz, aby toouse Azure Premium Storage. Nie wszystkie typy maszyny Wirtualnej obsługuje usługi Premium Storage. Aby uzyskać więcej informacji, zobacz [magazynu: Microsoft Azure Storage i dysków z danymi] [ planning-guide-storage-microsoft-azure-storage-and-data-disks] i [Azure Premium Storage] [ planning-guide-azure-premium-storage] w [maszyny wirtualne Azure planowania i wdrażania dla SAP w systemie Linux][planning-guide].

3. **Ustawienia**:
   * **Konto magazynu**: Wybierz istniejące konto magazynu lub Utwórz nową. Nie wszystkie typy magazynu działa w przypadku uruchamiania aplikacji SAP. Aby uzyskać więcej informacji na temat typów magazynu, zobacz [magazyn Microsoft Azure] [ dbms-guide-2.3] w [DBMS maszyny wirtualne Azure wdrożenie SAP w systemie Linux][dbms-guide].
   * **Sieć wirtualna** i **podsieci**: maszynę wirtualną hello toointegrate z sieci intranet hello wybierz sieć wirtualną tooyour połączonych sieci lokalnej.
   * **Publiczny adres IP**: Wybierz hello publiczny adres IP ma toouse lub wprowadzić parametry toocreate nowego publicznego adresu IP. Publiczny tooaccess adresów IP można użyć maszyny wirtualnej za pośrednictwem hello Internet. Upewnij się również utworzyć sieci zabezpieczeń grupy toohelp bezpiecznego dostępu tooyour maszynę wirtualną.
   * **Grupy zabezpieczeń sieci**: Aby uzyskać więcej informacji, zobacz [sterowaniu przepływem ruchu sieciowego z grup zabezpieczeń sieci][virtual-networks-nsg].
   * **Dostępność**: Wybierz zestaw dostępności lub wprowadź toocreate parametry hello dostępność nowych ustawić. Aby uzyskać więcej informacji, zobacz [zestawami dostępności Azure][planning-guide-3.2.3].
   * **Monitorowanie**: można wybrać **wyłączyć** monitorowania diagnostyki. Jego jest włączane automatycznie po uruchomieniu hello polecenia tooenable hello Azure ulepszone rozszerzenie monitorowania, zgodnie z opisem w [Konfigurowanie monitorowania][deployment-guide-configure-monitoring-scenario-1].

4. **Podsumowanie**:

  Przejrzyj wybrane opcje, a następnie wybierz **OK**.

Maszyna wirtualna jest wdrażana w grupie zasobów hello wybrane.

#### <a name="create-a-virtual-machine-by-using-a-template"></a>Utwórz maszynę wirtualną za pomocą szablonu
Można utworzyć maszynę wirtualną za pomocą jednego z szablonów SAP hello opublikowane w hello [repozytorium GitHub azure — Szybki Start — szablony][azure-quickstart-templates-github]. Również można ręcznie utworzyć maszynę wirtualną za pomocą hello [portalu Azure][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], lub [wiersza polecenia platformy Azure ][virtual-machines-linux-tutorial].

* [**Szablon konfiguracji dwuwarstwowej (tylko jedna maszyna wirtualna)** (sap-2-warstwy —-obrazu z witryny marketplace)][sap-templates-2-tier-marketplace-image]

  toocreate dwuwarstwowy system przy użyciu tylko jednej maszyny wirtualnej, użyj tego szablonu.
* [**Szablon konfiguracji trójwarstwowej (wiele maszyn wirtualnych)** (sap-3-warstwy —-obrazu z witryny marketplace)][sap-templates-3-tier-marketplace-image]

  toocreate system trójwarstwowa przy użyciu wielu maszyn wirtualnych, użyj tego szablonu.

W portalu Azure hello wprowadź następujące parametry szablonu hello hello:

1. **Podstawy**:
  * **Subskrypcja**: hello subskrypcji toouse toodeploy hello szablonu.
  * **Grupa zasobów**: hello zasobów grupy toouse toodeploy hello szablonu. Można utworzyć nową grupę zasobów lub wybrać istniejącą grupę zasobów w subskrypcji hello.
  * **Lokalizacja**: gdzie toodeploy hello szablonu. W przypadku wybrania istniejącej grupy zasobów jest używany hello lokalizacji tej grupy zasobów.

2. **Ustawienia**:
  * **Identyfikator systemu SAP**: hello systemu SAP (SID).
  * **Typ systemu operacyjnego**: hello ma toodeploy, na przykład systemu operacyjnego Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12) i Red Hat Enterprise Linux 7.2 (RHEL 7.2).

    domyślny widok listy Hello nie są wyświetlane wszystkie obsługiwane systemy operacyjne. Wybierz **zobaczyć wszystkie** pełną listę. Aby uzyskać więcej informacji na temat obsługiwanych systemów operacyjnych dla wdrożenia oprogramowania SAP, patrz Uwaga SAP [1928533].
  * **Rozmiar systemu SAP**: hello rozmiar hello systemu SAP.

    zawiera liczbę Hello protokoły SAP hello nowy system. Jeśli nie masz pewności, ile system hello protokoły SAP wymaga, zapytaj SAP technologii partnera lub Integrator systemu.
  * **Dostępność systemu** (tylko szablon trójwarstwowa): hello dostępność systemu.

    Wybierz **HA** konfiguracji, który jest odpowiedni dla instalacji wysokiej dostępności. Tworzone są dwa serwery baz danych i dwóch serwerów dla ABAP SAP centralnej usług (ASCS).
  * **Typ magazynu** (tylko szablon dwuwarstwowa): hello typu toouse magazynu.

    Dla większych systemów zdecydowanie zaleca się przy użyciu usługi Azure Premium Storage. Aby uzyskać więcej informacji na temat typów magazynu zawierają następujące zasoby:
      * [Użycie magazynu SSD Azure — wersja Premium dla wystąpienia systemu DBMS SAP][2367194]
      * [Microsoft Azure Storage] [ dbms-guide-2.3] w [DBMS maszyny wirtualne Azure wdrożenie SAP w systemie Linux][dbms-guide]
      * [Magazyn w warstwie Premium: Magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure][storage-premium-storage-preview-portal]
      * [Wprowadzenie tooMicrosoft usługi Azure Storage][storage-introduction]
  * **Nazwa użytkownika administratora** i **hasło administratora**: nazwa użytkownika i hasło.
    Nowy użytkownik jest tworzony dla logowania toohello maszyny wirtualnej.
  * **Nowy lub istniejący podsieci**: Określa, czy tworzenia nowej sieci wirtualnej i podsieci, czy jest używany przez istniejącą podsieć. Jeśli masz już sieć wirtualną tooyour połączonych sieci lokalnej, wybierz **istniejące**.
  * **Identyfikator podsieci**: identyfikator hello maszyn wirtualnych hello podsieci hello połączy się. Wybierz podsieć hello wirtualnej sieci prywatnej (VPN) lub Azure ExpressRoute sieci wirtualnej toouse tooconnect hello maszyny wirtualnej tooyour lokalnej sieci. Identyfikator Hello zwykle wygląda następująco: /subscriptions/&lt;identyfikator subskrypcji > /resourceGroups/&lt;Nazwa grupy zasobów > /providers/Microsoft.Network/virtualNetworks/&lt;wirtualnej nazwy sieciowej > /subnets/&lt;nazwy podsieci >

3. **Warunki i postanowienia**:  
    Przeczytaj i zaakceptuj postanowienia prawne hello.

4.  Wybierz **zakupu**.

Hello Agent maszyny Wirtualnej jest wdrażane domyślnie, korzystając z obrazu z hello Azure Marketplace.

#### <a name="configure-proxy-settings"></a>Skonfiguruj ustawienia serwera proxy
W zależności od konfiguracji sieci lokalnej może być konieczne tooset zapasową hello proxy na maszynie Wirtualnej. Maszyny Wirtualnej w przypadku sieci lokalnej tooyour połączonych za pośrednictwem sieci VPN lub usługi ExpressRoute, hello maszyny Wirtualnej może nie można hello stanie tooaccess Internet i nie toodownload stanie hello wymagane rozszerzenia lub zbierania danych monitorowania. Aby uzyskać więcej informacji, zobacz [skonfigurować serwer proxy hello][deployment-guide-configure-proxy].

#### <a name="join-a-domain-windows-only"></a>Przyłącz do domeny (tylko system Windows)
W przypadku wdrożenia usługi Azure połączonych tooan wystąpienia usługi Active Directory i DNS lokalnej za pośrednictwem połączenia sieci VPN lokacja lokacja platformy Azure lub usługa ExpressRoute (jest to *między lokalizacjami* w [planowania maszynach wirtualnych platformy Azure i implementacji dla SAP w systemie Linux][planning-guide]), oczekuje się, że hello maszyny Wirtualnej jest przyłączania do domeny lokalnej. Aby uzyskać więcej informacji na temat zagadnień dotyczących tego zadania, zobacz [Przyłącz do domeny lokalnej tooan maszyny Wirtualnej (tylko system Windows)][deployment-guide-4.3].

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Konfigurowanie monitorowania
toobe się środowisko obsługuje SAP, skonfiguruj hello Azure rozszerzenie monitorowania dla programu SAP, zgodnie z opisem w [Konfiguruj hello Azure ulepszone rozszerzenie monitorowania dla programu SAP][deployment-guide-4.5]. Sprawdź wymagania wstępne hello SAP monitorowania i wymagane minimalne wersje programu SAP jądra i agenta hosta SAP w hello zasobów wymienionych w [zasobów SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Monitorowanie wyboru
Sprawdź, czy monitorowanie działa, zgodnie z opisem w [sprawdzanie i rozwiązywanie problemów dotyczących konfigurowania monitorowania end-to-end][deployment-guide-troubleshooting-chapter].

#### <a name="post-deployment-steps"></a>Czynności po wdrożeniu
Po utworzeniu hello maszyny Wirtualnej i hello maszyna wirtualna jest wdrażana, potrzebne są składniki oprogramowania hello wymagane tooinstall w hello maszyny Wirtualnej. Ze względu na powitania sekwencji instalacji programowy wdrożenia w tym typie wdrożenia maszyny Wirtualnej hello toobe oprogramowania zainstalowane musi być dostępna, albo na platformie Azure na innej maszynie Wirtualnej lub jako dysk, który można dołączyć. Lub, należy rozważyć znajduje się przy użyciu scenariusza między lokalizacjami, w których łączności toohello lokalnych zasobów (udziałów instalacji).

Po wdrożeniu maszyny Wirtualnej na platformie Azure, wykonaj hello same wskazówki i narzędzia tooinstall hello SAP oprogramowania na maszynie Wirtualnej podczas czy w środowisku lokalnym. tooinstall oprogramowania SAP na maszynie Wirtualnej platformy Azure, zarówno firmy Microsoft i SAP zaleca przekazywanie i przechowywać nośnika instalacyjnego programu SAP hello na wirtualnych dyskach twardych Azure lub utworzenie maszyny Wirtualnej platformy Azure, która działa jako serwer plików, który zawiera wszystkie hello wymagane nośnika instalacyjnego programu SAP.

[comment]: <> (Dlaczego należy toorecommend zarządzania plikami, na przykład TODO MSSedusch serwera plików lub dysku VHD? Jest to tak różne z lokalnej?)

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Scenariusz 2: Wdrażanie maszyny Wirtualnej z obrazu niestandardowego dla SAP
Ponieważ różne wersje systemu operacyjnego lub DBMS mają różne wymagania dotyczące, hello obrazów, które możesz znaleźć w portalu Azure Marketplace hello nie spełnia Twoje potrzeby. Zamiast tego można toocreate Maszynę wirtualną przy użyciu własnego obrazu systemu operacyjnego/DBMS maszyny Wirtualnej, który można wdrożyć ponownie później.
Możesz użyć toocreate wykonania różnych kroków w prywatnej obrazu dla systemu Linux niż toocreate, jeden dla systemu Windows.

- - -
> ![Windows][Logo_Windows] Windows
>
> obraz systemu Windows można użyć toodeploy wiele maszyn wirtualnych, ustawień systemu Windows hello (takich jak Windows SID i nazwy hosta) musi być usunięte lub uogólniony na powitania tooprepare lokalnej maszyny Wirtualnej. Można użyć [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo to.
>
> ![Linux][Logo_Linux] Linux
>
> Niektóre ustawienia Linux tooprepare obrazu systemu Linux, których można używać toodeploy wiele maszyn wirtualnych musi być usunięte lub uogólniony na powitania lokalnej maszyny Wirtualnej. Można użyć `waagent -deprovision` toodo to. Aby uzyskać więcej informacji, zobacz [Przechwytywanie maszyny wirtualnej systemu Linux działających na platformie Azure] [ virtual-machines-linux-capture-image] i hello [Podręcznik użytkownika agenta systemu Linux Azure][virtual-machines-linux-agent-user-guide-command-line-options].
>
>

- - -
Należy przygotować i utworzyć niestandardowy obraz, a następnie użyj go toocreate wiele nowych maszyn wirtualnych. Jest to opisane w [maszyny wirtualne Azure planowania i wdrażania dla SAP w systemie Linux][planning-guide]. Konfigurowanie bazy danych zawartości przy użyciu Menedżera inicjowania obsługi oprogramowania SAP tooinstall nowego systemu SAP (przywrócenie kopii zapasowej bazy danych z wirtualnego dysku twardego, który jest dołączony toohello maszyny wirtualnej) lub przez przywrócenie kopii zapasowej bazy danych bezpośrednio z usługi Azure storage, jeśli systemu DBMS obsługuje tę funkcję. Aby uzyskać więcej informacji, zobacz [DBMS maszyny wirtualne Azure wdrożenie SAP w systemie Linux][dbms-guide]. Zainstalowano SAP system na lokalnej maszynie Wirtualnej (szczególnie w przypadku systemów dwuwarstwowa) można dostosować ustawienia systemu SAP hello po wdrożeniu hello hello maszyny Wirtualnej platformy Azure, za pomocą procedury zmienić System hello obsługiwane przez rozbudowy oprogramowania SAP Menedżer (Uwaga SAP [1619720]). W przeciwnym razie można zainstalować oprogramowania SAP hello po wdrożeniu hello maszyny Wirtualnej platformy Azure.

Witaj poniższy schemat przedstawia hello specyficzne dla programu SAP sekwencji kroki w celu wdrożenia maszyny Wirtualnej z obrazu niestandardowego:

![Schemat blokowy wdrożenia maszyny Wirtualnej dla systemów SAP przy użyciu obrazu maszyny Wirtualnej w prywatnej Marketplace][deployment-guide-figure-300]

#### <a name="create-hello-virtual-machine"></a>Utwórz maszynę wirtualną hello
toocreate wdrożenia przy użyciu prywatnych obrazu systemu operacyjnego z hello portalu Azure, użyj jednej z hello następujące szablony SAP. Te szablony są publikowane w hello [repozytorium GitHub azure — Szybki Start — szablony][azure-quickstart-templates-github]. Możesz również można ręcznie utworzyć maszynę wirtualną za pomocą [PowerShell][virtual-machines-upload-image-windows-resource-manager].

* [**Szablon konfiguracji dwuwarstwowej (tylko jedna maszyna wirtualna)** (sap-2-warstwy —-obrazu użytkownika)][sap-templates-2-tier-user-image]

  toocreate dwuwarstwowy system przy użyciu tylko jednej maszyny wirtualnej, użyj tego szablonu.
* [**Szablon konfiguracji trójwarstwowej (wiele maszyn wirtualnych)** (sap-3-warstwy —-obrazu użytkownika)][sap-templates-3-tier-user-image]

  Ten szablon służy toocreate trójwarstwowa systemu za pomocą wielu maszyn wirtualnych lub własny obraz systemu operacyjnego.

W portalu Azure hello wprowadź następujące parametry szablonu hello hello:

1. **Podstawy**:
  * **Subskrypcja**: hello subskrypcji toouse toodeploy hello szablonu.
  * **Grupa zasobów**: hello zasobów grupy toouse toodeploy hello szablonu. Możesz utworzyć nową grupę zasobów lub wybierz istniejącą grupę zasobów w subskrypcji hello.
  * **Lokalizacja**: gdzie toodeploy hello szablonu. W przypadku wybrania istniejącej grupy zasobów jest używany hello lokalizacji tej grupy zasobów.
2. **Ustawienia**:
  * **Identyfikator systemu SAP**: hello identyfikatora systemu SAP.
  * **Typ systemu operacyjnego**: hello typ systemu operacyjnego, który chcesz toodeploy (Windows lub Linux).
  * **Rozmiar systemu SAP**: hello rozmiar hello systemu SAP.

    zawiera liczbę Hello protokoły SAP hello nowy system. Jeśli nie masz pewności, ile system hello protokoły SAP wymaga, zapytaj SAP technologii partnera lub Integrator systemu.
  * **Dostępność systemu** (tylko szablon trójwarstwowa): hello dostępność systemu.

    Wybierz **HA** konfiguracji, który jest odpowiedni dla instalacji wysokiej dostępności. Dwa serwery baz danych i dwóch serwerów dla ASCS są tworzone.
  * **Typ magazynu** (tylko szablon dwuwarstwowa): hello typu toouse magazynu.

    Dla większych systemów zdecydowanie zaleca się przy użyciu usługi Azure Premium Storage. Aby uzyskać więcej informacji na temat typów magazynu zobacz następujące zasoby hello:
      * [Użycie magazynu SSD Azure — wersja Premium dla wystąpienia systemu DBMS SAP][2367194]
      * [Microsoft Azure Storage] [ dbms-guide-2.3] w [DBMS maszyny wirtualne Azure wdrożenie SAP w systemie Linux][dbms-guide]
      * [Magazyn w warstwie Premium: Magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej platformy Azure][storage-premium-storage-preview-portal]
      * [Wprowadzenie tooMicrosoft usługi Azure Storage][storage-introduction]
  * **Obraz użytkownika identyfikator URI dysku VHD**: hello identyfikatora URI obrazu systemu operacyjnego prywatnej hello wirtualnego dysku twardego, na przykład https://&lt;nazwa konta >.blob.core.windows.net/vhds/userimage.vhd.
  * **Konto magazynu obrazu użytkownika**: hello nazwę konta magazynu hello hello prywatnej obrazu systemu operacyjnego przechowywania, na przykład &lt;accountname > w https://&lt;nazwa konta >.blob.core.windows.net/vhds/userimage.vhd.
  * **Nazwa użytkownika administratora** i **hasło administratora**: hello nazwy użytkownika i hasła.

    Nowy użytkownik jest tworzony dla logowania toohello maszyny wirtualnej.
  * **Nowy lub istniejący podsieci**: Określa, czy utworzono nową sieć wirtualną i podsieć, czy jest używany przez istniejącą podsieć. Jeśli masz już sieć wirtualną tooyour połączonych sieci lokalnej, wybierz **istniejące**.
  * **Identyfikator podsieci**: identyfikator hello maszyn wirtualnych hello hello podsieci toowhich połączy się. Wybierz podsieć hello sieci VPN i ExpressRoute sieci wirtualnej toouse tooconnect hello maszyny wirtualnej tooyour w sieci lokalnej. Identyfikator Hello zwykle wygląda następująco:

    /Subscriptions/&lt;identyfikator subskrypcji > /resourceGroups/&lt;Nazwa grupy zasobów > /providers/Microsoft.Network/virtualNetworks/&lt;wirtualnej nazwy sieciowej > /subnets/&lt;nazwy podsieci >

3. **Warunki i postanowienia**:  
    Przeczytaj i zaakceptuj postanowienia prawne hello.

4.  Wybierz **zakupu**.

#### <a name="install-hello-vm-agent-linux-only"></a>Zainstaluj hello agenta maszyny Wirtualnej (tylko w systemie Linux)
Szablony hello toouse opisane w powyższej sekcji hello, powitalne agenta systemu Linux muszą być zainstalowane w obrazie użytkownika hello lub hello wdrożenia zakończy się niepowodzeniem. Pobierz i zainstaluj hello agenta maszyny Wirtualnej w hello obrazu użytkownika, zgodnie z opisem w [pobrać, zainstalować i włączyć hello agenta maszyny Wirtualnej Azure][deployment-guide-4.4]. Jeśli nie używasz hello szablony, można też zainstalować hello później agenta maszyny Wirtualnej.

#### <a name="join-a-domain-windows-only"></a>Przyłącz do domeny (tylko system Windows)
Jeśli wdrożenie Azure jest połączonych tooan wystąpienia usługi Active Directory i DNS lokalnej za pośrednictwem połączenia sieci VPN lokacja lokacja platformy Azure lub usługa Azure ExpressRoute (jest to *między lokalizacjami* w [maszyn wirtualnych platformy Azure Planowanie i wdrażanie dla SAP w systemie Linux][planning-guide]), oczekuje się, że hello maszyny Wirtualnej jest przyłączania do domeny lokalnej. Aby uzyskać więcej informacji dotyczących tego kroku, zobacz [Przyłącz do domeny lokalnej tooan maszyny Wirtualnej (tylko system Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Skonfiguruj ustawienia serwera proxy
W zależności od konfiguracji sieci lokalnej może być konieczne tooset zapasową hello proxy na maszynie Wirtualnej. Maszyny Wirtualnej w przypadku sieci lokalnej tooyour połączonych za pośrednictwem sieci VPN lub usługi ExpressRoute, hello maszyny Wirtualnej może nie można hello stanie tooaccess Internet i nie toodownload stanie hello wymagane rozszerzenia lub zbierania danych monitorowania. Aby uzyskać więcej informacji, zobacz [skonfigurować serwer proxy hello][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Konfigurowanie monitorowania
toobe się środowisko obsługuje SAP, skonfiguruj hello Azure rozszerzenie monitorowania dla programu SAP, zgodnie z opisem w [Konfiguruj hello Azure ulepszone rozszerzenie monitorowania dla programu SAP][deployment-guide-4.5]. Sprawdź wymagania wstępne hello SAP monitorowania i wymagane minimalne wersje programu SAP jądra i agenta hosta SAP w hello zasobów wymienionych w [zasobów SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Monitorowanie wyboru
Sprawdź, czy monitorowanie działa, zgodnie z opisem w [sprawdzanie i rozwiązywanie problemów dotyczących konfigurowania monitorowania end-to-end][deployment-guide-troubleshooting-chapter].




### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Scenariusz 3: Przenoszenie maszyny Wirtualnej z lokalnymi przy użyciu-uogólniony wirtualny dysk twardy Azure SAP
W tym scenariuszu planujesz toomove określonego systemu SAP z tooAzure środowiska lokalnego. Można to zrobić, przekazując hello wirtualny dysk twardy ma hello systemu operacyjnego, plików binarnych programu SAP hello, i po pewnym czasie hello DBMS plików binarnych, a także hello wirtualnych dysków twardych z danymi hello i plików hello systemu DBMS tooAzure dziennika. W odróżnieniu od hello scenariusz opisany w [Scenariusz 2: Wdrażanie maszyny Wirtualnej z obrazu niestandardowego dla SAP][deployment-guide-3.3], w tym przypadku zachować hello nazwa hosta, SAP SID i kont użytkowników SAP w hello wirtualna Azure, ponieważ zostały one skonfigurowana hello w środowisku lokalnym. Nie trzeba hello toogeneralize systemu operacyjnego. Ten scenariusz dotyczy najczęściej toocross lokalnych scenariuszy, w których część hello pozioma SAP działa lokalnie jego część nie działa na platformie Azure.

W tym scenariuszu hello agenta maszyny Wirtualnej nie jest automatycznie instalowany podczas wdrażania. Ponieważ hello agenta maszyny Wirtualnej i hello Azure ulepszone rozszerzenie monitorowania dla programu SAP wymaga toorun SAP, wystarczy toodownload, zainstaluj i włącz oba składniki ręcznie po utworzeniu maszyny wirtualnej hello.

Aby uzyskać więcej informacji na temat hello agenta maszyny Wirtualnej Azure zobacz następujące zasoby hello.

[comment]: <> (Poniższe łącze MSSedusch TODO Windows Update)

- - -
> ![Windows][Logo_Windows] Windows
>
> <http://blogs.msdn.com/b/wats/Archive/2014/02/17/bginfo-Guest-Agent-Extension-for-Azure-VMS.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> [Podręcznik użytkownika Azure agenta systemu Linux][virtual-machines-linux-agent-user-guide]
>
>

- - -

Schemat blokowy przedstawia hello sekwencji kroków do przenoszenia maszyny Wirtualnej z lokalnymi przy użyciu-uogólniony wirtualny dysk twardy Azure po Hello:

![Schemat blokowy wdrożenia maszyny Wirtualnej dla programu SAP systemów za pomocą dysku maszyny Wirtualnej][deployment-guide-figure-400]

Przy założeniu, że hello dysk jest już przekazany i określone na platformie Azure (zobacz [maszyny wirtualne Azure planowania i wdrażania dla SAP w systemie Linux][planning-guide]), czy zadania hello w hello opisane w dalszej części kilka sekcje.

#### <a name="create-a-virtual-machine"></a>Tworzenie maszyny wirtualnej
toocreate wdrożenia przy użyciu prywatnych dysku systemu operacyjnego za pomocą hello portalu Azure, użyj szablonu programu SAP hello opublikowane w hello [repozytorium GitHub azure — Szybki Start — szablony][azure-quickstart-templates-github]. Możesz również można ręcznie utworzyć maszynę wirtualną za pomocą programu PowerShell.

* [**Szablon konfiguracji dwuwarstwowej (tylko jedna maszyna wirtualna)** (sap-2-warstwy użytkownika dysk)][sap-templates-2-tier-os-disk]

  toocreate dwuwarstwowy system przy użyciu tylko jednej maszyny wirtualnej, użyj tego szablonu.

W portalu Azure hello wprowadź następujące parametry szablonu hello hello:

1. **Podstawy**:
  * **Subskrypcja**: hello subskrypcji toouse toodeploy hello szablonu.
  * **Grupa zasobów**: hello zasobów grupy toouse toodeploy hello szablonu. Możesz utworzyć nową grupę zasobów lub wybierz istniejącą grupę zasobów w subskrypcji hello.
  * **Lokalizacja**: gdzie toodeploy hello szablonu. W przypadku wybrania istniejącej grupy zasobów jest używany hello lokalizacji tej grupy zasobów.
2. **Ustawienia**:
  * **Identyfikator systemu SAP**: hello identyfikatora systemu SAP.
  * **Typ systemu operacyjnego**: hello typ systemu operacyjnego, który chcesz toodeploy (Windows lub Linux).
  * **Rozmiar systemu SAP**: hello rozmiar hello systemu SAP.

    zawiera liczbę Hello protokoły SAP hello nowy system. Jeśli nie masz pewności, ile system hello protokoły SAP wymaga, zapytaj SAP technologii partnera lub Integrator systemu.
  * **Typ magazynu** (tylko szablon dwuwarstwowa): hello typu toouse magazynu.

    Dla większych systemów zdecydowanie zaleca się przy użyciu usługi Azure Premium Storage. Aby uzyskać więcej informacji na temat typów magazynu zobacz następujące zasoby hello:
      * [Użycie magazynu SSD Azure — wersja Premium dla wystąpienia systemu DBMS SAP][2367194]
      * [Microsoft Azure Storage] [ dbms-guide-2.3] w [DBMS maszyny wirtualnej Azure wdrożenie SAP w systemie Linux][dbms-guide]
      * [Magazyn w warstwie Premium: Magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure][storage-premium-storage-preview-portal]
      * [Wprowadzenie tooMicrosoft usługi Azure Storage][storage-introduction]
  * **Identyfikator URI dysku VHD na dysku systemu operacyjnego**: hello URI hello dysku prywatnej systemu operacyjnego, na przykład https://&lt;nazwa konta >.blob.core.windows.net/vhds/osdisk.vhd.
  * **Nowy lub istniejący podsieci**: Określa, czy tworzenia nowej sieci wirtualnej i podsieci, czy jest używany przez istniejącą podsieć. Jeśli masz już sieć wirtualną tooyour połączonych sieci lokalnej, wybierz **istniejące**.
  * **Identyfikator podsieci**: identyfikator hello maszyn wirtualnych hello hello podsieci toowhich połączy się. Wybierz podsieć hello sieci VPN lub rozwiązania Azure ExpressRoute sieci wirtualnej toouse tooconnect hello maszyny wirtualnej tooyour w sieci lokalnej. Identyfikator Hello zwykle wygląda następująco:

    /Subscriptions/&lt;identyfikator subskrypcji > /resourceGroups/&lt;Nazwa grupy zasobów > /providers/Microsoft.Network/virtualNetworks/&lt;wirtualnej nazwy sieciowej > /subnets/&lt;nazwy podsieci >

3. **Warunki i postanowienia**:  
    Przeczytaj i zaakceptuj postanowienia prawne hello.

4.  Wybierz **zakupu**.

#### <a name="install-hello-vm-agent"></a>Zainstaluj hello agenta maszyny Wirtualnej
powitalne toouse szablony opisanego w hello poprzedniej sekcji, hello agenta maszyny Wirtualnej musi być zainstalowany na dysku systemu operacyjnego hello lub hello wdrożenie zakończy się niepowodzeniem. Pobierz i zainstaluj hello agenta maszyny Wirtualnej w hello maszyny Wirtualnej, zgodnie z opisem w [pobrać, zainstalować i włączyć hello agenta maszyny Wirtualnej Azure][deployment-guide-4.4].

Jeśli nie używasz szablony hello opisane w powyższej sekcji hello, można także zainstalować hello agenta maszyny Wirtualnej później.

#### <a name="join-a-domain-windows-only"></a>Przyłącz do domeny (tylko system Windows)
W przypadku wdrożenia usługi Azure połączonych tooan wystąpienia usługi Active Directory i DNS lokalnej za pośrednictwem połączenia sieci VPN lokacja lokacja platformy Azure lub usługa ExpressRoute (jest to *między lokalizacjami* w [planowania maszynach wirtualnych platformy Azure i implementacji dla SAP w systemie Linux][planning-guide]), oczekuje się, że hello maszyny Wirtualnej jest przyłączania do domeny lokalnej. Aby uzyskać więcej informacji na temat zagadnień dotyczących tego zadania, zobacz [Przyłącz do domeny lokalnej tooan maszyny Wirtualnej (tylko system Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Skonfiguruj ustawienia serwera proxy
W zależności od konfiguracji sieci lokalnej może być konieczne tooset zapasową hello proxy na maszynie Wirtualnej. Maszyny Wirtualnej w przypadku sieci lokalnej tooyour połączonych za pośrednictwem sieci VPN lub usługi ExpressRoute, hello maszyny Wirtualnej może nie można hello stanie tooaccess Internet i nie toodownload stanie hello wymagane rozszerzenia lub zbierania danych monitorowania. Aby uzyskać więcej informacji, zobacz [skonfigurować serwer proxy hello][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Konfigurowanie monitorowania
toobe się środowisko obsługuje SAP, skonfiguruj hello Azure rozszerzenie monitorowania dla programu SAP, zgodnie z opisem w [Konfiguruj hello Azure ulepszone rozszerzenie monitorowania dla programu SAP][deployment-guide-4.5]. Sprawdź wymagania wstępne hello SAP monitorowania i wymagane minimalne wersje programu SAP jądra i agenta hosta SAP w hello zasobów wymienionych w [zasobów SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Monitorowanie wyboru
Sprawdź, czy monitorowanie działa, zgodnie z opisem w [sprawdzanie i rozwiązywanie problemów dotyczących konfigurowania monitorowania end-to-end][deployment-guide-troubleshooting-chapter].

## <a name="update-hello-monitoring-configuration-for-sap"></a>Zaktualizuj hello konfiguracji monitorowania dla programu SAP
Aktualizacja konfiguracji monitorowania SAP hello w żadnym hello następujące scenariusze:
* Witaj wspólnego zespołu Microsoft/SAP rozszerza możliwości monitorowania hello i żąda liczniki więcej lub mniej.
* Microsoft wprowadziła nową wersję programu hello podstawowej infrastruktury platformy Azure polegającego na dostarczaniu hello danych monitorowania i hello rozszerzenia rozszerzonego monitorowania Azure dla programu SAP potrzeb toobe dostosowane toothose zmiany.
* W przypadku zainstalowania dodatkowych tooyour wirtualne dyski twarde maszyny Wirtualnej platformy Azure lub usunąć wirtualnego dysku twardego. W tym scenariuszu należy zaktualizować kolekcji hello związane z magazynowaniem danych. Zmiana konfiguracji przez dodanie lub usunięcie punktów końcowych lub przypisując IP tooa adresów maszyny Wirtualnej nie wpływa na powitania konfiguracji monitorowania.
* Możesz zmienić hello rozmiar maszyny Wirtualnej Azure, na przykład z tooany A5 rozmiar innych rozmiar maszyny Wirtualnej.
* Możesz dodać nowe tooyour interfejsy sieciowe maszyny Wirtualnej platformy Azure.

tooupdate ustawień monitorowania, hello aktualizacji Monitorowanie infrastruktury, hello następujące kroki [Konfiguruj hello Azure ulepszone rozszerzenie monitorowania dla programu SAP][deployment-guide-4.5].

## <a name="detailed-tasks-for-sap-software-deployment-on-a-windows-vm"></a>Szczegółowe zadania dla wdrożenia oprogramowania SAP na maszynie Wirtualnej systemu Windows
W tej sekcji przedstawiono szczegółowe kroki dotyczące wykonywania określonych zadań w procesie hello konfiguracji i wdrażania.

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Wdrażanie poleceń cmdlet programu Azure PowerShell
1.  Przejdź za[Microsoft Azure pobiera](https://azure.microsoft.com/downloads/).
2.  W obszarze **narzędzia wiersza polecenia**, w obszarze **PowerShell**, wybierz pozycję **Windows zainstaluj**.
3.  Okno dialogowe menedżera pobierania firmy Microsoft hello, hello pobrane pliku (na przykład WindowsAzurePowershellGet.3f.3f.3fnew.exe), wybierz **Uruchom**.
4.  Wybierz toorun Instalatora platformy sieci Web firmy Microsoft (Microsoft Web PI) **tak**.
5.  Strona, która wygląda jak pojawia się:

  ![Strona instalacji dla poleceń cmdlet programu Azure PowerShell][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Wybierz **zainstalować**, a następnie zaakceptuj postanowienia licencyjne dotyczące oprogramowania firmy Microsoft hello.
7.  Środowisko PowerShell jest zainstalowane. Wybierz **Zakończ** Kreatora instalacji hello tooclose.

Często sprawdzaj aktualizacje toohello poleceń cmdlet programu PowerShell, które zwykle są aktualizowane co miesiąc. Witaj Najprostszym sposobem toocheck aktualizacji jest hello toodo poprzedzających kroki instalacji toohello instalacji stronę przedstawionym w kroku 5. Hello numer daty i wydania wersji hello poleceń cmdlet znajdują się na stronie powitania przedstawionym w kroku 5. Jeżeli nie określono inaczej w Uwaga SAP [1928533] lub Uwaga SAP [2015553], zalecamy współpracę z najnowszej wersji hello poleceń cmdlet programu Azure PowerShell.

Wersja hello toocheck hello poleceń cmdlet programu Azure PowerShell, które są zainstalowane na komputerze, uruchom następujące polecenie programu PowerShell:
```powershell
Import-Module Azure
(Get-Module Azure).Version
```
wynik Hello wygląda następująco:

![Wynik sprawdzenie wersji polecenia cmdlet programu Azure PowerShell][deployment-guide-figure-600]
<a name="figure-6"></a>

Hello Azure polecenia cmdlet wersji zainstalowanej na komputerze w przypadku bieżącej wersji hello, pierwsza strona kreatora instalacji hello hello wskazuje, że przez dodanie **(zainstalować)** tytuł produktu toohello (zobacz powitania po zrzut ekranu). Polecenia cmdlet programu PowerShell Azure są aktualne. tooclose hello Kreatora instalacji, wybierz opcję **zakończenia**.

![Strona instalacji dla poleceń cmdlet programu Azure PowerShell wskazujący najnowszą wersję hello tego polecenia cmdlet programu PowerShell Azure są zainstalowane][deployment-guide-figure-700]
<a name="figure-7"></a>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Wdrażanie usługi Azure CLI
1.  Przejdź za[Microsoft Azure pobiera](https://azure.microsoft.com/downloads/).
2.  W obszarze **narzędzia wiersza polecenia**w obszarze **interfejsu wiersza polecenia platformy Azure**, wybierz pozycję hello **zainstalować** link dla systemu operacyjnego.
3.  Okno dialogowe menedżera pobierania firmy Microsoft hello, hello pobrane pliku (na przykład WindowsAzureXPlatCLI.3f.3f.3fnew.exe), wybierz **Uruchom**.
4.  Wybierz toorun Instalatora platformy sieci Web firmy Microsoft (Microsoft Web PI) **tak**.
5.  Strona, która wygląda jak pojawia się:

  ![Strona instalacji dla poleceń cmdlet programu Azure PowerShell][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Wybierz **zainstalować**, a następnie zaakceptuj postanowienia licencyjne dotyczące oprogramowania firmy Microsoft hello.
7.  Interfejs wiersza polecenia platformy Azure jest zainstalowany. Wybierz **Zakończ** Kreatora instalacji hello tooclose.

Często sprawdzaj aktualizacje tooAzure interfejsu wiersza polecenia, która zwykle jest aktualizowana co miesiąc. Witaj Najprostszym sposobem toocheck aktualizacji jest hello toodo poprzedzających kroki instalacji toohello instalacji stronę przedstawionym w kroku 5.


Wersja hello toocheck interfejsu wiersza polecenia Azure, która jest zainstalowana na komputerze, uruchom następujące polecenie:
```
azure --version
```

wynik Hello wygląda następująco:

![Wynik sprawdzania wersji interfejsu wiersza polecenia Azure][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Przyłącz do domeny lokalnej tooan maszyny Wirtualnej (tylko system Windows)
W przypadku wdrożenia SAP maszyn wirtualnych w scenariuszu obejmującym różne pomieszczenia, gdzie w lokalnej usłudze Active Directory i DNS zostały rozszerzone na platformie Azure, oczekuje się, że hello maszyny wirtualne są przyłączania do domeny lokalnej. Witaj szczegółowy opis kroków, które należy wykonać toojoin domeny lokalnej tooan maszyny Wirtualnej, a hello toobe wymagane dodatkowe oprogramowanie domeny lokalnej jest zależna od klienta. Zazwyczaj toojoin tooan wirtualna lokalnej domeny, należy tooinstall dodatkowego oprogramowania, takich jak ochrony przed złośliwym oprogramowaniem i tworzenia kopii zapasowej lub monitorowania oprogramowania.

W tym scenariuszu należy są również toomake się upewnić, że maszyna wirtualna jest dołączany do domeny w środowisku wymuszenie ustawień internetowego serwera proxy Windows hello ma lokalnego konta systemowego (S-1-5-18) w hello maszyny Wirtualnej gościa hello tych samych ustawień serwera proxy. Opcja najprostszym Hello jest tooforce hello proxy przy użyciu zasad grupy, które stosuje toosystems w domenie hello domeny.

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Pobrać, zainstalować i włączyć hello Agent maszyny Wirtualnej
W przypadku maszyn wirtualnych, które zostały wdrożone z obrazu systemu operacyjnego, który nie jest uogólniona (na przykład obraz, który nie pochodzą z narzędzia przygotowywania systemu Windows lub programu sysprep, hello) należy toomanually pobieranie, instalowanie i Włącz hello Agent maszyny Wirtualnej.

W przypadku wdrożenia maszyny Wirtualnej z hello Azure Marketplace, ten krok nie jest wymagane. Obrazy z hello Azure Marketplace już hello Agent maszyny Wirtualnej.

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Systemu Windows
1.  Pobierz hello Agent maszyny Wirtualnej:
  1.  Pobierz hello [pakiet Instalatora agenta maszyny Wirtualnej Azure](https://go.microsoft.com/fwlink/?LinkId=394789).
  2.  Lokalnie przechowywane hello pakiet MSI agenta maszyny Wirtualnej na serwerze lub komputerze osobistym.
2.  Zainstaluj agenta maszyny Wirtualnej Azure hello:
  1.  Połącz toohello wdrożyć maszyny Wirtualnej platformy Azure przy użyciu protokołu RDP (Remote Desktop).
  2.  Otwórz okno Eksploratora Windows na powitania maszyny Wirtualnej i hello wybierz katalog docelowy dla pliku MSI hello hello agenta maszyny Wirtualnej.
  3.  Przeciągnij plik MSI Instalatora agenta maszyny Wirtualnej Azure hello z katalogu lokalnego komputera/serwera toohello docelowej z hello agenta maszyny Wirtualnej na powitania maszyny Wirtualnej.
  4.  Kliknij dwukrotnie plik MSI hello na powitania maszyny Wirtualnej.
3.  Dla maszyn wirtualnych, które są lokalne tooon przyłączone do domeny, upewnij się, że ostatecznego ustawień internetowego serwera proxy obowiązują również toohello konta systemu lokalnego (S-1-5-18) hello maszyny Wirtualnej, zgodnie z opisem w [skonfigurować serwer proxy hello] [ deployment-guide-configure-proxy]. Witaj agenta maszyny Wirtualnej działa w tym kontekście i musi tooAzure stanie tooconnect toobe.

Interakcja użytkownika nie jest wymagane tooupdate hello Agent maszyny Wirtualnej. Hello agenta maszyny Wirtualnej jest aktualizowany automatycznie i nie wymaga ponownego uruchomienia maszyny Wirtualnej.

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux
Użyj hello następujące polecenia tooinstall hello agenta maszyny Wirtualnej dla systemu Linux:

* **SUSE Linux Enterprise Server (SLES)**

  ```
  sudo zypper install WALinuxAgent
  ```

* **Red Hat Enterprise Linux (RHEL)**

  ```
  sudo yum install WALinuxAgent
  ```

Jeśli zainstalowano agenta hello hello tooupdate agenta systemu Linux platformy Azure, hello procedury opisanej w [hello aktualizacji agenta systemu Linux Azure VM toohello najnowszej wersji z serwisu GitHub][virtual-machines-linux-update-agent].

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Skonfiguruj serwer proxy hello
Witaj kolejne kroki wykonywane tooconfigure hello proxy w systemie Windows różnią się od hello sposób konfigurowania serwera proxy hello w systemie Linux.

#### <a name="windows"></a>Windows
Ustawienia serwera proxy musi być poprawnie skonfigurowane dla hello tooaccess hello Internet konta systemu lokalnego. Jeśli ustawienia serwera proxy nie są skonfigurowane przy użyciu zasad grupy, można skonfigurować ustawienia hello hello lokalnego konta systemowego.

1. Przejdź za**Start**, wprowadź **gpedit.msc**, a następnie wybierz **Enter**.
2. Wybierz **Konfiguracja komputera** > **Szablony administracyjne** > **składniki systemu Windows** > **programu Internet Explorer**. Upewnij się, że ustawienie hello **upewnij proxy ustawienia dla poszczególnych komputerów (a nie dla poszczególnych użytkowników)** zostało wyłączone lub nieskonfigurowane.
3. W **Panelu sterowania**, przejdź do zbyt**Centrum sieci i udostępniania** > **Opcje internetowe**.
4. Na powitania **połączeń** kartę, zaznacz hello **ustawienia sieci LAN** przycisku.
5. Wyczyść hello **Automatycznie wykryj ustawienia** pole wyboru.
6. Wybierz hello **Użyj serwera proxy dla sieci LAN** pole wyboru, a następnie wprowadź hello adres i port proxy.
7. Wybierz hello **zaawansowane** przycisku.
8. W hello **wyjątki** wprowadź adres IP hello **168.63.129.16**. Kliknij przycisk **OK**.


#### <a name="linux"></a>Linux
Skonfiguruj serwer proxy poprawne hello w pliku konfiguracji hello hello gościa Agent usługi Microsoft Azure, która znajduje się pod adresem \\itp\\waagent.conf.

Ustaw hello następujące parametry:

1.  **Hosta serwera proxy HTTP**. Na przykład ustawić także**proxy.corp.local**.
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  **Port serwera proxy HTTP**. Na przykład ustawić także**80**.
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  Uruchom ponownie agenta hello.

  ```
  sudo service waagent restart
  ```

Witaj ustawień serwera proxy w \\itp\\waagent.conf mają zastosowanie również toohello wymagane rozszerzeń maszyny Wirtualnej. Jeśli chcesz, aby toouse hello Azure repozytoriów, upewnij się, że nie będzie hello ruchu toothese repozytoria za pośrednictwem sieci intranet lokalnymi. Jeśli utworzono zdefiniowane przez użytkownika tras tooenable wymuszone tunelowanie, upewnij się, że dodać trasy, który przekierowuje ruch toohello repozytoria bezpośrednio toohello Internet, a nie przez połączenie VPN lokacja lokacja.

* **SLES**

  Należy również tooadd trasy dla adresów IP hello wymienionych w \\itp\\regionserverclnt.cfg. Witaj poniższej ilustracji przedstawiono przykład:

  ![Wymuszone tunelowanie][deployment-guide-figure-50]


* **RHEL**

  Należy również tooadd trasy dla hello adresy IP hostów hello \\itp\\yum.repos.d\\rhui usługi równoważenia obciążenia. Na przykład zobacz hello powyższej ilustracji.

Aby uzyskać więcej informacji dotyczących tras zdefiniowanych przez użytkownika, zobacz [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP][virtual-networks-udr-overview].

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Skonfiguruj hello Azure ulepszone rozszerzenie monitorowania dla programu SAP
Kiedy zostały przygotowane hello maszyny Wirtualnej zgodnie z opisem w [scenariuszy wdrażania maszyn wirtualnych dla programu SAP na platformie Azure][deployment-guide-3], Agent maszyny Wirtualnej jest zainstalowany na maszynie wirtualnej hello hello. Witaj następnym krokiem jest toodeploy hello Azure rozszerzone monitorowanie rozszerzenie dla SAP, który jest dostępny w hello Azure rozszerzenia repozytorium w centrach danych platformy Azure globalne hello. Aby uzyskać więcej informacji, zobacz [maszyny wirtualne Azure planowania i wdrażania dla SAP w systemie Linux][planning-guide-9.1].

Można użyć programu PowerShell lub interfejsu wiersza polecenia Azure tooinstall i skonfigurować hello Azure ulepszone rozszerzenie monitorowania dla programu SAP. rozszerzenie hello tooinstall w systemie Windows lub maszyny Wirtualnej systemu Linux przy użyciu komputera z systemem Windows, temacie [programu Azure PowerShell][deployment-guide-4.5.1]. tooinstall hello rozszerzenia na maszynie Wirtualnej systemu Linux przy użyciu pulpitu systemu Linux, zobacz [interfejsu wiersza polecenia Azure][deployment-guide-4.5.2].

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Program Azure PowerShell dla systemu Linux i maszyn wirtualnych systemu Windows
tooinstall hello Azure ulepszone rozszerzenie monitorowania dla programu SAP przy użyciu programu PowerShell:

1. Upewnij się, że zainstalowano najnowszą wersję hello hello Azure polecenia cmdlet programu PowerShell. Aby uzyskać więcej informacji, zobacz [poleceń cmdlet wdrażania programu Azure PowerShell][deployment-guide-4.1].  
2. Uruchom następujące polecenia cmdlet programu PowerShell hello.
  Aby uzyskać listę dostępnych środowisk, należy uruchomić `commandlet Get-AzureRmEnvironment`. Jeśli chcesz, aby toouse publicznej Azure, środowisko to **AzureCloud**. Dla platformy Azure w Chinach, wybierz **AzureChinaCloud**.


      ```powershell
      $env = Get-AzureRmEnvironment -Name <name of hello environment>
      Login-AzureRmAccount -Environment $env
      Set-AzureRmContext -SubscriptionName <subscription name>

      Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
      ```

Po wprowadzeniu danych konta i zidentyfikować hello maszyny wirtualnej platformy Azure, skrypt hello wdraża hello wymagane rozszerzenia i umożliwia korzystanie z funkcji hello wymagane. Może to potrwać kilka minut.
Aby uzyskać więcej informacji na temat `Set-AzureRmVMAEMExtension`, zobacz [AzureRmVMAEMExtension zestaw][msdn-set-azurermvmaemextension].

![Pomyślne wykonanie specyficzne dla programu SAP Azure polecenia cmdlet Set-AzureRmVMAEMExtension][deployment-guide-figure-900]

Witaj `Set-AzureRmVMAEMExtension` konfiguracji jest wszystkich hostów hello kroki tooconfigure, monitorowania dla programu SAP.

dane wyjściowe skryptu Hello obejmuje hello następujących informacji:

* Potwierdzenie tego monitorowania hello podstawowy dysk VHD (hello systemu operacyjnego) i wszystkie dodatkowe wirtualne dyski twarde zainstalowanego toohello maszyny Wirtualnej zostały skonfigurowane.
* następne dwa wiadomości powitania Potwierdź hello konfiguracji metryki magazynu dla konta magazynu określonych.
* Jeden wiersz danych wyjściowych zawiera stan hello hello rzeczywista aktualizacja hello konfiguracji monitorowania.
* Kolejny wiersz danych wyjściowych potwierdza hello konfiguracji została wdrożona lub zaktualizowana.
* ostatni wiersz danych wyjściowych Hello ma charakter informacyjny. Przedstawia on opcje konfiguracji monitorowania hello testowania.

toocheck pomyślnie zostały wykonane wszystkie kroki Azure rozszerzonego monitorowania, czy ten hello infrastruktury platformy Azure udostępnia hello niezbędnych danych, kontynuować hello sprawdzanie gotowości dla hello Azure ulepszone rozszerzenie monitorowania dla programu SAP, zgodnie z opisem w temacie [Sprawdzanie gotowości do rozszerzonego monitorowania Azure dla programu SAP][deployment-guide-5.1]. Poczekaj 15 do 30 minut dla diagnostyki Azure toocollect hello odpowiednie dane.

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Azure CLI dla maszyn wirtualnych systemu Linux
tooinstall hello Azure ulepszone rozszerzenie monitorowania dla programu SAP przy użyciu wiersza polecenia platformy Azure:

1. Instalowanie interfejsu wiersza polecenia Azure, zgodnie z opisem w [hello instalowanie interfejsu wiersza polecenia Azure][azure-cli].
2. Zaloguj się przy użyciu konta platformy Azure:

  ```
  azure login
  ```

3. Przełącz tryb usługi Resource Manager tooAzure:

  ```
  azure config mode arm
  ```

4. Aby włączyć monitorowanie rozszerzonej platformy Azure:

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. Sprawdź, czy tego hello rozszerzenia rozszerzonego monitorowania Azure jest aktywna na powitania maszyny Wirtualnej systemu Linux platformy Azure. Sprawdź, czy hello pliku \\var\\lib\\AzureEnhancedMonitor\\PerfCounters istnieje. Jeśli istnieje, w wierszu polecenia Uruchom te informacje toodisplay polecenia zebrane przez hello Azure rozszerzone monitora:
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

dane wyjściowe Hello wygląda następująco:
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Sprawdzanie i rozwiązywanie problemów dotyczących monitorowania end-to-end
Po wdrożeniu maszyny Wirtualnej platformy Azure i konfigurowanie infrastruktury odpowiedniego monitorowania Azure hello, sprawdź, czy wszystkie składniki hello hello rozszerzenia rozszerzonego monitorowania Azure działają zgodnie z oczekiwaniami.

Uruchom sprawdzenie gotowości hello hello Azure ulepszone rozszerzenie monitorowania dla programu SAP, zgodnie z opisem w [sprawdzanie gotowości dla hello Azure ulepszone rozszerzenie monitorowania dla programu SAP][deployment-guide-5.1]. Jeśli wszystkie wyniki sprawdzania gotowości dodatnią oraz wszystkie liczniki wydajności są wyświetlane OK, monitorowania Azure został pomyślnie zainstalowany. Można kontynuować instalacji hello agenta hosta SAP opisanego w uwagach SAP hello w [zasobów SAP][deployment-guide-2.2]. Jeśli sprawdzanie gotowości hello wskazuje, że liczniki brakuje, uruchom sprawdzenie kondycji hello hello monitorowania infrastruktury platformy Azure, zgodnie z opisem w [sprawdzenie kondycji dla konfiguracji monitorowania infrastruktury platformy Azure] [ deployment-guide-5.2]. Aby uzyskać więcej opcji rozwiązywania problemów, zobacz [monitorowania Rozwiązywanie problemów z Azure dla programu SAP][deployment-guide-5.3].

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Sprawdź gotowość hello Azure ulepszone rozszerzenie monitorowania dla programu SAP
Ten test sprawdza, czy wszystkie metryki wydajności, które są wyświetlane w aplikacji SAP są dostarczane przez hello bazowy Azure Monitorowanie infrastruktury.

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a>Uruchom sprawdzanie gotowości hello na maszynie Wirtualnej systemu Windows

1.  Zaloguj się toohello maszyny wirtualnej platformy Azure (przy użyciu konta administratora nie jest to konieczne).
2.  Otwórz okno wiersza polecenia.
3.  W wierszu polecenia hello zmienić folder instalacji toohello katalogu hello z hello Azure ulepszone rozszerzenie monitorowania dla programu SAP: C:\\pakiety\\wtyczek\\ Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;wersji >\\upuść

  Witaj *wersji* w toohello ścieżka hello rozszerzenie dotyczące monitorowania może się różnić. Jeśli folderów dla różnych wersji monitorowania rozszerzenia w folderze instalacyjnym hello wyboru konfiguracji hello hello usługi AzureEnhancedMonitoring Windows hello są widoczne, a następnie folder toohello przełącznika wskazane jako *tooexecutable ścieżki* .

  ![Właściwości Usługa uruchomiona hello Azure ulepszone rozszerzenie monitorowania dla programu SAP][deployment-guide-figure-1000]

4.  W wierszu polecenia hello Uruchom **azperflib.exe** bez żadnych parametrów.

  > [!NOTE]
  > Azperflib.exe działa w pętli i aktualizuje hello zebrane liczniki co 60 sekund. tooend hello pętli hello Zamknij okno wiersza polecenia.
  >
  >

Jeśli hello Azure rozszerzone monitorowanie rozszerzenia nie jest zainstalowany lub hello AzureEnhancedMonitoring usługi nie jest uruchomiona, hello rozszerzenia ma nie został prawidłowo skonfigurowany. Aby uzyskać szczegółowe informacje dotyczące sposobu toodeploy hello rozszerzenia, zobacz [Rozwiązywanie problemów hello monitorowania infrastruktury platformy Azure dla programu SAP][deployment-guide-5.3].

##### <a name="check-hello-output-of-azperflibexe"></a>Sprawdź dane wyjściowe hello azperflib.exe
Dane wyjściowe Azperflib.exe pokazano, że wszystkie wypełnione liczniki wydajności platformy Azure dla programu SAP. U dołu hello hello Lista zebranych liczników wskaźnik Podsumowanie i kondycji Pokaż stan hello Azure monitorowania.

![Sprawdzenie kondycji, wykonując azperflib.exe, co oznacza, że nie istnieją problemy z danych wyjściowych][deployment-guide-figure-1100]
<a name="figure-11"></a>

Sprawdź wynik hello zwrócony dla hello **łącznie liczniki** dane wyjściowe, które jest raportowane jako pusty, a także **stan kondycji**, podanymi w powyższej ilustracji hello.

Interpretuj wyniki hello w następujący sposób:

| Wartości wyników Azperflib.exe | Stan kondycji monitorowania Azure |
| --- | --- |
| **Wywołania API — nie jest dostępna** | Liczniki, które nie są dostępne może być albo toohello nie dotyczy konfiguracji maszyny wirtualnej lub błędów. Zobacz **stan kondycji**. |
| **Łącznie liczniki — pusty** |Witaj następujące dwa liczniki magazynu Azure może być pusta: <ul><li>Op opóźnienie odczytu magazynu serwera (MS)</li><li>Op opóźnienie odczytu magazynu E2E (MS)</li></ul>Wszystkie inne liczniki muszą mieć wartości. |
| **Stan kondycji** |Jeśli tylko OK zwracać pokazuje stan **OK**. |
| **Diagnostyka** |Szczegółowe informacje o stanie kondycji. |

Jeśli hello **stan kondycji** wartość nie jest **OK**, postępuj zgodnie z instrukcjami hello [sprawdzenie kondycji dla konfiguracji monitorowania infrastruktury platformy Azure] [ deployment-guide-5.2].

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a>Uruchom sprawdzanie gotowości hello na Maszynę wirtualną systemu Linux

1.  Połącz toohello maszyny wirtualnej platformy Azure przy użyciu protokołu SSH.

2.  Sprawdź dane wyjściowe hello hello Azure rozszerzone monitorowanie rozszerzenia.

  a.  Uruchom polecenie `more /var/lib/AzureEnhancedMonitor/PerfCounters`

   **Oczekiwany wynik**: zwraca listę liczników wydajności. Witaj pliku nie może być pusta.

 b. Uruchom polecenie `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`

   **Oczekiwano wyniku**: zwraca jeden wiersz w przypadku błędu hello **Brak**, na przykład **3; konfiguracji; Błąd; 0; 0; Brak; 0; 1456416792; tst servercs;**

  c. Uruchom polecenie `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`

    **Oczekiwany wynik**: zwraca jako pusta lub nie istnieje.

Jeśli hello poprzedniego wyboru zakończyła się niepowodzeniem, należy uruchomić następujące dodatkowe kontrole:

1.  Upewnij się, że agenta waagent hello jest zainstalowane i włączone.

  a.  Uruchom polecenie `sudo ls -al /var/lib/waagent/`

      **Oczekiwany wynik**: Wyświetla zawartość hello hello agenta waagent katalogu.

  b.  Uruchom polecenie `ps -ax | grep waagent`

   **Oczekiwany wynik**: Wyświetla jednego wpisu podobnego do:`python /usr/sbin/waagent -daemon`

2. Upewnij się, że hello Linux rozszerzenia diagnostycznych jest zainstalowany i włączony.

  a.  Uruchom polecenie `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'`

   **Oczekiwany wynik**: Wyświetla zawartość hello hello rozszerzenia diagnostycznych Linux katalogu.

 b. Uruchom polecenie `ps -ax | grep diagnostic`

   **Oczekiwany wynik**: Wyświetla jednego wpisu podobnego do:`python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`

3.   Upewnij się, że tego rozszerzenia rozszerzonego monitorowania Azure hello jest zainstalowana i uruchomiona.

  a.  Uruchom polecenie `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'`

    **Oczekiwany wynik**: Wyświetla zawartość hello hello Azure rozszerzone monitorowanie rozszerzenia katalogu.

  b. Uruchom polecenie `ps -ax | grep AzureEnhanced`

     **Oczekiwany wynik**: Wyświetla jednego wpisu podobnego do:`python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`

3. Zainstaluj agenta hosta SAP, zgodnie z opisem w Uwaga SAP [1031096]i sprawdź dane wyjściowe hello `saposcol`.

  a.  Uruchom polecenie `/usr/sap/hostctrl/exe/saposcol -d`

  b.  Uruchom polecenie `dump ccm`

  c.  Sprawdź czy hello **Virtualization_Configuration\Enhanced monitorowania dostępu** Metryka to **true**.

Jeśli masz już zainstalowany serwer aplikacji SAP NetWeaver ABAP, otwórz transakcji ST06 i sprawdź, czy jest włączone monitorowanie rozszerzonej.

Jeśli żadnego z wymienionych testów zakończyć się niepowodzeniem i szczegółowe informacje dotyczące sposobu tooredeploy hello rozszerzenia, zobacz [Rozwiązywanie problemów hello monitorowania infrastruktury platformy Azure dla programu SAP][deployment-guide-5.3].

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Sprawdzanie kondycji dla hello konfiguracji monitorowania infrastruktury platformy Azure
Jeśli niektóre dane monitorowania hello nie zostanie dostarczone poprawnie wskazywany przez hello test opisanego w [sprawdzanie gotowości do rozszerzonego monitorowania Azure dla programu SAP][deployment-guide-5.1]Uruchom hello `Test-AzureRmVMAEMExtension` toocheck polecenia cmdlet Określa, czy hello Azure Monitorowanie infrastruktury i rozszerzenie dotyczące monitorowania dla programu SAP hello są poprawnie skonfigurowane.

1.  Upewnij się, że zainstalowano najnowszą wersję hello hello Azure polecenia cmdlet programu PowerShell, zgodnie z opisem w [poleceń cmdlet wdrażania programu Azure PowerShell][deployment-guide-4.1].
2.  Uruchom następujące polecenia cmdlet programu PowerShell hello. Aby uzyskać listę dostępnych środowisk, uruchom polecenie cmdlet hello `Get-AzureRmEnvironment`. toouse publicznej platformy Azure, wybierz hello **AzureCloud** środowiska. Dla platformy Azure w Chinach, wybierz **AzureChinaCloud**.
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  Wprowadź dane konta i zidentyfikuj hello maszyny wirtualnej platformy Azure.

  ![Wejściowy strony specyficzne dla programu SAP Azure polecenia cmdlet Test-VMConfigForSAP_GUI][deployment-guide-figure-1200]

4. Witaj skryptu testy hello konfiguracji maszyny wirtualnej hello należy wybrać.

  ![Dane wyjściowe pomyślnie testu hello monitorowania infrastruktury platformy Azure dla programu SAP][deployment-guide-figure-1300]

Upewnij się, że każdy wynik sprawdzania kondycji jest **OK**. Jeśli niektóre testy nie są wyświetlane **OK**, uruchom polecenie cmdlet update hello, zgodnie z opisem w [Konfiguruj hello Azure ulepszone rozszerzenie monitorowania dla programu SAP][deployment-guide-4.5]. Poczekaj 15 minut i kontroli powtarzania hello opisanych w [sprawdzanie gotowości do rozszerzonego monitorowania Azure dla programu SAP] [ deployment-guide-5.1] i [sprawdzenie kondycji dla konfiguracji infrastruktury monitorowania Azure] [deployment-guide-5.2]. Jeśli sprawdzenie hello nadal wskazywać na problem z niektórych lub wszystkich liczników, zobacz [Rozwiązywanie problemów hello monitorowania infrastruktury platformy Azure dla programu SAP][deployment-guide-5.3].

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Rozwiązywanie problemów z hello monitorowania infrastruktury platformy Azure dla programu SAP

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] Liczniki wydajności usługi Azure nie są wyświetlane w ogóle
Usługa AzureEnhancedMonitoring Windows Hello zbiera metryki wydajności na platformie Azure. Usługa hello nie został poprawnie zainstalowany lub nie jest uruchomiony w maszynie Wirtualnej, nie metryki wydajności mogą być zbierane.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>katalog instalacji Hello hello Azure rozszerzone monitorowanie rozszerzenia jest pusta

###### <a name="issue"></a>Problem
Katalog instalacyjny Hello C:\\pakiety\\wtyczek\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;wersji >\\upuszczania jest pusta.

###### <a name="solution"></a>Rozwiązanie
nie zainstalowano rozszerzenia Hello. Ustal, czy jest to problem serwera proxy (zgodnie z wcześniejszym opisem). Może być konieczne toorestart hello maszyny lub uruchom ponownie hello `Set-AzureRmVMAEMExtension` skryptu konfiguracji.

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a>Usługa Azure rozszerzonego monitorowania nie istnieje.

###### <a name="issue"></a>Problem
Usługa AzureEnhancedMonitoring Windows Hello nie istnieje.

Dane wyjściowe Azperflib.exe zwraca błąd:

![Wykonanie azperflib.exe wskazuje, że nie jest uruchomiona usługa hello hello rozszerzenia rozszerzonego monitorowania Azure dla programu SAP][deployment-guide-figure-1400]
<a name="figure-14"></a>

###### <a name="solution"></a>Rozwiązanie
Jeśli usługa hello nie istnieje, hello Azure ulepszone rozszerzenie monitorowania dla programu SAP ma nie został poprawnie zainstalowany. Należy ponownie wdrożyć hello rozszerzenia przy użyciu hello opisane dla danego scenariusza wdrażania w [scenariuszy wdrażania maszyn wirtualnych dla programu SAP na platformie Azure][deployment-guide-3].

Po wdrożeniu rozszerzenie hello, po upływie godziny, sprawdź ponownie czy liczniki wydajności usługi Azure hello znajdują się w hello maszyny Wirtualnej platformy Azure.

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a>Usługa Azure rozszerzonego monitorowania istnieje, ale nie powiedzie się toostart

###### <a name="issue"></a>Problem
Usługa AzureEnhancedMonitoring Windows Hello istnieje i jest włączona, ale nie powiedzie się toostart. Aby uzyskać więcej informacji Sprawdź dziennik zdarzeń aplikacji hello.

###### <a name="solution"></a>Rozwiązanie
Konfiguracja Hello jest nieprawidłowa. Uruchom ponownie hello monitorowania rozszerzenie hello maszyny Wirtualnej, zgodnie z opisem w [Konfiguruj hello Azure ulepszone rozszerzenie monitorowania dla programu SAP][deployment-guide-4.5].

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] Brak niektóre liczniki wydajności usługi Azure
Usługa AzureEnhancedMonitoring Windows Hello zbiera metryki wydajności na platformie Azure. Usługa Hello pobiera dane z wielu źródeł. Niektóre dane konfiguracji są zbierane lokalnie, a niektóre metryki wydajności są odczytywane z diagnostyki Azure. Liczniki magazynu są używane z Twojej rejestrowania na poziomie subskrypcji hello magazynu.

Jeśli Rozwiązywanie problemów przy użyciu Uwaga SAP [1999351] nie rozwiązać problem hello, uruchom ponownie hello `Set-AzureRmVMAEMExtension` skryptu konfiguracji. Ponieważ liczniki analityka lub diagnostyki magazynu nie można tworzyć bezpośrednio po są włączone, konieczne może być toowait na godzinę. Jeśli hello problem będzie się powtarzał, należy otworzyć komunikat pomocy technicznej SAP klienta na powitania BC-OP-NT-AZR składnika dla systemu Windows lub BC-OP-LNX-AZR dla maszyny wirtualnej systemu Linux.

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] Liczniki wydajności usługi Azure nie są wyświetlane w ogóle
Metryki wydajności na platformie Azure są zbierane przez demon. Jeśli demon hello nie jest uruchomiona, nie metryki wydajności mogą być zbierane.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>katalog instalacji Hello hello Azure rozszerzone monitorowanie rozszerzenia jest pusta

###### <a name="issue"></a>Problem
katalog Hello \\var\\lib\\agenta waagent\\ nie ma podkatalogu dla hello Azure rozszerzone monitorowanie rozszerzenia.

###### <a name="solution"></a>Rozwiązanie
nie zainstalowano rozszerzenia Hello. Ustal, czy jest to problem serwera proxy (zgodnie z wcześniejszym opisem). Może być konieczne toorestart hello maszyny i/lub uruchom ponownie hello `Set-AzureRmVMAEMExtension` skryptu konfiguracji.

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] Brak niektóre liczniki wydajności usługi Azure
Metryki wydajności na platformie Azure są zbierane przez demona, która pobiera dane z wielu źródeł. Niektóre dane konfiguracji są zbierane lokalnie, a niektóre metryki wydajności są odczytywane z diagnostyki Azure. Liczniki magazynu pochodzą z dzienników hello w ramach subskrypcji magazynu.

Pełne i aktualne listę znanych problemów, zobacz Uwaga SAP [1999351], która zawiera dodatkowe informacje dotyczące rozwiązywania problemów do rozszerzonego monitorowania Azure dla programu SAP.

Jeśli Rozwiązywanie problemów przy użyciu Uwaga SAP [1999351] nie rozwiązać problem hello, uruchom ponownie hello `Set-AzureRmVMAEMExtension` skryptu konfiguracji zgodnie z opisem w [Konfiguruj hello Azure ulepszone rozszerzenie monitorowania dla programu SAP][deployment-guide-4.5]. Konieczne może być toowait na godziny, ponieważ liczniki analityka lub diagnostyki magazynu nie można tworzyć bezpośrednio po są włączone. Jeśli hello problem będzie się powtarzał, należy otworzyć komunikat pomocy technicznej SAP klienta na powitania BC-OP-NT-AZR składnika dla systemu Windows lub BC-OP-LNX-AZR dla maszyny wirtualnej systemu Linux.
