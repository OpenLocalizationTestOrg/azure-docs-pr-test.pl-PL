---
title: "aaaProvision nowych dzierżaw w aplikacji wielodostępnych, który używa usługi Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprovision i wykaz nowej dzierżawy w hello aplikacji Wingtip SaaS"
keywords: "samouczek usługi sql database"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: sstein
ms.openlocfilehash: eb26f523305650c2124e36707d187dfcdad06fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-new-tenants-and-register-them-in-hello-catalog"></a>Udostępnić nowi dzierżawcy i zarejestruj je w katalogu hello

W tym samouczku informacje o hello udostępniania i wzorce SaaS katalogu i ich implementacji w hello aplikacji Wingtip SaaS. Tworzenie i zainicjować nowe dzierżawy bazy danych oraz zarejestrować je w katalogu dzierżawcy hello aplikacji. katalog Hello to bazy danych, która przechowuje hello mapowanie między swoich danych i aplikacji SaaS hello wiele dzierżaw. wykaz Hello odgrywa ważną rolę w kierowanie aplikacji żądań toohello poprawną bazą danych.  

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]

> * Udostępnianie jednej nowej dzierżawy, tym krokowe to implementowania
> * Aprowizowanie partii dodatkowych dzierżaw


toocomplete ukończenia tego samouczka, Utwórz hello się, że następujące wymagania wstępne:

* Aplikacja Wingtip SaaS Hello jest wdrażana. Zobacz toodeploy w mniej niż pięć minut [wdrażania i aplikacji Wingtip SaaS hello](sql-database-saas-tutorial.md)
* Zainstalowany jest program Azure PowerShell. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z programem Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toohello-saas-catalog-pattern"></a>Wprowadzenie toohello wzorzec katalogu SaaS

Kopie bazy danych wielodostępnych aplikacji SaaS jest ważne tooknow, w którym przechowywane są informacje dla każdego dzierżawcy. We wzorcu katalogu SaaS hello katalog bazy danych jest używane toohold hello mapowanie między każdego dzierżawcy i gdzie są przechowywane ich dane. Aplikacja Wingtip SaaS Hello używa pojedynczego dzierżawcy na Architektura bazy danych, ale hello podstawowy wzorzec przechowywania mapowania dzierżawcy w bazie danych w katalogu ma zastosowanie, czy ma być używana w wielu dzierżawców lub pojedynczej dzierżawy bazy danych.

Każdej dzierżawy jest przypisywana klucz identyfikujący je w katalogu hello, który jest mapowany toohello lokalizacji hello odpowiednie bazy danych. W aplikacji Wingtip SaaS hello klucza hello powstała z wyznaczania wartości skrótu o nazwie hello dzierżawy. Dzięki temu hello dzierżawy część nazwy toobe adres URL aplikacji hello używanych tooconstruct hello klucza. Można użyć innych systemów klucza dzierżawy.  

wykaz Hello umożliwia hello nazwę lub lokalizację hello toobe bazy danych, zmienić przy minimalnym wpływie na powitania aplikacji.  W modelu wielodostępnym bazy danych to również bierze pod uwagę "przenoszenia" dzierżawa między bazami danych.  Hello katalogu mogą być również używane tooindicate, czy dzierżawcy lub baza danych jest w trybie offline z powodu konserwacji lub innych działań. Jest to przedstawione w hello [Przywracanie pojedynczej dzierżawy samouczek](sql-database-saas-tutorial-restore-single-tenant.md).

Ponadto hello katalog, który jest włączone zarządzanie bazy danych dla aplikacji SaaS, można przechowywać dodatkowe metadane dzierżawy lub bazy danych, takich jak hello warstwy lub wersja bazy danych, wersji schematu, plan usługi lub umów SLA oferowanych tootenants i innych informacji o który Umożliwia zarządzanie aplikacjami, dział obsługi klienta lub procesów opracowywania oprogramowania.  

