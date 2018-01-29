---
title: "SAP NetWeaver instalacji o wysokiej dostępności na Windows trybu failover klastra i udział plików dla programu SAP ASCS/SCS wystąpień na platformie Azure | Dokumentacja firmy Microsoft"
description: "SAP NetWeaver instalacji o wysokiej dostępności na Windows trybu failover klastra i udział plików dla programu SAP ASCS/SCS wystąpień"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 71296618-673b-4093-ab17-b7a80df6e9ac
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc957ece0250d233db9cec4f1fdd8b063c13a136
ms.sourcegitcommit: a036a565bca3e47187eefcaf3cc54e3b5af5b369
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/17/2017
---
# <a name="install-sap-netweaver-high-availability-on-a-windows-failover-cluster-and-file-share-for-sap-ascsscs-instances-on-azure"></a>Zainstaluj SAP NetWeaver wysokiej dostępności na Windows trybu failover klastra i udział plików dla programu SAP ASCS/SCS wystąpień na platformie Azure

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1596496]:https://launchpad.support.sap.com/#/notes/1596496

[sap-installation-guides]:http://service.sap.com/instguides

[sap-powershell-scrips]:https://github.com/Azure-Samples/sap-powershell

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[s2d-in-win-2016]:https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview
[sofs-overview]:https://technet.microsoft.com/library/hh831349(v=ws.11).aspx
[new-in-win-2016-storage]:https://docs.microsoft.com/windows-server/storage/whats-new-in-storage

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[sap-blog-new-sap-cluster-resource-dll]:https://blogs.sap.com/2017/08/28/new-sap-cluster-resource-dll-is-available/
[sap-high-availability-architecture-scenarios]:sap-high-availability-architecture-scenarios.md
[sap-high-availability-guide-wsfc-shared-disk]:sap-high-availability-guide-wsfc-shared-disk.md
[sap-high-availability-guide-wsfc-file-share]:sap-high-availability-guide-wsfc-file-share.md
[sap-ascs-high-availability-multi-sid-wsfc]:sap-ascs-high-availability-multi-sid-wsfc.md
[sap-high-availability-infrastructure-wsfc-shared-disk]:sap-high-availability-infrastructure-wsfc-shared-disk.md
[sap-high-availability-infrastructure-wsfc-file-share]:sap-high-availability-infrastructure-wsfc-file-share.md
[sap-high-availability-installation-wsfc-shared-disk]:sap-high-availability-installation-wsfc-shared-disk.md
[sap-hana-ha]:sap-hana-high-availability.md
[sap-suse-ascs-ha]:high-availability-guide-suse.md

[sap-high-availability-installation-wsfc-shared-disk]:sap-high-availability-installation-wsfc-shared-disk.md
[sap-high-availability-installation-wsfc-shared-disk-create-ascs-virt-host]:sap-high-availability-installation-wsfc-shared-disk.md#a97ad604-9094-44fe-a364-f89cb39bf097
[sap-high-availability-installation-wsfc-shared-disk-add-probe-port]:sap-high-availability-installation-wsfc-shared-disk.md#10822f4f-32e7-4871-b63a-9b86c76ce761

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-high-availability-infrastructure-wsfc-shared-disk]:sap-high-availability-infrastructure-wsfc-shared-disk.md

[sap-high-availability-infrastructure-wsfc-shared-disk]:sap-high-availability-infrastructure-wsfc-shared-disk.md
[sap-high-availability-infrastructure-wsfc-shared-disk-vpn]:sap-high-availability-infrastructure-wsfc-shared-disk.md#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-high-availability-infrastructure-wsfc-shared-disk-change-def-ilb]:sap-high-availability-infrastructure-wsfc-shared-disk.md#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-high-availability-infrastructure-wsfc-shared-disk-setup-wsfc]:sap-high-availability-infrastructure-wsfc-shared-disk.md#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-high-availability-infrastructure-wsfc-shared-disk-collect-cluster-config]:sap-high-availability-infrastructure-wsfc-shared-disk.md#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-high-availability-infrastructure-wsfc-shared-disk-install-sios]:sap-high-availability-infrastructure-wsfc-shared-disk.md#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-high-availability-infrastructure-wsfc-shared-disk-add-dot-net]:sap-high-availability-infrastructure-wsfc-shared-disk.md#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-high-availability-infrastructure-wsfc-shared-disk-install-sios-both-nodes]:sap-high-availability-infrastructure-wsfc-shared-disk.md#dd41d5a2-8083-415b-9878-839652812102
[sap-high-availability-infrastructure-wsfc-shared-disk-setup-sios]:sap-high-availability-infrastructure-wsfc-shared-disk.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006

