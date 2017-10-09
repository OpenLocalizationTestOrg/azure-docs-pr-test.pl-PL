---
title: "aaaReplicate wdrażania Dynamics AX wielowarstwową przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooreplicate i chronić Dynamics AX przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>Replikowanie wielowarstwowej aplikacji Dynamics AX przy użyciu usługi Azure Site Recovery

## <a name="overview"></a>Omówienie


Microsoft Dynamics AX jest jednym z hello najpopularniejszych rozwiązań ERP między procesu toostandardized przedsiębiorstwa w lokalizacjach, zarządzanie zasobami i uproszczenia zgodności. Considering aplikacja hello jest biznesowe krytyczne tooan organizacji jest bardzo ważne toobe się, że jeśli wszelkie po awarii, aplikacja powinna być uruchomiona w minimalny czas.

Już dziś Microsoft Dynamics AX nie zapewnia żadnych funkcji odzyskiwania po awarii poza pole. Microsoft Dynamics AX składa się z wielu składników serwera, takich jak serwer bazy danych SQL serwera aplikacji, Active Directory (AD), serwer programu SharePoint, odzyskiwania po awarii itp serwera raportowania toomanage hello każdego z tych składników ręcznie jest nie tylko kosztowna, ale również podatne na błędy.

W tym artykule opisano szczegółowo dotyczące tworzenia rozwiązanie odzyskiwania po awarii dla programu Dynamics AX aplikacji przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md). Obejmuje ona również planowane/nieplanowane/testowanie oprogramowania przełączenia do trybu failover przy użyciu planu odzyskiwania jednym kliknięciem, obsługiwane konfiguracje i wymagania wstępne.
Rozwiązanie odzyskiwania po awarii w usłudze Azure Site Recovery na podstawie jest w pełni przetestowane, certyfikowane i zalecanymi przez program Microsoft Dynamics AX.



## <a name="prerequisites"></a>Wymagania wstępne

Wdrażanie odzyskiwania po awarii dla aplikacji Dynamics AX przy użyciu usługi Azure Site Recovery wymaga hello następujące wymagania wstępne ukończone.

• Lokalnego wdrożenia programu Dynamics AX został skonfigurowany

• Magazyn usług odzyskiwania azure lokacji został utworzony w subskrypcji Microsoft Azure

• Jeśli Azure to witryny odzyskiwania, uruchom narzędzie oceny gotowości maszyny wirtualnej Azure hello na tooensure maszyn wirtualnych zgodnych z maszynami wirtualnymi Azure i usług Azure Site Recovery


## <a name="site-recovery-support"></a>Obsługa odzyskiwania lokacji

Witaj w celu tworzenia w tym artykule użyto maszyn wirtualnych VMware z 2012R3 Dynamics AX w systemie Windows Server 2012 R2 Enterprise. Ponieważ replikacja z lokacji odzyskiwania jest niezależny od aplikacji, zalecenia hello podano tutaj toohold oczekiwanego w następujących scenariuszach również.

### <a name="source-and-target"></a>Źródłowa i docelowa

**Scenariusz** | **tooa lokacji dodatkowej** | **tooAzure**
--- | --- | ---
**Funkcja Hyper-V** | Tak | Tak
**VMware** | Tak | Tak
**Serwer fizyczny** | Tak | Tak

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>Włączenie odzyskiwania po awarii programu Dynamics AX aplikacji przy użyciu usługi Azure Site Recovery
### <a name="protect-your-dynamics-ax-application"></a>Ochrona aplikacji Dynamics AX
Każdy składnik hello Dynamics AX potrzeb toobe chronione replikacji kompletna aplikacja hello tooenable i odzyskiwania. W tej sekcji omówiono:

**1. Ochrona usługi Active Directory**

**2. Ochrona warstwy SQL**

**3. Ochrona aplikacji i warstwy sieci Web**

**4. Konfiguracja sieci**

**5. Plan odzyskiwania**

### <a name="1-setup-ad-and-dns-replication"></a>1. Instalator usługi AD i replikacja DNS

Usługi Active Directory jest wymagany w lokacji odzyskiwania po awarii hello toofunction aplikacji Dynamics AX. Istnieją dwie opcje zalecane w zależności od złożoności hello powitania klienta w środowisku lokalnym.

**Opcja 1**

