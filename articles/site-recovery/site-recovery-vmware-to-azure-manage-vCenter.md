---
title: " Zarządzanie programu VMware vCenter server w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób dodawania i zarządzania nimi w usłudze Azure Site Recovery program VMware vCenter."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 5be995f137d0c0efaf3050b5366a107098cae15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-vmware-vcenter-server-in-azure-site-recovery"></a>Zarządzanie VMware vCenter Server w usłudze Azure Site Recovery
W tym artykule omówiono hello różne operacje odzyskiwania lokacji, które można wykonywać w programie VMware vCenter.

## <a name="prerequisites"></a>Wymagania wstępne

**Obsługa programu VMware vCenter i VMware vSphere hosta ESX** | **Szczegóły** |
|--- | --- |
|**Serwery lokalne, VMware** | Co najmniej jeden VMware vSphere serwery, 6.0, 5.5, 5.1 z uruchomionym najnowsze aktualizacje. Serwery powinny znajdować się w hello sam sieci jako hello konfiguracji serwera (lub oddzielnego serwera przetwarzania).<br/><br/> Firma Microsoft zaleca vCenter hostach toomanage serwera z systemem w wersji 6.0 lub 5.5 z hello najnowsze aktualizacje. Tylko funkcje, które są dostępne w wersji 5.5 są obsługiwane w przypadku wdrożenia w wersji 6.0.|

## <a name="prepare-an-account-for-automatic-discovery"></a>Przygotowanie konta automatycznego wykrywania
Usługa Site Recovery musi tooVMware dostępu hello procesu serwera tooautomatically Odkryj maszyny wirtualne i trybu failover i powrotu po awarii maszyn wirtualnych.

* **Migrowanie**: należy tylko toomigrate tooAzure maszyny wirtualne VMware, niezawodnie kiedykolwiek je ponownie, należy użyć konta VMware z rolą tylko do odczytu. Takie roli można uruchomić trybu failover, ale nie można zamknąć chronionych maszyn źródłowych. Nie jest to konieczne do migracji.
* **Replikacja/odzyskania**: Jeśli chcesz toodeploy pełnej replikacji (replikacja, trybu failover i powrotu po awarii) hello konto musi być możliwe toorun operacji, takich jak tworzenie i usuwanie dysków, włączanie na maszynie wirtualnej.
* **Automatyczne odnajdowanie**: wymagane jest co najmniej konto tylko do odczytu.


|**Zadania** | **Wymagane konto/roli** | **Uprawnienia** | **Szczegóły**|
|--- | --- | --- | ---|
|**Serwer przetwarzania automatycznie odnajduje maszyn wirtualnych VMware** | Należy co najmniej użytkownika tylko do odczytu | Centrum danych obiektu –> tooChild propagowany obiektu roli = tylko do odczytu | Użytkownik przypisane na poziomie centrum danych i istnieją obiekty hello tooall dostępu hello centrum danych.<br/><br/> toorestrict dostępu, przypisz hello **dostępu** roli z hello **propagację toochild** obiektu, toohello obiektów podrzędnych (hostami vSphere, datastores maszyn wirtualnych i sieci).|
|**Tryb failover** | Należy co najmniej użytkownika tylko do odczytu | Centrum danych obiektu –> tooChild propagowany obiektu roli = tylko do odczytu | Użytkownik przypisane na poziomie centrum danych i istnieją obiekty hello tooall dostępu hello centrum danych.<br/><br/> toorestrict dostępu, przypisz hello **dostępu** roli z hello **propagację toochild** obiekt toohello obiektów podrzędnych (hostami vSphere, datastores maszyn wirtualnych i sieci).<br/><br/> Przydatna do celów migracji, ale nie pełnej replikacji, pracy awaryjnej, powrotu po awarii.|
|**Tryb failover i powrotu po awarii** | Zalecamy, aby utworzyć rolę (AzureSiteRecoveryRole) z hello wymagane uprawnienia, a następnie przypisz hello roli tooa VMware użytkownika lub grupy | Centrum danych obiektu –> tooChild propagowany obiektu roli = AzureSiteRecoveryRole<br/><br/> Magazyn danych -> Przydziel przestrzeń na, Przeglądaj magazynu danych, operacje na plikach niskiego poziomu, usuń plik, zaktualizuj pliki maszyny wirtualnej<br/><br/> Sieć -> Przypisywanie sieci<br/><br/> Zasób -> Przypisz wirtualna tooresource puli, migracji Zasilanie wyłączone maszyny Wirtualnej, migracja zasilanego na maszynie Wirtualnej<br/><br/> Zadania -> Utwórz zadanie, zadania aktualizacji<br/><br/> Maszyny wirtualne -> Konfiguracja<br/><br/> Maszyny wirtualne -> interakcja -> odpowiedzi na pytanie, połączenie z urządzeniem, skonfiguruj nośnik CD, skonfiguruj dyskietka, wyłącz zasilanie, włączania zasilania, zainstaluj narzędzia VMware<br/><br/> Maszyny wirtualne -> spisu -> Utwórz, rejestrowanie, wyrejestrowywanie<br/><br/> Maszyny wirtualne -> inicjowania obsługi administracyjnej -> Zezwalaj na pobieranie maszyny wirtualnej, a także zezwalanie przekazać pliki maszyny wirtualnej<br/><br/> Maszyny wirtualne -> migawki -> Usuń migawki | Użytkownik przypisane na poziomie centrum danych i istnieją obiekty hello tooall dostępu hello centrum danych.<br/><br/> toorestrict dostępu, przypisz hello **dostępu** roli z hello **propagację toochild** obiektu, toohello obiektów podrzędnych (hostami vSphere, datastores maszyn wirtualnych i sieci).|

