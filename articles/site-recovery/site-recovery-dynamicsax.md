---
title: "Replikowanie wdrażania Dynamics AX wielowarstwową przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób replikowania i chronić Dynamics AX przy użyciu usługi Azure Site Recovery"
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
ms.openlocfilehash: 03127c8f4841b67436c4819628319705af0b2cd5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>Replikowanie wielowarstwowej aplikacji Dynamics AX przy użyciu usługi Azure Site Recovery

## <a name="overview"></a>Omówienie


Microsoft Dynamics AX jest jednym z najbardziej popularnych rozwiązań ERP między przedsiębiorstwom standardowy proces w lokalizacjach, zarządzanie zasobami i uproszczenia zgodności. Considering aplikacji jest firma krytyczne znaczenie dla organizacji jest bardzo ważne, upewnij się, że jeśli wszelkie po awarii, aplikacja powinna być uruchomiona w minimalny czas.

Już dziś Microsoft Dynamics AX nie zapewnia żadnych funkcji odzyskiwania po awarii poza pole. Microsoft Dynamics AX składa się z wielu składników serwera, takich jak serwera aplikacji, Active Directory (AD), serwer bazy danych SQL, program SharePoint Server Reporting Server itd. Aby zarządzać awarią odzyskiwania każdego z tych składników ręcznie jest nie tylko kosztowna, ale również podatne na błędy.

W tym artykule opisano szczegółowo dotyczące tworzenia rozwiązanie odzyskiwania po awarii dla programu Dynamics AX aplikacji przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md). Obejmuje ona również planowane/nieplanowane/testowanie oprogramowania przełączenia do trybu failover przy użyciu planu odzyskiwania jednym kliknięciem, obsługiwane konfiguracje i wymagania wstępne.
Rozwiązanie odzyskiwania po awarii w usłudze Azure Site Recovery na podstawie jest w pełni przetestowane, certyfikowane i zalecanymi przez program Microsoft Dynamics AX.



## <a name="prerequisites"></a>Wymagania wstępne

Wdrażanie odzyskiwania po awarii dla aplikacji Dynamics AX przy użyciu usługi Azure Site Recovery wymaga następujące wymagania wstępne ukończone.

• Lokalnego wdrożenia programu Dynamics AX został skonfigurowany

• Magazyn usług odzyskiwania azure lokacji został utworzony w subskrypcji Microsoft Azure

• Jeśli Azure to witryny odzyskiwania, uruchom narzędzie oceny gotowości maszyny wirtualnej platformy Azure na maszynach wirtualnych, aby upewnić się, że są one zgodne z maszynami wirtualnymi Azure i usług Azure Site Recovery


## <a name="site-recovery-support"></a>Obsługa odzyskiwania lokacji

Na potrzeby tworzenia w tym artykule, użyto maszyn wirtualnych VMware z 2012R3 Dynamics AX w systemie Windows Server 2012 R2 Enterprise. Ponieważ replikacja z lokacji odzyskiwania jest niezależny od aplikacji, do przechowywania w następujących scenariuszach również powinny zalecenia zawarte w tym miejscu.

### <a name="source-and-target"></a>Źródłowa i docelowa

**Scenariusz** | **Do lokacji dodatkowej** | **Na platformie Azure**
--- | --- | ---
**Funkcja Hyper-V** | Tak | Tak
**VMware** | Tak | Tak
**Serwer fizyczny** | Tak | Tak

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>Włączenie odzyskiwania po awarii programu Dynamics AX aplikacji przy użyciu usługi Azure Site Recovery
### <a name="protect-your-dynamics-ax-application"></a>Ochrona aplikacji Dynamics AX
Każdego składnika programu Dynamics AX musi być chronione, aby włączyć replikację kompletna aplikacja i odzyskiwania. W tej sekcji omówiono:

**1. Ochrona usługi Active Directory**

**2. Ochrona warstwy SQL**

**3. Ochrona aplikacji i warstwy sieci Web**

**4. Konfiguracja sieci**

**5. Plan odzyskiwania**

### <a name="1-setup-ad-and-dns-replication"></a>1. Instalator usługi AD i replikacja DNS

Usługi Active Directory jest wymagany w lokacji odzyskiwania po awarii dla aplikacji Dynamics AX do funkcji. Istnieją dwie opcje zalecane w zależności od złożoności klienta w środowisku lokalnym.

**Opcja 1**

