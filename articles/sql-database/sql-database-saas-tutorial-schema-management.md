---
title: "schemat bazy danych SQL Azure aaaManage w aplikacji wielodostępnych | Dokumentacja firmy Microsoft"
description: "Zarządzanie schematami wielu dzierżaw w aplikacji z wieloma dzierżawami, która korzysta z usługi Azure SQL Database"
keywords: "samouczek usługi sql database"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: billgib; sstein
ms.openlocfilehash: ea946e556808dabd60dd39cb8173d0512d4bddec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-schema-for-multiple-tenants-in-hello-wingtip-saas-application"></a>Zarządzanie schematu dla wielu dzierżawców w hello aplikacji Wingtip SaaS

Witaj [pierwszy samouczek Wingtip SaaS](sql-database-saas-tutorial.md) pokazuje, jak udostępnić bazę danych dzierżawy i zarejestruj go w katalogu hello aplikacji hello. Podobnie jak wszelkie aplikacje powitalne aplikacji Wingtip SaaS rozpoczyna się wraz z upływem czasu, a czasem wymaga toohello zmian w bazie danych. Zmiany mogą obejmować schematu nowe lub zostały zmienione, dane referencyjne nowe lub zostały zmienione i bazy danych procedury obsługi zadań tooensure optymalną wydajność aplikacji. Przy użyciu aplikacji SaaS te zmiany należy toobe wdrożonego w skoordynowany sposób na potencjalnie ogromną floty dzierżawy baz danych. Toobe te zmiany w przyszłości dzierżawy baz danych, muszą one mieć toobe włączyć do procesu udostępniania hello.

W tym samouczku Eksploruje dwa scenariusze - wdrażania aktualizacji danych odwołania dla wszystkich dzierżawców i retuning indeksu na powitania tabeli zawierającej dane referencyjne hello. Witaj [zadania elastyczne](sql-database-elastic-jobs-overview.md) funkcji jest używane tooexecute te operacje we wszystkich dzierżaw i hello *złotego* bazy danych dzierżawy, który służy jako szablon dla nowych baz danych.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]

> * Tworzenie zadania konta
> * Wysyłanie zapytań na wielu dzierżawców
> * Aktualizowanie danych we wszystkich bazach danych dzierżaw
> * Tworzenie indeksu tabeli we wszystkich bazach danych dzierżaw


toocomplete tego samouczka, Utwórz hello się, że następujące wymagania wstępne są spełnione:

* Aplikacja Wingtip SaaS Hello jest wdrażana. Zobacz toodeploy w mniej niż pięć minut [wdrażania i aplikacji Wingtip SaaS hello](sql-database-saas-tutorial.md)
* Zainstalowany jest program Azure PowerShell. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z programem Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* zainstalowana jest najnowsza wersja Hello programu SQL Server Management Studio (SSMS). [Pobieranie i instalowanie programu SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

*Ten samouczek używa funkcji hello usługi baza danych SQL, które są w ograniczonym wersji zapoznawczej (zadania elastycznej bazy danych). Jeśli chcesz toodo w tym samouczku, podaj identyfikator subskrypcji tooSaaSFeedback@microsoft.com podmiotu = elastycznej Podgląd zadania. Po otrzymaniu potwierdzenia, że subskrypcja została włączona, [Pobierz i zainstaluj polecenia cmdlet hello najnowszej wersji wstępnej zadania](https://github.com/jaredmoo/azure-powershell/releases). Ta wersja zapoznawcza jest ograniczony, więc skontaktuj się z SaaSFeedback@microsoft.com pytania związane z lub pomocy technicznej.*


## <a name="introduction-toosaas-schema-management-patterns"></a>Wprowadzenie tooSaaS wzorców Zarządzanie schematami

Witaj pojedynczej dzierżawy na bazę danych SaaS wzorca korzyści na wiele sposobów z hello danych izolacji, co powoduje, ale na powitania jednocześnie wprowadza hello dodatkową złożoność obsługi i zarządzania nimi wielu baz danych. [Zadania elastyczne](sql-database-elastic-jobs-overview.md) ułatwia administrowanie i zarządzanie warstwy danych programu SQL hello. Zadania umożliwiają toosecurely a niezawodnie, uruchom zadania (skryptów T-SQL) niezależne od działań użytkownika lub danych wejściowych, na grupę baz danych. Ta metoda może być używane toodeploy schematu i wspólne zmiany danych odwołania dla wszystkich dzierżawców w aplikacji. Zadania elastyczne mogą być również używane toomaintain *złotego* toocreate nowi dzierżawcy, zapewniając zawsze zawiera najnowsze dane schematu i odwołanie hello używana kopia hello bazy danych.

![ekran](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a>Ograniczona wersja zapoznawcza Zadań elastycznych

Istnieje nowa wersja Zadań elastycznych, która jest teraz zintegrowaną funkcją usługi Azure SQL Database (nie wymaga żadnych dodatkowych usług ani składników). Nowa wersja Zadań elastycznych jest obecnie dostępna w ograniczonej wersji zapoznawczej. Ta ograniczona wersja zapoznawcza obecnie obsługuje PowerShell toocreate zadania konta i toocreate T-SQL zadania i zarządzać nimi.

> [!NOTE]
> *Ten samouczek używa funkcji hello usługi baza danych SQL, które są w ograniczonym wersji zapoznawczej (zadania elastycznej bazy danych). Jeśli chcesz toodo w tym samouczku, podaj identyfikator subskrypcji tooSaaSFeedback@microsoft.com podmiotu = elastycznej Podgląd zadania. Po otrzymaniu potwierdzenia, że subskrypcja została włączona, [Pobierz i zainstaluj polecenia cmdlet hello najnowszej wersji wstępnej zadania](https://github.com/jaredmoo/azure-powershell/releases). Ta wersja zapoznawcza jest ograniczony, więc skontaktuj się z SaaSFeedback@microsoft.com pytania związane z lub pomocy technicznej.*

## <a name="get-hello-wingtip-application-scripts"></a>Pobierz skrypty aplikacji hello Wingtip

Witaj Wingtip SaaS skrypty i kod źródłowy aplikacji są dostępne w hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repozytorium github. [Kroki skrypty Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-a-job-account-database-and-new-job-account"></a>Tworzenie bazy danych konta zadania oraz nowego konta zadania

Ten samouczek wymaga użycia programu PowerShell toocreate hello zadania konta bazy danych i zadania konta. Podobnie jak MSDB i agenta SQL korzysta zadania elastyczne Azure SQL z bazy danych definicje zadań toostore, stan zadania i historii. Po utworzeniu hello zadania konta można tworzyć i natychmiast monitorowania zadań.

1. Otwórz... \\Modułów uczenia\\Zarządzanie schematami\\*SchemaManagement.ps1 pokaz* w hello **PowerShell ISE**.
1. Naciśnij klawisz **F5** toorun hello skryptu.

Hello *SchemaManagement.ps1 pokaz* hello wywołania skryptu *SchemaManagement.ps1 Wdróż* skryptu toocreate *S2* bazy danych o nazwie **jobaccount** na powitania serwera wykazu. Następnie tworzy hello zadania konta, przekazywanie jako parametru toohello zadania konta tworzenia wywołanie hello jobaccount w bazie danych.

## <a name="create-a-job-toodeploy-new-reference-data-tooall-tenants"></a>Utwórz zadanie toodeploy nowe odwołanie danych tooall dzierżawcy

Każda baza danych dzierżawy zawiera zestaw miejscową typów, które definiują hello rodzaju zdarzenia, które znajdują się w miejscu. W tym ćwiczeniu można wdrożyć aktualizacji tooall hello dzierżawy baz danych tooadd dwa dodatkowe miejsce typów: *Racing motocykla* i *klub pływackich*. Te typy miejscową odpowiada obraz tła toohello widocznych hello dzierżawy zdarzeń aplikacji.

Kliknij menu rozwijane typu miejscową hello, a następnie sprawdź, czy tylko 10 miejscową typu opcje są dostępne, a w szczególności tej "Motocykla Racing" i "Pływackich klub" nie znajdują się na liście hello.

Teraz Utwórzmy hello tooupdate zadania *VenueTypes* tabeli w wszystkich baz danych dzierżawy hello i dodawanie nowych typów miejscową hello.

toocreate nowe zadanie używamy zestawu zadań systemu przechowywane procedury utworzone w bazie danych jobaccount hello podczas tworzenia hello zadania konta.

1. Otwórz SSMS i Połącz z serwerem wykazu toohello: katalogu -\<użytkownika\>. database.windows.net serwera
1. Także podłączyć serwer dzierżawy toohello: tenants1 -\<użytkownika\>. database.windows.net
1. Przeglądaj toohello *contosoconcerthall* bazy danych na powitania *tenants1* powitania serwera i zapytań *VenueTypes* tooconfirm tabeli który *Racing motocykla*  i *klub pływackich* **nie są** hello listy wyników.
1. Otwórz hello pliku... \\Modułów szkoleniowych\\Zarządzanie schematami\\DeployReferenceData.sql
1. Modyfikowanie instrukcji hello: Ustaw @wtpUser = &lt;użytkownika&gt; i zastąp wartość użytkownika hello używane po wdrożeniu aplikacji Wingtip hello
1. Upewnij się, są połączone toohello jobaccount w bazie danych i naciśnij klawisz **F5** do uruchamiania skryptu hello

* **SP\_dodać\_docelowej\_grupy** tworzy Nazwa grupy docelowej hello DemoServerGroup, teraz potrzebujemy tooadd członków docelowych.
* **SP\_dodać\_docelowej\_grupy\_elementu członkowskiego** dodaje *serwera* docelowy typ elementu członkowskiego, które uzna za wszystkie bazy danych w ramach tego serwera (Uwaga to hello tenants1-&lt; Użytkownik&gt; serwer zawierający hello dzierżawcy z bazy danych) w czasie zadania wykonywania powinny być uwzględnione w zadania hello hello drugi polega na dodaniu *bazy danych* docelowy typ elementu członkowskiego, w szczególności hello ("złotego" bazy danych basetenantdb) który znajduje się w katalogu -&lt;użytkownika&gt; serwera, a na koniec innego *bazy danych* docelowego elementu członkowskiego typu tooinclude hello adhocanalytics bazy danych grupy używany w samouczku nowsze.
* **sp\_add\_job** tworzy zadanie o nazwie „Reference Data Deployment”.
* **SP\_dodać\_etap zadania** tworzy hello etap zadania zawierające T-SQL polecenia tekst tooupdate hello odwołanie do tabeli, VenueTypes
* Widoki pozostałych Hello w skrypcie hello wyświetlanie istnienie hello hello obiektów i wykonywania zadania monitorowania. Użyj tych wartości stanu hello tooreview zapytań w hello **cyklu życia** toodetermine kolumny, gdy zadania hello zakończy się pomyślnie na wszystkie dzierżawy i bazy danych Witaj dwie dodatkowe zawierające hello tabeli referencyjnej.

1. W programie SSMS, Przeglądaj toohello *contosoconcerthall* bazy danych na powitania *tenants1* powitania serwera i zapytań *VenueTypes* tooconfirm tabeli który *motocykla Racing* i *klub pływackich* **są** teraz na liście wyników hello.


## <a name="create-a-job-toomanage-hello-reference-table-index"></a>Tworzenie indeksu tabeli zadania toomanage hello odwołania

Podobne toohello poprzednim ćwiczeniu, tym ćwiczeniu tworzy indeks hello toorebuild zadania hello klucza podstawowego tabeli odwołania, operacji zarządzania typowe bazy danych administrator może wykonać po załadowaniu dużej ilości danych do tabeli.

Utwórz zadanie, używając hello tego samego zadania "system" procedur składowanych.

1. Otwórz program SSMS i połącz toohello katalogu -&lt;użytkownika&gt;. database.windows.net serwera
1. Otwórz hello pliku... \\Modułów szkoleniowych\\Zarządzanie schematami\\OnlineReindex.sql
1. Kliknij prawym przyciskiem myszy, wybierz połączenie i połącz toohello katalogu -&lt;użytkownika&gt;. database.windows.net serwera, jeśli nie został jeszcze połączony
1. Upewnij się, są połączone toohello jobaccount w bazie danych i naciśnij klawisz F5 toorun hello skryptu

* sp\_add\_job tworzy nowe zadanie o nazwie „Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885”.
* SP\_dodać\_etap zadania tworzy hello etap zadania zawierające T-SQL polecenia tekst tooupdate hello indeksu




## <a name="next-steps"></a>Następne kroki

W tym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]

> * Utwórz zadania konta tooquery między wieloma dzierżawcami
> * Aktualizowanie danych we wszystkich bazach danych dzierżaw
> * Tworzenie indeksu tabeli we wszystkich bazach danych dzierżaw

[Samouczek analitycznych zapytań ad-hoc](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Dodatkowe samouczki, które zależą od hello wdrażanie aplikacji Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Zarządzanie skalowaną w poziomie bazą danych w chmurze](sql-database-elastic-jobs-overview.md)
* [Tworzenie baz danych skalowanych w poziomie i zarządzanie nimi](sql-database-elastic-jobs-create-and-manage.md)
