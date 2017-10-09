---
title: "aaaWhat obciążenia można chronić za pomocą usługi Azure Site Recovery?"
description: "Usługa Azure Site Recovery chroni obciążenia i aplikacje poprzez koordynowanie replikacji hello, trybu failover i odzyskiwania lokalnych maszyn wirtualnych i serwerów fizycznych tooAzure lub tooa lokalnej dodatkowej lokacji"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: 4953948f-26c0-4699-8fe7-59d3bfc1d3da
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/08/2017
ms.author: raynew
ms.openlocfilehash: cab2e1ce3c2b7b2c5f899d957219f5c12eb5965c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-workloads-can-you-protect-with-azure-site-recovery"></a>Jakie obciążenia można chronić za pomocą usługi Azure Site Recovery?
W tym artykule opisano obciążeń i aplikacji, które może replikować z hello usługi Azure Site Recovery.

Zamieść wszelkie komentarze lub pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="overview"></a>Omówienie
Organizacje wymagają ciągłość prowadzenia działalności biznesowej i po awarii (BCDR) odzyskiwania strategii tookeep obciążeń oraz danych bezpieczne i dostępne podczas planowanych lub nieplanowanych przestojów i odzyskać tooregular warunków roboczych możliwie jak.

Usługa Site Recovery jest usługą platformy Azure, która wspiera strategię BCDR tooyour. Przy użyciu usługi Site Recovery, można wdrożyć replikacji obsługującej toohello chmury lub tooa lokacji dodatkowej. Czy aplikacje będą systemu Windows lub opartych na systemie Linux, uruchomionych na serwerach fizycznych VMware lub funkcji Hyper-V, można użyć usługi Site Recovery tooorchestrate replikacji, testowanie odzyskiwania po awarii i uruchamiania trybu failover i powrotu po awarii.

Usługa Site Recovery integruje się z aplikacjami firmy Microsoft, w tym SharePoint, Exchange, Dynamics, SQL Server i Active Directory. Firma Microsoft współpracuje również blisko z czołowymi producentami, takimi jak Oracle, SAP, IBM i Red Hat. Rozwiązania replikacji można dostosować do poszczególnych aplikacji.

## <a name="why-use-site-recovery-for-application-replication"></a>Dlaczego warto używać usługi Site Recovery do replikacji aplikacji?
Usługa Site Recovery przyczynia tooapplication poziom ochrony i odzyskiwania w następujący sposób:

* Zapewnia replikację dla dowolnych obciążeń działających na obsługiwanej maszynie, niezależnie od aplikacji.
* Niemal synchroniczna replikacja z celami punktu odzyskiwania wynoszącymi nawet 30 sekund toomeet hello potrzeb najważniejsze aplikacje biznesowe.
* Spójne migawki jednowarstwowych lub wielowarstwowych aplikacji.
* Integracja z funkcją AlwaysOn programu SQL Server i współpraca z innymi technologiami replikacji na poziomie aplikacji, w tym replikacją AD, SQL AlwaysOn, grupami dostępności bazy danych (DAG, Database Availability Group) programu Exchange i Oracle Data Guard.
* Elastyczne plany odzyskiwania, Włącz toorecover całego stosu aplikacji za pomocą jednego kliknięcia, które obejmują tooinclude zewnętrzne skrypty i działania ręczne w planie hello.
* Zaawansowane zarządzanie siecią w usłudze Site Recovery i Azure toosimplify wymagania sieciowe aplikacji, w tym adresy IP tooreserve możliwości hello, skonfiguruj równoważenia obciążenia i integracja z usługi Azure Traffic Manager dla przełączania RTO niski w sieci.
* Bogata biblioteka automatyzacji, która zapewnia gotowe do zastosowania w środowisku produkcyjnym skrypty dopasowane do danych aplikacji, które można pobrać i zintegrować z planami odzyskiwania.

## <a name="workload-summary"></a>Podsumowanie obciążenia
Usługa Site Recovery może replikować dowolną aplikację uruchomioną na obsługiwanej maszynie. Ponadto współpracujemy z toocarry zespoły produktu się dodatkowe testy konkretnych aplikacji.