Jeśli klient ma niewielkiej liczby aplikacji i jednego kontrolera domeny dla jego całą lokalnej lokacji i będzie można przechodzenie w tryb failover całej witryny razem, a następnie zaleca się używanie ASR replikacji do replikowania maszyny kontrolera domeny do lokacji dodatkowej (dotyczy zarówno lokacji do lokacji i lokacji na platformę Azure).

**Opcja 2**

Jeśli klient ma dużą liczbę aplikacji i działa w lesie usługi Active Directory i będzie miała kilka aplikacji w czasie, a następnie zalecamy skonfigurowanie dodatkowego kontrolera domeny w lokacji odzyskiwania po awarii (lokacji dodatkowej lub na platformie Azure).

Zapoznaj się z [Przewodnik uzupełniający po na udostępnianie kontrolera domeny w lokacji odzyskiwania po awarii](site-recovery-active-directory.md). Dla pozostałej części tego dokumentu zostanie przyjęto założenie, że kontroler domeny jest dostępny w witrynie odzyskiwania po awarii.

### <a name="2-setup-sql-server-replication"></a>2. Ustawienia replikacji programu SQL Server
Zapoznaj się z Przewodnik uzupełniający po szczegółowe wskazówki techniczne na to zalecana opcja ochrony [warstwy SQL](site-recovery-sql.md).

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3. Włącz ochronę Dynamics AX klienta i serwera AOS maszyny wirtualne
Wykonaj odpowiednie konfigurację usługi Azure Site Recovery na czy maszyny wirtualne są wdrażane na podstawie [funkcji Hyper-V](site-recovery-hyper-v-site-to-azure.md) lub na [VMware](site-recovery-vmware-to-azure.md).

> [!TIP]
> Zalecana częstotliwość spójne awarii do skonfigurowania to 15 minut.
>

Poniżej migawki pokazuje stan ochrony maszyn wirtualnych składnika Dynamics w scenariuszu ochrony "Lokacji oprogramowania VMware do platformy Azure".
![Elementy chronione](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4. Konfigurowanie sieci
Konfigurowanie maszyny Wirtualnej obliczeniowe i ustawień sieciowych

AX klienta i serwera AOS maszyny wirtualne należy skonfigurować ustawienia sieciowe w usłudze Azure Site Recovery, aby sieci maszyn wirtualnych uzyskać dołączona do prawej sieci DR po pracy awaryjnej. Upewnij się, że sieć DR warstw jest routingu do warstwy SQL.

Możesz wybrać maszynę Wirtualną w zreplikowanych elementów, aby skonfigurować ustawienia sieciowe, jak pokazano poniżej migawki.

* Dla serwerów AOS wybrać zestaw dostępności jest prawidłowa.

* Jeśli jest używany statyczny adres IP, należy określić adres IP, który ma maszyny wirtualnej w **docelowy adres IP** pola ![ustawień sieci](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)



### <a name="5-creating-a-recovery-plan"></a>5. Tworzenie planu odzyskiwania

W usłudze Azure Site Recovery można zautomatyzować proces trybu failover można utworzyć planu odzyskiwania. Dodawanie warstwy aplikacji i warstwy sieci web w planie odzyskiwania. Kolejność ich w różnych grupach tak, aby warstwy frontonu zamknięcia przed aplikacji.

1)  Wybierz magazyn Azure Site Recovery w ramach subskrypcji i kliknij Kafelek "Plany odzyskiwania".

2)  Kliknij pozycję "+ plan i określ nazwę odzyskiwania.

3)  Wybierz 'Source' i 'Target'. Element docelowy może być Azure lub dodatkowej lokacji. W przypadku platformy Azure, należy określić model wdrażania

