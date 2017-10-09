---
title: "aaaPrepare lokalnych zasobów programu VMware tooAzure replikacji z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Podsumowanie hello czynności, które należy do replikowania obciążeń uruchomionych na maszynach wirtualnych VMware tooAzure magazynu"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 6aba0e89-ad7c-467e-9db2-cfb3bfe4c7d6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 09d81f15f6ee764135a62f5555e458c55fa30048
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-on-premises-vmware-replication-tooazure"></a>Krok 6: Przygotowanie tooAzure replikacji VMware lokalnej

Użyj instrukcji hello w toointeract tego artykułu tooprepare lokalnymi VMware w serwerów z usługą Azure Site Recovery i przygotować maszyn wirtualnych VMWare do instalacji usługi mobilności hello. agent usługi mobilności Hello musi być zainstalowany na wszystkich lokalnych maszyn wirtualnych, które mają tooreplicate tooAzure.

## <a name="prepare-for-automatic-discovery"></a>Przygotowanie do automatycznego wykrywania

Usługa Site Recovery automatycznie odnajduje maszyn wirtualnych na hostach ESXi vSphere (z lub bez serwera vCenter). Automatyczne odnajdowanie usługi Site Recovery potrzeb hostów tooaccess konta i serwerów:

1. toouse dedykowane konto, utworzyć rolę (na poziomie vCenter hello z uprawnieniami hello opisane w poniższej tabeli hello. Nadaj mu nazwę, taką jak **Azure_Site_Recovery**.
2. Następnie utwórz użytkownika hello vSphere hosta/vCenter Server, a następnie przypisz użytkownika toohello roli hello. To konto użytkownika można określić podczas wdrażania usługi Site Recovery.


### <a name="vmware-account-permissions"></a>VMware uprawnień konta

Usługa Site Recovery musi tooVMware dostępu hello procesu serwera tooautomatically odnajdywanie maszyn wirtualnych i trybu failover i powrotu po awarii maszyn wirtualnych.

- **Migrowanie**: należy tylko toomigrate tooAzure maszyn wirtualnych VMware, niezawodnie kiedykolwiek je ponownie, należy użyć konta VMware z rolą tylko do odczytu. Takie roli można uruchomić trybu failover, ale nie można zamknąć chronionych maszyn źródłowych. Nie jest to konieczne do migracji.
- **Replikacja/odzyskania**: Jeśli chcesz toodeploy pełnej replikacji (replikacja, trybu failover i powrotu po awarii) hello konto musi być możliwe toorun operacji, takich jak tworzenie i usuwanie dysków, włączanie na maszynach wirtualnych itd.
- **Automatyczne odnajdowanie**: wymagane jest co najmniej konto tylko do odczytu.


**Zadanie podrzędne** | **Wymagane konto/roli** | **Uprawnienia** | **Szczegóły**
--- | --- | --- | ---
**Serwer przetwarzania automatycznie odnajduje maszyn wirtualnych VMware** | Należy co najmniej użytkownika tylko do odczytu | Centrum danych obiektu –> tooChild propagowany obiektu roli = tylko do odczytu | Użytkownik przypisane na poziomie centrum danych i istnieją obiekty hello tooall dostępu hello centrum danych.<br/><br/> toorestrict dostępu, przypisz hello **dostępu** roli z hello **propagację toochild** obiekt toohello obiektów podrzędnych (hostami vSphere, datastores, maszyn wirtualnych i sieci).
**Tryb failover** | Należy co najmniej użytkownika tylko do odczytu | Centrum danych obiektu –> tooChild propagowany obiektu roli = tylko do odczytu | Użytkownik przypisane na poziomie centrum danych i istnieją obiekty hello tooall dostępu hello centrum danych.<br/><br/> toorestrict dostępu, przypisz hello **dostępu** roli z hello **propagację toochild** obiekt toohello obiektów podrzędnych (hostami vSphere, datastores, maszyn wirtualnych i sieci).<br/><br/> Przydatna do celów migracji, ale nie pełnej replikacji, pracy awaryjnej, powrotu po awarii.
**Tryb failover i powrotu po awarii** | Zalecamy, aby utworzyć rolę (Azure_Site_Recovery) z hello wymagane uprawnienia, a następnie przypisz hello roli tooa VMware użytkownika lub grupy | Centrum danych obiektu –> tooChild propagowany obiektu roli = Azure_Site_Recovery<br/><br/> Magazyn danych -> Przydziel przestrzeń na, Przeglądaj magazynu danych, operacje na plikach niskiego poziomu, usuń plik, zaktualizuj pliki maszyny wirtualnej<br/><br/> Sieć -> Przypisywanie sieci<br/><br/> Zasób -> Przypisz wirtualna tooresource puli, migracji Zasilanie wyłączone maszyny Wirtualnej, migracja zasilanego na maszynie Wirtualnej<br/><br/> Zadania -> Utwórz zadanie, zadania aktualizacji<br/><br/> Maszyny wirtualne -> Konfiguracja<br/><br/> Maszyny wirtualne -> interakcja -> odpowiedzi na pytanie, połączenie z urządzeniem, skonfiguruj nośnik CD, skonfiguruj dyskietka, wyłącz zasilanie, włączania zasilania, zainstaluj narzędzia VMware<br/><br/> Maszyny wirtualne -> spisu -> Utwórz, rejestrowanie, wyrejestrowywanie<br/><br/> Maszyny wirtualne -> inicjowania obsługi administracyjnej -> Zezwalaj na pobieranie maszyny wirtualnej, a także zezwalanie przekazać pliki maszyny wirtualnej<br/><br/> Maszyny wirtualne -> migawki -> Usuń migawki | Użytkownik przypisane na poziomie centrum danych i istnieją obiekty hello tooall dostępu hello centrum danych.<br/><br/> toorestrict dostępu, przypisz hello **dostępu** roli z hello **propagację toochild** obiekt toohello obiektów podrzędnych (hostami vSphere, datastores, maszyn wirtualnych i sieci).


## <a name="prepare-for-push-installation-of-hello-mobility-service"></a>Przygotowanie do instalacji wypychanej usługi mobilności hello

Witaj usługi mobilności musi być zainstalowany na wszystkich maszynach wirtualnych mają tooreplicate. Istnieje wiele sposobów tooinstall hello usługi, w tym instalacji ręcznej instalacji wypychanej z serwera przetwarzania hello odzyskiwania lokacji i instalacji przy użyciu metod, takich jak System Center Configuration Manager.

Jeśli chcesz toouse instalację wypychaną, należy tooprepare konta usługi Site Recovery za pomocą hello tooaccess maszyny Wirtualnej.

- Korzystając z domeny lub lokalnego konta
- W systemie Windows Jeśli nie używasz konta domeny, należy toodisable kontroli dostępu użytkownika zdalnego na komputerze lokalnym hello. toodo, hello rejestrowania w obszarze **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, Dodaj wpis DWORD hello **LocalAccountTokenFilterPolicy**, o wartości 1.
- Wpis rejestru hello tooadd dla systemu Windows z interfejsu wiersza polecenia, wpisz:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
- Dla systemu Linux hello konto powinno być głównym urzędem certyfikacji na serwerze Linux źródłowym hello.



## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[kroku 7: Tworzenie magazynu](vmware-walkthrough-create-vault.md)
