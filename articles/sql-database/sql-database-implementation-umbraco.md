---
title: aaaAzure bazy danych SQL Azure zastosowania - Umbraco | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o jak Umbraco używa zastrzegania tooquickly bazy danych SQL i skali usługi tysięcy dzierżawcy w chmurze hello"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5243d31e-3241-4cb0-9470-ad488ff28572
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 93e39e509831a5ff90f129d9537ece0b0dafef0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="umbraco-uses-azure-sql-database-tooquickly-provision-and-scale-services-for-thousands-of-tenants-in-hello-cloud"></a>Program Umbraco używa zastrzegania tooquickly bazy danych SQL Azure i skali usługi tysięcy dzierżawcy w chmurze hello
![Umbraco Logo](./media/sql-database-implementation-umbraco/umbracologo.png)

Program Umbraco jest popularnych open source zawartości — system zarządzania (CMS) można uruchamiać żadnych z małych kampanii lub broszura lokacji toocomplex aplikacje dla firm z listy Fortune 500 i globalnych nośnika witryn sieci Web. 

> "Mamy dość dużych społeczność deweloperów korzystających z systemu hello z deweloperami więcej niż 100 000 na naszych forach i więcej niż 350,000 witryn, które są aktywne, systemem Umbraco".
> 
> — Umbraco Witold Christensen, realizacji techniczne
> 
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-Umbraco/player]
> 
> 

wdrożenia klienta toosimplify, Umbraco dodane Umbraco jako — usługa (UaaS): oferty oprogramowania — jako — usługa (SaaS), która eliminuje potrzebę hello wdrożeń lokalnych zawiera wbudowane skalowanie i usuwa zarządzania obciążenie przez włączenie Deweloperzy toofocus produktu innowacji zamiast rozwiązania zarządzania. Program Umbraco jest w stanie tooprovide tych korzyści polegając na hello elastyczny model (PaaS) platformy jako usługi udostępniane przez Microsoft Azure.

UaaS umożliwia SaaS klientów toouse Umbraco CMS możliwości, które były wcześniej poza ich zasięgu. Ci klienci są udostępniane z środowiska CMS pracy, który zawiera produkcyjną bazę danych. Klienci mogą sumują tootwo dodatkowych baz danych do prac deweloperskich i środowisk, w zależności od wymagań przemieszczania. Po zażądaniu nowego środowiska zautomatyzowany proces przypisuje klienta bazy danych automatycznie. Hello nowej bazy danych jest gotowy w sekundach, ponieważ hello bazy danych już zostały wstępnie udostępnione przez program Umbraco z puli elastycznej Azure dostępnych baz danych (zobacz rysunek 1).

![Cykl życia inicjowania obsługi administracyjnej Umbraco](./media/sql-database-implementation-umbraco/figure1.png)

Rysunek 1. Inicjowanie obsługi cyklu życia Umbraco jako usługa (UaaS)

## <a name="azure-elastic-pools-and-automation-simplify-deployments"></a>Pule elastyczne Azure i automatyzację uprościć wdrożenia
Z bazy danych SQL Azure i innymi usługami Azure Umbraco klienci mogą samodzielnie inicjować środowiskami i Umbraco łatwo monitorowanie i zarządzanie bazami danych w ramach intuicyjne przepływu pracy:

1. Provision
   
   Program Umbraco przechowuje pojemności 200 dostępnych wstępnie przygotowany baz danych z puli elastycznej. Po zarejestrowaniu się nowego nabywcy dla UaaS Umbraco zapewnia powitania klienta z nowym środowisku SMF w najbliższym czasie rzeczywistym przez przypisywanie ich bazy danych z hello dostępności puli.
   
   Gdy puli dostępności osiągnie progu, tworzona jest nowa pula elastycznej i nowych baz danych są wstępnie przygotowany toobe przypisane toocustomers zgodnie z potrzebami.
   
   Implementacja jest pełni zautomatyzowany przy użyciu biblioteki zarządzania C# i kolejek usługi Azure Service Bus.
