---
title: "Klaster SAP ASCS/SCS wystąpienia klastra trybu failover z systemem Windows przy użyciu udziału plików na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klaster z wystąpieniem SAP ASCS/SCS klastra trybu failover z systemem Windows przy użyciu udziału plików na platformie Azure."
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
ms.openlocfilehash: 7fa09de63c6f148064861479138934976f1f3e38
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2017
---
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[2492395]:https://launchpad.support.sap.com/#/notes/2492395

[kb4025334]:https://support.microsoft.com/help/4025334/windows-10-update-kb4025334

[dv2-series]:https://docs.microsoft.com/azure/virtual-machines/windows/sizes-general#dv2-series
[ds-series]:https://docs.microsoft.com/azure/virtual-machines/windows/sizes-general#ds-series

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md
[sap-high-availability-architecture-scenarios]:sap-high-availability-architecture-scenarios.md
[sap-high-availability-guide-wsfc-shared-disk]:sap-high-availability-guide-wsfc-shared-disk.md
[sap-high-availability-guide-wsfc-file-share]:sap-high-availability-guide-wsfc-file-share.md
[sap-ascs-high-availability-multi-sid-wsfc]:sap-ascs-high-availability-multi-sid-wsfc.md
[sap-high-availability-infrastructure-wsfc-shared-disk]:sap-high-availability-infrastructure-wsfc-shared-disk.md
[sap-high-availability-infrastructure-wsfc-file-share]:sap-high-availability-infrastructure-wsfc-file-share.md
[sap-high-availability-installation-wsfc-shared-disk]:sap-high-availability-installation-wsfc-shared-disk.md
[sap-hana-ha]:sap-hana-high-availability.md
[sap-suse-ascs-ha]:high-availability-guide-suse.md

[planning-volumes-s2d-choosing-filesystem]:https://docs.microsoft.com/windows-server/storage/storage-spaces/plan-volumes#choosing-the-filesystem
[choosing-the-size-of-volumes-s2d]:https://docs.microsoft.com/windows-server/storage/storage-spaces/plan-volumes#choosing-the-size-of-volumes
[deploy-sofs-s2d-in-azure]:https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-storage-spaces-direct-deployment
[s2d-in-win-2016]:https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview
[deep-dive-volumes-in-s2d]:https://blogs.technet.microsoft.com/filecab/2016/08/29/deep-dive-volumes-in-spaces-direct/

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

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png


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

[1869038]:https://launchpad.support.sap.com/#/notes/1869038 

# <a name="cluster-an-sap-ascsscs-instance-on-a-windows-failover-cluster-by-using-a-file-share-in-azure"></a>Klaster SAP ASCS/SCS wystąpienia klastra trybu failover z systemem Windows przy użyciu udziału plików na platformie Azure

> ![Windows][Logo_Windows] Windows
>

Klaster pracy awaryjnej systemu Windows Server jest podstawą SAP ASCS/SCS instalacji wysokiej dostępności i bazami danych w systemie Windows.

Klaster trybu failover to grupa 1 + n niezależnych serwerów (węzłów), które współpracują ze sobą w celu zwiększenia dostępności aplikacji i usług. W przypadku awarii węzła klastra trybu failover systemu Windows Server oblicza liczbę błędów, które mogą wystąpić i zachować dobrej kondycji klastra zapewnienie aplikacji i usług. Istnieje możliwość z kworum różne tryby osiągnięcia klastra trybu failover.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem zadań, które zostały opisane w tym artykule, należy przejrzeć ten artykuł:

* [Scenariusze dla programu SAP NetWeaver i Azure architektura wysokiej dostępności maszyny wirtualnej][sap-high-availability-architecture-scenarios]

> [!IMPORTANT]
> Klastrowanie SAP ASCS/SCS wystąpienia przy użyciu udziału plików jest obsługiwane dla programu SAP NetWeaver 7.40 (i nowszych) z programu SAP 7.49 jądra (i nowszych).
>


## <a name="windows-server-failover-clustering-in-azure"></a>Awaryjnej systemu Windows Server na platformie Azure

W porównaniu do wdrożenia bez systemu operacyjnego lub prywatnej chmury, maszynach wirtualnych platformy Azure wymaga dodatkowych kroków, aby skonfigurować klaster pracy awaryjnej systemu Windows Server. Podczas tworzenia klastra, należy ustawić kilka adresów IP i nazwy hostów wirtualnych dla wystąpienia programu SAP ASCS/SCS.