[sap-official-ha-file-share-document]:https://www.sap.com/documents/2017/07/f453332f-c97c-0010-82c7-eda71af511fa.html

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

W tym artykule opisano sposób instalowania i konfigurowania systemu SAP wysokiej dostępności na platformie Azure, za pomocą usługi Windows Server Failover Cluster (WSFC) i serwera plików skalowalnego w poziomie jako opcję SAP ASCS/SCS wystąpienia klastra.

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem instalacji, przejrzyj następujące artykuły:

* [Przewodnik dotyczący architektury: klastra SAP ASCS/SCS wystąpienia klastra trybu failover z systemem Windows przy użyciu udziału plików][sap-high-availability-guide-wsfc-file-share]

* [Przygotowanie infrastruktury platformy Azure SAP wysokiej dostępności dzięki użyciu udziału klastra i plików trybu failover systemu Windows dla programu SAP ASCS/SCS wystąpień][sap-high-availability-infrastructure-wsfc-file-share]

Potrzebujesz następujących plików wykonywalnych i bibliotek DLL z SAP:
* SAP oprogramowania inicjowania obsługi administracyjnej Menedżera (SWPM) wersja narzędzia instalacyjnego SPS21 lub nowszym.
* Pobierz najnowsze NTCLUST. Archiwum SAR z SAP nowego klastra Biblioteka DLL zasobów. Nowy SAP klaster Obsługa bibliotek DLL SAP ASCS/SCS wysokiej dostępności z udziału plików w klastrze trybu Failover systemu Windows Server.

  Aby uzyskać więcej informacji na temat nowy zasób klastra SAP biblioteki DLL, zobacz ten blog: [Biblioteka DLL zasobów klastra nowe SAP jest dostępna!] [sap-blog-new-sap-cluster-resource-dll].

Firma Microsoft nie opisują Instalatora systemu zarządzania bazy danych (DBMS), konfiguracje się różnić w zależności od systemu DBMS używasz. Jednak przyjęto założenie, reagowania problemów o wysokiej dostępności z systemu DBMS z funkcje obsługujące przez różnych dostawców DBMS dla platformy Azure. Takie funkcje obejmują funkcji AlwaysOn lub dublowania bazy danych programu SQL Server i Oracle Data Guard dla baz danych Oracle. W tym scenariuszu używanych w tym artykule firma Microsoft nie dodał zwiększają ochronę dla systemu DBMS.

Istnieją specjalne uwagi dotyczące różnych usług systemu DBMS interakcji z tego rodzaju konfiguracji klastra SAP ASCS/SCS na platformie Azure.

> [!NOTE]
> Procedury instalacji programu SAP NetWeaver ABAP systemów, Java i systemami ABAP + Java są prawie takie same. Najbardziej znacząca różnica jest systemu SAP ABAP jedno wystąpienie ASCS. Systemu SAP Java ma jedno wystąpienie SCS. Systemu SAP ABAP + Java ma jedno wystąpienie ASCS i jedno wystąpienie SCS uruchomiony w tej samej grupie klastra trybu failover firmy Microsoft. Różnice instalacji dla każdej stosu instalacji SAP NetWeaver jawnie wymienione. Można założyć, że wszystkie inne elementy są takie same.  
>
>

## <a name="install-an-ascsscs-instance-on-an-ascsscs-cluster"></a>Instalowanie wystąpienia ASCS/SCS w klastrze ASCS/SCS

> [!IMPORTANT]
>
> Obecnie ustawienia wysokiej dostępności z konfiguracji udziału plików nie jest obsługiwana przez narzędzie instalacji SAP SWPM. W związku z tym niektóre ręczne przyjęcie jest niezbędne do zainstalowania systemu SAP (na przykład, aby zainstalować i SAP ASCS/SCS wystąpienia klastra i skonfigurować oddzielne hosta globalne SAP).  
>
> Nie została zmieniona w innych instalacji opis kroków instalacji (i klastrowania) systemu DBMS wystąpienia i SAP serwerów aplikacji.
>

