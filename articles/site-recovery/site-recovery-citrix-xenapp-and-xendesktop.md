---
title: "aaaReplicate wdrażania Citrix XenDesktop i program XenApp wielowarstwową przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooprotect Odzyskaj Citrix XenDesktop i program XenApp wdrożenia i przy użyciu usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a>Replikowanie wdrażania program Citrix XenApp i XenDesktop wielowarstwową przy użyciu usługi Azure Site Recovery

## <a name="overview"></a>Omówienie

Citrix XenDesktop to rozwiązanie wirtualizacji pulpitu, polegającego na dostarczaniu pulpitów i aplikacji na żądanie usługi tooany użytkownik dowolnego miejsca. Dzięki technologii dostarczania FlexCast XenDesktop szybko i bezpiecznie zapewnia aplikacji i toousers komputerów stacjonarnych.
Obecnie program Citrix XenApp nie zapewnia żadnych po awarii możliwości odzyskiwania.

Dobre rozwiązanie odzyskiwania po awarii, należy zezwala modelowania planów odzyskiwania wokół hello powyżej architekturach aplikacji złożonych i również mieć hello możliwości tooadd dostosowane kroki toohandle aplikacji mapowań między różnych warstw, dlatego zapewnienie jednym kliknięciem się, że zrzut rozwiązanie w przypadku awarii wiodące tooa hello obniżyć RTO.

Ten dokument zawiera wskazówki krok po kroku budowania rozwiązanie odzyskiwania po awarii dla lokalnej program Citrix XenApp wdrożeniach funkcji Hyper-V i oprogramowania VMware vSphere platform. Ten dokument zawiera również opis sposobu tooperform test trybu failover (wyszczególniania odzyskiwania po awarii) i tooAzure nieplanowanego trybu failover przy użyciu planów odzyskiwania, hello obsługiwane konfiguracje i wymagania wstępne.


## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem upewnij się, że rozumiesz hello poniżej:

1. [Replikowanie tooAzure maszyny wirtualnej](site-recovery-vmware-to-azure.md)
1. Jak zbyt[projektowania sieci odzyskiwania](site-recovery-network-design.md)
1. [Ten test trybu failover tooAzure](site-recovery-test-failover-to-azure.md)
1. [Sposób tooAzure trybu failover](site-recovery-failover.md)
1. Jak zbyt[replikacji kontrolera domeny](site-recovery-active-directory.md)
1. Jak zbyt[replikacji programu SQL Server](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Wzorce wdrożenia

Farma program Citrix XenApp i XenDesktop ma zazwyczaj hello następującego wzorca wdrażania:

**Wzorzec wdrożenia**

Program Citrix XenApp i XenDesktop wdrożenia z serwerem AD, DNS, SQL bazy danych serwera, Citrix dostarczania kontrolera sklepu server, program XenApp głównego (VDA), serwer licencji na program XenApp Citrix

![Wzorzec wdrożenia 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a>Obsługa odzyskiwania lokacji

W celu hello w tym artykule Citrix wdrożeń na maszynach wirtualnych VMware zarządza vSphere w wersji 6.0 / System Center VMM 2012 R2 były używane toosetup odzyskiwania po awarii.

### <a name="source-and-target"></a>Źródłowa i docelowa

**Scenariusz** | **tooa lokacji dodatkowej** | **tooAzure**
--- | --- | ---
**Funkcja Hyper-V** | Nie znajduje się w zakresie | Tak
**VMware** | Nie znajduje się w zakresie | Tak
**Serwer fizyczny** | Nie znajduje się w zakresie | Tak

### <a name="versions"></a>Wersje
Klienci mogą wdrożyć program XenApp składniki jako maszynami wirtualnymi funkcji Hyper-V lub programu VMware lub serwerach fizycznych. Usługa Azure Site Recovery może chronić tooAzure obu wdrożeń fizycznych i wirtualnych.
Ponieważ program XenApp 7,7 lub nowszej jest obsługiwana na platformie Azure, można nie tylko wdrożenia z tych wersji za pośrednictwem tooAzure dla odzyskiwania po awarii lub migracji.

### <a name="things-tookeep-in-mind"></a>Tookeep rzeczy pamiętać

1. Ochrona i odzyskiwanie z lokalnego wdrożenia przy użyciu serwerowy system operacyjny maszyny toodeliver program XenApp opublikowane aplikacje i program XenApp publikowane komputerów stacjonarnych jest obsługiwana.

2. Ochrona i odzyskiwanie wdrożenia lokalnego przy użyciu pulpitu systemu operacyjnego maszyny toodeliver Pulpitów dla pulpitów wirtualnych klienta, w tym Windows 10 nie jest obsługiwana. Jest tak, ponieważ funkcja automatycznego odzyskiwania systemu nie obsługuje odzyskiwania hello maszyn z pulpitem OS'es.  Ponadto niektóre klienta pulpitu wirtualnego smaki (np.) Windows 7) nie są jeszcze obsługiwane w przypadku licencjonowania na platformie Azure. [Dowiedz się więcej](https://azure.microsoft.com/pricing/licensing-faq/) na temat licencjonowania dla komputerów stacjonarnych klienta/serwera na platformie Azure.

3.  Usługa Azure Site Recovery nie może replikować i ochronę istniejących klony MCS lub Odwiedziny lokalnymi.
Należy toorecreate tych fragmentach operacje przy użyciu Menedżera zasobów Azure inicjowania obsługi administracyjnej z kontrolera dostarczania.

4. NetScaler nie mogą być chronione przy użyciu usługi Azure Site Recovery NetScaler jest oparta na FreeBSD i usługi Azure Site Recovery nie obsługuje ochrony FreeBSD systemu operacyjnego. Będzie konieczne toodeploy i skonfiguruj nowe urządzenie NetScaler z rynku Azure po tooAzure pracy awaryjnej.


## <a name="replicating-virtual-machines"></a>Replikowanie maszyn wirtualnych

następujące składniki hello wdrożenia program Citrix XenApp Hello muszą toobe chronione tooenable replikacji i odzyskiwania.

* Ochrona serwera AD DNS
* Ochrona serwera bazy danych SQL
* Ochrona kontrolera dostarczania Citrix
* Ochrona serwera sklepu.
* Ochrona program XenApp wzorca (VDA)
* Ochrona program Citrix XenApp serwera licencji


**Replikacja serwer AD DNS**

Zobacz zbyt[ochrony usługi Active Directory i DNS z usługą Azure Site Recovery](site-recovery-active-directory.md) na wskazówki dotyczące replikacji i konfigurowania kontrolera domeny na platformie Azure.

**Replikacja serwer bazy danych SQL**

Zobacz zbyt[ochrony programu SQL Server z odzyskiwania po awarii programu SQL Server i usługi Azure Site Recovery](site-recovery-sql.md) techniczne wskazówki dotyczące hello zalecane opcje ochrony serwerów SQL.

Postępuj zgodnie z [w tych wskazówkach](site-recovery-vmware-to-azure.md) replikowanie toostart hello tooAzure maszyn wirtualnych innych składników.

![Ochrona program XenApp składników](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

**Ustawienia sieci i obliczeń**

Po hello maszyn objętych ochroną (pokazuje stan jako "Protected" w obszarze elementy replikowane), hello obliczeń i toobe skonfigurowane wymagane ustawienia sieciowe.
W obliczenia i sieć > obliczeniowe właściwości, można określić rozmiaru maszyny Wirtualnej Azure hello nazwę i obiekt docelowy.
Zmodyfikować hello toocomply nazwy z wymagania dotyczące usługi Azure, jeśli potrzebujesz. Można również wyświetlić i dodać informacje dotyczące sieci docelowej hello, podsieci i adres IP, który zostanie przypisany toohello maszyny Wirtualnej platformy Azure.

Należy uwzględnić następujące hello:

* Można ustawić hello docelowy adres IP. Jeśli nie podasz adresu, hello maszyny przełączonej będzie używać protokołu DHCP. Jeśli ustawisz adres, który nie jest dostępna w trybie failover hello trybu failover nie będzie działać. Witaj, sam docelowy adres IP może być używane do testowania trybu failover, jeśli adres hello jest dostępny w testowej sieci trybu failover hello.

* Dla serwera AD DNS hello zachowując hello lokalnymi pozwala adres określić hello sama adresu jako powitania serwera DNS dla sieci wirtualnej Azure hello.

Hello liczbę kart sieciowych jest zależna hello rozmiar dla hello docelowej maszyny wirtualnej, w następujący sposób:

*   Jeśli hello liczbę kart sieciowych na maszynie źródłowej hello jest mniejsza lub równa toohello liczba kart dozwoloną dla rozmiaru maszyny docelowej hello, a następnie hello docelowa będzie mieć hello samą liczbę kart sieciowych jako źródło hello.
*   Jeśli hello liczbę kart sieciowych dla źródłowej maszyny wirtualnej hello przekracza liczbę hello dozwoloną dla hello rozmiar docelowy, a następnie maksymalny rozmiar docelowy hello będą używane.
* Na przykład jeśli maszyna źródłowa ma dwie karty sieciowe, a rozmiar maszyny docelowej hello obsługuje cztery, maszyna docelowa hello będzie mieć dwie karty sieciowe. Jeśli hello maszyna źródłowa ma dwie karty sieciowe, ale hello rozmiar docelowy obsługiwanych obsługuje tylko jedną maszyna docelowa hello będzie mieć tylko jedną kartę.
*   Jeśli maszyna wirtualna hello ma wiele kart sieciowych, wszystkie będą łączyć toohello tej samej sieci.
*   Jeśli maszyna wirtualna hello ma wiele kart sieciowych, hello pierwszego wyświetlane na liście hello staje się hello domyślnej karty sieciowej hello maszyny wirtualnej platformy Azure.


## <a name="creating-a-recovery-plan"></a>Tworzenie planu odzyskiwania

Po włączeniu replikacji dla hello maszyn wirtualnych składnika program XenApp hello następnym krokiem jest toocreate planu odzyskiwania.
Odzyskiwanie Planowanie grup razem maszyny wirtualne mają podobne wymagania dotyczące trybu failover i odzyskiwania.  

**Kroki toocreate planu odzyskiwania**

1. Dodaj maszyny wirtualne składnika program XenApp hello w hello planu odzyskiwania.
2. Kliknij przycisk planów odzyskiwania -> + planu odzyskiwania. Podaj nazwę intuicyjne hello planu odzyskiwania.
3. W przypadku maszyn wirtualnych VMware: Wybierz źródło jako serwer przetwarzania VMware, element docelowy jako Microsoft Azure i modelu wdrażania usługi Resource Manager i wybierz elementy, kliknij polecenie.
4. W przypadku maszyn wirtualnych funkcji Hyper-V: Wybierz źródło jako serwer programu VMM, docelowy jako Microsoft Azure i modelu wdrażania jak Menedżer zasobów i kliknij pozycję Wybierz elementy, a następnie wybierz hello program XenApp wdrażania maszyn wirtualnych.

### <a name="adding-virtual-machines-toofailover-groups"></a>Dodawanie grup toofailover maszyny wirtualne

Plany odzyskiwania może być dostosowane tooadd trybu failover grupy działań zamówienia, skrypty lub ręcznego uruchamiania określonego. Witaj następujące grupy muszą planu odzyskiwania dodano toohello toobe.

1. Grupa1 trybu failover: DNS AD
2. Grupa2 trybu failover: Maszyny wirtualne SQL Server
2. Trybu failover, grupa 3: Maszyna wirtualna obrazu wzorca VDA
3. Grupa 4 trybu failover: Kontroler dostarczania i maszyn wirtualnych serwera sklepu


### <a name="adding-scripts-toohello-recovery-plan"></a>Dodawanie skryptów toohello planu odzyskiwania

Można uruchamiać skrypty przed lub po określonej grupy w planie odzyskiwania. Ręczne akcje mogą być również być uwzględnione i wykonywane w trybie failover.

plan odzyskiwania dostosowane Hello wygląda hello poniżej:

1. Grupa1 trybu failover: DNS AD
2. Grupa2 trybu failover: Maszyny wirtualne SQL Server
3. Trybu failover, grupa 3: Maszyna wirtualna obrazu wzorca VDA

   >[!NOTE]     
   >Kroki 4, 6 i 7 zawierający akcje ręczne lub skryptu są stosowane tooonly program XenApp lokalnymi > środowisko z katalogami MCS/Odwiedziny.

4. Akcja ręczna lub skryptu grupa 3: zamknięcie wzorca hello VDA maszyny Wirtualnej VM VDA wzorca podczas przejścia w tryb failover tooAzure będzie w stanie uruchomienia. toocreate nowego serwera MCS katalogów przy użyciu hostingu Azure ARM, wzorzec hello VDA maszyny Wirtualnej jest wymagana toobe w zatrzymane (de przydzielone) stanu. Witaj zamykania maszyny Wirtualnej z portalu Azure.

5. Grupa 4 trybu failover: Kontroler dostarczania i maszyn wirtualnych serwera sklepu
6. Grupa 3 ręczny lub skryptu akcji 1:

    ***Dodaj połączenie hostów protokołu RM Azure***

    Utwórz połączenia hosta Azure ARM tooprovision maszyny kontrolera dostarczania nowych katalogów serwera MCS na platformie Azure. Wykonaj kroki hello, zgodnie z objaśnieniem w tym [artykułu](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).

7. Grupa 3 ręczny lub skryptu akcji 2:

    ***Utwórz ponownie MCS katalogi na platformie Azure***

    Hello istniejącego serwera MCS lub Odwiedziny klony w lokacji głównej hello nie będą replikowane tooAzure. Należy toorecreate tych fragmentach operacje przy użyciu hello replikowane VDA wzorca i Azure ARM inicjowania obsługi administracyjnej z kontrolera dostarczania. Wykonaj kroki hello, zgodnie z objaśnieniem w tym [artykułu](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS kataloguje na platformie Azure.

![Plan odzyskiwania program XenApp składników](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   >Możesz używać skryptów w [lokalizacji](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS z hello nowe adresy IP z hello przejścia w tryb failover > maszyn wirtualnych lub tooattach modułu równoważenia obciążenia na powitania przejścia w tryb failover maszyny wirtualnej, jeśli to konieczne.


## <a name="doing-a-test-failover"></a>Ten test trybu failover

Postępuj zgodnie z [w tych wskazówkach](site-recovery-test-failover-to-azure.md) toodo test trybu failover.

![Plan odzyskiwania](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a>Podczas pracy w trybie failover

Postępuj zgodnie z [w tych wskazówkach](site-recovery-failover.md) podczas wprowadzania trybu failover.

## <a name="next-steps"></a>Następne kroki

Możesz [więcej](https://aka.ms/citrix-xenapp-xendesktop-with-asr) o replikowanie wdrożenia program Citrix XenApp i XenDesktop w oficjalnym dokumencie. Obejrzyj wskazówki hello zbyt[replikacji z innych aplikacji](site-recovery-workload.md) przy użyciu usługi Site Recovery.