### <a name="name-resolution-in-azure-and-the-cluster-virtual-host-name"></a>Rozpoznawanie nazw w usłudze Azure i nazwę hosta wirtualnego klastra

Chmury Azure platforma nie oferuje opcję, aby skonfigurować wirtualne adresy IP, takie jak adresy IP zmiennoprzecinkowych. Należy rozwiązań alternatywnych, aby skonfigurować wirtualny adres IP do zasobu klastra w chmurze. 

Usługa równoważenia obciążenia Azure udostępnia *wewnętrznego modułu równoważenia obciążenia* dla platformy Azure. Z wewnętrznego modułu równoważenia obciążenia klienci osiągnąć klastra za pośrednictwem wirtualnego adresu IP klastra. 

Wdróż wewnętrznego modułu równoważenia obciążenia w grupie zasobów, która zawiera węzły klastra. Następnie należy skonfigurować wszystkie niezbędne portu przekazywania reguł za pomocą sondy porty wewnętrznego modułu równoważenia obciążenia. Klienci mogą łączyć się za pomocą nazwy hostów wirtualnych. Serwer DNS rozpoznaje adres IP klastra. Wewnętrzny moduł równoważenia obciążenia obsługuje przekazywanie portu do aktywnego węzła klastra.

![Rysunek 1: Windows Server Failover Clustering konfiguracji platformy Azure bez udostępnionego dysku][sap-ha-guide-figure-1001]

_**Rysunek 1.** konfiguracji platformy Azure bez udostępnionego dysku awaryjnej systemu Windows Server_

## <a name="sap-ascsscs-ha-with-file-share"></a>SAP ASCS/SCS HA z udziału plików

SAP opracowany nowe podejście, a zamiast klastra dyski udostępnione dla klastra SAP ASCS/SCS wystąpienia klastra trybu failover z systemem Windows. Zamiast używać udostępnionego klastra dysków, udziału plików SMB służy do wdrożenia SAP globalne hosta plików.

> [!NOTE]
> Udziału plików SMB jest to alternatywa dla użycia dysków klastra udostępnionego dla klastra SAP ASCS/SCS wystąpień.  
>

Taka architektura jest określone w następujący sposób:

* Usługi centralnej SAP (z własnego pliku struktury i komunikat i umieścić w kolejce procesów) są niezależne od plików hosta globalne SAP.
* Usługi centralnej SAP uruchamiana z wystąpieniem SAP ASCS/SCS.
* Wystąpienie programu SAP ASCS/SCS jest klastrowany i jest dostępny za pomocą \<nazwy hostów wirtualnych ASCS/SCS\> nazwę hosta wirtualnego.
* Pliki globalne SAP są umieszczane w udziale plików SMB i są dostępne za pomocą \<hosta globalne SAP\> nazwy hosta: \\ \\ &lt;hosta globalne SAP&gt;\sapmnt\\ &lt;SID&gt;\SYS\....
* Wystąpienie programu SAP ASCS/SCS jest zainstalowany na dysku lokalnym na obu węzłów klastra.
* \<Nazwy hostów wirtualnych ASCS/SCS\> Nazwa sieciowa różni się od &lt;hosta globalne SAP&gt;.

![Rysunek 2: SAP ASCS/SCS HA architektury z udziału plików SMB][sap-ha-guide-figure-8004]

_**Rysunek 2.** SAP ASCS/SCS HA architektura z udziału plików SMB_

Wymagania wstępne dotyczące udziału plików SMB:

* Protokół SMB 3.0 (lub nowszej) protokołu.
* Możliwość określenia dostępu do usługi Active Directory formantu listy (kontroli dostępu ACL) dla grup użytkowników usługi Active Directory i `computer$` obiektu komputera.
* Udział plików musi być włączona wysokiej dostępności:
    * Dysków używanych do przechowywania plików nie może być pojedynczym punktem awarii.
    * Serwera lub przestoju maszyna wirtualna nie powoduje przestój w udziale plików.

SAP \<SID\> roli klastra nie zawiera dysków udostępnionym w klastrze lub zasób klastra udziału pliku ogólnego.


![Rysunek 3: SAP \<SID\> roli zasoby dotyczące korzystania z udziału plików klastra][sap-ha-guide-figure-8005]

_**Rysunek 3.** SAP &lt;SID&gt; roli zasoby dotyczące korzystania z udziału plików klastra_