### <a name="install-an-ascsscs-instance-on-your-local-drive"></a>Instalowanie wystąpienia ASCS/SCS na lokalnym dysku

Instalowanie wystąpienia programu SAP ASCS/SCS w *zarówno* węzłów klastra ASCS/SCS. Go zainstalować na dysku lokalnym. W naszym przykładzie dysk lokalny jest C:\\, ale można wybrać inny dysk lokalny.  

Aby zainstalować wystąpienie, w narzędziu instalacji SAP SWPM, przejdź do:

**\<Produktu >** > **\<DBMS >** > **instalacji** > **serwera aplikacji ABAP**(lub **Java**) > **rozproszony System** > **ASCS/SCS wystąpienia**

> [!IMPORTANT]
> Obecnie scenariusz udziału plików nie jest obsługiwany przez narzędzie instalacji SAP SWPM. Możesz *nie można użyć* następująca ścieżka instalacji:
>
> **\<Produktu >** > **\<DBMS >** > **instalacji** > **serwera aplikacji ABAP**(lub **Java**) > **wysokiej dostępności systemu** >...
>

### <a name="remove-sapmnt-and-create-an-saploc-file-share"></a>Usuń SAPMNT i utworzenie udziału plików SAPLOC

SWMP utworzone udostępniania SAPMNT w C:\\usr\\folderu sap.

Usuń udział plików SAPMNT na *zarówno* ASCS/SCS węzły klastra.

Uruchom następujący skrypt programu PowerShell:

```PowerShell
Remove-SmbShare sapmnt -ScopeName * -Force
 ```

Jeśli udział SAPLOC nie istnieje, utwórz ją na *zarówno* ASCS/SCS węzły klastra.

Uruchom następujący skrypt programu PowerShell:

```PowerShell
#Create SAPLOC share and set security
$SAPSID = "PR1"
$DomainName = "SAPCLUSTER"
$SAPSIDGlobalAdminGroupName = "$DomainName\SAP_" + $SAPSID + "_GlobalAdmin"
$HostName = $env:computername
$SAPLocalAdminGroupName = "$HostName\SAP_LocalAdmin"
$SAPDisk = "C:"
$SAPusrSapPath = "$SAPDisk\usr\sap"

New-SmbShare -Name saploc -Path c:\usr\sap -FullAccess "BUILTIN\Administrators", $SAPSIDGlobalAdminGroupName , $SAPLocalAdminGroupName  
 ```

## <a name="prepare-an-sap-global-host-on-the-sofs-cluster"></a>Przygotowanie hosta globalne SAP w klastrze SOFS

Utwórz następujące woluminu i udział plików w klastrze SOFS:

* Plik SAP GLOBALHOST C:\ClusterStorage\Volume1\usr\sap\\<SID>\SYS\ struktury w klastrze SOFS udostępniony wolumin (CSV)

* SAPMNT udziału plików

* Ustawienia zabezpieczeń na SAPMNT udziału plików i folderów z pełnej kontroli dla:
    * \<Domeny > \SAP_\<SID > _GlobalAdmin grupy użytkowników
    * Obiekty komputera węzła klastra ASCS/SCS programu SAP \<domeny > \ClusterNode1$ i \<domeny > \ClusterNode2$

Do utworzenia woluminu CSV o odporności dublowanej, wykonaj następujące polecenie cmdlet programu PowerShell na jednym z węzłów klastra SOFS:


```PowerShell
New-Volume -StoragePoolFriendlyName S2D* -FriendlyName SAPPR1 -FileSystem CSVFS_ReFS -Size 5GB -ResiliencySettingName Mirror
```
Do utworzenia SAPMNT i ustawienia zabezpieczeń folderu i udziału, uruchom następujący skrypt programu PowerShell na jednym z węzłów klastra SOFS:

```PowerShell
# Create SAPMNT on file share
$SAPSID = "PR1"
$DomainName = "SAPCLUSTER"
$SAPSIDGlobalAdminGroupName = "$DomainName\SAP_" + $SAPSID + "_GlobalAdmin"

# SAP ASCS/SCS cluster nodes
$ASCSClusterNode1 = "ascs-1"
$ASCSClusterNode2 = "ascs-2"

# Define SAP ASCS/SCS cluster node computer objects
$ASCSClusterObjectNode1 = "$DomainName\$ASCSClusterNode1$"
$ASCSClusterObjectNode2 = "$DomainName\$ASCSClusterNode2$"

# Create usr\sap\.. folders on CSV
$SAPGlobalFolder = "C:\ClusterStorage\Volume1\usr\sap\$SAPSID\SYS"
New-Item -Path $SAPGlobalFOlder -ItemType Directory

$UsrSAPFolder = "C:\ClusterStorage\Volume1\usr\sap\"

# Create a SAPMNT file share and set share security
New-SmbShare -Name sapmnt -Path $UsrSAPFolder -FullAccess "BUILTIN\Administrators", $SAPSIDGlobalAdminGroupName, $ASCSClusterObjectNode1, $ASCSClusterObjectNode2 -ContinuouslyAvailable $false -CachingMode None -Verbose

# Get SAPMNT file share security settings
Get-SmbShareAccess sapmnt

# Set file and folder security
$Acl = Get-Acl $UsrSAPFolder

# Add a file security object of SAP_<sid>_GlobalAdmin group
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule($SAPSIDGlobalAdminGroupName,"FullControl", 'ContainerInherit,ObjectInherit', 'None', 'Allow')
$Acl.SetAccessRule($Ar)

# Add  a security object of the clusternode1$ computer object
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule($ASCSClusterObjectNode1,"FullControl",'ContainerInherit,ObjectInherit', 'None', 'Allow')
$Acl.SetAccessRule($Ar)

# Add a security object of the clusternode2$ computer object
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule($ASCSClusterObjectNode2,"FullControl",'ContainerInherit,ObjectInherit', 'None', 'Allow')
$Acl.SetAccessRule($Ar)

# Set security
Set-Acl $UsrSAPFolder $Acl -Verbose
 ```
## <a name="stop-ascsscs-instances-and-sap-services"></a>Zatrzymaj ASCS/SCS wystąpień i usługi SAP

Wykonaj następujące czynności:
1. Zatrzymaj wystąpień SAP ASCS/SCS na obu węzłach ASCS/SCS.
2. Zatrzymaj usługi Windows ASCS/SCS SAP **SAP\<SID > _\<InstanceNumber >** na obu węzłów klastra.

## <a name="move-the-sys-folder-to-the-sofs-cluster"></a>Przenieś \SYS\.. folderu do klastra SOFS

Wykonaj następujące czynności:
1. Skopiuj SYS folder (na przykład C:\usr\sap\\<SID>\SYS) z jednego z ASCS/SCS węzły klastra do klastra SOFS (na przykład, aby C:\ClusterStorage\Volume1\usr\sap\\<SID>\SYS).
2. Usuń C:\usr\sap\\<SID>\SYS folderu z obu węzłów klastra ASCS/SCS.

## <a name="update-the-cluster-security-setting-on-the-sap-ascsscs-cluster"></a>Ustawienia zabezpieczeń klastra w klastrze SAP ASCS/SCS aktualizacji

Uruchom następujący skrypt programu PowerShell na jednym z węzłów klastra SAP ASCS/SCS:

```PowerShell
# Grant <DOMAIN>\SAP_<SID>_GlobalAdmin group access to the cluster

$SAPSID = "PR1"
$DomainName = "SAPCLUSTER"
$SAPSIDGlobalAdminGroupName = "$DomainName\SAP_" + $SAPSID + "_GlobalAdmin"

# Set full access for the <DOMAIN>\SAP_<SID>_GlobalAdmin group
Grant-ClusterAccess -User $SAPSIDGlobalAdminGroupName -Full

#Check security settings
Get-ClusterAccess
```

## <a name="create-a-virtual-host-name-for-the-clustered-sap-ascsscs-instance"></a>Utwórz nazwę hosta wirtualnego wystąpienia klastra programu SAP ASCS/SCS

Utwórz SAP ASCS/SCS nazwy sieciowej klastra (na przykład **pr1-ascs [10.0.6.7]**), zgodnie z opisem w [Utwórz nazwę hosta wirtualnego wystąpienia klastra programu SAP ASCS/SCS] [ sap-high-availability-installation-wsfc-shared-disk-create-ascs-virt-host] .

## <a name="update-the-default-and-sap-ascsscs-instance-profile"></a>Zaktualizuj domyślne i SAP ASCS/SCS wystąpienia profilu

