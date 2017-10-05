---
title: "Zarządzanie schematami usługi Azure SQL Database w aplikacji z wieloma dzierżawami | Microsoft Docs"
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
ms.openlocfilehash: 78d76efb88bf11fa18a416b59e6f881539141232
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-schema-for-multiple-tenants-in-the-wingtip-saas-application"></a>Zarządzanie schematu dla wielu dzierżawców w aplikacji Wingtip SaaS

[Pierwszy samouczek Wingtip SaaS](sql-database-saas-tutorial.md) pokazuje, jak udostępnić bazę danych dzierżawy i zarejestruj go w katalogu aplikacji. Podobnie jak wszelkie aplikacje aplikacji Wingtip SaaS rozpoczyna się wraz z upływem czasu, a czasem wymaga zmiany w bazie danych. Zmiany mogą obejmować nowy lub zmieniony schemat, nowe lub zmienione dane referencyjne, oraz rutynowe zadania konserwacji bazy danych zapewniające optymalną wydajność aplikacji. W przypadku aplikacji SaaS zmiany te muszą zostać wprowadzone w sposób skoordynowany — potencjalnie w bardzo wielu bazach danych dzierżaw. Aby te zmiany można w przyszłości dzierżawy baz danych muszą należy włączyć do procesu inicjowania obsługi administracyjnej.

Ten samouczek analizuje dwa scenariusze — wdrażanie aktualizacji danych referencyjnych dla wszystkich dzierżaw i dostrajanie indeksu tabeli zawierającej dane referencyjne. [Zadania elastyczne](sql-database-elastic-jobs-overview.md) funkcja służy do wykonywania tych operacji we wszystkich dzierżawców i *złotego* bazy danych dzierżawy, który służy jako szablon dla nowych baz danych.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]

> * Tworzenie zadania konta
> * Wysyłanie zapytań na wielu dzierżawców
> * Aktualizowanie danych we wszystkich bazach danych dzierżaw
> * Tworzenie indeksu tabeli we wszystkich bazach danych dzierżaw


Do wykonania zadań opisanych w tym samouczku niezbędne jest spełnienie następujących wymagań wstępnych:

* Aplikacja Wingtip SaaS jest wdrażana. Aby wdrożyć w mniej niż 5 minut, zobacz [wdrażania i aplikacji Wingtip SaaS](sql-database-saas-tutorial.md)
* Zainstalowany jest program Azure PowerShell. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z programem Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* Zainstalowano najnowszą wersję programu SSMS (SQL Server Management Studio). [Pobieranie i instalowanie programu SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

*Ten samouczek zakłada użycie funkcji usługi SQL Database, które znajdują się w ograniczonej wersji zapoznawczej (zadania Elastic Database). Aby skorzystać z tego samouczka, prześlij identyfikator swojej subskrypcji na adres SaaSFeedback@microsoft.com z tematem Elastic Job Preview. Po otrzymaniu potwierdzenia, że Twoja subskrypcja została włączona, [pobierz i zainstaluj najnowsze polecenia cmdlet zadań w wersji wstępnej](https://github.com/jaredmoo/azure-powershell/releases). Ta wersja zapoznawcza jest ograniczony, więc skontaktuj się z SaaSFeedback@microsoft.com pytania związane z lub pomocy technicznej.*


## <a name="introduction-to-saas-schema-management-patterns"></a>Wprowadzenie do wzorców zarządzania schematami SaaS

Wzorzec SaaS pojedynczej dzierżawy na bazę danych korzysta na wiele sposobów z izolacji danych, ale jednocześnie cechuje się zwiększoną złożonością obsługi i zarządzania w przypadku wielu baz danych. Funkcja [Zadania elastyczne](sql-database-elastic-jobs-overview.md) ułatwia administrowanie i zarządzanie warstwą danych programu SQL. Zadania umożliwiają bezpieczne i niezawodne uruchamiania zleceń (skryptów T-SQL) na grupie baz danych niezależnie od interakcji z użytkownikiem lub danych wejściowych. Tej metody można użyć do wdrożenia schematu i zmiany wspólnych danych referencyjnych we wszystkich dzierżawach w aplikacji. Zadania elastyczne służą do konserwacji *wzorcowej* kopii bazy danych używanej do tworzenia nowych dzierżaw, dzięki czemu zawsze zawiera ona najnowszy schemat i dane referencyjne.

![ekran](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a>Ograniczona wersja zapoznawcza Zadań elastycznych

Istnieje nowa wersja Zadań elastycznych, która jest teraz zintegrowaną funkcją usługi Azure SQL Database (nie wymaga żadnych dodatkowych usług ani składników). Nowa wersja Zadań elastycznych jest obecnie dostępna w ograniczonej wersji zapoznawczej. Ograniczona wersja zapoznawcza obsługuje obecnie program PowerShell do tworzenia kont zadań, oraz oprogramowanie T-SQL do tworzenia zadań i zarządzania nimi.

> [!NOTE]
> *Ten samouczek zakłada użycie funkcji usługi SQL Database, które znajdują się w ograniczonej wersji zapoznawczej (zadania Elastic Database). Aby skorzystać z tego samouczka, prześlij identyfikator swojej subskrypcji na adres SaaSFeedback@microsoft.com z tematem Elastic Job Preview. Po otrzymaniu potwierdzenia, że Twoja subskrypcja została włączona, [pobierz i zainstaluj najnowsze polecenia cmdlet zadań w wersji wstępnej](https://github.com/jaredmoo/azure-powershell/releases). Ta wersja zapoznawcza jest ograniczony, więc skontaktuj się z SaaSFeedback@microsoft.com pytania związane z lub pomocy technicznej.*

## <a name="get-the-wingtip-application-scripts"></a>Pobieranie skryptów aplikacji Wingtip

Wingtip SaaS skrypty i kod źródłowy aplikacji są dostępne w [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repozytorium github. [Kroki, aby pobrać skrypty Wingtip SaaS](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-a-job-account-database-and-new-job-account"></a>Tworzenie bazy danych konta zadania oraz nowego konta zadania

Ten samouczek wymaga użycia programu PowerShell w celu utworzenia bazy danych konta zadania oraz samego konta zadania. Podobnie jak w przypadku aplikacji MSDB i SQL Agent, Zadania elastyczne używają usługi Azure SQL Database do przechowywania definicji zadań, ich stanu i historii. Po utworzeniu konta zadania można natychmiast przystąpić do tworzenia i monitorowania zadań.

1. Otwórz pozycję …\\Learning Modules\\Schema Management\\*Demo-SchemaManagement.ps1* w programie **PowerShell ISE**.
1. Naciśnij klawisz **F5**, aby uruchomić skrypt.

Skrypt *Demo-SchemaManagement.ps1* wywołuje skrypt *Deploy-SchemaManagement.ps1* w celu utworzenia bazy danych typu *S2* o nazwie **jobaccount** na serwerze wykazu. Następnie tworzy konto zadania, przekazując bazę danych jobaccount jako parametr wywołania tworzenia konta zadania.

## <a name="create-a-job-to-deploy-new-reference-data-to-all-tenants"></a>Tworzenie zadania służącego do wdrożenia nowych danych referencyjnych we wszystkich dzierżawach

Każda baza danych dzierżawy obejmuje zestaw typów miejsc, które definiują rodzaj zdarzeń obsługiwanych w danym miejscu. W tym ćwiczeniu wdrożysz i uaktualnisz wszystkie bazy danych dzierżaw w celu dodania dwóch dodatkowych typów miejsc: *Motorcycle Racing* i *Swimming Club*. Te typy miejsc odpowiadają obrazom tła, które widzisz w aplikacji zdarzeń dzierżawy.

Kliknij menu rozwijane typu miejsca i upewnij się, że jest dostępnych tylko 10 opcji typów miejsc — a w szczególności, że na liście brakuje opcji „Motorcycle Racing” i „Swimming Club”.

Utwórz teraz zadanie służące do zaktualizowania tabeli *VenueTypes* we wszystkich bazach danych dzierżawy i dodania nowych typów miejsc.

Aby utworzyć nowe zadanie, użyjemy zestawu procedur składowanych systemu zadań utworzonych w bazie danych jobaccount podczas tworzenia konta zadania.

1. Otwórz program SSMS i połącz się z serwerem wykazu: catalog-\<użytkownik\>.database.windows.net.
1. Połącz się również z serwerem dzierżaw: tenants1-\<użytkownik\>.database.windows.net.
1. Przejdź do bazy danych *contosoconcerthall* na serwerze *tenants1* i utwórz zapytanie dla tabeli *VenueTypes*, aby upewnić się, że na liście wyników nie ma pozycji *Motorcycle Racing* i *Swimming Club* ****.
1. Otwórz plik …\\Learning Modules\\Schema Management\\DeployReferenceData.sql.
1. Modyfikowanie instrukcji: Ustaw @wtpUser = &lt;użytkownika&gt; i zastąp wartość użytkownika używane w przypadku wdrażania aplikacji Wingtip
1. Upewnij się, że masz połączenie z bazą danych jobaccount, a następnie naciśnij klawisz **F5**, aby uruchomić skrypt.

* **sp\_add\_target\_group** tworzy nazwę grupy docelowej DemoServerGroup. Teraz należy dodać członków docelowych.
* **SP\_dodać\_docelowej\_grupy\_elementu członkowskiego** dodaje *serwera* docelowy typ elementu członkowskiego, które uzna za wszystkie bazy danych w ramach tego serwera (Uwaga to tenants1&lt; Użytkownik&gt; serwer zawierający dzierżawy baz danych) w czasie zadania wykonywania powinny być uwzględnione w zadaniu, polega na dodaniu drugiego *bazy danych* docelowy typ elementu członkowskiego, w szczególności "złotego" bazy danych (basetenantdb) który znajduje się w katalogu -&lt;użytkownika&gt; serwera, a na koniec innego *bazy danych* docelowy typ elementu członkowskiego grupy, aby uwzględnić adhocanalytics bazy danych, używany w samouczku nowsze.
* **sp\_add\_job** tworzy zadanie o nazwie „Reference Data Deployment”.
* **SP\_dodać\_etap zadania** tworzy etap zadania zawierające tekst polecenia T-SQL, aby zaktualizować tabeli referencyjnej VenueTypes
* Pozostałe widoki w skrypcie dotyczą istnienia obiektów i monitorowania wykonania zadań. Aby przejrzeć wartość stanu, użyj tych zapytań **cyklu życia** kolumnę, aby określić, kiedy zadanie pomyślnie zakończył się na wszystkie dzierżawy i dwóch dodatkowych baz danych zawierających tabeli referencyjnej.

1. W programie SSMS przejdź do bazy danych *contosoconcerthall* na serwerze *tenants1* i utwórz zapytanie dla tabeli *VenueTypes*, aby upewnić się, że na liście wyników znajdują się teraz pozycje *Motorcycle Racing* i *Swimming Club* ****.


## <a name="create-a-job-to-manage-the-reference-table-index"></a>Tworzenie zadania do zarządzania indeksem tabeli referencyjnej

Podobnie jak w poprzednim ćwiczeniu, w tym zostanie utworzone zadanie służące do odbudowania indeksu klucza podstawowego tabeli referencyjnej — typowej operacji z zakresu zarządzania bazą danych, którą administrator może wykonać po załadowaniu dużej ilości danych do tabeli.

Utwórz zadanie, używając tych samych procedur składowanych „system”.

1. Otwórz SSMS i połącz się katalogu -&lt;użytkownika&gt;. database.windows.net serwera
1. Otwórz plik …\\Learning Modules\\Schema Management\\OnlineReindex.sql.
1. Kliknij prawym przyciskiem myszy, wybierz połączenie i połącz się katalogu -&lt;użytkownika&gt;. database.windows.net serwera, jeśli nie został jeszcze połączony
1. Upewnij się, że masz połączenie z bazą danych jobaccount, a następnie naciśnij klawisz F5, aby uruchomić skrypt.

* sp\_add\_job tworzy nowe zadanie o nazwie „Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885”.
* sp\_add\_jobstep tworzy krok zadania zawierający tekst polecenia T-SQL służącego do aktualizacji indeksu.




## <a name="next-steps"></a>Następne kroki

W tym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]

> * Utworzenie konta zadania do tworzenia zapytań dotyczących wielu dzierżaw
> * Aktualizowanie danych we wszystkich bazach danych dzierżaw
> * Tworzenie indeksu tabeli we wszystkich bazach danych dzierżaw

[Samouczek analitycznych zapytań ad-hoc](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Dodatkowe samouczki, które zależą od wdrożenia aplikacji Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Zarządzanie skalowaną w poziomie bazą danych w chmurze](sql-database-elastic-jobs-overview.md)
* [Tworzenie baz danych skalowanych w poziomie i zarządzanie nimi](sql-database-elastic-jobs-create-and-manage.md)