## <a name="scale-out-file-shares-with-storage-spaces-direct-in-azure-as-an-sapmnt-file-share"></a>Udziały plików skalowalne w poziomie bezpośrednich miejsc do magazynowania na platformie Azure jako SAPMNT udziału plików

Udziału plików skalowalnego w poziomie służy do hosta i chronić pliki globalne hosta SAP. Udziału plików skalowalnego w poziomie oferuje również wysokiej dostępności usługi udziału plików SAPMNT.

![Rysunek 4: Udziału plików skalowalnego w poziomie używane do ochrony plików hosta globalne SAP][sap-ha-guide-figure-8006]

_**Rysunek 4:** udziału plików skalowalnego w poziomie, używane do ochrony plików hosta globalne SAP_

> [!IMPORTANT]
> Udziały plików skalowalne w poziomie są w pełni obsługiwane w chmurze Microsoft Azure i w środowisku lokalnym.
>

Udziału plików skalowalnego w poziomie oferuje wysokiej dostępności i skalowalnego w poziomie udział plików SAPMNT.

Bezpośrednie miejsca do magazynowania służy jako udostępniony dysk do udziału plików skalowalnego w poziomie. Bezpośrednie miejsca do magazynowania umożliwia tworzenie wysokiej dostępności i skalowalności magazynu przy użyciu serwerów z magazynem lokalnym. Udostępnionego magazynu, który jest używany do udziału plików skalowalnego w poziomie, takich jak SAP globalne hosta plików, nie jest pojedynczym punktem awarii.

> [!IMPORTANT]
>Jeśli użytkownik *nie* planu, aby skonfigurować odzyskiwania po awarii, zalecamy użycie udziału plików skalowalnego w poziomie jako rozwiązaniem dla udziału plików o wysokiej dostępności na platformie Azure.
>

### <a name="sap-prerequisites-for-scale-out-file-shares-in-azure"></a>Wymagania wstępne SAP dla udziałów plików skalowalnych w poziomie na platformie Azure

Aby używać udziału plików skalowalnego w poziomie, system musi spełniać następujące wymagania:

* Co najmniej dwóch klastra węzłów do udziału plików skalowalnego w poziomie.
* Każdy węzeł musi mieć co najmniej dwa dyski lokalne.
* Z powodu wydajności, należy użyć *dublowania odporności*:
    * Dwukierunkowe dublowania udziału plików skalowalnego w poziomie z dwoma węzłami klastra.
    * Trzystopniowo dublowania udziału plików skalowalnego w poziomie z trzech (lub więcej) węzły klastra.
* Zalecamy trzy (lub więcej) węzły klastra dla udziału plików skalowalnego w poziomie, z dublowania trzystopniowego.
    Ta konfiguracja zapewnia większą skalowalność i większą elastyczność magazynu niż konfiguracji udziału plików skalowalnego w poziomie z dwóch węzłów klastra i dublowanie dwustopniowe.
* Należy użyć dysków Azure Premium.
* Firma Microsoft zaleca użycie dysków zarządzanych platformy Azure.
* Firma Microsoft zaleca formatowanie woluminów przy użyciu System plików Refs (Resilient).
    * Aby uzyskać więcej informacji, zobacz [1869038 Uwaga SAP - SAP obsługę systemu plików ReFs] [ 1869038] i [Wybieranie systemu plików] [ planning-volumes-s2d-choosing-filesystem] rozdziału Artykuł woluminów planowanie w bezpośrednie miejsca do magazynowania.
    * Pamiętaj, że instalujesz program [aktualizacji zbiorczej firmy Microsoft KB4025334][kb4025334].
* Możesz użyć rozmiary serii DS lub serii DSv2 maszyny Wirtualnej platformy Azure.
* Wydajności dobrej sieci między maszynami wirtualnymi, które jest potrzebne do celów synchronizacji dysku bezpośrednie miejsca do magazynowania, należy użyć typu maszyny Wirtualnej, która ma co najmniej "high" przepustowości.
    Aby uzyskać więcej informacji, zobacz [serii DSv2] [ dv2-series] i [serii DS] [ ds-series] specyfikacji.