Poza hello aplikacji SaaS hello katalogu można włączyć narzędzi bazy danych.  W przykładzie Wingtip SaaS hello katalogu hello jest używane tooenable dzierżawy między zapytania, przedstawione w hello [samouczek analizy ad hoc](sql-database-saas-tutorial-adhoc-analytics.md). Zarządzanie zadaniami między bazami danych jest przedstawione w hello [Zarządzanie schematami](sql-database-saas-tutorial-schema-management.md) i [dzierżawy analytics](sql-database-saas-tutorial-tenant-analytics.md) samouczki. 

W aplikacji Wingtip SaaS hello katalogu hello jest implementowane za pomocą funkcji zarządzania niezależnego fragmentu hello hello [elastycznej bazy danych klienta biblioteki (EDCL)](sql-database-elastic-database-client-library.md). Witaj EDCL umożliwia toocreate aplikacji, zarządzanie i użyć mapy niezależnych kopii bazy danych. Mapy niezależnego fragmentu zawiera listę odłamków (bazy danych) i hello mapowanie między kluczy (dzierżawcami) i baz danych.  Funkcje EDCL mogą być używane z aplikacji i skryptów programu PowerShell podczas inicjowania obsługi administracyjnej toocreate hello wpisów w mapie niezależnego fragmentu hello dzierżawy i z aplikacji tooefficiently połączyć toohello poprawną bazą danych. EDCL buforuje połączenia informacji toominimize hello ruchu toohello katalogu bazy danych i poprawę szybkości działania aplikacji hello.  

> [!IMPORTANT]
> dane mapowania Hello jest dostępny w bazie danych katalogu hello, ale *nie go edytować*! Dane mapowania można edytować wyłącznie za pomocą interfejsu API biblioteki klienckiej Elastic Database. Bezpośrednie manipulowanie danych mapowania hello ryzyko uszkodzenia hello wykazu i nie jest obsługiwany.


## <a name="introduction-toohello-saas-provisioning-pattern"></a>Wzorzec SaaS inicjowania obsługi administracyjnej toohello wprowadzenie

Podczas przechodzenia do nowego dzierżawcy w aplikacji SaaS, która używa modelu bazy danych z pojedynczej dzierżawy nową bazę danych dzierżawcy należy udostępnić.  Muszą być tworzone w hello odpowiednią lokalizację i warstwy usług, zainicjować przy użyciu odpowiedniego schematu i danych referencyjnych, a następnie rejestrowane w katalogu hello klucza dzierżawy odpowiednie hello.  

Różne podejścia mogą być używane toodatabase inicjowania obsługi, które mogą obejmować wykonywanie skryptów SQL, wdrażanie pliku bacpac lub kopiowania bazy danych "złotego" szablonu.  

Witaj inicjowania obsługi administracyjnej podejście, którego używasz musi comprehended w strategii zarządzania ogólny schemat, który musi zapewnić, że nowych baz danych są udostępniane z hello najnowsze schematu.  Jest to przedstawione w hello [Samouczek zarządzania schematu](sql-database-saas-tutorial-schema-management.md).  

Witaj Wingtip SaaS aplikacji przepisy nowi dzierżawcy przez skopiowanie złotego bazy danych o nazwie basetenantdb wdrożone na serwerze wykazu hello.  Inicjowanie obsługi administracyjnej można zintegrowana aplikacja hello jako część środowisko tworzenia konta, i/lub być obsługiwane w trybie offline za pomocą skryptów. W tym samouczku może zapoznać się inicjowanie obsługi przy użyciu programu PowerShell. skrypty inicjowania obsługi administracyjnej Hello skopiuj toocreate basetenantdb hello nowej dzierżawy bazy danych w puli elastycznej, a następnie go zainicjować z użyciem informacji specyficznych dla dzierżawy i zarejestrować ją w hello katalogu niezależnych mapy.  W hello przykładowej aplikacji, baz danych są podane nazwy na podstawie nazwy dzierżawy hello, ale nie jest krytyczną częścią wzorzec hello — hello katalogu hello umożliwiają dowolnej nazwy bazy danych toohello toobe przypisane. + 


