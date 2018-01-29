---
title: "SAP ASCS/SCS wystąpienia identyfikatora SID multi wysokiej dostępności z systemu Windows Server Failover Clustering i udostępnionego dysku na platformie Azure | Dokumentacja firmy Microsoft"
description: "Identyfikator SID Multi wysoka dostępność dla wystąpienia SAP ASCS/SCS z systemu Windows Server Failover Clustering i udostępnionego dysku na platformie Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: cbf18abe-41cb-44f7-bdec-966f32c89325
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c82cc943f983b3dedfc0f64f2eec5b4425a4bf81
ms.sourcegitcommit: 9a61faf3463003375a53279e3adce241b5700879
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2017
---
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1869038]:https://launchpad.support.sap.com/#/notes/1869038
[2287140]:https://launchpad.support.sap.com/#/notes/2287140
[2492395]:https://launchpad.support.sap.com/#/notes/2492395

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md


[sap-net-weaver-ports]:https://help.sap.com/viewer/ports
[sap-high-availability-architecture-scenarios]:sap-high-availability-architecture-scenarios.md
[sap-high-availability-guide-wsfc-shared-disk]:sap-high-availability-guide-wsfc-shared-disk.md
[sap-high-availability-guide-wsfc-file-share]:sap-high-availability-guide-wsfc-file-share.md
[sap-ascs-high-availability-multi-sid-wsfc]:sap-ascs-high-availability-multi-sid-wsfc.md
[sap-high-availability-infrastructure-wsfc-shared-disk]:sap-high-availability-infrastructure-wsfc-shared-disk.md
[sap-high-availability-installation-wsfc-shared-disk]:sap-high-availability-installation-wsfc-shared-disk.md
[sap-hana-ha]:sap-hana-high-availability.md
[sap-suse-ascs-ha]:high-availability-guide-suse.md
[sap-net-weaver-ports-ascs-scs-ports]:sap-high-availability-infrastructure-wsfc-shared-disk.md#0f3ee255-b31e-4b8a-a95a-d9ed6200468b

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

[sap-high-availability-architecture-scenarios]:sap-high-availability-architecture-scenarios.md
[sap-high-availability-guide-wsfc-shared-disk]:sap-high-availability-guide-wsfc-shared-disk.md
[sap-high-availability-guide-wsfc-file-share]:sap-high-availability-guide-wsfc-file-share.md
[sap-ascs-high-availability-multi-sid-wsfc]:sap-ascs-high-availability-multi-sid-wsfc.md
[sap-high-availability-infrastructure-wsfc-shared-disk]:sap-high-availability-infrastructure-wsfc-shared-disk.md
[sap-high-availability-infrastructure-wsfc-file-share]:sap-high-availability-infrastructure-wsfc-file-share.md

[sap-high-availability-installation-wsfc-shared-disk]:sap-high-availability-installation-wsfc-shared-disk.md
[sap-high-availability-installation-wsfc-shared-disk-install-ascs]:sap-high-availability-installation-wsfc-shared-disk.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-high-availability-installation-wsfc-shared-disk-modify-ascs-profile]:sap-high-availability-installation-wsfc-shared-disk.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556
[sap-high-availability-installation-wsfc-shared-disk-add-probe-port]:sap-high-availability-installation-wsfc-shared-disk.md#10822f4f-32e7-4871-b63a-9b86c76ce761
[sap-high-availability-installation-wsfc-shared-disk-win-firewall-probe-port]:sap-high-availability-installation-wsfc-shared-disk.md#4498c707-86c0-4cde-9c69-058a7ab8c3ac
[sap-high-availability-installation-wsfc-shared-disk-change-ers-service-startup-type]:sap-high-availability-installation-wsfc-shared-disk.md#094bc895-31d4-4471-91cc-1513b64e406a
[sap-high-availability-installation-wsfc-shared-disk-test-ascs-failover-and-sios-repl]:sap-high-availability-installation-wsfc-shared-disk.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9


[sap-high-availability-installation-wsfc-file-share]:sap-high-availability-installation-wsfc-file-share.md
[sap-high-availability-infrastructure-wsfc-shared-disk-install-sios]:sap-high-availability-infrastructure-wsfc-shared-disk.md#5c8e5482-841e-45e1-a89d-a05c0907c868

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

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

[sap-ha-guide-figure-6001]:media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png



