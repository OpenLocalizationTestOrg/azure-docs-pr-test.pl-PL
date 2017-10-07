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
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a>Azure maszyn wirtualnych wysokiej dostępności dla programu SAP NetWeaver

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



Maszyny wirtualne platformy Azure jest hello rozwiązania dla organizacji, które muszą obliczeniowych, magazynu i zasobów sieciowych w czasie minimalnego i bez cykle nabywania długie. Możesz użyć aplikacji klasycznej toodeploy maszyn wirtualnych platformy Azure, takich jak ABAP na podstawie SAP NetWeaver, Java i stosu ABAP + Java. Rozszerzenie, niezawodności i dostępności bez dodatkowych lokalnych zasobów. Maszyny wirtualne platformy Azure obsługuje łączności między lokalizacjami, maszynach wirtualnych platformy Azure można zintegrować lokalnej domeny Twojej organizacji, chmur prywatnych i pozioma systemu SAP.

W tym artykule opisano firma Microsoft hello czy możesz zrobić toodeploy systemów SAP wysokiej dostępności na platformie Azure przy użyciu modelu wdrażania usługi Azure Resource Manager hello. Firma Microsoft przeprowadzi użytkownika przez proces te zadania główne:

* Znajdź hello prawo przewodniki SAP uwagi i instalacji na liście hello [zasobów] [ sap-ha-guide-2] sekcji. W tym artykule uzupełnia SAP instalacji dokumentacji i notatek SAP, które są hello głównej zasobów, które ułatwiają instalowanie i wdrażanie oprogramowania SAP na określonych platformach.
* Dowiedz się hello różnice między modelu wdrażania usługi Azure Resource Manager hello i hello Azure klasycznego modelu wdrażania.
* Więcej informacji na temat trybów kworum klastra trybu Failover systemu Windows Server, w którym można wybrać hello modelu, które jest odpowiednie dla danego wdrożenia usługi Azure.
* Więcej informacji na temat systemu Windows Server Failover Clustering udostępnionego magazynu w usług Azure.
* Dowiedz się, jak toohelp chronić pojedynczego punktu z awarii składników jak zaawansowane biznesowych aplikacji programowania (ABAP) SAP centralnej usług (ASCS) / SAP centralnej usługi (SCS) i systemy zarządzania bazami danych (DBMS) i działanie elementów nadmiarowych, takie jak SAP Serwer aplikacji na platformie Azure.
* Wykonaj krok przykład instalację i konfigurację systemu SAP wysokiej dostępności w klastrze systemu Windows Server Failover Clustering na platformie Azure przy użyciu usługi Azure Resource Manager.
* Więcej informacji na temat toouse wymagane dodatkowe kroki, Windows Server Failover Clustering na platformie Azure, ale nie są wymagane w przypadku lokalnego wdrożenia.

toosimplify wdrażania i konfiguracji, w tym artykule używamy hello szablony Menedżera zasobów systemu SAP trójwarstwowa wysokiej dostępności. Szablony Hello zautomatyzować wdrożenie całej infrastruktury hello potrzebnym do systemu SAP wysokiej dostępności. Infrastruktura Hello obsługuje również rozmiaru SAP aplikacji wydajności standardowe (protokoły SAP) systemu SAP.

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a>Wymagania wstępne
Przed rozpoczęciem upewnij się, że spełniają wymagania wstępne dotyczące hello, które zostały opisane w hello następujące sekcje. Można również, czy toocheck wszystkich zasobów wymienionych w hello [zasobów] [ sap-ha-guide-2] sekcji.