Do użycia nowej nazwy hostów wirtualnych SAP ASCS/SCS i SAP nazwy hosta globalnego, należy zaktualizować domyślne i SAP ASCS/SCS wystąpienia profilu \<SID >_ASCS/SCS\<Nr >_<Host>.


| Stare wartości |  |
| --- | --- |
| Nazwa hosta SAP ASCS/SCS = hosta globalne SAP | ascs-1 |
| Nazwa profilu SAP ASCS/SCS wystąpienia | PR1_ASCS00_ascs-1 |

| Nowe wartości |  |
| --- | --- |
| Nazwa hosta SAP ASCS/SCS | **PR1 ascs** |
| Globalne hosta SAP | **sapglobal** |
| Nazwa profilu SAP ASCS/SCS wystąpienia | PR1\_ASCS00\_**pr1 ascs** |

### <a name="update-sap-default-profile"></a>Aktualizuj profil domyślny SAP


| Nazwa parametru | Wartość parametru |
| --- | --- |
| SAPGLOBALHOST | **sapglobal** |
| rdisp/mshost | **PR1 ascs** |
| umieścić/serverhost | **PR1 ascs** |

### <a name="update-the-sap-ascsscs-instance-profile"></a>Aktualizuj profil wystąpieniem SAP ASCS/SCS

| Nazwa parametru | Wartość parametru |
| --- | --- |
| SAPGLOBALHOST | **sapglobal** |
| DIR_PROFILE | \\\sapglobal\sapmnt\PR1\SYS\profile |
| _PF | $(DIR_PROFILE) \PR1\_ASCS00_ pr1-ascs |
| Restart_Program_02 = local$(_MS) pf=$(_PF) | **Uruchom**_Program_02 = local$(_MS) pf=$(_PF) |
| SAPLOCALHOST | **PR1 ascs** |
| Restart_Program_03 = local$(_EN) pf=$(_PF) | **Uruchom**_Program_03 = local$(_EN) pf=$(_PF) |
| GW/netstat_once | **0** |
| umieścić/encni/set_so_keepalive  | **wartość true** |
| Usługa/ha_check_node | **1** |

> [!IMPORTANT]
>Można użyć **SAPASCSSCSProfile aktualizacji** polecenia cmdlet programu PowerShell do automatyzacji aktualizacji profilu.
>
>Polecenia cmdlet programu PowerShell obsługuje zarówno SAP ABAP ASCS, jak i SAP Java SCS wystąpień.
>

Kopiuj [ **SAPScripts.psm1** ] [ sap-powershell-scrips] na lokalny dysk C:\tmp, a następnie uruchom następujące polecenie cmdlet programu PowerShell:

```PowerShell
Import-Module C:\tmp\SAPScripts.psm1

Update-SAPASCSSCSProfile -PathToAscsScsInstanceProfile \\sapglobal\sapmnt\PR1\SYS\profile\PR1_ASCS00_ascs-1 -NewASCSHostName pr1-ascs -NewSAPGlobalHostName sapglobal -Verbose  
```

![Rysunek 1: Dane wyjściowe SAPScripts.psm1][sap-ha-guide-figure-8012]

_**Rysunek 1**: SAPScripts.psm1 danych wyjściowych_

## <a name="update-the-sidadm-user-environment-variable"></a>Aktualizacja \<sid > zmienną środowiskową adm

1. Aktualizacja \<sid > adm użytkownika środowiska nowych GLOBALHOST ścieżkę UNC w *zarówno* ASCS/SCS węzły klastra.
2. Zaloguj się jako \<identyfikatora sid > użytkownika adm, a następnie uruchom narzędzia Regedit.exe.
3. Przejdź do **HKEY_CURRENT_USER** > **środowiska**, a następnie zaktualizuj zmienne do nowej wartości:

| Zmienna | Wartość |
| --- | --- |
| RSEC_SSFS_DATAPATH | \\\\**sapglobal**\sapmnt\PR1\SYS\global\security\rsecssfs\data |
| RSEC_SSFS_KEYPATH | \\\\**sapglobal**\sapmnt\PR1\SYS\global\security\rsecssfs\key |
| SAPEXE | \\\\**sapglobal**\sapmnt\PR1\SYS\exe\uc\NTAMD64 |
| SAPLOCALHOST  | **PR1 ascs** |


## <a name="install-a-new-saprcdll-file"></a>Instalowanie nowego pliku saprc.dll

