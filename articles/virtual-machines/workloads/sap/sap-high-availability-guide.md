---
title: "Azure maszyn wirtualnych wysokiej dostępności dla programu SAP NetWeaver | Dokumentacja firmy Microsoft"
description: "Przewodnik wysokiej dostępności dla programu SAP NetWeaver na maszynach wirtualnych platformy Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d00db895ffcf9ba9a51e3df2dae5d33c0277dd6f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a><span data-ttu-id="e3197-103">Azure maszyn wirtualnych wysokiej dostępności dla programu SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="e3197-103">Azure Virtual Machines high availability for SAP NetWeaver</span></span>

<span data-ttu-id="e3197-104">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="e3197-104">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="e3197-105">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="e3197-105">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
<span data-ttu-id="e3197-106">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="e3197-106">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="e3197-107">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="e3197-107">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="e3197-108">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="e3197-108">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



<span data-ttu-id="e3197-109">Maszyny wirtualne platformy Azure to rozwiązanie dla organizacji, które muszą obliczeniowych, magazynu i zasobów sieciowych w czasie minimalnego i bez cykle nabywania długie.</span><span class="sxs-lookup"><span data-stu-id="e3197-109">Azure Virtual Machines is the solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="e3197-110">Maszyny wirtualne Azure służy do wdrażania aplikacji klasycznej jak SAP NetWeaver na podstawie ABAP, Java i stosu ABAP + Java.</span><span class="sxs-lookup"><span data-stu-id="e3197-110">You can use Azure Virtual Machines to deploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="e3197-111">Rozszerzenie, niezawodności i dostępności bez dodatkowych lokalnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="e3197-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="e3197-112">Maszyny wirtualne platformy Azure obsługuje łączności między lokalizacjami, maszynach wirtualnych platformy Azure można zintegrować lokalnej domeny Twojej organizacji, chmur prywatnych i pozioma systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="e3197-113">W tym artykule firma Microsoft opisano kroki, które należy wykonać w celu wdrażania systemów SAP wysokiej dostępności na platformie Azure przy użyciu modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e3197-113">In this article, we cover the steps that you can take to deploy high-availability SAP systems in Azure by using the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="e3197-114">Firma Microsoft przeprowadzi użytkownika przez proces te zadania główne:</span><span class="sxs-lookup"><span data-stu-id="e3197-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="e3197-115">Znajdź prawo SAP uwagi i przewodniki dotyczące instalacji, na liście [zasobów] [ sap-ha-guide-2] sekcji.</span><span class="sxs-lookup"><span data-stu-id="e3197-115">Find the right SAP Notes and installation guides, listed in the [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="e3197-116">W tym artykule uzupełnia SAP instalacji dokumentacji i notatek SAP, które są głównej zasoby, które ułatwiają instalowanie i wdrażanie oprogramowania SAP na określonych platformach.</span><span class="sxs-lookup"><span data-stu-id="e3197-116">This article complements SAP installation documentation and SAP Notes, which are the primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="e3197-117">Dowiedz się różnic między modelu wdrażania usługi Azure Resource Manager i model klasyczny wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-117">Learn the differences between the Azure Resource Manager deployment model and the Azure classic deployment model.</span></span>
* <span data-ttu-id="e3197-118">Więcej informacji na temat trybów kworum klastra trybu Failover systemu Windows Server, w którym można wybrać modelu, które jest odpowiednie dla danego wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-118">Learn about Windows Server Failover Clustering quorum modes, so you can select the model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="e3197-119">Więcej informacji na temat systemu Windows Server Failover Clustering udostępnionego magazynu w usług Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="e3197-120">Dowiedz się, jak chronić pojedynczego punktu z awarii składników jak zaawansowane biznesowych aplikacji programowania (ABAP) SAP centralnej usług (ASCS) / SAP centralnej usługi (SCS) i systemy zarządzania bazami danych (DBMS) i działanie elementów nadmiarowych, takie jak SAP serwera aplikacji, na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-120">Learn how to help protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="e3197-121">Wykonaj krok przykład instalację i konfigurację systemu SAP wysokiej dostępności w klastrze systemu Windows Server Failover Clustering na platformie Azure przy użyciu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e3197-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="e3197-122">Więcej informacji na temat dodatkowych czynności wymaganych do używania systemu Windows Server Failover Clustering w Azure, ale nie są wymagane w przypadku lokalnego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e3197-122">Learn about additional steps required to use Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="e3197-123">Aby uprościć wdrażanie i konfigurowanie, w tym artykule używamy szablony Menedżera zasobów systemu SAP trójwarstwowa wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="e3197-123">To simplify deployment and configuration, in this article, we use the SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="e3197-124">Szablony zautomatyzować wdrożenie całej infrastruktury potrzebnym do systemu SAP wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="e3197-124">The templates automate deployment of the entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="e3197-125">Infrastruktura obsługuje również rozmiaru SAP aplikacji wydajności standardowe (protokoły SAP) systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-125">The infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="e3197-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e3197-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="e3197-127">Przed rozpoczęciem upewnij się, że spełniają wymagania wstępne, które są opisane w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="e3197-127">Before you start, make sure that you meet the prerequisites that are described in the following sections.</span></span> <span data-ttu-id="e3197-128">Ponadto należy sprawdzić wszystkich zasobów wymienionych w [zasobów] [ sap-ha-guide-2] sekcji.</span><span class="sxs-lookup"><span data-stu-id="e3197-128">Also, be sure to check all resources listed in the [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="e3197-129">W tym artykule używamy szablonów usługi Azure Resource Manager dla [trójwarstwowa SAP NetWeaver za pomocą dysków zarządzanych](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span><span class="sxs-lookup"><span data-stu-id="e3197-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span></span> <span data-ttu-id="e3197-130">Przydatne Omówienie szablonów, zobacz [szablony Menedżera zasobów Azure SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="e3197-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="e3197-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a>Zasoby</span><span class="sxs-lookup"><span data-stu-id="e3197-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="e3197-132">Artykuły te obejmują wdrożenia SAP na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="e3197-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="e3197-133">[Azure maszyn wirtualnych, planowania i wdrażania dla programu SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="e3197-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="e3197-134">[Maszyny wirtualne Azure wdrożenia SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="e3197-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="e3197-135">[Azure wdrożenia SAP NetWeaver DBMS maszyny wirtualne][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="e3197-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="e3197-136">[Azure maszyn wirtualnych wysokiej dostępności dla programu SAP NetWeaver (w tym przewodniku)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="e3197-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="e3197-137">Jeśli to możliwe, możemy umożliwiają łącze do odwołującego się Przewodnik instalacji SAP (zobacz [Przewodnik po instalacji programu SAP][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="e3197-137">Whenever possible, we give you a link to the referring SAP installation guide (see the [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="e3197-138">Wymagania wstępne i informacje o procesie instalacji jest dobrym pomysłem jest dokładnie przeczytać SAP NetWeaver przewodniki instalacji.</span><span class="sxs-lookup"><span data-stu-id="e3197-138">For prerequisites and information about the installation process, it's a good idea to read the SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="e3197-139">W tym artykule opisano tylko określone zadania dla systemów opartych na procesorze SAP NetWeaver, których można użyć z maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="e3197-140">Te informacje SAP są związane z tym tematem SAP na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="e3197-140">These SAP Notes are related to the topic of SAP in Azure:</span></span>

| <span data-ttu-id="e3197-141">Numer</span><span class="sxs-lookup"><span data-stu-id="e3197-141">Note number</span></span> | <span data-ttu-id="e3197-142">Tytuł</span><span class="sxs-lookup"><span data-stu-id="e3197-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="e3197-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="e3197-143">[1928533]</span></span> |<span data-ttu-id="e3197-144">Aplikacje SAP na platformie Azure: obsługiwane produktów i zmiana rozmiaru</span><span class="sxs-lookup"><span data-stu-id="e3197-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="e3197-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="e3197-145">[2015553]</span></span> |<span data-ttu-id="e3197-146">SAP na platformie Microsoft Azure: obsługuje wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e3197-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="e3197-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="e3197-147">[1999351]</span></span> |<span data-ttu-id="e3197-148">Rozszerzone monitorowanie Azure dla programu SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="e3197-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="e3197-149">[2178632]</span></span> |<span data-ttu-id="e3197-150">Klucz monitorowania metryki dla SAP na platformie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e3197-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="e3197-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="e3197-151">[1999351]</span></span> |<span data-ttu-id="e3197-152">Wirtualizacji w systemie Windows: rozszerzonego monitorowania</span><span class="sxs-lookup"><span data-stu-id="e3197-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="e3197-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="e3197-153">[2243692]</span></span> |<span data-ttu-id="e3197-154">Użycie magazynu SSD Azure — wersja Premium dla wystąpienia systemu DBMS SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="e3197-155">Dowiedz się więcej o [ograniczenia subskrypcji platformy Azure][azure-subscription-service-limits-subscription], w tym domyślne ogólne ograniczenia i ograniczenia maksymalnej.</span><span class="sxs-lookup"><span data-stu-id="e3197-155">Learn more about the [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="e3197-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP wysokiej dostępności z usługi Azure Resource Manager a Azure klasycznym modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="e3197-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. the Azure classic deployment model</span></span>
<span data-ttu-id="e3197-157">Usługi Azure Resource Manager i usługi Azure klasycznych modeli wdrażania różnią się w następujących obszarach:</span><span class="sxs-lookup"><span data-stu-id="e3197-157">The Azure Resource Manager and Azure classic deployment models are different in the following areas:</span></span>

- <span data-ttu-id="e3197-158">Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="e3197-158">Resource groups</span></span>
- <span data-ttu-id="e3197-159">Zależności usługi równoważenia obciążenia wewnętrznego platformy Azure na grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e3197-159">Azure internal load balancer dependency on the Azure resource group</span></span>
- <span data-ttu-id="e3197-160">Obsługa scenariuszy identyfikatora SID multi SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="e3197-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a>Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="e3197-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="e3197-162">W systemie Azure Resource Manager można użyć grup zasobów do zarządzania wszystkie zasoby aplikacji w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-162">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="e3197-163">Podejście, w grupie zasobów, wszystkie zasoby mają tego samego cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="e3197-163">An integrated approach, in a resource group, all resources have the same life cycle.</span></span> <span data-ttu-id="e3197-164">Na przykład wszystkie zasoby są tworzone w tym samym czasie i są usuwane w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="e3197-164">For example, all resources are created at the same time and they are deleted at the same time.</span></span> <span data-ttu-id="e3197-165">Dowiedz się więcej o [grupach zasobów](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="e3197-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="e3197-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Zależności usługi równoważenia obciążenia wewnętrznego platformy Azure na grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e3197-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on the Azure resource group</span></span>

<span data-ttu-id="e3197-167">W modelu wdrażania klasycznego Azure istnieje zależność między Azure wewnętrznego modułu równoważenia obciążenia (usługa Azure Load Balancer) i usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e3197-167">In the Azure classic deployment model, there is a dependency between the Azure internal load balancer (Azure Load Balancer service) and the cloud service.</span></span> <span data-ttu-id="e3197-168">Co wewnętrzny moduł równoważenia obciążenia musi jedną usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e3197-168">Every internal load balancer needs one cloud service.</span></span>

<span data-ttu-id="e3197-169">W usłudze Azure Resource Manager, co zasobów platformy Azure musi być umieszczona w grupie zasobów platformy Azure i jest nieprawidłowa dla usługi równoważenia obciążenia Azure również.</span><span class="sxs-lookup"><span data-stu-id="e3197-169">In Azure Resource Manager, every Azure resource needs to be placed into an Azure resource group, and this is valid for Azure Load Balancer as well.</span></span> <span data-ttu-id="e3197-170">Jednak nie musi mieć jedną grupę zasobów platformy Azure dla usługi równoważenia obciążenia Azure, np. jedna grupa zasobów platformy Azure może zawierać wiele Azure usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e3197-170">However, there is no need to have one Azure resource group per Azure load balancer, e.g. one Azure resource group can contain multiple Azure Load Balancers.</span></span> <span data-ttu-id="e3197-171">Środowisko jest prostszy i bardziej elastyczne.</span><span class="sxs-lookup"><span data-stu-id="e3197-171">The environment is simpler and more flexible.</span></span> 

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="e3197-172">Obsługa scenariuszy identyfikatora SID multi SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-172">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="e3197-173">W systemie Azure Resource Manager można zainstalować wielu SAP identyfikator ASCS/SCS wystąpień systemu w jednym klastrze.</span><span class="sxs-lookup"><span data-stu-id="e3197-173">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="e3197-174">Identyfikator SID wielu wystąpień jest możliwe dzięki obsłudze wielu adresów IP dla każdego Azure wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e3197-174">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="e3197-175">Aby użyć Azure klasycznym modelu wdrażania, wykonaj procedury opisane w temacie [SAP NetWeaver na platformie Azure: wystąpień klastrowania SAP ASCS/SCS przy użyciu klastra trybu Failover systemu Windows Server na platformie Azure z SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="e3197-175">To use the Azure classic deployment model, follow the procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3197-176">Zdecydowanie zaleca się użycie modelu wdrażania usługi Azure Resource Manager dla instalacji programu SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-176">We strongly recommend that you use the Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="e3197-177">Oferuje wiele korzyści, które nie są dostępne w klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="e3197-177">It offers many benefits that are not available in the classic deployment model.</span></span> <span data-ttu-id="e3197-178">Dowiedz się więcej o usłudze Azure [modele wdrażania][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="e3197-178">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="e3197-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a>Klaster trybu Failover serwera systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e3197-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="e3197-180">Windows Server Failover Clustering jest podstawą SAP ASCS/SCS instalacji wysokiej dostępności i bazami danych w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="e3197-180">Windows Server Failover Clustering is the foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="e3197-181">Klaster trybu failover to grupa 1 + n niezależnych serwerów (węzłów), które współpracują ze sobą w celu zwiększenia dostępności aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="e3197-181">A failover cluster is a group of 1+n independent servers (nodes) that work together to increase the availability of applications and services.</span></span> <span data-ttu-id="e3197-182">W przypadku awarii węzła usługi Windows Server Failover Clustering oblicza liczbę błędów, które mogą wystąpić przy zachowaniu dobrej kondycji klastra zapewnienie aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="e3197-182">If a node failure occurs, Windows Server Failover Clustering calculates the number of failures that can occur while maintaining a healthy cluster to provide applications and services.</span></span> <span data-ttu-id="e3197-183">Istnieje możliwość z kworum różne tryby osiągnięcia klastra trybu failover.</span><span class="sxs-lookup"><span data-stu-id="e3197-183">You can choose from different quorum modes to achieve failover clustering.</span></span>

### <span data-ttu-id="e3197-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a>Tryb kworum</span><span class="sxs-lookup"><span data-stu-id="e3197-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="e3197-185">Korzystając z usługi Windows Server Failover Clustering można wybrać z czterech trybów kworum:</span><span class="sxs-lookup"><span data-stu-id="e3197-185">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="e3197-186">**Większość węzłów**.</span><span class="sxs-lookup"><span data-stu-id="e3197-186">**Node Majority**.</span></span> <span data-ttu-id="e3197-187">Głosować na każdym węźle klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-187">Each node of the cluster can vote.</span></span> <span data-ttu-id="e3197-188">Klaster działa tylko z większością głosów, czyli z więcej niż połowy głosów.</span><span class="sxs-lookup"><span data-stu-id="e3197-188">The cluster functions only with a majority of votes, that is, with more than half the votes.</span></span> <span data-ttu-id="e3197-189">Firma Microsoft zaleca tej opcji w przypadku klastrów nieparzysta liczba węzłów.</span><span class="sxs-lookup"><span data-stu-id="e3197-189">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="e3197-190">Na przykład trzech węzłów w klastrze siedem może zakończyć się niepowodzeniem, a aparaturze klastra osiąga większości i kontynuuje działanie.</span><span class="sxs-lookup"><span data-stu-id="e3197-190">For example, three nodes in a seven-node cluster can fail, and the cluster stills achieves a majority and continues to run.</span></span>  
* <span data-ttu-id="e3197-191">**Większość węzłów i dysków**.</span><span class="sxs-lookup"><span data-stu-id="e3197-191">**Node and Disk Majority**.</span></span> <span data-ttu-id="e3197-192">Każdy węzeł i wyznaczonych dysku (monitorem dysku) w magazynie klastra można głosowania, gdy są one dostępne i w komunikacie.</span><span class="sxs-lookup"><span data-stu-id="e3197-192">Each node and a designated disk (a disk witness) in the cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="e3197-193">Klaster działa tylko z większością głosów, oznacza to, z więcej niż połowy głosów.</span><span class="sxs-lookup"><span data-stu-id="e3197-193">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="e3197-194">W tym trybie ma sens w środowisku klastra z parzystą liczbą węzłów.</span><span class="sxs-lookup"><span data-stu-id="e3197-194">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="e3197-195">Jeśli połowa węzłów i dysk są w trybie online, gdy klaster będzie pozostawał w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="e3197-195">If half the nodes and the disk are online, the cluster remains in a healthy state.</span></span>
* <span data-ttu-id="e3197-196">**Węzeł i udziału plików większość**.</span><span class="sxs-lookup"><span data-stu-id="e3197-196">**Node and File Share Majority**.</span></span> <span data-ttu-id="e3197-197">Każdy węzeł plus udział plików wyznaczonych (monitora udziału plików), który administrator tworzy głosować, niezależnie od tego, czy są dostępne węzły i udziału plików i komunikacji.</span><span class="sxs-lookup"><span data-stu-id="e3197-197">Each node plus a designated file share (a file share witness) that the administrator creates can vote, regardless of whether the nodes and file share are available and in communication.</span></span> <span data-ttu-id="e3197-198">Klaster działa tylko z większością głosów, oznacza to, z więcej niż połowy głosów.</span><span class="sxs-lookup"><span data-stu-id="e3197-198">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="e3197-199">W tym trybie ma sens w środowisku klastra z parzystą liczbą węzłów.</span><span class="sxs-lookup"><span data-stu-id="e3197-199">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="e3197-200">Jest on podobny do trybu Większość węzłów i dysków, ale zamiast monitora dysku używa monitora udziału plików.</span><span class="sxs-lookup"><span data-stu-id="e3197-200">It's similar to the Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="e3197-201">Ten tryb jest łatwa do wdrożenia, ale jeśli udział plików sam nie ma wysokiej dostępności, mogą stać się pojedynczym punktem awarii.</span><span class="sxs-lookup"><span data-stu-id="e3197-201">This mode is easy to implement, but if the file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="e3197-202">**Bez większości: Na dysku tylko**.</span><span class="sxs-lookup"><span data-stu-id="e3197-202">**No Majority: Disk Only**.</span></span> <span data-ttu-id="e3197-203">Klaster ma kworum, jeśli jeden węzeł jest dostępny i komunikuje się z określonym dyskiem w magazynie klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-203">The cluster has a quorum if one node is available and in communication with a specific disk in the cluster storage.</span></span> <span data-ttu-id="e3197-204">Tylko węzły, które są także komunikuje się z tego dysku, można dołączyć do klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-204">Only the nodes that also are in communication with that disk can join the cluster.</span></span> <span data-ttu-id="e3197-205">Zaleca się, że nie należy używać tego trybu.</span><span class="sxs-lookup"><span data-stu-id="e3197-205">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="e3197-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a>Windows Server awaryjnej lokalnej</span><span class="sxs-lookup"><span data-stu-id="e3197-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="e3197-207">Rysunek 1 pokazuje klastra z dwoma węzłami.</span><span class="sxs-lookup"><span data-stu-id="e3197-207">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="e3197-208">Jeśli udostępnianie połączenie sieciowe między węzły kończy się niepowodzeniem i zarówno Pozostań węzłów w zapasowej i uruchamiania, dysku kworum lub pliku Określa, który węzeł będzie dostarczać aplikacji i usług klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-208">If the network connection between the nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue to provide the cluster's applications and services.</span></span> <span data-ttu-id="e3197-209">Węzeł, który ma dostęp do udziału pliku lub dysku kworum jest węzeł, który zapewnia, że usługi.</span><span class="sxs-lookup"><span data-stu-id="e3197-209">The node that has access to the quorum disk or file share is the node that ensures that services continue.</span></span>

<span data-ttu-id="e3197-210">Ponieważ w tym przykładzie użyto dwa węzły klastra, używamy Tryb kworum Większość węzłów i plików udziału.</span><span class="sxs-lookup"><span data-stu-id="e3197-210">Because this example uses a two-node cluster, we use the Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="e3197-211">Większość węzłów i dysków również jest prawidłową opcją.</span><span class="sxs-lookup"><span data-stu-id="e3197-211">The Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="e3197-212">W środowisku produkcyjnym zaleca się, że używasz dysku kworum.</span><span class="sxs-lookup"><span data-stu-id="e3197-212">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="e3197-213">Można użyć technologii systemu sieci i magazynu o wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="e3197-213">You can use network and storage system technology to make it highly available.</span></span>

![Rysunek 1: Na przykład Windows Server Failover Clustering konfiguracji dla programu SAP ASCS/SCS na platformie Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="e3197-215">_**Rysunek 1.** przykład Windows Server Failover Clustering konfiguracji dla programu SAP ASCS/SCS na platformie Azure_</span><span class="sxs-lookup"><span data-stu-id="e3197-215">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="e3197-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a>Magazyn udostępniony</span><span class="sxs-lookup"><span data-stu-id="e3197-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="e3197-217">Rysunek 1 pokazuje również klastra magazynu udostępnionego z dwoma węzłami.</span><span class="sxs-lookup"><span data-stu-id="e3197-217">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="e3197-218">W lokalnej klastra magazynu udostępnionego wszystkie węzły w klastrze wykryć magazynu udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="e3197-218">In an on-premises shared storage cluster, all nodes in the cluster detect shared storage.</span></span> <span data-ttu-id="e3197-219">Mechanizm blokowania chroni dane przed uszkodzeniem.</span><span class="sxs-lookup"><span data-stu-id="e3197-219">A locking mechanism protects the data from corruption.</span></span> <span data-ttu-id="e3197-220">Wszystkie węzły mogą wykryć, jeśli inny węzeł nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="e3197-220">All nodes can detect if another node fails.</span></span> <span data-ttu-id="e3197-221">Jeśli jeden węzeł ulegnie awarii, pozostałe węzeł przejmuje zasobów magazynu i zapewnia dostępność usług.</span><span class="sxs-lookup"><span data-stu-id="e3197-221">If one node fails, the remaining node takes ownership of the storage resources and ensures the availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="e3197-222">Nie trzeba udostępnionych dysków wysokiej dostępności z niektórymi aplikacjami systemu DBMS, takich jak z programem SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e3197-222">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="e3197-223">SQL Server AlwaysOn replikuje DBMS danych i plików dziennika z lokalnego dysku jednego węzła klastra na lokalny dysk innego węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-223">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="e3197-224">W takim przypadku konfiguracji klastra systemu Windows nie wymaga udostępnionego dysku.</span><span class="sxs-lookup"><span data-stu-id="e3197-224">In that case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="e3197-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a>Sieci i rozpoznawanie nazw</span><span class="sxs-lookup"><span data-stu-id="e3197-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="e3197-226">Komputery klienckie osiągnąć klastra za pośrednictwem wirtualnego adresu IP i nazwy hostów wirtualnych, które udostępnia serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="e3197-226">Client computers reach the cluster over a virtual IP address and a virtual host name that the DNS server provides.</span></span> <span data-ttu-id="e3197-227">Węzły lokalnymi i serwer DNS może obsługiwać wiele adresów IP.</span><span class="sxs-lookup"><span data-stu-id="e3197-227">The on-premises nodes and the DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="e3197-228">W typowej instalacji można użyć dwóch lub więcej połączeń sieciowych:</span><span class="sxs-lookup"><span data-stu-id="e3197-228">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="e3197-229">Dedykowane połączenie z magazynem</span><span class="sxs-lookup"><span data-stu-id="e3197-229">A dedicated connection to the storage</span></span>
* <span data-ttu-id="e3197-230">Połączenie z siecią wewnętrzną klastra dla pulsu</span><span class="sxs-lookup"><span data-stu-id="e3197-230">A cluster-internal network connection for the heartbeat</span></span>
* <span data-ttu-id="e3197-231">Używanego przez klientów Aby połączyć się z klastrem sieci publicznej</span><span class="sxs-lookup"><span data-stu-id="e3197-231">A public network that clients use to connect to the cluster</span></span>

## <span data-ttu-id="e3197-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a>Windows Server awaryjnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e3197-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="e3197-233">W porównaniu do bez systemu operacyjnego wdrożenia kompletnego stanu lub prywatnej chmury, maszyn wirtualnych Azure wymaga wykonania dodatkowych kroków do skonfigurowania klastra trybu Failover systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e3197-233">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="e3197-234">Podczas tworzenia dysku udostępnionego klastra, należy ustawić kilka adresów IP i nazwy hostów wirtualnych dla wystąpienia programu SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e3197-234">When you build a shared cluster disk, you need to set several IP addresses and virtual host names for the SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="e3197-235">W tym artykule omówiono kluczowe założenia i kolejne kroki wymagane do utworzenia klastra usług o wysokiej dostępności centralnej SAP na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-235">In this article, we discuss key concepts and the additional steps required to build an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="e3197-236">Firma Microsoft dowiesz się, jak skonfigurować narzędzia innej firmy SIOS DataKeeper oraz konfigurowania Azure wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e3197-236">We show you how to set up the third-party tool SIOS DataKeeper, and how to configure the Azure internal load balancer.</span></span> <span data-ttu-id="e3197-237">Te narzędzia służy do tworzenia klastra trybu failover systemu Windows z monitora udziału plików na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-237">You can use these tools to create a Windows failover cluster with a file share witness in Azure.</span></span>

![Rysunek 2: Windows Server Failover Clustering konfiguracji platformy Azure bez udostępnionego dysku][sap-ha-guide-figure-1001]

<span data-ttu-id="e3197-239">_**Rysunek 2.** Windows Server Failover Clustering konfiguracji na platformie Azure, bez udostępnionego dysku_</span><span class="sxs-lookup"><span data-stu-id="e3197-239">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="e3197-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a>Udostępniony dysk na platformie Azure z SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e3197-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="e3197-241">Należy klastra magazynu udostępnionego dla wystąpienia programu SAP ASCS/SCS wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="e3197-241">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="e3197-242">Począwszy od września 2016 r. Azure nie oferuje udostępnionego magazynu, którego można używać do tworzenia klastra magazynu udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="e3197-242">As of September 2016, Azure doesn't offer shared storage that you can use to create a shared storage cluster.</span></span> <span data-ttu-id="e3197-243">Oprogramowanie innych firm SIOS DataKeeper Cluster Edition umożliwia utworzenie magazynu dublowanej, która symuluje magazyn udostępniony klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-243">You can use third-party software SIOS DataKeeper Cluster Edition to create a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="e3197-244">Rozwiązanie SIOS zapewnia Replikacja synchroniczna danych w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="e3197-244">The SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="e3197-245">Jest to tworzenia zasobu dysku udostępnionego dla klastra:</span><span class="sxs-lookup"><span data-stu-id="e3197-245">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="e3197-246">Dodatkowy dysk należy dołączyć do poszczególnych maszyn wirtualnych (VM) w konfiguracji klastra systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="e3197-246">Attach an additional disk to each of the virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="e3197-247">Uruchamianie SIOS DataKeeper Cluster Edition w obu węzłach maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3197-247">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="e3197-248">Skonfiguruj SIOS DataKeeper Cluster Edition, aby go odzwierciedla zawartość woluminu dodatkowy dysk dołączony ze źródłowej maszyny wirtualnej, aby wielkość dodatkowy dysk dołączony docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3197-248">Configure SIOS DataKeeper Cluster Edition so that it mirrors the content of the additional disk attached volume from the source virtual machine to the additional disk attached volume of the target virtual machine.</span></span> <span data-ttu-id="e3197-249">SIOS DataKeeper abstracts lokalnych woluminów źródłowych i docelowych, a następnie je do systemu Windows Server Failover Clustering jako jeden dysk udostępniony.</span><span class="sxs-lookup"><span data-stu-id="e3197-249">SIOS DataKeeper abstracts the source and target local volumes, and then presents them to Windows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="e3197-250">Uzyskaj więcej informacji [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="e3197-250">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Rysunek 3: Windows Server Failover Clustering konfiguracji na platformie Azure z SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="e3197-252">_**Rysunek 3.** konfiguracji klastra trybu Failover systemu Windows Server na platformie Azure z SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e3197-252">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="e3197-253">Nie potrzebujesz wysokiej dostępności z niektórych produktów, bazami danych, takich jak SQL Server udostępnione dyski.</span><span class="sxs-lookup"><span data-stu-id="e3197-253">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="e3197-254">SQL Server AlwaysOn replikuje DBMS danych i plików dziennika z lokalnego dysku jednego węzła klastra na lokalny dysk innego węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-254">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="e3197-255">W takim przypadku konfiguracji klastra systemu Windows nie wymaga udostępnionego dysku.</span><span class="sxs-lookup"><span data-stu-id="e3197-255">In this case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="e3197-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Rozpoznawanie nazw w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="e3197-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="e3197-257">Chmury Azure platforma nie oferuje opcję, aby skonfigurować wirtualne adresy IP, takie jak adresy IP zmiennoprzecinkowych.</span><span class="sxs-lookup"><span data-stu-id="e3197-257">The Azure cloud platform doesn't offer the option to configure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="e3197-258">Należy rozwiązań alternatywnych, aby skonfigurować wirtualny adres IP do zasobu klastra w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e3197-258">You need an alternative solution to set up a virtual IP address to reach the cluster resource in the cloud.</span></span>
<span data-ttu-id="e3197-259">Platforma Azure ma wewnętrznego modułu równoważenia obciążenia w usłudze równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-259">Azure has an internal load balancer in the Azure Load Balancer service.</span></span> <span data-ttu-id="e3197-260">Z wewnętrznego modułu równoważenia obciążenia klienci osiągnąć klastra za pośrednictwem wirtualnego adresu IP klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-260">With the internal load balancer, clients reach the cluster over the cluster virtual IP address.</span></span>
<span data-ttu-id="e3197-261">Należy wdrożyć wewnętrznego modułu równoważenia obciążenia w grupie zasobów, która zawiera węzły klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-261">You need to deploy the internal load balancer in the resource group that contains the cluster nodes.</span></span> <span data-ttu-id="e3197-262">Następnie należy skonfigurować wszystkie niezbędne portu przekazywania reguły z badaniem porty wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e3197-262">Then, configure all necessary port forwarding rules with the probe ports of the internal load balancer.</span></span>
<span data-ttu-id="e3197-263">Klienci mogą łączyć się za pomocą nazwy hostów wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-263">The clients can connect via the virtual host name.</span></span> <span data-ttu-id="e3197-264">Serwer DNS rozpoznaje adres IP klastra, a port dojść modułu równoważenia obciążenia wewnętrznego przekazywania do aktywnego węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-264">The DNS server resolves the cluster IP address, and the internal load balancer handles port forwarding to the active node of the cluster.</span></span>

## <span data-ttu-id="e3197-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a>SAP NetWeaver wysokiej dostępności w Azure infrastruktury jako — usługa (IaaS)</span><span class="sxs-lookup"><span data-stu-id="e3197-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="e3197-266">Aby osiągnąć wysoką dostępność aplikacji SAP, takie jak dla składników oprogramowania SAP, musisz ochronę następujących składników:</span><span class="sxs-lookup"><span data-stu-id="e3197-266">To achieve SAP application high availability, such as for SAP software components, you need to protect the following components:</span></span>

* <span data-ttu-id="e3197-267">Wystąpienie serwera aplikacji SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-267">SAP Application Server instance</span></span>
* <span data-ttu-id="e3197-268">Wystąpienie programu SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-268">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="e3197-269">Serwer systemu DBMS</span><span class="sxs-lookup"><span data-stu-id="e3197-269">DBMS server</span></span>

<span data-ttu-id="e3197-270">Aby uzyskać więcej informacji o ochronie składników SAP w scenariuszach wysokiej dostępności, zobacz [maszyny wirtualne Azure planowania i wdrażania dla programu SAP NetWeaver][planning-guide-11].</span><span class="sxs-lookup"><span data-stu-id="e3197-270">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <span data-ttu-id="e3197-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a>Serwer aplikacji SAP wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="e3197-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="e3197-272">Zwykle nie trzeba konkretnego rozwiązania wysokiej dostępności dla wystąpień serwera aplikacji SAP i okna dialogowe.</span><span class="sxs-lookup"><span data-stu-id="e3197-272">You usually don't need a specific high-availability solution for the SAP Application Server and dialog instances.</span></span> <span data-ttu-id="e3197-273">Zapewniania wysokiej dostępności przez nadmiarowości i wiele wystąpień w oknie dialogowym należy skonfigurować w różnych wystąpień maszyn wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-273">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="e3197-274">Powinien mieć co najmniej dwóch wystąpień aplikacji SAP zainstalowane w dwóch wystąpień maszyn wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-274">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Rysunek 4: SAP wysokiej dostępności aplikacji serwera][sap-ha-guide-figure-2000]

<span data-ttu-id="e3197-276">_**Rysunek 4:** SAP wysokiej dostępności serwera aplikacji_</span><span class="sxs-lookup"><span data-stu-id="e3197-276">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="e3197-277">Należy umieścić wszystkich maszyn wirtualnych, które ustawić wystąpień serwera aplikacji SAP hosta w tym samym dostępności Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-277">You must place all virtual machines that host SAP Application Server instances in the same Azure availability set.</span></span> <span data-ttu-id="e3197-278">Zestaw dostępności Azure upewnia się, że:</span><span class="sxs-lookup"><span data-stu-id="e3197-278">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="e3197-279">Wszystkie maszyny wirtualne są częścią tej samej domeny uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="e3197-279">All virtual machines are part of the same upgrade domain.</span></span> <span data-ttu-id="e3197-280">Domeny uaktualnienia, na przykład upewnia się, że maszyny wirtualne nie są aktualizowane w tym samym czasie podczas zaplanowanej konserwacji przestoju.</span><span class="sxs-lookup"><span data-stu-id="e3197-280">An upgrade domain, for example, makes sure that the virtual machines aren't updated at the same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="e3197-281">Wszystkie maszyny wirtualne są częścią tej samej domenie błędów.</span><span class="sxs-lookup"><span data-stu-id="e3197-281">All virtual machines are part of the same fault domain.</span></span> <span data-ttu-id="e3197-282">Domeny błędów, na przykład upewnia się, że maszyny wirtualne są wdrażane tak, aby nie pojedynczego punktu awarii wpływa na dostępność maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-282">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects the availability of all virtual machines.</span></span>

<span data-ttu-id="e3197-283">Dowiedz się więcej o sposobie [Zarządzaj dostępnością maszyn wirtualnych][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="e3197-283">Learn more about how to [manage the availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="e3197-284">Niezarządzane tylko na dysku: ponieważ konto magazynu Azure jest potencjalnych pojedynczy punkt awarii, jest należy dysponować co najmniej dwa konta magazynu platformy Azure, w których dystrybuowane są przynajmniej dwie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="e3197-284">Unmanaged disk only: Because the Azure storage account is a potential single point of failure, it's important to have at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="e3197-285">W Instalatorze idealne dyski każdej maszyny wirtualnej, w którym jest uruchomione wystąpienie okna dialogowego SAP będzie można wdrożyć w innego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="e3197-285">In an ideal setup, the disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="e3197-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a>Wystąpienie programu SAP ASCS/SCS wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="e3197-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="e3197-287">Rysunek 5 jest przykładem wystąpienia SAP ASCS/SCS wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="e3197-287">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Rysunek 5: Wystąpienie wysokiej dostępności SAP ASCS/SCS][sap-ha-guide-figure-2001]

<span data-ttu-id="e3197-289">_**Rysunek 5.** SAP wysokiej dostępności ASCS/SCS wystąpienia_</span><span class="sxs-lookup"><span data-stu-id="e3197-289">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="e3197-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a>SAP ASCS/SCS wystąpienie wysokiej dostępności z systemu Windows Server Failover Clustering na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e3197-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="e3197-291">W porównaniu do bez systemu operacyjnego wdrożenia kompletnego stanu lub prywatnej chmury, maszyn wirtualnych Azure wymaga wykonania dodatkowych kroków do skonfigurowania klastra trybu Failover systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e3197-291">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="e3197-292">W celu zbudowania klastra pracy awaryjnej systemu Windows, należy dysku udostępnionego klastra, kilka adresów IP, kilka nazw hostów wirtualnych i Azure wewnętrznego modułu równoważenia obciążenia dla klastra z wystąpieniem SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e3197-292">To build a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="e3197-293">Omówiono to bardziej szczegółowo w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="e3197-293">We discuss this in more detail later in the article.</span></span>

![Rysunek 6: Windows Server Failover Clustering konfiguracji SAP ASCS/SCS na platformie Azure przy użyciu SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="e3197-295">_**Rysunek 6.** Windows Server Failover Clustering konfiguracji SAP ASCS/SCS na platformie Azure z SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e3197-295">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="e3197-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Wystąpienie systemu DBMS wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="e3197-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="e3197-297">Systemu DBMS jest również pojedynczy punkt kontaktu w systemie SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-297">The DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="e3197-298">Należy chronić go przy użyciu rozwiązania wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="e3197-298">You need to protect it by using a high-availability solution.</span></span> <span data-ttu-id="e3197-299">Rysunek nr 7 przedstawia rozwiązania wysokiej dostępności programu SQL Server zawsze na platformie Azure, Windows Server Failover Clustering i Azure wewnętrzne usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e3197-299">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and the Azure internal load balancer.</span></span> <span data-ttu-id="e3197-300">SQL Server AlwaysOn replikuje DBMS danych i plików dziennika przy użyciu własnego systemu DBMS replikacji.</span><span class="sxs-lookup"><span data-stu-id="e3197-300">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="e3197-301">W takim przypadku można nie muszą klastra udostępnione dyski, które upraszcza całą konfigurację.</span><span class="sxs-lookup"><span data-stu-id="e3197-301">In this case, you don't need cluster shared disks, which simplifies the entire setup.</span></span>

![Rysunek 7: Przykładem DBMS SAP wysokiej dostępności, z programu SQL Server AlwaysOn][sap-ha-guide-figure-2003]

<span data-ttu-id="e3197-303">_**Rysunek 7.** przykład DBMS SAP wysokiej dostępności, z programu SQL Server AlwaysOn_</span><span class="sxs-lookup"><span data-stu-id="e3197-303">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="e3197-304">Aby uzyskać więcej informacji o klastrach programu SQL Server na platformie Azure przy użyciu modelu wdrażania usługi Azure Resource Manager zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="e3197-304">For more information about clustering SQL Server in Azure by using the Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="e3197-305">[Konfiguruj zawsze włączone grupy dostępności w maszynach wirtualnych platformy Azure ręcznie przy użyciu usługi Resource Manager] [virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="e3197-305">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="e3197-306">[Konfiguruj Azure wewnętrznego modułu równoważenia obciążenia dla grupy dostępności AlwaysOn w Azure] [virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="e3197-306">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="e3197-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a>Scenariusze wdrażania wysokiej dostępności na trasie</span><span class="sxs-lookup"><span data-stu-id="e3197-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="e3197-308">Scenariusz wdrażania przy użyciu architektury 1 szablonu</span><span class="sxs-lookup"><span data-stu-id="e3197-308">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="e3197-309">Rysunek nr 8 przedstawia przykład architektury wysokiej dostępności programu SAP NetWeaver Azure **jeden** systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-309">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="e3197-310">Ten scenariusz jest skonfigurowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e3197-310">This scenario is set up as follows:</span></span>

- <span data-ttu-id="e3197-311">Jeden dedykowanego klastra jest używany dla wystąpienia programu SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e3197-311">One dedicated cluster is used for the SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="e3197-312">Jeden dedykowanego klastra jest używany dla wystąpienia systemu DBMS.</span><span class="sxs-lookup"><span data-stu-id="e3197-312">One dedicated cluster is used for the DBMS instance.</span></span>
- <span data-ttu-id="e3197-313">SAP wystąpień serwera aplikacji są wdrażane w ich własnych dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-313">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Rysunek 8: SAP wysokiej dostępności architektury szablonu 1, za pomocą dedykowanego klastra ASCS/SCS i bazami danych][sap-ha-guide-figure-2004]

<span data-ttu-id="e3197-315">_**Rysunek 8.** SAP architektury 1 szablonu wysokiej dostępności, dedykowane klastry ASCS/SCS i bazami danych_</span><span class="sxs-lookup"><span data-stu-id="e3197-315">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="e3197-316">Scenariusz wdrażania przy użyciu architektury 2 szablonu</span><span class="sxs-lookup"><span data-stu-id="e3197-316">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="e3197-317">Na rysunku nr 9 przedstawiono przykład architektury wysokiej dostępności programu SAP NetWeaver Azure **jeden** systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-317">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="e3197-318">Ten scenariusz jest skonfigurowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e3197-318">This scenario is set up as follows:</span></span>

- <span data-ttu-id="e3197-319">Jeden klaster dedykowanych służy do **zarówno** wystąpienia SAP ASCS/SCS i systemu DBMS.</span><span class="sxs-lookup"><span data-stu-id="e3197-319">One dedicated cluster is used for **both** the SAP ASCS/SCS instance and the DBMS.</span></span>
- <span data-ttu-id="e3197-320">SAP wystąpień serwera aplikacji są wdrażane w własnych dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-320">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Rysunek 9: SAP wysokiej dostępności architektury szablonu 2, dedykowanego klastra dla ASCS/SCS i dedykowanego klastra dla systemu DBMS][sap-ha-guide-figure-2005]

<span data-ttu-id="e3197-322">_**Rysunek 9:** SAP wysokiej dostępności architektury szablonu 2, dedykowanego klastra dla ASCS/SCS i dedykowanego klastra dla systemu DBMS_</span><span class="sxs-lookup"><span data-stu-id="e3197-322">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="e3197-323">Scenariusz wdrażania przy użyciu architektury 3 szablonu</span><span class="sxs-lookup"><span data-stu-id="e3197-323">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="e3197-324">Na rysunku nr 10 przedstawiono architekturę SAP NetWeaver wysokiej dostępności platformy Azure dla **dwóch** SAP systemy, z &lt;SID1&gt; i &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="e3197-324">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="e3197-325">Ten scenariusz jest skonfigurowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e3197-325">This scenario is set up as follows:</span></span>

- <span data-ttu-id="e3197-326">Jeden dedykowanego klastra jest używany do **zarówno** z wystąpieniem SAP ASCS/SCS SID1 *i* z wystąpieniem SAP ASCS/SCS SID2 (jednego klastra).</span><span class="sxs-lookup"><span data-stu-id="e3197-326">One dedicated cluster is used for **both** the SAP ASCS/SCS SID1 instance *and* the SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="e3197-327">Jeden dedykowanego klastra jest używany dla systemu DBMS SID1 i innym dedykowanego klastra jest używany dla systemu DBMS SID2 (dwa klastry).</span><span class="sxs-lookup"><span data-stu-id="e3197-327">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="e3197-328">SAP wystąpień serwera aplikacji dla systemu SAP SID1 ma swoje własne dedykowane maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="e3197-328">SAP Application Server instances for the SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="e3197-329">SAP wystąpień serwera aplikacji dla systemu SAP SID2 ma swoje własne dedykowane maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="e3197-329">SAP Application Server instances for the SAP system SID2 have their own dedicated VMs.</span></span>

![Rysunek 10: Wysoka dostępność architektury szablonu 3, z dedykowanym klastrem w różnych wystąpieniach ASCS/SCS SAP][sap-ha-guide-figure-6003]

<span data-ttu-id="e3197-331">_**Rysunek 10:** wysokiej dostępności architektury szablonu 3, z dedykowanym klastrem w różnych wystąpieniach ASCS/SCS SAP_</span><span class="sxs-lookup"><span data-stu-id="e3197-331">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="e3197-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Przygotowanie infrastruktury</span><span class="sxs-lookup"><span data-stu-id="e3197-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare the infrastructure</span></span>

### <a name="prepare-the-infrastructure-for-architectural-template-1"></a><span data-ttu-id="e3197-333">Przygotowanie infrastruktury dla architektury 1 szablonu</span><span class="sxs-lookup"><span data-stu-id="e3197-333">Prepare the infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="e3197-334">Szablony usługi Azure Resource Manager dla programu SAP uprościć wdrażanie wymaganych zasobów.</span><span class="sxs-lookup"><span data-stu-id="e3197-334">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="e3197-335">Trójwarstwowa szablonów usługi Azure Resource Manager obsługuje również scenariuszy wysokiej dostępności, takich jak w architektury 1 szablon, który ma dwa klastry.</span><span class="sxs-lookup"><span data-stu-id="e3197-335">The three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="e3197-336">Każdy klaster jest SAP pojedynczego punktu awarii dla programu SAP ASCS/SCS i bazami danych.</span><span class="sxs-lookup"><span data-stu-id="e3197-336">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="e3197-337">Oto, gdzie można uzyskać szablonów usługi Azure Resource Manager przykładowy scenariusz, który opisano w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="e3197-337">Here's where you can get Azure Resource Manager templates for the example scenario we describe in this article:</span></span>

* [<span data-ttu-id="e3197-338">Obraz Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e3197-338">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="e3197-339">Za pomocą zarządzanych dysków Azure obrazu z witryny Marketplace</span><span class="sxs-lookup"><span data-stu-id="e3197-339">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [<span data-ttu-id="e3197-340">Obraz niestandardowy</span><span class="sxs-lookup"><span data-stu-id="e3197-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [<span data-ttu-id="e3197-341">Niestandardowy obraz za pomocą dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="e3197-341">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

<span data-ttu-id="e3197-342">Aby przygotować infrastrukturę do architektury szablon 1:</span><span class="sxs-lookup"><span data-stu-id="e3197-342">To prepare the infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="e3197-343">W portalu Azure na **parametry** bloku, w **SYSTEMAVAILABILITY** wybierz opcję **HA**.</span><span class="sxs-lookup"><span data-stu-id="e3197-343">In the Azure portal, on the **Parameters** blade, in the **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Rysunek 11: Ustaw parametry usługi Azure Resource Manager wysokiej dostępności SAP][sap-ha-guide-figure-3000]

<span data-ttu-id="e3197-345">_**Rysunek 11:** ustawić parametry usługi Azure Resource Manager wysokiej dostępności SAP_</span><span class="sxs-lookup"><span data-stu-id="e3197-345">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="e3197-346">Tworzenie szablonów:</span><span class="sxs-lookup"><span data-stu-id="e3197-346">The templates create:</span></span>

  * <span data-ttu-id="e3197-347">**Maszyny wirtualne**:</span><span class="sxs-lookup"><span data-stu-id="e3197-347">**Virtual machines**:</span></span>
    * <span data-ttu-id="e3197-348">Maszyny wirtualne serwera aplikacji SAP: <*SAPSystemSID*> - podpisane — <*numer*></span><span class="sxs-lookup"><span data-stu-id="e3197-348">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="e3197-349">Maszyny wirtualne klastra ASCS/SCS: <*SAPSystemSID*> - ascs - <*numer*></span><span class="sxs-lookup"><span data-stu-id="e3197-349">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="e3197-350">Klaster systemu DBMS: <*SAPSystemSID*> - db - <*numer*></span><span class="sxs-lookup"><span data-stu-id="e3197-350">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="e3197-351">**Sieci karty dla wszystkich maszyn wirtualnych adresów IP skojarzonych**:</span><span class="sxs-lookup"><span data-stu-id="e3197-351">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="e3197-352"><*SAPSystemSID*> - nic - podpisane — <*numer*></span><span class="sxs-lookup"><span data-stu-id="e3197-352"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="e3197-353"><*SAPSystemSID*> - nic - ascs - <*numer*></span><span class="sxs-lookup"><span data-stu-id="e3197-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="e3197-354"><*SAPSystemSID*> - nic - db - <*numer*></span><span class="sxs-lookup"><span data-stu-id="e3197-354"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="e3197-355">**Konta magazynu platformy Azure (tylko w przypadku dysków niezarządzany)**</span><span class="sxs-lookup"><span data-stu-id="e3197-355">**Azure storage accounts (unmanaged disks only)**</span></span>

  * <span data-ttu-id="e3197-356">**Grupy dostępności** dla:</span><span class="sxs-lookup"><span data-stu-id="e3197-356">**Availability groups** for:</span></span>
    * <span data-ttu-id="e3197-357">Maszyny wirtualne serwera aplikacji SAP: <*SAPSystemSID*> - avset - podpisane</span><span class="sxs-lookup"><span data-stu-id="e3197-357">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="e3197-358">Maszyny wirtualne klastra SAP ASCS/SCS: <*SAPSystemSID*> - avset - ascs</span><span class="sxs-lookup"><span data-stu-id="e3197-358">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="e3197-359">System DBMS klastrowanie maszyn wirtualnych: <*SAPSystemSID*> - avset - db</span><span class="sxs-lookup"><span data-stu-id="e3197-359">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="e3197-360">**Azure wewnętrznego modułu równoważenia obciążenia**:</span><span class="sxs-lookup"><span data-stu-id="e3197-360">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="e3197-361">Z wszystkimi portami dla wystąpienia ASCS/SCS i adresu IP <*SAPSystemSID*> - lb - ascs</span><span class="sxs-lookup"><span data-stu-id="e3197-361">With all ports for the ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="e3197-362">Z wszystkimi portami dla adresu IP i bazami danych programu SQL Server <*SAPSystemSID*> - lb - db</span><span class="sxs-lookup"><span data-stu-id="e3197-362">With all ports for the SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="e3197-363">**Grupy zabezpieczeń sieci**: <*SAPSystemSID*> - nsg - ascs-0</span><span class="sxs-lookup"><span data-stu-id="e3197-363">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="e3197-364">Z otwartego portu zewnętrznego protokołu RDP (Remote Desktop) do <*SAPSystemSID*> - ascs - 0 maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e3197-364">With an open external Remote Desktop Protocol (RDP) port to the <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="e3197-365">Wszystkie adresy IP Azure wewnętrzne moduły równoważenia obciążenia i karty sieciowe są **dynamiczne** domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e3197-365">All IP addresses of the network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="e3197-366">Zmień je, aby **statycznych** adresów IP.</span><span class="sxs-lookup"><span data-stu-id="e3197-366">Change them to **static** IP addresses.</span></span> <span data-ttu-id="e3197-367">Firma Microsoft opisano, jak to zrobić w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="e3197-367">We describe how to do this later in the article.</span></span>
>
>

### <span data-ttu-id="e3197-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Wdrażanie maszyn wirtualnych z połączeniem sieci firmowej (między lokalizacjami) do użycia w środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="e3197-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) to use in production</span></span>
<span data-ttu-id="e3197-369">Dla systemów SAP produkcyjnych, wdrażanie maszyn wirtualnych platformy Azure z [łączności z siecią firmową (między lokalizacjami)] [ planning-guide-2.2] za pomocą usługi Azure Site to Site VPN lub rozwiązania Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e3197-369">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="e3197-370">Można użyć wystąpienia sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-370">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="e3197-371">Sieć wirtualna i podsieć już zostały utworzone i przygotowane.</span><span class="sxs-lookup"><span data-stu-id="e3197-371">The virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="e3197-372">W portalu Azure na **parametry** bloku, w **NEWOREXISTINGSUBNET** wybierz opcję **istniejących**.</span><span class="sxs-lookup"><span data-stu-id="e3197-372">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="e3197-373">W **SUBNETID** Dodaj pełne ciąg przygotowanego sieci Azure SubnetID, w którym zamierzasz wdrożyć maszyny wirtualne Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-373">In the **SUBNETID** box, add the full string of your prepared Azure network SubnetID where you plan to deploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="e3197-374">Aby uzyskać listę wszystkich podsieci w sieci Azure, uruchom następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e3197-374">To get a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="e3197-375">**Identyfikator** pola pokazuje **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="e3197-375">The **ID** field shows the **SUBNETID**.</span></span>
4. <span data-ttu-id="e3197-376">Aby uzyskać listę wszystkich **SUBNETID** wartości, uruchom to polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e3197-376">To get a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="e3197-377">**SUBNETID** wygląda podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="e3197-377">The **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="e3197-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a>Wdrażanie wystąpień SAP tylko w chmurze dla testu i pokaz</span><span class="sxs-lookup"><span data-stu-id="e3197-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="e3197-379">Można wdrożyć systemu SAP wysokiej dostępności w modelu wdrażania tylko w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e3197-379">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="e3197-380">Tego rodzaju wdrożenia przede wszystkim jest przydatna do demo i test przypadki użycia.</span><span class="sxs-lookup"><span data-stu-id="e3197-380">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="e3197-381">Nie nadaje się do przypadków użycia w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e3197-381">It's not suited for production use cases.</span></span>

- <span data-ttu-id="e3197-382">W portalu Azure na **parametry** bloku, w **NEWOREXISTINGSUBNET** wybierz opcję **nowe**.</span><span class="sxs-lookup"><span data-stu-id="e3197-382">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="e3197-383">Pozostaw **SUBNETID** pole puste.</span><span class="sxs-lookup"><span data-stu-id="e3197-383">Leave the **SUBNETID** field empty.</span></span>

  <span data-ttu-id="e3197-384">Szablon SAP usługi Azure Resource Manager automatycznie tworzy sieci wirtualnej platformy Azure i podsieć.</span><span class="sxs-lookup"><span data-stu-id="e3197-384">The SAP Azure Resource Manager template automatically creates the Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="e3197-385">Należy również wdrożyć co najmniej jednej maszyny wirtualnej dedykowanego dla usługi Active Directory i DNS w tym samym wystąpieniu sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-385">You also need to deploy at least one dedicated virtual machine for Active Directory and DNS in the same Azure Virtual Network instance.</span></span> <span data-ttu-id="e3197-386">Szablon nie tworzy tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-386">The template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-the-infrastructure-for-architectural-template-2"></a><span data-ttu-id="e3197-387">Przygotowanie infrastruktury dla architektury 2 szablonu</span><span class="sxs-lookup"><span data-stu-id="e3197-387">Prepare the infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="e3197-388">Ten szablon Menedżera zasobów Azure dla programu SAP służy do uproszczenia wdrażania zasobów wymaganej infrastruktury dla programu SAP architektury 2 szablonu.</span><span class="sxs-lookup"><span data-stu-id="e3197-388">You can use this Azure Resource Manager template for SAP to help simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="e3197-389">Oto, gdzie można uzyskać szablonów usługi Azure Resource Manager dla tego scenariusza wdrażania:</span><span class="sxs-lookup"><span data-stu-id="e3197-389">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="e3197-390">Obraz Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e3197-390">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="e3197-391">Za pomocą zarządzanych dysków Azure obrazu z witryny Marketplace</span><span class="sxs-lookup"><span data-stu-id="e3197-391">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [<span data-ttu-id="e3197-392">Obraz niestandardowy</span><span class="sxs-lookup"><span data-stu-id="e3197-392">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [<span data-ttu-id="e3197-393">Niestandardowy obraz za pomocą dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="e3197-393">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-the-infrastructure-for-architectural-template-3"></a><span data-ttu-id="e3197-394">Przygotowanie infrastruktury dla architektury 3 szablonu</span><span class="sxs-lookup"><span data-stu-id="e3197-394">Prepare the infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="e3197-395">Można przygotować infrastrukturę i skonfigurować SAP dla **multi-SID**.</span><span class="sxs-lookup"><span data-stu-id="e3197-395">You can prepare the infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="e3197-396">Na przykład można dodać dodatkowe wystąpienia SAP ASCS/SCS do *istniejących* konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-396">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="e3197-397">Aby uzyskać więcej informacji, zobacz [skonfigurować dodatkowe wystąpienia SAP ASCS/SCS do istniejącej konfiguracji klastra do utworzenia konfiguracji wielu SID SAP w usłudze Azure Resource Manager][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="e3197-397">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration to create an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="e3197-398">Jeśli chcesz utworzyć nowy klaster multi-identyfikator SID, można użyć identyfikatora SID multi [szablony szybkiego startu w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="e3197-398">If you want to create a new multi-SID cluster, you can use the multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="e3197-399">Aby utworzyć nowy klaster multi-identyfikator SID, należy wdrożyć trzy następujące szablony:</span><span class="sxs-lookup"><span data-stu-id="e3197-399">To create a new multi-SID cluster, you need to deploy the following three templates:</span></span>

* [<span data-ttu-id="e3197-400">ASCS/SCS szablonu</span><span class="sxs-lookup"><span data-stu-id="e3197-400">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="e3197-401">Szablon bazy danych</span><span class="sxs-lookup"><span data-stu-id="e3197-401">Database template</span></span>](#database-template)
* [<span data-ttu-id="e3197-402">Szablon serwerów aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3197-402">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="e3197-403">Poniższe sekcje mają więcej szczegółów na temat szablonów oraz parametry, które należy podać w szablonach.</span><span class="sxs-lookup"><span data-stu-id="e3197-403">The following sections have more details about the templates and the parameters you need to provide in the templates.</span></span>

#### <span data-ttu-id="e3197-404"><a name="ASCS-SCS-template"></a>ASCS/SCS szablonu</span><span class="sxs-lookup"><span data-stu-id="e3197-404"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="e3197-405">Szablon ASCS/SCS wdraża dwie maszyny wirtualne, których można utworzyć klaster trybu failover systemu Windows Server, który obsługuje wiele wystąpień ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e3197-405">The ASCS/SCS template deploys two virtual machines that you can use to create a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="e3197-406">Aby skonfigurować szablon identyfikatora SID multi ASCS/SCS, w [szablon identyfikatora SID multi ASCS/SCS] [ sap-templates-3-tier-multisid-xscs-marketplace-image] lub [ASCS/SCS identyfikatora SID multi szablonu za pomocą dysków zarządzanych] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], wprowadź wartości dla następujących parametrów:</span><span class="sxs-lookup"><span data-stu-id="e3197-406">To set up the ASCS/SCS multi-SID template, in the [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image] or [ASCS/SCS multi-SID template using Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], enter values for the following parameters:</span></span>

  - <span data-ttu-id="e3197-407">**Prefiks zasobów**.</span><span class="sxs-lookup"><span data-stu-id="e3197-407">**Resource Prefix**.</span></span>  <span data-ttu-id="e3197-408">Ustaw prefiks zasobu, który jest używany do prefiksu wszystkie zasoby, które są tworzone podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="e3197-408">Set the resource prefix, which is used to prefix all resources that are created during the deployment.</span></span> <span data-ttu-id="e3197-409">Ponieważ zasoby nie należą do tylko jednej systemu SAP, prefiks zasobu nie jest częścią identyfikatora SID jednego systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-409">Because the resources do not belong to only one SAP system, the prefix of the resource is not the SID of one SAP system.</span></span>  <span data-ttu-id="e3197-410">Prefiks musi należeć do zakresu od **trzech do sześciu znaków**.</span><span class="sxs-lookup"><span data-stu-id="e3197-410">The prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="e3197-411">**Na stosie typu**.</span><span class="sxs-lookup"><span data-stu-id="e3197-411">**Stack Type**.</span></span> <span data-ttu-id="e3197-412">Wybierz typ stosu systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-412">Select the stack type of the SAP system.</span></span> <span data-ttu-id="e3197-413">W zależności od typu stosu modułu równoważenia obciążenia Azure ma jeden (ABAP lub tylko Java) lub dwóch (ABAP + Java) prywatnych adresów IP na systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-413">Depending on the stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="e3197-414">**Typ systemu operacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="e3197-414">**OS Type**.</span></span> <span data-ttu-id="e3197-415">Wybierz system operacyjny maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-415">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="e3197-416">**Liczba systemu SAP**.</span><span class="sxs-lookup"><span data-stu-id="e3197-416">**SAP System Count**.</span></span> <span data-ttu-id="e3197-417">Wybierz liczbę systemów SAP, który ma zostać zainstalowany w tym klastrze.</span><span class="sxs-lookup"><span data-stu-id="e3197-417">Select the number of SAP systems you want to install in this cluster.</span></span>
  -  <span data-ttu-id="e3197-418">**Dostępność systemu**.</span><span class="sxs-lookup"><span data-stu-id="e3197-418">**System Availability**.</span></span> <span data-ttu-id="e3197-419">Wybierz **HA**.</span><span class="sxs-lookup"><span data-stu-id="e3197-419">Select **HA**.</span></span>
  -  <span data-ttu-id="e3197-420">**Nazwa użytkownika i hasło administratora**.</span><span class="sxs-lookup"><span data-stu-id="e3197-420">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="e3197-421">Utwórz nowego użytkownika, który może służyć do logowania się na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e3197-421">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="e3197-422">**Nowy lub istniejący podsieci**.</span><span class="sxs-lookup"><span data-stu-id="e3197-422">**New Or Existing Subnet**.</span></span> <span data-ttu-id="e3197-423">Określ, czy należy utworzyć nową sieć wirtualną i podsieć lub istniejącą podsieć powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="e3197-423">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="e3197-424">Jeśli masz już sieć wirtualną, która jest połączona z siecią lokalną, wybierz **istniejących**.</span><span class="sxs-lookup"><span data-stu-id="e3197-424">If you already have a virtual network that is connected to your on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="e3197-425">**Identyfikator podsieci**.</span><span class="sxs-lookup"><span data-stu-id="e3197-425">**Subnet Id**.</span></span> <span data-ttu-id="e3197-426">Ustawienia identyfikatorów podsieci, do którego powinny być połączone maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-426">Set the ID of the subnet to which the virtual machines should be connected.</span></span> <span data-ttu-id="e3197-427">Wybierz podsieć sieci wirtualnej sieci prywatnej (VPN) lub usługi sieci wirtualnej sieci lokalnej nawiązać połączenia z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="e3197-427">Select the subnet of your virtual private network (VPN) or ExpressRoute virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="e3197-428">Identyfikator zwykle wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e3197-428">The ID usually looks like this:</span></span>

   <span data-ttu-id="e3197-429">/Subscriptions/ <*identyfikator subskrypcji*> /resourceGroups/ <*Nazwa grupy zasobów*> /providers/Microsoft.Network/virtualNetworks/ <*wirtualnej nazwy sieciowej*> /subnets/ <*nazwy podsieci*></span><span class="sxs-lookup"><span data-stu-id="e3197-429">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="e3197-430">Szablon wdraża jedno wystąpienie usługi równoważenia obciążenia Azure, która obsługuje wiele systemów SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-430">The template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="e3197-431">Wystąpienia ASCS powinny być skonfigurowane dla liczby wystąpień 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="e3197-431">The ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="e3197-432">Wystąpienia SCS powinny być skonfigurowane dla liczby wystąpień 01 11, 21...</span><span class="sxs-lookup"><span data-stu-id="e3197-432">The SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="e3197-433">Wystąpienia ASCS umieścić w kolejce replikacji serwera (Wywołujących) (tylko w systemie Linux) są skonfigurowane dla liczby wystąpień 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="e3197-433">The ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="e3197-434">Wystąpienia Wywołujących SCS (tylko w systemie Linux) są skonfigurowane dla liczby wystąpień 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="e3197-434">The SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="e3197-435">Moduł równoważenia obciążenia zawiera 1 (2 dla systemu Linux) VIP(s), 1 x dla ASCS/SCS i 1 x adres VIP dla Wywołujących (tylko w systemie Linux).</span><span class="sxs-lookup"><span data-stu-id="e3197-435">The load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="e3197-436">Poniższa lista zawiera wszystkie reguły, o których (gdzie x jest numerem systemu SAP, na przykład 1, 2, 3...) równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="e3197-436">The following list contains all load balancing rules (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="e3197-437">Porty właściwe dla systemu Windows dla każdego systemu SAP: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="e3197-437">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="e3197-438">Porty ASCS (liczby wystąpień x0): 32 x 0, 36 x 0, 39 x 0, 81 x 0, 5 x 013, 5 x 014, 5 x 016</span><span class="sxs-lookup"><span data-stu-id="e3197-438">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="e3197-439">Porty SCS (liczby wystąpień x1): 32 x 1, 33 x 1, 39 x 1, 81 x 1, 5 x 113, 5 x 114, 5 x 116</span><span class="sxs-lookup"><span data-stu-id="e3197-439">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="e3197-440">Wywołujących ASCS porty w systemie Linux (liczby wystąpień x2): 33 x 2, 5 x 213, 5 x 214, 5 x 216</span><span class="sxs-lookup"><span data-stu-id="e3197-440">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="e3197-441">Wywołujących SCS porty w systemie Linux (liczby wystąpień x3): 33 x 3, 5 x 313, 5 x 314, 5 x 316</span><span class="sxs-lookup"><span data-stu-id="e3197-441">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="e3197-442">Moduł równoważenia obciążenia jest skonfigurowana do używania następujące porty sondowania (gdzie x jest numerem systemu SAP, na przykład 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="e3197-442">The load balancer is configured to use the following probe ports (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="e3197-443">Port sondy modułu równoważenia obciążenia wewnętrznego ASCS/SCS: 620 x 0</span><span class="sxs-lookup"><span data-stu-id="e3197-443">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="e3197-444">Wewnętrzny Wywołujących załadować port sondy modułu równoważenia (tylko w systemie Linux): 621 x 2</span><span class="sxs-lookup"><span data-stu-id="e3197-444">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="e3197-445"><a name="database-template"></a>Szablon bazy danych</span><span class="sxs-lookup"><span data-stu-id="e3197-445"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="e3197-446">Szablon bazy danych wdraża co najmniej dwóch maszyn wirtualnych, które służy do instalowania systemu zarządzania relacyjnej bazy danych (RDBMS) dla jednego systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-446">The database template deploys one or two virtual machines that you can use to install the relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="e3197-447">Na przykład jeśli wdrożono szablon ASCS/SCS pięć systemów SAP, należy wdrożyć tego szablonu pięć razy.</span><span class="sxs-lookup"><span data-stu-id="e3197-447">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="e3197-448">Aby skonfigurować szablon identyfikatora SID multi bazy danych, w [bazy danych wielu SID szablonu] [ sap-templates-3-tier-multisid-db-marketplace-image] lub [szablon identyfikatora SID multi bazy danych przy użyciu dysków zarządzanych] [ sap-templates-3-tier-multisid-db-marketplace-image-md], wprowadź wartości dla następujących parametrów:</span><span class="sxs-lookup"><span data-stu-id="e3197-448">To set up the database multi-SID template, in the [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image] or [database multi-SID template using Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="e3197-449">**Identyfikator systemu SAP**.</span><span class="sxs-lookup"><span data-stu-id="e3197-449">**Sap System Id**.</span></span> <span data-ttu-id="e3197-450">Wprowadź identyfikator systemu SAP systemu SAP, które chcesz zainstalować.</span><span class="sxs-lookup"><span data-stu-id="e3197-450">Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="e3197-451">Identyfikator będzie służyć jako prefiks dla zasobów, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="e3197-451">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="e3197-452">**Typ systemu operacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="e3197-452">**Os Type**.</span></span> <span data-ttu-id="e3197-453">Wybierz system operacyjny maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-453">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="e3197-454">**Wartość DbType**.</span><span class="sxs-lookup"><span data-stu-id="e3197-454">**Dbtype**.</span></span> <span data-ttu-id="e3197-455">Wybierz typ bazy danych, którą chcesz zainstalować w klastrze.</span><span class="sxs-lookup"><span data-stu-id="e3197-455">Select the type of the database you want to install on the cluster.</span></span> <span data-ttu-id="e3197-456">Wybierz **SQL** Jeśli chcesz zainstalować program Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e3197-456">Select **SQL** if you want to install Microsoft SQL Server.</span></span> <span data-ttu-id="e3197-457">Wybierz **HANA** Jeśli zamierzasz zainstalować SAP HANA na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-457">Select **HANA** if you plan to install SAP HANA on the virtual machines.</span></span> <span data-ttu-id="e3197-458">Upewnij się, że wybrano prawidłowy typ systemu operacyjnego: Wybierz **Windows** SQL i wybierz opcję dystrybucji systemu Linux HANA.</span><span class="sxs-lookup"><span data-stu-id="e3197-458">Make sure to select the correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="e3197-459">Równoważenia obciążenia Azure, który jest podłączony do maszyny wirtualnej zostanie skonfigurowany do obsługi typu wybranej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="e3197-459">The Azure Load Balancer that is connected to the virtual machines will be configured to support the selected database type:</span></span>
    * <span data-ttu-id="e3197-460">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="e3197-460">**SQL**.</span></span> <span data-ttu-id="e3197-461">Moduł równoważenia obciążenia będzie Równoważenie obciążenia portu 1433.</span><span class="sxs-lookup"><span data-stu-id="e3197-461">The load balancer will load-balance port 1433.</span></span> <span data-ttu-id="e3197-462">Upewnij się użyć tego portu dla ustawień programu SQL Server AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="e3197-462">Make sure to use this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="e3197-463">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="e3197-463">**HANA**.</span></span> <span data-ttu-id="e3197-464">Moduł równoważenia obciążenia będzie Równoważenie obciążenia portów 35015 i 35017.</span><span class="sxs-lookup"><span data-stu-id="e3197-464">The load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="e3197-465">Upewnij się zainstalować SAP HANA z liczby wystąpień **50**.</span><span class="sxs-lookup"><span data-stu-id="e3197-465">Make sure to install SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="e3197-466">Moduł równoważenia obciążenia będzie używać portu sondowania 62550.</span><span class="sxs-lookup"><span data-stu-id="e3197-466">The load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="e3197-467">**Rozmiar systemu SAP**.</span><span class="sxs-lookup"><span data-stu-id="e3197-467">**Sap System Size**.</span></span> <span data-ttu-id="e3197-468">Ustaw liczbę protokoły SAP zapewnia nowy system.</span><span class="sxs-lookup"><span data-stu-id="e3197-468">Set the number of SAPS the new system will provide.</span></span> <span data-ttu-id="e3197-469">Jeśli nie wiadomo jak wiele protokoły SAP wymaga systemu, zapytaj SAP technologii partnera lub Integrator systemu.</span><span class="sxs-lookup"><span data-stu-id="e3197-469">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="e3197-470">**Dostępność systemu**.</span><span class="sxs-lookup"><span data-stu-id="e3197-470">**System Availability**.</span></span> <span data-ttu-id="e3197-471">Wybierz **HA**.</span><span class="sxs-lookup"><span data-stu-id="e3197-471">Select **HA**.</span></span>
  -  <span data-ttu-id="e3197-472">**Nazwa użytkownika i hasło administratora**.</span><span class="sxs-lookup"><span data-stu-id="e3197-472">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="e3197-473">Utwórz nowego użytkownika, który może służyć do logowania się na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e3197-473">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="e3197-474">**Identyfikator podsieci**.</span><span class="sxs-lookup"><span data-stu-id="e3197-474">**Subnet Id**.</span></span> <span data-ttu-id="e3197-475">Wprowadź identyfikator podsieci, który został użyty podczas wdrażania szablonu ASCS/SCS lub identyfikator podsieci, który został utworzony jako część wdrożenia szablonu ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e3197-475">Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="e3197-476"><a name="application-servers-template"></a>Szablon serwerów aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3197-476"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="e3197-477">Szablon aplikacji serwerów wdraża dwóch lub więcej maszyn wirtualnych, które mogą służyć jako wystąpień serwera aplikacji SAP jednego systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-477">The application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="e3197-478">Na przykład jeśli wdrożono szablon ASCS/SCS pięć systemów SAP, należy wdrożyć tego szablonu pięć razy.</span><span class="sxs-lookup"><span data-stu-id="e3197-478">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="e3197-479">Aby skonfigurować szablon identyfikatora SID wielu serwerów aplikacji, w [szablon identyfikatora SID wielu serwerów aplikacji] [ sap-templates-3-tier-multisid-apps-marketplace-image] lub [szablon identyfikatora SID wielu serwerów aplikacji za pomocą zarządzania dyskami] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], wprowadź wartości dla następujących parametrów:</span><span class="sxs-lookup"><span data-stu-id="e3197-479">To set up the application servers multi-SID template, in the [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image] or [application servers multi-SID template using Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="e3197-480">**Identyfikator systemu SAP**.</span><span class="sxs-lookup"><span data-stu-id="e3197-480">**Sap System Id**.</span></span> <span data-ttu-id="e3197-481">Wprowadź identyfikator systemu SAP systemu SAP, które chcesz zainstalować.</span><span class="sxs-lookup"><span data-stu-id="e3197-481">Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="e3197-482">Identyfikator będzie służyć jako prefiks dla zasobów, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="e3197-482">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="e3197-483">**Typ systemu operacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="e3197-483">**Os Type**.</span></span> <span data-ttu-id="e3197-484">Wybierz system operacyjny maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-484">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="e3197-485">**Rozmiar systemu SAP**.</span><span class="sxs-lookup"><span data-stu-id="e3197-485">**Sap System Size**.</span></span> <span data-ttu-id="e3197-486">Liczba protokoły SAP zapewnia nowy system.</span><span class="sxs-lookup"><span data-stu-id="e3197-486">The number of SAPS the new system will provide.</span></span> <span data-ttu-id="e3197-487">Jeśli nie wiadomo jak wiele protokoły SAP wymaga systemu, zapytaj SAP technologii partnera lub Integrator systemu.</span><span class="sxs-lookup"><span data-stu-id="e3197-487">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="e3197-488">**Dostępność systemu**.</span><span class="sxs-lookup"><span data-stu-id="e3197-488">**System Availability**.</span></span> <span data-ttu-id="e3197-489">Wybierz **HA**.</span><span class="sxs-lookup"><span data-stu-id="e3197-489">Select **HA**.</span></span>
  -  <span data-ttu-id="e3197-490">**Nazwa użytkownika i hasło administratora**.</span><span class="sxs-lookup"><span data-stu-id="e3197-490">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="e3197-491">Utwórz nowego użytkownika, który może służyć do logowania się na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e3197-491">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="e3197-492">**Identyfikator podsieci**.</span><span class="sxs-lookup"><span data-stu-id="e3197-492">**Subnet Id**.</span></span> <span data-ttu-id="e3197-493">Wprowadź identyfikator podsieci, który został użyty podczas wdrażania szablonu ASCS/SCS lub identyfikator podsieci, który został utworzony jako część wdrożenia szablonu ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e3197-493">Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="e3197-494"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a>Sieć wirtualna platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e3197-494"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="e3197-495">W naszym przykładzie przestrzeni adresowej sieci wirtualnej platformy Azure jest 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="e3197-495">In our example, the address space of the Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="e3197-496">Brak jednej podsieci o nazwie **podsieci**, z zakresu adresów 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="e3197-496">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="e3197-497">Wszystkie maszyny wirtualne i wewnętrzne moduły równoważenia obciążenia są wdrażane w tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3197-497">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3197-498">Nie wprowadzono żadnych zmian w ustawieniach sieci w systemie operacyjnym gościa.</span><span class="sxs-lookup"><span data-stu-id="e3197-498">Don't make any changes to the network settings inside the guest operating system.</span></span> <span data-ttu-id="e3197-499">W tym adresy IP, serwery DNS i podsieci.</span><span class="sxs-lookup"><span data-stu-id="e3197-499">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="e3197-500">Skonfiguruj ustawienia sieci na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-500">Configure all your network settings in Azure.</span></span> <span data-ttu-id="e3197-501">Usługa protokołu dynamicznej konfiguracji hosta (DHCP) propaguje ustawienia.</span><span class="sxs-lookup"><span data-stu-id="e3197-501">The Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="e3197-502"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>Adresy IP serwera DNS</span><span class="sxs-lookup"><span data-stu-id="e3197-502"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="e3197-503">Aby ustawić wymagany adres IP DNS adresów, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="e3197-503">To set the required DNS IP addresses, do the following steps.</span></span>

1.  <span data-ttu-id="e3197-504">W portalu Azure na **serwerów DNS** bloku, upewnij się, że sieci wirtualnej **serwerów DNS** ustawiono opcję **niestandardowe DNS**.</span><span class="sxs-lookup"><span data-stu-id="e3197-504">In the Azure portal, on the **DNS servers** blade, make sure that your virtual network **DNS servers** option is set to **Custom DNS**.</span></span>
2.  <span data-ttu-id="e3197-505">Wybierz ustawienia, na podstawie typu sieci, z którą masz.</span><span class="sxs-lookup"><span data-stu-id="e3197-505">Select your settings based on the type of network you have.</span></span> <span data-ttu-id="e3197-506">Więcej informacji zawierają następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="e3197-506">For more information, see the following resources:</span></span>
    * <span data-ttu-id="e3197-507">[Łączność sieci firmowej (między lokalizacjami)][planning-guide-2.2]: Dodaj adresy IP lokalnych serwerów DNS.</span><span class="sxs-lookup"><span data-stu-id="e3197-507">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add the IP addresses of the on-premises DNS servers.</span></span>  
    <span data-ttu-id="e3197-508">Można rozszerzyć lokalnych serwerów DNS do maszyn wirtualnych, które są uruchomione na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-508">You can extend on-premises DNS servers to the virtual machines that are running in Azure.</span></span> <span data-ttu-id="e3197-509">W tym scenariuszu można dodać adresy IP maszyn wirtualnych platformy Azure, na których uruchomiono usługi DNS.</span><span class="sxs-lookup"><span data-stu-id="e3197-509">In that scenario, you can add the IP addresses of the Azure virtual machines on which you run the DNS service.</span></span>
    * <span data-ttu-id="e3197-510">[Tylko w chmurze wdrożenia][planning-guide-2.1]: wdrożyć dodatkowe maszyny wirtualnej, w tym samym wystąpieniu sieci wirtualnej, która służy jako serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="e3197-510">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in the same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="e3197-511">Dodaj adresy IP maszyn wirtualnych platformy Azure, które zostały skonfigurowane do uruchamiania usługi DNS.</span><span class="sxs-lookup"><span data-stu-id="e3197-511">Add the IP addresses of the Azure virtual machines that you've set up to run DNS service.</span></span>

    ![Rysunek 12: Należy skonfigurować serwery DNS dla sieci wirtualnej platformy Azure][sap-ha-guide-figure-3001]

    <span data-ttu-id="e3197-513">_**Rysunek 12:** DNS Konfigurowanie serwerów na potrzeby sieci wirtualnej platformy Azure_</span><span class="sxs-lookup"><span data-stu-id="e3197-513">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="e3197-514">W przypadku zmiany adresów IP serwerów DNS, musisz ponownie uruchomić maszyn wirtualnych platformy Azure, aby zastosować zmiany oraz propagację nowych serwerów DNS.</span><span class="sxs-lookup"><span data-stu-id="e3197-514">If you change the IP addresses of the DNS servers, you need to restart the Azure virtual machines to apply the change and propagate the new DNS servers.</span></span>
  >
  >

<span data-ttu-id="e3197-515">W tym przykładzie usługa DNS jest zainstalowany i skonfigurowany na tych maszyn wirtualnych systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="e3197-515">In our example, the DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="e3197-516">Roli maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e3197-516">Virtual machine role</span></span> | <span data-ttu-id="e3197-517">Nazwa hosta maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e3197-517">Virtual machine host name</span></span> | <span data-ttu-id="e3197-518">Nazwa karty sieciowej</span><span class="sxs-lookup"><span data-stu-id="e3197-518">Network card name</span></span> | <span data-ttu-id="e3197-519">Statyczny adres IP</span><span class="sxs-lookup"><span data-stu-id="e3197-519">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e3197-520">Pierwszy serwer DNS</span><span class="sxs-lookup"><span data-stu-id="e3197-520">First DNS server</span></span> |<span data-ttu-id="e3197-521">domcontr 0</span><span class="sxs-lookup"><span data-stu-id="e3197-521">domcontr-0</span></span> |<span data-ttu-id="e3197-522">PR1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="e3197-522">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="e3197-523">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="e3197-523">10.0.0.10</span></span> |
| <span data-ttu-id="e3197-524">Drugi serwer DNS</span><span class="sxs-lookup"><span data-stu-id="e3197-524">Second DNS server</span></span> |<span data-ttu-id="e3197-525">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="e3197-525">domcontr-1</span></span> |<span data-ttu-id="e3197-526">PR1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="e3197-526">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="e3197-527">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="e3197-527">10.0.0.11</span></span> |

### <span data-ttu-id="e3197-528"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Nazwy hosta i statyczne adresy IP dla SAP ASCS/SCS wystąpienia klastra i klastrowanego wystąpienia systemu DBMS</span><span class="sxs-lookup"><span data-stu-id="e3197-528"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for the SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="e3197-529">Dla wdrożenia lokalnego należy te hosta zarezerwowanych nazw i adresów IP:</span><span class="sxs-lookup"><span data-stu-id="e3197-529">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="e3197-530">Rola nazwy hostów wirtualnych</span><span class="sxs-lookup"><span data-stu-id="e3197-530">Virtual host name role</span></span> | <span data-ttu-id="e3197-531">Nazwy hostów wirtualnych</span><span class="sxs-lookup"><span data-stu-id="e3197-531">Virtual host name</span></span> | <span data-ttu-id="e3197-532">Wirtualne statycznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="e3197-532">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3197-533">Nazwa SAP ASCS/SCS do hostów wirtualnych pierwszej klastra (dla klastra zarządzania)</span><span class="sxs-lookup"><span data-stu-id="e3197-533">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="e3197-534">PR1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="e3197-534">pr1-ascs-vir</span></span> |<span data-ttu-id="e3197-535">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="e3197-535">10.0.0.42</span></span> |
| <span data-ttu-id="e3197-536">Nazwa hosta wirtualnego wystąpienia programu SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-536">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="e3197-537">PR1 ascs sap</span><span class="sxs-lookup"><span data-stu-id="e3197-537">pr1-ascs-sap</span></span> |<span data-ttu-id="e3197-538">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="e3197-538">10.0.0.43</span></span> |
| <span data-ttu-id="e3197-539">Nazwa systemu DBMS SAP do hostów wirtualnych drugi klastra (klastra zarządzania)</span><span class="sxs-lookup"><span data-stu-id="e3197-539">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="e3197-540">PR1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="e3197-540">pr1-dbms-vir</span></span> |<span data-ttu-id="e3197-541">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="e3197-541">10.0.0.32</span></span> |

<span data-ttu-id="e3197-542">Podczas tworzenia klastra, można utworzyć nazwy hostów wirtualnych **pr1-ascs-vir** i **pr1-dbms-vir** i skojarzony adresy IP, które zarządzania klastrem.</span><span class="sxs-lookup"><span data-stu-id="e3197-542">When you create the cluster, create the virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and the associated IP addresses that manage the cluster itself.</span></span> <span data-ttu-id="e3197-543">Aby dowiedzieć się, jak to zrobić, zobacz [zbieranie węzłów klastra w konfiguracji klastra][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="e3197-543">For information about how to do this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="e3197-544">Inne dwie nazwy hostów wirtualnych, można ręcznie utworzyć **pr1 ascs sap** i **pr1 dbms sap**i skojarzony adresy IP na serwerze DNS.</span><span class="sxs-lookup"><span data-stu-id="e3197-544">You can manually create the other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and the associated IP addresses, on the DNS server.</span></span> <span data-ttu-id="e3197-545">Wystąpienia SAP ASCS/SCS klastra i klastrowanego wystąpienia systemu DBMS używać tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="e3197-545">The clustered SAP ASCS/SCS instance and the clustered DBMS instance use these resources.</span></span> <span data-ttu-id="e3197-546">Aby dowiedzieć się, jak to zrobić, zobacz [Utwórz nazwę hosta wirtualnego dla klastrowanego wystąpienia programu SAP ASCS/SCS][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="e3197-546">For information about how to do this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="e3197-547"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Ustaw statycznych adresów IP dla maszyn wirtualnych SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-547"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for the SAP virtual machines</span></span>
<span data-ttu-id="e3197-548">Po wdrożeniu maszyny wirtualnej do użycia w klastrze, należy określić statycznych adresów IP dla wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-548">After you deploy the virtual machines to use in your cluster, you need to set static IP addresses for all virtual machines.</span></span> <span data-ttu-id="e3197-549">W tym w konfiguracji sieci wirtualnej platformy Azure, a nie w systemie operacyjnym gościa.</span><span class="sxs-lookup"><span data-stu-id="e3197-549">Do this in the Azure Virtual Network configuration, and not in the guest operating system.</span></span>

1.  <span data-ttu-id="e3197-550">W portalu Azure wybierz **grupy zasobów** > **karta sieciowa** > **ustawienia** > **adres IP**.</span><span class="sxs-lookup"><span data-stu-id="e3197-550">In the Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="e3197-551">Na **adresów IP** bloku, w obszarze **przypisania**, wybierz pozycję **statycznych**.</span><span class="sxs-lookup"><span data-stu-id="e3197-551">On the **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="e3197-552">W **adres IP** wprowadź adres IP, który ma być używany.</span><span class="sxs-lookup"><span data-stu-id="e3197-552">In the **IP address** box, enter the IP address that you want to use.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e3197-553">W przypadku zmiany adresu IP karty sieciowej, musisz ponownie uruchomić maszyn wirtualnych platformy Azure, aby zastosować zmiany.</span><span class="sxs-lookup"><span data-stu-id="e3197-553">If you change the IP address of the network card, you need to restart the Azure virtual machines to apply the change.</span></span>  
  >
  >

  ![Rysunek 13: Zestaw statycznych adresów IP dla każdej maszyny wirtualnej karty sieciowej][sap-ha-guide-figure-3002]

  <span data-ttu-id="e3197-555">_**Rysunek 13:** ustawić statyczny adres IP dla każdej maszyny wirtualnej karty sieciowej_</span><span class="sxs-lookup"><span data-stu-id="e3197-555">_**Figure 13:** Set static IP addresses for the network card of each virtual machine_</span></span>

  <span data-ttu-id="e3197-556">Powtórz ten krok dla wszystkich interfejsów sieciowych, dla wszystkich maszyn wirtualnych, włącznie ze maszyn wirtualnych, które ma być używany dla usługi Active Directory/serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="e3197-556">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want to use for your Active Directory/DNS service.</span></span>

<span data-ttu-id="e3197-557">W naszym przykładzie mamy tych maszyn wirtualnych i statycznymi adresami IP:</span><span class="sxs-lookup"><span data-stu-id="e3197-557">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="e3197-558">Roli maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e3197-558">Virtual machine role</span></span> | <span data-ttu-id="e3197-559">Nazwa hosta maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e3197-559">Virtual machine host name</span></span> | <span data-ttu-id="e3197-560">Nazwa karty sieciowej</span><span class="sxs-lookup"><span data-stu-id="e3197-560">Network card name</span></span> | <span data-ttu-id="e3197-561">Statyczny adres IP</span><span class="sxs-lookup"><span data-stu-id="e3197-561">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e3197-562">Pierwsze wystąpienie serwera aplikacji SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-562">First SAP Application Server instance</span></span> |<span data-ttu-id="e3197-563">PR1 podpisane 0</span><span class="sxs-lookup"><span data-stu-id="e3197-563">pr1-di-0</span></span> |<span data-ttu-id="e3197-564">PR1-nic podpisane-0</span><span class="sxs-lookup"><span data-stu-id="e3197-564">pr1-nic-di-0</span></span> |<span data-ttu-id="e3197-565">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="e3197-565">10.0.0.50</span></span> |
| <span data-ttu-id="e3197-566">Drugie wystąpienie serwera aplikacji SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-566">Second SAP Application Server instance</span></span> |<span data-ttu-id="e3197-567">PR1 podpisane 1</span><span class="sxs-lookup"><span data-stu-id="e3197-567">pr1-di-1</span></span> |<span data-ttu-id="e3197-568">PR1-nic podpisane-1</span><span class="sxs-lookup"><span data-stu-id="e3197-568">pr1-nic-di-1</span></span> |<span data-ttu-id="e3197-569">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="e3197-569">10.0.0.51</span></span> |
| <span data-ttu-id="e3197-570">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="e3197-570">...</span></span> |<span data-ttu-id="e3197-571">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="e3197-571">...</span></span> |<span data-ttu-id="e3197-572">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="e3197-572">...</span></span> |<span data-ttu-id="e3197-573">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="e3197-573">...</span></span> |
| <span data-ttu-id="e3197-574">Ostatnie wystąpienie serwera aplikacji SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-574">Last SAP Application Server instance</span></span> |<span data-ttu-id="e3197-575">PR1-podpisane-5</span><span class="sxs-lookup"><span data-stu-id="e3197-575">pr1-di-5</span></span> |<span data-ttu-id="e3197-576">PR1-nic podpisane-5</span><span class="sxs-lookup"><span data-stu-id="e3197-576">pr1-nic-di-5</span></span> |<span data-ttu-id="e3197-577">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="e3197-577">10.0.0.55</span></span> |
| <span data-ttu-id="e3197-578">Pierwszym węźle klastra dla wystąpienia ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-578">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="e3197-579">PR1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="e3197-579">pr1-ascs-0</span></span> |<span data-ttu-id="e3197-580">PR1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="e3197-580">pr1-nic-ascs-0</span></span> |<span data-ttu-id="e3197-581">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="e3197-581">10.0.0.40</span></span> |
| <span data-ttu-id="e3197-582">Drugi węzeł klastra dla wystąpienia ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-582">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="e3197-583">PR1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="e3197-583">pr1-ascs-1</span></span> |<span data-ttu-id="e3197-584">PR1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="e3197-584">pr1-nic-ascs-1</span></span> |<span data-ttu-id="e3197-585">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="e3197-585">10.0.0.41</span></span> |
| <span data-ttu-id="e3197-586">Pierwszym węźle klastra dla systemu DBMS wystąpienia</span><span class="sxs-lookup"><span data-stu-id="e3197-586">First cluster node for DBMS instance</span></span> |<span data-ttu-id="e3197-587">PR1-db-0</span><span class="sxs-lookup"><span data-stu-id="e3197-587">pr1-db-0</span></span> |<span data-ttu-id="e3197-588">PR1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="e3197-588">pr1-nic-db-0</span></span> |<span data-ttu-id="e3197-589">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="e3197-589">10.0.0.30</span></span> |
| <span data-ttu-id="e3197-590">Drugi węzeł klastra dla systemu DBMS wystąpienia</span><span class="sxs-lookup"><span data-stu-id="e3197-590">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="e3197-591">PR1-db-1</span><span class="sxs-lookup"><span data-stu-id="e3197-591">pr1-db-1</span></span> |<span data-ttu-id="e3197-592">PR1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="e3197-592">pr1-nic-db-1</span></span> |<span data-ttu-id="e3197-593">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="e3197-593">10.0.0.31</span></span> |

### <span data-ttu-id="e3197-594"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Ustawianie statycznego adresu IP dla platformy Azure wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e3197-594"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for the Azure internal load balancer</span></span>

<span data-ttu-id="e3197-595">Szablon SAP usługi Azure Resource Manager tworzy Azure wewnętrznego modułu równoważenia obciążenia używanego SAP ASCS/SCS wystąpienia klastra i klastrów systemu DBMS.</span><span class="sxs-lookup"><span data-stu-id="e3197-595">The SAP Azure Resource Manager template creates an Azure internal load balancer that is used for the SAP ASCS/SCS instance cluster and the DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3197-596">Adres IP, nazwy hostów wirtualnych SAP ASCS/SCS jest taki sam jak adres IP usługi równoważenia obciążenia wewnętrznego SAP ASCS/SCS: **pr1-lb-ascs**.</span><span class="sxs-lookup"><span data-stu-id="e3197-596">The IP address of the virtual host name of the SAP ASCS/SCS is the same as the IP address of the SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="e3197-597">Adres IP, nazwy wirtualnego systemu DBMS jest taki sam jak adres IP usługi równoważenia obciążenia wewnętrznego systemu DBMS: **pr1-lb-dbms**.</span><span class="sxs-lookup"><span data-stu-id="e3197-597">The IP address of the virtual name of the DBMS is the same as the IP address of the DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="e3197-598">Aby ustawić statyczny adres IP usługi równoważenia obciążenia wewnętrznego Azure:</span><span class="sxs-lookup"><span data-stu-id="e3197-598">To set a static IP address for the Azure internal load balancer:</span></span>

1.  <span data-ttu-id="e3197-599">Początkowe wdrożenie ustawia adres IP usługi równoważenia obciążenia wewnętrznego **dynamiczne**.</span><span class="sxs-lookup"><span data-stu-id="e3197-599">The initial deployment sets the internal load balancer IP address to **Dynamic**.</span></span> <span data-ttu-id="e3197-600">W portalu Azure na **adresów IP** bloku, w obszarze **przypisania**, wybierz pozycję **statycznych**.</span><span class="sxs-lookup"><span data-stu-id="e3197-600">In the Azure portal, on the **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="e3197-601">Ustawienie adresu IP usługi równoważenia obciążenia wewnętrznego **pr1-lb-ascs** adres IP nazwę hosta wirtualnego wystąpienia programu SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e3197-601">Set the IP address of the internal load balancer **pr1-lb-ascs** to the IP address of the virtual host name of the SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="e3197-602">Ustawienie adresu IP usługi równoważenia obciążenia wewnętrznego **pr1-lb-dbms** adres IP nazwę hosta wirtualnego wystąpienia systemu DBMS.</span><span class="sxs-lookup"><span data-stu-id="e3197-602">Set the IP address of the internal load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

  ![Rysunek 14: Ustaw statycznych adresów IP dla wewnętrznego modułu równoważenia obciążenia dla tego wystąpienia programu SAP ASCS/SCS][sap-ha-guide-figure-3003]

  <span data-ttu-id="e3197-604">_**Rysunek 14:** ustawić statycznych adresów IP dla wewnętrznego modułu równoważenia obciążenia dla tego wystąpienia programu SAP ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="e3197-604">_**Figure 14:** Set static IP addresses for the internal load balancer for the SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="e3197-605">W naszym przykładzie mamy dwa Azure wewnętrzne moduły równoważenia obciążenia mających te statycznych adresów IP:</span><span class="sxs-lookup"><span data-stu-id="e3197-605">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="e3197-606">Rola usługi równoważenia obciążenia wewnętrznego Azure</span><span class="sxs-lookup"><span data-stu-id="e3197-606">Azure internal load balancer role</span></span> | <span data-ttu-id="e3197-607">Nazwa modułu równoważenia obciążenia wewnętrznego platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e3197-607">Azure internal load balancer name</span></span> | <span data-ttu-id="e3197-608">Statyczny adres IP</span><span class="sxs-lookup"><span data-stu-id="e3197-608">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3197-609">SAP ASCS/SCS wystąpienia wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e3197-609">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="e3197-610">PR1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="e3197-610">pr1-lb-ascs</span></span> |<span data-ttu-id="e3197-611">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="e3197-611">10.0.0.43</span></span> |
| <span data-ttu-id="e3197-612">System DBMS SAP wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e3197-612">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="e3197-613">PR1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="e3197-613">pr1-lb-dbms</span></span> |<span data-ttu-id="e3197-614">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="e3197-614">10.0.0.33</span></span> |


### <span data-ttu-id="e3197-615"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Domyślne reguły dla usługi równoważenia obciążenia Azure wewnętrzny równoważenia obciążenia ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-615"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="e3197-616">Szablon SAP usługi Azure Resource Manager tworzy portów, które są potrzebne:</span><span class="sxs-lookup"><span data-stu-id="e3197-616">The SAP Azure Resource Manager template creates the ports you need:</span></span>
* <span data-ttu-id="e3197-617">Wystąpienie ABAP ASCS z domyślnej liczby wystąpień **00**</span><span class="sxs-lookup"><span data-stu-id="e3197-617">An ABAP ASCS instance, with the default instance number **00**</span></span>
* <span data-ttu-id="e3197-618">Wystąpienie Java SCS, numer wystąpienia domyślnego **01**</span><span class="sxs-lookup"><span data-stu-id="e3197-618">A Java SCS instance, with the default instance number **01**</span></span>

<span data-ttu-id="e3197-619">Po zainstalowaniu wystąpieniem SAP ASCS/SCS, należy użyć domyślnej liczby wystąpień **00** dla wystąpienia programu ABAP ASCS i numer wystąpienia domyślnego **01** dla swojego wystąpienia Java SCS.</span><span class="sxs-lookup"><span data-stu-id="e3197-619">When you install your SAP ASCS/SCS instance, you must use the default instance number **00** for your ABAP ASCS instance and the default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="e3197-620">Następnie należy utworzyć wymagane równoważenia punktów końcowych dla portów SAP NetWeaver obciążenia wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="e3197-620">Next, create required internal load balancing endpoints for the SAP NetWeaver ports.</span></span>

<span data-ttu-id="e3197-621">Aby utworzyć wymagane obciążenia wewnętrznego równoważenia punktów końcowych, najpierw należy utworzyć te równoważenia punktów końcowych dla portów SAP NetWeaver ABAP ASCS obciążenia:</span><span class="sxs-lookup"><span data-stu-id="e3197-621">To create required internal load balancing endpoints, first, create these load balancing endpoints for the SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="e3197-622">Nazwa reguły równoważenia obciążenia/usługi</span><span class="sxs-lookup"><span data-stu-id="e3197-622">Service/load balancing rule name</span></span> | <span data-ttu-id="e3197-623">Domyślne numery portów</span><span class="sxs-lookup"><span data-stu-id="e3197-623">Default port numbers</span></span> | <span data-ttu-id="e3197-624">Konkretnych portów (ASCS wystąpienia z liczby wystąpień 00) (Wywołujących z 10)</span><span class="sxs-lookup"><span data-stu-id="e3197-624">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3197-625">Umieścić serwer / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="e3197-625">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="e3197-626">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e3197-626">32<*InstanceNumber*></span></span> |<span data-ttu-id="e3197-627">3200</span><span class="sxs-lookup"><span data-stu-id="e3197-627">3200</span></span> |
| <span data-ttu-id="e3197-628">Serwer komunikatów ABAP / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="e3197-628">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="e3197-629">36 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e3197-629">36<*InstanceNumber*></span></span> |<span data-ttu-id="e3197-630">3600</span><span class="sxs-lookup"><span data-stu-id="e3197-630">3600</span></span> |
| <span data-ttu-id="e3197-631">Komunikat wewnętrzny ABAP / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="e3197-631">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="e3197-632">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e3197-632">39<*InstanceNumber*></span></span> |<span data-ttu-id="e3197-633">3900</span><span class="sxs-lookup"><span data-stu-id="e3197-633">3900</span></span> |
| <span data-ttu-id="e3197-634">Serwer HTTP / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="e3197-634">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="e3197-635">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e3197-635">81<*InstanceNumber*></span></span> |<span data-ttu-id="e3197-636">8100</span><span class="sxs-lookup"><span data-stu-id="e3197-636">8100</span></span> |
| <span data-ttu-id="e3197-637">SAP uruchamiania usługi ASCS HTTP / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="e3197-637">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="e3197-638">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="e3197-638">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="e3197-639">50013</span><span class="sxs-lookup"><span data-stu-id="e3197-639">50013</span></span> |
| <span data-ttu-id="e3197-640">SAP uruchamiania usługi ASCS HTTPS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="e3197-640">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="e3197-641">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="e3197-641">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="e3197-642">50014</span><span class="sxs-lookup"><span data-stu-id="e3197-642">50014</span></span> |
| <span data-ttu-id="e3197-643">Umieścić w kolejce replikacji / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="e3197-643">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="e3197-644">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="e3197-644">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="e3197-645">50016</span><span class="sxs-lookup"><span data-stu-id="e3197-645">50016</span></span> |
| <span data-ttu-id="e3197-646">SAP uruchamiania usługi Wywołujących HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="e3197-646">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="e3197-647">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="e3197-647">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="e3197-648">51013</span><span class="sxs-lookup"><span data-stu-id="e3197-648">51013</span></span> |
| <span data-ttu-id="e3197-649">SAP uruchamiania usługi Wywołujących HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="e3197-649">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="e3197-650">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="e3197-650">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="e3197-651">51014</span><span class="sxs-lookup"><span data-stu-id="e3197-651">51014</span></span> |
| <span data-ttu-id="e3197-652">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="e3197-652">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="e3197-653">5985</span><span class="sxs-lookup"><span data-stu-id="e3197-653">5985</span></span> |
| <span data-ttu-id="e3197-654">Udział plików *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="e3197-654">File Share *Lbrule445*</span></span> | |<span data-ttu-id="e3197-655">445</span><span class="sxs-lookup"><span data-stu-id="e3197-655">445</span></span> |

<span data-ttu-id="e3197-656">_**Tabela 1:** portu liczby wystąpień programu SAP NetWeaver ABAP ASCS_</span><span class="sxs-lookup"><span data-stu-id="e3197-656">_**Table 1:** Port numbers of the SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="e3197-657">Następnie utwórz te równoważenia punktów końcowych dla portów SAP NetWeaver Java SCS obciążenia:</span><span class="sxs-lookup"><span data-stu-id="e3197-657">Then, create these load balancing endpoints for the SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="e3197-658">Nazwa reguły równoważenia obciążenia/usługi</span><span class="sxs-lookup"><span data-stu-id="e3197-658">Service/load balancing rule name</span></span> | <span data-ttu-id="e3197-659">Domyślne numery portów</span><span class="sxs-lookup"><span data-stu-id="e3197-659">Default port numbers</span></span> | <span data-ttu-id="e3197-660">Konkretnych portów (SCS wystąpienia z liczby wystąpień 01) (Wywołujących z 11)</span><span class="sxs-lookup"><span data-stu-id="e3197-660">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3197-661">Umieścić serwer / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="e3197-661">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="e3197-662">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e3197-662">32<*InstanceNumber*></span></span> |<span data-ttu-id="e3197-663">3201</span><span class="sxs-lookup"><span data-stu-id="e3197-663">3201</span></span> |
| <span data-ttu-id="e3197-664">Serwer bramy / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="e3197-664">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="e3197-665">33 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e3197-665">33<*InstanceNumber*></span></span> |<span data-ttu-id="e3197-666">3301</span><span class="sxs-lookup"><span data-stu-id="e3197-666">3301</span></span> |
| <span data-ttu-id="e3197-667">Serwer komunikatów Java / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="e3197-667">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="e3197-668">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e3197-668">39<*InstanceNumber*></span></span> |<span data-ttu-id="e3197-669">3901</span><span class="sxs-lookup"><span data-stu-id="e3197-669">3901</span></span> |
| <span data-ttu-id="e3197-670">Serwer HTTP / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="e3197-670">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="e3197-671">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="e3197-671">81<*InstanceNumber*></span></span> |<span data-ttu-id="e3197-672">8101</span><span class="sxs-lookup"><span data-stu-id="e3197-672">8101</span></span> |
| <span data-ttu-id="e3197-673">SAP uruchamiania usługi SCS HTTP / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="e3197-673">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="e3197-674">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="e3197-674">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="e3197-675">50113</span><span class="sxs-lookup"><span data-stu-id="e3197-675">50113</span></span> |
| <span data-ttu-id="e3197-676">SAP uruchamiania usługi SCS HTTPS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="e3197-676">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="e3197-677">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="e3197-677">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="e3197-678">50114</span><span class="sxs-lookup"><span data-stu-id="e3197-678">50114</span></span> |
| <span data-ttu-id="e3197-679">Umieścić w kolejce replikacji / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="e3197-679">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="e3197-680">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="e3197-680">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="e3197-681">50116</span><span class="sxs-lookup"><span data-stu-id="e3197-681">50116</span></span> |
| <span data-ttu-id="e3197-682">SAP uruchamiania usługi Wywołujących HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="e3197-682">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="e3197-683">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="e3197-683">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="e3197-684">51113</span><span class="sxs-lookup"><span data-stu-id="e3197-684">51113</span></span> |
| <span data-ttu-id="e3197-685">SAP uruchamiania usługi Wywołujących HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="e3197-685">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="e3197-686">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="e3197-686">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="e3197-687">51114</span><span class="sxs-lookup"><span data-stu-id="e3197-687">51114</span></span> |
| <span data-ttu-id="e3197-688">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="e3197-688">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="e3197-689">5985</span><span class="sxs-lookup"><span data-stu-id="e3197-689">5985</span></span> |
| <span data-ttu-id="e3197-690">Udział plików *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="e3197-690">File Share *Lbrule445*</span></span> | |<span data-ttu-id="e3197-691">445</span><span class="sxs-lookup"><span data-stu-id="e3197-691">445</span></span> |

<span data-ttu-id="e3197-692">_**Tabela 2:** portu liczby wystąpień programu SAP NetWeaver Java SCS_</span><span class="sxs-lookup"><span data-stu-id="e3197-692">_**Table 2:** Port numbers of the SAP NetWeaver Java SCS instances_</span></span>

![Rys. 15: Reguły dla usługi równoważenia obciążenia Azure wewnętrzny równoważenia obciążenia domyślne ASCS/SCS][sap-ha-guide-figure-3004]

<span data-ttu-id="e3197-694">_**Rysunek 15:** reguły dla usługi równoważenia obciążenia Azure wewnętrzny równoważenia obciążenia domyślne ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="e3197-694">_**Figure 15:** Default ASCS/SCS load balancing rules for the Azure internal load balancer_</span></span>

<span data-ttu-id="e3197-695">Ustawienie adresu IP usługi równoważenia obciążenia **pr1-lb-dbms** adres IP nazwę hosta wirtualnego wystąpienia systemu DBMS.</span><span class="sxs-lookup"><span data-stu-id="e3197-695">Set the IP address of the load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

### <span data-ttu-id="e3197-696"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Zmień zasady dla usługi równoważenia obciążenia Azure wewnętrzny równoważenia obciążenia domyślne ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-696"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change the ASCS/SCS default load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="e3197-697">Jeśli chcesz użyć innej liczby wystąpień SAP ASCS lub SCS, należy zmienić nazwy i wartości ich porty wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-697">If you want to use different numbers for the SAP ASCS or SCS instances, you must change the names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="e3197-698">W portalu Azure wybierz  **<* SID*> - lb - ascs załadować równoważenia ** > **reguły równoważenia obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="e3197-698">In the Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="e3197-699">Dla wszystkich reguł, które należą do wystąpienia SAP ASCS lub SCS równoważenia obciążenia Zmień wartości tych:</span><span class="sxs-lookup"><span data-stu-id="e3197-699">For all load balancing rules that belong to the SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="e3197-700">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e3197-700">Name</span></span>
  * <span data-ttu-id="e3197-701">Port</span><span class="sxs-lookup"><span data-stu-id="e3197-701">Port</span></span>
  * <span data-ttu-id="e3197-702">Port zaplecza</span><span class="sxs-lookup"><span data-stu-id="e3197-702">Back-end port</span></span>

  <span data-ttu-id="e3197-703">Na przykład jeśli chcesz zmienić domyślną liczbę wystąpień ASCS od 00 do 31, musisz wprowadzić zmiany dla wszystkich portów wymienionych w tabeli 1.</span><span class="sxs-lookup"><span data-stu-id="e3197-703">For example, if you want to change the default ASCS instance number from 00 to 31, you need to make the changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="e3197-704">Oto przykład aktualizacji dla portu *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="e3197-704">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Rysunek 16: Zmień obciążenia domyślne ASCS/SCS równoważenia zasady Azure wewnętrznego modułu równoważenia obciążenia][sap-ha-guide-figure-3005]

  <span data-ttu-id="e3197-706">_**Rysunek 16:** Zmień zasady dla usługi równoważenia obciążenia Azure wewnętrzny równoważenia obciążenia domyślne ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="e3197-706">_**Figure 16:** Change the ASCS/SCS default load balancing rules for the Azure internal load balancer_</span></span>

### <span data-ttu-id="e3197-707"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Dodawanie maszyn wirtualnych systemu Windows do domeny</span><span class="sxs-lookup"><span data-stu-id="e3197-707"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines to the domain</span></span>

<span data-ttu-id="e3197-708">Po przypisaniu statycznego adresu IP do maszyn wirtualnych, Dodaj maszyny wirtualne do domeny.</span><span class="sxs-lookup"><span data-stu-id="e3197-708">After you assign a static IP address to the virtual machines, add the virtual machines to the domain.</span></span>

![Rysunek 17: Dodaj maszynę wirtualną do domeny][sap-ha-guide-figure-3006]

<span data-ttu-id="e3197-710">_**Rysunek 17:** Dodaj maszynę wirtualną do domeny_</span><span class="sxs-lookup"><span data-stu-id="e3197-710">_**Figure 17:** Add a virtual machine to a domain_</span></span>

### <span data-ttu-id="e3197-711"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Dodawanie wpisów rejestru na obu węzłach klastra z wystąpieniem SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-711"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of the SAP ASCS/SCS instance</span></span>

<span data-ttu-id="e3197-712">Moduł równoważenia obciążenia Azure zawiera wewnętrzny moduł równoważenia obciążenia zamknięciu połączeń w przypadku połączenia są w stanie bezczynności pewien okres czasu (limit czasu bezczynności).</span><span class="sxs-lookup"><span data-stu-id="e3197-712">Azure Load Balancer has an internal load balancer that closes connections when the connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="e3197-713">Procesy robocze SAP w oknie dialogowym wystąpień otwarte połączenia można umieścić w kolejce SAP przetworzyć zaraz po pierwszym umieścić w kolejce/usuwania z kolejki żądania musi być wysyłane.</span><span class="sxs-lookup"><span data-stu-id="e3197-713">SAP work processes in dialog instances open connections to the SAP enqueue process as soon as the first enqueue/dequeue request needs to be sent.</span></span> <span data-ttu-id="e3197-714">Te połączenia zazwyczaj pozostają ustalonych dopóki proces pracy lub ponownego uruchomienia procesu umieścić w kolejce.</span><span class="sxs-lookup"><span data-stu-id="e3197-714">These connections usually remain established until the work process or the enqueue process restarts.</span></span> <span data-ttu-id="e3197-715">Jednak jeśli połączenie jest bezczynne na wybrany okres czasu, Azure wewnętrznego modułu równoważenia obciążenia zamyka połączenia.</span><span class="sxs-lookup"><span data-stu-id="e3197-715">However, if the connection is idle for a set period of time, the Azure internal load balancer closes the connections.</span></span> <span data-ttu-id="e3197-716">Nie stanowi problemu, ponieważ proces roboczy SAP przywraca połączenie do procesu umieścić w kolejce, jeśli już nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="e3197-716">This isn't a problem because the SAP work process reestablishes the connection to the enqueue process if it no longer exists.</span></span> <span data-ttu-id="e3197-717">Te działania są udokumentowane w ślady developer procesów SAP, ale ich tworzyć dużą ilością zawartości dodatkowe w tych danych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="e3197-717">These activities are documented in the developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="e3197-718">Zaleca się zmienić TCP/IP `KeepAliveTime` i `KeepAliveInterval` na obu węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-718">It's a good idea to change the TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="e3197-719">Połącz te zmiany w parametrach TCP/IP z parametrami profilu SAP, opisane w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="e3197-719">Combine these changes in the TCP/IP parameters with SAP profile parameters, described later in the article.</span></span>

<span data-ttu-id="e3197-720">Aby dodać wpisów rejestru na obu węzłach klastra z wystąpieniem SAP ASCS/SCS, najpierw dodaj te wpisy rejestru systemu Windows na obu węzłów klastra systemu Windows dla programu SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="e3197-720">To add registry entries on both cluster nodes of the SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="e3197-721">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="e3197-721">Path</span></span> | <span data-ttu-id="e3197-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="e3197-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="e3197-723">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="e3197-723">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="e3197-724">Typ zmiennej</span><span class="sxs-lookup"><span data-stu-id="e3197-724">Variable type</span></span> |<span data-ttu-id="e3197-725">REG_DWORD (dziesiętna)</span><span class="sxs-lookup"><span data-stu-id="e3197-725">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="e3197-726">Wartość</span><span class="sxs-lookup"><span data-stu-id="e3197-726">Value</span></span> |<span data-ttu-id="e3197-727">120000</span><span class="sxs-lookup"><span data-stu-id="e3197-727">120000</span></span> |
| <span data-ttu-id="e3197-728">Połącz się z dokumentacją</span><span class="sxs-lookup"><span data-stu-id="e3197-728">Link to documentation</span></span> |[<span data-ttu-id="e3197-729">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="e3197-729">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="e3197-730">_**Tabela 3:** zmienić pierwszy parametr TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="e3197-730">_**Table 3:** Change the first TCP/IP parameter_</span></span>

<span data-ttu-id="e3197-731">Następnie należy dodać ten wpisów rejestru systemu Windows na obu węzłów klastra systemu Windows dla programu SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="e3197-731">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="e3197-732">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="e3197-732">Path</span></span> | <span data-ttu-id="e3197-733">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="e3197-733">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="e3197-734">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="e3197-734">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="e3197-735">Typ zmiennej</span><span class="sxs-lookup"><span data-stu-id="e3197-735">Variable type</span></span> |<span data-ttu-id="e3197-736">REG_DWORD (dziesiętna)</span><span class="sxs-lookup"><span data-stu-id="e3197-736">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="e3197-737">Wartość</span><span class="sxs-lookup"><span data-stu-id="e3197-737">Value</span></span> |<span data-ttu-id="e3197-738">120000</span><span class="sxs-lookup"><span data-stu-id="e3197-738">120000</span></span> |
| <span data-ttu-id="e3197-739">Połącz się z dokumentacją</span><span class="sxs-lookup"><span data-stu-id="e3197-739">Link to documentation</span></span> |[<span data-ttu-id="e3197-740">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="e3197-740">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="e3197-741">_**Tabela 4:** zmienić drugi parametr TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="e3197-741">_**Table 4:** Change the second TCP/IP parameter_</span></span>

<span data-ttu-id="e3197-742">**Aby zastosować zmiany, należy ponownie uruchomić oba węzły klastra**.</span><span class="sxs-lookup"><span data-stu-id="e3197-742">**To apply the changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="e3197-743"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a>Konfigurowanie klastra systemu Windows Server Failover Clustering dla wystąpienia programu SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-743"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="e3197-744">Konfigurowanie klastra systemu Windows Server Failover Clustering dla wystąpienia programu SAP ASCS/SCS obejmuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="e3197-744">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="e3197-745">Zbieranie węzłów klastra w konfiguracji klastra</span><span class="sxs-lookup"><span data-stu-id="e3197-745">Collecting the cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="e3197-746">Konfigurowanie monitora udziału plików klastra</span><span class="sxs-lookup"><span data-stu-id="e3197-746">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="e3197-747"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Zbieraj węzły klastra w konfiguracji klastra</span><span class="sxs-lookup"><span data-stu-id="e3197-747"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect the cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="e3197-748">Dodawanie roli i funkcji — Kreator Dodaj klaster dla obu węzłów klastra trybu failover.</span><span class="sxs-lookup"><span data-stu-id="e3197-748">In the Add Role and Features Wizard, add failover clustering to both cluster nodes.</span></span>
2.  <span data-ttu-id="e3197-749">Konfigurowanie klastra trybu failover za pomocą Menedżera klastra trybu Failover.</span><span class="sxs-lookup"><span data-stu-id="e3197-749">Set up the failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="e3197-750">W Menedżerze klastra trybu Failover wybierz **tworzenia klastrów**, a następnie dodaj tylko nazwę klastra pierwszy węzeł A. Nie dodawaj drugiego węzła jeszcze; drugi węzeł zostanie dodana w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="e3197-750">In Failover Cluster Manager, select **Create Cluster**, and then add only the name of the first cluster, node A. Do not add the second node yet; you'll add the second node in a later step.</span></span>

  ![Rysunek 18: Dodaj nazwę serwera lub maszyny wirtualnej na pierwszym węźle klastra][sap-ha-guide-figure-3007]

  <span data-ttu-id="e3197-752">_**Rysunek 18:** Dodaj nazwę serwera lub maszyny wirtualnej w pierwszym węźle klastra_</span><span class="sxs-lookup"><span data-stu-id="e3197-752">_**Figure 18:** Add the server or virtual machine name of the first cluster node_</span></span>

3.  <span data-ttu-id="e3197-753">Wprowadź nazwę sieci (nazwa hosta wirtualnego) klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-753">Enter the network name (virtual host name) of the cluster.</span></span>

  ![Rysunek 19: Wprowadź nazwę klastra][sap-ha-guide-figure-3008]

  <span data-ttu-id="e3197-755">_**Rysunek 19:** wprowadź nazwę klastra_</span><span class="sxs-lookup"><span data-stu-id="e3197-755">_**Figure 19:** Enter the cluster name_</span></span>

4.  <span data-ttu-id="e3197-756">Po utworzeniu klastra, uruchom test sprawdzania poprawności klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-756">After you've created the cluster, run a cluster validation test.</span></span>

  ![Rysunek 20: Uruchom sprawdzenie poprawności klastra][sap-ha-guide-figure-3009]

  <span data-ttu-id="e3197-758">_**Rysunek 20:** uruchom sprawdzenie poprawności klastra_</span><span class="sxs-lookup"><span data-stu-id="e3197-758">_**Figure 20:** Run the cluster validation check_</span></span>

  <span data-ttu-id="e3197-759">Możesz zignorować ostrzeżenia dotyczące dysków na tym etapie procesu.</span><span class="sxs-lookup"><span data-stu-id="e3197-759">You can ignore any warnings about disks at this point in the process.</span></span> <span data-ttu-id="e3197-760">Zostanie dodana monitora udostępniania plików i SIOS udostępnionych dysków później.</span><span class="sxs-lookup"><span data-stu-id="e3197-760">You'll add a file share witness and the SIOS shared disks later.</span></span> <span data-ttu-id="e3197-761">Na tym etapie nie trzeba martwić o kworum.</span><span class="sxs-lookup"><span data-stu-id="e3197-761">At this stage, you don't need to worry about having a quorum.</span></span>

  ![Rysunek 21: Odnaleziono żadnego dysku kworum][sap-ha-guide-figure-3010]

  <span data-ttu-id="e3197-763">_**Rysunek 21:** odnaleziono żadnego dysku kworum_</span><span class="sxs-lookup"><span data-stu-id="e3197-763">_**Figure 21:** No quorum disk is found_</span></span>

  ![Rysunek 22: Zasobu klastra Core wymaga nowego adresu IP][sap-ha-guide-figure-3011]

  <span data-ttu-id="e3197-765">_**Rysunek 22:** zasobu klastra Core wymaga nowego adresu IP_</span><span class="sxs-lookup"><span data-stu-id="e3197-765">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="e3197-766">Zmienianie adresu IP usługi klastrowania core.</span><span class="sxs-lookup"><span data-stu-id="e3197-766">Change the IP address of the core cluster service.</span></span> <span data-ttu-id="e3197-767">Klastra nie można uruchomić, dopóki nie zmieni adres IP klastra usługi podstawowej, ponieważ adres IP serwera wskazuje na jednym z węzłów maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3197-767">The cluster can't start until you change the IP address of the core cluster service, because the IP address of the server points to one of the virtual machine nodes.</span></span> <span data-ttu-id="e3197-768">To zrobić na **właściwości** strony podstawowej usługi klastrowania IP zasobu.</span><span class="sxs-lookup"><span data-stu-id="e3197-768">Do this on the **Properties** page of the core cluster service's IP resource.</span></span>

  <span data-ttu-id="e3197-769">Na przykład, należy przypisać adres IP (w naszym przykładzie **10.0.0.42**) dla nazwy hostów wirtualnych klastra **pr1-ascs-vir**.</span><span class="sxs-lookup"><span data-stu-id="e3197-769">For example, we need to assign an IP address (in our example, **10.0.0.42**) for the cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Rysunek 23: W oknie dialogowym właściwości Zmień adres IP][sap-ha-guide-figure-3012]

  <span data-ttu-id="e3197-771">_**Rysunek 23:** w **właściwości** okno dialogowe Zmień adres IP_</span><span class="sxs-lookup"><span data-stu-id="e3197-771">_**Figure 23:** In the **Properties** dialog box, change the IP address_</span></span>

  ![Rysunek 24: Przypisz adres IP, które jest zastrzeżone dla klastra][sap-ha-guide-figure-3013]

  <span data-ttu-id="e3197-773">_**Rysunek 24:** przypisać adres IP, które jest zastrzeżone dla klastra_</span><span class="sxs-lookup"><span data-stu-id="e3197-773">_**Figure 24:** Assign the IP address that is reserved for the cluster_</span></span>

6.  <span data-ttu-id="e3197-774">Przełącz tryb online nazwę hosta wirtualnego klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-774">Bring the cluster virtual host name online.</span></span>

  ![25 rysunek: Usługi podstawowej klastra jest uruchomiony i działa prawidłowo i z poprawny adres IP adresów][sap-ha-guide-figure-3014]

  <span data-ttu-id="e3197-776">_**Rysunek 25:** usługi podstawowej klastra jest uruchomiony i działa prawidłowo i z poprawny adres IP adresów_</span><span class="sxs-lookup"><span data-stu-id="e3197-776">_**Figure 25:** Cluster core service is up and running, and with the correct IP address_</span></span>

7.  <span data-ttu-id="e3197-777">Dodawanie drugiego węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-777">Add the second cluster node.</span></span>

  <span data-ttu-id="e3197-778">Teraz, podstawowa usługa klastrowania jest uruchomiona, można dodać drugiego węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-778">Now that the core cluster service is up and running, you can add the second cluster node.</span></span>

  ![Rysunek 26: Dodanie drugiego węzła klastra][sap-ha-guide-figure-3015]

  <span data-ttu-id="e3197-780">_**Rysunek 26:** dodania drugiego węzła klastra_</span><span class="sxs-lookup"><span data-stu-id="e3197-780">_**Figure 26:** Add the second cluster node_</span></span>

8.  <span data-ttu-id="e3197-781">Wprowadź nazwę hosta drugiego węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-781">Enter a name for the second cluster node host.</span></span>

  ![Rysunek 27: Wprowadź nazwę hosta drugiego węzła klastra][sap-ha-guide-figure-3016]

  <span data-ttu-id="e3197-783">_**Rysunek 27:** wprowadź nazwę hosta drugiego węzła klastra_</span><span class="sxs-lookup"><span data-stu-id="e3197-783">_**Figure 27:** Enter the second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e3197-784">Upewnij się, że **Dodaj wszystkie odpowiednie magazyny do klastra** pole wyboru jest **nie** wybrane.</span><span class="sxs-lookup"><span data-stu-id="e3197-784">Be sure that the **Add all eligible storage to the cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Rysunek 28: Nie zaznaczaj pola wyboru][sap-ha-guide-figure-3017]

  <span data-ttu-id="e3197-786">_**Rysunek 28:** czy **nie** zaznacz pole wyboru_</span><span class="sxs-lookup"><span data-stu-id="e3197-786">_**Figure 28:** Do **not** select the check box_</span></span>

  <span data-ttu-id="e3197-787">Możesz zignorować ostrzeżenia dotyczące kworum i dysków.</span><span class="sxs-lookup"><span data-stu-id="e3197-787">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="e3197-788">Należy ustawić kworum i udostępnić dysk później, zgodnie z opisem w [instalowanie SIOS DataKeeper Cluster Edition dla programu SAP ASCS/SCS dysku klastra, udziału][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="e3197-788">You'll set the quorum and share the disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Rysunek 29: Ignoruj ostrzeżenia dotyczące dysku kworum][sap-ha-guide-figure-3018]

  <span data-ttu-id="e3197-790">_**Rysunek 29:** Ignoruj ostrzeżenia dotyczące dysku kworum_</span><span class="sxs-lookup"><span data-stu-id="e3197-790">_**Figure 29:** Ignore warnings about the disk quorum_</span></span>


#### <span data-ttu-id="e3197-791"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a>Skonfiguruj Monitor udziału plików klastra</span><span class="sxs-lookup"><span data-stu-id="e3197-791"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="e3197-792">Konfigurowanie monitora udziału plików klastra obejmuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="e3197-792">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="e3197-793">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="e3197-793">Creating a file share</span></span>
- <span data-ttu-id="e3197-794">Ustawienia kworum monitora udziału plików w Menedżerze klastra trybu Failover</span><span class="sxs-lookup"><span data-stu-id="e3197-794">Setting the file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="e3197-795"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a>Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="e3197-795"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="e3197-796">Wybierz monitor udziału plików, zamiast dysku kworum.</span><span class="sxs-lookup"><span data-stu-id="e3197-796">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="e3197-797">SIOS DataKeeper obsługuje tę opcję.</span><span class="sxs-lookup"><span data-stu-id="e3197-797">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="e3197-798">W przykładach w niniejszym artykule monitora udziału plików jest na serwerze/DNS usługi Active Directory, który działa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-798">In the examples in this article, the file share witness is on the Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="e3197-799">Monitor udziału plików jest nazywany **domcontr 0**.</span><span class="sxs-lookup"><span data-stu-id="e3197-799">The file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="e3197-800">Czy skonfigurować połączenia sieci VPN platformy Azure (za pośrednictwem sieci VPN typu lokacja-lokacja lub usługa Azure ExpressRoute), monitor udostępniania sieci/DNS usługi Active Directory usługi lokalnej i nie jest odpowiedni do uruchomienia pliku.</span><span class="sxs-lookup"><span data-stu-id="e3197-800">Because you would have configured a VPN connection to Azure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable to run a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e3197-801">Jeśli usługa/DNS usługi Active Directory działa tylko na lokalne, nie skonfigurować Twoje monitora udziału plików na Active Directory/serwera DNS systemu operacyjnego działającej lokalnie.</span><span class="sxs-lookup"><span data-stu-id="e3197-801">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on the Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="e3197-802">Opóźnienie sieci między węzłami klastra z systemem Azure i/DNS usługi Active Directory w lokalnym programie może być zbyt duży i spowodować problemy z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="e3197-802">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="e3197-803">Należy skonfigurować monitor udostępniania plików na maszynie wirtualnej platformy Azure, uruchomionym bliski węzeł klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-803">Be sure to configure the file share witness on an Azure virtual machine that is running close to the cluster node.</span></span>  
  >
  >

  <span data-ttu-id="e3197-804">Stacja kworum wymaga co najmniej 1024 MB wolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="e3197-804">The quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="e3197-805">Zaleca się 2048 MB wolnego miejsca na dysku kworum.</span><span class="sxs-lookup"><span data-stu-id="e3197-805">We recommend 2,048 MB of free space for the quorum drive.</span></span>

2.  <span data-ttu-id="e3197-806">Dodaj obiekt nazwy klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-806">Add the cluster name object.</span></span>

  ![Rysunek 30: Przypisz uprawnienia udziału dla obiekt nazwy klastra][sap-ha-guide-figure-3019]

  <span data-ttu-id="e3197-808">_**Rysunek 30:** przypisać uprawnienia do udziału dla obiekt nazwy klastra_</span><span class="sxs-lookup"><span data-stu-id="e3197-808">_**Figure 30:** Assign the permissions on the share for the cluster name object_</span></span>

  <span data-ttu-id="e3197-809">Pamiętaj, że uprawnienia obejmuje uprawnienia do zmiany danych w udziale dla obiekt nazwy klastra (w naszym przykładzie **pr1-ascs-vir$**).</span><span class="sxs-lookup"><span data-stu-id="e3197-809">Be sure that the permissions include the authority to change data in the share for the cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="e3197-810">Aby dodać obiekt nazwy klastra do listy, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="e3197-810">To add the cluster name object to the list, select **Add**.</span></span> <span data-ttu-id="e3197-811">Zmień filtr, aby wyszukać obiektów komputerów, oprócz tych pokazano na rysunku 31.</span><span class="sxs-lookup"><span data-stu-id="e3197-811">Change the filter to check for computer objects, in addition to those shown in Figure 31.</span></span>

  ![Rysunek 31: Zmień typy obiektów, aby obejmują komputery][sap-ha-guide-figure-3020]

  <span data-ttu-id="e3197-813">_**Rysunek 31:** zmienić typ obiektu do obejmują komputery_</span><span class="sxs-lookup"><span data-stu-id="e3197-813">_**Figure 31:** Change the Object Types to include computers_</span></span>

  ![Rysunek 32: Zaznacz pole wyboru komputerów][sap-ha-guide-figure-3021]

  <span data-ttu-id="e3197-815">_**Rysunek 32:** wybierz **komputery** pole wyboru_</span><span class="sxs-lookup"><span data-stu-id="e3197-815">_**Figure 32:** Select the **Computers** check box_</span></span>

4.  <span data-ttu-id="e3197-816">Wprowadź obiektem nazwy klastra, tak jak pokazano na rysunku 31.</span><span class="sxs-lookup"><span data-stu-id="e3197-816">Enter the cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="e3197-817">Ponieważ rekord został już utworzony, można zmienić uprawnienia, jak pokazano na rysunku 30.</span><span class="sxs-lookup"><span data-stu-id="e3197-817">Because the record has already been created, you can change the permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="e3197-818">Wybierz **zabezpieczeń** karcie udziału, a następnie ustawić bardziej szczegółowe uprawnienia dla obiekt nazwy klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-818">Select the **Security** tab of the share, and then set more detailed permissions for the cluster name object.</span></span>

  ![Rysunek nr 33: Ustawić atrybutów zabezpieczeń dla obiekt nazwy klastra kworum udziału plików][sap-ha-guide-figure-3022]

  <span data-ttu-id="e3197-820">_**Rysunek nr 33:** ustawić atrybutów zabezpieczeń dla obiekt nazwy klastra kworum udziału plików_</span><span class="sxs-lookup"><span data-stu-id="e3197-820">_**Figure 33:** Set the security attributes for the cluster name object on the file share quorum_</span></span>

##### <span data-ttu-id="e3197-821"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Ustaw kworum monitora udziału plików w Menedżerze klastra trybu Failover</span><span class="sxs-lookup"><span data-stu-id="e3197-821"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set the file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="e3197-822">Otwórz kworum ustawienia kreatora konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e3197-822">Open the Configure Quorum Setting Wizard.</span></span>

  ![Rysunek 34: Uruchom Kreator ustawienia kworum klastra Konfiguruj][sap-ha-guide-figure-3023]

  <span data-ttu-id="e3197-824">_**Rysunek 34:** Uruchamianie Kreatora ustawienie Konfigurowanie kworum klastra_</span><span class="sxs-lookup"><span data-stu-id="e3197-824">_**Figure 34:** Start the Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="e3197-825">Na **wybrać konfigurację kworum** wybierz **Wybieranie monitora kworum**.</span><span class="sxs-lookup"><span data-stu-id="e3197-825">On the **Select Quorum Configuration** page, select **Select the quorum witness**.</span></span>

  ![Rysunek 35: Konfiguracji kworum, możesz wybrać z][sap-ha-guide-figure-3024]

  <span data-ttu-id="e3197-827">_**Rysunek 35:** konfiguracji kworum, możesz wybrać spośród_</span><span class="sxs-lookup"><span data-stu-id="e3197-827">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="e3197-828">Na **Wybieranie monitora kworum** wybierz **Konfigurowanie monitora udziału plików**.</span><span class="sxs-lookup"><span data-stu-id="e3197-828">On the **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![Rysunek 36: Wybierz monitor udziału plików][sap-ha-guide-figure-3025]

  <span data-ttu-id="e3197-830">_**Rysunek 36:** Wybierz monitor udziału plików_</span><span class="sxs-lookup"><span data-stu-id="e3197-830">_**Figure 36:** Select the file share witness_</span></span>

4.  <span data-ttu-id="e3197-831">Wprowadź ścieżkę UNC do udziału plików (w naszym przykładzie \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="e3197-831">Enter the UNC path to the file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="e3197-832">Aby wyświetlić listę wprowadzania zmian, zaznacz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="e3197-832">To see a list of the changes you can make, select **Next**.</span></span>

  ![Rysunek 37: Zdefiniuj lokalizację udziału plików monitora udziału][sap-ha-guide-figure-3026]

  <span data-ttu-id="e3197-834">_**Rysunek 37:** określić lokalizację udziału plików monitora udziału_</span><span class="sxs-lookup"><span data-stu-id="e3197-834">_**Figure 37:** Define the file share location for the witness share_</span></span>

5.  <span data-ttu-id="e3197-835">Wybierz zmiany, a następnie wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="e3197-835">Select the changes you want, and then select **Next**.</span></span> <span data-ttu-id="e3197-836">Należy pomyślnie ponownie skonfigurować konfigurację klastra, jak pokazano na rysunku 38.</span><span class="sxs-lookup"><span data-stu-id="e3197-836">You need to successfully reconfigure the cluster configuration as shown in Figure 38.</span></span>  

  ![38 rysunek: Potwierdzenie, że po zmianie konfiguracji klastra][sap-ha-guide-figure-3027]

  <span data-ttu-id="e3197-838">_**Rysunek 38:** potwierdzenie, że po zmianie konfiguracji klastra_</span><span class="sxs-lookup"><span data-stu-id="e3197-838">_**Figure 38:** Confirmation that you've reconfigured the cluster_</span></span>

<span data-ttu-id="e3197-839">Po pomyślnym zainstalowaniu klastra pracy awaryjnej systemu Windows, należy dokonać niektórych progi w celu dostosowania wykrywania trybu failover do warunków na platformie Azure zmiany.</span><span class="sxs-lookup"><span data-stu-id="e3197-839">After installing the Windows Failover Cluster successfully, changes need to be made to some thresholds to adapt failover detection to conditions in Azure.</span></span> <span data-ttu-id="e3197-840">Można zmienić parametry są opisane w tym blogu: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="e3197-840">The parameters to be changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="e3197-841">Przy założeniu, że Twoje dwóch maszyn wirtualnych, które kompilacji konfiguracji klastra systemu Windows dla ASCS/SCS znajdują się w tej samej podsieci, wymaga zmiany tych wartości następujących parametrów:</span><span class="sxs-lookup"><span data-stu-id="e3197-841">Assuming that your two VMs that build the Windows Cluster Configuration for ASCS/SCS are in the same SubNet, the following parameters need to be changed to these values:</span></span>
- <span data-ttu-id="e3197-842">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="e3197-842">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="e3197-843">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="e3197-843">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="e3197-844">Te ustawienia zostały przetestowane z klientami i dostępne dobrej naruszenia pozwala uzyskać odporność na jednej stronie.</span><span class="sxs-lookup"><span data-stu-id="e3197-844">These settings were tested with customers and provided a good compromise to be resilient enough on the one side.</span></span> <span data-ttu-id="e3197-845">Z drugiej strony te ustawienia zostały udostępnianie fast wystarczająco dużo pracy awaryjnej w warunkach rzeczywistych błędu w przypadku awarii oprogramowania lub węzeł/wirtualna SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-845">On the other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="e3197-846"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Zainstaluj dla dysku udziału klastra SAP ASCS/SCS SIOS DataKeeper Cluster Edition</span><span class="sxs-lookup"><span data-stu-id="e3197-846"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="e3197-847">Masz teraz pracy konfiguracji klastra trybu Failover systemu Windows Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-847">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="e3197-848">Jednak, aby zainstalować wystąpienie programu SAP ASCS/SCS, zasób udostępniony dysk.</span><span class="sxs-lookup"><span data-stu-id="e3197-848">But, to install an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="e3197-849">Nie można utworzyć o współużytkowane zasoby dyskowe potrzebne na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-849">You cannot create the shared disk resources you need in Azure.</span></span> <span data-ttu-id="e3197-850">SIOS DataKeeper Cluster Edition jest rozwiązań innych firm, których można używać do tworzenia współużytkowane zasoby dyskowe.</span><span class="sxs-lookup"><span data-stu-id="e3197-850">SIOS DataKeeper Cluster Edition is a third-party solution you can use to create shared disk resources.</span></span>

<span data-ttu-id="e3197-851">Instalowanie SIOS DataKeeper Cluster Edition dla udziału dysk klastrowy SAP ASCS/SCS obejmuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="e3197-851">Installing SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="e3197-852">Dodawanie programu .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="e3197-852">Adding the .NET Framework 3.5</span></span>
- <span data-ttu-id="e3197-853">Instalowanie SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e3197-853">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="e3197-854">Konfigurowanie SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e3197-854">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="e3197-855"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Dodaj programu .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="e3197-855"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add the .NET Framework 3.5</span></span>
<span data-ttu-id="e3197-856">Microsoft .NET Framework 3.5 nie jest automatycznie aktywowane lub zainstalowany w systemie Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="e3197-856">The Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="e3197-857">Ponieważ SIOS DataKeeper wymaga programu .NET Framework jako we wszystkich węzłach, które należy zainstalować na DataKeeper, należy zainstalować program .NET Framework 3.5 w systemie operacyjnym gościa wszystkich maszyn wirtualnych w klastrze.</span><span class="sxs-lookup"><span data-stu-id="e3197-857">Because SIOS DataKeeper requires the .NET Framework to be on all nodes that you install DataKeeper on, you must install the .NET Framework 3.5 on the guest operating system of all virtual machines in the cluster.</span></span>

<span data-ttu-id="e3197-858">Istnieją dwa sposoby dodawania programu .NET Framework 3.5:</span><span class="sxs-lookup"><span data-stu-id="e3197-858">There are two ways to add the .NET Framework 3.5:</span></span>

- <span data-ttu-id="e3197-859">Użyj funkcje Kreatora dodawania ról i w systemie Windows, jak pokazano na rysunku 39.</span><span class="sxs-lookup"><span data-stu-id="e3197-859">Use the Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Rysunek 39: Zainstalować program .NET Framework 3.5 przy użyciu dodawania ról i funkcji — Kreator][sap-ha-guide-figure-3028]

  <span data-ttu-id="e3197-861">_**Rysunek 39:** zainstalować program .NET Framework 3.5 przy użyciu dodawania ról i funkcji — Kreator_</span><span class="sxs-lookup"><span data-stu-id="e3197-861">_**Figure 39:** Install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

  ![40 rysunek: Postęp instalacji pasek po zainstalowaniu programu .NET Framework 3.5 przy użyciu dodawania ról i funkcji — Kreator][sap-ha-guide-figure-3029]

  <span data-ttu-id="e3197-863">_**Rysunek 40:** pasek po zainstalowaniu programu .NET Framework 3.5 przy użyciu funkcji Kreatora dodawania ról i postępu instalacji_</span><span class="sxs-lookup"><span data-stu-id="e3197-863">_**Figure 40:** Installation progress bar when you install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="e3197-864">Użyj narzędzia wiersza polecenia dism.exe.</span><span class="sxs-lookup"><span data-stu-id="e3197-864">Use the command-line tool dism.exe.</span></span> <span data-ttu-id="e3197-865">Ten typ instalacji należy uzyskać dostępu do katalogu SxS na nośniku instalacyjnym systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="e3197-865">For this type of installation, you need to access the SxS directory on the Windows installation media.</span></span> <span data-ttu-id="e3197-866">W wierszu polecenia z podwyższonym poziomem uprawnień wpisz polecenie:</span><span class="sxs-lookup"><span data-stu-id="e3197-866">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="e3197-867"><a name="dd41d5a2-8083-415b-9878-839652812102"></a>Zainstaluj SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e3197-867"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="e3197-868">Zainstaluj SIOS DataKeeper Cluster Edition w każdym węźle w klastrze.</span><span class="sxs-lookup"><span data-stu-id="e3197-868">Install SIOS DataKeeper Cluster Edition on each node in the cluster.</span></span> <span data-ttu-id="e3197-869">Aby utworzyć wirtualny magazynu udostępnionego z SIOS DataKeeper, Utwórz zsynchronizowanej dublowania i następnie symulować magazyn udostępniony klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-869">To create virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="e3197-870">Przed zainstalowaniem oprogramowania SIOS, Utwórz użytkownika domeny **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="e3197-870">Before you install the SIOS software, create the domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="e3197-871">Dodaj **DataKeeperSvc** użytkownikowi **administratora lokalnego** na obu węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-871">Add the **DataKeeperSvc** user to the **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="e3197-872">Aby zainstalować SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="e3197-872">To install SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="e3197-873">Zainstaluj oprogramowanie SIOS na obu węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-873">Install the SIOS software on both cluster nodes.</span></span>

  ![Instalator SIOS][sap-ha-guide-figure-3030]

  ![41 rysunku: Pierwsza strona instalacji SIOS DataKeeper][sap-ha-guide-figure-3031]

  <span data-ttu-id="e3197-876">_**Rysunek 41:** pierwszej strony instalacji SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e3197-876">_**Figure 41:** First page of the SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="e3197-877">W oknie dialogowym pokazano na rysunku 42, wybierz **tak**.</span><span class="sxs-lookup"><span data-stu-id="e3197-877">In the dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Rysunek 42: DataKeeper informuje, czy usługa zostanie wyłączona][sap-ha-guide-figure-3032]

  <span data-ttu-id="e3197-879">_**Rysunek 42:** DataKeeper informuje, że usługa zostanie wyłączona_</span><span class="sxs-lookup"><span data-stu-id="e3197-879">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="e3197-880">W oknie dialogowym pokazano na rysunku 43, zaleca się wybranie **konta domeny lub tego serwera**.</span><span class="sxs-lookup"><span data-stu-id="e3197-880">In the dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Rysunek 43: Wybór użytkownika dla SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="e3197-882">_**Rysunek 43:** SIOS DataKeeper określonego użytkownika_</span><span class="sxs-lookup"><span data-stu-id="e3197-882">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="e3197-883">Wprowadź nazwę użytkownika konta domeny i hasła, które zostały utworzone dla SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="e3197-883">Enter the domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Rysunek 44: Wprowadź nazwę użytkownika domeny i hasło dla instalacji SIOS DataKeeper][sap-ha-guide-figure-3034]

  <span data-ttu-id="e3197-885">_**Rysunek 44:** wprowadź nazwę użytkownika domeny i hasło dla instalacji SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e3197-885">_**Figure 44:** Enter the domain user name and password for the SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="e3197-886">Zainstaluj klucz licencji dla swojego wystąpienia SIOS DataKeeper, jak pokazano na rysunku 45.</span><span class="sxs-lookup"><span data-stu-id="e3197-886">Install the license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Rysunek 45: Wprowadź klucz licencji SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="e3197-888">_**Rysunek 45:** wprowadź klucz licencji SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="e3197-888">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="e3197-889">Po wyświetleniu monitu uruchom ponownie maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="e3197-889">When prompted, restart the virtual machine.</span></span>

#### <span data-ttu-id="e3197-890"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a>Konfigurowanie SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="e3197-890"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="e3197-891">Po zainstalowaniu SIOS DataKeeper na obu węzłach, należy uruchomić konfigurację.</span><span class="sxs-lookup"><span data-stu-id="e3197-891">After you install SIOS DataKeeper on both nodes, you need to start the configuration.</span></span> <span data-ttu-id="e3197-892">Cel konfiguracji ma synchroniczne dane replikacji między dodatkowych dysków dołączonych do poszczególnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-892">The goal of the configuration is to have synchronous data replication between the additional disks attached to each of the virtual machines.</span></span>

1.  <span data-ttu-id="e3197-893">Uruchom narzędzie DataKeeper zarządzania i konfiguracji, a następnie wybierz **połączenia serwera**.</span><span class="sxs-lookup"><span data-stu-id="e3197-893">Start the DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="e3197-894">(W 46 rysunku, ta opcja jest zaznaczona kółkiem na czerwono.)</span><span class="sxs-lookup"><span data-stu-id="e3197-894">(In Figure 46, this option is circled in red.)</span></span>

  ![Rysunek 46: SIOS DataKeeper zarządzanie i narzędzia do konfiguracji][sap-ha-guide-figure-3036]

  <span data-ttu-id="e3197-896">_**Rysunek 46:** narzędzie SIOS DataKeeper zarządzania i konfiguracji_</span><span class="sxs-lookup"><span data-stu-id="e3197-896">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="e3197-897">Wprowadź nazwę lub adres TCP/IP pierwszy węzeł, który narzędzia zarządzania i konfiguracji należy połączenia oraz, w drugim kroku drugiego węzła.</span><span class="sxs-lookup"><span data-stu-id="e3197-897">Enter the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and, in a second step, the second node.</span></span>

  ![Rysunek 47: Wstaw nazwę lub adres TCP/IP pierwszego węzła Zarządzanie i narzędzia do konfiguracji należy łączyć, a w drugim etapie drugiego węzła][sap-ha-guide-figure-3037]

  <span data-ttu-id="e3197-899">_**Rysunek 47:** Wstaw nazwę lub adres TCP/IP pierwszego węzła narzędzie zarządzania i konfiguracji należy łączyć, a w drugim etapie drugiego węzła_</span><span class="sxs-lookup"><span data-stu-id="e3197-899">_**Figure 47:** Insert the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and in a second step, the second node_</span></span>

3.  <span data-ttu-id="e3197-900">Utwórz zadanie replikacji między dwoma węzłami.</span><span class="sxs-lookup"><span data-stu-id="e3197-900">Create the replication job between the two nodes.</span></span>

  ![Rysunek 48: Tworzenie zadania replikacji][sap-ha-guide-figure-3038]

  <span data-ttu-id="e3197-902">_**Rysunek 48:** Utwórz zadanie replikacji_</span><span class="sxs-lookup"><span data-stu-id="e3197-902">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="e3197-903">Kreator prowadzi przez proces tworzenia zadania replikacji.</span><span class="sxs-lookup"><span data-stu-id="e3197-903">A wizard guides you through the process of creating a replication job.</span></span>
4.  <span data-ttu-id="e3197-904">Zdefiniuj nazwę, adres TCP/IP i wolumin dysku węzła źródłowego.</span><span class="sxs-lookup"><span data-stu-id="e3197-904">Define the name, TCP/IP address, and disk volume of the source node.</span></span>

  ![Rysunek 49: Zdefiniuj nazwę zadania replikacji][sap-ha-guide-figure-3039]

  <span data-ttu-id="e3197-906">_**Rysunek 49:** Zdefiniuj nazwę zadania replikacji_</span><span class="sxs-lookup"><span data-stu-id="e3197-906">_**Figure 49:** Define the name of the replication job_</span></span>

  ![Rysunek 50: Definiowanie danych podstawowych dla tego węzła, który powinien być bieżącego węzła źródłowego][sap-ha-guide-figure-3040]

  <span data-ttu-id="e3197-908">_**Rysunek 50:** zdefiniować podstawowe dane dla tego węzła, który powinien być bieżącego węzła źródłowego_</span><span class="sxs-lookup"><span data-stu-id="e3197-908">_**Figure 50:** Define the base data for the node, which should be the current source node_</span></span>

5.  <span data-ttu-id="e3197-909">Zdefiniuj nazwę, adres TCP/IP i wolumin dysku węzła docelowego.</span><span class="sxs-lookup"><span data-stu-id="e3197-909">Define the name, TCP/IP address, and disk volume of the target node.</span></span>

  ![Rysunek 51: Definiowanie danych podstawowych dla tego węzła, który powinien być bieżący węzeł docelowy][sap-ha-guide-figure-3041]

  <span data-ttu-id="e3197-911">_**Rysunek 51:** zdefiniować podstawowe dane dla tego węzła, który powinien być bieżący węzeł docelowy_</span><span class="sxs-lookup"><span data-stu-id="e3197-911">_**Figure 51:** Define the base data for the node, which should be the current target node_</span></span>

6.  <span data-ttu-id="e3197-912">Zdefiniuj algorytmy kompresji.</span><span class="sxs-lookup"><span data-stu-id="e3197-912">Define the compression algorithms.</span></span> <span data-ttu-id="e3197-913">W naszym przykładzie zaleca się, że kompresji strumienia replikacji.</span><span class="sxs-lookup"><span data-stu-id="e3197-913">In our example, we recommend that you compress the replication stream.</span></span> <span data-ttu-id="e3197-914">Szczególnie w sytuacjach, ponowna synchronizacja kompresji, replikacji strumienia znacznie skraca czas ponownej synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="e3197-914">Especially in resynchronization situations, the compression of the replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="e3197-915">Należy pamiętać, że kompresja używa zasobów Procesora i pamięci RAM maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3197-915">Note that compression uses the CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="e3197-916">Jak zwiększa się częstotliwość kompresji, co powoduje ilości zasobów procesora CPU używanych.</span><span class="sxs-lookup"><span data-stu-id="e3197-916">As the compression rate increases, so does the volume of CPU resources used.</span></span> <span data-ttu-id="e3197-917">Można również dostosować to ustawienie później.</span><span class="sxs-lookup"><span data-stu-id="e3197-917">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="e3197-918">Inne ustawienie, które należy sprawdzić to, czy replikacja odbywa się asynchronicznie lub synchronicznie.</span><span class="sxs-lookup"><span data-stu-id="e3197-918">Another setting you need to check is whether the replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="e3197-919">*W przypadku ochrony SAP ASCS/SCS konfiguracji, należy użyć Replikacja synchroniczna*.</span><span class="sxs-lookup"><span data-stu-id="e3197-919">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Rysunek 52: Zdefiniuj szczegóły replikacji][sap-ha-guide-figure-3042]

  <span data-ttu-id="e3197-921">_**Rysunek 52:** Zdefiniuj szczegóły replikacji_</span><span class="sxs-lookup"><span data-stu-id="e3197-921">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="e3197-922">Należy określić, czy wolumin, który jest replikowany za zadanie replikacji powinny być reprezentowane w konfiguracji klastra z systemem Windows Server Failover Clustering jako udostępniony dysk.</span><span class="sxs-lookup"><span data-stu-id="e3197-922">Define whether the volume that is replicated by the replication job should be represented to a Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="e3197-923">SAP ASCS/SCS konfiguracji, wybierz **tak** tak, aby klaster systemu Windows widzi replikowanego woluminu jako udostępnionego dysku, której można użyć jako woluminu klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-923">For the SAP ASCS/SCS configuration, select **Yes** so that the Windows cluster sees the replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Rysunek 53: Wybierz tak, aby ustawić replikowanego woluminu jako woluminu klastra][sap-ha-guide-figure-3043]

  <span data-ttu-id="e3197-925">_**Rysunek 53:** wybierz **tak** można ustawić replikowanego woluminu jako woluminu klastra_</span><span class="sxs-lookup"><span data-stu-id="e3197-925">_**Figure 53:** Select **Yes** to set the replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="e3197-926">Po utworzeniu woluminu narzędzie DataKeeper zarządzania i konfiguracji pokazuje, że zadanie replikacji jest aktywne.</span><span class="sxs-lookup"><span data-stu-id="e3197-926">After the volume is created, the DataKeeper Management and Configuration tool shows that the replication job is active.</span></span>

  ![Rysunek 54: DataKeeper synchronicznego duplikowania dysku udziału SAP ASCS/SCS jest aktywny][sap-ha-guide-figure-3044]

  <span data-ttu-id="e3197-928">_**Rysunek 54:** DataKeeper duplikowanie synchroniczne dla ASCS/SCS programu SAP współużytkować dysku jest aktywny_</span><span class="sxs-lookup"><span data-stu-id="e3197-928">_**Figure 54:** DataKeeper synchronous mirroring for the SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="e3197-929">Menedżer klastra trybu failover zawiera obecnie dysku jako dysku DataKeeper, jak pokazano na rysunku 55.</span><span class="sxs-lookup"><span data-stu-id="e3197-929">Failover Cluster Manager now shows the disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Rysunek 55: Menedżer klastra trybu Failover zawiera dysk, który jest replikowany DataKeeper][sap-ha-guide-figure-3045]

  <span data-ttu-id="e3197-931">_**Rysunek 55:** Menedżera klastra trybu Failover zawiera dysk tego DataKeeper replikowane_</span><span class="sxs-lookup"><span data-stu-id="e3197-931">_**Figure 55:** Failover Cluster Manager shows the disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="e3197-932"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Instalowanie systemu SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="e3197-932"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install the SAP NetWeaver system</span></span>

<span data-ttu-id="e3197-933">Instalator systemu DBMS nie opisano ustawienia się różnić w zależności od używanego systemu DBMS.</span><span class="sxs-lookup"><span data-stu-id="e3197-933">We won’t describe the DBMS setup because setups vary depending on the DBMS system you use.</span></span> <span data-ttu-id="e3197-934">Jednak przyjęto założenie, reagowania problemów o wysokiej dostępności z systemu DBMS z funkcje obsługiwanych przez różnych dostawców DBMS dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-934">However, we assume that high-availability concerns with the DBMS are addressed with the functionalities the different DBMS vendors support for Azure.</span></span> <span data-ttu-id="e3197-935">Na przykład zawsze włączone lub dublowania bazy danych programu SQL Server i Oracle Data Guard dla baz danych Oracle.</span><span class="sxs-lookup"><span data-stu-id="e3197-935">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="e3197-936">W tym scenariuszu używanych w tym artykule firma Microsoft nie dodał zwiększają ochronę dla systemu DBMS.</span><span class="sxs-lookup"><span data-stu-id="e3197-936">In the scenario we use in this article, we didn't add more protection to the DBMS.</span></span>

<span data-ttu-id="e3197-937">Istnieją specjalne uwagi dotyczące różnych usług systemu DBMS interakcji z tego rodzaju konfiguracji klastra SAP ASCS/SCS na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e3197-937">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e3197-938">Procedury instalacji programu SAP NetWeaver ABAP systemów, Java i systemami ABAP + Java są prawie takie same.</span><span class="sxs-lookup"><span data-stu-id="e3197-938">The installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="e3197-939">Najbardziej znacząca różnica jest systemu SAP ABAP jedno wystąpienie ASCS.</span><span class="sxs-lookup"><span data-stu-id="e3197-939">The most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="e3197-940">Systemu SAP Java ma jedno wystąpienie SCS.</span><span class="sxs-lookup"><span data-stu-id="e3197-940">The SAP Java system has one SCS instance.</span></span> <span data-ttu-id="e3197-941">Systemu SAP ABAP + Java ma jedno wystąpienie ASCS i jedno wystąpienie SCS uruchomiony w tej samej grupie klastra trybu failover firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e3197-941">The SAP ABAP+Java system has one ASCS instance and one SCS instance running in the same Microsoft failover cluster group.</span></span> <span data-ttu-id="e3197-942">Różnice instalacji dla każdej stosu instalacji SAP NetWeaver jawnie wymienione.</span><span class="sxs-lookup"><span data-stu-id="e3197-942">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="e3197-943">Można założyć, że wszystkie inne elementy są takie same.</span><span class="sxs-lookup"><span data-stu-id="e3197-943">You can assume that all other parts are the same.</span></span>  
>
>

### <span data-ttu-id="e3197-944"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a>Instalowanie programu SAP przy użyciu wystąpienia ASCS/SCS wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="e3197-944"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3197-945">Pamiętaj, aby nie umieszczenia pliku stronicowania na DataKeeper dublowanych woluminów.</span><span class="sxs-lookup"><span data-stu-id="e3197-945">Be sure not to place your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="e3197-946">DataKeeper nie obsługuje woluminy dublowane.</span><span class="sxs-lookup"><span data-stu-id="e3197-946">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="e3197-947">Możesz pozostawić pliku stronicowania na dysku tymczasowym D maszyny wirtualnej platformy Azure, co jest ustawieniem domyślnym.</span><span class="sxs-lookup"><span data-stu-id="e3197-947">You can leave your page file on the temporary drive D of an Azure virtual machine, which is the default.</span></span> <span data-ttu-id="e3197-948">Jeśli nie jest już istnieje, należy przenieść plik stronicowania systemu Windows na dysk D: Azure maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3197-948">If it's not already there, move the Windows page file to drive D: of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="e3197-949">Instalowanie SAP przy użyciu wystąpienia ASCS/SCS wysokiej dostępności obejmuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="e3197-949">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="e3197-950">Tworzenie nazwę hosta wirtualnego wystąpienia klastra programu SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-950">Creating a virtual host name for the clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="e3197-951">Instalowanie programu SAP pierwszym węźle klastra</span><span class="sxs-lookup"><span data-stu-id="e3197-951">Installing the SAP first cluster node</span></span>
- <span data-ttu-id="e3197-952">Modyfikowanie profilu SAP wystąpienia ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-952">Modifying the SAP profile of the ASCS/SCS instance</span></span>
- <span data-ttu-id="e3197-953">Dodawanie portu sondy</span><span class="sxs-lookup"><span data-stu-id="e3197-953">Adding a probe port</span></span>
- <span data-ttu-id="e3197-954">Otwarcie portu sondowania zapory systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e3197-954">Opening the Windows firewall probe port</span></span>

#### <span data-ttu-id="e3197-955"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Utwórz nazwę hosta wirtualnego wystąpienia klastra programu SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-955"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for the clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="e3197-956">W Menedżerze DNS z systemem Windows utwórz wpis DNS dla nazwy hostów wirtualnych ASCS/SCS wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="e3197-956">In the Windows DNS manager, create a DNS entry for the virtual host name of the ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e3197-957">Adres IP, który można przypisać nazwę hosta wirtualnego wystąpienia ASCS/SCS musi być taka sama jak adres IP, który został przypisany do usługi równoważenia obciążenia Azure (**<*SID*> - lb - ascs **).</span><span class="sxs-lookup"><span data-stu-id="e3197-957">The IP address that you assign to the virtual host name of the ASCS/SCS instance must be the same as the IP address that you assigned to Azure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="e3197-958">Adres IP nazwę hosta wirtualnego SAP ASCS/SCS (**pr1 ascs sap**) jest taka sama jak adres IP usługi równoważenia obciążenia Azure (**pr1-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="e3197-958">The IP address of the virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is the same as the IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Rysunek 56: Definiowanie wpis DNS dla nazwy wirtualnego klastra SAP ASCS/SCS i adres TCP/IP][sap-ha-guide-figure-3046]

  <span data-ttu-id="e3197-960">_**Rysunek 56:** zdefiniować wpis DNS dla nazwy wirtualnego klastra SAP ASCS/SCS i adres TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="e3197-960">_**Figure 56:** Define the DNS entry for the SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="e3197-961">Aby zdefiniować adres IP przypisany do nazwy hostów wirtualnych, wybierz **Menedżera DNS** > **domeny**.</span><span class="sxs-lookup"><span data-stu-id="e3197-961">To define the IP address assigned to the virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![57 rysunek: Nowa nazwa wirtualnego i adres TCP/IP dla konfiguracji klastra SAP ASCS/SCS][sap-ha-guide-figure-3047]

  <span data-ttu-id="e3197-963">_**Rysunek 57:** nową nazwę wirtualnego i TCP/IP adresów dla SAP ASCS/SCS konfiguracji klastra_</span><span class="sxs-lookup"><span data-stu-id="e3197-963">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="e3197-964"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Zainstaluj na pierwszym węźle klastra SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-964"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install the SAP first cluster node</span></span>

1.  <span data-ttu-id="e3197-965">Wykonanie pierwszej opcji węzła klastra w węźle klastra A. Na przykład na **pr1 ascs 0** hosta.</span><span class="sxs-lookup"><span data-stu-id="e3197-965">Execute the first cluster node option on cluster node A. For example, on the **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="e3197-966">Zachowaj ustawienie domyślne portów dla usługi równoważenia obciążenia wewnętrznego platformy Azure, wybierz:</span><span class="sxs-lookup"><span data-stu-id="e3197-966">To keep the default ports for the Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="e3197-967">**ABAP system**: **ASCS** wystąpienie numer **00**</span><span class="sxs-lookup"><span data-stu-id="e3197-967">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="e3197-968">**Java system**: **SCS** wystąpienie numer **01**</span><span class="sxs-lookup"><span data-stu-id="e3197-968">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="e3197-969">**System ABAP + Java**: **ASCS** wystąpienie numer **00** i **SCS** wystąpienie numer **01**</span><span class="sxs-lookup"><span data-stu-id="e3197-969">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="e3197-970">Aby użyć wystąpienia liczb innych niż 00 dla wystąpienia ABAP ASCS i 01 dla wystąpienia Java SCS, najpierw należy zmienić reguły, opisane w równoważenia obciążenia domyślne usługi równoważenia obciążenia wewnętrznego Azure [Zmień zasady dla usługi równoważenia obciążenia Azure wewnętrzny równoważenia obciążenia domyślne ASCS/SCS][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="e3197-970">To use instance numbers other than 00 for the ABAP ASCS instance and 01 for the Java SCS instance, first you need to change the Azure internal load balancer default load balancing rules, described in [Change the ASCS/SCS default load balancing rules for the Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="e3197-971">Następny kilka zadań nie są opisane w standardowe dokumentacji instalacji SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-971">The next few tasks aren't described in the standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="e3197-972">Dokumentacja instalacji programu SAP opisuje sposób instalowania pierwszego węzła klastra ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="e3197-972">The SAP installation documentation describes how to install the first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="e3197-973"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modyfikowanie profilu SAP wystąpienia ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-973"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify the SAP profile of the ASCS/SCS instance</span></span>

<span data-ttu-id="e3197-974">Należy dodać nowy parametr profilu.</span><span class="sxs-lookup"><span data-stu-id="e3197-974">You need to add a new profile parameter.</span></span> <span data-ttu-id="e3197-975">Parametr profilu zapobiega połączeń między procesów roboczych SAP i umieścić w kolejce zamykania po okresie bezczynności wynoszącym zbyt długo.</span><span class="sxs-lookup"><span data-stu-id="e3197-975">The profile parameter prevents connections between SAP work processes and the enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="e3197-976">Wspomniano scenariusz problemu w [dodać wpisów rejestru na obu węzłach klastra z wystąpieniem SAP ASCS/SCS][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="e3197-976">We mentioned the problem scenario in [Add registry entries on both cluster nodes of the SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="e3197-977">W tej sekcji również wprowadzono dwie zmiany do niektórych podstawowych parametrów połączenia TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="e3197-977">In that section, we also introduced two changes to some basic TCP/IP connection parameters.</span></span> <span data-ttu-id="e3197-978">W drugim kroku, należy określić serwer umieścić w kolejce do wysłania `keep_alive` sygnału, dzięki czemu połączeń nie osiągnął Próg bezczynności Azure wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e3197-978">In a second step, you need to set the enqueue server to send a `keep_alive` signal so that the connections don't hit the Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="e3197-979">Aby zmodyfikować profil SAP wystąpienia ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="e3197-979">To modify the SAP profile of the ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="e3197-980">Dodaj parametr ten profil, do profilu wystąpienia SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="e3197-980">Add this profile parameter to the SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="e3197-981">W naszym przykładzie ścieżka jest:</span><span class="sxs-lookup"><span data-stu-id="e3197-981">In our example, the path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="e3197-982">Na przykład do profilu wystąpienia SAP SCS i odpowiednie ścieżki:</span><span class="sxs-lookup"><span data-stu-id="e3197-982">For example, to the SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="e3197-983">Aby zastosować zmiany, ponownie uruchom wystąpienie /SCS SAP ASCS.</span><span class="sxs-lookup"><span data-stu-id="e3197-983">To apply the changes, restart the SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="e3197-984"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a>Dodaj port sondy</span><span class="sxs-lookup"><span data-stu-id="e3197-984"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="e3197-985">Funkcja równoważenia obciążenia wewnętrznego sondy do pracy z usługą równoważenia obciążenia w Azure konfigurację całego klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-985">Use the internal load balancer's probe functionality to make the entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="e3197-986">Azure wewnętrznego modułu równoważenia obciążenia zwykle rozdziela przychodzące obciążenie równomiernie w poszczególnych uczestniczących maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e3197-986">The Azure internal load balancer usually distributes the incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="e3197-987">Jednak to nie będzie działać w niektórych konfiguracjach klastra, ponieważ jest aktywna tylko jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="e3197-987">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="e3197-988">Inne wystąpienie jest w stanie pasywnym i nie akceptuje dowolne obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e3197-988">The other instance is passive and can’t accept any of the workload.</span></span> <span data-ttu-id="e3197-989">Funkcja badania pomaga Azure wewnętrznego modułu równoważenia obciążenia przypisuje pracy tylko do aktywnego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="e3197-989">A probe functionality helps when the Azure internal load balancer assigns work only to an active instance.</span></span> <span data-ttu-id="e3197-990">Z funkcją sondowania wewnętrznego modułu równoważenia obciążenia może wykryć, które wystąpienia są aktywne, a następnie ograniczyć tylko wystąpienia o obciążenie.</span><span class="sxs-lookup"><span data-stu-id="e3197-990">With the probe functionality, the internal load balancer can detect which instances are active, and then target only the instance with the workload.</span></span>

<span data-ttu-id="e3197-991">Aby dodać port sondy:</span><span class="sxs-lookup"><span data-stu-id="e3197-991">To add a probe port:</span></span>

1.  <span data-ttu-id="e3197-992">Sprawdź bieżący **ProbePort** ustawienie za pomocą następującego polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3197-992">Check the current **ProbePort** setting by running the following PowerShell command.</span></span> <span data-ttu-id="e3197-993">Wykonanie go z jednej maszyny wirtualnej w konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-993">Execute it from within one of the virtual machines in the cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="e3197-994">Zdefiniuj port sondy.</span><span class="sxs-lookup"><span data-stu-id="e3197-994">Define a probe port.</span></span> <span data-ttu-id="e3197-995">Domyślny numer portu sondowania to **0**.</span><span class="sxs-lookup"><span data-stu-id="e3197-995">The default probe port number is **0**.</span></span> <span data-ttu-id="e3197-996">W tym przykładzie używamy port sondy **62000**.</span><span class="sxs-lookup"><span data-stu-id="e3197-996">In our example, we use probe port **62000**.</span></span>

  ![Rysunek 58: Port sondy konfiguracji klastra jest równa 0, domyślnie][sap-ha-guide-figure-3048]

  <span data-ttu-id="e3197-998">_**Rysunek 58:** domyślny port sondy konfiguracji klastra jest równa 0_</span><span class="sxs-lookup"><span data-stu-id="e3197-998">_**Figure 58:** The default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="e3197-999">Numer portu jest zdefiniowany w szablonach SAP usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e3197-999">The port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="e3197-1000">Można przypisać numer portu w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3197-1000">You can assign the port number in PowerShell.</span></span>

  <span data-ttu-id="e3197-1001">Aby ustawić nową wartość ProbePort  **SAP <*SID*> IP ** zasobu klastra, uruchom następujący skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3197-1001">To set a new ProbePort value for the **SAP <*SID*> IP** cluster resource, run the following PowerShell script.</span></span> <span data-ttu-id="e3197-1002">Zaktualizuj zmienne środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3197-1002">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="e3197-1003">Po uruchomieniu skryptu, zostanie wyświetlony monit o ponowne uruchomienie Grupa klastra SAP do aktywowania zmian.</span><span class="sxs-lookup"><span data-stu-id="e3197-1003">After the script runs, you'll be prompted to restart the SAP cluster group to activate the changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of the SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting the new probe port property of the SAP cluster resource '$SAPIPresourceName' to '$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want to take restart SAP cluster role '$SAPClusterRoleName', to activate the changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  <span data-ttu-id="e3197-1004">Po przełączeniu  **SAP <*SID*> ** klastra roli w tryb online, upewnij się, że **ProbePort** jest ustawiona na nową wartość.</span><span class="sxs-lookup"><span data-stu-id="e3197-1004">After you bring the **SAP <*SID*>** cluster role online, verify that **ProbePort** is set to the new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Rysunek 59: Sondowania portu klastra po zainstalowaniu nowej wartości][sap-ha-guide-figure-3049]

  <span data-ttu-id="e3197-1006">_**Rysunek 59:** sondowania portu klastra po zainstalowaniu nowej wartości_</span><span class="sxs-lookup"><span data-stu-id="e3197-1006">_**Figure 59:** Probe the cluster port after you set the new value_</span></span>

#### <span data-ttu-id="e3197-1007"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Otwórz port sondy zapory systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e3197-1007"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open the Windows firewall probe port</span></span>

<span data-ttu-id="e3197-1008">Należy otworzyć port sondy zapory systemu Windows na obu węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-1008">You need to open a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="e3197-1009">Użyj następującego skryptu, aby otworzyć port sondy zapory systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="e3197-1009">Use the following script to open a Windows firewall probe port.</span></span> <span data-ttu-id="e3197-1010">Zaktualizuj zmienne środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3197-1010">Update the PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="e3197-1011">**ProbePort** ustawiono **62000**.</span><span class="sxs-lookup"><span data-stu-id="e3197-1011">The **ProbePort** is set to **62000**.</span></span> <span data-ttu-id="e3197-1012">Teraz można uzyskać dostępu do udziału plików  **\\\ascsha-clsap\sapmnt** od innych hostów, takie jak z **ascsha dbas**.</span><span class="sxs-lookup"><span data-stu-id="e3197-1012">Now you can access the file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="e3197-1013"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Zainstaluj wystąpienie bazy danych</span><span class="sxs-lookup"><span data-stu-id="e3197-1013"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install the database instance</span></span>

<span data-ttu-id="e3197-1014">Aby zainstalować wystąpienie bazy danych, wykonaj proces opisany w dokumentacji instalacji SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-1014">To install the database instance, follow the process described in the SAP installation documentation.</span></span>

### <span data-ttu-id="e3197-1015"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Zainstaluj drugiego węzła klastra</span><span class="sxs-lookup"><span data-stu-id="e3197-1015"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install the second cluster node</span></span>

<span data-ttu-id="e3197-1016">Aby zainstalować drugi klaster, wykonaj czynności opisane w przewodniku instalacji SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-1016">To install the second cluster, follow the steps in the SAP installation guide.</span></span>

### <span data-ttu-id="e3197-1017"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Zmień typ uruchomienia wystąpienia usługi Windows Wywołujących SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-1017"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change the start type of the SAP ERS Windows service instance</span></span>

<span data-ttu-id="e3197-1018">Zmień typ uruchomienia usługi systemu Windows Wywołujących SAP **automatycznie (opóźnione uruchomienie)** na obu węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="e3197-1018">Change the start type of the SAP ERS Windows service to **Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Rysunek 60: Zmień typ usługi dla wystąpienia Wywołujących SAP do opóźnionego automatycznego][sap-ha-guide-figure-3050]

<span data-ttu-id="e3197-1020">_**Rysunek 60:** Zmień typ usługi wystąpienie Wywołujących SAP do opóźnionego automatycznego_</span><span class="sxs-lookup"><span data-stu-id="e3197-1020">_**Figure 60:** Change the service type for the SAP ERS instance to delayed automatic_</span></span>

### <span data-ttu-id="e3197-1021"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Zainstaluj serwer aplikacji głównej SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-1021"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install the SAP Primary Application Server</span></span>

<span data-ttu-id="e3197-1022">Zainstaluj wystąpienie serwera aplikacji głównej (adresy) <*SID*> - podpisane - 0 na maszynie wirtualnej, który został wybrany do obsługi adresy dostawcy.</span><span class="sxs-lookup"><span data-stu-id="e3197-1022">Install the Primary Application Server (PAS) instance <*SID*>-di-0 on the virtual machine that you've designated to host the PAS.</span></span> <span data-ttu-id="e3197-1023">Nie ma żadnych zależności, Azure lub DataKeeper określonych ustawień.</span><span class="sxs-lookup"><span data-stu-id="e3197-1023">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="e3197-1024"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Instalowanie serwera aplikacji dodatkowe SAP</span><span class="sxs-lookup"><span data-stu-id="e3197-1024"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install the SAP Additional Application Server</span></span>

<span data-ttu-id="e3197-1025">Zainstaluj SAP dodatkowych aplikacji serwera (AAS) na wszystkich maszynach wirtualnych, które zostały wyznaczone do obsługi wystąpienia serwera aplikacji SAP.</span><span class="sxs-lookup"><span data-stu-id="e3197-1025">Install an SAP Additional Application Server (AAS) on all the virtual machines that you've designated to host an SAP Application Server instance.</span></span> <span data-ttu-id="e3197-1026">Na przykład na <*SID*> - podpisane - 1 do <*SID*> - podpisane -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="e3197-1026">For example, on <*SID*>-di-1 to <*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="e3197-1027">Zakończy się instalacja systemu SAP NetWeaver wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="e3197-1027">This finishes the installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="e3197-1028">Następnie należy kontynuować testowanie trybu failover.</span><span class="sxs-lookup"><span data-stu-id="e3197-1028">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="e3197-1029"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Testowanie trybu failover wystąpienia programu SAP ASCS/SCS i SIOS replikacji</span><span class="sxs-lookup"><span data-stu-id="e3197-1029"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test the SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="e3197-1030">Jest łatwy do testowania i monitorowania za pomocą narzędzia Menedżera klastra trybu Failover oraz zarządzania DataKeeper SIOS i konfiguracji trybu failover wystąpienia programu SAP ASCS/SCS i SIOS replikacji dysku.</span><span class="sxs-lookup"><span data-stu-id="e3197-1030">It's easy to test and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and the SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="e3197-1031"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a>W węźle klastra, A jest uruchomione wystąpienie SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="e3197-1031"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="e3197-1032">**SAP PR1** grupy klastra jest uruchomiona w węźle klastra A. Na przykład na **pr1 ascs 0**.</span><span class="sxs-lookup"><span data-stu-id="e3197-1032">The **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="e3197-1033">Przypisywanie udostępnionego dysku S, który jest częścią programu **SAP PR1** Grupa klastra, i używający wystąpienia ASCS/SCS, do klastra z węzła A.</span><span class="sxs-lookup"><span data-stu-id="e3197-1033">Assign the shared disk drive S, which is part of the **SAP PR1** cluster group, and which the ASCS/SCS instance uses, to cluster node A.</span></span>

![61 rysunek: Menedżer klastra trybu Failover: SAP < SID > grupy klastra jest uruchomiona w węźle klastra, A][sap-ha-guide-figure-5000]

<span data-ttu-id="e3197-1035">_**Rysunek 61:** Menedżera klastra trybu Failover: SAP <*SID*> grupy klastra jest uruchomiona w węźle klastra, A_</span><span class="sxs-lookup"><span data-stu-id="e3197-1035">_**Figure 61:** Failover Cluster Manager: The SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="e3197-1036">W narzędziu Zarządzanie DataKeeper SIOS i jego konfiguracja widać, że udostępniony dysk synchronicznie replikacji danych z dysku woluminu źródłowego S w węźle klastra, A na dysku woluminu docelowego S w węźle klastra B. Na przykład są replikowane z **pr1 ascs 0 [10.0.0.40]** do **pr1 ascs 1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="e3197-1036">In the SIOS DataKeeper Management and Configuration tool, you can see that the shared disk data is synchronously replicated from the source volume drive S on cluster node A to the target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** to **pr1-ascs-1 [10.0.0.41]**.</span></span>

![Rysunek 62: W SIOS DataKeeper replikowane lokalnym woluminie z węzła klastra, A do węzła klastra B][sap-ha-guide-figure-5001]

<span data-ttu-id="e3197-1038">_**Rysunek 62:** w SIOS DataKeeper replikowane lokalnym woluminie z węzła klastra, A do węzła klastra B_</span><span class="sxs-lookup"><span data-stu-id="e3197-1038">_**Figure 62:** In SIOS DataKeeper, replicate the local volume from cluster node A to cluster node B_</span></span>

### <span data-ttu-id="e3197-1039"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Tryb failover z węzła A węzła B</span><span class="sxs-lookup"><span data-stu-id="e3197-1039"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A to node B</span></span>

1.  <span data-ttu-id="e3197-1040">Wybierz jedną z tych opcji, aby zainicjować trybu failover SAP <*SID*> Grupa klastra z węzła klastra, A do węzła klastra B:</span><span class="sxs-lookup"><span data-stu-id="e3197-1040">Choose one of these options to initiate a failover of the SAP <*SID*> cluster group from cluster node A to cluster node B:</span></span>
  - <span data-ttu-id="e3197-1041">Menedżer klastra trybu Failover</span><span class="sxs-lookup"><span data-stu-id="e3197-1041">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="e3197-1042">Za pomocą programu PowerShell klastra trybu Failover</span><span class="sxs-lookup"><span data-stu-id="e3197-1042">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="e3197-1043">Uruchom ponownie, A węzeł klastra w ramach systemu operacyjnego gościa (powoduje to zainicjowanie automatycznej pracy awaryjnej SAP <*identyfikatora SID*> Grupa klastra z węzła A do węzła B).</span><span class="sxs-lookup"><span data-stu-id="e3197-1043">Restart cluster node A within the Windows guest operating system (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
3.  <span data-ttu-id="e3197-1044">Uruchom ponownie, A węzeł klastra przy użyciu portalu Azure (powoduje to zainicjowanie automatycznej pracy awaryjnej SAP <*identyfikatora SID*> Grupa klastra z węzła A do węzła B).</span><span class="sxs-lookup"><span data-stu-id="e3197-1044">Restart cluster node A from the Azure portal (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
4.  <span data-ttu-id="e3197-1045">Uruchom ponownie A węzła klastra za pomocą programu Azure PowerShell (powoduje to zainicjowanie automatycznej pracy awaryjnej SAP <*identyfikatora SID*> Grupa klastra z węzła A do węzła B).</span><span class="sxs-lookup"><span data-stu-id="e3197-1045">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>

  <span data-ttu-id="e3197-1046">Po przejściu w tryb failover, SAP <*SID*> grupy klastra jest uruchomiona w węźle klastra B. Na przykład, że jest uruchomiona w **pr1 ascs 1**.</span><span class="sxs-lookup"><span data-stu-id="e3197-1046">After failover, the SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Rysunek 63: W Menedżerze klastra trybu Failover SAP < SID > grupy klastra jest uruchomiona w węźle klastra B][sap-ha-guide-figure-5002]

  <span data-ttu-id="e3197-1048">_**Rysunek 63**: W Menedżerze klastra trybu Failover, SAP <*SID*> grupy klastra jest uruchomiona w węźle klastra B_</span><span class="sxs-lookup"><span data-stu-id="e3197-1048">_**Figure 63**: In Failover Cluster Manager, the SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="e3197-1049">Udostępniony dysk jest teraz zainstalowany w klastrze węzła B. SIOS DataKeeper jest replikowanie danych z dysku woluminu źródłowego S w węźle klastra B na dysku woluminu docelowego S w węźle klastra A. Na przykład jest replikowany z **pr1 ascs 1 [10.0.0.41]** do **pr1 ascs 0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="e3197-1049">The shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B to target volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** to **pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Rysunek 64: SIOS DataKeeper replikuje lokalnym woluminie z węzła klastra B do A węzła klastra][sap-ha-guide-figure-5003]

  <span data-ttu-id="e3197-1051">_**Rysunek 64:** SIOS DataKeeper replikuje lokalnym woluminie z węzła klastra B do A węzła klastra_</span><span class="sxs-lookup"><span data-stu-id="e3197-1051">_**Figure 64:** SIOS DataKeeper replicates the local volume from cluster node B to cluster node A_</span></span>