| **Obciążenie** | **Replikowanie maszyn wirtualnych funkcji Hyper-V tooa dodatkowej lokacji** | **Replikowanie maszyn wirtualnych funkcji Hyper-V tooAzure** | **Replikowanie maszyn wirtualnych VMware tooa dodatkowej lokacji** | **Replikowanie maszyn wirtualnych VMware tooAzure** |
| --- | --- | --- | --- | --- |
| Active Directory, DNS |Tak |Tak |Tak |Tak |
| Aplikacje sieci Web (IIS, SQL) |Tak |Tak |Tak |Tak |
| System Center Operations Manager |Tak |Tak |Tak |Tak |
| Sharepoint |Tak |Tak |Tak |Tak |
| SAP<br/><br/>Replikowanie tooAzure lokacji SAP do klastra z systemem innym niż |Tak (przetestowane przez firmę Microsoft) |Tak (przetestowane przez firmę Microsoft) |Tak (przetestowane przez firmę Microsoft) |Tak (przetestowane przez firmę Microsoft) |
| Exchange (bez grupy DAG) |Tak |Tak |Tak |Tak |
| Pulpit zdalny/VDI |Tak |Tak |Tak |Nie dotyczy |
| Linux (system operacyjny i aplikacje) |Tak (przetestowane przez firmę Microsoft) |Tak (przetestowane przez firmę Microsoft) |Tak (przetestowane przez firmę Microsoft) |Tak (przetestowane przez firmę Microsoft) |
| Dynamics AX |Tak |Tak |Tak |Tak |
| Dynamics CRM |Tak |Wkrótce |Tak |Wkrótce |
| Oracle |Tak (przetestowane przez firmę Microsoft) |Tak (przetestowane przez firmę Microsoft) |Tak (przetestowane przez firmę Microsoft) |Tak (przetestowane przez firmę Microsoft) |
| Serwer plików systemu Windows |Tak |Tak |Tak |Tak |
| Citrix XenApp i XenDesktop |Nie dotyczy |Tak |Nie dotyczy |Tak |

## <a name="replicate-active-directory-and-dns"></a>Replikacja usługi Active Directory i DNS
Infrastruktura usługi Active Directory i DNS są istotne toomost aplikacje przedsiębiorstwa. Podczas odzyskiwania po awarii będzie konieczne tooprotect i odzyskać te składniki infrastruktury przed odzyskaniem obciążeń i aplikacji.

Można użyć usługi Site Recovery toocreate planu odzyskiwania ukończenia automatycznego po awarii dla usługi Active Directory i DNS. Na przykład jeśli chcesz toofail za pośrednictwem programu SharePoint i SAP z tooa głównej lokacji dodatkowej, możesz skonfigurować plan odzyskiwania, który najpierw przełączy usługi Active Directory i następnie dodatkowe odzyskiwania specyficzny dla aplikacji zaplanować toofail za pośrednictwem hello inne aplikacje, które opierają się na aktywny Katalog.

[Dowiedz się więcej](site-recovery-active-directory.md) o ochronie usługi Active Directory i infrastruktury DNS.

## <a name="protect-sql-server"></a>Ochrona programu SQL Server
Program SQL Server stanowi podstawę dla usług danych wielu aplikacji biznesowych w lokalnym centrum danych.  Usługi Site Recovery może być używany razem technologii SQL Server wysokiej dostępności i odzyskiwania po awarii, tooprotect aplikacji wielowarstwowych przedsiębiorstwa, które używają programu SQL Server. Usługa Site Recovery zapewnia:

* Proste i ekonomiczne rozwiązanie do odzyskiwania po awarii dla programu SQL Server. Replikacja wielu wersji i wydania programu SQL Server autonomicznych serwerów i klastrów, tooAzure lub tooa lokacji dodatkowej.  
* Integracja z grup dostępności AlwaysOn programu SQL, toomanage trybu failover i powrotu po awarii z planami odzyskiwania usługi Azure Site Recovery.
* Plany odzyskiwania na trasie dla hello wszystkich warstw w aplikacji, w tym hello baz danych serwera SQL.
* Skalowanie programu SQL Server dla obciążeń szczytowych z usługą Site Recovery poprzez „szybkie przekierowanie” do większych rozmiarów maszyn wirtualnych IaaS na platformie Azure.
* Łatwe testowanie odzyskiwania po awarii programu SQL Server. Możesz uruchomić testowy tryb failover tooanalyze dane i przeprowadzić kontrole zgodności bez wpływu na środowisko produkcyjne.

[Dowiedz się więcej](site-recovery-sql.md) o ochronie programu SQL Server.

## <a name="protect-sharepoint"></a>Ochrona programu SharePoint
Usługa Azure Site Recovery pomaga w ochronie wdrożeń programu SharePoint w następujący sposób:

* Eliminuje konieczność hello i koszty infrastrukturalne skojarzone dla farmy gotowości do odzyskiwania po awarii. Użyj usługi Site Recovery tooreplicate całą farmę (warstwy sieci Web, aplikacji i bazy danych) tooAzure lub tooa dodatkowej lokacji.
* Upraszcza wdrażanie aplikacji i zarządzanie nimi. Lokacja główna toohello wdrożonych aktualizacji są automatycznie replikowane i dlatego są dostępne po trybu failover i odzyskiwania farmy w lokacji dodatkowej. Zmniejsza również hello zarządzanie i obniża koszty związane z utrzymywaniem aktualny stan wstrzymania przy zachowaniu farmy.
* Upraszcza projektowanie i testowanie aplikacji programu SharePoint poprzez tworzenie na żądanie repliki środowiska z kopią przypominającą środowisko produkcyjne, co umożliwia testowanie i debugowanie.
* Upraszcza przejście toohello chmury przy użyciu tooAzure wdrożeń programu SharePoint toomigrate usługi Site Recovery.

[Dowiedz się więcej](site-recovery-sharepoint.md) o ochronie programu SharePoint.

## <a name="protect-dynamics-ax"></a>Ochrona programu Dynamics AX
Usługa Azure Site Recovery pomaga chronić rozwiązanie Dynamics AX ERP w następujący sposób:

* Organizowanie replikacji całego środowiska Dynamics AX (warstw sieci Web i serwera AOS, warstw baz danych, SharePoint) tooAzure, lub tooa lokacji dodatkowej.
* Upraszczanie migracji wdrożeń Dynamics AX, toohello chmury (Azure).
* Upraszczanie projektowania i testowania aplikacji programu Dynamics AX poprzez tworzenie na żądanie kopii środowiska przypominającej środowisko produkcyjne, co umożliwia testowanie i debugowanie.

[Dowiedz się więcej](site-recovery-dynamicsax.md) o ochronie programu Dynamic AX.

## <a name="protect-rds"></a>Ochrona usług pulpitu zdalnego
Usługi pulpitu zdalnego (RDS) umożliwia infrastruktury pulpitów wirtualnych (VDI), pulpity oparte na sesji i aplikacji, dzięki czemu użytkownicy toowork w dowolnym miejscu. Za pomocą usługi Azure Site Recovery można wykonywać następujące czynności:

* Replikowanie zarządzanych lub niezarządzanych pulpitów wirtualnych tooa dodatkowej lokacji i zdalnego aplikacje i sesje tooa lokacji dodatkowej lub platformy Azure.
* Oto co można replikować:

| **RDS** | **Replikowanie maszyn wirtualnych funkcji Hyper-V tooa dodatkowej lokacji** | **Replikowanie maszyn wirtualnych funkcji Hyper-V tooAzure** | **Replikowanie maszyn wirtualnych VMware tooa dodatkowej lokacji** | **Replikowanie maszyn wirtualnych VMware tooAzure** | **Lokacja dodatkowa tooa replikowania serwerów fizycznych** | **Replikowanie tooAzure serwerów fizycznych** |
| --- | --- | --- | --- | --- | --- | --- |
| **Pulpit wirtualny w puli (niezarządzany)** |Tak |Nie |Tak |Nie |Tak |Nie |
| **Pulpit wirtualny w puli (zarządzany i bez dysku UPD)** |Tak |Nie |Tak |Nie |Tak |Nie |
| **Zdalne aplikacje i sesje pulpitu (bez dysku UPD)** |Tak |Tak |Tak |Tak |Tak |Tak |