1. Instalowanie nowej wersji zasobu klastra SAP, który obsługuje scenariusz udziału plików.

2. Pobierz najnowsze NTCLUST. Pakiet SAR z portalu Marketplace usługi SAP.

3. Rozpakuj NTCLUS. SAR na jednym z ASCS/SCS węzły klastra, a następnie uruchom następujące polecenie w wierszu polecenia, aby zainstalować nowy plik saprc.dll:

```
.\NTCLUST\insaprct.exe -yes -install
```

Nowy plik saprc.dll jest zainstalowany na obu węzłach ASCS/SCS.

Aby uzyskać więcej informacji, zobacz [1596496 Uwaga SAP — jak zaktualizować typu zasobu SAP biblioteki dll do Monitor zasobów klastra][1596496].

## <a name="create-a-sap-sid-cluster-group-network-name-and-ip"></a>Utwórz SAP <SID> grupy, nazwy sieciowej i adresu IP klastra

Aby utworzyć SAP \<SID > grupy klastrów, Nazwa sieciowa ASCS/SCS i odpowiedni adres IP, uruchom następujące polecenie cmdlet programu PowerShell:

```PowerShell
# Create SAP Cluster Group
$SAPSID = "PR1"
$SAPClusterGroupName = "SAP $SAPSID"
$SAPIPClusterResourceName = "SAP $SAPSID IP"
$SAPASCSNetworkName = "pr1-ascs"
$SAPASCSIPAddress = "10.0.6.7"
$SAPASCSSubnetMask = "255.255.255.0"

# Create an SAP ASCS instance virtual IP cluster resource
Add-ClusterGroup -Name $SAPClusterGroupName -Verbose

#Create an SAP ASCS virtual IP address
$SAPIPClusterResource = Add-ClusterResource -Name $SAPIPClusterResourceName -ResourceType "IP Address" -Group $SAPClusterGroupName -Verbose

# Set a static IP address
$param1 = New-Object Microsoft.FailoverClusters.PowerShell.ClusterParameter $SAPIPClusterResource,Address,$SAPASCSIPAddress
$param2 = New-Object Microsoft.FailoverClusters.PowerShell.ClusterParameter $SAPIPClusterResource,SubnetMask,$SAPASCSSubnetMask
$params = $param1,$param2
$params | Set-ClusterParameter

# Create a corresponding network name
$SAPNetworkNameClusterResourceName = $SAPASCSNetworkName
Add-ClusterResource -Name $SAPNetworkNameClusterResourceName -ResourceType "Network Name" -Group $SAPClusterGroupName -Verbose

# Set a network DNS name
$SAPNetworkNameClusterResource = Get-ClusterResource $SAPNetworkNameClusterResourceName
$SAPNetworkNameClusterResource | Set-ClusterParameter -Name Name -Value $SAPASCSNetworkName

#Check the updated values
$SAPNetworkNameClusterResource | Get-ClusterParameter

#Set resource dependencies
Set-ClusterResourceDependency -Resource $SAPNetworkNameClusterResourceName -Dependency "[$SAPIPClusterResourceName]" -Verbose

#Start an SAP <SID> cluster group
Start-ClusterGroup -Name $SAPClusterGroupName -Verbose
```

## <a name="register-the-sap-start-service-on-both-nodes"></a>Zarejestruj usługę start SAP na obu węzłach

Zarejestruj ponownie usługę SAP ASCS/SCS start wskaż polecenie Nowy profil i ścieżka profilu.

Ta ponowna rejestracja musi być wykonywany na *zarówno* ASCS/SCS węzły klastra.

W wierszu polecenia z podwyższonym poziomem uprawnień uruchom następujące polecenie:

```
C:\usr\sap\PR1\ASCS00\exe\sapstartsrv.exe -r -p \\sapglobal\sapmnt\PR1\SYS\profile\PR1_ASCS00_pr1-ascs -s PR1 -n 00 -U SAPCLUSTER\SAPServicePR1 -P mypasswd12 -e SAPCLUSTER\pr1adm
```

![Rysunek 2: Ponownie zainstaluj usługę SAP][sap-ha-guide-figure-8013]

_**Rysunek 2**: Usługa ponownej instalacji programu SAP_

Upewnij się, że parametry są poprawne, a następnie wybierz **ręcznego** jako **uruchamiana**.

