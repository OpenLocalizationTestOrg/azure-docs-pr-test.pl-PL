---
title: "Maszyny wirtualne wysokiej dostępności dla programu SAP NetWeaver aaaAzure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a><span data-ttu-id="afbe1-103">Azure maszyn wirtualnych wysokiej dostępności dla programu SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="afbe1-103">Azure Virtual Machines high availability for SAP NetWeaver</span></span>

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

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



<span data-ttu-id="afbe1-109">Maszyny wirtualne platformy Azure jest hello rozwiązania dla organizacji, które muszą obliczeniowych, magazynu i zasobów sieciowych w czasie minimalnego i bez cykle nabywania długie.</span><span class="sxs-lookup"><span data-stu-id="afbe1-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="afbe1-110">Możesz użyć aplikacji klasycznej toodeploy maszyn wirtualnych platformy Azure, takich jak ABAP na podstawie SAP NetWeaver, Java i stosu ABAP + Java.</span><span class="sxs-lookup"><span data-stu-id="afbe1-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="afbe1-111">Rozszerzenie, niezawodności i dostępności bez dodatkowych lokalnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="afbe1-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="afbe1-112">Maszyny wirtualne platformy Azure obsługuje łączności między lokalizacjami, maszynach wirtualnych platformy Azure można zintegrować lokalnej domeny Twojej organizacji, chmur prywatnych i pozioma systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="afbe1-113">W tym artykule opisano firma Microsoft hello czy możesz zrobić toodeploy systemów SAP wysokiej dostępności na platformie Azure przy użyciu modelu wdrażania usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="afbe1-114">Firma Microsoft przeprowadzi użytkownika przez proces te zadania główne:</span><span class="sxs-lookup"><span data-stu-id="afbe1-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="afbe1-115">Znajdź hello prawo przewodniki SAP uwagi i instalacji na liście hello [zasobów] [ sap-ha-guide-2] sekcji.</span><span class="sxs-lookup"><span data-stu-id="afbe1-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="afbe1-116">W tym artykule uzupełnia SAP instalacji dokumentacji i notatek SAP, które są hello głównej zasobów, które ułatwiają instalowanie i wdrażanie oprogramowania SAP na określonych platformach.</span><span class="sxs-lookup"><span data-stu-id="afbe1-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="afbe1-117">Dowiedz się hello różnice między modelu wdrażania usługi Azure Resource Manager hello i hello Azure klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="afbe1-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="afbe1-118">Więcej informacji na temat trybów kworum klastra trybu Failover systemu Windows Server, w którym można wybrać hello modelu, które jest odpowiednie dla danego wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="afbe1-119">Więcej informacji na temat systemu Windows Server Failover Clustering udostępnionego magazynu w usług Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="afbe1-120">Dowiedz się, jak toohelp chronić pojedynczego punktu z awarii składników jak zaawansowane biznesowych aplikacji programowania (ABAP) SAP centralnej usług (ASCS) / SAP centralnej usługi (SCS) i systemy zarządzania bazami danych (DBMS) i działanie elementów nadmiarowych, takie jak SAP Serwer aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="afbe1-121">Wykonaj krok przykład instalację i konfigurację systemu SAP wysokiej dostępności w klastrze systemu Windows Server Failover Clustering na platformie Azure przy użyciu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="afbe1-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="afbe1-122">Więcej informacji na temat toouse wymagane dodatkowe kroki, Windows Server Failover Clustering na platformie Azure, ale nie są wymagane w przypadku lokalnego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="afbe1-123">toosimplify wdrażania i konfiguracji, w tym artykule używamy hello szablony Menedżera zasobów systemu SAP trójwarstwowa wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="afbe1-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="afbe1-124">Szablony Hello zautomatyzować wdrożenie całej infrastruktury hello potrzebnym do systemu SAP wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="afbe1-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="afbe1-125">Infrastruktura Hello obsługuje również rozmiaru SAP aplikacji wydajności standardowe (protokoły SAP) systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="afbe1-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="afbe1-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="afbe1-127">Przed rozpoczęciem upewnij się, że spełniają wymagania wstępne dotyczące hello, które zostały opisane w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="afbe1-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="afbe1-128">Można również, czy toocheck wszystkich zasobów wymienionych w hello [zasobów] [ sap-ha-guide-2] sekcji.</span><span class="sxs-lookup"><span data-stu-id="afbe1-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="afbe1-129">W tym artykule używamy szablonów usługi Azure Resource Manager dla [trójwarstwowa SAP NetWeaver za pomocą dysków zarządzanych](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span><span class="sxs-lookup"><span data-stu-id="afbe1-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span></span> <span data-ttu-id="afbe1-130">Przydatne Omówienie szablonów, zobacz [szablony Menedżera zasobów Azure SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span><span class="sxs-lookup"><span data-stu-id="afbe1-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="afbe1-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a>Zasoby</span><span class="sxs-lookup"><span data-stu-id="afbe1-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="afbe1-132">Artykuły te obejmują wdrożenia SAP na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="afbe1-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="afbe1-133">[Azure maszyn wirtualnych, planowania i wdrażania dla programu SAP NetWeaver][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="afbe1-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="afbe1-134">[Maszyny wirtualne Azure wdrożenia SAP NetWeaver][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="afbe1-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="afbe1-135">[Azure wdrożenia SAP NetWeaver DBMS maszyny wirtualne][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="afbe1-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="afbe1-136">[Azure maszyn wirtualnych wysokiej dostępności dla programu SAP NetWeaver (w tym przewodniku)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="afbe1-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="afbe1-137">Jeśli to możliwe, możemy zapewniają toohello łącza, odwoływanie SAP w podręczniku instalacji (zobacz hello [Przewodnik po instalacji programu SAP][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="afbe1-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="afbe1-138">Wymagania wstępne i informacje o hello proces instalacji, to jest instalację dobrze tooread hello SAP NetWeaver prowadzi dokładnie.</span><span class="sxs-lookup"><span data-stu-id="afbe1-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="afbe1-139">W tym artykule opisano tylko określone zadania dla systemów opartych na procesorze SAP NetWeaver, których można użyć z maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="afbe1-140">Te informacje SAP są powiązane toohello tematu SAP na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="afbe1-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="afbe1-141">Numer</span><span class="sxs-lookup"><span data-stu-id="afbe1-141">Note number</span></span> | <span data-ttu-id="afbe1-142">Tytuł</span><span class="sxs-lookup"><span data-stu-id="afbe1-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="afbe1-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="afbe1-143">[1928533]</span></span> |<span data-ttu-id="afbe1-144">Aplikacje SAP na platformie Azure: obsługiwane produktów i zmiana rozmiaru</span><span class="sxs-lookup"><span data-stu-id="afbe1-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="afbe1-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="afbe1-145">[2015553]</span></span> |<span data-ttu-id="afbe1-146">SAP na platformie Microsoft Azure: obsługuje wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="afbe1-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="afbe1-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="afbe1-147">[1999351]</span></span> |<span data-ttu-id="afbe1-148">Rozszerzone monitorowanie Azure dla programu SAP</span><span class="sxs-lookup"><span data-stu-id="afbe1-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="afbe1-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="afbe1-149">[2178632]</span></span> |<span data-ttu-id="afbe1-150">Klucz monitorowania metryki dla SAP na platformie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="afbe1-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="afbe1-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="afbe1-151">[1999351]</span></span> |<span data-ttu-id="afbe1-152">Wirtualizacji w systemie Windows: rozszerzonego monitorowania</span><span class="sxs-lookup"><span data-stu-id="afbe1-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="afbe1-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="afbe1-153">[2243692]</span></span> |<span data-ttu-id="afbe1-154">Użycie magazynu SSD Azure — wersja Premium dla wystąpienia systemu DBMS SAP</span><span class="sxs-lookup"><span data-stu-id="afbe1-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="afbe1-155">Dowiedz się więcej o hello [ograniczenia subskrypcji platformy Azure][azure-subscription-service-limits-subscription], w tym domyślne ogólne ograniczenia i ograniczenia maksymalnej.</span><span class="sxs-lookup"><span data-stu-id="afbe1-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="afbe1-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP wysokiej dostępności z usługi Azure Resource Manager a hello Azure klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="afbe1-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="afbe1-157">Hello Azure Resource Manager i usługi Azure klasycznych modeli wdrażania są inne hello w następujących obszarach:</span><span class="sxs-lookup"><span data-stu-id="afbe1-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="afbe1-158">Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="afbe1-158">Resource groups</span></span>
- <span data-ttu-id="afbe1-159">Azure wewnętrzny załadować równoważenia zależności na powitania grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="afbe1-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="afbe1-160">Obsługa scenariuszy identyfikatora SID multi SAP</span><span class="sxs-lookup"><span data-stu-id="afbe1-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="afbe1-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a>Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="afbe1-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="afbe1-162">W systemie Azure Resource Manager służy toomanage grup zasobów wszystkie zasoby aplikacji hello w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="afbe1-163">Witaj ma podejście, w grupie zasobów, wszystkie zasoby tego samego cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="afbe1-164">Na przykład wszystkie zasoby są tworzone w hello sam czas i są usuwane przy hello tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="afbe1-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="afbe1-165">Dowiedz się więcej o [grupach zasobów](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="afbe1-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="afbe1-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure wewnętrzny załadować równoważenia zależności na powitania grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="afbe1-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="afbe1-167">W hello Azure klasycznego modelu wdrażania istnieje zależność między hello Azure wewnętrznego modułu równoważenia obciążenia (usługa Azure Load Balancer) i usługi w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service.</span></span> <span data-ttu-id="afbe1-168">Co wewnętrzny moduł równoważenia obciążenia musi jedną usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="afbe1-168">Every internal load balancer needs one cloud service.</span></span>

<span data-ttu-id="afbe1-169">W usłudze Azure Resource Manager, co zasobów platformy Azure musi toobe umieszczane grupy zasobów platformy Azure i jest nieprawidłowa dla usługi równoważenia obciążenia Azure również.</span><span class="sxs-lookup"><span data-stu-id="afbe1-169">In Azure Resource Manager, every Azure resource needs toobe placed into an Azure resource group, and this is valid for Azure Load Balancer as well.</span></span> <span data-ttu-id="afbe1-170">Jednak brak nie potrzeby toohave jednej Azure grupy zasobów dla usługi równoważenia obciążenia Azure, np. jedna grupa zasobów platformy Azure może zawierać wiele Azure usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-170">However, there is no need toohave one Azure resource group per Azure load balancer, e.g. one Azure resource group can contain multiple Azure Load Balancers.</span></span> <span data-ttu-id="afbe1-171">środowisko Hello jest prostszy i bardziej elastyczne.</span><span class="sxs-lookup"><span data-stu-id="afbe1-171">hello environment is simpler and more flexible.</span></span> 

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="afbe1-172">Obsługa scenariuszy identyfikatora SID multi SAP</span><span class="sxs-lookup"><span data-stu-id="afbe1-172">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="afbe1-173">W systemie Azure Resource Manager można zainstalować wielu SAP identyfikator ASCS/SCS wystąpień systemu w jednym klastrze.</span><span class="sxs-lookup"><span data-stu-id="afbe1-173">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="afbe1-174">Identyfikator SID wielu wystąpień jest możliwe dzięki obsłudze wielu adresów IP dla każdego Azure wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-174">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="afbe1-175">toouse hello Azure klasycznego modelu wdrażania, wykonaj procedury hello opisane w temacie [SAP NetWeaver na platformie Azure: wystąpień klastrowania SAP ASCS/SCS przy użyciu klastra trybu Failover systemu Windows Server na platformie Azure z SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span><span class="sxs-lookup"><span data-stu-id="afbe1-175">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afbe1-176">Zdecydowanie zaleca się użycie modelu wdrażania usługi Azure Resource Manager powitania dla instalacji programu SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-176">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="afbe1-177">Oferuje wiele korzyści, które nie są dostępne w hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="afbe1-177">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="afbe1-178">Dowiedz się więcej o usłudze Azure [modele wdrażania][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span><span class="sxs-lookup"><span data-stu-id="afbe1-178">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="afbe1-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a>Klaster trybu Failover serwera systemu Windows</span><span class="sxs-lookup"><span data-stu-id="afbe1-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="afbe1-180">Windows Server Failover Clustering jest foundation hello instalacji SAP ASCS/SCS wysokiej dostępności i bazami danych w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="afbe1-180">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="afbe1-181">Klaster trybu failover to grupa 1 + n niezależnych serwerów (węzłów), które współpracują ze sobą tooincrease hello dostępności aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="afbe1-181">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="afbe1-182">W przypadku awarii węzła usługi Windows Server Failover Clustering oblicza hello liczbę błędów, które mogą wystąpić przy zachowaniu dobrej kondycji klastra tooprovide aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="afbe1-182">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="afbe1-183">Można wybrać z kworum różne tryby tooachieve awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="afbe1-183">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="afbe1-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a>Tryb kworum</span><span class="sxs-lookup"><span data-stu-id="afbe1-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="afbe1-185">Korzystając z usługi Windows Server Failover Clustering można wybrać z czterech trybów kworum:</span><span class="sxs-lookup"><span data-stu-id="afbe1-185">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="afbe1-186">**Większość węzłów**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-186">**Node Majority**.</span></span> <span data-ttu-id="afbe1-187">Każdy węzeł klastra hello głosować.</span><span class="sxs-lookup"><span data-stu-id="afbe1-187">Each node of hello cluster can vote.</span></span> <span data-ttu-id="afbe1-188">funkcje klastra Hello tylko z większością głosów, czyli z więcej niż połowy hello głosów.</span><span class="sxs-lookup"><span data-stu-id="afbe1-188">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="afbe1-189">Firma Microsoft zaleca tej opcji w przypadku klastrów nieparzysta liczba węzłów.</span><span class="sxs-lookup"><span data-stu-id="afbe1-189">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="afbe1-190">Na przykład trzech węzłów w klastrze siedem może zakończyć się niepowodzeniem, a aparaturze klastra hello osiąga większości i kontynuuje toorun.</span><span class="sxs-lookup"><span data-stu-id="afbe1-190">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="afbe1-191">**Większość węzłów i dysków**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-191">**Node and Disk Majority**.</span></span> <span data-ttu-id="afbe1-192">Każdy węzeł i wyznaczonych dysku (monitorem dysku) w magazynie klastra hello głosować gdy są one dostępne i w komunikacie.</span><span class="sxs-lookup"><span data-stu-id="afbe1-192">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="afbe1-193">funkcje klastra Hello tylko w przypadku większości hello głosów, oznacza to, z więcej niż połowy głosów hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-193">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="afbe1-194">W tym trybie ma sens w środowisku klastra z parzystą liczbą węzłów.</span><span class="sxs-lookup"><span data-stu-id="afbe1-194">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="afbe1-195">Jeśli hello połowa węzłów i dysków hello są w trybie online, hello klaster będzie pozostawał w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="afbe1-195">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="afbe1-196">**Węzeł i udziału plików większość**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-196">**Node and File Share Majority**.</span></span> <span data-ttu-id="afbe1-197">Każdy węzeł plus udział plików wyznaczonych (monitora udziału plików), który hello administrator tworzy głosować, niezależnie od tego, czy są dostępne węzły hello i udziału plików i komunikacji.</span><span class="sxs-lookup"><span data-stu-id="afbe1-197">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="afbe1-198">funkcje klastra Hello tylko w przypadku większości hello głosów, oznacza to, z więcej niż połowy głosów hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-198">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="afbe1-199">W tym trybie ma sens w środowisku klastra z parzystą liczbą węzłów.</span><span class="sxs-lookup"><span data-stu-id="afbe1-199">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="afbe1-200">Jest podobne toohello węzła i tryb większość dysku, ale zamiast monitora dysku używa monitora udziału plików.</span><span class="sxs-lookup"><span data-stu-id="afbe1-200">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="afbe1-201">Ten tryb jest łatwe tooimplement, ale jeśli udział plików hello sam nie ma wysokiej dostępności, mogą stać się pojedynczym punktem awarii.</span><span class="sxs-lookup"><span data-stu-id="afbe1-201">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="afbe1-202">**Bez większości: Na dysku tylko**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-202">**No Majority: Disk Only**.</span></span> <span data-ttu-id="afbe1-203">Hello klaster ma kworum, jeśli jeden węzeł jest dostępny i komunikuje się z określonym dyskiem w magazynie klastra hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-203">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="afbe1-204">Tylko węzły hello, które są także komunikuje się z tego dysku może dołączać hello klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-204">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="afbe1-205">Zaleca się, że nie należy używać tego trybu.</span><span class="sxs-lookup"><span data-stu-id="afbe1-205">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="afbe1-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a>Windows Server awaryjnej lokalnej</span><span class="sxs-lookup"><span data-stu-id="afbe1-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="afbe1-207">Rysunek 1 pokazuje klastra z dwoma węzłami.</span><span class="sxs-lookup"><span data-stu-id="afbe1-207">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="afbe1-208">Jeśli hello połączenie sieciowe między węzłami hello nie powiedzie się i oba węzły pozostać w górę i uruchomiona, udziału pliku lub dysku kworum Określa, który węzeł będzie tooprovide hello klastra aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="afbe1-208">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="afbe1-209">węzeł Hello, dysku kworum toohello dostępu lub udział plików jest hello węzła, który zapewnia, że usługi.</span><span class="sxs-lookup"><span data-stu-id="afbe1-209">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="afbe1-210">Ponieważ w tym przykładzie użyto dwa węzły klastra, używamy hello węzła i Tryb kworum Większość udziału plików.</span><span class="sxs-lookup"><span data-stu-id="afbe1-210">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="afbe1-211">Większość dysku i Hello węzła również jest prawidłową opcją.</span><span class="sxs-lookup"><span data-stu-id="afbe1-211">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="afbe1-212">W środowisku produkcyjnym zaleca się, że używasz dysku kworum.</span><span class="sxs-lookup"><span data-stu-id="afbe1-212">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="afbe1-213">Można użyć sieci i magazynu toomake technologii systemu go wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="afbe1-213">You can use network and storage system technology toomake it highly available.</span></span>

![Rysunek 1: Na przykład Windows Server Failover Clustering konfiguracji dla programu SAP ASCS/SCS na platformie Azure][sap-ha-guide-figure-1000]

<span data-ttu-id="afbe1-215">_**Rysunek 1.** przykład Windows Server Failover Clustering konfiguracji dla programu SAP ASCS/SCS na platformie Azure_</span><span class="sxs-lookup"><span data-stu-id="afbe1-215">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="afbe1-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a>Magazyn udostępniony</span><span class="sxs-lookup"><span data-stu-id="afbe1-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="afbe1-217">Rysunek 1 pokazuje również klastra magazynu udostępnionego z dwoma węzłami.</span><span class="sxs-lookup"><span data-stu-id="afbe1-217">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="afbe1-218">W lokalnej klastra magazynu udostępnionego wszystkie węzły w klastrze hello wykryć magazynu udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="afbe1-218">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="afbe1-219">Mechanizm blokowania chroni dane hello przed uszkodzeniem.</span><span class="sxs-lookup"><span data-stu-id="afbe1-219">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="afbe1-220">Wszystkie węzły mogą wykryć, jeśli inny węzeł nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="afbe1-220">All nodes can detect if another node fails.</span></span> <span data-ttu-id="afbe1-221">Jeśli jeden węzeł ulegnie awarii, drugi węzeł hello przejmuje hello zasoby magazynu oraz zapewnia hello dostępności usług.</span><span class="sxs-lookup"><span data-stu-id="afbe1-221">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="afbe1-222">Nie trzeba udostępnionych dysków wysokiej dostępności z niektórymi aplikacjami systemu DBMS, takich jak z programem SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afbe1-222">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="afbe1-223">SQL Server AlwaysOn replikuje DBMS danych i plików dziennika z hello dysku jednego węzła toohello lokalnego dysku klastrowego innego węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-223">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="afbe1-224">W takim przypadku konfiguracji klastra z systemem Windows hello nie wymaga udostępnionego dysku.</span><span class="sxs-lookup"><span data-stu-id="afbe1-224">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="afbe1-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a>Sieci i rozpoznawanie nazw</span><span class="sxs-lookup"><span data-stu-id="afbe1-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="afbe1-226">Komputery klienckie osiągnąć hello klastra za pośrednictwem wirtualnego adresu IP i nazwy hostów wirtualnych tego hello, które udostępnia serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-226">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="afbe1-227">Witaj węzłów lokalnymi i hello serwer DNS może obsłużyć wielu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-227">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="afbe1-228">W typowej instalacji można użyć dwóch lub więcej połączeń sieciowych:</span><span class="sxs-lookup"><span data-stu-id="afbe1-228">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="afbe1-229">Magazyn toohello dedykowanego połączenia</span><span class="sxs-lookup"><span data-stu-id="afbe1-229">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="afbe1-230">Połączenie z siecią wewnętrzną klastra dla hello pulsu</span><span class="sxs-lookup"><span data-stu-id="afbe1-230">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="afbe1-231">Sieć publiczną, że klienci używają tooconnect toohello klastra</span><span class="sxs-lookup"><span data-stu-id="afbe1-231">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="afbe1-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a>Windows Server awaryjnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="afbe1-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="afbe1-233">W porównaniu toobare wdrożenia kompletnego stanu lub prywatnej chmury, maszyn wirtualnych Azure wymaga systemu Windows Server Failover Clustering tooconfigure dodatkowe kroki.</span><span class="sxs-lookup"><span data-stu-id="afbe1-233">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="afbe1-234">Podczas tworzenia dysku udostępnionego klastra konieczne tooset kilka adresów IP i hostów wirtualnych nazwy hello SAP ASCS/SCS wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-234">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="afbe1-235">W tym artykule firma Microsoft omówiono kluczowe założenia i hello toobuild wymagane dodatkowe kroki SAP klastra usług centralnej o wysokiej dostępności na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-235">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="afbe1-236">Firma Microsoft przedstawiają sposób tooset się narzędzia innej firmy hello SIOS DataKeeper i jak tooconfigure hello Azure wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-236">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="afbe1-237">Toocreate te narzędzia klastra trybu failover w systemie Windows można użyć z monitora udziału plików na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-237">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![Rysunek 2: Windows Server Failover Clustering konfiguracji platformy Azure bez udostępnionego dysku][sap-ha-guide-figure-1001]

<span data-ttu-id="afbe1-239">_**Rysunek 2.** Windows Server Failover Clustering konfiguracji na platformie Azure, bez udostępnionego dysku_</span><span class="sxs-lookup"><span data-stu-id="afbe1-239">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="afbe1-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a>Udostępniony dysk na platformie Azure z SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="afbe1-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="afbe1-241">Należy klastra magazynu udostępnionego dla wystąpienia programu SAP ASCS/SCS wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="afbe1-241">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="afbe1-242">Września 2016 r. Azure nie oferuje magazyn udostępniony który program toocreate klastra magazynu udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="afbe1-242">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="afbe1-243">Można użyć oprogramowania innych firm SIOS DataKeeper Cluster Edition toocreate dublowany magazynu, która symuluje magazyn udostępniony klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-243">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="afbe1-244">Hello SIOS rozwiązanie zapewnia replikację danych w czasie rzeczywistym synchroniczne.</span><span class="sxs-lookup"><span data-stu-id="afbe1-244">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="afbe1-245">Jest to tworzenia zasobu dysku udostępnionego dla klastra:</span><span class="sxs-lookup"><span data-stu-id="afbe1-245">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="afbe1-246">Dołącz tooeach dodatkowy dysk hello maszyn wirtualnych (VM) w konfiguracji klastra systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="afbe1-246">Attach an additional disk tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="afbe1-247">Uruchamianie SIOS DataKeeper Cluster Edition w obu węzłach maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afbe1-247">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="afbe1-248">Skonfiguruj SIOS DataKeeper Cluster Edition, aby go odzwierciedla hello zawartości woluminu dysku dodatkowe hello z hello źródłowej maszyny wirtualnej toohello dodatkowy dysk dołączony woluminu hello docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afbe1-248">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional disk attached volume from hello source virtual machine toohello additional disk attached volume of hello target virtual machine.</span></span> <span data-ttu-id="afbe1-249">SIOS DataKeeper abstracts hello źródłowa i docelowa woluminy lokalne, a następnie je tooWindows serwera jako jeden dysk udostępniony klaster pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="afbe1-249">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="afbe1-250">Uzyskaj więcej informacji [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span><span class="sxs-lookup"><span data-stu-id="afbe1-250">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![Rysunek 3: Windows Server Failover Clustering konfiguracji na platformie Azure z SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="afbe1-252">_**Rysunek 3.** konfiguracji klastra trybu Failover systemu Windows Server na platformie Azure z SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="afbe1-252">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="afbe1-253">Nie potrzebujesz wysokiej dostępności z niektórych produktów, bazami danych, takich jak SQL Server udostępnione dyski.</span><span class="sxs-lookup"><span data-stu-id="afbe1-253">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="afbe1-254">SQL Server AlwaysOn replikuje DBMS danych i plików dziennika z hello dysku jednego węzła toohello lokalnego dysku klastrowego innego węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-254">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="afbe1-255">W takim przypadku konfiguracji klastra z systemem Windows hello nie wymaga udostępnionego dysku.</span><span class="sxs-lookup"><span data-stu-id="afbe1-255">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="afbe1-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Rozpoznawanie nazw w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="afbe1-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="afbe1-257">Witaj chmury Azure platforma nie oferuje hello opcja tooconfigure wirtualnych adresów IP, takie jak adresy IP zmiennoprzecinkowych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-257">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="afbe1-258">Należy tooset rozwiązań alternatywnych zapasowej wirtualnego adresu IP adres tooreach hello zasób klastra w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-258">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="afbe1-259">Platforma Azure ma wewnętrznego modułu równoważenia obciążenia w hello Usługa równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-259">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="afbe1-260">Z hello wewnętrznego modułu równoważenia obciążenia klienci osiągnąć hello klastra za pośrednictwem hello klastra wirtualnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-260">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="afbe1-261">Należy toodeploy hello wewnętrznego modułu równoważenia obciążenia w grupie zasobów hello zawierający hello węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-261">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="afbe1-262">Następnie należy skonfigurować wszystkie niezbędne portu przekazywania reguły z badania hello porty hello wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-262">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="afbe1-263">Witaj, klienci mogą łączyć za pomocą nazwy hostów wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-263">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="afbe1-264">Witaj serwer DNS rozpoznaje adres IP klastra hello i przekazywania toohello aktywnego węzła klastra hello hello obciążenia wewnętrznego modułu równoważenia dojścia do portu.</span><span class="sxs-lookup"><span data-stu-id="afbe1-264">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="afbe1-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a>SAP NetWeaver wysokiej dostępności w Azure infrastruktury jako — usługa (IaaS)</span><span class="sxs-lookup"><span data-stu-id="afbe1-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="afbe1-266">tooachieve SAP wysoką dostępność aplikacji, takie jak SAP składników oprogramowania, muszą hello tooprotect następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="afbe1-266">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="afbe1-267">Wystąpienie serwera aplikacji SAP</span><span class="sxs-lookup"><span data-stu-id="afbe1-267">SAP Application Server instance</span></span>
* <span data-ttu-id="afbe1-268">Wystąpienie programu SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="afbe1-268">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="afbe1-269">Serwer systemu DBMS</span><span class="sxs-lookup"><span data-stu-id="afbe1-269">DBMS server</span></span>

<span data-ttu-id="afbe1-270">Aby uzyskać więcej informacji o ochronie składników SAP w scenariuszach wysokiej dostępności, zobacz [maszyny wirtualne Azure planowania i wdrażania dla programu SAP NetWeaver][planning-guide-11].</span><span class="sxs-lookup"><span data-stu-id="afbe1-270">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <span data-ttu-id="afbe1-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a>Serwer aplikacji SAP wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="afbe1-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="afbe1-272">Zwykle nie trzeba konkretnego rozwiązania wysokiej dostępności dla wystąpień serwera aplikacji SAP i okna dialogowe hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-272">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="afbe1-273">Zapewniania wysokiej dostępności przez nadmiarowości i wiele wystąpień w oknie dialogowym należy skonfigurować w różnych wystąpień maszyn wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-273">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="afbe1-274">Powinien mieć co najmniej dwóch wystąpień aplikacji SAP zainstalowane w dwóch wystąpień maszyn wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-274">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![Rysunek 4: SAP wysokiej dostępności aplikacji serwera][sap-ha-guide-figure-2000]

<span data-ttu-id="afbe1-276">_**Rysunek 4:** SAP wysokiej dostępności serwera aplikacji_</span><span class="sxs-lookup"><span data-stu-id="afbe1-276">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="afbe1-277">Należy umieścić wszystkich maszyn wirtualnych, że host wystąpień serwera aplikacji SAP w hello tego samego zestawu dostępności Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-277">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="afbe1-278">Zestaw dostępności Azure upewnia się, że:</span><span class="sxs-lookup"><span data-stu-id="afbe1-278">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="afbe1-279">Wszystkie maszyny wirtualne są częścią hello tej samej domeny uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-279">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="afbe1-280">Domeny uaktualnienia, na przykład upewnia się, że hello maszyny wirtualne nie są aktualizowane na powitania jednocześnie podczas zaplanowanej konserwacji przestoju.</span><span class="sxs-lookup"><span data-stu-id="afbe1-280">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="afbe1-281">Wszystkie maszyny wirtualne są częścią hello tej samej domenie błędów.</span><span class="sxs-lookup"><span data-stu-id="afbe1-281">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="afbe1-282">Domeny błędów, na przykład upewnia się, że maszyny wirtualne są wdrażane tak, aby nie pojedynczego punktu awarii wpływa na dostępność hello wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-282">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="afbe1-283">Dowiedz się więcej o tym, jak za[Zarządzanie hello dostępność maszyn wirtualnych][virtual-machines-manage-availability].</span><span class="sxs-lookup"><span data-stu-id="afbe1-283">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="afbe1-284">Niezarządzane tylko na dysku: hello kontem magazynu platformy Azure jest potencjalnych pojedynczy punkt awarii, dlatego jest ważne toohave przynajmniej dwóch kont magazynu Azure, w których są dystrybuowane co najmniej dwóch maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-284">Unmanaged disk only: Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="afbe1-285">W Instalatorze idealne dysków hello każdej maszyny wirtualnej, na którym jest uruchomione wystąpienie okna dialogowego SAP będzie można wdrożyć w innego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="afbe1-285">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="afbe1-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a>Wystąpienie programu SAP ASCS/SCS wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="afbe1-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="afbe1-287">Rysunek 5 jest przykładem wystąpienia SAP ASCS/SCS wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="afbe1-287">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![Rysunek 5: Wystąpienie wysokiej dostępności SAP ASCS/SCS][sap-ha-guide-figure-2001]

<span data-ttu-id="afbe1-289">_**Rysunek 5.** SAP wysokiej dostępności ASCS/SCS wystąpienia_</span><span class="sxs-lookup"><span data-stu-id="afbe1-289">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="afbe1-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a>SAP ASCS/SCS wystąpienie wysokiej dostępności z systemu Windows Server Failover Clustering na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="afbe1-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="afbe1-291">W porównaniu toobare wdrożenia kompletnego stanu lub prywatnej chmury, maszyn wirtualnych Azure wymaga systemu Windows Server Failover Clustering tooconfigure dodatkowe kroki.</span><span class="sxs-lookup"><span data-stu-id="afbe1-291">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="afbe1-292">toobuild klastra pracy awaryjnej systemu Windows, należy dysku udostępnionego klastra, kilka adresów IP, kilka nazw hostów wirtualnych i Azure wewnętrznego modułu równoważenia obciążenia dla klastra z wystąpieniem SAP ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-292">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="afbe1-293">Omówiono bardziej szczegółowo w dalszej części artykułu hello to.</span><span class="sxs-lookup"><span data-stu-id="afbe1-293">We discuss this in more detail later in hello article.</span></span>

![Rysunek 6: Windows Server Failover Clustering konfiguracji SAP ASCS/SCS na platformie Azure przy użyciu SIOS DataKeeper][sap-ha-guide-figure-1002]

<span data-ttu-id="afbe1-295">_**Rysunek 6.** Windows Server Failover Clustering konfiguracji SAP ASCS/SCS na platformie Azure z SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="afbe1-295">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="afbe1-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Wystąpienie systemu DBMS wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="afbe1-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="afbe1-297">Witaj DBMS jest również pojedynczy punkt kontaktu w systemie SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-297">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="afbe1-298">Należy tooprotect go za pomocą rozwiązania wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="afbe1-298">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="afbe1-299">Rysunek nr 7 przedstawia rozwiązania wysokiej dostępności programu SQL Server zawsze na platformie Azure, Windows Server Failover Clustering i hello Azure wewnętrzne usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-299">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="afbe1-300">SQL Server AlwaysOn replikuje DBMS danych i plików dziennika przy użyciu własnego systemu DBMS replikacji.</span><span class="sxs-lookup"><span data-stu-id="afbe1-300">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="afbe1-301">W takim przypadku możesz nie muszą klastra udostępnione dyski, które upraszcza hello wszystkie ustawienia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-301">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![Rysunek 7: Przykładem DBMS SAP wysokiej dostępności, z programu SQL Server AlwaysOn][sap-ha-guide-figure-2003]

<span data-ttu-id="afbe1-303">_**Rysunek 7.** przykład DBMS SAP wysokiej dostępności, z programu SQL Server AlwaysOn_</span><span class="sxs-lookup"><span data-stu-id="afbe1-303">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="afbe1-304">Aby uzyskać więcej informacji o klastrach programu SQL Server na platformie Azure przy użyciu modelu wdrażania usługi Azure Resource Manager hello zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="afbe1-304">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="afbe1-305">[Konfiguruj zawsze włączone grupy dostępności w maszynach wirtualnych platformy Azure ręcznie przy użyciu usługi Resource Manager] [virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="afbe1-305">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="afbe1-306">[Konfiguruj Azure wewnętrznego modułu równoważenia obciążenia dla grupy dostępności AlwaysOn w Azure] [virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="afbe1-306">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="afbe1-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a>Scenariusze wdrażania wysokiej dostępności na trasie</span><span class="sxs-lookup"><span data-stu-id="afbe1-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="afbe1-308">Scenariusz wdrażania przy użyciu architektury 1 szablonu</span><span class="sxs-lookup"><span data-stu-id="afbe1-308">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="afbe1-309">Rysunek nr 8 przedstawia przykład architektury wysokiej dostępności programu SAP NetWeaver Azure **jeden** systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-309">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="afbe1-310">Ten scenariusz jest skonfigurowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="afbe1-310">This scenario is set up as follows:</span></span>

- <span data-ttu-id="afbe1-311">Jeden dedykowanego klastra jest używany dla wystąpienia programu SAP ASCS/SCS hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-311">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="afbe1-312">Jeden dedykowanego klastra jest używany dla wystąpienia systemu DBMS hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-312">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="afbe1-313">SAP wystąpień serwera aplikacji są wdrażane w ich własnych dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-313">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![Rysunek 8: SAP wysokiej dostępności architektury szablonu 1, za pomocą dedykowanego klastra ASCS/SCS i bazami danych][sap-ha-guide-figure-2004]

<span data-ttu-id="afbe1-315">_**Rysunek 8.** SAP architektury 1 szablonu wysokiej dostępności, dedykowane klastry ASCS/SCS i bazami danych_</span><span class="sxs-lookup"><span data-stu-id="afbe1-315">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="afbe1-316">Scenariusz wdrażania przy użyciu architektury 2 szablonu</span><span class="sxs-lookup"><span data-stu-id="afbe1-316">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="afbe1-317">Na rysunku nr 9 przedstawiono przykład architektury wysokiej dostępności programu SAP NetWeaver Azure **jeden** systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-317">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="afbe1-318">Ten scenariusz jest skonfigurowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="afbe1-318">This scenario is set up as follows:</span></span>

- <span data-ttu-id="afbe1-319">Jeden klaster dedykowanych służy do **zarówno** hello SAP ASCS/SCS wystąpienia i hello systemu DBMS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-319">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="afbe1-320">SAP wystąpień serwera aplikacji są wdrażane w własnych dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-320">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![Rysunek 9: SAP wysokiej dostępności architektury szablonu 2, dedykowanego klastra dla ASCS/SCS i dedykowanego klastra dla systemu DBMS][sap-ha-guide-figure-2005]

<span data-ttu-id="afbe1-322">_**Rysunek 9:** SAP wysokiej dostępności architektury szablonu 2, dedykowanego klastra dla ASCS/SCS i dedykowanego klastra dla systemu DBMS_</span><span class="sxs-lookup"><span data-stu-id="afbe1-322">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="afbe1-323">Scenariusz wdrażania przy użyciu architektury 3 szablonu</span><span class="sxs-lookup"><span data-stu-id="afbe1-323">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="afbe1-324">Na rysunku nr 10 przedstawiono architekturę SAP NetWeaver wysokiej dostępności platformy Azure dla **dwóch** SAP systemy, z &lt;SID1&gt; i &lt;SID2&gt;.</span><span class="sxs-lookup"><span data-stu-id="afbe1-324">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="afbe1-325">Ten scenariusz jest skonfigurowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="afbe1-325">This scenario is set up as follows:</span></span>

- <span data-ttu-id="afbe1-326">Jeden dedykowanego klastra służy do **zarówno** wystąpienia hello SAP ASCS/SCS SID1 *i* hello SID2 ASCS/SCS SAP wystąpienia (jednego klastra).</span><span class="sxs-lookup"><span data-stu-id="afbe1-326">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="afbe1-327">Jeden dedykowanego klastra jest używany dla systemu DBMS SID1 i innym dedykowanego klastra jest używany dla systemu DBMS SID2 (dwa klastry).</span><span class="sxs-lookup"><span data-stu-id="afbe1-327">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="afbe1-328">SAP wystąpień serwera aplikacji hello systemu SAP SID1 ma swoje własne dedykowane maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="afbe1-328">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="afbe1-329">SAP wystąpień serwera aplikacji hello systemu SAP SID2 ma swoje własne dedykowane maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="afbe1-329">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![Rysunek 10: Wysoka dostępność architektury szablonu 3, z dedykowanym klastrem w różnych wystąpieniach ASCS/SCS SAP][sap-ha-guide-figure-6003]

<span data-ttu-id="afbe1-331">_**Rysunek 10:** wysokiej dostępności architektury szablonu 3, z dedykowanym klastrem w różnych wystąpieniach ASCS/SCS SAP_</span><span class="sxs-lookup"><span data-stu-id="afbe1-331">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="afbe1-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Przygotowanie infrastruktury hello</span><span class="sxs-lookup"><span data-stu-id="afbe1-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="afbe1-333">Przygotowanie infrastruktury hello architektury 1 szablonu</span><span class="sxs-lookup"><span data-stu-id="afbe1-333">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="afbe1-334">Szablony usługi Azure Resource Manager dla programu SAP uprościć wdrażanie wymaganych zasobów.</span><span class="sxs-lookup"><span data-stu-id="afbe1-334">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="afbe1-335">Hello trójwarstwowa szablonów usługi Azure Resource Manager obsługuje również scenariuszy wysokiej dostępności, takich jak w architektury 1 szablon, który ma dwa klastry.</span><span class="sxs-lookup"><span data-stu-id="afbe1-335">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="afbe1-336">Każdy klaster jest SAP pojedynczego punktu awarii dla programu SAP ASCS/SCS i bazami danych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-336">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="afbe1-337">Oto, gdzie można uzyskać szablonów usługi Azure Resource Manager hello przykładowy scenariusz, który opisano w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="afbe1-337">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="afbe1-338">Obraz Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="afbe1-338">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="afbe1-339">Za pomocą zarządzanych dysków Azure obrazu z witryny Marketplace</span><span class="sxs-lookup"><span data-stu-id="afbe1-339">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [<span data-ttu-id="afbe1-340">Obraz niestandardowy</span><span class="sxs-lookup"><span data-stu-id="afbe1-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [<span data-ttu-id="afbe1-341">Niestandardowy obraz za pomocą dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="afbe1-341">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

<span data-ttu-id="afbe1-342">Infrastruktura hello tooprepare dla architektury szablon 1:</span><span class="sxs-lookup"><span data-stu-id="afbe1-342">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="afbe1-343">W portalu Azure na powitania hello **parametry** bloku w hello **SYSTEMAVAILABILITY** wybierz opcję **HA**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-343">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![Rysunek 11: Ustaw parametry usługi Azure Resource Manager wysokiej dostępności SAP][sap-ha-guide-figure-3000]

<span data-ttu-id="afbe1-345">_**Rysunek 11:** ustawić parametry usługi Azure Resource Manager wysokiej dostępności SAP_</span><span class="sxs-lookup"><span data-stu-id="afbe1-345">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="afbe1-346">Utwórz szablony Hello:</span><span class="sxs-lookup"><span data-stu-id="afbe1-346">hello templates create:</span></span>

  * <span data-ttu-id="afbe1-347">**Maszyny wirtualne**:</span><span class="sxs-lookup"><span data-stu-id="afbe1-347">**Virtual machines**:</span></span>
    * <span data-ttu-id="afbe1-348">Maszyny wirtualne serwera aplikacji SAP: <*SAPSystemSID*> - podpisane — <*numer*></span><span class="sxs-lookup"><span data-stu-id="afbe1-348">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="afbe1-349">Maszyny wirtualne klastra ASCS/SCS: <*SAPSystemSID*> - ascs - <*numer*></span><span class="sxs-lookup"><span data-stu-id="afbe1-349">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="afbe1-350">Klaster systemu DBMS: <*SAPSystemSID*> - db - <*numer*></span><span class="sxs-lookup"><span data-stu-id="afbe1-350">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="afbe1-351">**Sieci karty dla wszystkich maszyn wirtualnych adresów IP skojarzonych**:</span><span class="sxs-lookup"><span data-stu-id="afbe1-351">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="afbe1-352"><*SAPSystemSID*> - nic - podpisane — <*numer*></span><span class="sxs-lookup"><span data-stu-id="afbe1-352"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="afbe1-353"><*SAPSystemSID*> - nic - ascs - <*numer*></span><span class="sxs-lookup"><span data-stu-id="afbe1-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="afbe1-354"><*SAPSystemSID*> - nic - db - <*numer*></span><span class="sxs-lookup"><span data-stu-id="afbe1-354"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="afbe1-355">**Konta magazynu platformy Azure (tylko w przypadku dysków niezarządzany)**</span><span class="sxs-lookup"><span data-stu-id="afbe1-355">**Azure storage accounts (unmanaged disks only)**</span></span>

  * <span data-ttu-id="afbe1-356">**Grupy dostępności** dla:</span><span class="sxs-lookup"><span data-stu-id="afbe1-356">**Availability groups** for:</span></span>
    * <span data-ttu-id="afbe1-357">Maszyny wirtualne serwera aplikacji SAP: <*SAPSystemSID*> - avset - podpisane</span><span class="sxs-lookup"><span data-stu-id="afbe1-357">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="afbe1-358">Maszyny wirtualne klastra SAP ASCS/SCS: <*SAPSystemSID*> - avset - ascs</span><span class="sxs-lookup"><span data-stu-id="afbe1-358">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="afbe1-359">System DBMS klastrowanie maszyn wirtualnych: <*SAPSystemSID*> - avset - db</span><span class="sxs-lookup"><span data-stu-id="afbe1-359">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="afbe1-360">**Azure wewnętrznego modułu równoważenia obciążenia**:</span><span class="sxs-lookup"><span data-stu-id="afbe1-360">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="afbe1-361">Z wszystkimi portami dla wystąpienia ASCS/SCS hello i adresu IP <*SAPSystemSID*> - lb - ascs</span><span class="sxs-lookup"><span data-stu-id="afbe1-361">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="afbe1-362">Z wszystkimi portami dla adresu IP i bazami danych programu SQL Server hello <*SAPSystemSID*> - lb - db</span><span class="sxs-lookup"><span data-stu-id="afbe1-362">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="afbe1-363">**Grupy zabezpieczeń sieci**: <*SAPSystemSID*> - nsg - ascs-0</span><span class="sxs-lookup"><span data-stu-id="afbe1-363">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="afbe1-364">Z otwartych zewnętrznych toohello port protokołu RDP (Remote Desktop) <*SAPSystemSID*> - ascs - 0 maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="afbe1-364">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="afbe1-365">Wszystkie adresy IP karty sieciowej hello i Azure wewnętrzne moduły równoważenia obciążenia są **dynamiczne** domyślnie.</span><span class="sxs-lookup"><span data-stu-id="afbe1-365">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="afbe1-366">Zmień je za**statycznych** adresów IP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-366">Change them too**static** IP addresses.</span></span> <span data-ttu-id="afbe1-367">Opisano sposób toodo to w dalszej części artykułu hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-367">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="afbe1-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Wdrażanie maszyn wirtualnych z siecią firmową toouse łączności (między lokalizacjami) w środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="afbe1-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="afbe1-369">Dla systemów SAP produkcyjnych, wdrażanie maszyn wirtualnych platformy Azure z [łączności z siecią firmową (między lokalizacjami)] [ planning-guide-2.2] za pomocą usługi Azure Site to Site VPN lub rozwiązania Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="afbe1-369">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="afbe1-370">Można użyć wystąpienia sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-370">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="afbe1-371">sieć wirtualna Hello i podsieć już zostały utworzone i przygotowane.</span><span class="sxs-lookup"><span data-stu-id="afbe1-371">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="afbe1-372">W portalu Azure na powitania hello **parametry** bloku w hello **NEWOREXISTINGSUBNET** wybierz opcję **istniejących**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-372">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="afbe1-373">W hello **SUBNETID** Dodaj pełne ciąg hello sieci Azure przygotowane SubnetID, w którym planujesz toodeploy maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-373">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="afbe1-374">tooget listę wszystkich podsieci w sieci Azure, uruchom następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="afbe1-374">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="afbe1-375">Witaj **identyfikator** pole zawiera hello **SUBNETID**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-375">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="afbe1-376">Lista wszystkich tooget **SUBNETID** wartości, uruchom to polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="afbe1-376">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="afbe1-377">Witaj **SUBNETID** wygląda podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="afbe1-377">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="afbe1-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a>Wdrażanie wystąpień SAP tylko w chmurze dla testu i pokaz</span><span class="sxs-lookup"><span data-stu-id="afbe1-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="afbe1-379">Można wdrożyć systemu SAP wysokiej dostępności w modelu wdrażania tylko w chmurze.</span><span class="sxs-lookup"><span data-stu-id="afbe1-379">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="afbe1-380">Tego rodzaju wdrożenia przede wszystkim jest przydatna do demo i test przypadki użycia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-380">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="afbe1-381">Nie nadaje się do przypadków użycia w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="afbe1-381">It's not suited for production use cases.</span></span>

- <span data-ttu-id="afbe1-382">W portalu Azure na powitania hello **parametry** bloku w hello **NEWOREXISTINGSUBNET** wybierz opcję **nowe**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-382">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="afbe1-383">Pozostaw hello **SUBNETID** pole puste.</span><span class="sxs-lookup"><span data-stu-id="afbe1-383">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="afbe1-384">Witaj SAP usługi Azure Resource Manager automatycznie tworzy szablon hello sieci wirtualnej platformy Azure i podsieć.</span><span class="sxs-lookup"><span data-stu-id="afbe1-384">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="afbe1-385">Należy również toodeploy maszyny wirtualnej co najmniej jednego przeznaczonego do usługi Active Directory i DNS w hello tego samego wystąpienia usługi Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="afbe1-385">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="afbe1-386">Szablon Hello nie tworzy tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-386">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="afbe1-387">Przygotowanie infrastruktury hello architektury 2 szablonu</span><span class="sxs-lookup"><span data-stu-id="afbe1-387">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="afbe1-388">Dla SAP toohelp uprościć wdrażanie zasobów wymaganej infrastruktury dla programu SAP architektury szablonu 2, można użyć tego szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="afbe1-388">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="afbe1-389">Oto, gdzie można uzyskać szablonów usługi Azure Resource Manager dla tego scenariusza wdrażania:</span><span class="sxs-lookup"><span data-stu-id="afbe1-389">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="afbe1-390">Obraz Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="afbe1-390">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="afbe1-391">Za pomocą zarządzanych dysków Azure obrazu z witryny Marketplace</span><span class="sxs-lookup"><span data-stu-id="afbe1-391">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [<span data-ttu-id="afbe1-392">Obraz niestandardowy</span><span class="sxs-lookup"><span data-stu-id="afbe1-392">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [<span data-ttu-id="afbe1-393">Niestandardowy obraz za pomocą dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="afbe1-393">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="afbe1-394">Przygotowanie infrastruktury hello architektury 3 szablonu</span><span class="sxs-lookup"><span data-stu-id="afbe1-394">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="afbe1-395">Można przygotować infrastrukturę hello i skonfigurować SAP dla **multi-SID**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-395">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="afbe1-396">Na przykład można dodać dodatkowe wystąpienia SAP ASCS/SCS do *istniejących* konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-396">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="afbe1-397">Aby uzyskać więcej informacji, zobacz [skonfigurować dodatkowe wystąpienia SAP ASCS/SCS do istniejącej konfiguracji klastra toocreate SAP identyfikatora SID wielu konfiguracji usługi Azure Resource Manager][sap-ha-multi-sid-guide].</span><span class="sxs-lookup"><span data-stu-id="afbe1-397">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="afbe1-398">Chcąc toocreate multi-SID nowego klastra, można użyć hello multi-SID [szablony szybkiego startu w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="afbe1-398">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="afbe1-399">toocreate multi-SID nowego klastra należy hello toodeploy następujące trzy szablony:</span><span class="sxs-lookup"><span data-stu-id="afbe1-399">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* [<span data-ttu-id="afbe1-400">ASCS/SCS szablonu</span><span class="sxs-lookup"><span data-stu-id="afbe1-400">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="afbe1-401">Szablon bazy danych</span><span class="sxs-lookup"><span data-stu-id="afbe1-401">Database template</span></span>](#database-template)
* [<span data-ttu-id="afbe1-402">Szablon serwerów aplikacji</span><span class="sxs-lookup"><span data-stu-id="afbe1-402">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="afbe1-403">Witaj następujące sekcje mają więcej szczegółów na temat szablonów hello i parametry hello należy tooprovide w szablonach hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-403">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="afbe1-404"><a name="ASCS-SCS-template"></a>ASCS/SCS szablonu</span><span class="sxs-lookup"><span data-stu-id="afbe1-404"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="afbe1-405">Szablon ASCS/SCS Hello wdraża dwie maszyny wirtualne, których można używać klastra pracy awaryjnej systemu Windows Server, który obsługuje wiele wystąpień ASCS/SCS toocreate.</span><span class="sxs-lookup"><span data-stu-id="afbe1-405">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="afbe1-406">tooset się szablon hello ASCS/SCS multi-SID w hello [szablon identyfikatora SID multi ASCS/SCS] [ sap-templates-3-tier-multisid-xscs-marketplace-image] lub [ASCS/SCS identyfikatora SID multi szablonu za pomocą dysków zarządzanych] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], wprowadź wartości dla hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="afbe1-406">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image] or [ASCS/SCS multi-SID template using Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="afbe1-407">**Prefiks zasobów**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-407">**Resource Prefix**.</span></span>  <span data-ttu-id="afbe1-408">Ustaw wszystkie zasoby, które są tworzone podczas wdrażania hello hello zasobów prefiks, który jest używany tooprefix.</span><span class="sxs-lookup"><span data-stu-id="afbe1-408">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="afbe1-409">Ponieważ zasoby hello nie należą tooonly jednego systemu SAP, prefiks hello hello zasobu nie jest hello identyfikatora SID jednego systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-409">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="afbe1-410">Prefiks Hello musi należeć do zakresu od **trzech do sześciu znaków**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-410">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="afbe1-411">**Na stosie typu**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-411">**Stack Type**.</span></span> <span data-ttu-id="afbe1-412">Wybierz typ stosu hello hello systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-412">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="afbe1-413">W zależności od typu stosu hello usługi równoważenia obciążenia Azure ma jeden (ABAP lub tylko Java) lub dwóch (ABAP + Java) prywatnych adresów IP na systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-413">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="afbe1-414">**Typ systemu operacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-414">**OS Type**.</span></span> <span data-ttu-id="afbe1-415">Wybierz system operacyjny hello hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-415">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="afbe1-416">**Liczba systemu SAP**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-416">**SAP System Count**.</span></span> <span data-ttu-id="afbe1-417">Wybierz liczbę hello systemów SAP ma tooinstall w tym klastrze.</span><span class="sxs-lookup"><span data-stu-id="afbe1-417">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="afbe1-418">**Dostępność systemu**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-418">**System Availability**.</span></span> <span data-ttu-id="afbe1-419">Wybierz **HA**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-419">Select **HA**.</span></span>
  -  <span data-ttu-id="afbe1-420">**Nazwa użytkownika i hasło administratora**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-420">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="afbe1-421">Utwórz nowego użytkownika, które mogą być używane toosign toohello maszyny.</span><span class="sxs-lookup"><span data-stu-id="afbe1-421">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="afbe1-422">**Nowy lub istniejący podsieci**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-422">**New Or Existing Subnet**.</span></span> <span data-ttu-id="afbe1-423">Określ, czy należy utworzyć nową sieć wirtualną i podsieć lub istniejącą podsieć powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="afbe1-423">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="afbe1-424">Jeśli masz już sieć wirtualną tooyour połączonych sieci lokalnej, wybierz **istniejących**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-424">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="afbe1-425">**Identyfikator podsieci**. Identyfikator zestawu hello maszyn wirtualnych hello hello podsieci toowhich powinny być połączone.</span><span class="sxs-lookup"><span data-stu-id="afbe1-425">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="afbe1-426">Wybierz podsieć hello wirtualnej sieci prywatnej (VPN) lub sieci lokalnej tooyour ExpressRoute sieci wirtualnej tooconnect hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afbe1-426">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="afbe1-427">Identyfikator Hello zwykle wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="afbe1-427">hello ID usually looks like this:</span></span>

   <span data-ttu-id="afbe1-428">/Subscriptions/ <*identyfikator subskrypcji*> /resourceGroups/ <*Nazwa grupy zasobów*> /providers/Microsoft.Network/virtualNetworks/ <*wirtualnej nazwy sieciowej*> /subnets/ <*nazwy podsieci*></span><span class="sxs-lookup"><span data-stu-id="afbe1-428">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="afbe1-429">Szablon Hello wdraża jedno wystąpienie usługi równoważenia obciążenia Azure, która obsługuje wiele systemów SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-429">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="afbe1-430">wystąpienia ASCS Hello są skonfigurowane dla liczby wystąpień 00, 10, 20...</span><span class="sxs-lookup"><span data-stu-id="afbe1-430">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="afbe1-431">wystąpienia SCS Hello są skonfigurowane dla liczby wystąpień 01 11, 21...</span><span class="sxs-lookup"><span data-stu-id="afbe1-431">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="afbe1-432">Witaj wystąpień ASCS umieścić w kolejce replikacji serwera (Wywołujących) (tylko w systemie Linux) są skonfigurowane do liczby wystąpień 02, 12, 22...</span><span class="sxs-lookup"><span data-stu-id="afbe1-432">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="afbe1-433">Witaj wystąpień Wywołujących SCS (tylko w systemie Linux) są skonfigurowane do liczby wystąpień 03, 13, 23...</span><span class="sxs-lookup"><span data-stu-id="afbe1-433">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="afbe1-434">Witaj modułu równoważenia obciążenia zawiera 1 (2 dla systemu Linux) VIP(s), 1 x dla ASCS/SCS i 1 x adres VIP dla Wywołujących (tylko w systemie Linux).</span><span class="sxs-lookup"><span data-stu-id="afbe1-434">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="afbe1-435">Witaj Poniższa lista zawiera wszystkie reguły, o których (gdzie x to liczba hello hello systemu SAP, na przykład 1, 2, 3...) równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="afbe1-435">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="afbe1-436">Porty właściwe dla systemu Windows dla każdego systemu SAP: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="afbe1-436">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="afbe1-437">Porty ASCS (liczby wystąpień x0): 32 x 0, 36 x 0, 39 x 0, 81 x 0, 5 x 013, 5 x 014, 5 x 016</span><span class="sxs-lookup"><span data-stu-id="afbe1-437">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="afbe1-438">Porty SCS (liczby wystąpień x1): 32 x 1, 33 x 1, 39 x 1, 81 x 1, 5 x 113, 5 x 114, 5 x 116</span><span class="sxs-lookup"><span data-stu-id="afbe1-438">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="afbe1-439">Wywołujących ASCS porty w systemie Linux (liczby wystąpień x2): 33 x 2, 5 x 213, 5 x 214, 5 x 216</span><span class="sxs-lookup"><span data-stu-id="afbe1-439">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="afbe1-440">Wywołujących SCS porty w systemie Linux (liczby wystąpień x3): 33 x 3, 5 x 313, 5 x 314, 5 x 316</span><span class="sxs-lookup"><span data-stu-id="afbe1-440">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="afbe1-441">Moduł równoważenia obciążenia Hello jest hello toouse skonfigurowane następujące porty sondowania (gdzie x to liczba hello hello systemu SAP, na przykład 1, 2, 3...):</span><span class="sxs-lookup"><span data-stu-id="afbe1-441">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="afbe1-442">Port sondy modułu równoważenia obciążenia wewnętrznego ASCS/SCS: 620 x 0</span><span class="sxs-lookup"><span data-stu-id="afbe1-442">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="afbe1-443">Wewnętrzny Wywołujących załadować port sondy modułu równoważenia (tylko w systemie Linux): 621 x 2</span><span class="sxs-lookup"><span data-stu-id="afbe1-443">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="afbe1-444"><a name="database-template"></a>Szablon bazy danych</span><span class="sxs-lookup"><span data-stu-id="afbe1-444"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="afbe1-445">szablon bazy danych Hello wdraża jedną lub dwie maszyny wirtualne, których można używać tooinstall hello system zarządzania relacyjnymi bazami (danych RDBMS) dla jednego systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-445">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="afbe1-446">Na przykład jeśli wdrożono szablon ASCS/SCS pięć systemów SAP, należy toodeploy ten szablon pięć razy.</span><span class="sxs-lookup"><span data-stu-id="afbe1-446">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="afbe1-447">tooset się hello szablon identyfikatora SID multi bazy danych, w hello [bazy danych wielu SID szablonu] [ sap-templates-3-tier-multisid-db-marketplace-image] lub [szablon identyfikatora SID multi bazy danych przy użyciu dysków zarządzanych] [ sap-templates-3-tier-multisid-db-marketplace-image-md], wprowadź wartości dla hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="afbe1-447">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image] or [database multi-SID template using Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="afbe1-448">**Identyfikator systemu SAP**. Wprowadź identyfikator systemu SAP hello hello ma tooinstall systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-448">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="afbe1-449">Identyfikator Hello będzie służyć jako prefiks hello zasobów, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="afbe1-449">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="afbe1-450">**Typ systemu operacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-450">**Os Type**.</span></span> <span data-ttu-id="afbe1-451">Wybierz system operacyjny hello hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-451">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="afbe1-452">**Wartość DbType**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-452">**Dbtype**.</span></span> <span data-ttu-id="afbe1-453">Wybierz typ hello hello bazy danych ma tooinstall na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-453">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="afbe1-454">Wybierz **SQL** Jeśli chcesz tooinstall programu Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afbe1-454">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="afbe1-455">Wybierz **HANA** Jeśli planujesz tooinstall SAP HANA hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-455">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="afbe1-456">Upewnij się, że tooselect hello poprawnego typu systemu operacyjnego: Wybierz **Windows** SQL i wybierz opcję dystrybucji systemu Linux HANA.</span><span class="sxs-lookup"><span data-stu-id="afbe1-456">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="afbe1-457">Witaj równoważenia obciążenia Azure, który jest połączony toohello, które maszyny wirtualne będą skonfigurowane toosupport hello wybrane bazy danych typu:</span><span class="sxs-lookup"><span data-stu-id="afbe1-457">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="afbe1-458">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-458">**SQL**.</span></span> <span data-ttu-id="afbe1-459">Moduł równoważenia obciążenia Hello będzie Równoważenie obciążenia portu 1433.</span><span class="sxs-lookup"><span data-stu-id="afbe1-459">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="afbe1-460">Upewnij się, że toouse tego portu dla ustawień programu SQL Server AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="afbe1-460">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="afbe1-461">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-461">**HANA**.</span></span> <span data-ttu-id="afbe1-462">Moduł równoważenia obciążenia Hello będzie Równoważenie obciążenia portów 35015 i 35017.</span><span class="sxs-lookup"><span data-stu-id="afbe1-462">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="afbe1-463">Upewnij się, że tooinstall SAP HANA z liczby wystąpień **50**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-463">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="afbe1-464">Moduł równoważenia obciążenia Hello będzie używać portu sondowania 62550.</span><span class="sxs-lookup"><span data-stu-id="afbe1-464">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="afbe1-465">**Rozmiar systemu SAP**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-465">**Sap System Size**.</span></span> <span data-ttu-id="afbe1-466">Dostarcza zestaw hello liczba protokoły SAP hello nowy system.</span><span class="sxs-lookup"><span data-stu-id="afbe1-466">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="afbe1-467">Jeśli nie masz pewności, ile protokoły SAP hello system będzie wymagać, zapytaj SAP technologii partnera lub Integrator systemu.</span><span class="sxs-lookup"><span data-stu-id="afbe1-467">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="afbe1-468">**Dostępność systemu**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-468">**System Availability**.</span></span> <span data-ttu-id="afbe1-469">Wybierz **HA**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-469">Select **HA**.</span></span>
  -  <span data-ttu-id="afbe1-470">**Nazwa użytkownika i hasło administratora**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-470">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="afbe1-471">Utwórz nowego użytkownika, które mogą być używane toosign toohello maszyny.</span><span class="sxs-lookup"><span data-stu-id="afbe1-471">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="afbe1-472">**Identyfikator podsieci**. Wprowadź identyfikator hello hello podsieci, który został użyty podczas wdrażania hello hello ASCS/SCS szablonu lub identyfikator hello hello podsieci, który został utworzony jako część hello ASCS/SCS szablonu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-472">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="afbe1-473"><a name="application-servers-template"></a>Szablon serwerów aplikacji</span><span class="sxs-lookup"><span data-stu-id="afbe1-473"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="afbe1-474">Szablon serwerów aplikacji Hello wdraża dwóch lub więcej maszyn wirtualnych, które mogą służyć jako wystąpień serwera aplikacji SAP jednego systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-474">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="afbe1-475">Na przykład jeśli wdrożono szablon ASCS/SCS pięć systemów SAP, należy toodeploy ten szablon pięć razy.</span><span class="sxs-lookup"><span data-stu-id="afbe1-475">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="afbe1-476">tooset się hello serwerów wielu SID szablon aplikacji w hello [szablon identyfikatora SID wielu serwerów aplikacji] [ sap-templates-3-tier-multisid-apps-marketplace-image] lub [szablon identyfikatora SID wielu serwerów aplikacji za pomocą zarządzania dyskami] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], wprowadź wartości dla hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="afbe1-476">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image] or [application servers multi-SID template using Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="afbe1-477">**Identyfikator systemu SAP**. Wprowadź identyfikator systemu SAP hello hello ma tooinstall systemu SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-477">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="afbe1-478">Identyfikator Hello będzie służyć jako prefiks hello zasobów, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="afbe1-478">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="afbe1-479">**Typ systemu operacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-479">**Os Type**.</span></span> <span data-ttu-id="afbe1-480">Wybierz system operacyjny hello hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-480">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="afbe1-481">**Rozmiar systemu SAP**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-481">**Sap System Size**.</span></span> <span data-ttu-id="afbe1-482">określi liczbę Hello protokoły SAP hello nowy system.</span><span class="sxs-lookup"><span data-stu-id="afbe1-482">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="afbe1-483">Jeśli nie masz pewności, ile protokoły SAP hello system będzie wymagać, zapytaj SAP technologii partnera lub Integrator systemu.</span><span class="sxs-lookup"><span data-stu-id="afbe1-483">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="afbe1-484">**Dostępność systemu**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-484">**System Availability**.</span></span> <span data-ttu-id="afbe1-485">Wybierz **HA**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-485">Select **HA**.</span></span>
  -  <span data-ttu-id="afbe1-486">**Nazwa użytkownika i hasło administratora**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-486">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="afbe1-487">Utwórz nowego użytkownika, które mogą być używane toosign toohello maszyny.</span><span class="sxs-lookup"><span data-stu-id="afbe1-487">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="afbe1-488">**Identyfikator podsieci**. Wprowadź identyfikator hello hello podsieci, który został użyty podczas wdrażania hello hello ASCS/SCS szablonu lub identyfikator hello hello podsieci, który został utworzony jako część hello ASCS/SCS szablonu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-488">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="afbe1-489"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a>Sieć wirtualna platformy Azure</span><span class="sxs-lookup"><span data-stu-id="afbe1-489"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="afbe1-490">W naszym przykładzie hello przestrzeni adresowej sieci wirtualnej platformy Azure hello jest 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="afbe1-490">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="afbe1-491">Brak jednej podsieci o nazwie **podsieci**, z zakresu adresów 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="afbe1-491">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="afbe1-492">Wszystkie maszyny wirtualne i wewnętrzne moduły równoważenia obciążenia są wdrażane w tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afbe1-492">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afbe1-493">Nie wprowadzono żadnych zmian toohello ustawień sieciowych w systemie operacyjnym gościa hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-493">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="afbe1-494">W tym adresy IP, serwery DNS i podsieci.</span><span class="sxs-lookup"><span data-stu-id="afbe1-494">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="afbe1-495">Skonfiguruj ustawienia sieci na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-495">Configure all your network settings in Azure.</span></span> <span data-ttu-id="afbe1-496">Witaj usługi protokołu dynamicznej konfiguracji hosta (DHCP) propaguje ustawienia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-496">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="afbe1-497"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>Adresy IP serwera DNS</span><span class="sxs-lookup"><span data-stu-id="afbe1-497"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="afbe1-498">Witaj tooset wymagane adresy IP serwera DNS, hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="afbe1-498">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="afbe1-499">W portalu Azure na powitania hello **serwerów DNS** bloku, upewnij się, że sieci wirtualne **serwerów DNS** opcja jest ustawiona zbyt**niestandardowe DNS**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-499">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="afbe1-500">Wybierz ustawienia, na podstawie typu hello sieci, do których masz.</span><span class="sxs-lookup"><span data-stu-id="afbe1-500">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="afbe1-501">Aby uzyskać więcej informacji zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="afbe1-501">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="afbe1-502">[Łączność sieci firmowej (między lokalizacjami)][planning-guide-2.2]: Dodaj hello adresy IP serwerów DNS lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="afbe1-502">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="afbe1-503">Można rozszerzyć lokalnymi DNS serwerów toohello maszyn wirtualnych, które są uruchomione na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-503">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="afbe1-504">W tym scenariuszu można dodać adresy IP hello hello Azure maszyn wirtualnych, na których uruchomiono hello usługi DNS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-504">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="afbe1-505">[Tylko w chmurze wdrożenia][planning-guide-2.1]: wdrożyć dodatkowe maszyny wirtualnej w hello tego samego wystąpienia sieci wirtualnej, która służy jako serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-505">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="afbe1-506">Dodaj adresy IP hello hello Azure maszyn wirtualnych, które po skonfigurowaniu toorun usługi DNS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-506">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![Rysunek 12: Należy skonfigurować serwery DNS dla sieci wirtualnej platformy Azure][sap-ha-guide-figure-3001]

    <span data-ttu-id="afbe1-508">_**Rysunek 12:** DNS Konfigurowanie serwerów na potrzeby sieci wirtualnej platformy Azure_</span><span class="sxs-lookup"><span data-stu-id="afbe1-508">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="afbe1-509">Jeśli zmienisz hello adresy IP serwerów DNS hello należy toorestart hello maszyn wirtualnych platformy Azure tooapply hello zmiany oraz propagację hello nowych serwerów DNS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-509">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="afbe1-510">W naszym przykładzie hello usługa DNS jest instalowany i konfigurowany na tych maszynach wirtualnych systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="afbe1-510">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="afbe1-511">Roli maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="afbe1-511">Virtual machine role</span></span> | <span data-ttu-id="afbe1-512">Nazwa hosta maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="afbe1-512">Virtual machine host name</span></span> | <span data-ttu-id="afbe1-513">Nazwa karty sieciowej</span><span class="sxs-lookup"><span data-stu-id="afbe1-513">Network card name</span></span> | <span data-ttu-id="afbe1-514">Statyczny adres IP</span><span class="sxs-lookup"><span data-stu-id="afbe1-514">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="afbe1-515">Pierwszy serwer DNS</span><span class="sxs-lookup"><span data-stu-id="afbe1-515">First DNS server</span></span> |<span data-ttu-id="afbe1-516">domcontr 0</span><span class="sxs-lookup"><span data-stu-id="afbe1-516">domcontr-0</span></span> |<span data-ttu-id="afbe1-517">PR1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="afbe1-517">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="afbe1-518">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="afbe1-518">10.0.0.10</span></span> |
| <span data-ttu-id="afbe1-519">Drugi serwer DNS</span><span class="sxs-lookup"><span data-stu-id="afbe1-519">Second DNS server</span></span> |<span data-ttu-id="afbe1-520">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="afbe1-520">domcontr-1</span></span> |<span data-ttu-id="afbe1-521">PR1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="afbe1-521">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="afbe1-522">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="afbe1-522">10.0.0.11</span></span> |

### <span data-ttu-id="afbe1-523"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Nazwy hosta i statyczne adresy IP dla klastrowanego wystąpienia programu SAP ASCS/SCS hello i DBMS klastrowanego wystąpienia</span><span class="sxs-lookup"><span data-stu-id="afbe1-523"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="afbe1-524">Dla wdrożenia lokalnego należy te hosta zarezerwowanych nazw i adresów IP:</span><span class="sxs-lookup"><span data-stu-id="afbe1-524">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="afbe1-525">Rola nazwy hostów wirtualnych</span><span class="sxs-lookup"><span data-stu-id="afbe1-525">Virtual host name role</span></span> | <span data-ttu-id="afbe1-526">Nazwy hostów wirtualnych</span><span class="sxs-lookup"><span data-stu-id="afbe1-526">Virtual host name</span></span> | <span data-ttu-id="afbe1-527">Wirtualne statycznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="afbe1-527">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="afbe1-528">Nazwa SAP ASCS/SCS do hostów wirtualnych pierwszej klastra (dla klastra zarządzania)</span><span class="sxs-lookup"><span data-stu-id="afbe1-528">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="afbe1-529">PR1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="afbe1-529">pr1-ascs-vir</span></span> |<span data-ttu-id="afbe1-530">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="afbe1-530">10.0.0.42</span></span> |
| <span data-ttu-id="afbe1-531">Nazwa hosta wirtualnego wystąpienia programu SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="afbe1-531">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="afbe1-532">PR1 ascs sap</span><span class="sxs-lookup"><span data-stu-id="afbe1-532">pr1-ascs-sap</span></span> |<span data-ttu-id="afbe1-533">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="afbe1-533">10.0.0.43</span></span> |
| <span data-ttu-id="afbe1-534">Nazwa systemu DBMS SAP do hostów wirtualnych drugi klastra (klastra zarządzania)</span><span class="sxs-lookup"><span data-stu-id="afbe1-534">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="afbe1-535">PR1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="afbe1-535">pr1-dbms-vir</span></span> |<span data-ttu-id="afbe1-536">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="afbe1-536">10.0.0.32</span></span> |

<span data-ttu-id="afbe1-537">Podczas tworzenia klastra hello, utworzyć hello nazwy hostów wirtualnych **pr1-ascs-vir** i **pr1-dbms-vir** i hello skojarzony adresy IP, które Zarządzanie hello samego klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-537">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="afbe1-538">Aby uzyskać informacje na temat toodo tego, zobacz [zbieranie węzłów klastra w konfiguracji klastra][sap-ha-guide-8.12.1].</span><span class="sxs-lookup"><span data-stu-id="afbe1-538">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="afbe1-539">Można ręcznie utworzyć hello innych dwie nazwy hostów wirtualnych, **pr1 ascs sap** i **pr1 dbms sap**, i hello skojarzony adresy IP na powitania serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-539">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="afbe1-540">Witaj klastrowanego wystąpienia programu SAP ASCS/SCS i hello klastrowane wystąpienie DBMS używać tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="afbe1-540">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="afbe1-541">Aby uzyskać informacje na temat toodo tego, zobacz [Utwórz nazwę hosta wirtualnego dla klastrowanego wystąpienia programu SAP ASCS/SCS][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="afbe1-541">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="afbe1-542"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Ustaw statycznych adresów IP dla maszyn wirtualnych hello SAP</span><span class="sxs-lookup"><span data-stu-id="afbe1-542"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="afbe1-543">Po wdrożeniu hello toouse maszyny wirtualne w klastrze, należy tooset statycznych adresów IP dla wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-543">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="afbe1-544">W tym w konfiguracji sieci wirtualnej Azure hello, a nie w systemie operacyjnym gościa hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-544">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="afbe1-545">Hello portalu Azure, wybierz **grupy zasobów** > **karta sieciowa** > **ustawienia** > **adresu IP** .</span><span class="sxs-lookup"><span data-stu-id="afbe1-545">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="afbe1-546">Na powitania **adresów IP** bloku, w obszarze **przypisania**, wybierz pozycję **statycznych**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-546">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="afbe1-547">W hello **adres IP** wprowadź adres IP hello, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="afbe1-547">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="afbe1-548">Jeśli zmienisz hello adresu IP karty sieciowej hello należy toorestart hello maszyn wirtualnych platformy Azure tooapply hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="afbe1-548">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![Rysunek 13: Ustaw statycznych adresów IP dla karty sieciowej hello każdej maszyny wirtualnej][sap-ha-guide-figure-3002]

  <span data-ttu-id="afbe1-550">_**Rysunek 13:** ustawić statyczny adres IP dla karty sieciowej hello każdej maszyny wirtualnej_</span><span class="sxs-lookup"><span data-stu-id="afbe1-550">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="afbe1-551">Powtórz ten krok dla wszystkich interfejsów sieciowych, oznacza to, że dla wszystkich maszyn wirtualnych, w tym maszyny wirtualne mają toouse usługi/DNS usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="afbe1-551">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="afbe1-552">W naszym przykładzie mamy tych maszyn wirtualnych i statycznymi adresami IP:</span><span class="sxs-lookup"><span data-stu-id="afbe1-552">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="afbe1-553">Roli maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="afbe1-553">Virtual machine role</span></span> | <span data-ttu-id="afbe1-554">Nazwa hosta maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="afbe1-554">Virtual machine host name</span></span> | <span data-ttu-id="afbe1-555">Nazwa karty sieciowej</span><span class="sxs-lookup"><span data-stu-id="afbe1-555">Network card name</span></span> | <span data-ttu-id="afbe1-556">Statyczny adres IP</span><span class="sxs-lookup"><span data-stu-id="afbe1-556">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="afbe1-557">Pierwsze wystąpienie serwera aplikacji SAP</span><span class="sxs-lookup"><span data-stu-id="afbe1-557">First SAP Application Server instance</span></span> |<span data-ttu-id="afbe1-558">PR1 podpisane 0</span><span class="sxs-lookup"><span data-stu-id="afbe1-558">pr1-di-0</span></span> |<span data-ttu-id="afbe1-559">PR1-nic podpisane-0</span><span class="sxs-lookup"><span data-stu-id="afbe1-559">pr1-nic-di-0</span></span> |<span data-ttu-id="afbe1-560">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="afbe1-560">10.0.0.50</span></span> |
| <span data-ttu-id="afbe1-561">Drugie wystąpienie serwera aplikacji SAP</span><span class="sxs-lookup"><span data-stu-id="afbe1-561">Second SAP Application Server instance</span></span> |<span data-ttu-id="afbe1-562">PR1 podpisane 1</span><span class="sxs-lookup"><span data-stu-id="afbe1-562">pr1-di-1</span></span> |<span data-ttu-id="afbe1-563">PR1-nic podpisane-1</span><span class="sxs-lookup"><span data-stu-id="afbe1-563">pr1-nic-di-1</span></span> |<span data-ttu-id="afbe1-564">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="afbe1-564">10.0.0.51</span></span> |
| <span data-ttu-id="afbe1-565">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="afbe1-565">...</span></span> |<span data-ttu-id="afbe1-566">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="afbe1-566">...</span></span> |<span data-ttu-id="afbe1-567">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="afbe1-567">...</span></span> |<span data-ttu-id="afbe1-568">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="afbe1-568">...</span></span> |
| <span data-ttu-id="afbe1-569">Ostatnie wystąpienie serwera aplikacji SAP</span><span class="sxs-lookup"><span data-stu-id="afbe1-569">Last SAP Application Server instance</span></span> |<span data-ttu-id="afbe1-570">PR1-podpisane-5</span><span class="sxs-lookup"><span data-stu-id="afbe1-570">pr1-di-5</span></span> |<span data-ttu-id="afbe1-571">PR1-nic podpisane-5</span><span class="sxs-lookup"><span data-stu-id="afbe1-571">pr1-nic-di-5</span></span> |<span data-ttu-id="afbe1-572">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="afbe1-572">10.0.0.55</span></span> |
| <span data-ttu-id="afbe1-573">Pierwszym węźle klastra dla wystąpienia ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="afbe1-573">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="afbe1-574">PR1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="afbe1-574">pr1-ascs-0</span></span> |<span data-ttu-id="afbe1-575">PR1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="afbe1-575">pr1-nic-ascs-0</span></span> |<span data-ttu-id="afbe1-576">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="afbe1-576">10.0.0.40</span></span> |
| <span data-ttu-id="afbe1-577">Drugi węzeł klastra dla wystąpienia ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="afbe1-577">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="afbe1-578">PR1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="afbe1-578">pr1-ascs-1</span></span> |<span data-ttu-id="afbe1-579">PR1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="afbe1-579">pr1-nic-ascs-1</span></span> |<span data-ttu-id="afbe1-580">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="afbe1-580">10.0.0.41</span></span> |
| <span data-ttu-id="afbe1-581">Pierwszym węźle klastra dla systemu DBMS wystąpienia</span><span class="sxs-lookup"><span data-stu-id="afbe1-581">First cluster node for DBMS instance</span></span> |<span data-ttu-id="afbe1-582">PR1-db-0</span><span class="sxs-lookup"><span data-stu-id="afbe1-582">pr1-db-0</span></span> |<span data-ttu-id="afbe1-583">PR1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="afbe1-583">pr1-nic-db-0</span></span> |<span data-ttu-id="afbe1-584">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="afbe1-584">10.0.0.30</span></span> |
| <span data-ttu-id="afbe1-585">Drugi węzeł klastra dla systemu DBMS wystąpienia</span><span class="sxs-lookup"><span data-stu-id="afbe1-585">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="afbe1-586">PR1-db-1</span><span class="sxs-lookup"><span data-stu-id="afbe1-586">pr1-db-1</span></span> |<span data-ttu-id="afbe1-587">PR1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="afbe1-587">pr1-nic-db-1</span></span> |<span data-ttu-id="afbe1-588">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="afbe1-588">10.0.0.31</span></span> |

### <span data-ttu-id="afbe1-589"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Ustawianie statycznego adresu IP dla hello Azure wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="afbe1-589"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="afbe1-590">Szablon SAP usługi Azure Resource Manager Hello tworzy Azure wewnętrznego modułu równoważenia obciążenia używanego hello SAP ASCS/SCS wystąpienia klastra i hello DBMS klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-590">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afbe1-591">Witaj adresu IP, nazwy hostów wirtualnych hello hello jest SAP ASCS/SCS hello sam jako adres IP hello hello SAP ASCS/SCS wewnętrznego modułu równoważenia obciążenia: **pr1-lb-ascs**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-591">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="afbe1-592">Witaj adresu IP wirtualnej nazwy hello jest DBMS hello hello sam jako adres IP hello hello DBMS wewnętrznego modułu równoważenia obciążenia: **pr1-lb-dbms**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-592">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="afbe1-593">tooset statyczny adres IP dla hello Azure wewnętrzny moduł równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="afbe1-593">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="afbe1-594">Witaj początkowe wdrożenie ustawia adres IP usługi równoważenia obciążenia wewnętrznego hello zbyt**dynamiczne**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-594">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="afbe1-595">W portalu Azure na powitania hello **adresów IP** bloku, w obszarze **przypisania**, wybierz pozycję **statycznych**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-595">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="afbe1-596">Ustaw adres IP hello hello wewnętrznego modułu równoważenia obciążenia **pr1-lb-ascs** toohello adres IP nazwę hosta wirtualnego hello hello SAP ASCS/SCS wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-596">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="afbe1-597">Ustaw adres IP hello hello wewnętrznego modułu równoważenia obciążenia **pr1-lb-dbms** adres IP toohello nazwę hosta wirtualnego hello hello DBMS wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-597">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![Rysunek 14: Ustaw statycznych adresów IP dla hello wewnętrznego modułu równoważenia obciążenia dla wystąpienia programu SAP ASCS/SCS hello][sap-ha-guide-figure-3003]

  <span data-ttu-id="afbe1-599">_**Rysunek 14:** ustawić statycznych adresów IP dla hello wewnętrznego modułu równoważenia obciążenia dla wystąpienia programu SAP ASCS/SCS hello_</span><span class="sxs-lookup"><span data-stu-id="afbe1-599">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="afbe1-600">W naszym przykładzie mamy dwa Azure wewnętrzne moduły równoważenia obciążenia mających te statycznych adresów IP:</span><span class="sxs-lookup"><span data-stu-id="afbe1-600">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="afbe1-601">Rola usługi równoważenia obciążenia wewnętrznego Azure</span><span class="sxs-lookup"><span data-stu-id="afbe1-601">Azure internal load balancer role</span></span> | <span data-ttu-id="afbe1-602">Nazwa modułu równoważenia obciążenia wewnętrznego platformy Azure</span><span class="sxs-lookup"><span data-stu-id="afbe1-602">Azure internal load balancer name</span></span> | <span data-ttu-id="afbe1-603">Statyczny adres IP</span><span class="sxs-lookup"><span data-stu-id="afbe1-603">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="afbe1-604">SAP ASCS/SCS wystąpienia wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="afbe1-604">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="afbe1-605">PR1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="afbe1-605">pr1-lb-ascs</span></span> |<span data-ttu-id="afbe1-606">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="afbe1-606">10.0.0.43</span></span> |
| <span data-ttu-id="afbe1-607">System DBMS SAP wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="afbe1-607">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="afbe1-608">PR1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="afbe1-608">pr1-lb-dbms</span></span> |<span data-ttu-id="afbe1-609">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="afbe1-609">10.0.0.33</span></span> |


### <span data-ttu-id="afbe1-610"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Domyślne reguły dla hello Azure wewnętrznego modułu równoważenia obciążenia równoważenia obciążenia ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="afbe1-610"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="afbe1-611">Szablon Menedżera zasobów Azure SAP Hello tworzy hello portów, które są potrzebne:</span><span class="sxs-lookup"><span data-stu-id="afbe1-611">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="afbe1-612">Wystąpienie ABAP ASCS o numerze wystąpienia domyślnego hello **00**</span><span class="sxs-lookup"><span data-stu-id="afbe1-612">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="afbe1-613">Wystąpienie Java SCS, z numerem wystąpienie domyślne hello **01**</span><span class="sxs-lookup"><span data-stu-id="afbe1-613">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="afbe1-614">Po zainstalowaniu wystąpieniem SAP ASCS/SCS, należy użyć liczby wystąpień domyślnego hello **00** dla ABAP ASCS wystąpienia i hello domyślne wystąpienie numer **01** dla swojego wystąpienia Java SCS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-614">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="afbe1-615">Następnie należy utworzyć równoważenia punktów końcowych dla hello SAP NetWeaver porty wymagane obciążenia wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="afbe1-615">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="afbe1-616">toocreate wymagane punkty końcowe równoważenia obciążenia wewnętrznego, najpierw należy utworzyć te równoważenia punktów końcowych dla portów SAP NetWeaver ABAP ASCS hello obciążenia:</span><span class="sxs-lookup"><span data-stu-id="afbe1-616">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="afbe1-617">Nazwa reguły równoważenia obciążenia/usługi</span><span class="sxs-lookup"><span data-stu-id="afbe1-617">Service/load balancing rule name</span></span> | <span data-ttu-id="afbe1-618">Domyślne numery portów</span><span class="sxs-lookup"><span data-stu-id="afbe1-618">Default port numbers</span></span> | <span data-ttu-id="afbe1-619">Konkretnych portów (ASCS wystąpienia z liczby wystąpień 00) (Wywołujących z 10)</span><span class="sxs-lookup"><span data-stu-id="afbe1-619">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="afbe1-620">Umieścić serwer / *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="afbe1-620">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="afbe1-621">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="afbe1-621">32<*InstanceNumber*></span></span> |<span data-ttu-id="afbe1-622">3200</span><span class="sxs-lookup"><span data-stu-id="afbe1-622">3200</span></span> |
| <span data-ttu-id="afbe1-623">Serwer komunikatów ABAP / *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="afbe1-623">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="afbe1-624">36 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="afbe1-624">36<*InstanceNumber*></span></span> |<span data-ttu-id="afbe1-625">3600</span><span class="sxs-lookup"><span data-stu-id="afbe1-625">3600</span></span> |
| <span data-ttu-id="afbe1-626">Komunikat wewnętrzny ABAP / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="afbe1-626">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="afbe1-627">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="afbe1-627">39<*InstanceNumber*></span></span> |<span data-ttu-id="afbe1-628">3900</span><span class="sxs-lookup"><span data-stu-id="afbe1-628">3900</span></span> |
| <span data-ttu-id="afbe1-629">Serwer HTTP / *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="afbe1-629">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="afbe1-630">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="afbe1-630">81<*InstanceNumber*></span></span> |<span data-ttu-id="afbe1-631">8100</span><span class="sxs-lookup"><span data-stu-id="afbe1-631">8100</span></span> |
| <span data-ttu-id="afbe1-632">SAP uruchamiania usługi ASCS HTTP / *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="afbe1-632">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="afbe1-633">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="afbe1-633">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="afbe1-634">50013</span><span class="sxs-lookup"><span data-stu-id="afbe1-634">50013</span></span> |
| <span data-ttu-id="afbe1-635">SAP uruchamiania usługi ASCS HTTPS / *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="afbe1-635">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="afbe1-636">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="afbe1-636">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="afbe1-637">50014</span><span class="sxs-lookup"><span data-stu-id="afbe1-637">50014</span></span> |
| <span data-ttu-id="afbe1-638">Umieścić w kolejce replikacji / *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="afbe1-638">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="afbe1-639">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="afbe1-639">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="afbe1-640">50016</span><span class="sxs-lookup"><span data-stu-id="afbe1-640">50016</span></span> |
| <span data-ttu-id="afbe1-641">SAP uruchamiania usługi Wywołujących HTTP *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="afbe1-641">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="afbe1-642">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="afbe1-642">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="afbe1-643">51013</span><span class="sxs-lookup"><span data-stu-id="afbe1-643">51013</span></span> |
| <span data-ttu-id="afbe1-644">SAP uruchamiania usługi Wywołujących HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="afbe1-644">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="afbe1-645">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="afbe1-645">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="afbe1-646">51014</span><span class="sxs-lookup"><span data-stu-id="afbe1-646">51014</span></span> |
| <span data-ttu-id="afbe1-647">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="afbe1-647">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="afbe1-648">5985</span><span class="sxs-lookup"><span data-stu-id="afbe1-648">5985</span></span> |
| <span data-ttu-id="afbe1-649">Udział plików *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="afbe1-649">File Share *Lbrule445*</span></span> | |<span data-ttu-id="afbe1-650">445</span><span class="sxs-lookup"><span data-stu-id="afbe1-650">445</span></span> |

<span data-ttu-id="afbe1-651">_**Tabela 1:** portu liczby wystąpień programu SAP NetWeaver ABAP ASCS hello_</span><span class="sxs-lookup"><span data-stu-id="afbe1-651">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="afbe1-652">Następnie utwórz te równoważenia punktów końcowych dla portów SAP NetWeaver Java SCS hello obciążenia:</span><span class="sxs-lookup"><span data-stu-id="afbe1-652">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="afbe1-653">Nazwa reguły równoważenia obciążenia/usługi</span><span class="sxs-lookup"><span data-stu-id="afbe1-653">Service/load balancing rule name</span></span> | <span data-ttu-id="afbe1-654">Domyślne numery portów</span><span class="sxs-lookup"><span data-stu-id="afbe1-654">Default port numbers</span></span> | <span data-ttu-id="afbe1-655">Konkretnych portów (SCS wystąpienia z liczby wystąpień 01) (Wywołujących z 11)</span><span class="sxs-lookup"><span data-stu-id="afbe1-655">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="afbe1-656">Umieścić serwer / *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="afbe1-656">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="afbe1-657">32 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="afbe1-657">32<*InstanceNumber*></span></span> |<span data-ttu-id="afbe1-658">3201</span><span class="sxs-lookup"><span data-stu-id="afbe1-658">3201</span></span> |
| <span data-ttu-id="afbe1-659">Serwer bramy / *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="afbe1-659">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="afbe1-660">33 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="afbe1-660">33<*InstanceNumber*></span></span> |<span data-ttu-id="afbe1-661">3301</span><span class="sxs-lookup"><span data-stu-id="afbe1-661">3301</span></span> |
| <span data-ttu-id="afbe1-662">Serwer komunikatów Java / *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="afbe1-662">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="afbe1-663">39 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="afbe1-663">39<*InstanceNumber*></span></span> |<span data-ttu-id="afbe1-664">3901</span><span class="sxs-lookup"><span data-stu-id="afbe1-664">3901</span></span> |
| <span data-ttu-id="afbe1-665">Serwer HTTP / *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="afbe1-665">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="afbe1-666">81 <*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="afbe1-666">81<*InstanceNumber*></span></span> |<span data-ttu-id="afbe1-667">8101</span><span class="sxs-lookup"><span data-stu-id="afbe1-667">8101</span></span> |
| <span data-ttu-id="afbe1-668">SAP uruchamiania usługi SCS HTTP / *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="afbe1-668">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="afbe1-669">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="afbe1-669">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="afbe1-670">50113</span><span class="sxs-lookup"><span data-stu-id="afbe1-670">50113</span></span> |
| <span data-ttu-id="afbe1-671">SAP uruchamiania usługi SCS HTTPS / *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="afbe1-671">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="afbe1-672">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="afbe1-672">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="afbe1-673">50114</span><span class="sxs-lookup"><span data-stu-id="afbe1-673">50114</span></span> |
| <span data-ttu-id="afbe1-674">Umieścić w kolejce replikacji / *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="afbe1-674">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="afbe1-675">5 <*InstanceNumber*> 16</span><span class="sxs-lookup"><span data-stu-id="afbe1-675">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="afbe1-676">50116</span><span class="sxs-lookup"><span data-stu-id="afbe1-676">50116</span></span> |
| <span data-ttu-id="afbe1-677">SAP uruchamiania usługi Wywołujących HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="afbe1-677">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="afbe1-678">5 <*InstanceNumber*> 13</span><span class="sxs-lookup"><span data-stu-id="afbe1-678">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="afbe1-679">51113</span><span class="sxs-lookup"><span data-stu-id="afbe1-679">51113</span></span> |
| <span data-ttu-id="afbe1-680">SAP uruchamiania usługi Wywołujących HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="afbe1-680">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="afbe1-681">5 <*InstanceNumber*> 14</span><span class="sxs-lookup"><span data-stu-id="afbe1-681">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="afbe1-682">51114</span><span class="sxs-lookup"><span data-stu-id="afbe1-682">51114</span></span> |
| <span data-ttu-id="afbe1-683">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="afbe1-683">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="afbe1-684">5985</span><span class="sxs-lookup"><span data-stu-id="afbe1-684">5985</span></span> |
| <span data-ttu-id="afbe1-685">Udział plików *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="afbe1-685">File Share *Lbrule445*</span></span> | |<span data-ttu-id="afbe1-686">445</span><span class="sxs-lookup"><span data-stu-id="afbe1-686">445</span></span> |

<span data-ttu-id="afbe1-687">_**Tabela 2:** portu liczby wystąpień programu SAP NetWeaver Java SCS hello_</span><span class="sxs-lookup"><span data-stu-id="afbe1-687">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![Rys. 15: Reguły dla hello Azure wewnętrznego modułu równoważenia obciążenia równoważenia obciążenia domyślne ASCS/SCS][sap-ha-guide-figure-3004]

<span data-ttu-id="afbe1-689">_**Rysunek 15:** reguły dla hello Azure wewnętrznego modułu równoważenia obciążenia równoważenia obciążenia domyślne ASCS/SCS_</span><span class="sxs-lookup"><span data-stu-id="afbe1-689">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="afbe1-690">Ustawienie hello adresu IP usługi równoważenia obciążenia hello **pr1-lb-dbms** adres IP toohello nazwę hosta wirtualnego hello hello DBMS wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-690">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="afbe1-691"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Zmień obciążenia domyślne ASCS/SCS hello równoważenia zasady hello Azure wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="afbe1-691"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="afbe1-692">Jeśli mają różne liczby toouse dla hello SAP ASCS lub SCS wystąpienia, należy zmienić hello nazwy i wartości ich porty z wartościami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="afbe1-692">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="afbe1-693">Hello portalu Azure, wybierz  **<* SID*> - lb - ascs załadować równoważenia ** > **reguły równoważenia obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-693">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="afbe1-694">Dla wszystkich reguł, należące toohello SAP ASCS lub wystąpienie SCS równoważenia obciążenia Zmień wartości tych:</span><span class="sxs-lookup"><span data-stu-id="afbe1-694">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="afbe1-695">Nazwa</span><span class="sxs-lookup"><span data-stu-id="afbe1-695">Name</span></span>
  * <span data-ttu-id="afbe1-696">Port</span><span class="sxs-lookup"><span data-stu-id="afbe1-696">Port</span></span>
  * <span data-ttu-id="afbe1-697">Port zaplecza</span><span class="sxs-lookup"><span data-stu-id="afbe1-697">Back-end port</span></span>

  <span data-ttu-id="afbe1-698">Na przykład jeśli chcesz toochange hello domyślnej liczby wystąpień ASCS od 00 too31 należy toomake hello zmiany dla wszystkich portów wymienionych w tabeli 1.</span><span class="sxs-lookup"><span data-stu-id="afbe1-698">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="afbe1-699">Oto przykład aktualizacji dla portu *lbrule3200*.</span><span class="sxs-lookup"><span data-stu-id="afbe1-699">Here's an example of an update for port *lbrule3200*.</span></span>

  ![Rysunek 16: Zmień obciążenia domyślne ASCS/SCS hello równoważenia zasady hello Azure wewnętrznego modułu równoważenia obciążenia][sap-ha-guide-figure-3005]

  <span data-ttu-id="afbe1-701">_**Rysunek 16:** zmiany hello ASCS/SCS domyślne obciążenia równoważenia zasady hello Azure wewnętrznego modułu równoważenia obciążenia_</span><span class="sxs-lookup"><span data-stu-id="afbe1-701">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="afbe1-702"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Dodawanie domeny toohello maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="afbe1-702"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="afbe1-703">Po przypisaniu statycznego maszyn wirtualnych toohello adres IP, należy dodać hello maszyn wirtualnych toohello domeny.</span><span class="sxs-lookup"><span data-stu-id="afbe1-703">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![Rysunek 17: Dodawanie domeny tooa maszyny wirtualnej][sap-ha-guide-figure-3006]

<span data-ttu-id="afbe1-705">_**Rysunek 17:** Dodawanie domeny tooa maszyny wirtualnej_</span><span class="sxs-lookup"><span data-stu-id="afbe1-705">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="afbe1-706"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Dodawanie wpisów rejestru na obu węzłach hello SAP ASCS/SCS wystąpienia</span><span class="sxs-lookup"><span data-stu-id="afbe1-706"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="afbe1-707">Moduł równoważenia obciążenia Azure zawiera wewnętrzny moduł równoważenia obciążenia zamknięciu połączeń w przypadku połączeń hello są w stanie bezczynności pewien okres czasu (limit czasu bezczynności).</span><span class="sxs-lookup"><span data-stu-id="afbe1-707">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="afbe1-708">Procesów roboczych SAP w oknie dialogowym wystąpień otwarte połączenia toohello SAP umieścić przetworzyć jak hello pierwszy umieścić w kolejce/usuwania z kolejki żądania wysyłane toobe potrzeb.</span><span class="sxs-lookup"><span data-stu-id="afbe1-708">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="afbe1-709">Te połączenia zazwyczaj pozostaje ustalonych do procesu roboczego hello lub ponownego uruchomienia procesu umieścić w kolejce hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-709">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="afbe1-710">Jednak jeśli hello połączenie jest bezczynne na wybrany okres czasu, hello połączeń hello zostanie zamknięty usługi równoważenia obciążenia wewnętrznego platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-710">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="afbe1-711">Nie stanowi problemu, ponieważ hello procesu roboczego SAP ustanawia ponownie hello połączenia toohello umieścić procesu, jeśli już nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="afbe1-711">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="afbe1-712">Te działania są udokumentowane w ślady developer hello procesów SAP, ale ich tworzyć dużą ilością zawartości dodatkowe w tych danych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-712">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="afbe1-713">Jest dobrym rozwiązaniem toochange hello TCP/IP `KeepAliveTime` i `KeepAliveInterval` na obu węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-713">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="afbe1-714">Połącz te zmiany w parametrach TCP/IP hello z parametrami profilu SAP, opisane w dalszej części artykułu hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-714">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="afbe1-715">wpisy rejestru tooadd na obu węzłach hello SAP ASCS/SCS wystąpienia, najpierw dodaj te wpisy rejestru systemu Windows na obu węzłów klastra systemu Windows dla programu SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="afbe1-715">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="afbe1-716">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="afbe1-716">Path</span></span> | <span data-ttu-id="afbe1-717">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="afbe1-717">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="afbe1-718">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="afbe1-718">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="afbe1-719">Typ zmiennej</span><span class="sxs-lookup"><span data-stu-id="afbe1-719">Variable type</span></span> |<span data-ttu-id="afbe1-720">REG_DWORD (dziesiętna)</span><span class="sxs-lookup"><span data-stu-id="afbe1-720">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="afbe1-721">Wartość</span><span class="sxs-lookup"><span data-stu-id="afbe1-721">Value</span></span> |<span data-ttu-id="afbe1-722">120000</span><span class="sxs-lookup"><span data-stu-id="afbe1-722">120000</span></span> |
| <span data-ttu-id="afbe1-723">Łącze toodocumentation</span><span class="sxs-lookup"><span data-stu-id="afbe1-723">Link toodocumentation</span></span> |[<span data-ttu-id="afbe1-724">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="afbe1-724">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="afbe1-725">_**Tabela 3:** zmiany hello pierwszy parametr TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="afbe1-725">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="afbe1-726">Następnie należy dodać ten wpisów rejestru systemu Windows na obu węzłów klastra systemu Windows dla programu SAP ASCS/SCS:</span><span class="sxs-lookup"><span data-stu-id="afbe1-726">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="afbe1-727">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="afbe1-727">Path</span></span> | <span data-ttu-id="afbe1-728">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="afbe1-728">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="afbe1-729">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="afbe1-729">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="afbe1-730">Typ zmiennej</span><span class="sxs-lookup"><span data-stu-id="afbe1-730">Variable type</span></span> |<span data-ttu-id="afbe1-731">REG_DWORD (dziesiętna)</span><span class="sxs-lookup"><span data-stu-id="afbe1-731">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="afbe1-732">Wartość</span><span class="sxs-lookup"><span data-stu-id="afbe1-732">Value</span></span> |<span data-ttu-id="afbe1-733">120000</span><span class="sxs-lookup"><span data-stu-id="afbe1-733">120000</span></span> |
| <span data-ttu-id="afbe1-734">Łącze toodocumentation</span><span class="sxs-lookup"><span data-stu-id="afbe1-734">Link toodocumentation</span></span> |[<span data-ttu-id="afbe1-735">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="afbe1-735">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="afbe1-736">_**Tabela 4:** zmiany hello drugi parametr TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="afbe1-736">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="afbe1-737">**tooapply hello zmiany, ponownie uruchom oba węzły klastra**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-737">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="afbe1-738"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a>Konfigurowanie klastra systemu Windows Server Failover Clustering dla wystąpienia programu SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="afbe1-738"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="afbe1-739">Konfigurowanie klastra systemu Windows Server Failover Clustering dla wystąpienia programu SAP ASCS/SCS obejmuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="afbe1-739">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="afbe1-740">Zbieranie hello węzły klastra w konfiguracji klastra</span><span class="sxs-lookup"><span data-stu-id="afbe1-740">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="afbe1-741">Konfigurowanie monitora udziału plików klastra</span><span class="sxs-lookup"><span data-stu-id="afbe1-741">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="afbe1-742"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Zbieraj hello węzły klastra w konfiguracji klastra</span><span class="sxs-lookup"><span data-stu-id="afbe1-742"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="afbe1-743">Hello Dodawanie roli i funkcji — Kreator Dodaj klaster tooboth węzły klastra pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="afbe1-743">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="afbe1-744">Konfigurowanie klastra trybu failover hello za pomocą Menedżera klastra trybu Failover.</span><span class="sxs-lookup"><span data-stu-id="afbe1-744">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="afbe1-745">W Menedżerze klastra trybu Failover wybierz **tworzenia klastrów**, a następnie dodaj tylko hello nazwę hello pierwszy klaster, węzeł A. Nie dodawaj hello drugiego węzła jeszcze; w kolejnym kroku zostanie dodana hello drugiego węzła.</span><span class="sxs-lookup"><span data-stu-id="afbe1-745">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![Rysunek 18: Dodaj powitania serwera lub nazwę maszyny wirtualnej hello na pierwszym węźle klastra][sap-ha-guide-figure-3007]

  <span data-ttu-id="afbe1-747">_**Rysunek 18:** Dodaj nazwę serwera lub maszyny wirtualnej hello hello pierwszego węzła klastra_</span><span class="sxs-lookup"><span data-stu-id="afbe1-747">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="afbe1-748">Wprowadź nazwę sieci hello (nazwa hosta wirtualnego) hello klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-748">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![Rysunek 19: Wprowadź nazwę klastra hello][sap-ha-guide-figure-3008]

  <span data-ttu-id="afbe1-750">_**Rysunek 19:** wprowadź nazwę klastra hello_</span><span class="sxs-lookup"><span data-stu-id="afbe1-750">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="afbe1-751">Po utworzeniu klastra hello uruchomienie testu poprawności klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-751">After you've created hello cluster, run a cluster validation test.</span></span>

  ![Rysunek 20: Uruchom sprawdzenie poprawności klastra hello][sap-ha-guide-figure-3009]

  <span data-ttu-id="afbe1-753">_**Rysunek 20:** uruchom sprawdzenie poprawności klastra hello_</span><span class="sxs-lookup"><span data-stu-id="afbe1-753">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="afbe1-754">Możesz zignorować ostrzeżenia dotyczące dysków w tym momencie w procesie hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-754">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="afbe1-755">Zostanie dodana monitora udostępniania plików i hello SIOS udostępnionych dysków później.</span><span class="sxs-lookup"><span data-stu-id="afbe1-755">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="afbe1-756">Na tym etapie nie jest konieczne tooworry o kworum.</span><span class="sxs-lookup"><span data-stu-id="afbe1-756">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![Rysunek 21: Odnaleziono żadnego dysku kworum][sap-ha-guide-figure-3010]

  <span data-ttu-id="afbe1-758">_**Rysunek 21:** odnaleziono żadnego dysku kworum_</span><span class="sxs-lookup"><span data-stu-id="afbe1-758">_**Figure 21:** No quorum disk is found_</span></span>

  ![Rysunek 22: Zasobu klastra Core wymaga nowego adresu IP][sap-ha-guide-figure-3011]

  <span data-ttu-id="afbe1-760">_**Rysunek 22:** zasobu klastra Core wymaga nowego adresu IP_</span><span class="sxs-lookup"><span data-stu-id="afbe1-760">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="afbe1-761">Zmień adres IP hello hello podstawowej usługi klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-761">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="afbe1-762">Witaj klastra nie można uruchomić, dopóki nie zmieni adres IP hello hello podstawowej klastra usługi, ponieważ hello adres IP serwera hello punktów tooone hello węzły maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afbe1-762">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="afbe1-763">To zrobić na powitania **właściwości** strony usługi hello podstawowej klastra IP zasobu.</span><span class="sxs-lookup"><span data-stu-id="afbe1-763">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="afbe1-764">Na przykład, potrzebujemy tooassign adresu IP (w naszym przykładzie **10.0.0.42**) dla nazwy hosta wirtualnego klastra hello **pr1-ascs-vir**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-764">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![Rysunek 23: Okno dialogowe właściwości hello, zmienić adres IP hello][sap-ha-guide-figure-3012]

  <span data-ttu-id="afbe1-766">_**Rysunek 23:** w hello **właściwości** okno dialogowe, Zmień adres IP hello_</span><span class="sxs-lookup"><span data-stu-id="afbe1-766">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![Rysunek 24: Przypisać adres IP hello, które jest zastrzeżone dla klastra hello][sap-ha-guide-figure-3013]

  <span data-ttu-id="afbe1-768">_**Rysunek 24:** przypisać adres IP hello, które jest zastrzeżone dla klastra hello_</span><span class="sxs-lookup"><span data-stu-id="afbe1-768">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="afbe1-769">Przełącz nazwę hosta wirtualnego klastra hello online.</span><span class="sxs-lookup"><span data-stu-id="afbe1-769">Bring hello cluster virtual host name online.</span></span>

  ![Rysunek 25: Usługi podstawowej klastra jest uruchomiony i działa prawidłowo, a z hello Popraw adres IP][sap-ha-guide-figure-3014]

  <span data-ttu-id="afbe1-771">_**Rysunek 25:** usługi podstawowej klastra jest uruchomiony i działa i z hello Popraw adres IP_</span><span class="sxs-lookup"><span data-stu-id="afbe1-771">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="afbe1-772">Dodaj hello drugiego węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-772">Add hello second cluster node.</span></span>

  <span data-ttu-id="afbe1-773">Teraz, że usługa klastrowania core hello jest uruchomiona, można dodać hello drugiego węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-773">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![Rysunek 26: Dodaj hello drugiego węzła klastra][sap-ha-guide-figure-3015]

  <span data-ttu-id="afbe1-775">_**Rysunek 26:** hello Dodaj drugi węzeł klastra_</span><span class="sxs-lookup"><span data-stu-id="afbe1-775">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="afbe1-776">Wprowadź nazwę hello hosta drugiego węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-776">Enter a name for hello second cluster node host.</span></span>

  ![Rysunek 27: Wprowadź hello nazwy hosta w drugiego węzła klastra][sap-ha-guide-figure-3016]

  <span data-ttu-id="afbe1-778">_**Rysunek 27:** Enter hello drugi nazwa węzła klastra hosta_</span><span class="sxs-lookup"><span data-stu-id="afbe1-778">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="afbe1-779">Upewnij się, że hello **Dodaj wszystkie odpowiednie magazyny toohello klaster** pole wyboru jest **nie** wybrane.</span><span class="sxs-lookup"><span data-stu-id="afbe1-779">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![Rysunek 28: Nie zaznaczaj pola wyboru hello][sap-ha-guide-figure-3017]

  <span data-ttu-id="afbe1-781">_**Rysunek 28:** czy **nie** wybierz hello pole wyboru_</span><span class="sxs-lookup"><span data-stu-id="afbe1-781">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="afbe1-782">Możesz zignorować ostrzeżenia dotyczące kworum i dysków.</span><span class="sxs-lookup"><span data-stu-id="afbe1-782">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="afbe1-783">Opcje ustawisz hello kworum i udziału hello dysku później, zgodnie z opisem w [instalowanie SIOS DataKeeper Cluster Edition dla programu SAP ASCS/SCS dysku klastra, udziału][sap-ha-guide-8.12.3].</span><span class="sxs-lookup"><span data-stu-id="afbe1-783">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![Rysunek 29: Ignoruj ostrzeżenia dotyczące hello dysku kworum][sap-ha-guide-figure-3018]

  <span data-ttu-id="afbe1-785">_**Rysunek 29:** Ignoruj ostrzeżenia dotyczące hello dysku kworum_</span><span class="sxs-lookup"><span data-stu-id="afbe1-785">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="afbe1-786"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a>Skonfiguruj Monitor udziału plików klastra</span><span class="sxs-lookup"><span data-stu-id="afbe1-786"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="afbe1-787">Konfigurowanie monitora udziału plików klastra obejmuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="afbe1-787">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="afbe1-788">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="afbe1-788">Creating a file share</span></span>
- <span data-ttu-id="afbe1-789">Ustawienia kworum monitora udziału plików hello w Menedżerze klastra trybu Failover</span><span class="sxs-lookup"><span data-stu-id="afbe1-789">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="afbe1-790"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a>Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="afbe1-790"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="afbe1-791">Wybierz monitor udziału plików, zamiast dysku kworum.</span><span class="sxs-lookup"><span data-stu-id="afbe1-791">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="afbe1-792">SIOS DataKeeper obsługuje tę opcję.</span><span class="sxs-lookup"><span data-stu-id="afbe1-792">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="afbe1-793">W przykładach hello w tym artykule Monitor udziału plików hello jest na powitania serwera/DNS usługi Active Directory, który działa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-793">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="afbe1-794">Witaj monitora udziału plików jest nazywany **domcontr 0**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-794">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="afbe1-795">Ponieważ czy skonfigurowano tooAzure połączenia sieci VPN (za pośrednictwem sieci VPN typu lokacja-lokacja lub Azure ExpressRoute), monitor udostępniania sieci/DNS usługi Active Directory usługi lokalnej i nie jest toorun odpowiedniego pliku.</span><span class="sxs-lookup"><span data-stu-id="afbe1-795">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="afbe1-796">Jeśli usługa/DNS usługi Active Directory działa tylko na lokalne, nie skonfigurować Twoje monitora udziału plików na hello Active Directory/serwera DNS systemu operacyjnego działającej lokalnie.</span><span class="sxs-lookup"><span data-stu-id="afbe1-796">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="afbe1-797">Opóźnienie sieci między węzłami klastra z systemem Azure i/DNS usługi Active Directory w lokalnym programie może być zbyt duży i spowodować problemy z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="afbe1-797">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="afbe1-798">Należy się tooconfigure hello monitora udziału plików na maszynie wirtualnej platformy Azure, uruchomionym Zamknij toohello węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-798">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="afbe1-799">Stacja kworum Hello wymaga co najmniej 1024 MB wolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="afbe1-799">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="afbe1-800">Zaleca się 2048 MB wolnego miejsca na dysku kworum hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-800">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="afbe1-801">Dodaj obiekt nazwy klastra hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-801">Add hello cluster name object.</span></span>

  ![Rysunek 30: Przypisz hello uprawnienia udziału powitania dla obiekt nazwy klastra hello][sap-ha-guide-figure-3019]

  <span data-ttu-id="afbe1-803">_**Rysunek 30:** przypisać uprawnienia hello hello udziału dla obiekt nazwy klastra hello_</span><span class="sxs-lookup"><span data-stu-id="afbe1-803">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="afbe1-804">Pamiętaj, że uprawnienia hello Dołącz dane toochange urzędu hello hello udział dla obiekt nazwy klastra hello (w naszym przykładzie **pr1-ascs-vir$**).</span><span class="sxs-lookup"><span data-stu-id="afbe1-804">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="afbe1-805">tooadd hello klastra Nazwa obiektu toohello listy, wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-805">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="afbe1-806">Zmień hello toocheck filtru dla obiektów komputerów w toothose dodanie pokazano na rysunku 31.</span><span class="sxs-lookup"><span data-stu-id="afbe1-806">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![Rysunek 31: Zmiana hello typy obiektów tooinclude komputerów][sap-ha-guide-figure-3020]

  <span data-ttu-id="afbe1-808">_**Rysunek 31:** zmienić hello typy obiektów tooinclude komputerów_</span><span class="sxs-lookup"><span data-stu-id="afbe1-808">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![32 rysunku: Zaznacz pole wyboru komputerów hello][sap-ha-guide-figure-3021]

  <span data-ttu-id="afbe1-810">_**Rysunek 32:** wybierz hello **komputery** pole wyboru_</span><span class="sxs-lookup"><span data-stu-id="afbe1-810">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="afbe1-811">Wprowadź hello obiektem nazwy klastra, jak pokazano na rysunku 31.</span><span class="sxs-lookup"><span data-stu-id="afbe1-811">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="afbe1-812">Ponieważ hello rekord został już utworzony, można zmienić uprawnienia hello, jak pokazano na rysunku 30.</span><span class="sxs-lookup"><span data-stu-id="afbe1-812">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="afbe1-813">Wybierz hello **zabezpieczeń** karcie hello udziału, a następnie ustawić bardziej szczegółowe uprawnienia dla obiekt nazwy klastra hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-813">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![Rysunek nr 33: Ustawić atrybutów zabezpieczeń hello dla obiekt nazwy klastra hello na powitania pliku udziału kworum][sap-ha-guide-figure-3022]

  <span data-ttu-id="afbe1-815">_**Rysunek nr 33:** ustawić atrybutów zabezpieczeń powitania dla obiekt nazwy klastra hello na powitania pliku udziału kworum_</span><span class="sxs-lookup"><span data-stu-id="afbe1-815">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="afbe1-816"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Ustaw kworum monitora udziału plików hello w Menedżerze klastra trybu Failover</span><span class="sxs-lookup"><span data-stu-id="afbe1-816"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="afbe1-817">Otwórz hello Konfigurowanie kworum ustawienia kreatora.</span><span class="sxs-lookup"><span data-stu-id="afbe1-817">Open hello Configure Quorum Setting Wizard.</span></span>

  ![Rysunek 34: Start hello kreatora ustawienia kworum klastra konfiguracji][sap-ha-guide-figure-3023]

  <span data-ttu-id="afbe1-819">_**Rysunek 34:** Start hello kreatora ustawienia konfiguracji kworum klastra_</span><span class="sxs-lookup"><span data-stu-id="afbe1-819">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="afbe1-820">Na powitania **wybrać konfigurację kworum** wybierz **Wybieranie monitora kworum hello**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-820">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![Rysunek 35: Konfiguracji kworum, możesz wybrać z][sap-ha-guide-figure-3024]

  <span data-ttu-id="afbe1-822">_**Rysunek 35:** konfiguracji kworum, możesz wybrać spośród_</span><span class="sxs-lookup"><span data-stu-id="afbe1-822">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="afbe1-823">Na powitania **Wybieranie monitora kworum** wybierz **Konfigurowanie monitora udziału plików**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-823">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![36 rysunku: Monitor udziału plików wybierz hello][sap-ha-guide-figure-3025]

  <span data-ttu-id="afbe1-825">_**Rysunek 36:** Wybierz monitor udziału plików hello_</span><span class="sxs-lookup"><span data-stu-id="afbe1-825">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="afbe1-826">Wprowadź udziału plików toohello ścieżki UNC hello (w naszym przykładzie \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="afbe1-826">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="afbe1-827">toosee listę hello zmiany mogą być, wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-827">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![Rysunek 37: Zdefiniuj lokalizację udziału plików hello hello monitora udziału][sap-ha-guide-figure-3026]

  <span data-ttu-id="afbe1-829">_**Rysunek 37:** określić lokalizację udziału plików hello hello monitora udziału_</span><span class="sxs-lookup"><span data-stu-id="afbe1-829">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="afbe1-830">Wybierz hello zmiany, a następnie wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-830">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="afbe1-831">Należy toosuccessfully ponownie skonfigurować hello konfiguracji klastra, jak pokazano na rysunku 38.</span><span class="sxs-lookup"><span data-stu-id="afbe1-831">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![38 rysunku: Czy został ponownie skonfigurować klaster hello potwierdzenie][sap-ha-guide-figure-3027]

  <span data-ttu-id="afbe1-833">_**Rysunek 38:** potwierdzenie, że zostały ponownie skonfigurować hello klastra_</span><span class="sxs-lookup"><span data-stu-id="afbe1-833">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="afbe1-834">Po pomyślnym zainstalowaniu klastra pracy awaryjnej systemu Windows hello zmiany muszą toobe wprowadzone toosome progi tooadapt pracy awaryjnej wykrywania tooconditions na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-834">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="afbe1-835">Hello zmienić toobe parametry są opisane w tym blogu: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/.</span><span class="sxs-lookup"><span data-stu-id="afbe1-835">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="afbe1-836">Przy założeniu, że dwóch maszyn wirtualnych, które kompilacji hello konfiguracji klastra systemu Windows dla ASCS/SCS znajdują się w hello tej samej podsieci, hello następujące parametry muszą zmienić toobe toothese wartości:</span><span class="sxs-lookup"><span data-stu-id="afbe1-836">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="afbe1-837">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="afbe1-837">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="afbe1-838">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="afbe1-838">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="afbe1-839">Te ustawienia zostały przetestowane z klientami i dostępne toobe dobrej naruszenia wystarczająco odporne na jednej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="afbe1-839">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="afbe1-840">Na powitania drugiej te ustawienia zostały udostępnianie fast wystarczająco dużo pracy awaryjnej w warunkach rzeczywistych błędu w przypadku awarii oprogramowania lub węzeł/wirtualna SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-840">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="afbe1-841"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Zainstaluj dla dysku udziału klastra SAP ASCS/SCS hello SIOS DataKeeper Cluster Edition</span><span class="sxs-lookup"><span data-stu-id="afbe1-841"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="afbe1-842">Masz teraz pracy konfiguracji klastra trybu Failover systemu Windows Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-842">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="afbe1-843">Jednak tooinstall wystąpieniem SAP ASCS/SCS należy zasób udostępniony dysk.</span><span class="sxs-lookup"><span data-stu-id="afbe1-843">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="afbe1-844">Nie można utworzyć potrzebne zasoby dysku udostępnionego hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-844">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="afbe1-845">SIOS DataKeeper Cluster Edition jest rozwiązań innych firm, można użyć toocreate współużytkowane zasoby dyskowe.</span><span class="sxs-lookup"><span data-stu-id="afbe1-845">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="afbe1-846">Instalowanie SIOS DataKeeper Cluster Edition dla programu SAP ASCS/SCS hello dysku klastrowego udziału obejmuje te zadania:</span><span class="sxs-lookup"><span data-stu-id="afbe1-846">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="afbe1-847">Dodawanie hello .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="afbe1-847">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="afbe1-848">Instalowanie SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="afbe1-848">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="afbe1-849">Konfigurowanie SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="afbe1-849">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="afbe1-850"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Dodaj hello .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="afbe1-850"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="afbe1-851">Hello Microsoft .NET Framework 3.5 nie jest automatycznie aktywowane lub zainstalowany w systemie Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="afbe1-851">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="afbe1-852">SIOS DataKeeper wymaga hello toobe .NET Framework na wszystkich węzłach, które należy zainstalować na DataKeeper, dlatego należy zainstalować w systemie operacyjnym gościa hello wszystkich maszyn wirtualnych w klastrze hello hello .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="afbe1-852">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="afbe1-853">Istnieją dwa sposoby hello tooadd .NET Framework 3.5:</span><span class="sxs-lookup"><span data-stu-id="afbe1-853">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="afbe1-854">Użyj Kreatora hello dodawania ról i funkcji w systemie Windows, jak pokazano 39 rysunku.</span><span class="sxs-lookup"><span data-stu-id="afbe1-854">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![Rysunek 39: Zainstaluj hello .NET Framework 3.5 przy użyciu hello dodawania ról i funkcji — Kreator][sap-ha-guide-figure-3028]

  <span data-ttu-id="afbe1-856">_**Rysunek 39:** hello instalacji programu .NET Framework 3.5 przy użyciu hello dodawania ról i funkcji — Kreator_</span><span class="sxs-lookup"><span data-stu-id="afbe1-856">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![40 rysunek: Postęp instalacji pasek po zainstalowaniu hello .NET Framework 3.5 przy użyciu hello dodawania ról i funkcji — Kreator][sap-ha-guide-figure-3029]

  <span data-ttu-id="afbe1-858">_**Rysunek 40:** pasek po zainstalowaniu hello .NET Framework 3.5 przy użyciu hello dodawania ról i funkcji — Kreator postępu instalacji_</span><span class="sxs-lookup"><span data-stu-id="afbe1-858">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="afbe1-859">Użyj hello narzędzia wiersza polecenia dism.exe.</span><span class="sxs-lookup"><span data-stu-id="afbe1-859">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="afbe1-860">Ten typ instalacji należy katalogu SxS hello tooaccess na powitania nośnik instalacyjny systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="afbe1-860">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="afbe1-861">W wierszu polecenia z podwyższonym poziomem uprawnień wpisz polecenie:</span><span class="sxs-lookup"><span data-stu-id="afbe1-861">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="afbe1-862"><a name="dd41d5a2-8083-415b-9878-839652812102"></a>Zainstaluj SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="afbe1-862"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="afbe1-863">Zainstaluj SIOS DataKeeper Cluster Edition w każdym węźle w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-863">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="afbe1-864">toocreate wirtualnego magazynu udostępnionego SIOS DataKeeper Tworzenie zsynchronizowanej dublowania i następnie symulować magazyn udostępniony klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-864">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="afbe1-865">Przed zainstalowaniem oprogramowania SIOS hello, Utwórz użytkownika domeny hello **DataKeeperSvc**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-865">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="afbe1-866">Dodaj hello **DataKeeperSvc** toohello użytkownika **administratora lokalnego** na obu węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-866">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="afbe1-867">tooinstall SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="afbe1-867">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="afbe1-868">Zainstaluj oprogramowanie SIOS hello na obu węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-868">Install hello SIOS software on both cluster nodes.</span></span>

  ![Instalator SIOS][sap-ha-guide-figure-3030]

  ![41 rysunku: Pierwsza strona hello instalacji SIOS DataKeeper][sap-ha-guide-figure-3031]

  <span data-ttu-id="afbe1-871">_**Rysunek 41:** pierwszej strony hello SIOS DataKeeper instalacji_</span><span class="sxs-lookup"><span data-stu-id="afbe1-871">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="afbe1-872">Okno dialogowe hello pokazano na rysunku 42, wybierz **tak**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-872">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![Rysunek 42: DataKeeper informuje, czy usługa zostanie wyłączona][sap-ha-guide-figure-3032]

  <span data-ttu-id="afbe1-874">_**Rysunek 42:** DataKeeper informuje, że usługa zostanie wyłączona_</span><span class="sxs-lookup"><span data-stu-id="afbe1-874">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="afbe1-875">Okno dialogowe hello pokazano na rysunku 43, zalecane w wybranym **konta domeny lub tego serwera**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-875">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![Rysunek 43: Wybór użytkownika dla SIOS DataKeeper][sap-ha-guide-figure-3033]

  <span data-ttu-id="afbe1-877">_**Rysunek 43:** SIOS DataKeeper określonego użytkownika_</span><span class="sxs-lookup"><span data-stu-id="afbe1-877">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="afbe1-878">Wprowadź nazwę hello domeny konta użytkownika i hasła, które zostały utworzone dla SIOS DataKeeper.</span><span class="sxs-lookup"><span data-stu-id="afbe1-878">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Rysunek 44: Wprowadź hello domena, nazwa użytkownika i hasło dla hello SIOS DataKeeper instalacji][sap-ha-guide-figure-3034]

  <span data-ttu-id="afbe1-880">_**Rysunek 44:** wprowadź nazwę użytkownika domeny hello i hasło dla hello SIOS DataKeeper instalacji_</span><span class="sxs-lookup"><span data-stu-id="afbe1-880">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="afbe1-881">Zainstaluj klucz licencji powitania dla swojego wystąpienia SIOS DataKeeper, jak pokazano na rysunku 45.</span><span class="sxs-lookup"><span data-stu-id="afbe1-881">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![Rysunek 45: Wprowadź klucz licencji SIOS DataKeeper][sap-ha-guide-figure-3035]

  <span data-ttu-id="afbe1-883">_**Rysunek 45:** wprowadź klucz licencji SIOS DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="afbe1-883">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="afbe1-884">Po wyświetleniu monitu uruchom ponownie maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-884">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="afbe1-885"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a>Konfigurowanie SIOS DataKeeper</span><span class="sxs-lookup"><span data-stu-id="afbe1-885"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="afbe1-886">Po zainstalowaniu SIOS DataKeeper na obu węzłach należy toostart hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="afbe1-886">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="afbe1-887">Celem Hello konfiguracji hello jest toohave synchroniczne dane replikacji między hello dodatkowych dysków dołączonych tooeach hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-887">hello goal of hello configuration is toohave synchronous data replication between hello additional disks attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="afbe1-888">Uruchom hello DataKeeper zarządzanie i narzędzia do konfiguracji, a następnie wybierz **połączenia serwera**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-888">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="afbe1-889">(W 46 rysunku, ta opcja jest zaznaczona kółkiem na czerwono.)</span><span class="sxs-lookup"><span data-stu-id="afbe1-889">(In Figure 46, this option is circled in red.)</span></span>

  ![Rysunek 46: SIOS DataKeeper zarządzanie i narzędzia do konfiguracji][sap-ha-guide-figure-3036]

  <span data-ttu-id="afbe1-891">_**Rysunek 46:** narzędzie SIOS DataKeeper zarządzania i konfiguracji_</span><span class="sxs-lookup"><span data-stu-id="afbe1-891">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="afbe1-892">Wprowadź nazwę hello lub adres TCP/IP hello pierwszy węzeł hello zarządzania i konfiguracji narzędzia powinny połączenia oraz, w drugim kroku hello drugiego węzła.</span><span class="sxs-lookup"><span data-stu-id="afbe1-892">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![Rysunek 47: Wstaw hello nazwę lub adres TCP/IP hello pierwszy węzeł hello zarządzania i konfiguracji narzędzia należy łączyć, a w drugim etapie hello drugiego węzła][sap-ha-guide-figure-3037]

  <span data-ttu-id="afbe1-894">_**Rysunek 47:** Insert hello nazwę lub adres TCP/IP hello pierwszy węzeł hello zarządzania i konfiguracji narzędzia należy łączyć, a w drugim etapie hello drugiego węzła_</span><span class="sxs-lookup"><span data-stu-id="afbe1-894">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="afbe1-895">Utwórz zadanie replikacji hello między dwoma węzłami hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-895">Create hello replication job between hello two nodes.</span></span>

  ![Rysunek 48: Tworzenie zadania replikacji][sap-ha-guide-figure-3038]

  <span data-ttu-id="afbe1-897">_**Rysunek 48:** Utwórz zadanie replikacji_</span><span class="sxs-lookup"><span data-stu-id="afbe1-897">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="afbe1-898">Kreator prowadzi hello proces tworzenia zadania replikacji.</span><span class="sxs-lookup"><span data-stu-id="afbe1-898">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="afbe1-899">Zdefiniuj hello nazwa, adres TCP/IP i wolumin dysku hello źródło węzła.</span><span class="sxs-lookup"><span data-stu-id="afbe1-899">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![Rysunek 49: Zdefiniuj nazwę hello hello zadania replikacji][sap-ha-guide-figure-3039]

  <span data-ttu-id="afbe1-901">_**Rysunek 49:** Zdefiniuj nazwę hello hello replikacji zadania_</span><span class="sxs-lookup"><span data-stu-id="afbe1-901">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![Rysunek 50: Zdefiniuj hello danych podstawowych dla węzła hello, która powinna być hello bieżącego węzła źródłowego][sap-ha-guide-figure-3040]

  <span data-ttu-id="afbe1-903">_**Rysunek 50:** zdefiniować hello podstawowe dane dla węzła hello, która powinna być hello bieżącego węzła źródłowego_</span><span class="sxs-lookup"><span data-stu-id="afbe1-903">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="afbe1-904">Zdefiniuj nazwę hello, adres TCP/IP i wolumin dysku hello docelowego węzła.</span><span class="sxs-lookup"><span data-stu-id="afbe1-904">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![Rysunek 51: Zdefiniuj hello danych podstawowych dla węzła hello, która powinna być hello bieżący węzeł docelowy.][sap-ha-guide-figure-3041]

  <span data-ttu-id="afbe1-906">_**Rysunek 51:** zdefiniować hello podstawowe dane dla węzła hello, która powinna być hello bieżący węzeł docelowy._</span><span class="sxs-lookup"><span data-stu-id="afbe1-906">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="afbe1-907">Zdefiniuj hello algorytmy kompresji.</span><span class="sxs-lookup"><span data-stu-id="afbe1-907">Define hello compression algorithms.</span></span> <span data-ttu-id="afbe1-908">W naszym przykładzie zaleca się, że kompresji hello replikacji strumienia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-908">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="afbe1-909">Szczególnie w sytuacjach, ponowna synchronizacja kompresji hello strumienia replikacji hello znacznie skraca czas ponownej synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="afbe1-909">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="afbe1-910">Należy pamiętać, że kompresja używa zasobów Procesora i pamięci RAM hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afbe1-910">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="afbe1-911">Jako hello kompresji szybkość wzrostu tak hello ilości zasobów procesora CPU używanych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-911">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="afbe1-912">Można również dostosować to ustawienie później.</span><span class="sxs-lookup"><span data-stu-id="afbe1-912">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="afbe1-913">Inny ustawienie konieczne jest toocheck czy hello replikacji asynchronicznie lub synchronicznie.</span><span class="sxs-lookup"><span data-stu-id="afbe1-913">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="afbe1-914">*W przypadku ochrony SAP ASCS/SCS konfiguracji, należy użyć Replikacja synchroniczna*.</span><span class="sxs-lookup"><span data-stu-id="afbe1-914">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![Rysunek 52: Zdefiniuj szczegóły replikacji][sap-ha-guide-figure-3042]

  <span data-ttu-id="afbe1-916">_**Rysunek 52:** Zdefiniuj szczegóły replikacji_</span><span class="sxs-lookup"><span data-stu-id="afbe1-916">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="afbe1-917">Należy określić, czy hello wolumin, który jest replikowany za zadanie replikacji hello powinny być reprezentowana tooa Windows Server Failover Clustering konfiguracji klastra jako udostępniony dysk.</span><span class="sxs-lookup"><span data-stu-id="afbe1-917">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="afbe1-918">Witaj SAP ASCS/SCS konfiguracji, wybierz **tak** , dzięki czemu widzi klastra Windows hello hello replikowanego woluminu jako udostępnionego dysku, której można użyć jako woluminu klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-918">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![Rysunek 53: Wybierz tak tooset hello replikowane wolumin jako wolumin klastra][sap-ha-guide-figure-3043]

  <span data-ttu-id="afbe1-920">_**Rysunek 53:** wybierz **tak** tooset hello replikowane jako woluminu klastra_</span><span class="sxs-lookup"><span data-stu-id="afbe1-920">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="afbe1-921">Po utworzeniu woluminu hello hello DataKeeper zarządzania i konfiguracji narzędzia przedstawia zadania replikacji hello jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="afbe1-921">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![Rysunek 54: DataKeeper duplikowanie synchroniczne dla hello SAP ASCS/SCS udziału dysku jest aktywny][sap-ha-guide-figure-3044]

  <span data-ttu-id="afbe1-923">_**Rysunek 54:** DataKeeper duplikowanie synchroniczne dla hello SAP ASCS/SCS współużytkować dysku jest aktywny_</span><span class="sxs-lookup"><span data-stu-id="afbe1-923">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="afbe1-924">Menedżer klastra trybu failover zawiera obecnie hello dysku jako dysku DataKeeper, jak pokazano na rysunku 55.</span><span class="sxs-lookup"><span data-stu-id="afbe1-924">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![Rysunek 55: Menedżer klastra trybu Failover zawiera dysk hello replikowane DataKeeper][sap-ha-guide-figure-3045]

  <span data-ttu-id="afbe1-926">_**Rysunek 55:** Menedżera klastra trybu Failover zawiera dysk hello tego DataKeeper replikowane_</span><span class="sxs-lookup"><span data-stu-id="afbe1-926">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="afbe1-927"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Instalowanie systemu SAP NetWeaver hello</span><span class="sxs-lookup"><span data-stu-id="afbe1-927"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="afbe1-928">Instalator systemu DBMS hello nie opisano ustawienia się różnić w zależności od używanego systemu DBMS hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-928">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="afbe1-929">Jednak przyjęto założenie, że dotyczy wysokiej dostępności z systemu DBMS hello są adresowane za pomocą funkcje hello, obsługiwanych przez różnych dostawców DBMS hello Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-929">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="afbe1-930">Na przykład zawsze włączone lub dublowania bazy danych programu SQL Server i Oracle Data Guard dla baz danych Oracle.</span><span class="sxs-lookup"><span data-stu-id="afbe1-930">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="afbe1-931">W scenariuszu hello używanych w tym artykule firma Microsoft nie dodał więcej toohello ochrony systemu DBMS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-931">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="afbe1-932">Istnieją specjalne uwagi dotyczące różnych usług systemu DBMS interakcji z tego rodzaju konfiguracji klastra SAP ASCS/SCS na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-932">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="afbe1-933">procedury instalacji Hello programu SAP NetWeaver ABAP systemów, Java i systemami ABAP + Java są prawie takie same.</span><span class="sxs-lookup"><span data-stu-id="afbe1-933">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="afbe1-934">najbardziej znacząca różnica Hello jest systemu SAP ABAP jedno wystąpienie ASCS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-934">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="afbe1-935">Witaj systemu SAP Java ma jedno wystąpienie SCS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-935">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="afbe1-936">Witaj systemu SAP ABAP + Java ma jedno wystąpienie ASCS i działania jednej wystąpienia SCS hello tej samej grupy klastra trybu failover firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="afbe1-936">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="afbe1-937">Różnice instalacji dla każdej stosu instalacji SAP NetWeaver jawnie wymienione.</span><span class="sxs-lookup"><span data-stu-id="afbe1-937">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="afbe1-938">Można założyć, wszystkie inne elementy są hello takie same.</span><span class="sxs-lookup"><span data-stu-id="afbe1-938">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="afbe1-939"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a>Instalowanie programu SAP przy użyciu wystąpienia ASCS/SCS wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="afbe1-939"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afbe1-940">Upewnij się, nie tooplace ze strony plików na DataKeeper dublowanych woluminów.</span><span class="sxs-lookup"><span data-stu-id="afbe1-940">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="afbe1-941">DataKeeper nie obsługuje woluminy dublowane.</span><span class="sxs-lookup"><span data-stu-id="afbe1-941">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="afbe1-942">Można pozostawić pliku stronicowania na powitania tymczasowego dysku D z maszyny wirtualnej platformy Azure, który jest domyślnym hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-942">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="afbe1-943">Jeśli nie jest już istnieje, należy przenieść hello Windows strony pliku toodrive D: Azure maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afbe1-943">If it's not already there, move hello Windows page file toodrive D: of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="afbe1-944">Instalowanie SAP przy użyciu wystąpienia ASCS/SCS wysokiej dostępności obejmuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="afbe1-944">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="afbe1-945">Tworzenie nazwę hosta wirtualnego wystąpienia programu SAP ASCS/SCS hello w klastrze</span><span class="sxs-lookup"><span data-stu-id="afbe1-945">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="afbe1-946">Instalowanie programu SAP hello pierwszym węźle klastra</span><span class="sxs-lookup"><span data-stu-id="afbe1-946">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="afbe1-947">Modyfikowanie profilu SAP hello hello ASCS/SCS wystąpienia</span><span class="sxs-lookup"><span data-stu-id="afbe1-947">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="afbe1-948">Dodawanie portu sondy</span><span class="sxs-lookup"><span data-stu-id="afbe1-948">Adding a probe port</span></span>
- <span data-ttu-id="afbe1-949">Otwarcie portu sondowania zapory systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="afbe1-949">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="afbe1-950"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Utwórz nazwę hosta wirtualnego wystąpienia programu SAP ASCS/SCS hello w klastrze</span><span class="sxs-lookup"><span data-stu-id="afbe1-950"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="afbe1-951">W Menedżerze DNS z systemem Windows hello Utwórz wpis DNS dla nazwy hostów wirtualnych hello hello ASCS/SCS wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-951">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="afbe1-952">Witaj adres IP, który można przypisać nazwę hosta wirtualnego toohello hello ASCS/SCS wystąpienie musi być hello sam jako adres IP hello przypisania tooAzure modułu równoważenia obciążenia (**<*SID*> - lb - ascs **).</span><span class="sxs-lookup"><span data-stu-id="afbe1-952">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="afbe1-953">Witaj adresu IP wirtualnej nazwy hosta SAP ASCS/SCS hello (**pr1 ascs sap**) jest hello takie same jak hello adresu IP usługi równoważenia obciążenia Azure (**pr1-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="afbe1-953">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Rysunek 56: Definiowanie hello wpisu DNS dla nazwy wirtualnego hello SAP ASCS/SCS klastra i adres TCP/IP][sap-ha-guide-figure-3046]

  <span data-ttu-id="afbe1-955">_**Rysunek 56:** zdefiniuj hello wpisu DNS dla nazwy wirtualnego hello SAP ASCS/SCS klastra i adres TCP/IP_</span><span class="sxs-lookup"><span data-stu-id="afbe1-955">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="afbe1-956">toodefine hello nazwę adresów IP przypisanych toohello hostów wirtualnych, wybierz **Menedżera DNS** > **domeny**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-956">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![57 rysunek: Nowa nazwa wirtualnego i adres TCP/IP dla konfiguracji klastra SAP ASCS/SCS][sap-ha-guide-figure-3047]

  <span data-ttu-id="afbe1-958">_**Rysunek 57:** nową nazwę wirtualnego i TCP/IP adresów dla SAP ASCS/SCS konfiguracji klastra_</span><span class="sxs-lookup"><span data-stu-id="afbe1-958">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="afbe1-959"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Zainstaluj hello SAP pierwszym węźle klastra</span><span class="sxs-lookup"><span data-stu-id="afbe1-959"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="afbe1-960">Wykonanie opcję hello do węzła pierwszego klastra w węźle klastra A. Na przykład na powitania **pr1 ascs 0** hosta.</span><span class="sxs-lookup"><span data-stu-id="afbe1-960">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="afbe1-961">porty domyślne hello tookeep hello Azure wewnętrznego modułu równoważenia obciążenia, wybierz:</span><span class="sxs-lookup"><span data-stu-id="afbe1-961">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="afbe1-962">**ABAP system**: **ASCS** wystąpienie numer **00**</span><span class="sxs-lookup"><span data-stu-id="afbe1-962">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="afbe1-963">**Java system**: **SCS** wystąpienie numer **01**</span><span class="sxs-lookup"><span data-stu-id="afbe1-963">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="afbe1-964">**System ABAP + Java**: **ASCS** wystąpienie numer **00** i **SCS** wystąpienie numer **01**</span><span class="sxs-lookup"><span data-stu-id="afbe1-964">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="afbe1-965">wystąpienie toouse innych niż 00 hello ABAP ASCS liczb, wystąpienia i 01 hello Java SCS wystąpienia, należy najpierw toochange hello Azure obciążenia wewnętrznego domyślne równoważenia obciążenia modułu równoważenia reguł, opisanych w [zmiany hello ASCS/SCS domyślne obciążenia Równoważenie zasady hello Azure wewnętrznego modułu równoważenia obciążenia][sap-ha-guide-8.9].</span><span class="sxs-lookup"><span data-stu-id="afbe1-965">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="afbe1-966">Witaj dalej kilka zadań nie są opisane w hello standardowe SAP instalacji dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="afbe1-966">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="afbe1-967">Hello SAP instalacji dokumentacji opisano, jak tooinstall hello pierwszym węźle klastra ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="afbe1-967">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="afbe1-968"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modyfikowanie profilu SAP hello hello ASCS/SCS wystąpienia</span><span class="sxs-lookup"><span data-stu-id="afbe1-968"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="afbe1-969">Należy tooadd nowy parametr profilu.</span><span class="sxs-lookup"><span data-stu-id="afbe1-969">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="afbe1-970">Parametr profilu Hello zapobiega połączeń między procesów roboczych SAP i hello umieścić serwer zamykania po okresie bezczynności wynoszącym zbyt długo.</span><span class="sxs-lookup"><span data-stu-id="afbe1-970">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="afbe1-971">Wspomniano hello scenariusz problemu w [dodać wpisów rejestru na obu węzłach hello SAP ASCS/SCS wystąpienia][sap-ha-guide-8.11].</span><span class="sxs-lookup"><span data-stu-id="afbe1-971">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="afbe1-972">W tej sekcji wprowadzono są również dwie zmiany toosome podstawowe TCP/IP Parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-972">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="afbe1-973">W drugim kroku należy tooset hello umieścić serwer toosend `keep_alive` sygnału, dzięki czemu hello połączeń nie osiągnął Próg bezczynności hello Azure wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-973">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="afbe1-974">Witaj toomodify profilu SAP wystąpienia ASCS/SCS hello:</span><span class="sxs-lookup"><span data-stu-id="afbe1-974">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="afbe1-975">Dodaj ten profil parametru toohello SAP ASCS/SCS wystąpienia profilu:</span><span class="sxs-lookup"><span data-stu-id="afbe1-975">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="afbe1-976">W naszym przykładzie ścieżka hello jest:</span><span class="sxs-lookup"><span data-stu-id="afbe1-976">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="afbe1-977">Na przykład toohello SAP SCS wystąpienia profilu i odpowiednie ścieżki:</span><span class="sxs-lookup"><span data-stu-id="afbe1-977">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="afbe1-978">tooapply hello zmiany, ponownie uruchom wystąpienie /SCS SAP ASCS hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-978">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="afbe1-979"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a>Dodaj port sondy</span><span class="sxs-lookup"><span data-stu-id="afbe1-979"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="afbe1-980">Używać funkcji hello wewnętrznego modułu równoważenia obciążenia sondowania funkcji toomake hello całego klastra konfiguracji Praca z modułem równoważenia obciążenia w Azure.</span><span class="sxs-lookup"><span data-stu-id="afbe1-980">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="afbe1-981">Hello Azure wewnętrznego modułu równoważenia obciążenia zwykle rozdziela przychodzące obciążenie hello równomiernie w poszczególnych uczestniczących maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afbe1-981">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="afbe1-982">Jednak to nie będzie działać w niektórych konfiguracjach klastra, ponieważ jest aktywna tylko jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="afbe1-982">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="afbe1-983">Hello inne wystąpienie jest w stanie pasywnym i nie akceptuje dowolne hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="afbe1-983">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="afbe1-984">Funkcja badania pomaga przypisuje usługi równoważenia obciążenia Azure wewnętrzny hello działa tylko tooan aktywnym wystąpieniu.</span><span class="sxs-lookup"><span data-stu-id="afbe1-984">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="afbe1-985">Z funkcją sondowania hello hello wewnętrznego modułu równoważenia obciążenia może wykryć, które wystąpienia są aktywne, a następnie tylko hello wystąpienia z obciążenia hello docelowego.</span><span class="sxs-lookup"><span data-stu-id="afbe1-985">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="afbe1-986">port sondy tooadd:</span><span class="sxs-lookup"><span data-stu-id="afbe1-986">tooadd a probe port:</span></span>

1.  <span data-ttu-id="afbe1-987">Sprawdź bieżący hello **ProbePort** ustawienie, uruchamiając następujące polecenia programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-987">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="afbe1-988">Wykonanie go z jednej z maszyn wirtualnych hello w konfiguracji klastra hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-988">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="afbe1-989">Zdefiniuj port sondy.</span><span class="sxs-lookup"><span data-stu-id="afbe1-989">Define a probe port.</span></span> <span data-ttu-id="afbe1-990">Witaj domyślny numer portu sondy jest **0**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-990">hello default probe port number is **0**.</span></span> <span data-ttu-id="afbe1-991">W tym przykładzie używamy port sondy **62000**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-991">In our example, we use probe port **62000**.</span></span>

  ![Rysunek 58: port sondy konfiguracji klastra hello jest 0 domyślnie][sap-ha-guide-figure-3048]

  <span data-ttu-id="afbe1-993">_**Rysunek 58:** port sondy konfiguracji klastra domyślne hello wynosi 0_</span><span class="sxs-lookup"><span data-stu-id="afbe1-993">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="afbe1-994">numer portu Hello jest zdefiniowany w szablonach SAP usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="afbe1-994">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="afbe1-995">Można przypisać numer portu hello w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afbe1-995">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="afbe1-996">tooset nową wartość ProbePort hello  **SAP <*SID*> IP ** zasobu klastra, uruchom hello następującego skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afbe1-996">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="afbe1-997">Zaktualizuj hello zmiennych środowiska PowerShell dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="afbe1-997">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="afbe1-998">Po uruchomieniu skryptu hello się, zostanie wyświetlony monit o toorestart hello SAP grupy tooactivate hello zmiany dotyczące klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-998">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

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
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

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

  <span data-ttu-id="afbe1-999">Po przełączeniu hello  **SAP <*SID*> ** klastra roli w tryb online, upewnij się, że **ProbePort** ustawiono toohello nową wartość.</span><span class="sxs-lookup"><span data-stu-id="afbe1-999">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Rysunek 59: Sondowania hello portu klastra po ustawieniu hello nowej wartości][sap-ha-guide-figure-3049]

  <span data-ttu-id="afbe1-1001">_**Rysunek 59:** sondowania portu klastra powitania po ustawieniu hello nowej wartości_</span><span class="sxs-lookup"><span data-stu-id="afbe1-1001">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="afbe1-1002"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Otwórz port sondy zapory systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="afbe1-1002"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="afbe1-1003">Należy tooopen port sondy zapory systemu Windows na obu węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1003">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="afbe1-1004">Użyj następującego skryptu tooopen port sondy zapory systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1004">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="afbe1-1005">Zaktualizuj hello zmiennych środowiska PowerShell dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1005">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="afbe1-1006">Witaj **ProbePort** ustawiono zbyt**62000**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1006">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="afbe1-1007">Teraz można dostęp do udziału plików hello  **\\\ascsha-clsap\sapmnt** od innych hostów, takie jak z **ascsha dbas**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1007">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="afbe1-1008"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Zainstaluj hello wystąpienia bazy danych</span><span class="sxs-lookup"><span data-stu-id="afbe1-1008"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="afbe1-1009">Baza danych hello tooinstall wystąpienia, należy wykonać hello procesu opisanego w hello dokumentacji instalacji SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1009">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="afbe1-1010"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Zainstaluj hello drugiego węzła klastra</span><span class="sxs-lookup"><span data-stu-id="afbe1-1010"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="afbe1-1011">tooinstall hello drugi klaster, wykonaj kroki hello hello SAP w podręczniku instalacji.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1011">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="afbe1-1012"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Zmień typ uruchomienia hello wystąpienie usługi SAP Wywołujących Windows hello</span><span class="sxs-lookup"><span data-stu-id="afbe1-1012"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="afbe1-1013">Zmień typ uruchamiania usługi SAP Wywołujących Windows hello hello zbyt**automatycznie (opóźnione uruchomienie)** na obu węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1013">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![Rysunek 60: Zmień typ usługi hello hello Wywołujących SAP wystąpienia toodelayed automatyczne][sap-ha-guide-figure-3050]

<span data-ttu-id="afbe1-1015">_**Rysunek 60:** zmienić typ usługi hello hello Wywołujących SAP wystąpienia toodelayed automatyczne_</span><span class="sxs-lookup"><span data-stu-id="afbe1-1015">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="afbe1-1016"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Zainstaluj hello SAP podstawowego serwera aplikacji</span><span class="sxs-lookup"><span data-stu-id="afbe1-1016"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="afbe1-1017">Zainstaluj wystąpienie serwera aplikacji głównej (adresy) hello <*SID*> - podpisane - 0 na maszynie wirtualnej hello, który został wybrany toohost hello adresy dostawcy.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1017">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="afbe1-1018">Nie ma żadnych zależności, Azure lub DataKeeper określonych ustawień.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1018">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="afbe1-1019"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Zainstaluj hello SAP dodatkowego serwera aplikacji</span><span class="sxs-lookup"><span data-stu-id="afbe1-1019"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="afbe1-1020">Zainstaluj SAP dodatkowych aplikacji serwera (AAS) na wszystkich maszynach wirtualnych hello, że ustawiono toohost wystąpienia serwera aplikacji SAP.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1020">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="afbe1-1021">Na przykład na <*SID*> - podpisane - 1 za <*SID*> - podpisane -&lt;n&gt;.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1021">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="afbe1-1022">Zakończy się instalacja hello systemu SAP NetWeaver wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1022">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="afbe1-1023">Następnie należy kontynuować testowanie trybu failover.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1023">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="afbe1-1024"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Testowanie trybu failover wystąpienia programu SAP ASCS/SCS hello i SIOS replikacji</span><span class="sxs-lookup"><span data-stu-id="afbe1-1024"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="afbe1-1025">Jest łatwy tootest i monitorowanie trybu failover wystąpienia programu SAP ASCS/SCS i replikacji dysku SIOS za pomocą Menedżera klastra trybu Failover i narzędzia hello SIOS DataKeeper zarządzania i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1025">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="afbe1-1026"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a>W węźle klastra, A jest uruchomione wystąpienie SAP ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="afbe1-1026"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="afbe1-1027">Witaj **SAP PR1** grupy klastra jest uruchomiona w węźle klastra A. Na przykład na **pr1 ascs 0**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1027">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="afbe1-1028">Przypisz hello udostępnionego dysku S, który jest częścią hello **SAP PR1** grupy i które wystąpienie ASCS/SCS hello używa toocluster A. węzła klastra</span><span class="sxs-lookup"><span data-stu-id="afbe1-1028">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![61 rysunek: Menedżer klastra trybu Failover: Grupa klastra SAP < SID > hello jest uruchomiona w węźle klastra, A][sap-ha-guide-figure-5000]

<span data-ttu-id="afbe1-1030">_**Rysunek 61:** Menedżera klastra trybu Failover: hello SAP <*SID*> grupy klastra jest uruchomiona w węźle klastra, A_</span><span class="sxs-lookup"><span data-stu-id="afbe1-1030">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="afbe1-1031">Witaj SIOS DataKeeper zarządzanie i narzędzia do konfiguracji zawiera tego hello dysk udostępniony, który dane są replikowane synchronicznie w z dysku woluminu źródłowego hello S w węźle klastra toohello dysku woluminu docelowego S w węźle klastra B. Na przykład są replikowane z **pr1 ascs 0 [10.0.0.40]** za**pr1 ascs 1 [10.0.0.41]**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1031">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![Rysunek 62: W SIOS DataKeeper replikowane woluminu lokalne powitania z węzła z klastra węzeł toocluster B][sap-ha-guide-figure-5001]

<span data-ttu-id="afbe1-1033">_**Rysunek 62:** w SIOS DataKeeper replikowane woluminu lokalne powitania z węzła z klastra węzeł toocluster B_</span><span class="sxs-lookup"><span data-stu-id="afbe1-1033">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="afbe1-1034"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Tryb failover z węzła A toonode B</span><span class="sxs-lookup"><span data-stu-id="afbe1-1034"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="afbe1-1035">Wybierz jedną z tych opcji tooinitiate awarię hello SAP <*SID*> Grupa klastra z klastra węzeł A toocluster węzeł B:</span><span class="sxs-lookup"><span data-stu-id="afbe1-1035">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="afbe1-1036">Menedżer klastra trybu Failover</span><span class="sxs-lookup"><span data-stu-id="afbe1-1036">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="afbe1-1037">Za pomocą programu PowerShell klastra trybu Failover</span><span class="sxs-lookup"><span data-stu-id="afbe1-1037">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="afbe1-1038">Uruchom ponownie, A węzeł klastra w systemie operacyjnym gościa Windows hello (powoduje to zainicjowanie automatycznej pracy awaryjnej hello SAP <*SID*> Grupa klastra z węzła A toonode B).</span><span class="sxs-lookup"><span data-stu-id="afbe1-1038">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="afbe1-1039">Uruchom ponownie, A węzeł klastra z hello portalu Azure (powoduje to zainicjowanie automatycznej pracy awaryjnej hello SAP <*SID*> Grupa klastra z węzła A toonode B).</span><span class="sxs-lookup"><span data-stu-id="afbe1-1039">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="afbe1-1040">Uruchom ponownie A węzła klastra za pomocą programu Azure PowerShell (powoduje to zainicjowanie automatycznej pracy awaryjnej hello SAP <*SID*> Grupa klastra z węzła A toonode B).</span><span class="sxs-lookup"><span data-stu-id="afbe1-1040">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="afbe1-1041">Po przejściu w tryb failover, hello SAP <*SID*> grupy klastra jest uruchomiona w węźle klastra B. Na przykład, że jest uruchomiona w **pr1 ascs 1**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1041">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![Rysunek 63: W Menedżerze klastra trybu Failover Grupa klastra SAP < SID > hello jest uruchomiona w węźle klastra B][sap-ha-guide-figure-5002]

  <span data-ttu-id="afbe1-1043">_**Rysunek 63**: W Menedżerze klastra trybu Failover, hello SAP <*SID*> grupy klastra jest uruchomiona w węźle klastra B_</span><span class="sxs-lookup"><span data-stu-id="afbe1-1043">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="afbe1-1044">Witaj udostępniony dysk jest teraz zainstalowany w klastrze węzła B. SIOS DataKeeper jest replikowanie danych z dysku woluminu źródłowego S na węzeł B tootarget woluminu dysku klastrowego S w węźle klastra A. Na przykład jest replikowany z **pr1 ascs 1 [10.0.0.41]** za**pr1 ascs 0 [10.0.0.40]**.</span><span class="sxs-lookup"><span data-stu-id="afbe1-1044">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![Rysunek 64: SIOS DataKeeper replikuje woluminu lokalne powitania z klastra węzeł B toocluster węzła A][sap-ha-guide-figure-5003]

  <span data-ttu-id="afbe1-1046">_**Rysunek 64:** SIOS DataKeeper replikuje woluminu lokalne powitania z klastra węzeł B toocluster węzeł A_</span><span class="sxs-lookup"><span data-stu-id="afbe1-1046">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>