Jeśli powitania klienta ma małej liczby aplikacji i jednego kontrolera domeny dla całej jego lokalnej lokacji i będzie można przechodzenie w tryb failover hello całej witryny razem, a następnie firma Microsoft zaleca używanie replikacji ASR tooreplicate hello DC maszyny toosecondary lokacji ( dotyczy zarówno tooSite lokacji i lokacji tooAzure).

**Opcja 2**

Jeśli powitania klienta ma dużą liczbę aplikacji i działa w lesie usługi Active Directory i będzie miała kilka aplikacji w czasie, a następnie zalecamy skonfigurowanie dodatkowego kontrolera domeny w lokacji hello DR (lokacji dodatkowej lub na platformie Azure).

Zobacz zbyt[Przewodnik uzupełniający po na udostępnianie kontrolera domeny w lokacji odzyskiwania po awarii](site-recovery-active-directory.md). Dla pozostałej części tego dokumentu zostanie przyjęto założenie, że kontroler domeny jest dostępny w witrynie odzyskiwania po awarii.

### <a name="2-setup-sql-server-replication"></a>2. Ustawienia replikacji programu SQL Server
Można znaleźć w przewodniku toocompanion techniczne wskazówki dotyczące hello zalecana opcja ochrony [warstwy SQL](site-recovery-sql.md).

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3. Włącz ochronę Dynamics AX klienta i serwera AOS maszyny wirtualne
Wykonaj odpowiednie konfigurację usługi Azure Site Recovery na czy hello maszyny wirtualne są wdrażane na podstawie [funkcji Hyper-V](site-recovery-hyper-v-site-to-azure.md) lub na [VMware](site-recovery-vmware-to-azure.md).

> [!TIP]
> Zalecane tooconfigure spójne częstotliwość awarii wynosi 15 minut.
>

Hello poniżej migawki Wyświetla stan ochrony hello maszyn wirtualnych składnika Dynamics w scenariuszu ochrony "VMware lokacji tooAzure".
![Elementy chronione](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4. Konfigurowanie sieci
Konfigurowanie maszyny Wirtualnej obliczeniowe i ustawień sieciowych

Hello AX klienta i serwera AOS maszyn wirtualnych konfigurowania ustawień sieciowych w usłudze Azure Site Recovery, tak aby hello sieci maszyn wirtualnych pobierać dołączonych toohello prawo odzyskiwania po awarii sieci po pracy awaryjnej. Upewnij się, że sieć DR hello warstw jest warstwy SQL toohello routingu.

Możesz wybrać hello maszyny Wirtualnej w hello replikowane ustawienia sieciowe hello tooconfigure elementów, jak pokazano w migawce hello poniżej.

* Dla serwerów AOS wybierz hello zestawu dostępności jest prawidłowa.

* Jeśli jest używany statyczny adres IP, określ IP hello, interesujące hello tootake maszyny wirtualnej w hello **docelowy adres IP** pola ![ustawień sieci](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)



### <a name="5-creating-a-recovery-plan"></a>5. Tworzenie planu odzyskiwania

Plan odzyskiwania można utworzyć procesu pracy awaryjnej hello tooautomate usługi Azure Site Recovery. Dodawanie warstwy aplikacji i warstwa sieci web w programie hello planu odzyskiwania. Kolejność ich w różnych grupach, które hello frontonu zamknięcia przed warstwy aplikacji.

1)  Wybierz magazyn Azure Site Recovery hello w ramach subskrypcji i kliknij Kafelek "Plany odzyskiwania".

2)  Kliknij pozycję "+ plan i określ nazwę odzyskiwania.

3)  Wybierz hello 'Source' i 'Target'. Witaj docelowym może być Azure lub dodatkowej lokacji. W przypadku platformy Azure, należy określić hello modelu wdrażania