## <a name="stop-the-ascsscs-service"></a>Zatrzymaj usługę ASCS/SCS

Zatrzymaj usługę SAP ASCS/SCS SAP\<SID > _\<InstanceNumber > ASCS/SCS oba węzły klastra.

## <a name="create-a-new-sap-service-and-sap-instance-resources"></a>Utwórz nową usługę SAP i zasoby wystąpienie SAP

Aby zakończyć tworzenie zasobów SAP SAP\<SID > Grupa klastrów, utworzenie następujących zasobów:

* SAP \<SID > \<InstanceNumber > Usługa
* SAP \<SID > \<InstanceNumber > wystąpienia

Uruchom następujące polecenie cmdlet programu PowerShell:

```PowerShell
$SAPSID = "PR1"
$SAPInstanceNumber = "00"
$SAPNetworkNameClusterResourceName = "pr1-ascs"

$SAPServiceName = "SAP$SAPSID"+ "_" + $SAPInstanceNumber

$SAPClusterGroupName = "SAP $SAPSID"
$SAPServiceClusterResourceName = "SAP $SAPSID $SAPInstanceNumber Service"

$SAPASCSServiceClusterResource = Add-ClusterResource -Name $SAPServiceClusterResourceName -Group $SAPClusterGroupName -ResourceType "SAP Service" -SeparateMonitor -Verbose
$SAPASCSServiceClusterResource  | Set-ClusterParameter  -Name ServiceName -Value $SAPServiceName

#Set resource dependencies
Set-ClusterResourceDependency -Resource $SAPASCSServiceClusterResource  -Dependency "[$SAPNetworkNameClusterResourceName]" -Verbose

$SAPInstanceClusterResourceName = "SAP $SAPSID $SAPInstanceNumber Instance"

# Create SAP instance cluster resource
$SAPASCSServiceClusterResource = Add-ClusterResource -Name $SAPInstanceClusterResourceName -Group $SAPClusterGroupName -ResourceType "SAP Resource" -SeparateMonitor -Verbose

#Set SAP instance cluster resource parameters
$SAPASCSServiceClusterResource  | Set-ClusterParameter  -Name SAPSystemName -Value $SAPSID -Verbose
$SAPASCSServiceClusterResource  | Set-ClusterParameter  -Name SAPSystem -Value $SAPInstanceNumber -Verbose

#Set resource dependencies
Set-ClusterResourceDependency -Resource $SAPASCSServiceClusterResource  -Dependency "[$SAPServiceClusterResourceName]" -Verbose
```

## <a name="add-a-probe-port"></a>Dodaj port sondy

Zasób klastra SAP, port sondy SAP SID IP, należy skonfigurować przy użyciu programu PowerShell. Wykonanie tej konfiguracji na jednym z węzłów klastra SAP ASCS/SCS, zgodnie z opisem [w tym artykule][sap-high-availability-installation-wsfc-shared-disk-add-probe-port].

## <a name="install-an-ers-instance-on-both-cluster-nodes"></a>Instalowanie wystąpienia Wywołujących w obu węzłów klastra

Zainstaluj wystąpienie serwera replikacji umieścić w kolejce (Wywołujących) na *zarówno* węzłów klastra ASCS/SCS. W SWPM menu tej ścieżki instalacji:

**\<Produktu >** > **\<DBMS >** > **instalacji** > **wystąpień dodatkowe systemu SAP**  >  **Wystąpienie serwera umieścić w kolejce replikacji**

## <a name="install-a-dbms-instance-and-sap-application-servers"></a>Zainstaluj wystąpienie systemu DBMS i serwerów aplikacji SAP

Zakończ instalację systemu SAP, instalując:
* Wystąpienie systemu DBMS.
* Podstawowy serwer aplikacji SAP.
* Dodatkowy serwer aplikacji SAP.

## <a name="next-steps"></a>Następne kroki

* [Instalowanie wystąpienia ASCS/SCS w klastrze trybu failover z dysków — oficjalny SAP wytyczne dotyczące udziału plików o wysokiej dostępności][sap-official-ha-file-share-document]

* [Bezpośrednie miejsca do magazynowania w systemie Windows Server 2016][s2d-in-win-2016]

* [Serwer plików skalowalny w poziomie dla danych aplikacji — omówienie][sofs-overview]

* [Nowości w pamięci masowej w systemie Windows Server 2016][new-in-win-2016-storage]