## <a name="get-hello-wingtip-application-scripts"></a>Pobierz skrypty aplikacji hello Wingtip

Witaj Wingtip SaaS skrypty i kod źródłowy aplikacji są dostępne w hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repozytorium github. [Kroki skrypty Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).


## <a name="provision-and-catalog-detailed-walkthrough"></a>Szczegółowy przewodnik po aprowizacji i wykazie

toounderstand jak hello Wingtip aplikacji implementuje nowej dzierżawy inicjowania obsługi, Dodaj punkt przerwania i krok za pomocą przepływu pracy hello podczas inicjowania obsługi administracyjnej dzierżawcy:

1. Otwórz... \\Modułów uczenia\\ProvisionAndCatalog\\_ProvisionAndCatalog.ps1 pokaz_ i hello ustaw następujące parametry:
   * **$TenantName** = nazwa hello nowe miejsce hello (na przykład *niebieskie Bushwillow*).
   * **$VenueType** = jednego z typów wstępnie zdefiniowanych miejscową hello: *niebieskie*, classicalmusic, tańca, jazz, judo, motorracing uniwersalne, opera, rockmusic, nożną.
   * **$DemoScenario** = **1**zbyt ustaw**1** za*udostępnić pojedynczej dzierżawy*.

1. Dodaj punkt przerwania umieszczając kursor dowolne miejsce w 48, hello wiersz informacją: *nowej dzierżawy "*i naciśnij klawisz **F9**.

   ![punkt przerwania](media/sql-database-saas-tutorial-provision-and-catalog/breakpoint.png)

1. Naciśnij klawisz skryptu hello toorun **F5**.

1. Po zatrzymaniu wykonywania skryptu hello na powitania punkt przerwania, naciśnij klawisz **F11** toostep hello kodu.

   ![punkt przerwania](media/sql-database-saas-tutorial-provision-and-catalog/debug.png)



Wykonanie skryptu hello hello śledzenia **debugowania** menu Opcje - **F10** i **F11** toostep za pośrednictwem lub hello wywołuje funkcje. Aby uzyskać więcej informacji na temat debugowania skryptów programu PowerShell, zobacz [porady dotyczące pracy z i debugowania skryptów programu PowerShell](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise).


następujące Hello nie są tooexplicitly wykonaj kroki, ale wyjaśnienie przepływu pracy hello krokowo podczas debugowania skryptu hello:

1. **Importuj hello SubscriptionManagement.psm1** moduł, który zawiera funkcje logowania tooAzure i wyboru hello pracy z subskrypcją platformy Azure.
1. **Importuj hello CatalogAndDatabaseManagement.psm1** moduł, który udostępnia katalog i poziomie dzierżawy abstrakcji za pośrednictwem hello [zarządzania niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md) funkcji. Jest to ważne moduł, który hermetyzuje znacznie hello katalogu wzorca i warto eksploracji.
1. **Uzyskaj szczegółowe informacje o konfiguracji**. Wkrocz Get-konfiguracji (z F11) i zobacz, jak określono hello konfiguracji aplikacji. Nazwy zasobów i inne wartości specyficzny dla aplikacji są zdefiniowane w tym miejscu, ale nie należy zmieniać tych wartości do momentu znasz hello skryptów.
1. **Pobierz obiekt katalogu hello**. Krok do katalogu Get, która Redaguj i zwraca obiekt katalogu, który jest używany w skrypcie wyższego poziomu hello.  Ta funkcja korzysta z funkcji zarządzania niezależnego fragmentu, które są importowane z **AzureShardManagement.psm1**. obiekt katalogu Hello składa się z następujących hello:
   * $catalogServerFullyQualifiedName jest tworzony przy użyciu standardowych stem hello oraz nazwę użytkownika: _katalogu -\<użytkownika\>. database.windows.net_.
   * $catalogDatabaseName są pobierane z konfiguracji hello: *tenantcatalog*.
   * Obiekt $shardMapManager został zainicjowany z bazy danych katalogu hello.
   * Obiekt $shardMap został zainicjowany z hello *tenantcatalog* mapy niezależnego fragmentu w hello katalogu w bazie danych.
   Obiekcie wykazu jest złożony i zwrócił i używany w hello skryptu wyższego poziomu.
