---
title: "aaaRestore bazy danych Azure SQL w aplikacji wielodostępnych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toorestore pojedynczej dzierżawy SQL bazy danych po przypadkowym usunięciu danych"
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
ms.date: 05/10/2017
ms.author: billgib;sstein
ms.openlocfilehash: 8507ecec2424c135f1859b88ebf2bb4e17538a58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a>Przywracanie bazy danych SQL dzierżaw Wingtip SaaS

Aplikacja Wingtip SaaS Hello jest utworzony przy użyciu modelu bazy danych dla dzierżawy, którym każdy dzierżawca ma własnych bazy danych. Jedną z zalet hello ten model jest jego jest łatwe toorestore danych pojedynczej dzierżawy w izolacji bez wpływu na innych dzierżawców.

W tym samouczku Dowiedz się dwa wzorce odzyskiwania danych:

> [!div class="checklist"]

> * Przywróć bazę danych do bazy danych równoległej (side-by-side)
> * Przywracanie bazy danych w miejscu


|||
|:--|:--|
| **Przywróć dzierżawy tooa wcześniejszego punktu w czasie do równoległego bazy danych** | Ten wzorzec może być używany przez dzierżawcę hello w recenzji, inspekcji, zgodności, oryginalnej bazy danych itp. hello pozostaje bez zmian i online. |
| **Przywróć dzierżawy w miejscu** | Ten wzorzec jest najczęściej używanymi toorecover dzierżawy tooa wcześniejszego punktu w czasie, po dzierżawcy przypadkowo usunął danych. Hello oryginalnej bazy danych jest przełączona w tryb offline i zastąpione hello przywróconej bazy danych. |
|||

toocomplete ukończenia tego samouczka, Utwórz hello się, że następujące wymagania wstępne:

* Aplikacja Wingtip SaaS Hello jest wdrażana. Zobacz toodeploy w mniej niż pięć minut [wdrażania i aplikacji Wingtip SaaS hello](sql-database-saas-tutorial.md)
* Zainstalowany jest program Azure PowerShell. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z programem Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toohello-saas-tenant-restore-pattern"></a>Wprowadzenie toohello SaaS dzierżawy przywracania wzorca

Dla dzierżawcy hello przywrócić wzorzec, istnieją dwa proste wzorce w celu przywrócenia danych dzierżawy usługi. Ponieważ dzierżawy baz danych są od siebie odizolowane, Przywracanie jednego dzierżawcy nie ma wpływu na dane żadnych innych dzierżawców.

We wzorcu pierwszy hello dane są przywracane do nowej bazy danych. dzierżawy Hello następnie otrzymuje baz danych programu access toothis obok ich danych produkcyjnych. Ten wzorzec umożliwia dzierżawcy admin tooreview hello przywrócić danych i potencjalnie przy jego użyciu tooselectively zastąpić bieżące wartości danych. Jest zapasowej toohello SaaS aplikacji projektanta toodetermine jak zaawansowane hello odzyskiwania danych, który powinien być opcje. Po prostu stanie tooreview danych w stanie hello, który znajdował się w danym punkcie w czasie może być wszystkie, który jest wymagany w niektórych scenariuszach. Jeśli baza danych hello używa [— replikacja geograficzna](sql-database-geo-replication-overview.md), zaleca się kopiowanie danych hello wymagane z kopii hello przywrócone do hello oryginalnej bazy danych. Jeśli zastąpić oryginalnej bazy danych hello hello przywrócić bazy danych, należy tooreconfigure go i ponownie zsynchronizować replikację geograficzną.

We wzorcu drugi hello, który tej dzierżawy hello poniosła utratę lub uszkodzenie danych przyjmuje się, że dzierżawy hello w produkcyjnej bazie danych jest przywracany tooa wcześniejszego punktu w czasie. W ramach operacji przywracania hello we wzorcu miejsce hello dzierżawy do trybu offline przez krótki czas podczas hello baza danych jest przywracane i przywrócony do trybu online. Witaj oryginalnej bazy danych zostanie usunięty, ale nadal można przywrócić z, jeśli potrzebujesz tooan wstecz toogo nawet wcześniejszego punktu w czasie. Odmianą tego wzorca można zmienić nazwy bazy danych hello zamiast usuwania, mimo że zmiana nazwy bazy danych hello oferuje nie dodatkowych zalet pod względem zabezpieczeń danych.

## <a name="get-hello-wingtip-application-scripts"></a>Pobierz skrypty aplikacji hello Wingtip