2. Korzystanie z
   
   Stosowanie toothree środowiska (produkcji, tymczasowego, i/lub Programowanie), każdy z własną bazę danych. Klient bazy danych znajdują się w pule elastyczne, które umożliwia wydajne skalowanie bez udostępniania tooover tooprovide Umbraco.
   
   ![Przegląd projektu Umbraco](./media/sql-database-implementation-umbraco/figure2.png)
   
   ![Szczegóły projektu Umbraco](./media/sql-database-implementation-umbraco/figure3.png)
   
   Rysunek 2. Program Umbraco jako — usługa (UaaS) klienta witryny sieci Web, przedstawiający Przegląd projektu i szczegóły
   
   Baza danych SQL Azure używa jednostki transakcji bazy danych (Dtu) toorepresent hello względną wydajność wymagane dla transakcji bazy danych rzeczywistych. Dla klientów UaaS baz danych jest zwykle używana w Dtu około 10, ale każda ma tooscale elastyczność hello na żądanie. Oznacza to, że UaaS można zapewnić, że klienci zawsze są niezbędne zasoby, nawet w godzinach szczytu. Na przykład podczas ostatniego zdarzenia sportowych niedzielę wieczorem jednego klienta UaaS wystąpił pików bazy danych w górę Dtu too100 na czas trwania hello hello gier. Azure pule elastyczne możliwe jej Umbraco toosupport tego wysokie zapotrzebowanie, bez spadku wydajności.
3. Monitorowanie
   
   Monitory Umbraco bazy danych za pomocą pulpitów nawigacyjnych w portalu Azure, wraz z niestandardowych wiadomości e-mail dla alertów hello działania.
4. Odzyskiwanie po awarii
   
   Platforma Azure oferuje dwie opcje odzyskiwania awaryjnego (DR): aktywna replikacja geograficzna i przywracaniem geograficznym. Witaj firmy należy wybrać opcję odzyskiwania po awarii zależy od jego [cele ciągłość prowadzenia działalności biznesowej](sql-database-business-continuity.md).
   
   aktywna replikacja geograficzna zapewnia hello najszybszym poziom odpowiedzi w przypadku hello przestoju. Przy użyciu aktywna replikacja geograficzna, utworzeniem toofour elementów dodatkowych do odczytu na serwerach w różnych regionach, a następnie można zainicjować trybu failover tooany liczbę hello pomocniczych baz danych w przypadku hello awarii.
   
   Program Umbraco nie wymaga — replikacja geograficzna, ale jego korzystać z przywracaniem geograficznym Azure toohelp upewnij się, minimalna przestoju w przypadku hello awarii. geograficzne polega na kopie zapasowe bazy danych w geograficznie nadmiarowego magazynu Azure. Gdy jest awaria w regionie podstawowym hello, która umożliwia użytkownikom toorestore z kopii zapasowej.
5. Usuwanie
   
   Po usunięciu środowiska projektu, wszystkie skojarzone bazy danych (Programowanie, przemieszczania lub na żywo) zostaną usunięte podczas oczyszczania kolejki usługi Azure Service Bus. To automatyczne proces przywracania hello puli elastycznej bazy danych dostępności tooUmbraco nieużywanych baz danych, udostępnia je do przyszłych udostępniania przy zachowaniu maksymalne wykorzystanie.

## <a name="elastic-pools-allow-uaas-tooscale-with-ease"></a>Elastyczne pule zezwalają UaaS tooscale z łatwością
Dzięki wykorzystaniu Azure pule elastyczne, Umbraco zoptymalizować wydajność w przypadku klientów bez konieczności tooover lub niepełnej udostępniania. Umbraco ma obecnie niemal 3000 baz danych między 19 pule elastyczne, z hello tooeasily możliwości skalowania jako tooaccommodate wymagane ich istniejących klientów 325,000 lub nowych klientów, którzy są gotowe toodeploy SMF w chmurze hello.