W tym artykule używamy szablonów usługi Azure Resource Manager dla [trójwarstwowa SAP NetWeaver za pomocą dysków zarządzanych](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/). Przydatne Omówienie szablonów, zobacz [szablony Menedżera zasobów Azure SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a>Zasoby
Artykuły te obejmują wdrożenia SAP na platformie Azure:

* [Azure maszyn wirtualnych, planowania i wdrażania dla programu SAP NetWeaver][planning-guide]
* [Maszyny wirtualne Azure wdrożenia SAP NetWeaver][deployment-guide]
* [Azure wdrożenia SAP NetWeaver DBMS maszyny wirtualne][dbms-guide]
* [Azure maszyn wirtualnych wysokiej dostępności dla programu SAP NetWeaver (w tym przewodniku)][sap-ha-guide]

> [!NOTE]
> Jeśli to możliwe, możemy zapewniają toohello łącza, odwoływanie SAP w podręczniku instalacji (zobacz hello [Przewodnik po instalacji programu SAP][sap-installation-guides]). Wymagania wstępne i informacje o hello proces instalacji, to jest instalację dobrze tooread hello SAP NetWeaver prowadzi dokładnie. W tym artykule opisano tylko określone zadania dla systemów opartych na procesorze SAP NetWeaver, których można użyć z maszyn wirtualnych platformy Azure.
>
>

Te informacje SAP są powiązane toohello tematu SAP na platformie Azure:

| Numer | Tytuł |
| --- | --- |
| [1928533] |Aplikacje SAP na platformie Azure: obsługiwane produktów i zmiana rozmiaru |
| [2015553] |SAP na platformie Microsoft Azure: obsługuje wymagania wstępne |
| [1999351] |Rozszerzone monitorowanie Azure dla programu SAP |
| [2178632] |Klucz monitorowania metryki dla SAP na platformie Microsoft Azure |
| [1999351] |Wirtualizacji w systemie Windows: rozszerzonego monitorowania |
| [2243692] |Użycie magazynu SSD Azure — wersja Premium dla wystąpienia systemu DBMS SAP |

Dowiedz się więcej o hello [ograniczenia subskrypcji platformy Azure][azure-subscription-service-limits-subscription], w tym domyślne ogólne ograniczenia i ograniczenia maksymalnej.

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP wysokiej dostępności z usługi Azure Resource Manager a hello Azure klasycznego modelu wdrażania
Hello Azure Resource Manager i usługi Azure klasycznych modeli wdrażania są inne hello w następujących obszarach:

- Grupy zasobów
- Azure wewnętrzny załadować równoważenia zależności na powitania grupy zasobów platformy Azure
- Obsługa scenariuszy identyfikatora SID multi SAP

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a>Grupy zasobów
W systemie Azure Resource Manager służy toomanage grup zasobów wszystkie zasoby aplikacji hello w Twojej subskrypcji platformy Azure. Witaj ma podejście, w grupie zasobów, wszystkie zasoby tego samego cyklu życia. Na przykład wszystkie zasoby są tworzone w hello sam czas i są usuwane przy hello tym samym czasie. Dowiedz się więcej o [grupach zasobów](../../../azure-resource-manager/resource-group-overview.md#resource-groups).

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure wewnętrzny załadować równoważenia zależności na powitania grupy zasobów platformy Azure

W hello Azure klasycznego modelu wdrażania istnieje zależność między hello Azure wewnętrznego modułu równoważenia obciążenia (usługa Azure Load Balancer) i usługi w chmurze hello. Co wewnętrzny moduł równoważenia obciążenia musi jedną usługę w chmurze.

W usłudze Azure Resource Manager, co zasobów platformy Azure musi toobe umieszczane grupy zasobów platformy Azure i jest nieprawidłowa dla usługi równoważenia obciążenia Azure również. Jednak brak nie potrzeby toohave jednej Azure grupy zasobów dla usługi równoważenia obciążenia Azure, np. jedna grupa zasobów platformy Azure może zawierać wiele Azure usługi równoważenia obciążenia. środowisko Hello jest prostszy i bardziej elastyczne. 

### <a name="support-for-sap-multi-sid-scenarios"></a>Obsługa scenariuszy identyfikatora SID multi SAP

W systemie Azure Resource Manager można zainstalować wielu SAP identyfikator ASCS/SCS wystąpień systemu w jednym klastrze. Identyfikator SID wielu wystąpień jest możliwe dzięki obsłudze wielu adresów IP dla każdego Azure wewnętrznego modułu równoważenia obciążenia.

toouse hello Azure klasycznego modelu wdrażania, wykonaj procedury hello opisane w temacie [SAP NetWeaver na platformie Azure: wystąpień klastrowania SAP ASCS/SCS przy użyciu klastra trybu Failover systemu Windows Server na platformie Azure z SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).

> [!IMPORTANT]
> Zdecydowanie zaleca się użycie modelu wdrażania usługi Azure Resource Manager powitania dla instalacji programu SAP. Oferuje wiele korzyści, które nie są dostępne w hello klasycznego modelu wdrażania. Dowiedz się więcej o usłudze Azure [modele wdrażania][virtual-machines-azure-resource-manager-architecture-benefits-arm].   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a>Klaster trybu Failover serwera systemu Windows
Windows Server Failover Clustering jest foundation hello instalacji SAP ASCS/SCS wysokiej dostępności i bazami danych w systemie Windows.

Klaster trybu failover to grupa 1 + n niezależnych serwerów (węzłów), które współpracują ze sobą tooincrease hello dostępności aplikacji i usług. W przypadku awarii węzła usługi Windows Server Failover Clustering oblicza hello liczbę błędów, które mogą wystąpić przy zachowaniu dobrej kondycji klastra tooprovide aplikacji i usług. Można wybrać z kworum różne tryby tooachieve awaryjnej.

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a>Tryb kworum
Korzystając z usługi Windows Server Failover Clustering można wybrać z czterech trybów kworum:

* **Większość węzłów**. Każdy węzeł klastra hello głosować. funkcje klastra Hello tylko z większością głosów, czyli z więcej niż połowy hello głosów. Firma Microsoft zaleca tej opcji w przypadku klastrów nieparzysta liczba węzłów. Na przykład trzech węzłów w klastrze siedem może zakończyć się niepowodzeniem, a aparaturze klastra hello osiąga większości i kontynuuje toorun.  
* **Większość węzłów i dysków**. Każdy węzeł i wyznaczonych dysku (monitorem dysku) w magazynie klastra hello głosować gdy są one dostępne i w komunikacie. funkcje klastra Hello tylko w przypadku większości hello głosów, oznacza to, z więcej niż połowy głosów hello. W tym trybie ma sens w środowisku klastra z parzystą liczbą węzłów. Jeśli hello połowa węzłów i dysków hello są w trybie online, hello klaster będzie pozostawał w dobrej kondycji.
* **Węzeł i udziału plików większość**. Każdy węzeł plus udział plików wyznaczonych (monitora udziału plików), który hello administrator tworzy głosować, niezależnie od tego, czy są dostępne węzły hello i udziału plików i komunikacji. funkcje klastra Hello tylko w przypadku większości hello głosów, oznacza to, z więcej niż połowy głosów hello. W tym trybie ma sens w środowisku klastra z parzystą liczbą węzłów. Jest podobne toohello węzła i tryb większość dysku, ale zamiast monitora dysku używa monitora udziału plików. Ten tryb jest łatwe tooimplement, ale jeśli udział plików hello sam nie ma wysokiej dostępności, mogą stać się pojedynczym punktem awarii.
* **Bez większości: Na dysku tylko**. Hello klaster ma kworum, jeśli jeden węzeł jest dostępny i komunikuje się z określonym dyskiem w magazynie klastra hello. Tylko węzły hello, które są także komunikuje się z tego dysku może dołączać hello klastra. Zaleca się, że nie należy używać tego trybu.
 

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a>Windows Server awaryjnej lokalnej
Rysunek 1 pokazuje klastra z dwoma węzłami. Jeśli hello połączenie sieciowe między węzłami hello nie powiedzie się i oba węzły pozostać w górę i uruchomiona, udziału pliku lub dysku kworum Określa, który węzeł będzie tooprovide hello klastra aplikacji i usług. węzeł Hello, dysku kworum toohello dostępu lub udział plików jest hello węzła, który zapewnia, że usługi.

Ponieważ w tym przykładzie użyto dwa węzły klastra, używamy hello węzła i Tryb kworum Większość udziału plików. Większość dysku i Hello węzła również jest prawidłową opcją. W środowisku produkcyjnym zaleca się, że używasz dysku kworum. Można użyć sieci i magazynu toomake technologii systemu go wysokiej dostępności.

![Rysunek 1: Na przykład Windows Server Failover Clustering konfiguracji dla programu SAP ASCS/SCS na platformie Azure][sap-ha-guide-figure-1000]

_**Rysunek 1.** przykład Windows Server Failover Clustering konfiguracji dla programu SAP ASCS/SCS na platformie Azure_

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a>Magazyn udostępniony
Rysunek 1 pokazuje również klastra magazynu udostępnionego z dwoma węzłami. W lokalnej klastra magazynu udostępnionego wszystkie węzły w klastrze hello wykryć magazynu udostępnionego. Mechanizm blokowania chroni dane hello przed uszkodzeniem. Wszystkie węzły mogą wykryć, jeśli inny węzeł nie powiedzie się. Jeśli jeden węzeł ulegnie awarii, drugi węzeł hello przejmuje hello zasoby magazynu oraz zapewnia hello dostępności usług.

> [!NOTE]
> Nie trzeba udostępnionych dysków wysokiej dostępności z niektórymi aplikacjami systemu DBMS, takich jak z programem SQL Server. SQL Server AlwaysOn replikuje DBMS danych i plików dziennika z hello dysku jednego węzła toohello lokalnego dysku klastrowego innego węzła klastra. W takim przypadku konfiguracji klastra z systemem Windows hello nie wymaga udostępnionego dysku.
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a>Sieci i rozpoznawanie nazw
Komputery klienckie osiągnąć hello klastra za pośrednictwem wirtualnego adresu IP i nazwy hostów wirtualnych tego hello, które udostępnia serwer DNS. Witaj węzłów lokalnymi i hello serwer DNS może obsłużyć wielu adresów IP.

W typowej instalacji można użyć dwóch lub więcej połączeń sieciowych:

* Magazyn toohello dedykowanego połączenia
* Połączenie z siecią wewnętrzną klastra dla hello pulsu
* Sieć publiczną, że klienci używają tooconnect toohello klastra

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a>Windows Server awaryjnej na platformie Azure
W porównaniu toobare wdrożenia kompletnego stanu lub prywatnej chmury, maszyn wirtualnych Azure wymaga systemu Windows Server Failover Clustering tooconfigure dodatkowe kroki. Podczas tworzenia dysku udostępnionego klastra konieczne tooset kilka adresów IP i hostów wirtualnych nazwy hello SAP ASCS/SCS wystąpienia.

W tym artykule firma Microsoft omówiono kluczowe założenia i hello toobuild wymagane dodatkowe kroki SAP klastra usług centralnej o wysokiej dostępności na platformie Azure. Firma Microsoft przedstawiają sposób tooset się narzędzia innej firmy hello SIOS DataKeeper i jak tooconfigure hello Azure wewnętrznego modułu równoważenia obciążenia. Toocreate te narzędzia klastra trybu failover w systemie Windows można użyć z monitora udziału plików na platformie Azure.

![Rysunek 2: Windows Server Failover Clustering konfiguracji platformy Azure bez udostępnionego dysku][sap-ha-guide-figure-1001]

_**Rysunek 2.** Windows Server Failover Clustering konfiguracji na platformie Azure, bez udostępnionego dysku_

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a>Udostępniony dysk na platformie Azure z SIOS DataKeeper
Należy klastra magazynu udostępnionego dla wystąpienia programu SAP ASCS/SCS wysokiej dostępności. Września 2016 r. Azure nie oferuje magazyn udostępniony który program toocreate klastra magazynu udostępnionego. Można użyć oprogramowania innych firm SIOS DataKeeper Cluster Edition toocreate dublowany magazynu, która symuluje magazyn udostępniony klastra. Hello SIOS rozwiązanie zapewnia replikację danych w czasie rzeczywistym synchroniczne. Jest to tworzenia zasobu dysku udostępnionego dla klastra:

1. Dołącz tooeach dodatkowy dysk hello maszyn wirtualnych (VM) w konfiguracji klastra systemu Windows.
2. Uruchamianie SIOS DataKeeper Cluster Edition w obu węzłach maszyny wirtualnej.
3. Skonfiguruj SIOS DataKeeper Cluster Edition, aby go odzwierciedla hello zawartości woluminu dysku dodatkowe hello z hello źródłowej maszyny wirtualnej toohello dodatkowy dysk dołączony woluminu hello docelowej maszyny wirtualnej. SIOS DataKeeper abstracts hello źródłowa i docelowa woluminy lokalne, a następnie je tooWindows serwera jako jeden dysk udostępniony klaster pracy awaryjnej.

Uzyskaj więcej informacji [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).

![Rysunek 3: Windows Server Failover Clustering konfiguracji na platformie Azure z SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Rysunek 3.** konfiguracji klastra trybu Failover systemu Windows Server na platformie Azure z SIOS DataKeeper_

> [!NOTE]
> Nie potrzebujesz wysokiej dostępności z niektórych produktów, bazami danych, takich jak SQL Server udostępnione dyski. SQL Server AlwaysOn replikuje DBMS danych i plików dziennika z hello dysku jednego węzła toohello lokalnego dysku klastrowego innego węzła klastra. W takim przypadku konfiguracji klastra z systemem Windows hello nie wymaga udostępnionego dysku.
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a>Rozpoznawanie nazw w systemie Azure
Witaj chmury Azure platforma nie oferuje hello opcja tooconfigure wirtualnych adresów IP, takie jak adresy IP zmiennoprzecinkowych. Należy tooset rozwiązań alternatywnych zapasowej wirtualnego adresu IP adres tooreach hello zasób klastra w chmurze hello.
Platforma Azure ma wewnętrznego modułu równoważenia obciążenia w hello Usługa równoważenia obciążenia Azure. Z hello wewnętrznego modułu równoważenia obciążenia klienci osiągnąć hello klastra za pośrednictwem hello klastra wirtualnego adresu IP.
Należy toodeploy hello wewnętrznego modułu równoważenia obciążenia w grupie zasobów hello zawierający hello węzłów klastra. Następnie należy skonfigurować wszystkie niezbędne portu przekazywania reguły z badania hello porty hello wewnętrznego modułu równoważenia obciążenia.
Witaj, klienci mogą łączyć za pomocą nazwy hostów wirtualnych hello. Witaj serwer DNS rozpoznaje adres IP klastra hello i przekazywania toohello aktywnego węzła klastra hello hello obciążenia wewnętrznego modułu równoważenia dojścia do portu.

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a>SAP NetWeaver wysokiej dostępności w Azure infrastruktury jako — usługa (IaaS)
tooachieve SAP wysoką dostępność aplikacji, takie jak SAP składników oprogramowania, muszą hello tooprotect następujące składniki:

* Wystąpienie serwera aplikacji SAP
* Wystąpienie programu SAP ASCS/SCS
* Serwer systemu DBMS

Aby uzyskać więcej informacji o ochronie składników SAP w scenariuszach wysokiej dostępności, zobacz [maszyny wirtualne Azure planowania i wdrażania dla programu SAP NetWeaver][planning-guide-11].

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a>Serwer aplikacji SAP wysokiej dostępności
Zwykle nie trzeba konkretnego rozwiązania wysokiej dostępności dla wystąpień serwera aplikacji SAP i okna dialogowe hello. Zapewniania wysokiej dostępności przez nadmiarowości i wiele wystąpień w oknie dialogowym należy skonfigurować w różnych wystąpień maszyn wirtualnych Azure. Powinien mieć co najmniej dwóch wystąpień aplikacji SAP zainstalowane w dwóch wystąpień maszyn wirtualnych Azure.

![Rysunek 4: SAP wysokiej dostępności aplikacji serwera][sap-ha-guide-figure-2000]

_**Rysunek 4:** SAP wysokiej dostępności serwera aplikacji_

Należy umieścić wszystkich maszyn wirtualnych, że host wystąpień serwera aplikacji SAP w hello tego samego zestawu dostępności Azure. Zestaw dostępności Azure upewnia się, że:

* Wszystkie maszyny wirtualne są częścią hello tej samej domeny uaktualnienia. Domeny uaktualnienia, na przykład upewnia się, że hello maszyny wirtualne nie są aktualizowane na powitania jednocześnie podczas zaplanowanej konserwacji przestoju.
* Wszystkie maszyny wirtualne są częścią hello tej samej domenie błędów. Domeny błędów, na przykład upewnia się, że maszyny wirtualne są wdrażane tak, aby nie pojedynczego punktu awarii wpływa na dostępność hello wszystkich maszyn wirtualnych.

Dowiedz się więcej o tym, jak za[Zarządzanie hello dostępność maszyn wirtualnych][virtual-machines-manage-availability].

Niezarządzane tylko na dysku: hello kontem magazynu platformy Azure jest potencjalnych pojedynczy punkt awarii, dlatego jest ważne toohave przynajmniej dwóch kont magazynu Azure, w których są dystrybuowane co najmniej dwóch maszyn wirtualnych. W Instalatorze idealne dysków hello każdej maszyny wirtualnej, na którym jest uruchomione wystąpienie okna dialogowego SAP będzie można wdrożyć w innego konta magazynu.

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a>Wystąpienie programu SAP ASCS/SCS wysokiej dostępności
Rysunek 5 jest przykładem wystąpienia SAP ASCS/SCS wysokiej dostępności.

![Rysunek 5: Wystąpienie wysokiej dostępności SAP ASCS/SCS][sap-ha-guide-figure-2001]

_**Rysunek 5.** SAP wysokiej dostępności ASCS/SCS wystąpienia_

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a>SAP ASCS/SCS wystąpienie wysokiej dostępności z systemu Windows Server Failover Clustering na platformie Azure
W porównaniu toobare wdrożenia kompletnego stanu lub prywatnej chmury, maszyn wirtualnych Azure wymaga systemu Windows Server Failover Clustering tooconfigure dodatkowe kroki. toobuild klastra pracy awaryjnej systemu Windows, należy dysku udostępnionego klastra, kilka adresów IP, kilka nazw hostów wirtualnych i Azure wewnętrznego modułu równoważenia obciążenia dla klastra z wystąpieniem SAP ASCS/SCS. Omówiono bardziej szczegółowo w dalszej części artykułu hello to.

![Rysunek 6: Windows Server Failover Clustering konfiguracji SAP ASCS/SCS na platformie Azure przy użyciu SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Rysunek 6.** Windows Server Failover Clustering konfiguracji SAP ASCS/SCS na platformie Azure z SIOS DataKeeper_

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Wystąpienie systemu DBMS wysokiej dostępności
Witaj DBMS jest również pojedynczy punkt kontaktu w systemie SAP. Należy tooprotect go za pomocą rozwiązania wysokiej dostępności. Rysunek nr 7 przedstawia rozwiązania wysokiej dostępności programu SQL Server zawsze na platformie Azure, Windows Server Failover Clustering i hello Azure wewnętrzne usługi równoważenia obciążenia. SQL Server AlwaysOn replikuje DBMS danych i plików dziennika przy użyciu własnego systemu DBMS replikacji. W takim przypadku możesz nie muszą klastra udostępnione dyski, które upraszcza hello wszystkie ustawienia.

![Rysunek 7: Przykładem DBMS SAP wysokiej dostępności, z programu SQL Server AlwaysOn][sap-ha-guide-figure-2003]

_**Rysunek 7.** przykład DBMS SAP wysokiej dostępności, z programu SQL Server AlwaysOn_

Aby uzyskać więcej informacji o klastrach programu SQL Server na platformie Azure przy użyciu modelu wdrażania usługi Azure Resource Manager hello zobacz następujące artykuły:

* [Konfiguruj zawsze włączone grupy dostępności w maszynach wirtualnych platformy Azure ręcznie przy użyciu usługi Resource Manager] [virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]
* [Konfiguruj Azure wewnętrznego modułu równoważenia obciążenia dla grupy dostępności AlwaysOn w Azure] [virtual-machines-windows-portal-sql-alwayson-int-listener]

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a>Scenariusze wdrażania wysokiej dostępności na trasie

### <a name="deployment-scenario-using-architectural-template-1"></a>Scenariusz wdrażania przy użyciu architektury 1 szablonu

Rysunek nr 8 przedstawia przykład architektury wysokiej dostępności programu SAP NetWeaver Azure **jeden** systemu SAP. Ten scenariusz jest skonfigurowane w następujący sposób:

- Jeden dedykowanego klastra jest używany dla wystąpienia programu SAP ASCS/SCS hello.
- Jeden dedykowanego klastra jest używany dla wystąpienia systemu DBMS hello.
- SAP wystąpień serwera aplikacji są wdrażane w ich własnych dedykowanych maszyn wirtualnych.

![Rysunek 8: SAP wysokiej dostępności architektury szablonu 1, za pomocą dedykowanego klastra ASCS/SCS i bazami danych][sap-ha-guide-figure-2004]

_**Rysunek 8.** SAP architektury 1 szablonu wysokiej dostępności, dedykowane klastry ASCS/SCS i bazami danych_

### <a name="deployment-scenario-using-architectural-template-2"></a>Scenariusz wdrażania przy użyciu architektury 2 szablonu

Na rysunku nr 9 przedstawiono przykład architektury wysokiej dostępności programu SAP NetWeaver Azure **jeden** systemu SAP. Ten scenariusz jest skonfigurowane w następujący sposób:

- Jeden klaster dedykowanych służy do **zarówno** hello SAP ASCS/SCS wystąpienia i hello systemu DBMS.
- SAP wystąpień serwera aplikacji są wdrażane w własnych dedykowanych maszyn wirtualnych.

![Rysunek 9: SAP wysokiej dostępności architektury szablonu 2, dedykowanego klastra dla ASCS/SCS i dedykowanego klastra dla systemu DBMS][sap-ha-guide-figure-2005]

_**Rysunek 9:** SAP wysokiej dostępności architektury szablonu 2, dedykowanego klastra dla ASCS/SCS i dedykowanego klastra dla systemu DBMS_

### <a name="deployment-scenario-using-architectural-template-3"></a>Scenariusz wdrażania przy użyciu architektury 3 szablonu

Na rysunku nr 10 przedstawiono architekturę SAP NetWeaver wysokiej dostępności platformy Azure dla **dwóch** SAP systemy, z &lt;SID1&gt; i &lt;SID2&gt;. Ten scenariusz jest skonfigurowane w następujący sposób:

- Jeden dedykowanego klastra służy do **zarówno** wystąpienia hello SAP ASCS/SCS SID1 *i* hello SID2 ASCS/SCS SAP wystąpienia (jednego klastra).
- Jeden dedykowanego klastra jest używany dla systemu DBMS SID1 i innym dedykowanego klastra jest używany dla systemu DBMS SID2 (dwa klastry).
- SAP wystąpień serwera aplikacji hello systemu SAP SID1 ma swoje własne dedykowane maszyny wirtualne.
- SAP wystąpień serwera aplikacji hello systemu SAP SID2 ma swoje własne dedykowane maszyny wirtualne.

![Rysunek 10: Wysoka dostępność architektury szablonu 3, z dedykowanym klastrem w różnych wystąpieniach ASCS/SCS SAP][sap-ha-guide-figure-6003]

_**Rysunek 10:** wysokiej dostępności architektury szablonu 3, z dedykowanym klastrem w różnych wystąpieniach ASCS/SCS SAP_

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Przygotowanie infrastruktury hello

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a>Przygotowanie infrastruktury hello architektury 1 szablonu
Szablony usługi Azure Resource Manager dla programu SAP uprościć wdrażanie wymaganych zasobów.

Hello trójwarstwowa szablonów usługi Azure Resource Manager obsługuje również scenariuszy wysokiej dostępności, takich jak w architektury 1 szablon, który ma dwa klastry. Każdy klaster jest SAP pojedynczego punktu awarii dla programu SAP ASCS/SCS i bazami danych.

Oto, gdzie można uzyskać szablonów usługi Azure Resource Manager hello przykładowy scenariusz, który opisano w tym artykule:

* [Obraz Azure Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [Za pomocą zarządzanych dysków Azure obrazu z witryny Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [Obraz niestandardowy](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [Niestandardowy obraz za pomocą dysków zarządzanych](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

Infrastruktura hello tooprepare dla architektury szablon 1:

- W portalu Azure na powitania hello **parametry** bloku w hello **SYSTEMAVAILABILITY** wybierz opcję **HA**.

  ![Rysunek 11: Ustaw parametry usługi Azure Resource Manager wysokiej dostępności SAP][sap-ha-guide-figure-3000]

_**Rysunek 11:** ustawić parametry usługi Azure Resource Manager wysokiej dostępności SAP_


  Utwórz szablony Hello:

  * **Maszyny wirtualne**:
    * Maszyny wirtualne serwera aplikacji SAP: <*SAPSystemSID*> - podpisane — <*numer*>
    * Maszyny wirtualne klastra ASCS/SCS: <*SAPSystemSID*> - ascs - <*numer*>
    * Klaster systemu DBMS: <*SAPSystemSID*> - db - <*numer*>

  * **Sieci karty dla wszystkich maszyn wirtualnych adresów IP skojarzonych**:
    * <*SAPSystemSID*> - nic - podpisane — <*numer*>
    * <*SAPSystemSID*> - nic - ascs - <*numer*>
    * <*SAPSystemSID*> - nic - db - <*numer*>

  * **Konta magazynu platformy Azure (tylko w przypadku dysków niezarządzany)**

  * **Grupy dostępności** dla:
    * Maszyny wirtualne serwera aplikacji SAP: <*SAPSystemSID*> - avset - podpisane
    * Maszyny wirtualne klastra SAP ASCS/SCS: <*SAPSystemSID*> - avset - ascs
    * System DBMS klastrowanie maszyn wirtualnych: <*SAPSystemSID*> - avset - db

  * **Azure wewnętrznego modułu równoważenia obciążenia**:
    * Z wszystkimi portami dla wystąpienia ASCS/SCS hello i adresu IP <*SAPSystemSID*> - lb - ascs
    * Z wszystkimi portami dla adresu IP i bazami danych programu SQL Server hello <*SAPSystemSID*> - lb - db

  * **Grupy zabezpieczeń sieci**: <*SAPSystemSID*> - nsg - ascs-0  
    * Z otwartych zewnętrznych toohello port protokołu RDP (Remote Desktop) <*SAPSystemSID*> - ascs - 0 maszyny wirtualnej

> [!NOTE]
> Wszystkie adresy IP karty sieciowej hello i Azure wewnętrzne moduły równoważenia obciążenia są **dynamiczne** domyślnie. Zmień je za**statycznych** adresów IP. Opisano sposób toodo to w dalszej części artykułu hello.
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Wdrażanie maszyn wirtualnych z siecią firmową toouse łączności (między lokalizacjami) w środowisku produkcyjnym
Dla systemów SAP produkcyjnych, wdrażanie maszyn wirtualnych platformy Azure z [łączności z siecią firmową (między lokalizacjami)] [ planning-guide-2.2] za pomocą usługi Azure Site to Site VPN lub rozwiązania Azure ExpressRoute.

> [!NOTE]
> Można użyć wystąpienia sieci wirtualnej platformy Azure. sieć wirtualna Hello i podsieć już zostały utworzone i przygotowane.
>
>

1.  W portalu Azure na powitania hello **parametry** bloku w hello **NEWOREXISTINGSUBNET** wybierz opcję **istniejących**.
2.  W hello **SUBNETID** Dodaj pełne ciąg hello sieci Azure przygotowane SubnetID, w którym planujesz toodeploy maszynach wirtualnych platformy Azure.
3.  tooget listę wszystkich podsieci w sieci Azure, uruchom następujące polecenie programu PowerShell:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  Witaj **identyfikator** pole zawiera hello **SUBNETID**.
4. Lista wszystkich tooget **SUBNETID** wartości, uruchom to polecenie programu PowerShell:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  Witaj **SUBNETID** wygląda podobnie do następującej:

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a>Wdrażanie wystąpień SAP tylko w chmurze dla testu i pokaz
Można wdrożyć systemu SAP wysokiej dostępności w modelu wdrażania tylko w chmurze. Tego rodzaju wdrożenia przede wszystkim jest przydatna do demo i test przypadki użycia. Nie nadaje się do przypadków użycia w środowisku produkcyjnym.

- W portalu Azure na powitania hello **parametry** bloku w hello **NEWOREXISTINGSUBNET** wybierz opcję **nowe**. Pozostaw hello **SUBNETID** pole puste.

  Witaj SAP usługi Azure Resource Manager automatycznie tworzy szablon hello sieci wirtualnej platformy Azure i podsieć.

> [!NOTE]
> Należy również toodeploy maszyny wirtualnej co najmniej jednego przeznaczonego do usługi Active Directory i DNS w hello tego samego wystąpienia usługi Azure Virtual Network. Szablon Hello nie tworzy tych maszyn wirtualnych.
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a>Przygotowanie infrastruktury hello architektury 2 szablonu

Dla SAP toohelp uprościć wdrażanie zasobów wymaganej infrastruktury dla programu SAP architektury szablonu 2, można użyć tego szablonu usługi Azure Resource Manager.

Oto, gdzie można uzyskać szablonów usługi Azure Resource Manager dla tego scenariusza wdrażania:

* [Obraz Azure Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [Za pomocą zarządzanych dysków Azure obrazu z witryny Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [Obraz niestandardowy](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [Niestandardowy obraz za pomocą dysków zarządzanych](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a>Przygotowanie infrastruktury hello architektury 3 szablonu

Można przygotować infrastrukturę hello i skonfigurować SAP dla **multi-SID**. Na przykład można dodać dodatkowe wystąpienia SAP ASCS/SCS do *istniejących* konfiguracji klastra. Aby uzyskać więcej informacji, zobacz [skonfigurować dodatkowe wystąpienia SAP ASCS/SCS do istniejącej konfiguracji klastra toocreate SAP identyfikatora SID wielu konfiguracji usługi Azure Resource Manager][sap-ha-multi-sid-guide].

Chcąc toocreate multi-SID nowego klastra, można użyć hello multi-SID [szablony szybkiego startu w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates).
toocreate multi-SID nowego klastra należy hello toodeploy następujące trzy szablony:

* [ASCS/SCS szablonu](#ASCS-SCS-template)
* [Szablon bazy danych](#database-template)
* [Szablon serwerów aplikacji](#application-servers-template)

Witaj następujące sekcje mają więcej szczegółów na temat szablonów hello i parametry hello należy tooprovide w szablonach hello.

#### <a name="ASCS-SCS-template"></a>ASCS/SCS szablonu

Szablon ASCS/SCS Hello wdraża dwie maszyny wirtualne, których można używać klastra pracy awaryjnej systemu Windows Server, który obsługuje wiele wystąpień ASCS/SCS toocreate.

tooset się szablon hello ASCS/SCS multi-SID w hello [szablon identyfikatora SID multi ASCS/SCS] [ sap-templates-3-tier-multisid-xscs-marketplace-image] lub [ASCS/SCS identyfikatora SID multi szablonu za pomocą dysków zarządzanych] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], wprowadź wartości dla hello następujące parametry:

  - **Prefiks zasobów**.  Ustaw wszystkie zasoby, które są tworzone podczas wdrażania hello hello zasobów prefiks, który jest używany tooprefix. Ponieważ zasoby hello nie należą tooonly jednego systemu SAP, prefiks hello hello zasobu nie jest hello identyfikatora SID jednego systemu SAP.  Prefiks Hello musi należeć do zakresu od **trzech do sześciu znaków**.
  - **Na stosie typu**. Wybierz typ stosu hello hello systemu SAP. W zależności od typu stosu hello usługi równoważenia obciążenia Azure ma jeden (ABAP lub tylko Java) lub dwóch (ABAP + Java) prywatnych adresów IP na systemu SAP.
  -  **Typ systemu operacyjnego**. Wybierz system operacyjny hello hello maszyn wirtualnych.
  -  **Liczba systemu SAP**. Wybierz liczbę hello systemów SAP ma tooinstall w tym klastrze.
  -  **Dostępność systemu**. Wybierz **HA**.
  -  **Nazwa użytkownika i hasło administratora**. Utwórz nowego użytkownika, które mogą być używane toosign toohello maszyny.
  -  **Nowy lub istniejący podsieci**. Określ, czy należy utworzyć nową sieć wirtualną i podsieć lub istniejącą podsieć powinna być używana. Jeśli masz już sieć wirtualną tooyour połączonych sieci lokalnej, wybierz **istniejących**.
  -  **Identyfikator podsieci**. Identyfikator zestawu hello maszyn wirtualnych hello hello podsieci toowhich powinny być połączone. Wybierz podsieć hello wirtualnej sieci prywatnej (VPN) lub sieci lokalnej tooyour ExpressRoute sieci wirtualnej tooconnect hello maszyny wirtualnej. Identyfikator Hello zwykle wygląda następująco:

   /Subscriptions/ <*identyfikator subskrypcji*> /resourceGroups/ <*Nazwa grupy zasobów*> /providers/Microsoft.Network/virtualNetworks/ <*wirtualnej nazwy sieciowej*> /subnets/ <*nazwy podsieci*>

Szablon Hello wdraża jedno wystąpienie usługi równoważenia obciążenia Azure, która obsługuje wiele systemów SAP.

- wystąpienia ASCS Hello są skonfigurowane dla liczby wystąpień 00, 10, 20...
- wystąpienia SCS Hello są skonfigurowane dla liczby wystąpień 01 11, 21...
- Witaj wystąpień ASCS umieścić w kolejce replikacji serwera (Wywołujących) (tylko w systemie Linux) są skonfigurowane do liczby wystąpień 02, 12, 22...
- Witaj wystąpień Wywołujących SCS (tylko w systemie Linux) są skonfigurowane do liczby wystąpień 03, 13, 23...

Witaj modułu równoważenia obciążenia zawiera 1 (2 dla systemu Linux) VIP(s), 1 x dla ASCS/SCS i 1 x adres VIP dla Wywołujących (tylko w systemie Linux).

Witaj Poniższa lista zawiera wszystkie reguły, o których (gdzie x to liczba hello hello systemu SAP, na przykład 1, 2, 3...) równoważenia obciążenia:
- Porty właściwe dla systemu Windows dla każdego systemu SAP: 445, 5985
- Porty ASCS (liczby wystąpień x0): 32 x 0, 36 x 0, 39 x 0, 81 x 0, 5 x 013, 5 x 014, 5 x 016
- Porty SCS (liczby wystąpień x1): 32 x 1, 33 x 1, 39 x 1, 81 x 1, 5 x 113, 5 x 114, 5 x 116
- Wywołujących ASCS porty w systemie Linux (liczby wystąpień x2): 33 x 2, 5 x 213, 5 x 214, 5 x 216
- Wywołujących SCS porty w systemie Linux (liczby wystąpień x3): 33 x 3, 5 x 313, 5 x 314, 5 x 316

Moduł równoważenia obciążenia Hello jest hello toouse skonfigurowane następujące porty sondowania (gdzie x to liczba hello hello systemu SAP, na przykład 1, 2, 3...):
- Port sondy modułu równoważenia obciążenia wewnętrznego ASCS/SCS: 620 x 0
- Wewnętrzny Wywołujących załadować port sondy modułu równoważenia (tylko w systemie Linux): 621 x 2

#### <a name="database-template"></a>Szablon bazy danych

szablon bazy danych Hello wdraża jedną lub dwie maszyny wirtualne, których można używać tooinstall hello system zarządzania relacyjnymi bazami (danych RDBMS) dla jednego systemu SAP. Na przykład jeśli wdrożono szablon ASCS/SCS pięć systemów SAP, należy toodeploy ten szablon pięć razy.

tooset się hello szablon identyfikatora SID multi bazy danych, w hello [bazy danych wielu SID szablonu] [ sap-templates-3-tier-multisid-db-marketplace-image] lub [szablon identyfikatora SID multi bazy danych przy użyciu dysków zarządzanych] [ sap-templates-3-tier-multisid-db-marketplace-image-md], wprowadź wartości dla hello następujące parametry:

  -  **Identyfikator systemu SAP**. Wprowadź identyfikator systemu SAP hello hello ma tooinstall systemu SAP. Identyfikator Hello będzie służyć jako prefiks hello zasobów, które zostały wdrożone.
  -  **Typ systemu operacyjnego**. Wybierz system operacyjny hello hello maszyn wirtualnych.
  -  **Wartość DbType**. Wybierz typ hello hello bazy danych ma tooinstall na powitania klastra. Wybierz **SQL** Jeśli chcesz tooinstall programu Microsoft SQL Server. Wybierz **HANA** Jeśli planujesz tooinstall SAP HANA hello maszyn wirtualnych. Upewnij się, że tooselect hello poprawnego typu systemu operacyjnego: Wybierz **Windows** SQL i wybierz opcję dystrybucji systemu Linux HANA. Witaj równoważenia obciążenia Azure, który jest połączony toohello, które maszyny wirtualne będą skonfigurowane toosupport hello wybrane bazy danych typu:
    * **SQL**. Moduł równoważenia obciążenia Hello będzie Równoważenie obciążenia portu 1433. Upewnij się, że toouse tego portu dla ustawień programu SQL Server AlwaysOn.
    * **HANA**. Moduł równoważenia obciążenia Hello będzie Równoważenie obciążenia portów 35015 i 35017. Upewnij się, że tooinstall SAP HANA z liczby wystąpień **50**.
    Moduł równoważenia obciążenia Hello będzie używać portu sondowania 62550.
  -  **Rozmiar systemu SAP**. Dostarcza zestaw hello liczba protokoły SAP hello nowy system. Jeśli nie masz pewności, ile protokoły SAP hello system będzie wymagać, zapytaj SAP technologii partnera lub Integrator systemu.
  -  **Dostępność systemu**. Wybierz **HA**.
  -  **Nazwa użytkownika i hasło administratora**. Utwórz nowego użytkownika, które mogą być używane toosign toohello maszyny.
  -  **Identyfikator podsieci**. Wprowadź identyfikator hello hello podsieci, który został użyty podczas wdrażania hello hello ASCS/SCS szablonu lub identyfikator hello hello podsieci, który został utworzony jako część hello ASCS/SCS szablonu wdrożenia.

#### <a name="application-servers-template"></a>Szablon serwerów aplikacji

Szablon serwerów aplikacji Hello wdraża dwóch lub więcej maszyn wirtualnych, które mogą służyć jako wystąpień serwera aplikacji SAP jednego systemu SAP. Na przykład jeśli wdrożono szablon ASCS/SCS pięć systemów SAP, należy toodeploy ten szablon pięć razy.

tooset się hello serwerów wielu SID szablon aplikacji w hello [szablon identyfikatora SID wielu serwerów aplikacji] [ sap-templates-3-tier-multisid-apps-marketplace-image] lub [szablon identyfikatora SID wielu serwerów aplikacji za pomocą zarządzania dyskami] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], wprowadź wartości dla hello następujące parametry:

  -  **Identyfikator systemu SAP**. Wprowadź identyfikator systemu SAP hello hello ma tooinstall systemu SAP. Identyfikator Hello będzie służyć jako prefiks hello zasobów, które zostały wdrożone.
  -  **Typ systemu operacyjnego**. Wybierz system operacyjny hello hello maszyn wirtualnych.
  -  **Rozmiar systemu SAP**. określi liczbę Hello protokoły SAP hello nowy system. Jeśli nie masz pewności, ile protokoły SAP hello system będzie wymagać, zapytaj SAP technologii partnera lub Integrator systemu.
  -  **Dostępność systemu**. Wybierz **HA**.
  -  **Nazwa użytkownika i hasło administratora**. Utwórz nowego użytkownika, które mogą być używane toosign toohello maszyny.
  -  **Identyfikator podsieci**. Wprowadź identyfikator hello hello podsieci, który został użyty podczas wdrażania hello hello ASCS/SCS szablonu lub identyfikator hello hello podsieci, który został utworzony jako część hello ASCS/SCS szablonu wdrożenia.


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a>Sieć wirtualna platformy Azure
W naszym przykładzie hello przestrzeni adresowej sieci wirtualnej platformy Azure hello jest 10.0.0.0/16. Brak jednej podsieci o nazwie **podsieci**, z zakresu adresów 10.0.0.0/24. Wszystkie maszyny wirtualne i wewnętrzne moduły równoważenia obciążenia są wdrażane w tej sieci wirtualnej.

> [!IMPORTANT]
> Nie wprowadzono żadnych zmian toohello ustawień sieciowych w systemie operacyjnym gościa hello. W tym adresy IP, serwery DNS i podsieci. Skonfiguruj ustawienia sieci na platformie Azure. Witaj usługi protokołu dynamicznej konfiguracji hosta (DHCP) propaguje ustawienia.
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>Adresy IP serwera DNS

Witaj tooset wymagane adresy IP serwera DNS, hello następujące kroki.

1.  W portalu Azure na powitania hello **serwerów DNS** bloku, upewnij się, że sieci wirtualne **serwerów DNS** opcja jest ustawiona zbyt**niestandardowe DNS**.
2.  Wybierz ustawienia, na podstawie typu hello sieci, do których masz. Aby uzyskać więcej informacji zobacz następujące zasoby hello:
    * [Łączność sieci firmowej (między lokalizacjami)][planning-guide-2.2]: Dodaj hello adresy IP serwerów DNS lokalne powitania.  
    Można rozszerzyć lokalnymi DNS serwerów toohello maszyn wirtualnych, które są uruchomione na platformie Azure. W tym scenariuszu można dodać adresy IP hello hello Azure maszyn wirtualnych, na których uruchomiono hello usługi DNS.
    * [Tylko w chmurze wdrożenia][planning-guide-2.1]: wdrożyć dodatkowe maszyny wirtualnej w hello tego samego wystąpienia sieci wirtualnej, która służy jako serwer DNS. Dodaj adresy IP hello hello Azure maszyn wirtualnych, które po skonfigurowaniu toorun usługi DNS.

    ![Rysunek 12: Należy skonfigurować serwery DNS dla sieci wirtualnej platformy Azure][sap-ha-guide-figure-3001]

    _**Rysunek 12:** DNS Konfigurowanie serwerów na potrzeby sieci wirtualnej platformy Azure_

  > [!NOTE]
  > Jeśli zmienisz hello adresy IP serwerów DNS hello należy toorestart hello maszyn wirtualnych platformy Azure tooapply hello zmiany oraz propagację hello nowych serwerów DNS.
  >
  >

W naszym przykładzie hello usługa DNS jest instalowany i konfigurowany na tych maszynach wirtualnych systemu Windows:

| Roli maszyny wirtualnej | Nazwa hosta maszyny wirtualnej | Nazwa karty sieciowej | Statyczny adres IP |
| --- | --- | --- | --- |
| Pierwszy serwer DNS |domcontr 0 |PR1-nic-domcontr-0 |10.0.0.10 |
| Drugi serwer DNS |domcontr-1 |PR1-nic-domcontr-1 |10.0.0.11 |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Nazwy hosta i statyczne adresy IP dla klastrowanego wystąpienia programu SAP ASCS/SCS hello i DBMS klastrowanego wystąpienia

Dla wdrożenia lokalnego należy te hosta zarezerwowanych nazw i adresów IP:

| Rola nazwy hostów wirtualnych | Nazwy hostów wirtualnych | Wirtualne statycznego adresu IP |
| --- | --- | --- |
| Nazwa SAP ASCS/SCS do hostów wirtualnych pierwszej klastra (dla klastra zarządzania) |PR1-ascs-vir |10.0.0.42 |
| Nazwa hosta wirtualnego wystąpienia programu SAP ASCS/SCS |PR1 ascs sap |10.0.0.43 |
| Nazwa systemu DBMS SAP do hostów wirtualnych drugi klastra (klastra zarządzania) |PR1-dbms-vir |10.0.0.32 |

Podczas tworzenia klastra hello, utworzyć hello nazwy hostów wirtualnych **pr1-ascs-vir** i **pr1-dbms-vir** i hello skojarzony adresy IP, które Zarządzanie hello samego klastra. Aby uzyskać informacje na temat toodo tego, zobacz [zbieranie węzłów klastra w konfiguracji klastra][sap-ha-guide-8.12.1].

Można ręcznie utworzyć hello innych dwie nazwy hostów wirtualnych, **pr1 ascs sap** i **pr1 dbms sap**, i hello skojarzony adresy IP na powitania serwera DNS. Witaj klastrowanego wystąpienia programu SAP ASCS/SCS i hello klastrowane wystąpienie DBMS używać tych zasobów. Aby uzyskać informacje na temat toodo tego, zobacz [Utwórz nazwę hosta wirtualnego dla klastrowanego wystąpienia programu SAP ASCS/SCS][sap-ha-guide-9.1.1].

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Ustaw statycznych adresów IP dla maszyn wirtualnych hello SAP
Po wdrożeniu hello toouse maszyny wirtualne w klastrze, należy tooset statycznych adresów IP dla wszystkich maszyn wirtualnych. W tym w konfiguracji sieci wirtualnej Azure hello, a nie w systemie operacyjnym gościa hello.

1.  Hello portalu Azure, wybierz **grupy zasobów** > **karta sieciowa** > **ustawienia** > **adresu IP** .
2.  Na powitania **adresów IP** bloku, w obszarze **przypisania**, wybierz pozycję **statycznych**. W hello **adres IP** wprowadź adres IP hello, które mają toouse.

  > [!NOTE]
  > Jeśli zmienisz hello adresu IP karty sieciowej hello należy toorestart hello maszyn wirtualnych platformy Azure tooapply hello zmiany.  
  >
  >

  ![Rysunek 13: Ustaw statycznych adresów IP dla karty sieciowej hello każdej maszyny wirtualnej][sap-ha-guide-figure-3002]

  _**Rysunek 13:** ustawić statyczny adres IP dla karty sieciowej hello każdej maszyny wirtualnej_

  Powtórz ten krok dla wszystkich interfejsów sieciowych, oznacza to, że dla wszystkich maszyn wirtualnych, w tym maszyny wirtualne mają toouse usługi/DNS usługi Active Directory.

W naszym przykładzie mamy tych maszyn wirtualnych i statycznymi adresami IP:

| Roli maszyny wirtualnej | Nazwa hosta maszyny wirtualnej | Nazwa karty sieciowej | Statyczny adres IP |
| --- | --- | --- | --- |
| Pierwsze wystąpienie serwera aplikacji SAP |PR1 podpisane 0 |PR1-nic podpisane-0 |10.0.0.50 |
| Drugie wystąpienie serwera aplikacji SAP |PR1 podpisane 1 |PR1-nic podpisane-1 |10.0.0.51 |
| Przyciski ... |Przyciski ... |Przyciski ... |Przyciski ... |
| Ostatnie wystąpienie serwera aplikacji SAP |PR1-podpisane-5 |PR1-nic podpisane-5 |10.0.0.55 |
| Pierwszym węźle klastra dla wystąpienia ASCS/SCS |PR1-ascs-0 |PR1-nic-ascs-0 |10.0.0.40 |
| Drugi węzeł klastra dla wystąpienia ASCS/SCS |PR1-ascs-1 |PR1-nic-ascs-1 |10.0.0.41 |
| Pierwszym węźle klastra dla systemu DBMS wystąpienia |PR1-db-0 |PR1-nic-db-0 |10.0.0.30 |
| Drugi węzeł klastra dla systemu DBMS wystąpienia |PR1-db-1 |PR1-nic-db-1 |10.0.0.31 |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Ustawianie statycznego adresu IP dla hello Azure wewnętrznego modułu równoważenia obciążenia

Szablon SAP usługi Azure Resource Manager Hello tworzy Azure wewnętrznego modułu równoważenia obciążenia używanego hello SAP ASCS/SCS wystąpienia klastra i hello DBMS klastra.

> [!IMPORTANT]
> Witaj adresu IP, nazwy hostów wirtualnych hello hello jest SAP ASCS/SCS hello sam jako adres IP hello hello SAP ASCS/SCS wewnętrznego modułu równoważenia obciążenia: **pr1-lb-ascs**.
> Witaj adresu IP wirtualnej nazwy hello jest DBMS hello hello sam jako adres IP hello hello DBMS wewnętrznego modułu równoważenia obciążenia: **pr1-lb-dbms**.
>
>

tooset statyczny adres IP dla hello Azure wewnętrzny moduł równoważenia obciążenia:

1.  Witaj początkowe wdrożenie ustawia adres IP usługi równoważenia obciążenia wewnętrznego hello zbyt**dynamiczne**. W portalu Azure na powitania hello **adresów IP** bloku, w obszarze **przypisania**, wybierz pozycję **statycznych**.
2.  Ustaw adres IP hello hello wewnętrznego modułu równoważenia obciążenia **pr1-lb-ascs** toohello adres IP nazwę hosta wirtualnego hello hello SAP ASCS/SCS wystąpienia.
3.  Ustaw adres IP hello hello wewnętrznego modułu równoważenia obciążenia **pr1-lb-dbms** adres IP toohello nazwę hosta wirtualnego hello hello DBMS wystąpienia.

  ![Rysunek 14: Ustaw statycznych adresów IP dla hello wewnętrznego modułu równoważenia obciążenia dla wystąpienia programu SAP ASCS/SCS hello][sap-ha-guide-figure-3003]

  _**Rysunek 14:** ustawić statycznych adresów IP dla hello wewnętrznego modułu równoważenia obciążenia dla wystąpienia programu SAP ASCS/SCS hello_

W naszym przykładzie mamy dwa Azure wewnętrzne moduły równoważenia obciążenia mających te statycznych adresów IP:

| Rola usługi równoważenia obciążenia wewnętrznego Azure | Nazwa modułu równoważenia obciążenia wewnętrznego platformy Azure | Statyczny adres IP |
| --- | --- | --- |
| SAP ASCS/SCS wystąpienia wewnętrznego modułu równoważenia obciążenia |PR1-lb-ascs |10.0.0.43 |
| System DBMS SAP wewnętrznego modułu równoważenia obciążenia |PR1-lb-dbms |10.0.0.33 |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Domyślne reguły dla hello Azure wewnętrznego modułu równoważenia obciążenia równoważenia obciążenia ASCS/SCS

Szablon Menedżera zasobów Azure SAP Hello tworzy hello portów, które są potrzebne:
* Wystąpienie ABAP ASCS o numerze wystąpienia domyślnego hello **00**
* Wystąpienie Java SCS, z numerem wystąpienie domyślne hello **01**

Po zainstalowaniu wystąpieniem SAP ASCS/SCS, należy użyć liczby wystąpień domyślnego hello **00** dla ABAP ASCS wystąpienia i hello domyślne wystąpienie numer **01** dla swojego wystąpienia Java SCS.

Następnie należy utworzyć równoważenia punktów końcowych dla hello SAP NetWeaver porty wymagane obciążenia wewnętrznego.

toocreate wymagane punkty końcowe równoważenia obciążenia wewnętrznego, najpierw należy utworzyć te równoważenia punktów końcowych dla portów SAP NetWeaver ABAP ASCS hello obciążenia:

| Nazwa reguły równoważenia obciążenia/usługi | Domyślne numery portów | Konkretnych portów (ASCS wystąpienia z liczby wystąpień 00) (Wywołujących z 10) |
| --- | --- | --- |
| Umieścić serwer / *lbrule3200* |32 <*InstanceNumber*> |3200 |
| Serwer komunikatów ABAP / *lbrule3600* |36 <*InstanceNumber*> |3600 |
| Komunikat wewnętrzny ABAP / *lbrule3900* |39 <*InstanceNumber*> |3900 |
| Serwer HTTP / *Lbrule8100* |81 <*InstanceNumber*> |8100 |
| SAP uruchamiania usługi ASCS HTTP / *Lbrule50013* |5 <*InstanceNumber*> 13 |50013 |
| SAP uruchamiania usługi ASCS HTTPS / *Lbrule50014* |5 <*InstanceNumber*> 14 |50014 |
| Umieścić w kolejce replikacji / *Lbrule50016* |5 <*InstanceNumber*> 16 |50016 |
| SAP uruchamiania usługi Wywołujących HTTP *Lbrule51013* |5 <*InstanceNumber*> 13 |51013 |
| SAP uruchamiania usługi Wywołujących HTTP *Lbrule51014* |5 <*InstanceNumber*> 14 |51014 |
| Win RM *Lbrule5985* | |5985 |
| Udział plików *Lbrule445* | |445 |

_**Tabela 1:** portu liczby wystąpień programu SAP NetWeaver ABAP ASCS hello_

Następnie utwórz te równoważenia punktów końcowych dla portów SAP NetWeaver Java SCS hello obciążenia:

| Nazwa reguły równoważenia obciążenia/usługi | Domyślne numery portów | Konkretnych portów (SCS wystąpienia z liczby wystąpień 01) (Wywołujących z 11) |
| --- | --- | --- |
| Umieścić serwer / *lbrule3201* |32 <*InstanceNumber*> |3201 |
| Serwer bramy / *lbrule3301* |33 <*InstanceNumber*> |3301 |
| Serwer komunikatów Java / *lbrule3900* |39 <*InstanceNumber*> |3901 |
| Serwer HTTP / *Lbrule8101* |81 <*InstanceNumber*> |8101 |
| SAP uruchamiania usługi SCS HTTP / *Lbrule50113* |5 <*InstanceNumber*> 13 |50113 |
| SAP uruchamiania usługi SCS HTTPS / *Lbrule50114* |5 <*InstanceNumber*> 14 |50114 |
| Umieścić w kolejce replikacji / *Lbrule50116* |5 <*InstanceNumber*> 16 |50116 |
| SAP uruchamiania usługi Wywołujących HTTP *Lbrule51113* |5 <*InstanceNumber*> 13 |51113 |
| SAP uruchamiania usługi Wywołujących HTTP *Lbrule51114* |5 <*InstanceNumber*> 14 |51114 |
| Win RM *Lbrule5985* | |5985 |
| Udział plików *Lbrule445* | |445 |

_**Tabela 2:** portu liczby wystąpień programu SAP NetWeaver Java SCS hello_

![Rys. 15: Reguły dla hello Azure wewnętrznego modułu równoważenia obciążenia równoważenia obciążenia domyślne ASCS/SCS][sap-ha-guide-figure-3004]

_**Rysunek 15:** reguły dla hello Azure wewnętrznego modułu równoważenia obciążenia równoważenia obciążenia domyślne ASCS/SCS_

Ustawienie hello adresu IP usługi równoważenia obciążenia hello **pr1-lb-dbms** adres IP toohello nazwę hosta wirtualnego hello hello DBMS wystąpienia.

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Zmień obciążenia domyślne ASCS/SCS hello równoważenia zasady hello Azure wewnętrznego modułu równoważenia obciążenia

Jeśli mają różne liczby toouse dla hello SAP ASCS lub SCS wystąpienia, należy zmienić hello nazwy i wartości ich porty z wartościami domyślnymi.

1.  Hello portalu Azure, wybierz  **<* SID*> - lb - ascs załadować równoważenia ** > **reguły równoważenia obciążenia**.
2.  Dla wszystkich reguł, należące toohello SAP ASCS lub wystąpienie SCS równoważenia obciążenia Zmień wartości tych:

  * Nazwa
  * Port
  * Port zaplecza

  Na przykład jeśli chcesz toochange hello domyślnej liczby wystąpień ASCS od 00 too31 należy toomake hello zmiany dla wszystkich portów wymienionych w tabeli 1.

  Oto przykład aktualizacji dla portu *lbrule3200*.

  ![Rysunek 16: Zmień obciążenia domyślne ASCS/SCS hello równoważenia zasady hello Azure wewnętrznego modułu równoważenia obciążenia][sap-ha-guide-figure-3005]

  _**Rysunek 16:** zmiany hello ASCS/SCS domyślne obciążenia równoważenia zasady hello Azure wewnętrznego modułu równoważenia obciążenia_

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Dodawanie domeny toohello maszyn wirtualnych systemu Windows

Po przypisaniu statycznego maszyn wirtualnych toohello adres IP, należy dodać hello maszyn wirtualnych toohello domeny.

![Rysunek 17: Dodawanie domeny tooa maszyny wirtualnej][sap-ha-guide-figure-3006]

_**Rysunek 17:** Dodawanie domeny tooa maszyny wirtualnej_

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Dodawanie wpisów rejestru na obu węzłach hello SAP ASCS/SCS wystąpienia

Moduł równoważenia obciążenia Azure zawiera wewnętrzny moduł równoważenia obciążenia zamknięciu połączeń w przypadku połączeń hello są w stanie bezczynności pewien okres czasu (limit czasu bezczynności). Procesów roboczych SAP w oknie dialogowym wystąpień otwarte połączenia toohello SAP umieścić przetworzyć jak hello pierwszy umieścić w kolejce/usuwania z kolejki żądania wysyłane toobe potrzeb. Te połączenia zazwyczaj pozostaje ustalonych do procesu roboczego hello lub ponownego uruchomienia procesu umieścić w kolejce hello. Jednak jeśli hello połączenie jest bezczynne na wybrany okres czasu, hello połączeń hello zostanie zamknięty usługi równoważenia obciążenia wewnętrznego platformy Azure. Nie stanowi problemu, ponieważ hello procesu roboczego SAP ustanawia ponownie hello połączenia toohello umieścić procesu, jeśli już nie istnieje. Te działania są udokumentowane w ślady developer hello procesów SAP, ale ich tworzyć dużą ilością zawartości dodatkowe w tych danych śledzenia. Jest dobrym rozwiązaniem toochange hello TCP/IP `KeepAliveTime` i `KeepAliveInterval` na obu węzłów klastra. Połącz te zmiany w parametrach TCP/IP hello z parametrami profilu SAP, opisane w dalszej części artykułu hello.

wpisy rejestru tooadd na obu węzłach hello SAP ASCS/SCS wystąpienia, najpierw dodaj te wpisy rejestru systemu Windows na obu węzłów klastra systemu Windows dla programu SAP ASCS/SCS:

| Ścieżka | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Nazwa zmiennej |`KeepAliveTime` |
| Typ zmiennej |REG_DWORD (dziesiętna) |
| Wartość |120000 |
| Łącze toodocumentation |[https://technet.microsoft.com/en-us/library/cc957549.aspx](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

_**Tabela 3:** zmiany hello pierwszy parametr TCP/IP_

Następnie należy dodać ten wpisów rejestru systemu Windows na obu węzłów klastra systemu Windows dla programu SAP ASCS/SCS:

| Ścieżka | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Nazwa zmiennej |`KeepAliveInterval` |
| Typ zmiennej |REG_DWORD (dziesiętna) |
| Wartość |120000 |
| Łącze toodocumentation |[https://technet.microsoft.com/en-us/library/cc957548.aspx](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

_**Tabela 4:** zmiany hello drugi parametr TCP/IP_

**tooapply hello zmiany, ponownie uruchom oba węzły klastra**.

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a>Konfigurowanie klastra systemu Windows Server Failover Clustering dla wystąpienia programu SAP ASCS/SCS

Konfigurowanie klastra systemu Windows Server Failover Clustering dla wystąpienia programu SAP ASCS/SCS obejmuje następujące zadania:

- Zbieranie hello węzły klastra w konfiguracji klastra
- Konfigurowanie monitora udziału plików klastra

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Zbieraj hello węzły klastra w konfiguracji klastra

1.  Hello Dodawanie roli i funkcji — Kreator Dodaj klaster tooboth węzły klastra pracy awaryjnej.
2.  Konfigurowanie klastra trybu failover hello za pomocą Menedżera klastra trybu Failover. W Menedżerze klastra trybu Failover wybierz **tworzenia klastrów**, a następnie dodaj tylko hello nazwę hello pierwszy klaster, węzeł A. Nie dodawaj hello drugiego węzła jeszcze; w kolejnym kroku zostanie dodana hello drugiego węzła.

  ![Rysunek 18: Dodaj powitania serwera lub nazwę maszyny wirtualnej hello na pierwszym węźle klastra][sap-ha-guide-figure-3007]

  _**Rysunek 18:** Dodaj nazwę serwera lub maszyny wirtualnej hello hello pierwszego węzła klastra_

3.  Wprowadź nazwę sieci hello (nazwa hosta wirtualnego) hello klastra.

  ![Rysunek 19: Wprowadź nazwę klastra hello][sap-ha-guide-figure-3008]

  _**Rysunek 19:** wprowadź nazwę klastra hello_

4.  Po utworzeniu klastra hello uruchomienie testu poprawności klastra.

  ![Rysunek 20: Uruchom sprawdzenie poprawności klastra hello][sap-ha-guide-figure-3009]

  _**Rysunek 20:** uruchom sprawdzenie poprawności klastra hello_

  Możesz zignorować ostrzeżenia dotyczące dysków w tym momencie w procesie hello. Zostanie dodana monitora udostępniania plików i hello SIOS udostępnionych dysków później. Na tym etapie nie jest konieczne tooworry o kworum.

  ![Rysunek 21: Odnaleziono żadnego dysku kworum][sap-ha-guide-figure-3010]

  _**Rysunek 21:** odnaleziono żadnego dysku kworum_

  ![Rysunek 22: Zasobu klastra Core wymaga nowego adresu IP][sap-ha-guide-figure-3011]

  _**Rysunek 22:** zasobu klastra Core wymaga nowego adresu IP_

5.  Zmień adres IP hello hello podstawowej usługi klastra. Witaj klastra nie można uruchomić, dopóki nie zmieni adres IP hello hello podstawowej klastra usługi, ponieważ hello adres IP serwera hello punktów tooone hello węzły maszyny wirtualnej. To zrobić na powitania **właściwości** strony usługi hello podstawowej klastra IP zasobu.

  Na przykład, potrzebujemy tooassign adresu IP (w naszym przykładzie **10.0.0.42**) dla nazwy hosta wirtualnego klastra hello **pr1-ascs-vir**.

  ![Rysunek 23: Okno dialogowe właściwości hello, zmienić adres IP hello][sap-ha-guide-figure-3012]

  _**Rysunek 23:** w hello **właściwości** okno dialogowe, Zmień adres IP hello_

  ![Rysunek 24: Przypisać adres IP hello, które jest zastrzeżone dla klastra hello][sap-ha-guide-figure-3013]

  _**Rysunek 24:** przypisać adres IP hello, które jest zastrzeżone dla klastra hello_

6.  Przełącz nazwę hosta wirtualnego klastra hello online.

  ![Rysunek 25: Usługi podstawowej klastra jest uruchomiony i działa prawidłowo, a z hello Popraw adres IP][sap-ha-guide-figure-3014]

  _**Rysunek 25:** usługi podstawowej klastra jest uruchomiony i działa i z hello Popraw adres IP_

7.  Dodaj hello drugiego węzła klastra.

  Teraz, że usługa klastrowania core hello jest uruchomiona, można dodać hello drugiego węzła klastra.

  ![Rysunek 26: Dodaj hello drugiego węzła klastra][sap-ha-guide-figure-3015]

  _**Rysunek 26:** hello Dodaj drugi węzeł klastra_

8.  Wprowadź nazwę hello hosta drugiego węzła klastra.

  ![Rysunek 27: Wprowadź hello nazwy hosta w drugiego węzła klastra][sap-ha-guide-figure-3016]

  _**Rysunek 27:** Enter hello drugi nazwa węzła klastra hosta_

  > [!IMPORTANT]
  > Upewnij się, że hello **Dodaj wszystkie odpowiednie magazyny toohello klaster** pole wyboru jest **nie** wybrane.  
  >
  >

  ![Rysunek 28: Nie zaznaczaj pola wyboru hello][sap-ha-guide-figure-3017]

  _**Rysunek 28:** czy **nie** wybierz hello pole wyboru_

  Możesz zignorować ostrzeżenia dotyczące kworum i dysków. Opcje ustawisz hello kworum i udziału hello dysku później, zgodnie z opisem w [instalowanie SIOS DataKeeper Cluster Edition dla programu SAP ASCS/SCS dysku klastra, udziału][sap-ha-guide-8.12.3].

  ![Rysunek 29: Ignoruj ostrzeżenia dotyczące hello dysku kworum][sap-ha-guide-figure-3018]

  _**Rysunek 29:** Ignoruj ostrzeżenia dotyczące hello dysku kworum_


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a>Skonfiguruj Monitor udziału plików klastra

Konfigurowanie monitora udziału plików klastra obejmuje następujące zadania:

- Tworzenie udziału plików
- Ustawienia kworum monitora udziału plików hello w Menedżerze klastra trybu Failover

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a>Tworzenie udziału plików

1.  Wybierz monitor udziału plików, zamiast dysku kworum. SIOS DataKeeper obsługuje tę opcję.

  W przykładach hello w tym artykule Monitor udziału plików hello jest na powitania serwera/DNS usługi Active Directory, który działa na platformie Azure. Witaj monitora udziału plików jest nazywany **domcontr 0**. Ponieważ czy skonfigurowano tooAzure połączenia sieci VPN (za pośrednictwem sieci VPN typu lokacja-lokacja lub Azure ExpressRoute), monitor udostępniania sieci/DNS usługi Active Directory usługi lokalnej i nie jest toorun odpowiedniego pliku.

  > [!NOTE]
  > Jeśli usługa/DNS usługi Active Directory działa tylko na lokalne, nie skonfigurować Twoje monitora udziału plików na hello Active Directory/serwera DNS systemu operacyjnego działającej lokalnie. Opóźnienie sieci między węzłami klastra z systemem Azure i/DNS usługi Active Directory w lokalnym programie może być zbyt duży i spowodować problemy z połączeniem. Należy się tooconfigure hello monitora udziału plików na maszynie wirtualnej platformy Azure, uruchomionym Zamknij toohello węzła klastra.  
  >
  >

  Stacja kworum Hello wymaga co najmniej 1024 MB wolnego miejsca. Zaleca się 2048 MB wolnego miejsca na dysku kworum hello.

2.  Dodaj obiekt nazwy klastra hello.

  ![Rysunek 30: Przypisz hello uprawnienia udziału powitania dla obiekt nazwy klastra hello][sap-ha-guide-figure-3019]

  _**Rysunek 30:** przypisać uprawnienia hello hello udziału dla obiekt nazwy klastra hello_

  Pamiętaj, że uprawnienia hello Dołącz dane toochange urzędu hello hello udział dla obiekt nazwy klastra hello (w naszym przykładzie **pr1-ascs-vir$**).

3.  tooadd hello klastra Nazwa obiektu toohello listy, wybierz **Dodaj**. Zmień hello toocheck filtru dla obiektów komputerów w toothose dodanie pokazano na rysunku 31.

  ![Rysunek 31: Zmiana hello typy obiektów tooinclude komputerów][sap-ha-guide-figure-3020]

  _**Rysunek 31:** zmienić hello typy obiektów tooinclude komputerów_

  ![32 rysunku: Zaznacz pole wyboru komputerów hello][sap-ha-guide-figure-3021]

  _**Rysunek 32:** wybierz hello **komputery** pole wyboru_

4.  Wprowadź hello obiektem nazwy klastra, jak pokazano na rysunku 31. Ponieważ hello rekord został już utworzony, można zmienić uprawnienia hello, jak pokazano na rysunku 30.

5.  Wybierz hello **zabezpieczeń** karcie hello udziału, a następnie ustawić bardziej szczegółowe uprawnienia dla obiekt nazwy klastra hello.

  ![Rysunek nr 33: Ustawić atrybutów zabezpieczeń hello dla obiekt nazwy klastra hello na powitania pliku udziału kworum][sap-ha-guide-figure-3022]

  _**Rysunek nr 33:** ustawić atrybutów zabezpieczeń powitania dla obiekt nazwy klastra hello na powitania pliku udziału kworum_

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Ustaw kworum monitora udziału plików hello w Menedżerze klastra trybu Failover

1.  Otwórz hello Konfigurowanie kworum ustawienia kreatora.

  ![Rysunek 34: Start hello kreatora ustawienia kworum klastra konfiguracji][sap-ha-guide-figure-3023]

  _**Rysunek 34:** Start hello kreatora ustawienia konfiguracji kworum klastra_

2.  Na powitania **wybrać konfigurację kworum** wybierz **Wybieranie monitora kworum hello**.

  ![Rysunek 35: Konfiguracji kworum, możesz wybrać z][sap-ha-guide-figure-3024]

  _**Rysunek 35:** konfiguracji kworum, możesz wybrać spośród_

3.  Na powitania **Wybieranie monitora kworum** wybierz **Konfigurowanie monitora udziału plików**.

  ![36 rysunku: Monitor udziału plików wybierz hello][sap-ha-guide-figure-3025]

  _**Rysunek 36:** Wybierz monitor udziału plików hello_

4.  Wprowadź udziału plików toohello ścieżki UNC hello (w naszym przykładzie \\domcontr 0\FSW). toosee listę hello zmiany mogą być, wybierz **dalej**.

  ![Rysunek 37: Zdefiniuj lokalizację udziału plików hello hello monitora udziału][sap-ha-guide-figure-3026]

  _**Rysunek 37:** określić lokalizację udziału plików hello hello monitora udziału_

5.  Wybierz hello zmiany, a następnie wybierz **dalej**. Należy toosuccessfully ponownie skonfigurować hello konfiguracji klastra, jak pokazano na rysunku 38.  

  ![38 rysunku: Czy został ponownie skonfigurować klaster hello potwierdzenie][sap-ha-guide-figure-3027]

  _**Rysunek 38:** potwierdzenie, że zostały ponownie skonfigurować hello klastra_

Po pomyślnym zainstalowaniu klastra pracy awaryjnej systemu Windows hello zmiany muszą toobe wprowadzone toosome progi tooadapt pracy awaryjnej wykrywania tooconditions na platformie Azure. Hello zmienić toobe parametry są opisane w tym blogu: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/. Przy założeniu, że dwóch maszyn wirtualnych, które kompilacji hello konfiguracji klastra systemu Windows dla ASCS/SCS znajdują się w hello tej samej podsieci, hello następujące parametry muszą zmienić toobe toothese wartości:
- SameSubNetDelay = 2
- SameSubNetThreshold = 15

Te ustawienia zostały przetestowane z klientami i dostępne toobe dobrej naruszenia wystarczająco odporne na jednej stronie powitania. Na powitania drugiej te ustawienia zostały udostępnianie fast wystarczająco dużo pracy awaryjnej w warunkach rzeczywistych błędu w przypadku awarii oprogramowania lub węzeł/wirtualna SAP. 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Zainstaluj dla dysku udziału klastra SAP ASCS/SCS hello SIOS DataKeeper Cluster Edition

Masz teraz pracy konfiguracji klastra trybu Failover systemu Windows Server na platformie Azure. Jednak tooinstall wystąpieniem SAP ASCS/SCS należy zasób udostępniony dysk. Nie można utworzyć potrzebne zasoby dysku udostępnionego hello na platformie Azure. SIOS DataKeeper Cluster Edition jest rozwiązań innych firm, można użyć toocreate współużytkowane zasoby dyskowe.

Instalowanie SIOS DataKeeper Cluster Edition dla programu SAP ASCS/SCS hello dysku klastrowego udziału obejmuje te zadania:

- Dodawanie hello .NET Framework 3.5
- Instalowanie SIOS DataKeeper
- Konfigurowanie SIOS DataKeeper

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Dodaj hello .NET Framework 3.5
Hello Microsoft .NET Framework 3.5 nie jest automatycznie aktywowane lub zainstalowany w systemie Windows Server 2012 R2. SIOS DataKeeper wymaga hello toobe .NET Framework na wszystkich węzłach, które należy zainstalować na DataKeeper, dlatego należy zainstalować w systemie operacyjnym gościa hello wszystkich maszyn wirtualnych w klastrze hello hello .NET Framework 3.5.

Istnieją dwa sposoby hello tooadd .NET Framework 3.5:

- Użyj Kreatora hello dodawania ról i funkcji w systemie Windows, jak pokazano 39 rysunku.

  ![Rysunek 39: Zainstaluj hello .NET Framework 3.5 przy użyciu hello dodawania ról i funkcji — Kreator][sap-ha-guide-figure-3028]

  _**Rysunek 39:** hello instalacji programu .NET Framework 3.5 przy użyciu hello dodawania ról i funkcji — Kreator_

  ![40 rysunek: Postęp instalacji pasek po zainstalowaniu hello .NET Framework 3.5 przy użyciu hello dodawania ról i funkcji — Kreator][sap-ha-guide-figure-3029]

  _**Rysunek 40:** pasek po zainstalowaniu hello .NET Framework 3.5 przy użyciu hello dodawania ról i funkcji — Kreator postępu instalacji_

- Użyj hello narzędzia wiersza polecenia dism.exe. Ten typ instalacji należy katalogu SxS hello tooaccess na powitania nośnik instalacyjny systemu Windows. W wierszu polecenia z podwyższonym poziomem uprawnień wpisz polecenie:

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a>Zainstaluj SIOS DataKeeper

Zainstaluj SIOS DataKeeper Cluster Edition w każdym węźle w klastrze hello. toocreate wirtualnego magazynu udostępnionego SIOS DataKeeper Tworzenie zsynchronizowanej dublowania i następnie symulować magazyn udostępniony klastra.

Przed zainstalowaniem oprogramowania SIOS hello, Utwórz użytkownika domeny hello **DataKeeperSvc**.

> [!NOTE]
> Dodaj hello **DataKeeperSvc** toohello użytkownika **administratora lokalnego** na obu węzłów klastra.
>
>

tooinstall SIOS DataKeeper:

1.  Zainstaluj oprogramowanie SIOS hello na obu węzłów klastra.

  ![Instalator SIOS][sap-ha-guide-figure-3030]

  ![41 rysunku: Pierwsza strona hello instalacji SIOS DataKeeper][sap-ha-guide-figure-3031]

  _**Rysunek 41:** pierwszej strony hello SIOS DataKeeper instalacji_

2.  Okno dialogowe hello pokazano na rysunku 42, wybierz **tak**.

  ![Rysunek 42: DataKeeper informuje, czy usługa zostanie wyłączona][sap-ha-guide-figure-3032]

  _**Rysunek 42:** DataKeeper informuje, że usługa zostanie wyłączona_

3.  Okno dialogowe hello pokazano na rysunku 43, zalecane w wybranym **konta domeny lub tego serwera**.

  ![Rysunek 43: Wybór użytkownika dla SIOS DataKeeper][sap-ha-guide-figure-3033]

  _**Rysunek 43:** SIOS DataKeeper określonego użytkownika_

4.  Wprowadź nazwę hello domeny konta użytkownika i hasła, które zostały utworzone dla SIOS DataKeeper.

  ![Rysunek 44: Wprowadź hello domena, nazwa użytkownika i hasło dla hello SIOS DataKeeper instalacji][sap-ha-guide-figure-3034]

  _**Rysunek 44:** wprowadź nazwę użytkownika domeny hello i hasło dla hello SIOS DataKeeper instalacji_

5.  Zainstaluj klucz licencji powitania dla swojego wystąpienia SIOS DataKeeper, jak pokazano na rysunku 45.

  ![Rysunek 45: Wprowadź klucz licencji SIOS DataKeeper][sap-ha-guide-figure-3035]

  _**Rysunek 45:** wprowadź klucz licencji SIOS DataKeeper_

6.  Po wyświetleniu monitu uruchom ponownie maszynę wirtualną hello.

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a>Konfigurowanie SIOS DataKeeper

Po zainstalowaniu SIOS DataKeeper na obu węzłach należy toostart hello konfiguracji. Celem Hello konfiguracji hello jest toohave synchroniczne dane replikacji między hello dodatkowych dysków dołączonych tooeach hello maszyn wirtualnych.

1.  Uruchom hello DataKeeper zarządzanie i narzędzia do konfiguracji, a następnie wybierz **połączenia serwera**. (W 46 rysunku, ta opcja jest zaznaczona kółkiem na czerwono.)

  ![Rysunek 46: SIOS DataKeeper zarządzanie i narzędzia do konfiguracji][sap-ha-guide-figure-3036]

  _**Rysunek 46:** narzędzie SIOS DataKeeper zarządzania i konfiguracji_

2.  Wprowadź nazwę hello lub adres TCP/IP hello pierwszy węzeł hello zarządzania i konfiguracji narzędzia powinny połączenia oraz, w drugim kroku hello drugiego węzła.

  ![Rysunek 47: Wstaw hello nazwę lub adres TCP/IP hello pierwszy węzeł hello zarządzania i konfiguracji narzędzia należy łączyć, a w drugim etapie hello drugiego węzła][sap-ha-guide-figure-3037]

  _**Rysunek 47:** Insert hello nazwę lub adres TCP/IP hello pierwszy węzeł hello zarządzania i konfiguracji narzędzia należy łączyć, a w drugim etapie hello drugiego węzła_

3.  Utwórz zadanie replikacji hello między dwoma węzłami hello.

  ![Rysunek 48: Tworzenie zadania replikacji][sap-ha-guide-figure-3038]

  _**Rysunek 48:** Utwórz zadanie replikacji_

  Kreator prowadzi hello proces tworzenia zadania replikacji.
4.  Zdefiniuj hello nazwa, adres TCP/IP i wolumin dysku hello źródło węzła.

  ![Rysunek 49: Zdefiniuj nazwę hello hello zadania replikacji][sap-ha-guide-figure-3039]

  _**Rysunek 49:** Zdefiniuj nazwę hello hello replikacji zadania_

  ![Rysunek 50: Zdefiniuj hello danych podstawowych dla węzła hello, która powinna być hello bieżącego węzła źródłowego][sap-ha-guide-figure-3040]

  _**Rysunek 50:** zdefiniować hello podstawowe dane dla węzła hello, która powinna być hello bieżącego węzła źródłowego_

5.  Zdefiniuj nazwę hello, adres TCP/IP i wolumin dysku hello docelowego węzła.

  ![Rysunek 51: Zdefiniuj hello danych podstawowych dla węzła hello, która powinna być hello bieżący węzeł docelowy.][sap-ha-guide-figure-3041]

  _**Rysunek 51:** zdefiniować hello podstawowe dane dla węzła hello, która powinna być hello bieżący węzeł docelowy._

6.  Zdefiniuj hello algorytmy kompresji. W naszym przykładzie zaleca się, że kompresji hello replikacji strumienia. Szczególnie w sytuacjach, ponowna synchronizacja kompresji hello strumienia replikacji hello znacznie skraca czas ponownej synchronizacji. Należy pamiętać, że kompresja używa zasobów Procesora i pamięci RAM hello maszyny wirtualnej. Jako hello kompresji szybkość wzrostu tak hello ilości zasobów procesora CPU używanych. Można również dostosować to ustawienie później.

7.  Inny ustawienie konieczne jest toocheck czy hello replikacji asynchronicznie lub synchronicznie. *W przypadku ochrony SAP ASCS/SCS konfiguracji, należy użyć Replikacja synchroniczna*.  

  ![Rysunek 52: Zdefiniuj szczegóły replikacji][sap-ha-guide-figure-3042]

  _**Rysunek 52:** Zdefiniuj szczegóły replikacji_

8.  Należy określić, czy hello wolumin, który jest replikowany za zadanie replikacji hello powinny być reprezentowana tooa Windows Server Failover Clustering konfiguracji klastra jako udostępniony dysk. Witaj SAP ASCS/SCS konfiguracji, wybierz **tak** , dzięki czemu widzi klastra Windows hello hello replikowanego woluminu jako udostępnionego dysku, której można użyć jako woluminu klastra.

  ![Rysunek 53: Wybierz tak tooset hello replikowane wolumin jako wolumin klastra][sap-ha-guide-figure-3043]

  _**Rysunek 53:** wybierz **tak** tooset hello replikowane jako woluminu klastra_

  Po utworzeniu woluminu hello hello DataKeeper zarządzania i konfiguracji narzędzia przedstawia zadania replikacji hello jest aktywny.

  ![Rysunek 54: DataKeeper duplikowanie synchroniczne dla hello SAP ASCS/SCS udziału dysku jest aktywny][sap-ha-guide-figure-3044]

  _**Rysunek 54:** DataKeeper duplikowanie synchroniczne dla hello SAP ASCS/SCS współużytkować dysku jest aktywny_

  Menedżer klastra trybu failover zawiera obecnie hello dysku jako dysku DataKeeper, jak pokazano na rysunku 55.

  ![Rysunek 55: Menedżer klastra trybu Failover zawiera dysk hello replikowane DataKeeper][sap-ha-guide-figure-3045]

  _**Rysunek 55:** Menedżera klastra trybu Failover zawiera dysk hello tego DataKeeper replikowane_

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Instalowanie systemu SAP NetWeaver hello

Instalator systemu DBMS hello nie opisano ustawienia się różnić w zależności od używanego systemu DBMS hello. Jednak przyjęto założenie, że dotyczy wysokiej dostępności z systemu DBMS hello są adresowane za pomocą funkcje hello, obsługiwanych przez różnych dostawców DBMS hello Azure. Na przykład zawsze włączone lub dublowania bazy danych programu SQL Server i Oracle Data Guard dla baz danych Oracle. W scenariuszu hello używanych w tym artykule firma Microsoft nie dodał więcej toohello ochrony systemu DBMS.

Istnieją specjalne uwagi dotyczące różnych usług systemu DBMS interakcji z tego rodzaju konfiguracji klastra SAP ASCS/SCS na platformie Azure.

> [!NOTE]
> procedury instalacji Hello programu SAP NetWeaver ABAP systemów, Java i systemami ABAP + Java są prawie takie same. najbardziej znacząca różnica Hello jest systemu SAP ABAP jedno wystąpienie ASCS. Witaj systemu SAP Java ma jedno wystąpienie SCS. Witaj systemu SAP ABAP + Java ma jedno wystąpienie ASCS i działania jednej wystąpienia SCS hello tej samej grupy klastra trybu failover firmy Microsoft. Różnice instalacji dla każdej stosu instalacji SAP NetWeaver jawnie wymienione. Można założyć, wszystkie inne elementy są hello takie same.  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a>Instalowanie programu SAP przy użyciu wystąpienia ASCS/SCS wysokiej dostępności

> [!IMPORTANT]
> Upewnij się, nie tooplace ze strony plików na DataKeeper dublowanych woluminów. DataKeeper nie obsługuje woluminy dublowane. Można pozostawić pliku stronicowania na powitania tymczasowego dysku D z maszyny wirtualnej platformy Azure, który jest domyślnym hello. Jeśli nie jest już istnieje, należy przenieść hello Windows strony pliku toodrive D: Azure maszyny wirtualnej.
>
>

Instalowanie SAP przy użyciu wystąpienia ASCS/SCS wysokiej dostępności obejmuje następujące zadania:

- Tworzenie nazwę hosta wirtualnego wystąpienia programu SAP ASCS/SCS hello w klastrze
- Instalowanie programu SAP hello pierwszym węźle klastra
- Modyfikowanie profilu SAP hello hello ASCS/SCS wystąpienia
- Dodawanie portu sondy
- Otwarcie portu sondowania zapory systemu Windows hello

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Utwórz nazwę hosta wirtualnego wystąpienia programu SAP ASCS/SCS hello w klastrze

1.  W Menedżerze DNS z systemem Windows hello Utwórz wpis DNS dla nazwy hostów wirtualnych hello hello ASCS/SCS wystąpienia.

  > [!IMPORTANT]
  > Witaj adres IP, który można przypisać nazwę hosta wirtualnego toohello hello ASCS/SCS wystąpienie musi być hello sam jako adres IP hello przypisania tooAzure modułu równoważenia obciążenia (**<*SID*> - lb - ascs **).  
  >
  >

  Witaj adresu IP wirtualnej nazwy hosta SAP ASCS/SCS hello (**pr1 ascs sap**) jest hello takie same jak hello adresu IP usługi równoważenia obciążenia Azure (**pr1-lb-ascs**).

  ![Rysunek 56: Definiowanie hello wpisu DNS dla nazwy wirtualnego hello SAP ASCS/SCS klastra i adres TCP/IP][sap-ha-guide-figure-3046]

  _**Rysunek 56:** zdefiniuj hello wpisu DNS dla nazwy wirtualnego hello SAP ASCS/SCS klastra i adres TCP/IP_

2.  toodefine hello nazwę adresów IP przypisanych toohello hostów wirtualnych, wybierz **Menedżera DNS** > **domeny**.

  ![57 rysunek: Nowa nazwa wirtualnego i adres TCP/IP dla konfiguracji klastra SAP ASCS/SCS][sap-ha-guide-figure-3047]

  _**Rysunek 57:** nową nazwę wirtualnego i TCP/IP adresów dla SAP ASCS/SCS konfiguracji klastra_

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Zainstaluj hello SAP pierwszym węźle klastra

1.  Wykonanie opcję hello do węzła pierwszego klastra w węźle klastra A. Na przykład na powitania **pr1 ascs 0** hosta.
2.  porty domyślne hello tookeep hello Azure wewnętrznego modułu równoważenia obciążenia, wybierz:

  * **ABAP system**: **ASCS** wystąpienie numer **00**
  * **Java system**: **SCS** wystąpienie numer **01**
  * **System ABAP + Java**: **ASCS** wystąpienie numer **00** i **SCS** wystąpienie numer **01**

  wystąpienie toouse innych niż 00 hello ABAP ASCS liczb, wystąpienia i 01 hello Java SCS wystąpienia, należy najpierw toochange hello Azure obciążenia wewnętrznego domyślne równoważenia obciążenia modułu równoważenia reguł, opisanych w [zmiany hello ASCS/SCS domyślne obciążenia Równoważenie zasady hello Azure wewnętrznego modułu równoważenia obciążenia][sap-ha-guide-8.9].

Witaj dalej kilka zadań nie są opisane w hello standardowe SAP instalacji dokumentacji.

> [!NOTE]
> Hello SAP instalacji dokumentacji opisano, jak tooinstall hello pierwszym węźle klastra ASCS/SCS.
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modyfikowanie profilu SAP hello hello ASCS/SCS wystąpienia

Należy tooadd nowy parametr profilu. Parametr profilu Hello zapobiega połączeń między procesów roboczych SAP i hello umieścić serwer zamykania po okresie bezczynności wynoszącym zbyt długo. Wspomniano hello scenariusz problemu w [dodać wpisów rejestru na obu węzłach hello SAP ASCS/SCS wystąpienia][sap-ha-guide-8.11]. W tej sekcji wprowadzono są również dwie zmiany toosome podstawowe TCP/IP Parametry połączenia. W drugim kroku należy tooset hello umieścić serwer toosend `keep_alive` sygnału, dzięki czemu hello połączeń nie osiągnął Próg bezczynności hello Azure wewnętrznego modułu równoważenia obciążenia.

Witaj toomodify profilu SAP wystąpienia ASCS/SCS hello:

1.  Dodaj ten profil parametru toohello SAP ASCS/SCS wystąpienia profilu:

  ```
  enque/encni/set_so_keepalive = true
  ```
  W naszym przykładzie ścieżka hello jest:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  Na przykład toohello SAP SCS wystąpienia profilu i odpowiednie ścieżki:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  tooapply hello zmiany, ponownie uruchom wystąpienie /SCS SAP ASCS hello.

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a>Dodaj port sondy

Używać funkcji hello wewnętrznego modułu równoważenia obciążenia sondowania funkcji toomake hello całego klastra konfiguracji Praca z modułem równoważenia obciążenia w Azure. Hello Azure wewnętrznego modułu równoważenia obciążenia zwykle rozdziela przychodzące obciążenie hello równomiernie w poszczególnych uczestniczących maszyn wirtualnych. Jednak to nie będzie działać w niektórych konfiguracjach klastra, ponieważ jest aktywna tylko jedno wystąpienie. Hello inne wystąpienie jest w stanie pasywnym i nie akceptuje dowolne hello obciążenia. Funkcja badania pomaga przypisuje usługi równoważenia obciążenia Azure wewnętrzny hello działa tylko tooan aktywnym wystąpieniu. Z funkcją sondowania hello hello wewnętrznego modułu równoważenia obciążenia może wykryć, które wystąpienia są aktywne, a następnie tylko hello wystąpienia z obciążenia hello docelowego.

port sondy tooadd:

1.  Sprawdź bieżący hello **ProbePort** ustawienie, uruchamiając następujące polecenia programu PowerShell hello. Wykonanie go z jednej z maszyn wirtualnych hello w konfiguracji klastra hello.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  Zdefiniuj port sondy. Witaj domyślny numer portu sondy jest **0**. W tym przykładzie używamy port sondy **62000**.

  ![Rysunek 58: port sondy konfiguracji klastra hello jest 0 domyślnie][sap-ha-guide-figure-3048]

  _**Rysunek 58:** port sondy konfiguracji klastra domyślne hello wynosi 0_

  numer portu Hello jest zdefiniowany w szablonach SAP usługi Azure Resource Manager. Można przypisać numer portu hello w programie PowerShell.

  tooset nową wartość ProbePort hello  **SAP <*SID*> IP ** zasobu klastra, uruchom hello następującego skryptu programu PowerShell. Zaktualizuj hello zmiennych środowiska PowerShell dla danego środowiska. Po uruchomieniu skryptu hello się, zostanie wyświetlony monit o toorestart hello SAP grupy tooactivate hello zmiany dotyczące klastra.

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

  Po przełączeniu hello  **SAP <*SID*> ** klastra roli w tryb online, upewnij się, że **ProbePort** ustawiono toohello nową wartość.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Rysunek 59: Sondowania hello portu klastra po ustawieniu hello nowej wartości][sap-ha-guide-figure-3049]

  _**Rysunek 59:** sondowania portu klastra powitania po ustawieniu hello nowej wartości_

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Otwórz port sondy zapory systemu Windows hello

Należy tooopen port sondy zapory systemu Windows na obu węzłów klastra. Użyj następującego skryptu tooopen port sondy zapory systemu Windows hello. Zaktualizuj hello zmiennych środowiska PowerShell dla danego środowiska.

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

Witaj **ProbePort** ustawiono zbyt**62000**. Teraz można dostęp do udziału plików hello  **\\\ascsha-clsap\sapmnt** od innych hostów, takie jak z **ascsha dbas**.

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Zainstaluj hello wystąpienia bazy danych

Baza danych hello tooinstall wystąpienia, należy wykonać hello procesu opisanego w hello dokumentacji instalacji SAP.

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Zainstaluj hello drugiego węzła klastra

tooinstall hello drugi klaster, wykonaj kroki hello hello SAP w podręczniku instalacji.

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Zmień typ uruchomienia hello wystąpienie usługi SAP Wywołujących Windows hello

Zmień typ uruchamiania usługi SAP Wywołujących Windows hello hello zbyt**automatycznie (opóźnione uruchomienie)** na obu węzłów klastra.

![Rysunek 60: Zmień typ usługi hello hello Wywołujących SAP wystąpienia toodelayed automatyczne][sap-ha-guide-figure-3050]

_**Rysunek 60:** zmienić typ usługi hello hello Wywołujących SAP wystąpienia toodelayed automatyczne_

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Zainstaluj hello SAP podstawowego serwera aplikacji

Zainstaluj wystąpienie serwera aplikacji głównej (adresy) hello <*SID*> - podpisane - 0 na maszynie wirtualnej hello, który został wybrany toohost hello adresy dostawcy. Nie ma żadnych zależności, Azure lub DataKeeper określonych ustawień.

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Zainstaluj hello SAP dodatkowego serwera aplikacji

Zainstaluj SAP dodatkowych aplikacji serwera (AAS) na wszystkich maszynach wirtualnych hello, że ustawiono toohost wystąpienia serwera aplikacji SAP. Na przykład na <*SID*> - podpisane - 1 za <*SID*> - podpisane -&lt;n&gt;.

> [!NOTE]
> Zakończy się instalacja hello systemu SAP NetWeaver wysokiej dostępności. Następnie należy kontynuować testowanie trybu failover.
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Testowanie trybu failover wystąpienia programu SAP ASCS/SCS hello i SIOS replikacji
Jest łatwy tootest i monitorowanie trybu failover wystąpienia programu SAP ASCS/SCS i replikacji dysku SIOS za pomocą Menedżera klastra trybu Failover i narzędzia hello SIOS DataKeeper zarządzania i konfiguracji.

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a>W węźle klastra, A jest uruchomione wystąpienie SAP ASCS/SCS

Witaj **SAP PR1** grupy klastra jest uruchomiona w węźle klastra A. Na przykład na **pr1 ascs 0**. Przypisz hello udostępnionego dysku S, który jest częścią hello **SAP PR1** grupy i które wystąpienie ASCS/SCS hello używa toocluster A. węzła klastra

![61 rysunek: Menedżer klastra trybu Failover: Grupa klastra SAP < SID > hello jest uruchomiona w węźle klastra, A][sap-ha-guide-figure-5000]

_**Rysunek 61:** Menedżera klastra trybu Failover: hello SAP <*SID*> grupy klastra jest uruchomiona w węźle klastra, A_

Witaj SIOS DataKeeper zarządzanie i narzędzia do konfiguracji zawiera tego hello dysk udostępniony, który dane są replikowane synchronicznie w z dysku woluminu źródłowego hello S w węźle klastra toohello dysku woluminu docelowego S w węźle klastra B. Na przykład są replikowane z **pr1 ascs 0 [10.0.0.40]** za**pr1 ascs 1 [10.0.0.41]**.

![Rysunek 62: W SIOS DataKeeper replikowane woluminu lokalne powitania z węzła z klastra węzeł toocluster B][sap-ha-guide-figure-5001]

_**Rysunek 62:** w SIOS DataKeeper replikowane woluminu lokalne powitania z węzła z klastra węzeł toocluster B_

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Tryb failover z węzła A toonode B

1.  Wybierz jedną z tych opcji tooinitiate awarię hello SAP <*SID*> Grupa klastra z klastra węzeł A toocluster węzeł B:
  - Menedżer klastra trybu Failover  
  - Za pomocą programu PowerShell klastra trybu Failover

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  Uruchom ponownie, A węzeł klastra w systemie operacyjnym gościa Windows hello (powoduje to zainicjowanie automatycznej pracy awaryjnej hello SAP <*SID*> Grupa klastra z węzła A toonode B).  
3.  Uruchom ponownie, A węzeł klastra z hello portalu Azure (powoduje to zainicjowanie automatycznej pracy awaryjnej hello SAP <*SID*> Grupa klastra z węzła A toonode B).  
4.  Uruchom ponownie A węzła klastra za pomocą programu Azure PowerShell (powoduje to zainicjowanie automatycznej pracy awaryjnej hello SAP <*SID*> Grupa klastra z węzła A toonode B).

  Po przejściu w tryb failover, hello SAP <*SID*> grupy klastra jest uruchomiona w węźle klastra B. Na przykład, że jest uruchomiona w **pr1 ascs 1**.

  ![Rysunek 63: W Menedżerze klastra trybu Failover Grupa klastra SAP < SID > hello jest uruchomiona w węźle klastra B][sap-ha-guide-figure-5002]

  _**Rysunek 63**: W Menedżerze klastra trybu Failover, hello SAP <*SID*> grupy klastra jest uruchomiona w węźle klastra B_

  Witaj udostępniony dysk jest teraz zainstalowany w klastrze węzła B. SIOS DataKeeper jest replikowanie danych z dysku woluminu źródłowego S na węzeł B tootarget woluminu dysku klastrowego S w węźle klastra A. Na przykład jest replikowany z **pr1 ascs 1 [10.0.0.41]** za**pr1 ascs 0 [10.0.0.40]**.

  ![Rysunek 64: SIOS DataKeeper replikuje woluminu lokalne powitania z klastra węzeł B toocluster węzła A][sap-ha-guide-figure-5003]

  _**Rysunek 64:** SIOS DataKeeper replikuje woluminu lokalne powitania z klastra węzeł B toocluster węzeł A_