![Tworzenie planu odzyskiwania](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  Wybierz AOS i klienta maszyn wirtualnych do planu odzyskiwania, a następnie kliknij przycisk ✓.
![Tworzenie planu odzyskiwania](./media/site-recovery-dynamics-ax/selectvms.png)


![Plan odzyskiwania](./media/site-recovery-dynamics-ax/recoveryplan.png)

Plan odzyskiwania aplikacji Dynamics AX można dostosować, dodając różnych kroków zgodnie z opisem poniżej. Migawki powyżej przedstawiono planu odzyskiwania ukończone po dodaniu wszystkich kroków.

*Kroki:*

*1. Program SQL Server w tryb failover kroki*

Zapoznaj się ["Rozwiązanie odzyskiwania po awarii programu SQL Server"](site-recovery-sql.md) Przewodnik uzupełniający po szczegółowe informacje na temat określonych czynności odzyskiwania do programu SQL server.

*2. Tryb failover Grupa 1: Tryb failover maszyn wirtualnych serwera AOS*

Upewnij się, że wybrany punkt odzyskiwania jest możliwie najbliżej PIT bazy danych, lecz nie wyprzedzeniem.

*3. Skrypt: Moduł równoważenia obciążenia Dodaj (tylko A E)* Dodaj skryptów (za pośrednictwem usługi Automatyzacja Azure) po grupie maszyny Wirtualnej serwera AOS pojawia się, aby dodać usługi równoważenia obciążenia. Skrypt służy do wykonania tego zadania. Zobacz artykuł [sposób dodawania usługi równoważenia obciążenia dla aplikacji wielowarstwowych DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)

*4. Tryb failover, grupa 2: Awaryjnie klienta AX maszyn wirtualnych.*
Tryb failover warstwa sieci web maszyn wirtualnych w ramach planu odzyskiwania.


### <a name="doing-a-test-failover"></a>Ten test trybu failover

Zobacz "Rozwiązanie odzyskiwania po awarii AD" i "Rozwiązanie odzyskiwania po awarii programu SQL Server" przewodników uzupełniających dotyczących kwestii związanych z określonego celu AD i programu SQL server odpowiednio podczas testowania trybu Failover.

1.  Przejdź do portalu Azure i wybierz z magazynu usługi Site Recovery.
2.  Kliknij utworzony dla Dynamics AX planu odzyskiwania.
3.  Kliknij na "Test trybu Failover".
4.  Wybierz sieć wirtualną, aby rozpocząć proces awaryjnej testu.
5.  Po skonfigurowaniu dodatkowej środowiska można wykonywać z operacji sprawdzania poprawności.
6.  Po zakończeniu operacji sprawdzania poprawności, wybierz opcję "Ukończenie operacji sprawdzania poprawności" i testowe środowisko trybu failover zostaną wyczyszczone.

Postępuj zgodnie z [w tych wskazówkach](site-recovery-test-failover-to-azure.md) przeprowadzić test trybu failover.

### <a name="doing-a-failover"></a>Podczas pracy w trybie failover

1.  Przejdź do portalu Azure i wybierz z magazynu usługi Site Recovery.
2.  Kliknij utworzony dla Dynamics AX planu odzyskiwania.
3.  Kliknij "Failover" i wybierz polecenie "Failover".
4.  Wybierz sieć docelowa, a następnie kliknij przycisk ✓, aby rozpocząć proces trybu failover.

Postępuj zgodnie z [w tych wskazówkach](site-recovery-failover.md) podczas wprowadzania trybu failover.

### <a name="perform-a-failback"></a>Wykonaj powrót po awarii

Zapoznaj się Przewodnik uzupełniający po "Rozwiązanie odzyskiwania po awarii programu SQL Server" Aby uzyskać informacje o określonym do programu SQL server podczas powrotu po awarii.

1.  Przejdź do portalu Azure i wybierz z magazynu usługi Site Recovery.
2.  Kliknij utworzony dla Dynamics AX planu odzyskiwania.
3.  Kliknij "Failover" i wybierz polecenie pracy awaryjnej.
4.  Kliknij "Zmień kierunek".
5.  Wybierz odpowiednie opcje - synchronizacji danych i opcje tworzenia maszyny Wirtualnej
6.  Kliknij przycisk ✓, aby rozpocząć proces "Powrotu po awarii".


Postępuj zgodnie z [w tych wskazówkach](site-recovery-failback-azure-to-vmware.md) podczas wprowadzania powrotu po awarii.

##<a name="summary"></a>Podsumowanie
Za pomocą usługi Azure Site Recovery, można utworzyć plan odzyskiwania ukończenia automatycznego po awarii aplikacji Dynamics AX. Możesz zainicjować trybu failover w ciągu kilku sekund z dowolnego miejsca w przypadku przerwy w pracy i get aplikacji do pracy w minutach.

## <a name="next-steps"></a>Następne kroki
Odczyt [jakie obciążenia mogę chronić?](site-recovery-workload.md) Aby dowiedzieć się więcej o ochronie obciążeń przedsiębiorstwa z usługą Azure Site Recovery.
