---
title: "aaaDeploy i eksplorowanie hello wielodostępne Wingtip SaaS aplikacji, która używa usługi Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Wdrażanie i Eksploruj aplikacji wielodostępnej Wingtip SaaS hello, który demonstruje wzorce SaaS przy użyciu bazy danych SQL Azure."
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
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: 7c528ee19472d3b8c7a285b2f86013945e8f4bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-explore-a-multi-tenant-application-that-uses-azure-sql-database---wingtip-saas"></a>Wdrażanie i Eksploruj aplikacji wielodostępnych, która używa bazy danych SQL Azure - Wingtip SaaS

W tym samouczku wdrażanie i Eksploruj aplikacji Wingtip SaaS hello. Aplikacja Hello używa bazy danych na dzierżawcy, wzorzec aplikacji SaaS, tooservice wielu dzierżawców. Aplikacja Hello jest funkcje zaprojektowane tooshowcase bazy danych SQL Azure, upraszczające Włączanie scenariusze SaaS.

Witaj pięć minut po kliknięciu przycisku *wdrażanie tooAzure* poniższy przycisk, masz wielodostępnych aplikacji SaaS, nawet przy użyciu bazy danych SQL i w chmurze hello. Aplikacja Hello jest wdrażana z trzech dzierżawami próbki, każda z własną bazę danych, wszystkie wdrożone w puli elastycznej SQL. Aplikacja Hello jest wdrożony tooyour subskrypcji platformy Azure, co daje pełny dostęp tooexplore i pracować z hello poszczególnych składników aplikacji. Witaj źródła kodu i zarządzanie skryptów aplikacji są dostępne w repozytorium WingtipSaaS GitHub hello.


Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]

> * Jak toodeploy hello aplikacji Wingtip SaaS
> * Gdzie tooget hello kodu źródłowego aplikacji i skrypty zarządzania
> * O serwerach hello pule adresów i baz danych, które tworzą aplikacji hello
> * Jak dzierżawcy są mapowane tootheir danych za pomocą hello *katalogu*
> * Jak tooprovision nowej dzierżawy
> * Jak toomonitor dzierżawy działania w aplikacji hello

tooexplore różnych SaaS projektowania i zarządzania wzorców, [serii samouczków pokrewne](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials) jest dostępna które zależą od tego pierwszego wdrożenia. Podczas przechodzenia przez hello samouczki, Poznaj skrypty hello pod warunkiem i sprawdź, implementowania hello różnych wzorców SaaS. Krok za pomocą skryptów hello w każdej samouczek toogain lepiej zrozumieć, jak tooimplement hello bazy danych SQL wiele funkcji uprościć tworzenie aplikacji SaaS.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete ukończenia tego samouczka, Utwórz hello się, że następujące wymagania wstępne:

* Zainstalowany jest program Azure PowerShell. Aby uzyskać szczegółowe informacje, zobacz [Rozpoczynanie pracy z programem Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="deploy-hello-wingtip-saas-application"></a>Wdrażanie aplikacji Wingtip SaaS hello

Wdrażanie aplikacji Wingtip SaaS hello:

1. Kliknięcie przycisku hello **wdrażanie tooAzure** przycisk otwiera hello Azure toohello portalu Wingtip SaaS wdrażania szablonu. Szablon Hello wymaga dwóch wartości parametru; Nazwa nowej grupy zasobów i nazwę użytkownika, która odróżnia to wdrożenie od innych wdrożeń aplikacji Wingtip SaaS hello. następnym krokiem Hello szczegółowe informacje dotyczące ustawiania tych wartości.

   Upewnij się, że toonote hello dokładne wartości, które można użyć ponieważ będą potrzebne tooenter je do konfiguracji później pliku.

   <a href="http://aka.ms/deploywtpapp" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

1. Wprowadź wartości wymaganego parametru hello wdrożenia:

    > [!IMPORTANT]
    > Niektóre uwierzytelnienia i zapory serwera są celowo niezabezpieczone w celach demonstracyjnych. **Utwórz nową grupę zasobów**i nie należy używać istniejącej grupy zasobów, serwerami lub pul. Nie należy używać tej aplikacji lub wszystkie zasoby, które tworzy, w środowisku produkcyjnym. Usunąć ten zasób grupy po zakończeniu pracy z toostop aplikacji hello związane z rozliczeniami.

    * **Grupa zasobów** — wybierz tę opcję **Utwórz nowy** i podaj **nazwa** hello grupy zasobów. Wybierz **lokalizacji** z listy rozwijanej hello.
    * **Użytkownik** -niektórych zasobów wymagają nazw, które są globalnie unikatowe. Unikatowość tooensure każdym wdrożeniu aplikacji hello Podaj wartość zasobów toodifferentiate tworzenia, z zasobów tworzone przez każdego innego wdrażania hello Wingtip aplikacji. Zaleca toouse krótki **użytkownika** nazwę, np. z Twoimi inicjałami i numer (na przykład *bg1*) i użyć jej w polu Nazwa grupy zasobów hello (na przykład *wingtip-bg1*). **Użytkownika** parametr może zawierać tylko litery, cyfry i łączniki (bez spacji). Witaj pierwszy i ostatni znak musi być literą lub cyfrą (wszystkie małe jest zalecane).


1. **Wdrażanie aplikacji hello**.

    * Kliknij przycisk tooagree toohello warunki i postanowienia.
    * Kliknij pozycję **Kup**.

1. Monitorowanie stanu wdrożenia, klikając **powiadomienia** (hello ikonę dzwonka prawej strony pola wyszukiwania hello). Wdrażanie aplikacji Wingtip SaaS hello trwa około pięciu minut.

   ![wdrażanie zakończyło się pomyślnie](media/sql-database-saas-tutorial/succeeded.png)

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Pobierz i odblokować hello Wingtip SaaS skryptów

Podczas wdrożenia aplikacji hello Pobierz skrypty zarządzania i kod źródłowy hello.

> [!IMPORTANT]
> Zawartość pliku wykonywalnego (skrypty, biblioteki dll) mogą być blokowane przez system Windows, gdy pliki zip są pobierane z zewnętrznego źródła i wyodrębnione. Podczas wyodrębniania hello skryptów z pliku zip, procedura hello poniżej plik zip hello toounblock przed wyodrębniania. Dzięki temu mogą toorun hello skryptów.

1. Przeglądaj zbyt[repozytorium github Wingtip SaaS hello](https://github.com/Microsoft/WingtipSaaS).
1. Kliknij przycisk **klonowania lub pobierania**.
1. Kliknij przycisk **Pobierz ZIP** i Zapisz plik hello.
1. Kliknij prawym przyciskiem myszy hello **WingtipSaaS master.zip** pliku, a następnie wybierz **właściwości**.
1. Na powitania **ogólne** wybierz opcję **Odblokuj**i kliknij przycisk **Zastosuj**.
1. Kliknij przycisk **OK**.
1. Wyodrębnij pliki hello.

Skrypty znajdują się w hello *... \\Wzorca WingtipSaaS\\modułów uczenia* folderu.

## <a name="update-hello-configuration-file-for-this-deployment"></a>Aktualizuj plik konfiguracji powitania dla tego wdrożenia

Przed uruchomieniem skrypty należy ustawić hello *grupy zasobów* i *użytkownika* wartości w **UserConfig.psm1**. Ustaw wartości toohello, które można ustawić podczas wdrażania tych zmiennych.

1. Otwórz... \\Modułów uczenia\\*UserConfig.psm1* w hello *PowerShell ISE*
1. Aktualizacja *ResourceGroupName* i *nazwa* z określonymi wartościami hello wdrożenia (wierszach 10 i 11 tylko).
1. Zapisz zmiany Witaj!

W tym miejscu to ustawienie po prostu uniemożliwia posiadanie tooupdate te wartości charakterystyczne dla wdrożenia każdego skryptu.

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello

Aplikacja Hello ilustrację miejsc, takich jak koncertowe, jazz klubów sportowy klubów, który obsługiwać zdarzeń. Miejsc Zarejestruj jako klientów (lub dzierżawcy) hello Wingtip platformy, dla zdarzeń toolist łatwe i sprzedawać bilety. Każdy miejsce pobiera toomanage aplikacji sieci web spersonalizowane i wyświetlić ich zdarzenia i sprzedawać bilety, niezależne i odizolowany od pozostałych dzierżawców. W obszarze obejmuje hello każdego dzierżawcy pobiera wdrożonych w puli elastycznej SQL bazy danych SQL.

Centralnego **Centrum zdarzeń** zawiera listę dzierżawy adresów URL tooyour określonego wdrożenia.

1. Otwórz hello _Centrum zdarzeń_ w przeglądarce sieci web: http://events.wtp.&lt; Użytkownik&gt;. trafficmanager.net (Zastąp nazwą użytkownika danego wdrożenia):

    ![centrum zdarzeń](media/sql-database-saas-tutorial/events-hub.png)

1. Kliknij przycisk **Fabrikam Jazz Club** w *Centrum zdarzeń*.

   ![Zdarzenia](./media/sql-database-saas-tutorial/fabrikam.png)


toocontrol hello dystrybucji żądań przychodzących, używa aplikacji hello [ *usługi Azure Traffic Manager*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview). Hello zdarzenia stron, które są specyficzne dla dzierżawy, wymagają nazwy dzierżawy są objęte hello adresów URL. Wszystkie hello dzierżawy adresów URL obejmują konkretnej *użytkownika* wartości i odpowiada temu formatowi: http://events.wtp.&lt; Użytkownik&gt;.trafficmanager.net/*fabrikamjazzclub*. Hello zdarzeń aplikacji hello nazwa dzierżawcy z adresu URL hello analizuje i używający tych informacji toocreate tooaccess klucza, przy użyciu katalogu [ *zarządzania mapy niezależnego fragmentu*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-shard-map-management). mapy katalogu Hello hello toohello klucza dzierżawy lokalizacji bazy danych. Witaj **Centrum zdarzeń** używa rozszerzonych metadanych w nazwie hello katalogu tooretrieve hello dzierżawcy skojarzone z każdym bazy danych tooprovide hello listę adresów URL.

W środowisku produkcyjnym należy zwykle utworzyć rekord CNAME DNS [ *punktu firmowej domeny internetowej* ](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-point-internet-domain) profilu Menedżera ruchu hello.

## <a name="start-generating-load-on-hello-tenant-databases"></a>Rozpocznij generowanie obciążenie hello dzierżawcy z bazy danych

Teraz, gdy hello aplikacja jest wdrażana, umieśćmy go toowork! Witaj *LoadGenerator pokaz* pracą dzierżawy w przypadku wszystkich baz danych uruchamia skrypt programu PowerShell. wiele aplikacji SaaS obciążenie rzeczywistych Hello jest zwykle sporadyczne i nieprzewidywalnych. toosimulate tego rodzaju obciążenia, hello generator tworzy obciążenia dystrybuowana do wszystkich dzierżawców z losowego seria każdego dzierżawcy występujących w losowego odstępach czasu. Ze względu na to, jaki zajmuje kilka minut tooemerge wzorzec obciążenia hello jest najlepszym generator hello toolet uruchamiania dla co najmniej trzech lub czterech minut przed hello monitorowania obciążenia.

1. W hello *PowerShell ISE*, otwórz hello... \\Modułów uczenia\\narzędzia\\*LoadGenerator.ps1 pokaz* skryptu.
1. Naciśnij klawisz **F5** do uruchomienia skryptu hello i uruchamiania hello obciążenia generator (pozostaw hello domyślnych wartości parametrów teraz).

> [!IMPORTANT]
> toorun inne skrypty, Otwórz nowe okno programu PowerShell ISE. generator obciążenia Hello jest uruchomiona jako serię zadań w lokalnej sesji programu PowerShell. Witaj *LoadGenerator.ps1 pokaz* skryptu dotyczącego hello rzeczywiste obciążenie generator skryptu, który jest uruchamiany jako zadanie pierwszego planu oraz szereg zadań generacji obciążenia w tle. Zadanie generator obciążenia jest wywoływana dla każdej bazy danych zarejestrowany w wykazie hello. zadania Hello działają w lokalnej sesji programu PowerShell, więc zamykania sesji programu PowerShell hello zatrzymuje wszystkie zadania. Jeśli zawiesić komputera, generowanie obciążenia został wstrzymany i zostanie wznowiona po wznowieniu komputera.

Po generator obciążenia hello wywołuje obciążenia generacji zadań dla każdego dzierżawcy, zadanie pierwszego planu hello pozostaje w stanie wywoływania zadania, gdzie uruchamiana dodatkowe zadania dla nowi dzierżawcy, które są następnie udostępniane. Można użyć *Ctrl-C* lub naciśnij klawisz hello *zatrzymać* przycisk toostop hello pierwszego planu zadań, ale istniejące tła zadań będzie kontynuować generowania obciążenia w każdej bazie danych. Jeśli konieczne toomonitor i kontrolować hello zadań w tle, użyj *Get-Job*, *Receive-Job* i *zadanie zatrzymania*. Podczas wykonywania hello pierwszego zadania możesz nie Użyj hello tego samego tooexecute sesji programu PowerShell inne skrypty. toorun inne skrypty, Otwórz nowe okno programu PowerShell ISE.

Jeśli chcesz toorestart hello obciążenia generator sesji, na przykład o innych parametrach, można zatrzymać hello pierwszego planu zadań, a następnie ponownie uruchom hello *LoadGenerator.ps1 pokaz* skryptu. Ponowne uruchomienie *LoadGenerator.ps1 pokaz* najpierw zatrzymuje wszelkie uruchomione zadania, a następnie ponowne uruchomienie generator hello dotyczącego nowy zestaw zadań przy użyciu bieżących parametrów hello.

Na razie pozostaw generator obciążenia hello uruchomiony w stanie wywoływania zadania hello.


## <a name="provision-a-new-tenant"></a>Aprowizacja nowej dzierżawy

początkowe wdrożenie Hello tworzy trzy dzierżaw przykładowe, ale Utwórzmy innej dzierżawy toosee jak dotyczy to aplikacji hello wdrożone. Hello dzierżaw inicjowania obsługi administracyjnej Wingtip SaaS przepływu pracy została szczegółowo opisana na powitania [samouczek udostępniania i wykaz](sql-database-saas-tutorial-provision-and-catalog.md). W tym kroku możesz szybko utworzyć nową dzierżawę.

1. Otwórz... \\Modules\Provision uczenie i wykaz\\*ProvisionAndCatalog.ps1 pokaz* w hello *PowerShell ISE*.
1. Naciśnij klawisz **F5** do uruchamiania skryptu hello (pozostaw hello wartości domyślne dla teraz).

   > [!NOTE]
   > Użyj wielu skryptów Wingtip SaaS *$PSScriptRoot* tooallow nawigowanie po funkcji toocall folderów w innych skryptów. Tej zmiennej jest oceniana tylko wtedy, gdy hello skrypt zostanie wykonany przez naciśnięcie przycisku **F5**.  Wyróżnianie i uruchamianie zaznaczenia (**F8**) może powodować błędy, więc naciśnij **F5** podczas uruchamiania skryptów.

Hello nowej dzierżawy w bazie danych jest utworzony w puli elastycznej SQL, zainicjować i zarejestrowanych w wykazie hello. Po pomyślnym zainicjowaniu obsługi administracyjnej, jego sprzedaży biletów hello nowej dzierżawy *zdarzenia* lokacji zostanie wyświetlona w przeglądarce:

![Nowa dzierżawa](./media/sql-database-saas-tutorial/red-maple-racing.png)

Odśwież hello *Centrum zdarzeń* i pojawi się na liście hello hello nowej dzierżawy.


## <a name="explore-hello-servers-pools-and-tenant-databases"></a>Eksploruj hello serwerów, pule i dzierżawy baz danych

Teraz, gdy rozpoczęciu uruchamiania obciążenia hello kolekcję dzierżawców przyjrzymy hello zasobów, które zostały wdrożone:

1. W [portalu Azure](http://portal.azure.com), przeglądanie tooyour lista serwerów SQL i otworzyć **katalogu -&lt;użytkownika&gt;**  serwera. Serwer katalogu Hello zawiera dwie bazy danych. Witaj **tenantcatalog**i hello **basetenantdb** (pusta *złotego* lub szablonu bazy danych, który jest kopiowany toocreate nowi dzierżawcy).

   ![bazy danych](./media/sql-database-saas-tutorial/databases.png)

1. Przejdź wstecz tooyour lista serwerów SQL i otworzyć hello **tenants1 -&lt;użytkownika&gt;**  serwer zawierający hello dzierżawcy z bazy danych. Każda baza danych dzierżawy jest _elastycznej standardowe_ bazy danych w puli standardowej 50 eDTU. Ponadto istnieje _Racing klon czerwony_ bazy danych, bazy danych dzierżawy hello aprowizowanej wcześniej.

   ![serwer](./media/sql-database-saas-tutorial/server.png)

## <a name="monitor-hello-pool"></a>Monitor hello puli

Jeśli hello generator obciążenia uruchomione przez kilka minut, jest za mało danych powinny być dostępne toostart spojrzenie na niektóre hello monitorowania wbudowane pul i baz danych.

1. Przeglądaj serwera toohello **tenants1 -&lt;użytkownika&gt;**i kliknij przycisk **Pool1** do wyświetlania wykorzystania zasobów dla puli hello (generator obciążenia hello został uruchomiony przez godzinę w powitania po wykresów) :

   ![monitorowanie puli](./media/sql-database-saas-tutorial/monitor-pool.png)

Oba wykresy pokazują, jak dobrze elastyczne pule i usługa SQL Database są dostosowane do pracy przy obciążeniu przez aplikacje SaaS. Cztery bazy danych, które są każdego poszerzająca tooas tak, jak łatwo jest obsługiwanych 40 jednostek Edtu w puli 50 eDTU. Jeśli zostały one udostępniane jako autonomiczny baz danych, jak każdy toobe potrzeby S2 (50 DTU) toosupport hello seria. Koszt Hello 4 baz danych S2 autonomiczny są prawie 3 razy hello cen hello puli i hello puli nadal ma szerokie możliwości rozbudowy dużo więcej baz danych. W sytuacjach rzeczywistych klientów bazy danych SQL są aktualnie uruchomione zapasową baz danych too500 w pulach eDTU 200. Aby uzyskać więcej informacji, zobacz hello [samouczek monitorowania wydajności](sql-database-saas-tutorial-performance-monitoring.md).


## <a name="next-steps"></a>Następne kroki

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]

> * Jak toodeploy hello aplikacji Wingtip SaaS
> * O serwerach hello pule adresów i baz danych, które tworzą aplikacji hello
> * Dzierżaw są mapowane tootheir danych za pomocą hello *katalogu*
> * Jak tooprovision nowi dzierżawcy
> * Jak toomonitor wykorzystania puli tooview dzierżawy działania
> * Jak toodelete przykładowych zasobów toostop dotyczące rozliczeń

Teraz spróbuj hello [samouczek udostępniania i katalogu](sql-database-saas-tutorial-provision-and-catalog.md)



## <a name="additional-resources"></a>Dodatkowe zasoby

* Dodatkowe [aplikacji Wingtip SaaS hello samouczków, z którymi kompilacji na](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* toolearn o pule elastyczne, zobacz [ *co to jest puli elastycznej Azure SQL*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)
* Zobacz toolearn o zadania elastyczne [ *Zarządzanie baz danych z chmury skalowalnych w poziomie*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)
* toolearn o wielodostępnych aplikacji SaaS, zobacz [ *projektowania wzorce dla wielodostępnych aplikacji SaaS*](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)
