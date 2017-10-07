---
title: "aaaReplicate IIS wielowarstwowych na podstawie aplikacji sieci web przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooreplicate IIS sieci web farmy maszyn wirtualnych za pomocą usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 1974265b3cb05f6dc57049876306d2e08424bb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-iis-based-web-application-using-azure-site-recovery"></a>Replikowanie aplikacji sieci web usług IIS na podstawie wielowarstwową przy użyciu usługi Azure Site Recovery

## <a name="overview"></a>Omówienie


Oprogramowanie to aparat hello wydajności biznesowej w organizacji. Różne aplikacje sieci web może obsługiwać różnych celów w organizacji. Niektóre z nich, takie jak lista płac przetwarzania, aplikacje finansowe i klientów witryn sieci Web może być najwyższym krytyczne dla organizacji. Będzie on potrzebny do hello organizacji toohave je i uruchomiona na zawsze tooprevent zmniejszeniu wydajności pracy i więcej istotne zapobiec żadnego obrazu marki toohello uszkodzenia hello organizacji.

Aplikacje sieci web krytyczne są zwykle tworzone jako aplikacje wielowarstwowe hello sieci web, bazy danych i aplikacji na różnych warstw. Oprócz są rozkładane do różnych warstw, aplikacji hello może również używać wielu serwerów w każdej warstwie tooload równoważenie hello ruchu. Ponadto hello mapowania między warstwami różnych i na serwerze sieci web hello może opierać się na statycznych adresów IP. W tryb failover niektóre z tych mapowania należy toobe zaktualizowane, zwłaszcza, jeśli masz wiele witryn sieci Web, które są skonfigurowane na serwerze sieci web hello. W przypadku aplikacji sieci web przy użyciu protokołu SSL powiązania certyfikatu należy zaktualizować toobe.

Metod tradycyjnych odzyskiwania na podstawie — replikacja obejmują tworzenie kopii zapasowych różnych plików konfiguracji, ustawienia rejestru, powiązania, niestandardowych składników (COM lub .NET), zawartość i również certyfikaty i odzyskiwanie plików hello za pomocą zestawu wymagane ręczne wykonanie czynności. Te techniki są jasno obciążeniem, błąd podatnych na błędy i nie skalowalności. Jest na przykład może łatwo tooforget wykonywanie kopii zapasowej certyfikatów i pozostać z nie wyboru, ale toobuy nowe certyfikaty serwera na powitania po pracy awaryjnej.

Dobre rozwiązanie odzyskiwania po awarii, należy zezwala modelowania planów odzyskiwania wokół hello powyżej architekturach aplikacji złożonych i również mieć hello możliwości tooadd dostosowane kroki toohandle aplikacji mapowań między różnych warstw, dlatego zapewnienie jednym kliknięciem się, że zrzut rozwiązanie w przypadku awarii wiodące tooa hello obniżyć RTO.


W tym artykule opisano, jak tooprotect usług IIS na podstawie aplikacji sieci web przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md). W tym artykule opisano najlepsze rozwiązania dotyczące replikacji trzy warstwy usług IIS na podstawie tooAzure aplikacji sieci web, jak wyszczególniania odzyskiwania po awarii i sposób tooAzure aplikacji hello trybu failover.


## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem upewnij się, że rozumiesz hello poniżej:

1. [Replikowanie tooAzure maszyny wirtualnej](site-recovery-vmware-to-azure.md)
1. Jak zbyt[projektowania sieci odzyskiwania](site-recovery-network-design.md)
1. [Ten test trybu failover tooAzure](./site-recovery-test-failover-to-azure.md)
1. [Sposób tooAzure trybu failover](site-recovery-failover.md)
1. Jak zbyt[replikacji kontrolera domeny](site-recovery-active-directory.md)
1. Jak zbyt[replikacji programu SQL Server](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Wzorce wdrożenia
Aplikacja sieci web usług IIS na podstawie zazwyczaj odpowiada jednemu z powitania po wzorców wdrożenia:

** Wdrożenia wzorzec 1 ** usług IIS na podstawie kolektywu serwerów sieci web z Routing(ARR) żądania aplikacji, serwer usług IIS i Microsoft SQL Server.

![Wzorzec wdrożenia](./media/site-recovery-iis/deployment-pattern1.png)

**Wzorzec wdrożenia 2** usług IIS na podstawie kolektywu serwerów sieci web z Routing(ARR) żądania aplikacji, serwer usług IIS, serwera aplikacji i programu Microsoft SQL Server.


![Wzorzec wdrożenia](./media/site-recovery-iis/deployment-pattern2.png)

## <a name="site-recovery-support"></a>Obsługa odzyskiwania lokacji

Witaj w celu tworzenia maszyn wirtualnych VMware tego artykułu z serwerem usług IIS w wersji 7.5 w systemie Windows Server 2012 R2 Enterprise były używane. Ponieważ replikacja z lokacji odzyskiwania jest niezależny od aplikacji, zalecenia hello podano tutaj toohold oczekiwanego w następujących scenariuszach również i dla różnych wersji programu IIS.

### <a name="source-and-target"></a>Źródłowa i docelowa

**Scenariusz** | **tooa lokacji dodatkowej** | **tooAzure**
--- | --- | ---
**Funkcja Hyper-V** | Tak | Tak
**VMware** | Tak | Tak
**Serwer fizyczny** | Nie | Tak

## <a name="replicate-virtual-machines"></a>Replikowanie maszyn wirtualnych

Postępuj zgodnie z [w tych wskazówkach](site-recovery-vmware-to-azure.md) toostart replikację wszystkich tooAzure maszyn wirtualnych kolektywu serwerów sieci web hello usług IIS.

Jeśli jest używany statyczny adres IP, określ IP hello, interesujące hello tootake maszyny wirtualnej w hello [ **docelowy adres IP** ](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) ustawienie w ustawieniach obliczeń i sieci.

![Adres IP obiektu docelowego](./media/site-recovery-active-directory/dns-target-ip.png)


## <a name="creating-a-recovery-plan"></a>Tworzenie planu odzyskiwania

Plan odzyskiwania umożliwia sekwencjonowania trybu failover hello różnych poziomów w wielowarstwowej aplikacji, w związku z tym zachowaniu spójności aplikacji. Wykonaj hello kroki podczas tworzenia planu odzyskiwania dla aplikacji sieci web w wielowarstwowych.  [Dowiedz się więcej o tworzeniu planu odzyskiwania](./site-recovery-create-recovery-plans.md).

### <a name="adding-virtual-machines-toofailover-groups"></a>Dodawanie grup toofailover maszyny wirtualne
Typowa aplikacja sieci web usług IIS wielowarstwowych będzie składać się z warstwy bazy danych SQL maszyn wirtualnych, warstwa sieci web hello utworzoną przez serwer usług IIS i warstwy aplikacji. Dodaj wszystkie te maszyny wirtualne toodifferent grupy na podstawie warstwy jako poniżej. [Dowiedz się więcej o dostosowanie planu odzyskiwania](site-recovery-runbook-automation.md#customize-the-recovery-plan).

1. Tworzenie planu odzyskiwania. Dodaj maszyny wirtualne warstwy hello bazy danych w obszarze grupy 1 tooensure ostatnio są zamykania i włączane pierwszej.

1. Dodaj maszyny wirtualne warstwy aplikacji hello w obszarze grupy 2 w taki sposób, że są włączane po włączane hello warstwy bazy danych.

1. Dodaj maszyny wirtualne warstwy sieci web hello w grupa 3 taki sposób, że są włączane po włączane hello warstwy aplikacji.

1. Dodaj maszyny wirtualne równoważenia obciążenia w grupie 4 taki sposób, że są włączane po włączane hello warstwa sieci web.


### <a name="adding-scripts-toohello-recovery-plan"></a>Dodawanie skryptów toohello planu odzyskiwania
Może być konieczne toodo niektóre operacje na powitania maszyn wirtualnych platformy Azure post trybu failover i testowanie trybu failover toomake IIS sieci web farmy funkcja poprawnie. Można zautomatyzować tryb failover post hello takich jak aktualizacja wpisu DNS zmiana powiązania witryny, zmiany w parametrach połączenia, dodając odpowiednie skrypty w planie odzyskiwania hello zgodnie z poniższymi instrukcjami. [Dowiedz się więcej na temat dodawania skryptu planu odzyskiwania](./site-recovery-create-recovery-plans.md#add-scripts).

#### <a name="dns-update"></a>Aktualizację DNS
Jeśli hello DNS jest skonfigurowany do dynamicznej aktualizacji DNS, a następnie maszyn wirtualnych zwykle po rozpoczęciu aktualizacji hello DNS z hello nowego adresu IP. Tooadd tooupdate jawne krok DNS z hello nowe adresy IP maszyn wirtualnych hello następnie należy dodać to [skryptu tooupdate IP w systemie DNS](https://aka.ms/asr-dns-update) akcji post na grupach planu odzyskiwania.  

#### <a name="connection-string-in-an-applications-webconfig"></a>Parametry połączenia w pliku web.config aplikacji
Określa parametry połączenia Hello hello bazy danych, który hello witryny sieci web, który komunikuje się z.

Jeśli parametry połączenia hello niesie hello Nazwa maszyny wirtualnej bazy danych hello, żadne dalsze czynności będą potrzebne post trybu failover i aplikacji hello będą mogli tooautomatically komunikacji toohello bazy danych. Ponadto jeśli hello adresu IP dla maszyny wirtualnej hello bazy danych jest zachowywana, nie będzie wymagane parametry połączenia hello tooupdate. Parametry połączenia hello odwołuje się toohello maszyny wirtualnej dla bazy danych przy użyciu adresu IP, należy toobe zaktualizowane post w tryb failover. Na przykład toohello bazy danych z adresem IP 127.0.1.2 punktów Hello poniżej parametrów połączenia

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
        <connectionStrings>
        <add name="ConnStringDb1" connectionString="Data Source= 127.0.1.2\SqlExpress; Initial Catalog=TestDB1;Integrated Security=False;" />
        </connectionStrings>
        </configuration>

Parametry połączenia hello w warstwa sieci web można zaktualizować przez dodanie [skryptu aktualizacji połączenia usług IIS](https://aka.ms/asr-update-webtier-script-classic) po grupa 3 w planie odzyskiwania hello.

#### <a name="site-bindings-for-hello-application"></a>Powiązania witryny w aplikacji hello
Każda witryna składa się z powiązania informacje obejmujące hello typ powiązania, hello adresu IP, na które powitania serwera IIS nasłuchuje żądań toohello hello lokacji, hello numer portu i nazwy hostów hello hello witryny. W czasie hello trybu failover te powiązania może być konieczne toobe aktualizowane, jeśli nie nastąpiła zmiana adresu IP hello skojarzonych z nimi.

> [!NOTE]
>
> Jeśli zostały oznaczone jako "wszystkie nieprzypisane" dla powiązania witryny hello tak jak w poniższym przykładzie hello, nie musisz tooupdate tej pracy awaryjnej post powiązania. Ponadto jeśli hello adresu IP skojarzonego z lokacji nie zostanie zmieniona post trybu failover, powiązania witryny hello muszą: nie można zaktualizować (przechowywania hello adres IP jest zależna od hello architektury sieci i podsieci przypisane toohello lokacji głównej i odzyskiwania lokacji i dlatego mogą lub nie mogą być zastosowane w danej organizacji).

![Powiązanie SSL](./media/site-recovery-iis/sslbinding.png)

Jeśli adres IP hello został skojarzony z lokacją, konieczne będzie tooupdate wszystkie powiązania witryny przy użyciu nowego adresu IP hello. Możesz dodać [skryptu aktualizacji warstwy sieci Web usług IIS](https://aka.ms/asr-web-tier-update-runbook-classic) po grupa 3 w powiązania witryny hello toochange planu odzyskiwania.


#### <a name="update-load-balancer-ip-address"></a>Zaktualizuj adres IP usługi równoważenia obciążenia
Jeśli masz Routing żądań aplikacji maszyny wirtualnej, dodać [skryptu trybu failover IIS ARR](https://aka.ms/asr-iis-arrtier-failover-script-classic) po adres IP hello tooupdate grupy 4.

#### <a name="hello-ssl-cert-binding-for-an-https-connection"></a>Witaj powiązania certyfikatu SSL dla połączenia https
Witryny sieci Web może mieć skojarzone certyfikatu SSL, który pomaga w celu zapewnienia bezpiecznej komunikacji między hello serwer sieci Web i przeglądarką hello użytkownika. Jeśli witryna sieci Web hello połączenia https i adres IP toohello powiązania witryny https skojarzone powitania serwera IIS wraz z powiązaniem certyfikatu SSL, nowego powiązania witryny należy toobe dodane cert hello z hello IP maszyny wirtualnej IIS hello post trybu failover.

certyfikat SSL Hello mogą być wystawiane przed-

) nazwy FQDN hello hello witryny sieci Web<br>
b) nazwa hello powitania serwera<br>
c) certyfikat uniwersalny hello nazwy domeny<br>
d) adres IP — Jeśli certyfikat SSL hello jest wystawiony na podstawie IP hello powitania serwera IIS, innym toobe potrzeb certyfikatu SSL wystawiony na podstawie adresu IP hello powitania serwera usług IIS na powitania usługi Azure site i dodatkowe powiązania SSL dla tego certyfikatu, należy utworzyć toobe. W związku z tym jest toonot zaleca się użycie certyfikatu SSL wystawiony na podstawie adresu IP. To jest opcja mniej powszechnie używane i wkrótce zostaną wycofane zgodnie z harmonogramem nowych zmian forum urzędu certyfikacji/przeglądarki.

#### <a name="update-hello-dependency-between-hello-web-and-hello-application-tier"></a>Aktualizacja hello zależność między hello sieci web i warstwy aplikacji hello
Jeśli masz zależność określonych aplikacji na podstawie adresu IP hello hello maszyn wirtualnych, należy tooupdate tej pracy awaryjnej post zależności.

## <a name="doing-a-test-failover"></a>Ten test trybu failover
Postępuj zgodnie z [w tych wskazówkach](site-recovery-test-failover-to-azure.md) toodo test trybu failover.

1.  Przejdź tooAzure portalu i wybierz magazyn usług odzyskiwania.
1.  Polecenie hello planu odzyskiwania utworzone dla kolektywu serwerów sieci web usług IIS.
1.  Kliknij na "Test trybu Failover".
1.  Wybierz punkt odzyskiwania i procesu sieci wirtualnej platformy Azure toostart hello testowego trybu failover.
1.  Po skonfigurowaniu dodatkowej środowiska hello można wykonywać z operacji sprawdzania poprawności.
1.  Po zakończeniu operacji sprawdzania poprawności hello, wybierz opcję "Ukończenie operacji sprawdzania poprawności" i hello testowe środowisko trybu failover zostaną wyczyszczone.

## <a name="doing-a-failover"></a>Podczas pracy w trybie failover
Postępuj zgodnie z [w tych wskazówkach](site-recovery-failover.md) podczas wprowadzania trybu failover.

1.  Przejdź tooAzure portalu i wybierz magazyn usług odzyskiwania.
1.  Polecenie hello planu odzyskiwania utworzone dla kolektywu serwerów sieci web usług IIS.
1.  Kliknij pozycję "Failover".
1.  Wybierz proces pracy awaryjnej hello toostart punktu odzyskiwania.

## <a name="next-steps"></a>Następne kroki
Użytkownik może dowiedzieć się więcej o [replikacji z innych aplikacji](site-recovery-workload.md) przy użyciu usługi Site Recovery.