W rzeczywistości zgodnie z tooMorten Christensen, techniczne prowadzić na Umbraco, "UaaS teraz występują wzrostu około 30 nowych klientów na dzień. Naszych klientów są szczególną przyjemność z wygodę hello jest możliwe tooprovision nowe projekty w sekundach, natychmiast publikowanie witryn aktualizacji tootheir na żywo ze środowiska programowania przy użyciu "jednym kliknięciem wdrożenia" i wprowadź zmiany, podobnie jak szybko, jeśli znajduje się błędy . "

Jeśli klient nie wymaga już środowisku drugi i/lub trzeci, wystarczy po prostu usunąć tych środowisk. Który zwolni zasoby, które może służyć do innych klientów jako część hello Umbraco puli elastycznej bazy danych dostępności.

![Architektura wdrażania usługi program Umbraco](./media/sql-database-implementation-umbraco/figure4.png)

Rysunek 3. UaaS architektura wdrażania usługi Microsoft Azure

## <a name="hello-path-from-datacenter-toocloud"></a>Ścieżka Hello z toocloud centrum danych
Gdy deweloperzy Umbraco hello początkowo hello decyzji toomove tooa modelu SaaS, znał czy powinny toobuild sposób ekonomiczne i skalowalne, usługi hello wychodzącego.

> "elastyczne pule są dokładne dopasowanie dla naszych SaaS oferty, ponieważ firma Microsoft może wybrać pojemności górę i w dół zgodnie z potrzebami. Inicjowanie obsługi administracyjnej jest łatwe, a z naszych Instalatora możemy zapewnić wykorzystania maksimum."
> 
> — Umbraco Witold Christensen, realizacji techniczne
> 
> 

"Możemy toospend czasu na rozwiązywanie problemów klientów, nie zarządzanie infrastrukturą. Możemy toomake go łatwo tooget naszym klientom Witaj najbardziej wartości "mówi Niels Hartvig, twórcę Umbraco. "Początkowo uznane serwerów hello, nad hosta, ale planowania pojemności byłby nightmare". Przypadkowo Umbraco nie zawiera żadnych administratorów bazy danych, które podkreślenia propozycji wartość klucza dla przy użyciu UaaS.

Jeden cel ważne dla deweloperów Umbraco hello został tooprovide sposób dla środowisk tooprovision klientów UaaS szybko i bez ograniczeń pojemności. Jednak warunkiem, że dedykowanych usługi hostowanej w centrach danych Umbraco byłyby wymagane wiele toohandle nadmiarowej pojemności ulega zapaleniu podczas przetwarzania. Który będzie mieć przeznaczone Dodawanie infrastruktury obliczeniowej znaczne, który będzie regularnie wykorzystany.

Ponadto zespół deweloperów Umbraco hello chciał rozwiązania, które umożliwiałyby ich tooreuse tyle ich istniejący kod, jak to możliwe. Deweloper Umbraco Mikkel Madsen stany, "możemy zadowalający hello narzędzi programistycznych firmy Microsoft, które możemy już znasz, takich jak Microsoft SQL Server, bazy danych SQL Microsoft Azure, platformy ASP.net i internetowe usługi informacyjne (IIS). Przed inwestycją w IaaS i PaaS w chmurze rozwiązania, możemy się upewnić, że będzie obsługuje on naszych narzędzi firmy Microsoft i platformy, dlatego nie mamy bazy kodu tooour masowych zmian toomake toomake. "

toomeet wszystkie jego kryteriów, Umbraco wyszukiwanego partnera chmury z powitania po kwalifikacji:

* Wystarczająca pojemność i niezawodności
* Obsługa narzędzi programistycznych firmy Microsoft, dzięki tym Umbraco, nie będzie inżynierów wymuszone toocompletely reinvent swoje Środowisko deweloperskie
* Obecność we wszystkich hello rynkach geograficznych, w których UaaS konkuruje (firm potrzeby tooensure czy one szybko dostęp do danych i czy dane są przechowywane w lokalizacji, która spełnia wymogi prawne regionalne)