[sap-ha-guide-figure-8001]:./media/virtual-machines-shared-sap-high-availability-guide/8001.png
[sap-ha-guide-figure-8002]:./media/virtual-machines-shared-sap-high-availability-guide/8002.png
[sap-ha-guide-figure-8003]:./media/virtual-machines-shared-sap-high-availability-guide/8003.png
[sap-ha-guide-figure-8004]:./media/virtual-machines-shared-sap-high-availability-guide/8004.png
[sap-ha-guide-figure-8005]:./media/virtual-machines-shared-sap-high-availability-guide/8005.png
[sap-ha-guide-figure-8006]:./media/virtual-machines-shared-sap-high-availability-guide/8006.png
[sap-ha-guide-figure-8007]:./media/virtual-machines-shared-sap-high-availability-guide/8007.png
[sap-ha-guide-figure-8008]:./media/virtual-machines-shared-sap-high-availability-guide/8008.png
[sap-ha-guide-figure-8009]:./media/virtual-machines-shared-sap-high-availability-guide/8009.png
[sap-ha-guide-figure-8010]:./media/virtual-machines-shared-sap-high-availability-guide/8010.png
[sap-ha-guide-figure-8011]:./media/virtual-machines-shared-sap-high-availability-guide/8011.png
[sap-ha-guide-figure-8012]:./media/virtual-machines-shared-sap-high-availability-guide/8012.png
[sap-ha-guide-figure-8013]:./media/virtual-machines-shared-sap-high-availability-guide/8013.png
[sap-ha-guide-figure-8014]:./media/virtual-machines-shared-sap-high-availability-guide/8014.png
[sap-ha-guide-figure-8015]:./media/virtual-machines-shared-sap-high-availability-guide/8015.png
[sap-ha-guide-figure-8016]:./media/virtual-machines-shared-sap-high-availability-guide/8016.png
[sap-ha-guide-figure-8017]:./media/virtual-machines-shared-sap-high-availability-guide/8017.png
[sap-ha-guide-figure-8018]:./media/virtual-machines-shared-sap-high-availability-guide/8018.png
[sap-ha-guide-figure-8019]:./media/virtual-machines-shared-sap-high-availability-guide/8019.png
[sap-ha-guide-figure-8020]:./media/virtual-machines-shared-sap-high-availability-guide/8020.png
[sap-ha-guide-figure-8021]:./media/virtual-machines-shared-sap-high-availability-guide/8021.png
[sap-ha-guide-figure-8022]:./media/virtual-machines-shared-sap-high-availability-guide/8022.png
[sap-ha-guide-figure-8023]:./media/virtual-machines-shared-sap-high-availability-guide/8023.png
[sap-ha-guide-figure-8024]:./media/virtual-machines-shared-sap-high-availability-guide/8024.png
[sap-ha-guide-figure-8025]:./media/virtual-machines-shared-sap-high-availability-guide/8025.png


