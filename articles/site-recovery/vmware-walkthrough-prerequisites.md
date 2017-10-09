---
title: "aaaPrerequisites VMware tooAzure replikacji przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie wymagań wstępnych hello obciążeń uruchomionych na maszynach wirtualnych VMware tooAzure, przy użyciu usługi Azure Site Recovery hello replikacji."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 318156ba-793b-48d0-98d4-cc5436bf28a3
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 14f8e9713b42a1d8da71223fbbb7a6b7c4303adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-vmware-tooazure-replication"></a>Krok 2: Przejrzyj wymagania wstępne hello VMware tooAzure replikacji

Przeczytaj warunki wstępne hello podsumowane w poniższej tabeli hello.

**Wymagania wstępne** | **Szczegóły**
--- | ---
**Azure** | Dowiedz się więcej o [wymagania dotyczące usługi Azure](site-recovery-prereq.md#azure-requirements)
**Lokalny serwer konfiguracji** | Należy maszyny Wirtualnej VMware systemem Windows Server 2012 R2 lub nowszym. Serwer jest skonfigurowany podczas wdrażania usługi Site Recovery.<br/><br/> Przez proces hello domyślnego serwera i główny serwer docelowy są również instalowane na tej maszynie Wirtualnej. Gdy skalowanie w górę, może być konieczne oddzielnego serwera przetwarzania i ma hello te same wymagania co serwer konfiguracji hello.<br/><br/> Dowiedz się więcej o tych składników [tutaj](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**Serwery lokalne, VMware** | Co najmniej jeden VMware vSphere serwery, 6.5, 6.0, 5.5, 5.1 z uruchomionym najnowsze aktualizacje. Serwery powinny znajdować się w hello sam sieci jako hello konfiguracji serwera (lub oddzielnego serwera przetwarzania).<br/><br/> Firma Microsoft zaleca serwera vCenter toomanage hostach z systemem 6.5, 6.0 lub 5.5 z hello najnowsze aktualizacje.
**Lokalne maszyny wirtualne** | Maszyny wirtualne mają powinna być uruchomiona tooreplicate [obsługiwanym systemie operacyjnym](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)i być zgodne z [wymagania wstępne platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). Maszyna wirtualna powinna mieć uruchamiania narzędzi VMware.
**Adresy URL** | Serwer konfiguracji Hello wymagany jest dostęp toothese adresów URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Jeśli masz reguły zapory oparte na adresie IP, sprawdź, czy umożliwiają one tooAzure komunikacji.<br/></br> Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i hello port HTTPS (port 443).<br/></br> Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).<br/><br/> Zezwalaj na ten adres URL do pobrania MySQL hello: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Usługa mobilności** | Zainstalowany na każdym zreplikowanej maszyny Wirtualnej.




## <a name="limitations"></a>Ograniczenia

Upewnij się, że rozumiesz ograniczenia hello podsumowane w tabeli hello przed wdrożeniem.

**Ograniczenia** | **Szczegóły**
--- | ---
**Azure** | Konta magazynu i sieci muszą być w hello tym samym regionie co magazyn hello<br/><br/> Jeśli używasz konta magazynu w warstwie premium, należy również standard przechowywania dzienników replikacji toostore konta<br/><br/> Nie można replikować toopremium kont w środkowej i Południowa, Indie.
**Lokalny serwer konfiguracji** | Typ karty maszyny Wirtualnej VMware powinna być VMXNET3. Jeśli nie, [Zainstaluj tę aktualizację](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> należy zainstalować vSphere PowerCLI 6.0.<br/><br> Witaj maszyny nie powinien być kontrolerem domeny. Maszyna Hello powinien mieć statyczny adres IP.<br/><br/> Nazwa hosta Hello powinna być 15 znaków lub mniej, a system operacyjny będzie w języku angielskim.
**VMware** | Usługa Site Recovery nie obsługuje nowe vCenter i vSphere 6.5 i 6.0 funkcje takie jak cross vCenter vMotion, woluminy i magazynu usługi rejestracji urządzeń.
**Maszyny wirtualne** | Sprawdź [ograniczenia maszyny Wirtualnej Azure](site-recovery-prereq.md#azure-requirements)<br/><br/> Nie można replikować maszyny wirtualne z zaszyfrowanych dysków lub maszyn wirtualnych z rozruchem UEFI/EFI.<br/><br> Udostępniony dysk, który klastrów nie są obsługiwane. Jeśli hello źródłowej maszyny Wirtualnej ma wiele kart, konwersją tooa pojedyncza karta sieciowa po pracy awaryjnej.<br/><br/> Jeśli maszyny wirtualne mają dysku iSCSI, Site Recovery konwertuje go tooa pliku VHD po pracy awaryjnej. Jeśli hello obiektów docelowych iSCSI może być osiągnięta poprzez hello maszyny Wirtualnej platformy Azure, łączy tooit i widzi ona i hello wirtualnego dysku twardego. Jeśli tak się stanie, odłącz hello obiektów docelowych iSCSI.<br/><br/> Jeśli chcesz tooenable spójności wielu maszyn wirtualnych, dzięki czemu maszyny wirtualne z systemami hello odzyskane toobe obciążenia tego samego razem tooa spójności danych punktu, otwórz port 20004 na powitania maszyny Wirtualnej.<br/><br/> Na dysku hello C musi zostać zainstalowany system Windows. dysk systemu operacyjnego Hello powinna być podstawowych i nie dynamicznych. Witaj dysku danych może być dynamiczny.<br/><br/> Plik/etc/hosts systemu Linux na maszynach wirtualnych powinien zawierać wpisów, które mapują hello hosta lokalnego nazwa tooIP skojarzonego z wszystkich kart sieciowych. Witaj, nazwy hosta, punkty instalacji, nazwa urządzenia, ścieżki systemu i nazwy pliku (/ etc; usr) powinny być tylko w języku angielskim.<br/><br/> Określone typy [magazynu Linux](site-recovery-support-matrix-to-azure.md#support-for-storage) są obsługiwane.<br/><br/>Utwórz lub ustawić **disk.enableUUID=true** w hello ustawienia maszyny Wirtualnej. To zapewnia spójne toohello UUID VMDK, instaluje poprawnie i zapewnia, że zmiany różnicowe tylko są przeniesione wstecz lokalnych tooon podczas powrotu po awarii bez pełnej replikacji.


## <a name="next-steps"></a>Następne kroki

- Jeśli pełne wdrożenie robimy, przejdź zbyt[krok 3: Planowanie pojemności](vmware-walkthrough-capacity.md)
- Jeśli podczas wykonywania testu proste wdrożenie, należy przejść za[krok 4: Planowanie sieci](vmware-walkthrough-network.md).