![Tworzenie planu odzyskiwania](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  Wybierz hello AOS i planu odzyskiwania toohello maszyny wirtualne klienta, a następnie kliknij przycisk ✓.
![Tworzenie planu odzyskiwania](./media/site-recovery-dynamics-ax/selectvms.png)


![Plan odzyskiwania](./media/site-recovery-dynamics-ax/recoveryplan.png)

Plan odzyskiwania hello aplikacji Dynamics AX można dostosować, dodając różnych kroków zgodnie z opisem poniżej. Witaj powyżej migawki pokazuje hello planu odzyskiwania ukończone po dodaniu wszystkich kroków hello.

*Kroki:*

*1. Program SQL Server w tryb failover kroki*

Odwołuje się zbyt["Rozwiązanie odzyskiwania po awarii programu SQL Server"](site-recovery-sql.md) Przewodnik uzupełniający po szczegółowe informacje o serwerze tooSQL określone kroki odzyskiwania.

*2. Tryb failover Grupa 1: Tryb failover maszyn wirtualnych serwera AOS hello*

Upewnij się, że wybrany punkt odzyskiwania hello jest blisko bazy danych można toohello PIT, ale nie wyprzedzeniem.

*3. Skrypt: Moduł równoważenia obciążenia Dodaj (tylko A E)* dodać skrypt (za pośrednictwem usługi Automatyzacja Azure) po grupie AOS wirtualna funkcjonuje tooadd tooit usługi równoważenia obciążenia. Tego zadania można używać toodo skryptu. Zobacz artykuł [jak tooadd Usługa równoważenia obciążenia dla aplikacji wielowarstwowych DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)

*4. Tryb failover, grupa 2: Awaryjnie powitania klienta AX maszyn wirtualnych.*
Warstwa sieci web hello maszyn wirtualnych w ramach planu odzyskiwania hello pracy awaryjnej.


### <a name="doing-a-test-failover"></a>Ten test trybu failover

Zobacz too'AD rozwiązanie odzyskiwania po awarii "i"Rozwiązanie odzyskiwania po awarii programu SQL Server"przewodników uzupełniających dotyczących tooAD szczególne zagadnienia i SQL server odpowiednio podczas testowania trybu Failover.

1.  Przejdź tooAzure portalu i wybierz z magazynu usługi Site Recovery.
2.  Polecenie hello planu odzyskiwania utworzone dla Dynamics AX.
3.  Kliknij na "Test trybu Failover".
4.  Wybierz proces awaryjnej testowego hello toostart hello sieci wirtualnej.
5.  Po skonfigurowaniu dodatkowej środowiska hello można wykonywać z operacji sprawdzania poprawności.
6.  Po zakończeniu operacji sprawdzania poprawności hello, wybierz opcję "Ukończenie operacji sprawdzania poprawności" i hello testowe środowisko trybu failover zostaną wyczyszczone.

Postępuj zgodnie z [w tych wskazówkach](site-recovery-test-failover-to-azure.md) toodo test trybu failover.

### <a name="doing-a-failover"></a>Podczas pracy w trybie failover

1.  Przejdź tooAzure portalu i wybierz z magazynu usługi Site Recovery.
2.  Polecenie hello planu odzyskiwania utworzone dla Dynamics AX.
3.  Kliknij "Failover" i wybierz polecenie "Failover".
4.  Wybierz sieć docelowa hello, a następnie kliknij przycisk ✓ toostart hello trybu failover procesu.

Postępuj zgodnie z [w tych wskazówkach](site-recovery-failover.md) podczas wprowadzania trybu failover.

### <a name="perform-a-failback"></a>Wykonaj powrót po awarii

Zobacz too'SQL rozwiązanie odzyskiwania po awarii serwera "Przewodnik uzupełniający po zagadnienia dotyczące określonych tooSQL serwera podczas powrotu po awarii.

1.  Przejdź tooAzure portalu i wybierz z magazynu usługi Site Recovery.
2.  Polecenie hello planu odzyskiwania utworzone dla Dynamics AX.
3.  Kliknij "Failover" i wybierz polecenie pracy awaryjnej.
4.  Kliknij "Zmień kierunek".
5.  Wybierz odpowiednie opcje hello - synchronizacji danych i opcje tworzenia maszyny Wirtualnej
6.  Kliknij przycisk ✓ toostart hello "Powrotu po awarii" proces.


Postępuj zgodnie z [w tych wskazówkach](site-recovery-failback-azure-to-vmware.md) podczas wprowadzania powrotu po awarii.

##<a name="summary"></a>Podsumowanie
Za pomocą usługi Azure Site Recovery, można utworzyć plan odzyskiwania ukończenia automatycznego po awarii aplikacji Dynamics AX. Możesz zainicjować hello trybu failover w ciągu kilku sekund z dowolnego miejsca w hello zdarzeń zakłócenia i pobrać aplikacji hello do pracy w minutach.

## <a name="next-steps"></a>Następne kroki
Odczyt [jakie obciążenia mogę chronić?](site-recovery-workload.md) toolearn więcej o ochronie obciążeń przedsiębiorstwa z usługą Azure Site Recovery.