1. **Oblicz hello nowego klucza dzierżawy**. Funkcja wyznaczania wartości skrótu jest klucz dzierżawy hello używane toocreate hello nazwa dzierżawcy.
1. **Sprawdź, czy klucz dzierżawy hello już istnieje**. wykaz Hello jest wyewidencjonowywany tooensure hello klucz jest dostępny.
1. **Witaj dzierżawcy z bazy danych jest udostępniane z TenantDatabase nowy.** Użyj **F11** toostep w i zobacz, jak baza danych hello jest udostępnione za pomocą [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).

Nazwa bazy danych Hello jest tworzony z hello dzierżawy nazwa toomake go wyczyścić niezależnych, które należy toowhich dzierżawy. (Inne strategie nazewnictwa bazy danych może być wykorzystane.) + Szablon Menedżera zasobów jest używane toocreate dzierżawy bazy danych przez skopiowanie złotego bazy danych (baseTenantDB) na serwerze wykazu hello. O innym podejściu może być toocreate pustej bazy danych, a następnie Zainicjuj go przez zaimportowanie pliku bacpac lub tooexecute skrypt inicjacji z dobrze znanej lokalizacji.  

Szablon usługi Resource Manager Hello znajduje się w folderze Modules\Common\ ...\Learning hello: *tenantdatabasecopytemplate.json*

Po utworzeniu bazy danych dzierżawy hello jest następnie dalsze **zainicjowany przy użyciu hello miejscową (dzierżawcy) nazwę i typ miejscową hello**. Można również stosować inne metody inicjowania.

Witaj **dzierżawy bazy danych jest zarejestrowany w wykazie hello** z *TenantDatabaseToCatalog Dodaj* przy użyciu klucza dzierżawy hello. Użyj **F11** toostep hello uzyskać szczegółowe informacje:

* Baza danych katalogu Hello jest dodawana toohello mapy niezależnego fragmentu (hello listę znanych baz danych).
* Mapowanie niezależnych toohello tego łącza hello wartość klucza Hello jest tworzony.
* Dodatkowe dane meta (nazwa miejscową hello) dotyczące dzierżawy hello jest dodawany toohello dzierżaw tabeli w katalogu hello.  Witaj dzierżaw tabeli nie jest częścią hello ShardManagement schematu i nie jest instalowany przez hello EDCL.  W tej tabeli przedstawiono, jak baza danych katalogu hello można rozszerzyć toosupport dodatkowe dane specyficzne dla aplikacji.   


Po zakończeniu inicjowania obsługi administracyjnej wykonywania zwraca toohello oryginalnego *ProvisionAndCatalog pokaz* skryptu, który otwiera hello **zdarzenia** strony dla nowej dzierżawy hello w przeglądarce hello:

   ![zdarzenia](media/sql-database-saas-tutorial-provision-and-catalog/new-tenant.png)


## <a name="provision-a-batch-of-tenants"></a>Zainicjuj obsługę partii dzierżawcy

Tego ćwiczenia inicjuje partii 17 dzierżaw. Zaleca się, że udostępnieniem tej partii dzierżaw przed rozpoczęciem samouczków Wingtip SaaS, więc ma więcej niż kilka toowork baz danych z.

1. Otwórz... \\Modułów uczenia\\ProvisionAndCatalog\\*ProvisionAndCatalog.ps1 pokaz* w hello *PowerShell ISE* i zmień hello *$ DemoScenario* too3 parametru:
   * **$DemoScenario** = **3**, zmień zbyt**3** za*udostępnić partii dzierżaw*.
1. Naciśnij klawisz **F5** i uruchom skrypt hello.

