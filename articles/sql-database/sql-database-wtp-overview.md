---
title: "aaaIntro SaaS Wingtip — baza danych SQL Azure wielodostępnych aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, korzystając z przykładowej aplikacji wielodostępnych, która używa usługi Azure SQL Database aplikacji Wingtip SaaS hello"
keywords: "samouczek usługi sql database"
services: sql-database
author: stevestein
manager: jhubbard
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: sstein
ms.openlocfilehash: daeed293116fca22718831b780533be6ef2ad178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-wingtip-saas-application"></a>Wprowadzenie toohello aplikacji Wingtip SaaS

Witaj *Wingtip SaaS* jest aplikacja przykładowa aplikacja wielodostępne, który demonstruje hello wyjątkowych zalet bazy danych SQL. Aplikacja Hello korzysta z bazy danych na dzierżawcy, wzorzec aplikacji SaaS, tooservice wielu dzierżawców. Aplikacja Hello jest zaprojektowana tooshowcase funkcje bazy danych SQL Azure, które umożliwiają SaaS scenariuszy, w tym kilka wzorce projektowania i zarządzania SaaS. Uzyskaj tooquickly i uruchomiona, wdraża aplikacji Wingtip SaaS hello w mniej niż pięć minut!

Skrypty zarządzania i kodu źródłowego aplikacji są dostępne w hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repozytorium github. skrypty hello toorun, [hello modułów uczenia folder pobierania](#download-and-unblock-the-wingtip-saas-scripts) tooyour komputera lokalnego.

## <a name="sql-database-wingtip-saas-tutorials"></a>Samouczki SaaS Wingtip bazy danych SQL

Po wdrożeniu aplikacji hello, Poznaj hello następujące samouczki, które zależą od hello początkowe wdrożenie. Te samouczki Poznaj typowe wzorce SaaS, które korzystają z wbudowanych funkcji bazy danych SQL, SQL Data Warehouse i innymi usługami Azure. Samouczki zawierają skryptów programu PowerShell z szczegółowe wyjaśnienia, które znacznie ułatwić zrozumienie, i implementowanie hello tego samego wzorce zarządzania SaaS w aplikacji.


| Samouczek | Opis |
|:--|:--|
|[Wdrażanie i Eksploruj aplikacji Wingtip SaaS hello](sql-database-saas-tutorial.md)| **ZACZNIJ TUTAJ!** Wdrażanie i Eksploruj tooyour aplikacji Wingtip SaaS hello subskrypcji platformy Azure. |
|[Dostarczanie i katalogu dzierżawcy](sql-database-saas-tutorial-provision-and-catalog.md)| Dowiedz się, jak aplikacja hello łączy tootenants korzystanie z bazy danych katalogu, i jak mapuje katalogu hello dzierżawy tootheir danych. |
|[Monitorowanie i zarządzanie nimi wydajności](sql-database-saas-tutorial-performance-monitoring.md)| Dowiedz się, jak monitorowanie toouse funkcje bazy danych SQL i jak tooset alerty, gdy przekroczenia progów wydajności. |
|[Monitorowanie za pomocą analizy dzienników (OMS)](sql-database-saas-tutorial-log-analytics.md) | Informacje o używaniu [analizy dzienników](../log-analytics/log-analytics-overview.md) toomonitor dużych ilości zasobów, między wiele pul. |
|[Przywracanie pojedynczej dzierżawy](sql-database-saas-tutorial-restore-single-tenant.md)| Dowiedz się, jak toorestore tooa bazy danych dzierżawy wcześniejszego punktu w czasie. Kroki toorestore tooa równoległych bazy danych, zostawianie hello istniejącej dzierżawy bazy danych w trybie online, również są uwzględniane. |
|[Zarządzanie schematem dzierżawy](sql-database-saas-tutorial-schema-management.md)| Dowiedz się, jak tooupdate schematu i aktualizacja odwoływał się do danych, we wszystkich dzierżawców Wingtip SaaS. |
|[Uruchom analytics ad hoc](sql-database-saas-tutorial-adhoc-analytics.md) | Tworzenie bazy danych analizy ad hoc i uruchamianie zapytań rozproszonych w czasie rzeczywistym we wszystkich dzierżawców.  |
|[Uruchom analytics dzierżawy](sql-database-saas-tutorial-tenant-analytics.md) | Wyodrębnianie danych dzierżawy do analityka bazy danych lub dane magazynu na potrzeby uruchamiania zapytań analityczne w trybie offline. |



## <a name="application-architecture"></a>Architektura aplikacji

Aplikacja Wingtip SaaS Hello wykorzystuje model bazy danych dla dzierżawy hello i używa SQL pule elastyczne toomaximize wydajności. Inicjowanie obsługi administracyjnej i mapowanie danych tootheir dzierżawcy, katalog bazy danych jest używany. Witaj aplikacji Wingtip SaaS core, używa puli w przypadku dzierżaw trzy próbki oraz hello katalogu w bazie danych. Kończenie wiele hello samouczki Wingtip SaaS spowodować dodatki toohello początkowe wdrożenie, wprowadzając baz danych analitycznych, między bazami danych zarządzania schematu itp.


![Architektura SaaS Wingtip](media/sql-database-wtp-overview/app-architecture.png)


Podczas przechodzenia przez hello samouczki i Praca z aplikacji hello, jest ważne toofocus wzorce SaaS hello w odniesieniu toohello warstwy danych. Innymi słowy skupić się na powitania warstwy danych i nie ponad analizowanie hello samej aplikacji. Opis wdrażania hello tych wzorców SaaS jest tooimplementing klucza tych wzorców w aplikacjach, rozważając wszelkie potrzebne modyfikacje dla konkretnych potrzeb biznesowych.

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Pobierz i odblokować hello Wingtip SaaS skryptów

Zawartość pliku wykonywalnego (skrypty, biblioteki dll) mogą być blokowane przez system Windows, gdy pliki zip są pobierane z zewnętrznego źródła i wyodrębnione. Podczas wyodrębniania pliku zip skrypty hello ***wykonaj kroki hello poniżej plik zip hello toounblock przed wyodrębniania***. Dzięki temu mogą toorun hello skryptów.

1. Przeglądaj zbyt[repozytorium github Wingtip SaaS hello](https://github.com/Microsoft/WingtipSaaS).
1. Kliknij przycisk **klonowania lub pobierania**.
1. Kliknij przycisk **Pobierz ZIP** i Zapisz plik hello.
1. Kliknij prawym przyciskiem myszy hello **WingtipSaaS master.zip** pliku, a następnie wybierz **właściwości**.
1. Na powitania **ogólne** wybierz opcję **Odblokuj**.
1. Kliknij przycisk **OK**.
1. Wyodrębnij pliki hello.

Skrypty znajdują się w hello *... \\Wzorca WingtipSaaS\\modułów uczenia* folderu.


## <a name="working-with-hello-wingtip-saas-powershell-scripts"></a>Praca z hello skryptów programu PowerShell Wingtip SaaS

Witaj tooget najbardziej poza próbki hello należy toodive na powitania podane skrypty. Użyj punktów przerwania i krok za pomocą skryptów hello, sprawdzając szczegóły hello implementowania hello różnych wzorców SaaS. tooeasily kroków hello podane skryptów i modułów hello najlepiej zrozumienie, zaleca się używanie hello [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).

### <a name="update-hello-configuration-file-for-your-deployment"></a>Aktualizuj plik konfiguracji powitania dla danego wdrożenia

Edytuj hello **UserConfig.psm1** pliku z hello zasobów grup i użytkowników wartość ustawiona podczas wdrażania:

1. Otwórz hello *PowerShell ISE* i obciążenia... \\Modułów szkoleniowych\\*UserConfig.psm1* 
1. Aktualizacja *ResourceGroupName* i *nazwa* z określonymi wartościami hello wdrożenia (wierszach 10 i 11 tylko).
1. Zapisz zmiany Witaj!

Ustawienie tych wartości w tym miejscu po prostu uniemożliwia posiadanie tooupdate te wartości charakterystyczne dla wdrożenia każdego skryptu.

### <a name="execute-scripts-by-pressing-f5"></a>Wykonywanie skryptów poprzez naciśnięcie klawisza F5

Użyj skryptów kilka *$PSScriptRoot* foldery toonavigate i *$PSScriptRoot* jest oceniana tylko wtedy, gdy skryptów są wykonywane przez naciśnięcie przycisku **F5**.  Wyróżnianie i uruchamianie zaznaczenia (**F8**) może powodować błędy, więc naciśnij **F5** podczas uruchamiania skryptów.

### <a name="step-through-hello-scripts-tooexamine-hello-implementation"></a>Przejrzyj kroki implementacji hello tooexamine skrypty hello

Witaj najlepsze sposób toounderstand hello skryptów jest przy przechodzeniu przez nich toosee ich działania. Zapoznaj się z hello uwzględnione **pokaz -** skrypty, które przedstawia ogólny przepływ pracy toofollow łatwe. Witaj **pokaz -** skrypty tooaccomplish wymagane kroki hello każdego zadania, a więc Ustaw punkty przerwania i bardziej szczegółowego do poszczególnych hello wymaga szczegóły implementacji toosee hello różnych wzorców SaaS.

Wskazówki dotyczące eksplorowania i krokowe wykonywanie skryptów programu PowerShell:

* Otwórz **pokaz -** skryptów w hello PowerShell ISE.
* Wykonanie lub kontynuować **F5** (przy użyciu **F8** nie jest zalecana, ponieważ *$PSScriptRoot* nie jest oceniany, podczas uruchamiania opcji skryptu).
* Umieść punkty przerwania, klikając lub zaznaczając wiersz i naciskając klawisz **F9**.
* Pomiń wywołanie funkcji lub skryptu, używając klawisza **F10**.
* Wejdź do wywoływanej funkcji lub skryptu, używając klawisza **F11**.
* Wychodzenia z bieżącej funkcji hello lub skryptu, za pomocą wywołania **Shift + F11**.


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a>Badanie schematu bazy danych i wykonywanie zapytań SQL za pomocą aplikacji SSMS

Użyj [programu SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect i przeglądania hello serwery aplikacji i baz danych.

wdrożenie Hello początkowo ma dwie bazy danych SQL serwerów tooconnect zbyt hello *tenants1 -&lt;użytkownika&gt;*  serwera i hello *katalogu -&lt;użytkownika&gt;* serwera. tooensure połączenia pomyślne pokaz oba serwery mają [reguły zapory](sql-database-firewall-configure.md) stosowanie wszystkich adresów IP za pośrednictwem.


1. Otwórz *SSMS* i połącz toohello *tenants1 -&lt;użytkownika&gt;. database.windows.net* serwera.
1. Kliknij kolejno opcje **Połącz** > **Aparat bazy danych...** :

   ![serwer wykazu](media/sql-database-wtp-overview/connect.png)

1. W wersji demonstracyjnej są używane następujące poświadczenia: Nazwa logowania = *developer*, hasło =*P@ssword1*

   ![połączenie](media\sql-database-wtp-overview\tenants1-connect.png)

1. Powtórz kroki 2 i 3 i połącz toohello *katalogu -&lt;użytkownika&gt;. database.windows.net* serwera.

Po pomyślnym nawiązaniu połączenia powinny być widoczne oba serwery. Listy baz danych, które mogą być różne w zależności od dzierżawcy hello, które zostały udostępnione:

![eksplorator obiektów](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a>Następne kroki

[Wdrażanie aplikacji Wingtip SaaS hello](sql-database-saas-tutorial.md)