* Firma Microsoft zaleca, aby zarezerwować niektóre nieprzydzielonego miejsca w puli magazynu. Pozostawienie niektórych nieprzydzielonego pojemności w puli magazynu zapewnia woluminy miejsca, aby naprawić "w miejscu", jeśli dysk nie powiedzie się. Zwiększa to bezpieczeństwo danych i wydajności.  Aby uzyskać więcej informacji, zobacz [wybranie rozmiaru woluminu][choosing-the-size-of-volumes-s2d].
* Udziału plików skalowalnego w poziomie maszynach wirtualnych platformy Azure musi być wdrażana w własny zestaw dostępności Azure.
* Nie trzeba skonfigurować Azure wewnętrznego modułu równoważenia obciążenia dla nazwy sieci udziału plików skalowalnego w poziomie, takich jak dla \<hosta globalne SAP\>. Jest to wykonywane \<nazwy hostów wirtualnych ASCS/SCS\> wystąpienia SAP ASCS/SCS lub systemu DBMS. Udziału plików skalowalnego w poziomie skaluje się obciążenia we wszystkich węzłach klastra. \<Globalne hosta SAP\> używa lokalny adres IP dla wszystkich węzłów klastra.


> [!IMPORTANT]
> Nie można zmienić nazwy SAPMNT udziału plików, która wskazuje na \<hosta globalne SAP\>. SAP obsługuje tylko udziału nazwy "sapmnt."

> Aby uzyskać więcej informacji, zobacz [Uwaga SAP 2492395 — może sapmnt nazwa udziału można zmienić?][2492395]

### <a name="configure-sap-ascsscs-instances-and-a-scale-out-file-share-in-two-clusters"></a>Skonfiguruj SAP ASCS/SCS wystąpień i skalowalnego w poziomie udziału plików w dwóch klastrów

Można wdrożyć SAP ASCS/SCS wystąpień w jednym klastrze z własnych SAP \<SID\> roli klastra. W takim przypadku udział plików skalowalnego w poziomie można skonfigurować w innym klastrze z inną rolą klastra.

> [!IMPORTANT]
>W tym scenariuszu wystąpieniem SAP ASCS/SCS skonfigurowano dostęp do hosta globalne SAP przy użyciu ścieżki UNC \\ \\ &lt;hosta globalne SAP&gt;\sapmnt\\&lt;SID&gt;\SYS\.
>

![Rysunek 5: Wystąpienie programu SAP ASCS/SCS i udziału plików skalowalnego w poziomie wdrożonych w dwa klastry][sap-ha-guide-figure-8007]

_**Rysunek 5.** wystąpieniem SAP ASCS/SCS i skalowanie w poziomie pliku udziału wdrożone w dwóch klastrów_

> [!IMPORTANT]
> W chmurze Azure Ustaw każdego klastra, który jest używany dla SAP i plików skalowalnego w poziomie udziałów muszą być wdrożone w jego własnej dostępności Azure. Dzięki temu rozproszonej umieszczania maszyn wirtualnych klastra w ramach podstawowej infrastruktury platformy Azure.
>

## <a name="generic-file-share-with-sios-datakeeper-as-cluster-shared-disks"></a>Udział plików ogólnego DataKeeper SIOS jako udostępnione dyski klastra


> [!IMPORTANT]
> Zaleca się rozwiązanie udziału plików skalowalnego w poziomie udziału plików o wysokiej dostępności.
>
> Jeśli planujesz włączyć również odzyskiwanie po awarii dla swojego udziału plików o wysokiej dostępności, możesz korzystać udziału plików ogólnego i SISO DataKeeper dla dysków udostępnionego klastra.
>

Udział plików ogólnego jest inną opcją w przypadku osiągnięcia udziału plików o wysokiej dostępności.

W takim przypadku można użyć rozwiązania innych firm SIOS jako udostępniony dysk klastra.

## <a name="next-steps"></a>Następne kroki

* [Przygotowanie infrastruktury platformy Azure dla programu SAP HA dzięki użyciu udziału klastra i plików trybu failover systemu Windows dla programu SAP ASCS/SCS wystąpienia][sap-high-availability-infrastructure-wsfc-file-share]
* [Zainstaluj SAP NetWeaver HA na Windows trybu failover klastra i udział plików dla wystąpienia programu SAP ASCS/SCS][sap-high-availability-installation-wsfc-shared-disk]
* [Wdrażanie dwa węzły serwera plików skalowalnego w poziomie bezpośrednie miejsca do magazynowania dla magazynu UPD na platformie Azure][deploy-sofs-s2d-in-azure]
* [Bezpośrednie miejsca do magazynowania w systemie Windows Server 2016][s2d-in-win-2016]
* [Nowości: woluminy w bezpośrednie miejsca do magazynowania][deep-dive-volumes-in-s2d]