[Dowiedz się więcej](https://gallery.technet.microsoft.com/Remote-Desktop-DR-Solution-bdf6ddcb) o ochronie usług pulpitu zdalnego.

## <a name="protect-exchange"></a>Ochrona programu Exchange
Usługa Site Recovery pomaga chronić program Exchange w następujący sposób:

* Dla małych wdrożeń programu Exchange, takie jak serwery pojedyncza lub autonomicznej usługi Site Recovery można replikować i tooAzure lub tooa lokacji dodatkowej pracy awaryjnej.
* W przypadku większych wdrożeń usługa Site Recovery integruje się z grupami DAG programu Exchange.
* Grupy DAG programu Exchange są hello zalecane rozwiązanie odzyskiwania po awarii programu Exchange w przedsiębiorstwie.  Plany odzyskiwania usługi Site może zawierać grupy DAG, pracy awaryjnej tooorchestrate DAG między lokacjami.

[Dowiedz się więcej](https://gallery.technet.microsoft.com/Exchange-DR-Solution-using-11a7dcb6) o ochronie programu Exchange.

## <a name="protect-sap"></a>Ochrona systemu SAP
Należy użyć usługi Site Recovery tooprotect wdrożenia SAP, w następujący sposób:

* Włącz ochronę SAP NetWeaver i produkcji NetWeaver aplikacje uruchamiane lokalnie, poprzez replikację tooAzure składników.
* Włącz ochronę SAP NetWeaver i produkcji NetWeaver aplikacje platformy Azure, poprzez replikację tooanother składniki centrum danych Azure.
* Uproszczenie migracja do chmury, za pomocą usługi Site Recovery toomigrate Twojego tooAzure wdrożenia SAP.
* Uprość uaktualnienia, testowanie i tworzenie prototypów projektu SAP, tworząc na żądanie klony środowiska produkcyjnego na potrzeby testowania aplikacji SAP.

[Dowiedz się więcej](site-recovery-sap.md) o ochronie systemu SAP.

## <a name="protect-iis"></a>Ochrona usług IIS
Użyj wdrożenia usług IIS, usługi Site Recovery tooprotect w następujący sposób:

Usługa Azure Site Recovery zapewnia odzyskiwanie po awarii poprzez replikację hello krytycznych składników w środowisku tooa zimnych zdalnej witrynie lub chmury publicznej, takich jak Microsoft Azure. Ponieważ hello maszyny wirtualnej z serwera sieci web hello i hello bazy danych są replikowane toohello odzyskiwania lokacji, nie jest Brak plików konfiguracyjnych toobackup wymaganie lub certyfikaty oddzielnie. Witaj mapowania aplikacji i powiązania w zależności od zmiennych środowiskowych, które zostały zmienione po trybu failover może zostać zaktualizowany za pomocą skryptów zintegrowane planów odzyskiwania po awarii hello. Maszyny wirtualne są włączane w lokacji odzyskiwania hello tylko w przypadku hello trybu failover. Nie tylko, usługi Azure Site Recovery pomaga to również organizować trybu failover tooend zakończenia hello zapewniając Witaj, następujące możliwości:

-   Zamknięcie hello sekwencjonowania i uruchamiania maszyn wirtualnych w hello różnych warstw.
-   Dodawanie skryptów tooallow Aktualizacja zależności aplikacji i powiązania na maszynach wirtualnych powitania po ich rozpoczęło. skrypty Hello może być również używane tooupdate hello DNS serwera toopoint toohello odzyskiwania lokacji.
-   Przydziel IP adresów toovirtual maszyny pre-trybu failover przez mapowanie sieci hello podstawowymi i odzyskiwania, a więc użyć skryptów, które nie są zaktualizowane toobe post w tryb failover.
-   Możliwość pracy awaryjnej dla wielu aplikacji sieci web na serwerach sieci web hello, eliminując hello zakres pomyłek w zdarzeniu hello awarii jednego kliknięcia.
-   Możliwość tootest hello planów odzyskiwania w izolowanym środowisku dla ćwiczenia odzyskiwania po awarii.

[Dowiedz się więcej](https://aka.ms/asr-iis) o ochronie farmy sieci Web usług IIS.

## <a name="protect-citrix-xenapp-and-xendesktop"></a>Ochrona programów Citrix XenApp i XenDesktop
Użyć wdrożeń program Citrix XenApp i XenDesktop, tooprotect usługi Site Recovery w następujący sposób:

* Włączanie ochrony hello wdrożenia program Citrix XenApp i XenDesktop, poprzez replikację różnych wdrożenia warstwy, w tym (serwer AD DNS, SQL Serwer bazy danych serwera, Citrix dostarczania kontrolera sklepu, program XenApp głównego (VDA), serwer licencji na program XenApp Citrix) tooAzure.
* Uproszczenie migracji chmury przy użyciu usługi Site Recovery toomigrate Twojego program Citrix XenApp i XenDesktop tooAzure wdrożenia.
* Ułatw projektowanie i testowanie wdrożenia Citrix XenApp/XenDesktop przez tworzenie na żądanie kopii środowiska przypominającej środowisko produkcyjne, co umożliwia testowanie i debugowanie.
* To rozwiązanie ma zastosowanie tylko w przypadku pulpitów wirtualnych systemu operacyjnego Windows Server, a nie pulpitów wirtualnych klientów, ponieważ pulpity wirtualne klienta nie są jeszcze obsługiwane w przypadku licencjonowania na platformie Azure.
[Dowiedz się więcej](https://azure.microsoft.com/pricing/licensing-faq/) na temat licencjonowania dla komputerów stacjonarnych klienta/serwera na platformie Azure.

[Dowiedz się więcej](site-recovery-citrix-xenapp-and-xendesktop.md) na temat chronienia wdrożeń programów Citrix XenApp i XenDesktop. Alternatywnie można odwoływać się hello [oficjalny dokument z Citrix](https://aka.ms/citrix-xenapp-xendesktop-with-asr) wyszczególnieniem hello takie same.

## <a name="next-steps"></a>Następne kroki
[Sprawdzanie wymagań wstępnych](site-recovery-prereq.md)