skrypt Hello wdraża partii dodatkowi dzierżawcy. Używa [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md) steruje hello partii i następnie deleguje inicjowania obsługi każdego szablonu połączonego tooa bazy danych. Za pomocą szablonów w ten sposób umożliwia inicjowanie obsługi procesów dla skryptu hello toobroker usługi Azure Resource Manager. Szablony udostępniania bazy danych równolegle, gdzie można i obsługuje ponownych prób w razie potrzeby optymalizacji hello ogólny proces. Witaj skryptu jest idempotentności więc jeśli nie powiedzie się lub zatrzymuje się z jakiegokolwiek powodu, uruchom go ponownie.

### <a name="verify-hello-batch-of-tenants-successfully-deployed"></a>Sprawdź hello partii dzierżaw pomyślnie wdrożona

* Otwórz hello *tenants1* serwer, przechodząc tooyour listę serwerów w hello [portalu Azure](https://portal.azure.com), kliknij przycisk **baz danych**i sprawdź partii hello 17 dodatkowych baz danych są teraz na liście hello:

   ![lista baz danych](media/sql-database-saas-tutorial-provision-and-catalog/database-list.png)



## <a name="other-provisioning-patterns"></a>Inne wzorce aprowizacji

Inne wzorce aprowizacji, których nie uwzględniono w tym samouczku, obejmują:

**Wstępne aprowizowanie baz danych.** Hello wstępnego inicjowania obsługi administracyjnej wzorzec wykorzystuje hello fakt, że bazy danych w puli elastycznej nie należy dodawać z żadnymi dodatkowymi kosztami. Rozliczenia jest przeznaczony dla puli elastycznej hello nie hello baz danych i baz danych w stanie bezczynności korzystać z żadnych zasobów. Wstępne inicjowanie obsługi baz danych w puli i przydzielanie je w razie potrzeby, można znacznie zmniejszyć czasu dołączenia do dzierżawy. Hello liczba baz danych wstępnie tworzyć można dostosować do własnych tookeep wymagane odpowiednie dla hello buforu zakładano inicjowania obsługi administracyjnej szybkości.

**Automatyczne aprowizowanie.** We wzorcu automatycznego inicjowania obsługi administracyjnej hello dedykowanych usługa inicjowania obsługi administracyjnej jest tooprovision używanych serwerów, pul i baz danych automatycznie w razie potrzeby — tym wstępnego inicjowania obsługi administracyjnej baz danych w pule elastyczne, w razie potrzeby. A jeśli bazy danych są zlecone wyłączyć i usunąć, luk w pule elastyczne może zostać wypełniony przez hello świadczenie usługi zgodnie z potrzebami. Takie usługi może być prostymi lub złożonymi — na przykład obsługa inicjowania obsługi administracyjnej na wielu różnych obszarach geograficznych i można skonfigurować replikację geograficzną automatycznie Jeśli tej strategii jest używana dla odzyskiwania po awarii. Z wzorcem automatycznego inicjowania obsługi administracyjnej hello aplikacji klienckiej lub skryptu czy przesłać inicjowania obsługi administracyjnej toobe kolejki tooa żądania, na przetworzonych przez program hello inicjowania obsługi usługi, a następnie będzie sondować hello usługi toodetermine ukończenia. Jeśli używana jest wstępnie inicjowania obsługi, żądania może szybko obsługiwane z usługą hello Zarządzanie inicjowania obsługi administracyjnej zastąpienia bazy danych działa w tle hello.



## <a name="next-steps"></a>Następne kroki

W tym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]

> * Aprowizowanie pojedynczej nowej dzierżawy
> * Aprowizowanie partii dodatkowych dzierżaw
> * Krok do szczegółów hello udostępnianie dzierżaw i rejestrowania ich do katalogu hello

Spróbuj hello [samouczek monitorowania wydajności](sql-database-saas-tutorial-performance-monitoring.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* Dodatkowe [samouczki, które zależą od hello aplikacji Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Biblioteka kliencka Elastic Database](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-database-client-library)
* [Jak tooDebug skrypty w środowisku Windows PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise)