Witaj Wingtip SaaS skrypty i kod źródłowy aplikacji są dostępne w hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repozytorium github. [Kroki skrypty Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="simulate-a-tenant-accidentally-deleting-data"></a>Symulowanie dzierżawcy przypadkowego usunięcia danych

toodemonstrate tych scenariuszy odzyskiwania potrzebujemy zbyt*przypadkowo* usuwać niektóre dane w jednej z baz danych dzierżawy hello. Podczas można usunąć rekordu, hello następny krok konfiguruje toonot pokaz hello zablokowane przez naruszenie integralności referencyjnej! Dodane również pewne dane zakupu biletu, można użyć w dalszej części hello *samouczki Wingtip SaaS Analytics*.

Uruchom skrypt generator biletu hello i utworzyć dodatkowe dane. generator biletu Hello celowo nie kupuje biletów dla poszczególnych dzierżawców ostatniego zdarzenia.

1. Otwórz... \\Modułów uczenia\\narzędzia\\*TicketGenerator.ps1 pokaz* w hello *PowerShell ISE*
1. Naciśnij klawisz **F5** toorun hello skryptu i generowanie odbiorców i biletu danych sprzedaży.


### <a name="open-hello-events-app-tooreview-hello-current-events"></a>Otwórz hello zdarzeń aplikacji tooreview hello bieżącego zdarzeń

1. Otwórz hello *Centrum zdarzeń* (http://events.wtp.&lt; Użytkownik&gt;. trafficmanager.net) i kliknij przycisk **Hall porozumieniu Contoso**:

   ![centrum zdarzeń](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. Przewiń listę hello zdarzeń i zanotuj hello ostatnie zdarzenie na liście hello:

   ![Ostatnie zdarzenie](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-hello-demo-scenario-tooaccidentally-delete-hello-last-event"></a>Uruchom hello pokaz scenariusza tooaccidentally delete hello ostatniego zdarzenia

1. Otwórz... \\Modułów uczenia\\ciągłość prowadzenia działalności biznesowej i odzyskiwania po awarii\\RestoreTenant\\*RestoreTenant.ps1 pokaz* w hello *PowerShell ISE*, i hello ustaw następujące wartości:
   * **$DemoScenario** = **1**zbyt ustaw**1** -Usuń zdarzenia bez sprzedaży biletów.
1. Naciśnij klawisz **F5** toorun hello skryptu i usunąć hello ostatnie zdarzenie. Powinny pojawić się potwierdzenie komunikat podobny toohello następujące czynności:

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. zostanie otwarta strona zdarzenia Contoso Hello. Przewiń w dół i sprawdź, czy zdarzenie hello został usunięty. Jeśli zdarzenie hello jest nadal znajduje się na liście hello, kliknij przycisk Odśwież i sprawdź, czy został on usunięty.

   ![Ostatnie zdarzenie](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-hello-production-database"></a>Przywróć bazę danych dzierżawy równolegle z hello w produkcyjnej bazie danych

Tego ćwiczenia przywraca hello Hall porozumieniu Contoso bazy danych tooa punktu w czasie przed hello zdarzenie zostało usunięte. Po usunięciu zdarzenia hello w poprzednich krokach hello mają toorecover i wyświetlić dane hello usunięte. Nie ma potrzeby toorestore produkcyjnej bazy danych za pomocą hello usunąć rekord, ale należy toorecover hello stare bazy danych tooaccess hello stare dane z innych powodów biznesowych.

 Witaj *TenantInParallel.ps1 przywracania* skrypt tworzy równoległych dzierżawy bazy danych i równoległych wpisu katalogu zarówno o nazwie *ContosoConcertHall\_starego*. Ten wzorzec przywracania jest najodpowiedniejsze do odzyskiwania danych po utracie danych drobne lub zgodności i inspekcji scenariuszy odzyskiwania. Jest również zalecane podejście, gdy używasz hello [— replikacja geograficzna](sql-database-geo-replication-overview.md).

1. Zakończenie hello [symulować użytkownika przypadkowego usunięcia danych](#simulate-a-tenant-accidentally-deleting-data) sekcji.
1. Otwórz... \\Modułów uczenia\\ciągłość prowadzenia działalności biznesowej i odzyskiwania po awarii\\RestoreTenant\\_RestoreTenant.ps1 pokaz_ w hello *PowerShell ISE*.
1. Ustaw **$DemoScenario** = **2**, ustaw tę wartość za**2** za*dzierżawy przywracania równolegle*.
1. Naciśnij klawisz **F5** toorun hello skryptu.

skrypt Hello przywraca hello dzierżawy bazy danych (bazy danych równoległych tooa) tooa punktu w czasie, aby usunąć zdarzenie hello w poprzedniej sekcji hello. Tworzy drugi bazę danych, spowoduje usunięcie wszystkich istniejących metadanych katalogu, które istnieje w tej bazie danych i dodaje hello katalogu toohello bazy danych w obszarze hello *ContosoConcertHall\_starego* wpisu.

Witaj pokaz skryptu spowoduje otwarcie strony zdarzenia hello w przeglądarce. Uwaga z adresu URL hello: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` czy to jest wyświetlane dane z bazy danych hello przywrócić gdzie *_old* dodaniu toohello nazwy.

Hello przewijania zdarzenia wymienione w hello tooconfirm przeglądarki, które hello zdarzeń usunięte w poprzedniej sekcji hello została przywrócona.

Należy zwrócić uwagę tego uwidaczniającą dzierżawy hello przywrócić dodatkowe dzierżawy, z własnego biletów toobrowse zdarzeń aplikacji jest mało prawdopodobne toobe, w jaki będzie zapewnia się, że dane toorestored dostępu dzierżawy, ale służy tooeasily ilustrują hello przywracania wzorzec.

W rzeczywistości ma prawdopodobnie tylko zachowanie tej przywróconej bazy danych w zdefiniowanym okresie. Możesz usunąć wpis dzierżawy hello przywrócić po zakończeniu przez wywołanie hello *RestoredTenant.ps1 Usuń* skryptu.

1. Ustaw **$DemoScenario** za**4** tooselect hello *dzierżawy Usuń przywrócić* scenariusza.
1. **Wykonanie** **przy użyciu** **F5**
1. Witaj *ContosoConcertHall\_starego* wpis jest teraz usunięty z katalogu hello. Przejdź dalej i zamknij hello wydarzenia strony dla tej dzierżawy w przeglądarce.


## <a name="restore-a-tenant-in-place-replacing-hello-existing-tenant-database"></a>Przywróć dzierżawcy w miejscu, zastępując hello istniejącej dzierżawy bazy danych

Tego ćwiczenia przywraca hello Hall porozumieniu Contoso dzierżawy tooa punktu w czasie przed hello zdarzenie zostało usunięte. Witaj *TenantInPlace przywracania* skryptu przywrócenie hello bieżącej dzierżawy bazy danych tooa nową bazę danych wskazujące tooa wcześniejszego punktu w czasie i usuwa hello oryginalnej bazy danych. Ten wzorzec przywracania jest najodpowiedniejsze, odzyskiwanie danych poważne uszkodzenie jako może być utracie dużej ilości danych, które hello dzierżawy może mieć tooaccommodate.

1. Otwórz **RestoreTenant.ps1 pokaz** pliku w programie PowerShell ISE
1. Ustaw **$DemoScenario** za**5** tooselect hello *przywrócić dzierżawy w scenariuszu miejscu*.
1. Wykonywanie za pomocą **F5**.

skrypt Hello przywraca punktu tooa bazy danych dzierżawy hello pięć minut przed hello zdarzenie zostało usunięte. Robi to przy pierwszym biorąc hello Contoso porozumieniu Hall dzierżawy w trybie offline więc nie wyszukiwanie aktualizacji toohello danych. Następnie równoległych bazy danych jest tworzone przez przywrócenie z punktu przywracania hello i o nazwie z sygnaturą czasową Nazwa bazy danych hello tooensure nie powoduje konfliktu z hello nazwy istniejącej bazy danych dzierżawy. Następnie hello starego dzierżawcy w bazie danych zostanie usunięta, a hello przywróconej bazy danych jest toohello zmieniono nazwę oryginalną nazwę bazy danych. Na koniec Hall porozumieniu Contoso jest przełączana w tryb online tooallow hello aplikacji dostępu toohello przywrócić do bazy danych.

Pomyślnie przywrócił się hello bazy danych tooa punktu w czasie przed hello zdarzenie zostało usunięte. Witaj zostanie otwarta strona zdarzeń, upewnij się, więc hello ostatnie zdarzenie zostało przywrócone.


## <a name="next-steps"></a>Następne kroki

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]

> * Przywróć bazę danych do bazy danych równoległej (side-by-side)
> * Przywracanie bazy danych w miejscu

[Zarządzanie dzierżawy schematu bazy danych](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a>Dodatkowe zasoby

* Dodatkowe [samouczki, które zależą od hello aplikacji Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Omówienie ciągłości działalności biznesowej z bazy danych SQL Azure](sql-database-business-continuity.md)
* [Więcej informacji na temat tworzenia kopii zapasowych bazy danych SQL](sql-database-automated-backups.md)