## <a name="create-an-account-tooconnect-toovmware-vcenter-server-vmware-vsphere-exsi-host"></a>Utwórz konto tooconnect tooVMware vCenter Server / VMware vSphere EXSi hosta
1. Zaloguj się do hello konfiguracji serwera, a następnie uruchom hello cspsconfigtool.exe za pomocą skrótu hello dotyczącymi hello pulpitu.
2. Kliknij przycisk **Dodaj konto** na powitania **Zarządzaj kontem** kartę.

  ![Dodaj konto](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Podaj szczegóły konta hello, a następnie kliknij przycisk OK tooadd hello konta. Witaj, konto musi mieć uprawnienia hello na liście hello [przygotować konta do automatycznego odnajdowania](#prepare-an-account-for-automatic-discovery) sekcji.

  >[!NOTE]
  Trwa około 15 minut toobe informacji konta hello zsynchronizowane hello usługi Site Recovery.


## <a name="associate-a-vmware-vcenter-vmware-vsphere-esx-host-add-vcenter"></a>Skojarz VMware vCenter / VMware vSphere ESX host (Dodaj vCenter)
* Na hello portalu Azure, przejdź zbyt*YourRecoveryServicesVault* > **infrastruktura usługi Site Recovery** > **serwery konfiguracji**  >  *ConfigurationServer*
* Na stronie Szczegóły serwera konfiguracji powitania kliknij hello + vCenter przycisku.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

## <a name="modify-credentials-used-tooconnect-toohello-vcenter-server-vsphere-esxi-host"></a>Modyfikowanie serwera vCenter toohello tooconnect poświadczenia używane / hoście ESXi vSphere

1. Zaloguj się do hello konfiguracji serwera, a następnie uruchom hello cspsconfigtool.exe
2. Kliknij przycisk **Dodaj konto** na powitania **Zarządzaj kontem** kartę.

  ![Dodaj konto](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Podaj hello nowych szczegółów konta, a następnie kliknij przycisk OK tooadd hello konta. Witaj, konto musi mieć uprawnienia hello na liście hello [przygotować konta do automatycznego odnajdowania](#prepare-an-account-for-automatic-discovery) sekcji.
4. Na hello portalu Azure, przejdź zbyt*YourRecoveryServicesVault* > **infrastruktura usługi Site Recovery** > **serwery konfiguracji**  >  *ConfigurationServer*
5. Na stronie Szczegóły serwera konfiguracji powitania kliknij hello **odświeżania serwera** przycisku.
6. Po zakończeniu zadania serwer odświeżania hello, wybierz hello vCenter Server tooopen hello vCenter strony podsumowania.
7. Wybierz hello nowo dodane konto hello **vCenter server/vSphere hosta konta** a następnie kliknij przycisk hello **zapisać** przycisku.

  ![modyfikowanie konta](./media/site-recovery-vmware-to-azure-manage-vcenter/modify-vcente-creds.png)

## <a name="delete-a-vcenter-in-azure-site-recovery"></a>Usuń vCenter w usłudze Azure Site Recovery
1. Na hello portalu Azure, przejdź zbyt*YourRecoveryServicesVault* > **infrastruktura usługi Site Recovery** > **serwery konfiguracji**  >  *ConfigurationServer*
2. Na stronie Szczegóły serwera konfiguracji hello wybierz hello vCenter Server tooopen hello vCenter strony podsumowania.
3. Polecenie hello **usunąć** vCenter hello toodelete przycisku

  ![Usuń konto](./media/site-recovery-vmware-to-azure-manage-vcenter/delete-vcenter.png)

> [!NOTE]
Jeśli potrzebujesz toomodify hello Vcenter adres IP/FQDN, Szczegóły portu, a następnie konieczne toodelete hello vCenter Server i dodaj go ponownie ponownie.