[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md

# <a name="sap-ascsscs-instance-multi-sid-high-availability-with-windows-server-failover-clustering-and-shared-disk-on-azure"></a>SAP ASCS/SCS wystąpienia identyfikatora SID multi wysokiej dostępności z systemu Windows Server Failover Clustering i udostępnionego dysku na platformie Azure

> ![Windows][Logo_Windows] Windows
>

We wrześniu 2016 roku firma Microsoft wydała gdzie wielu wirtualnych adresów IP można zarządzać za pomocą funkcji [Azure wewnętrznego modułu równoważenia obciążenia][load-balancer-multivip-overview]. Ta funkcja jest już istnieje w Azure zewnętrznej usługi równoważenia obciążenia. 

W przypadku wdrożenia SAP, możesz korzystać wewnętrznego modułu równoważenia obciążenia do utworzenia konfiguracji klastra systemu Windows dla wystąpień usługi centralnej SAP (ASCS/SCS).

W tym artykule przedstawiono sposób przenoszenia z jednej instalacji ASCS/SCS do konfiguracji wielu SID SAP, instalując dodatkowe wystąpienia SAP ASCS/SCS w klastrze do istniejącego klastra systemu Windows Server Failover Clustering (WSFC) z udostępnionego dysku. Po zakończeniu tego procesu skonfigurowano SAP identyfikatora SID multi klastra.

> [!NOTE]
> Ta funkcja jest dostępna tylko w modelu wdrażania usługi Azure Resource Manager.
>
>Istnieje limit liczby prywatnych adresów IP frontonu, dla każdej platformy Azure wewnętrznego modułu równoważenia obciążenia.
>
>Maksymalna liczba wystąpień SAP ASCS/SCS w jednym klastrze usługi WSFC jest taki sam, jak maksymalna liczba prywatnych adresów IP frontonu, dla każdej platformy Azure wewnętrznego modułu równoważenia obciążenia.
>

Aby uzyskać więcej informacji na temat limitów modułu równoważenia obciążenia, zobacz sekcję "Prywatne IP frontonu dla usługi równoważenia obciążenia" w [limity sieci: usługi Azure Resource Manager][networking-limits-azure-resource-manager].

## <a name="prerequisites"></a>Wymagania wstępne

Został już skonfigurowany klaster usługi WSFC do użycia dla jednego wystąpienia SAP ASCS/SCS za pomocą **udziału plików**, jak pokazano na tym diagramie.

![Wystąpienie programu SAP ASCS/SCS wysokiej dostępności][sap-ha-guide-figure-6001]

> [!IMPORTANT]
> Instalator musi spełniać następujące warunki:
> * Wystąpienia SAP ASCS/SCS muszą współużytkować tego samego klastra usługi WSFC.
> * Każdy system zarządzania bazami danych (DBMS) identyfikatora SID musi mieć własny dedykowany klaster usługi WSFC.
> * Serwery aplikacji SAP, które należą do jednego systemu SAP identyfikatora SID musi mieć własne dedykowanych maszyn wirtualnych.

## <a name="sap-ascsscs-multi-sid-architecture-with-shared-disk"></a>Architektura identyfikatora SID multi SAP ASCS/SCS z udostępnionego dysku

Celem jest zainstalowanie wielu ASCS ABAP SAP lub SAP Java SCS klastrowanego wystąpienia tego samego klastra usługi WSFC, jako ilustrowane tutaj:

![Wiele wystąpień programu SAP ASCS/SCS klastrowanego na platformie Azure][sap-ha-guide-figure-6002]

Aby uzyskać więcej informacji na temat limitów modułu równoważenia obciążenia, zobacz sekcję "Prywatne IP frontonu dla usługi równoważenia obciążenia" w [limity sieci: usługi Azure Resource Manager][networking-limits-azure-resource-manager].

Zakończenie pozioma z dwoma systemami SAP wysokiej dostępności będzie wyglądać następująco:

![SAP wysokiej dostępności multi-SID Instalatorowi systemu SAP identyfikatorów SID][sap-ha-guide-figure-6003]

## <a name="25e358f8-92e5-4e8d-a1e5-df7580a39cb0"></a>Przygotowanie infrastruktury scenariusz identyfikatora SID multi SAP

Aby przygotować infrastrukturę, można zainstalować dodatkowe wystąpienia SAP ASCS/SCS z następującymi parametrami:

| Nazwa parametru | Wartość |
| --- | --- |
| SAP ASCS/SCS IDENTYFIKATORA SID |PR1-lb-ascs |
| System DBMS SAP wewnętrznego modułu równoważenia obciążenia | PR5 |
| Nazwa hosta wirtualnego SAP | cl-pr5-sap |
| Adres IP hosta wirtualnego SAP ASCS/SCS (adres IP usługi równoważenia obciążenia Azure dodatkowe) | 10.0.0.50 |
| SAP ASCS/SCS liczby wystąpień | 50 |
| Port sondy ILB dodatkowe wystąpienia SAP ASCS/SCS | 62350 |

> [!NOTE]
> Każdy adres IP wystąpienia klastra programu SAP ASCS/SCS, wymaga port sondy unikatowy. Na przykład jeśli jeden adres IP na Azure wewnętrznego modułu równoważenia obciążenia używa portu sondowania 62300, żaden adres IP w tej usługi równoważenia obciążenia można użyć portu sondowania 62300.
>
>W naszym celów ponieważ port sondy 62300 jest już zarezerwowany, użyto port sondy 62350.

Można zainstalować dodatkowe wystąpienia SAP ASCS/SCS w istniejącym klastrze usługi WSFC z dwoma węzłami:

| Roli maszyny wirtualnej | Nazwa hosta maszyny wirtualnej | Statyczny adres IP |
| --- | --- | --- |
| Pierwszym węźle klastra dla wystąpienia ASCS/SCS |PR1-ascs-0 |10.0.0.10 |
| Drugi węzeł klastra dla wystąpienia ASCS/SCS |PR1-ascs-1 |10.0.0.9 |

### <a name="create-a-virtual-host-name-for-the-clustered-sap-ascsscs-instance-on-the-dns-server"></a>Utwórz nazwę hosta wirtualnego wystąpienia klastra programu SAP ASCS/SCS na serwerze DNS

Można utworzyć wpis DNS dla nazwy hostów wirtualnych wystąpienia ASCS/SCS przy użyciu następujących parametrów:

| Nowa nazwa hosta wirtualnego SAP ASCS/SCS | Skojarzony adres IP |
| --- | --- | --- |
|cl-pr5-sap |10.0.0.50 |

Nowa nazwa hosta i adresu IP są wyświetlane w Menedżerze DNS, jak pokazano na poniższym zrzucie ekranu:

![Lista Menedżera DNS wyróżnianie zdefiniowanych wpis DNS dla nowej SAP ASCS/SCS klastra wirtualnego nazwę i adres TCP/IP][sap-ha-guide-figure-6004]

> [!NOTE]
> Nowy adres IP przypisany do nazwy hostów wirtualnych dodatkowe wystąpienia ASCS/SCS musi być taka sama jak nowego adresu IP przypisanego do usługi równoważenia obciążenia SAP Azure.
>
>W naszym scenariuszu adres IP jest 10.0.0.50.

### <a name="add-an-ip-address-to-an-existing-azure-internal-load-balancer-by-using-powershell"></a>Dodaj adres IP do istniejących Azure wewnętrznego modułu równoważenia obciążenia przy użyciu programu PowerShell

Aby utworzyć więcej niż jedno wystąpienie SAP ASCS/SCS w tym samym klastrze usługi WSFC, Dodaj adres IP do istniejących Azure wewnętrznego modułu równoważenia obciążenia za pomocą programu PowerShell. Każdy adres IP wymaga własne reguły równoważenia obciążenia, port sondy frontonu puli adresów IP i puli zaplecza.

Poniższy skrypt dodaje nowy adres IP do istniejącej usługi równoważenia obciążenia. Zaktualizuj zmienne środowiska PowerShell. Skrypt tworzy wszystkie wymagane równoważenia obciążenia reguły dla wszystkich portów SAP ASCS/SCS.

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get the Azure virtual network and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add a second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get a new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Get an updated LP FrontendIpConfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add a back-end configuration into an existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get an updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs to the back-end pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of the '$VMName' VM to the backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for the ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for the port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Successfully added new IP '$ILBIP' to the internal load balancer '$ILBName'!" -ForegroundColor Green

```
Po uruchomieniu skryptu, wyniki są wyświetlane w portalu Azure, jak pokazano na poniższym zrzucie ekranu:

![Nowa pula IP frontonu, w portalu Azure][sap-ha-guide-figure-6005]

### <a name="add-disks-to-cluster-machines-and-configure-the-sios-cluster-share-disk"></a>Dodawanie dysków do klastra maszyny i skonfiguruj SIOS dysku udziału klastra

Należy dodać nowy dysk klastra udziału dla każdego dodatkowego wystąpienia SAP ASCS/SCS. Dla systemu Windows Server 2012 R2 dysk udziału klastra usługi WSFC obecnie w użyciu jest rozwiązanie programowe SIOS DataKeeper.

Wykonaj następujące czynności:
1. Dodaj dodatkowy dysk lub dyski o tym samym rozmiarze (co trzeba paskowych) do każdego z węzłów klastra, a ich format.
2. Skonfigurować SIOS DataKeeper replikacji magazynu.

W tej procedurze przyjęto założenie, zainstalowano SIOS DataKeeper na komputerach klastra usługi WSFC. Po zainstalowaniu go teraz należy skonfigurować replikacji między komputerami. Proces jest szczegółowo opisane w [zainstalować SIOS DataKeeper Cluster Edition dla dysku udziału klastra SAP ASCS/SCS][sap-high-availability-infrastructure-wsfc-shared-disk-install-sios].  

![DataKeeper synchroniczne dublowania dla nowych ASCS SAP/SCS współużytkować dysku][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-the-dbms-cluster"></a>Wdrażanie maszyn wirtualnych dla programu SAP aplikacji serwerów i klastrów systemu DBMS

Aby ukończyć przygotowanie infrastruktury do drugiego systemu SAP, wykonaj następujące czynności:

1. Wdrażanie dedykowanych maszyn wirtualnych dla serwerów aplikacji SAP i umieścić je w grupie własne dedykowane dostępności.
2. Wdrażanie dedykowanych maszyn wirtualnych klastra systemu DBMS i umieścić je w grupie własne dedykowane dostępności.

## <a name="install-an-sap-netweaver-multi-sid-system"></a>Zainstaluj system identyfikatora SID multi SAP NetWeaver

Opis ukończenia procesu instalacji drugiego systemu SAP SID2, zobacz [SAP NetWeaver HA na instalację klastra pracy awaryjnej systemu Windows i udostępnionego dysku dla wystąpienia programu SAP ASCS/SCS][sap-high-availability-installation-wsfc-shared-disk].

Procedury ogólne wygląda następująco:

1. [Instalowanie programu SAP przy użyciu wystąpienia ASCS/SCS wysokiej dostępności][sap-high-availability-installation-wsfc-shared-disk-install-ascs].  
 W tym kroku jest instalowany przy użyciu wystąpienia ASCS/SCS wysokiej dostępności na istniejący węzeł klastra usługi WSFC 1 SAP.

2. [Modyfikowanie profilu SAP wystąpienia ASCS/SCS][sap-high-availability-installation-wsfc-shared-disk-modify-ascs-profile].

3. [Skonfiguruj port sondy][sap-high-availability-installation-wsfc-shared-disk-add-probe-port].  
 W tym kroku konfigurowana jest zasób klastra SAP port sondy SAP SID2 IP przy użyciu programu PowerShell. Tej konfiguracji należy wykonać na jednym z węzłów klastra SAP ASCS/SCS.

4. Zainstaluj wystąpienie bazy danych.  
 Aby zainstalować drugi klaster, wykonaj czynności opisane w przewodniku instalacji SAP.

5. Zainstaluj drugiego węzła klastra.  
 W tym kroku jest instalowany przy użyciu wystąpienia ASCS/SCS wysokiej dostępności na istniejący węzeł klastra usługi WSFC 2 SAP. Aby zainstalować drugi klaster, wykonaj czynności opisane w przewodniku instalacji SAP.

6. Otwórz porty zapory systemu Windows dla portu wystąpienia i badania SAP ASCS/SCS.  
    Na obu węzłów klastra używane dla wystąpień SAP ASCS/SCS otwierasz wszystkie porty zapory systemu Windows, które są używane przez SAP ASCS/SCS. Porty te SAP ASCS/SCS wystąpienia są wymienione w rozdziale [SAP ASCS / portów SCS][sap-net-weaver-ports-ascs-scs-ports].

    Aby uzyskać listę wszystkich portów SAP, zobacz [porty TCP/IP wszystkich produktów SAP][sap-net-weaver-ports].  

    Również otworzyć portu sondy modułu równoważenia obciążenia wewnętrznego platformy Azure, który 62350 w naszym scenariuszu jest. Opisano [w tym artykule][sap-high-availability-installation-wsfc-shared-disk-win-firewall-probe-port].

7. [Zmień typ uruchamiania wystąpienia usługi systemu Windows rozliczenie odbioru otrzymania SAP obliczone][sap-high-availability-installation-wsfc-shared-disk-change-ers-service-startup-type].

8. Zainstaluj serwer aplikacji głównej SAP nowy dedykowany maszynie Wirtualnej, zgodnie z opisem w podręczniku instalacji SAP.  

9. Zainstaluj serwer aplikacji dodatkowe SAP nowy dedykowany maszynie Wirtualnej, zgodnie z opisem w podręczniku instalacji SAP.

10. [Testowanie trybu failover wystąpienia programu SAP ASCS/SCS i replikacji SIOS][sap-high-availability-installation-wsfc-shared-disk-test-ascs-failover-and-sios-repl].

## <a name="next-steps"></a>Następne kroki

- [Ograniczenia sieciowe: Usługa Azure Resource Manager][networking-limits-azure-resource-manager]
- [Moduł równoważenia obciążenia z wieloma wirtualnymi adresami IP na platformie Azure][load-balancer-multivip-overview]