## <a name="why-umbraco-chose-azure-for-uaas"></a>Dlaczego Umbraco wybrany Azure dla UaaS
Zgodnie z tooMorten Christensen "po uwzględnieniu wszystkich opcji, wybraliśmy Azure ponieważ spełniał wszystkie nasze kryteria z możliwości zarządzania i skalowalność toofamiliarity i efektywności. Skonfigurowanie środowiska hello na maszynach wirtualnych Azure, a każde środowisko ma własne wystąpienie bazy danych SQL Azure z wszystkich wystąpień hello w pule elastyczne. Oddzielenie baz danych między programowanie, przemieszczania i środowiskach produkcyjnych, możemy zaoferować klientów niezawodną wydajność izolacji dopasowane tooscale — Windows ogromnych. "

Witold będzie nadal występował, "przed tooprovision serwerów sieci web, baz danych było ręcznie. Nie mamy teraz toothink informacji na ten temat. Wszystko jest zautomatyzowany — od zainicjowania obsługi toocleanup. "

Witold jest również wszystkiego o hello skalowanie możliwości oferowane przez platformę Azure. "elastyczne pule są dokładne dopasowanie dla naszych SaaS oferty, ponieważ firma Microsoft może wybrać pojemności górę i w dół zgodnie z potrzebami. Inicjowanie obsługi administracyjnej jest łatwe, a z naszych Instalatora możemy zapewnić wykorzystania maksimum." Stany Witold, "hello prostotę pule elastyczne, oraz zapewnienie hello na podstawie warstwy usługi Dtu zapewnia nam hello zasilania tooprovision nowych pul zasobów na żądanie. Ostatnio jeden z naszych klientów większych daszenie kalenicowe Dtu too100 w jego środowisku produkcyjnym. Za pomocą platformy Azure, naszych pule elastyczne podać baz danych powitania klienta zasoby hello one potrzebne w czasie rzeczywistym bez konieczności toopredict jednostek dtu w warstwie wymagania. Krótko mówiąc, naszym klientom uzyskać hello Włącz wokół czasu oczekiwane, czy możemy spełnić naszych umów poziomu usług wydajności."

Go podsumowuje przez Mikkel Madsen: "Firma Microsoft już przyjętych hello zaawansowanych Azure algorytmu, który łączy na powitania wspólnego SaaS scenariusza (dołączania nowych klientów w czasie rzeczywistym na dużą skalę) tooour aplikacji wzorca (wstępnie udostępniania bazy danych, zarówno programowanie i na żywo) podstawową technologią (przy użyciu kolejek usługi Azure Service Bus w połączeniu z bazą danych SQL Azure)."

## <a name="with-azure-uaas-is-exceeding-customer-expectations"></a>Przy użyciu platformy Azure UaaS jest przekroczenie oczekiwań klientów
Po wybraniu Azure jako partnera chmury, Umbraco została stanie tooprovide UaaS klientów z optymalizacji wydajności zarządzanie zawartością, bez wymaganych od siebie rozwiązanie inwestycji hello zasobów IT. Jak Witold jest wyświetlany komunikat "przyłączyć hello wygody deweloperów i skalowalność, Azure zapewnia nam i klientów są thrilled z funkcjami hello i niezawodności. Ogólnie był dużą win firmie Microsoft!"

## <a name="more-information"></a>Więcej informacji
* toolearn więcej informacji na temat usługi Azure pule elastyczne, zobacz [pule elastyczne](sql-database-elastic-pool.md).
* toolearn więcej informacji na temat usługi Azure Service Bus, zobacz [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).
* Zobacz toolearn więcej informacji na temat ról sieć Web i roli proces roboczy [roli proces roboczy](../fundamentals-introduction-to-azure.md#compute).    
* toolearn więcej informacji na temat sieci wirtualne, zobacz [sieci wirtualne](https://azure.microsoft.com/documentation/services/virtual-network/).    
* toolearn więcej informacji na temat tworzenia kopii zapasowych i odzyskiwania, zobacz [ciągłość prowadzenia działalności biznesowej](sql-database-business-continuity.md).    
* toolearn więcej informacji na temat monitorowania ppols, zobacz [monitorowania pule](sql-database-elastic-pool-manage-portal.md).    
* toolearn więcej informacji na temat Umbraco jako usługa, zobacz [Umbraco](https://umbraco.com/cloud).

