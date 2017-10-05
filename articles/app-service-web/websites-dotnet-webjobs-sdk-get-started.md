---
title: "Utwórz zadanie WebJob platformy .NET w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Utwórz aplikację wielowarstwową przy użyciu platformy ASP.NET MVC i platformy Azure. Fronton jest uruchamiany w aplikacji sieci web w usłudze Azure App Service i Wstecz działa zakończenia jako zadanie WebJob. Aplikacja korzysta z programu Entity Framework, bazy danych SQL i kolejek usługi Azure storage i obiektów blob."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: a20b13058caecff75af14957468f20e63a3325c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>Tworzenie zadania WebJob .NET w usłudze Azure App Service
Ten samouczek pokazuje, jak napisać kod dla prostą aplikację ASP.NET MVC 5 wielowarstwowej, która używa [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md).

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Celem [zestaw SDK zadań Webjob](websites-webjobs-resources.md) jest uprościć kod zapisu typowych zadań, które mogą wykonywać zadanie WebJob, takich jak przetwarzania obrazu, przetwarzanie kolejki, agregacja danych RSS, plików obsługi i wysyłania wiadomości e-mail. Zestaw SDK zadań Webjob ma wbudowane funkcje do pracy z usługą Azure Storage i usługi Service Bus, planowanie zadań i obsługa błędów i wielu innych typowych scenariuszy. Ponadto ona ma być rozszerzony, a istnieje [repozytorium typu open source dla rozszerzeń](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Przykładowa aplikacja to reklamowa Tablica ogłoszeń. Użytkownicy można przekazywać obrazy dla reklam i procesu zaplecza konwertuje obrazy miniatur. Na stronie listy ad miniatury, a na stronie Szczegóły ad pokazuje obrazu w pełnym rozmiarze. Poniżej przedstawiono zrzut ekranu:

![Lista reklam](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

Ta przykładowa aplikacja działa z [kolejek Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) i [obiekty BLOB platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage). Samouczek pokazuje, jak wdrożyć aplikację na [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) i [bazy danych SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).

## <a id="prerequisites"></a>Wymagania wstępne
W tym samouczku założono, że wiesz, jak pracować z [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projekty w programie Visual Studio.

Samouczek pierwotnie sformatowano dla programu Visual Studio 2013, ale może być używany z nowszej wersji programu Visual Studio. Jeśli używasz programu Visual Studio 2015 lub 2017, zwróć uwagę, że przed uruchomieniem aplikacji lokalnie, należy zmienić `Data Source` część ciągu połączenia bazy danych LocalDB programu SQL Server w plikach Web.config i App.config z `Data Source=(localdb)\v11.0` do `Data Source=(LocalDb)\MSSQLLocalDB`.

> [!NOTE]
> <a name="note"></a>Musi mieć konto platformy Azure do ukończenia tego samouczka:
>
> * Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): otrzymasz kredyt, że można użyć do wypróbowania płatnych usług Azure, a nawet po wyczerpaniu, można zachować konto i korzystać z bezpłatnych usług platformy Azure, takich jak witryny sieci Web. Karta kredytowa nie zostanie obciążona, chyba że jawnie zmienisz ustawienia i poprosisz o jej obciążenie.
> * Możesz [aktywowania Azure miesięczne środki dla subskrybentów usługi Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): subskrypcji otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.
>
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
>
>

## <a id="learn"></a>Dowiesz się
Samouczek przedstawia sposób wykonywania następujących zadań:

* Włącz komputer dla rozwoju platformy Azure przez zainstalowanie zestawu Azure SDK (tylko dla programu Visual Studio 2013 i użytkowników 2015).
* Utwórz projekt aplikacji konsoli, która automatycznie wdraża jako zadanie WebJob platformy Azure, podczas wdrażania projektu sieci web skojarzony.
* Przetestuj zestaw SDK zadań Webjob wewnętrznej bazy danych lokalnie na komputerze dewelopera.
* Publikowanie aplikacji z zapleczem zadania Webjob do aplikacji sieci web w usłudze App Service.
* Przekazywanie plików i zapisywanie ich w usłudze obiektów Blob platformy Azure.
* Używanie zestawu SDK zadań Webjob Azure do pracy z obiektów blob i kolejek usługi Azure Storage.

## <a id="contosoads"></a>Architektura aplikacji
Przykładowa aplikacja korzysta z [wzorzec skoncentrowane kolejki pracy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) do obciążające pracy obciążające Procesor z tworzeniem miniatur do procesu zaplecza.

Aplikacja przechowuje reklamy w bazie danych SQL oraz tworzy tabele i uzyskuje dostęp do danych za pomocą funkcji Code First platformy Entity Framework. W przypadku każdej reklamy baza danych zawiera dwa adresy URL: jeden dla obrazu w pełnym rozmiarze i jeden do miniatury.

![Tabela reklam](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

Gdy użytkownik przesyła obraz, aplikacji sieci web zapisuje obraz w [obiektów blob platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), oraz informacje o reklamie są przechowywane w bazie danych przy użyciu adresu URL, który wskazuje obiekt blob. W tym samym czasie w kolejce platformy Azure jest zapisywany komunikat. W ramach procesu zaplecza uruchomiony jako zadanie WebJob platformy Azure zestaw SDK zadań Webjob sonduje kolejki wiadomości. Gdy pojawi się nowy komunikat, zadania WebJob tworzy miniaturę obrazu i aktualizuje pole bazy danych adresu URL miniatury dla danej reklamy. Poniżej przedstawiono diagram przedstawia interakcje między częściami aplikacji:

![Architektura aplikacji Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
Samouczek instrukcje dotyczą zestawu Azure SDK dla platformy .NET 2.7.1 lub nowszej.

## <a id="storage"></a>Tworzenie konta usługi Azure Storage
Konto magazynu platformy Azure udostępnia zasoby służące do przechowywania danych kolejek i obiektów blob w chmurze. Jest on używany również przez zestaw SDK zadań Webjob do przechowywania danych rejestrowania pulpitu nawigacyjnego.

W przypadku aplikacji rzeczywistych można zwykle utworzyć oddzielne konta dla danych aplikacji porównywanych z danymi rejestrowania oraz oddzielne konta dla danych testowych porównywanych z danymi produkcyjnymi. W tym samouczku będzie używane tylko jedno konto.

1. Otwórz **Eksploratora serwera** okna w programie Visual Studio.
2. Kliknij prawym przyciskiem myszy **Azure** węzeł, a następnie kliknij przycisk **nawiązywanie połączenia z subskrypcją platformy Microsoft Azure...** .
   
   ![Nawiązywanie połączenia z usługą Azure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. Zaloguj się przy użyciu poświadczeń konta platformy Azure.
4. Kliknij prawym przyciskiem myszy **magazynu** w obszarze węzła Azure, a następnie kliknij przycisk **Utwórz konto magazynu**.
   
   ![Tworzenie konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. W **Utwórz konto magazynu** okna dialogowego, wprowadź nazwę konta magazynu.

    Nazwa musi być muszą być unikatowe (inne konto magazynu platformy Azure mogą mieć takiej samej nazwy). Jeśli wprowadzona nazwa jest już w użyciu, uzyskasz możliwość go zmienić.

    Adres URL, aby uzyskać dostęp do konta magazynu będzie *{nazwa}*. core.windows.net.
6. Ustaw **Region lub grupę koligacji** listy rozwijanej do najbliższego regionu.

    To ustawienie określa, w którym Centrum danych Azure będą obsługiwać Twoje konto magazynu. W tym samouczku wybór nie należy to znaczącej różnicy. Jednak w przypadku aplikacji sieci web produkcji mają serwera sieci web i konta magazynu w tym samym regionie, aby zminimalizować opóźnienie i danych opłaty za wyjście. Aplikacja sieci web (do którego należy utworzyć później) centrum danych powinien być możliwie jak najbardziej zbliżone do przeglądarki, aby zminimalizować czas oczekiwania na dostęp do aplikacji sieci web.
7. Z listy rozwijanej **Replikacja** wybierz wartość **Lokalnie nadmiarowy**.

    Jeśli na koncie magazynu włączono replikację geograficzną, przechowywana zawartość jest replikowana do pomocniczego centrum danych. Pozwala to na przejście do trybu failover w tej lokalizacji w przypadku poważnej awarii w lokalizacji głównej. Replikacja geograficzna może pociągnąć za sobą dodatkowe koszty. W przypadku kont testowych i projektowych przeważnie nie chcesz płacić za replikację geograficzną. Aby uzyskać więcej informacji, zobacz temat dotyczący [tworzenia i usuwania konta magazynu oraz zarządzania nim](../storage/common/storage-create-storage-account.md).
8. Kliknij przycisk **Utwórz**.

    ![Nowe konto usługi Storage](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>Pobierz aplikację
1. Pobierz i rozpakuj [ukończone rozwiązanie](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).
2. Uruchom program Visual Studio.
3. Z **pliku** menu wybierz **Otwórz > Projekt/rozwiązanie**, przejdź do lokalizacji pobranego rozwiązania, a następnie otwórz plik rozwiązania.
4. Naciśnij kombinację klawiszy CTRL+SHIFT+B w celu skompilowania rozwiązania.

    Domyślnie program Visual Studio automatycznie przywraca zawartość pakietu NuGet, która nie została uwzględniona w pliku *ZIP*. Jeśli pakiety nie zostaną przywrócone, zainstaluj je ręcznie, przechodząc do **Zarządzaj pakietami NuGet dla rozwiązania** okno dialogowe i klikając **przywrócić** u góry po prawej stronie.
5. W **Eksploratora rozwiązań**, upewnij się, że **ContosoAdsWeb** został wybrany jako projekt startowy.

## <a id="configurestorage"></a>Konfigurowanie aplikacji w celu używania konta magazynu
1. Otwórz aplikację *Web.config* pliku w projekcie ContosoAdsWeb.

    Plik zawiera parametry połączenia SQL i parametry połączenia magazynu Azure do pracy z obiektów blob i kolejek.

    Parametry połączenia SQL wskazuje [programu SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) bazy danych.

    Parametry połączenia magazynu jest przykład symbole zastępcze klucz nazwy i dostępu do konta magazynu. Będzie to zastąpić przy użyciu parametrów połączenia, nazwa i klucz konta magazynu.  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    Parametry połączenia magazynu nosi nazwę AzureWebJobsStorage, ponieważ jest to nazwa, który korzysta z zestawu SDK WebJobs domyślnie. Tej samej nazwie jest używany w tym miejscu, należy ustawić tylko jedną wartość ciągu połączenia w środowisku platformy Azure.
2. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy konto magazynu w obszarze **magazynu** węzeł, a następnie kliknij przycisk **właściwości**.

    ![Kliknij przycisk Właściwości konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. W **właściwości** okna, kliknij przycisk **klucze konta magazynu**, a następnie kliknij przycisk wielokropka.

    ![Klucze konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. Kopiuj **ciąg połączenia**.

    ![Okno dialogowe klucze konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. Zastąp parametry połączenia magazynu w *Web.config* plik został skopiowany ciągu połączenia. Upewnij się, że możesz zaznaczyć wszystko w cudzysłowach, ale bez cudzysłowów przed wklejeniem.
6. Otwórz *App.config* plik w projekcie ContosoAdsWebJob.

    Ten plik zawiera dwa parametry połączenia magazynu, jeden dla danych aplikacji i jeden dla rejestrowania. Możesz użyć oddzielny magazyn kont dla danych aplikacji i rejestrowania i można użyć [konta wielu magazynu dla danych](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs). W tym samouczku użyjesz konto jednego magazynu. Parametry połączenia mają symbole zastępcze klucze konta magazynu.

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    Domyślnie zestaw SDK zadań Webjob szuka parametry połączenia o nazwie AzureWebJobsStorage i AzureWebJobsDashboard. Alternatywnie, można [magazynu parametrów połączenia, ale mają i przekaż go w jawnie na `JobHost` obiektu](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).
7. Zastąp parametry połączenia magazynu przy użyciu parametrów połączenia, które wcześniej zostały skopiowane.
8. Zapisz zmiany.

## <a id="run"></a>Uruchamianie aplikacji lokalnie
1. Aby rozpocząć frontonu sieci web aplikacji, naciśnij kombinację klawiszy CTRL + F5.

    W domyślnej przeglądarce otworzy się do strony głównej. (Projekt sieci web jest uruchomiona, ponieważ zostały wprowadzone projekt startowy.)

    ![Strona główna aplikacji contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. Można uruchomić zadania WebJob wewnętrznej bazy danych aplikacji, kliknij prawym przyciskiem myszy projekt ContosoAdsWebJob w **Eksploratora rozwiązań**, a następnie kliknij przycisk **debugowania** > **Start nowe wystąpienie**.

    Okno aplikacji konsoli otwiera i wyświetla rejestrowanie komunikatów wskazujący, że obiekt JobHost zestawu SDK zadań Webjob został uruchomiony w trybie uruchamiania.

    ![Okno aplikacji konsoli pokazujący, że działa wewnętrznej bazy danych](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. W przeglądarce, kliknij przycisk **tworzenia Ad**.
4. Wprowadź dane testowe, wybierz obraz do przekazania, a następnie kliknij przycisk **Utwórz**.

    ![Tworzenie strony](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    Aplikacja przechodzi do strony indeksu, ale nie wyświetla miniatury nowej reklamy, ponieważ przetwarzanie nie zostało jeszcze przeprowadzone.

    W tym samym czasie po krótkim okresie oczekiwania komunikat rejestrowania w oknie aplikacji konsoli Pokazuje, że komunikatu w kolejce został odebrany i został przetworzony.

    ![Okno aplikacji konsoli przedstawiający przetworzeniu komunikatu w kolejce](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. Po rejestrowanie komunikatów w oknie aplikacji konsoli, Odśwież stronę indeksu, aby zobaczyć miniaturę.

    ![Strona indeksu](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. Kliknij link **Details** (Szczegóły) obok reklamy, aby wyświetlić obraz w pełnym rozmiarze.

    ![Strona szczegółów](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

Działała aplikacja na komputerze lokalnym i używa programu SQL Server, bazy danych znajdującej się na komputerze, ale działa w przypadku kolejek i obiektów blob w chmurze. W poniższej sekcji uruchomisz aplikację w chmurze przy użyciu bazy danych w chmurze, a także chmury obiekty BLOB i kolejki.  

## <a id="runincloud"></a>Uruchamianie aplikacji w chmurze
Aby uruchomić aplikację w chmurze, należy wykonać następujące kroki:

* Wdrażanie w aplikacjach sieci Web. Visual Studio automatycznie tworzy nową aplikację sieci web usługi aplikacji i wystąpienie bazy danych SQL.
* Konfigurowanie aplikacji sieci web do używania konta magazynu i bazy danych Azure SQL.

Po utworzeniu niektóre reklamy podczas uruchamiania w chmurze, zostanie wyświetlona pulpitu nawigacyjnego zestaw SDK zadań Webjob, aby zobaczyć zaawansowanej funkcji, które musi oferować monitorowania.

### <a name="deploy-to-web-apps"></a>Wdrażanie w aplikacjach sieci Web

1. Zamknij przeglądarkę i okna aplikacji konsoli.
2. Postępuj zgodnie z instrukcjami [publikowania na platformie Azure w usłudze SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) sekcji.
3. Po wykonaniu kroków wdrażania kontynuować wykonywanie kolejnych zadań w tym artykule.

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a>Konfigurowanie aplikacji sieci web do używania konta magazynu i bazy danych Azure SQL
Zabezpieczeń najlepszym rozwiązaniem jest [należy unikać umieszczania poufne informacje, takie jak parametry połączenia w plikach, które są przechowywane w repozytoriach kodów źródłowych](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets). Platforma Azure udostępnia sposób, aby to zrobić: można ustawić parametry połączenia i inne wartości ustawienia w środowisku platformy Azure i interfejsy API konfiguracji ASP.NET automatyczne pobranie te wartości po uruchomieniu aplikacji na platformie Azure. Te wartości zostaną ustawione na platformie Azure, używając **Eksploratora serwera**, portalu Azure, programu Windows PowerShell lub interfejsu wiersza polecenia i platform. Aby uzyskać więcej informacji, zobacz [jak ciągi aplikacji i pracy ciągów połączenia](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).

W tej sekcji użyjesz **Eksploratora serwera** można ustawić wartości ciągu połączenia na platformie Azure.

1. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy aplikację sieci web, w obszarze **Azure > App Service > {grupie zasobów}**, a następnie kliknij przycisk **ustawienia widoku**.

    **Aplikacji sieci Web Azure** na zostanie otwarte okno **konfiguracji** kartę.
2. Zmień nazwę parametrów połączenia parametru DefaultConnection na nazwę wybraną podczas konfigurowania bazy danych SQL w [publikowania na platformie Azure w usłudze SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) artykułu.

    Ten ciąg połączenia tworzone automatycznie, podczas tworzenia aplikacji sieci web z skojarzonej bazy danych, więc ma już wartość ciągu połączenia na odpowiednie platformy Azure. Tylko nazwę chcesz zmienić do kodu poszukuje programu.
3. Dodaj dwa nowe parametry połączenia, o nazwie AzureWebJobsStorage i AzureWebJobsDashboard. Ustaw typ bazy danych **niestandardowy**i ustaw wartość ciągu połączenia na tę samą wartość, który był wcześniej używany przez *Web.config* i *App.config* plików. (Upewnij się, zawierają ciąg całego połączenia, nie tylko klucz dostępu, a nie zawierają znaki cudzysłowu.)

    Te parametry połączenia są używane przez zestaw SDK zadań Webjob, jeden dla danych aplikacji i jeden do rejestrowania. Jak przedstawiono wcześniej, jeden dla danych aplikacji jest również używany przez kod frontonu sieci web.
4. Kliknij pozycję **Zapisz**.

    ![Parametry połączenia w portalu Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy aplikację sieci web, a następnie kliknij przycisk **zatrzymać**.
6. Po zatrzymaniu aplikacji sieci web, ponownie kliknij prawym przyciskiem myszy aplikację sieci web, a następnie kliknij przycisk **Start**.

   Zadania WebJob jest uruchamiana automatycznie, gdy opublikujesz, ale zatrzymuje go po wprowadzeniu zmiany konfiguracji. Aby uruchomić go ponownie, można ponownie uruchomić aplikacji sieci web lub ponownego uruchomienia zadania WebJob w [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Ogólnie zaleca się ponowne uruchomienie aplikacji sieci web po zmianie konfiguracji.
7. Odśwież okno przeglądarki, które ma adres URL aplikacji sieci web na pasku adresu.

    Zostanie wyświetlona strona główna.
8. Utwórz reklamę, jak w przypadku należy [lokalnego uruchomienia aplikacji](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).

   Pokazuje stronę indeksu bez miniatur na początku.
9. Odśwież stronę za kilka sekund i pojawi się miniatury.

   Jeśli nie ma miniatury, może być konieczne Zaczekaj minutę lub tak dla zadania WebJob do ponownego uruchomienia. Jeśli po chwili, nadal nie widzisz miniatury podczas odświeżania strony, zadania WebJob nie może być uruchomiony automatycznie. W takim przypadku przejdź do **usługi aplikacji** bloku w [portalu Azure](https://portal.azure.com/), Znajdź aplikację sieci web, a następnie kliknij przycisk **Start**.

### <a name="view-the-webjobs-sdk-dashboard"></a>Widok pulpitu nawigacyjnego zestaw SDK zadań Webjob
1. W [portalu Azure](https://portal.azure.com/), wybierz pozycję **blok App Services**Znajdź aplikację sieci web i zaznacz **Webjob**.
3. Wybierz **dzienniki** kartę.

    ![Karta dzienniki](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    Otwiera nową kartę przeglądarki do pulpitu nawigacyjnego, zestaw SDK zadań Webjob. Pulpit nawigacyjny pokazuje, że zadania WebJob działa i czy zawiera listę funkcji w kodzie, która wyzwoliła zestaw SDK zadań Webjob.
4. Kliknij jedną z funkcji, aby wyświetlić szczegółowe informacje o jego wykonywania.

    ![Zestaw SDK zadań Webjob pulpitu nawigacyjnego](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Zestaw SDK zadań Webjob pulpitu nawigacyjnego](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    **Funkcja powtarzania** framework zestaw SDK zadań Webjob ponownie wywołać funkcji powoduje, że przycisk na tej stronie i daje możliwość zmiany danych, najpierw przekazany do funkcji.

> [!NOTE]
> Po zakończeniu testowania, rozważ usunięcie aplikacji sieci web, konta magazynu i wystąpienie bazy danych SQL. Aplikacja sieci web jest bezpłatne, ale wystąpienie konta i bazy danych magazynu SQL Naliczanie opłat (chociaż, ze względu na mały rozmiar minimalny). Ponadto pozostawienie uruchomieniu aplikacji sieci web, każda osoba, która znajdzie adres URL można tworzyć i wyświetlać reklamy. 
>
>

### <a name="delete-your-web-app"></a>Usuń aplikację sieci web
W portalu, przejdź do **usługi aplikacji** bloku, Znajdź i wybierz aplikację sieci web, a następnie kliknij **usunąć**. Jeśli chcesz tylko czasowo uniemożliwić innym użytkownikom uzyskiwanie dostępu do aplikacji sieci web, kliknij przycisk **zatrzymać** zamiast tego. W takim przypadku opłaty będą nadal naliczane dla konta magazynu i bazy danych SQL.

### <a name="delete-your-storage-account"></a>Usuwanie konta magazynu
Aby usunąć konta magazynu, zobacz [usuwania konta magazynu](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account). 

### <a name="delete-your-database"></a>Usunięcie bazy danych
Aby usunąć bazę danych SQL, zobacz [interfejsu API REST bazy danych SQL Azure](https://docs.microsoft.com/rest/api/sql/) dokumentacji.

## <a id="create"></a>Tworzenie aplikacji od początku
W tej sekcji należy wykonać następujące zadania:

* Tworzenie rozwiązania Visual Studio z projektu sieci web.
* Dodawanie projektu biblioteki klas dla danych warstwy dostępu, która jest udostępniana między frontonu i zaplecza.
* Dodaj projekt aplikacji konsoli wewnętrznej bazy danych, z włączonym wdrażaniem zadań Webjob.
* Dodawanie pakietów NuGet.
* Ustawianie odwołań do projektu.
* Skopiuj pliki kodu i konfiguracji aplikacji z pobraną aplikację, którą doświadczenie z poprzedniej sekcji samouczka.
* Przejrzyj części kodu, współdziałające z obiekty BLOB platformy Azure i kolejek oraz zestaw SDK zadań Webjob.

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>Tworzenie rozwiązań programu Visual Studio z projektu sieci web i projektu biblioteki klas
1. W programie Visual Studio, wybierz **pliku** > **nowy** > **projektu**.
2. W **nowy projekt** okno dialogowe, wybierz **Visual C#** > **Web** > **aplikacji sieci Web platformy ASP.NET (.NET Framework)**.
3. Nazwij projekt ContosoAdsWeb, nazwa rozwiązania ContosoAdsWebJobsSDK (zmiana nazwy rozwiązania, jeśli umieścić go w tym samym folderze co pobranego rozwiązania), a następnie kliknij przycisk **OK**.

    ![Nowy projekt](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. W **nowej aplikacji sieci Web ASP.NET** okno dialogowe, wybierz szablon MVC, a następnie wybierz **Zmień uwierzytelnianie**.

    ![Zmienianie uwierzytelniania](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. W **Zmień uwierzytelnianie** okno dialogowe, wybierz **bez uwierzytelniania**, a następnie kliknij przycisk **OK**.

    ![Bez uwierzytelniania](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. W **nowej aplikacji sieci Web ASP.NET** okna dialogowego, kliknij przycisk **OK**.

    Program Visual Studio tworzy rozwiązanie i projektu sieci web.
7. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy rozwiązanie (nie projekt) i wybierz **Dodaj** > **nowy projekt**.
8. W **Dodawanie nowego projektu** okno dialogowe, wybierz **Visual C#** > **Windows Desktop klasycznego** > **biblioteki klas (.NET Framework)** szablonu.  
9. Nazwij projekt *ContosoAdsCommon*, a następnie kliknij przycisk **OK**.

    Ten projekt będzie zawierać kontekst Entity Framework, jak i model danych, który będzie używany zarówno frontonu i zaplecza. Alternatywnie można zdefiniować klasy związane z platformą EF w projekcie sieci web i odwoływać się do tego projektu z projektu zadania WebJob. Ale następnie projektu zadania WebJob musi odwołania do zestawów sieci web, których nie potrzebuje.

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>Dodaj projekt aplikacji konsoli z włączonym wdrażaniem zadań Webjob
1. Kliknij prawym przyciskiem myszy projekt sieci web (nie rozwiązania lub projektu biblioteki klas), a następnie kliknij przycisk **Dodaj** > **nowy projekt zadania WebJob Azure**.

    ![Nowe zaznaczenie menu projektu zadania WebJob platformy Azure](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. W **dodać zadania WebJob Azure** okna dialogowego, wprowadź ContosoAdsWebJob jednocześnie jako **Nazwa projektu** i **Nazwa zadania WebJob**. Pozostaw **tryb uruchomienia zadania WebJob** ustawioną **Uruchom stale**.
3. Kliknij przycisk **OK**.

   Program Visual Studio tworzy aplikacja Konsolowa, która jest skonfigurowana do wdrożenia jako zadanie WebJob zawsze, gdy wdrażanie projektu sieci web. W tym celu wykonać następujące zadania po utworzeniu projektu:

   * Dodaje *zadania webjob publikowania settings.json* plików w folderze właściwości projektu zadania WebJob.
   * Dodaje *list.json webjob* plików w folderze właściwości projektu sieci web.
   * Zainstalowany pakiet Microsoft.Web.WebJobs.Publish NuGet projektu zadania WebJob.

   Aby uzyskać więcej informacji na temat tych zmian, zobacz [wdrażanie zadań Webjob za pomocą programu Visual Studio](websites-dotnet-deploy-webjobs.md).

### <a name="add-nuget-packages"></a>Dodawanie pakietów NuGet
Szablon nowego projektu dla projektu zadania WebJob automatycznie instaluje pakiet NuGet zestawu SDK zadań Webjob [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) i jego zależności.

Jedna z zależności zestawu SDK zadań Webjob, które jest instalowane automatycznie w projektu zadania WebJob jest biblioteka klienta magazynu Azure (SCL). Jednak należy dodać go do projektu sieci web do pracy z obiektów blob i kolejek.

1. Otwórz **Zarządzaj pakietami NuGet** okna dialogowego dla rozwiązania.
2. W okienku po lewej stronie wybierz **zainstalowane pakiety**.
3. Znajdź *usługi Azure Storage* pakietu, a następnie kliknij przycisk **Zarządzaj**.
4. W **Wybierz projekty** wybierz **ContosoAdsWeb** pole wyboru, a następnie kliknij przycisk **OK**.

    Wszystkie trzy projekty Użyj programu Entity Framework do pracy z danymi w bazie danych SQL.
5. W okienku po lewej stronie wybierz **Online**.
6. Znajdź pakiet NuGet *EntityFramework*, a następnie zainstaluj go we wszystkich trzech projektach.

### <a name="set-project-references"></a>Ustawianie odwołań do projektu
Sieć web i projektów zadania WebJob pracy z bazy danych SQL, tak zarówno potrzebują odwołania do projektu ContosoAdsCommon.

1. W projekcie ContosoAdsWeb ustaw odwołanie do projektu ContosoAdsCommon. (Kliknij prawym przyciskiem myszy projekt ContosoAdsWeb, a następnie kliknij przycisk **Dodaj** > **odwołania**. 
2. W **Menedżera odwołań** okno dialogowe, wybierz opcję **projekty** > **rozwiązania** > **ContosoAdsCommon**, a następnie kliknij przycisk **OK**.)
   
    Projektu zadania WebJob musi odwołań do pracy z obrazami i uzyskać dostęp do parametrów połączenia.

4. W projekcie ContosoAdsWebJob Ustaw odwołanie do `System.Drawing` i `System.Configuration`.

### <a name="add-code-and-configuration-files"></a>Dodawanie plików kodu i konfiguracji
Nie są wyświetlane w tym samouczku jak [utworzyć przy użyciu funkcji szkieletów widoków i kontrolerów MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), jak do [pisania kodu programu Entity Framework, który współpracuje z baz danych programu SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), lub [podstawy programowania asynchronicznego w programie ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async). Tak, czy pozostaje zrobić to skopiować kod i konfiguracja pliki z pobranego rozwiązania do nowego rozwiązania. Po wykonaniu tej czynności, w poniższych sekcjach Pokaż i objaśnione części kodu.

Aby dodać pliki do projektu lub folderu, kliknij prawym przyciskiem myszy projekt lub folder, a następnie kliknij kolejno pozycje **Dodaj** > **Istniejący element**. Wybierz pliki, a następnie kliknij przycisk **Dodaj**. Jeśli pojawi się pytanie, czy chcesz zastąpić istniejące pliki, kliknij pozycję **Tak**.

1. W projekcie ContosoAdsCommon Usuń *Class1.cs* i Dodaj w jego miejsce następujące pliki z pobranego projektu.

   * *AD.CS*
   * *ContosoAdscontext.cs*
   * *BlobInformation.cs*
2. W projekcie ContosoAdsWeb dodaj poniższe pliki z pobranego projektu.

   * *Plik Web.config*
   * *Global.asax.CS*  
   * W *kontrolerów* folder: *AdController.cs*
   * W *Views\Shared* folder: *_Layout.cshtml* pliku
   * W *Views\Home* folder: *Index.cshtml*
   * W *Views\Ad* folder (najpierw utwórz folder): pięć *.cshtml* plików
3. W projekcie ContosoAdsWebJob należy dodać następujące pliki z pobranego projektu.

   * *App.config* (Zmień filtr typu plików, aby **wszystkie pliki**)
   * *Plik program.CS*
   * *Functions.CS*

Można teraz kompilacji, uruchamiania i wdrażania aplikacji, zgodnie z instrukcją wcześniej w samouczku. Przed tym, jednak zatrzymać zadania WebJob, że nadal działa w pierwszej wdrożonej w aplikacji sieci web. W przeciwnym razie tego zadania WebJob będzie przetwarzać wiadomości w kolejce utworzony lokalnie lub za pomocą aplikacji uruchomionych w nowej aplikacji sieci web, ponieważ wszystkie korzystają z tego samego konta magazynu.

## <a id="code"></a>Przegląd kodu aplikacji
W poniższych sekcjach opisano kod powiązany z pracą z zestawu SDK zadań Webjob i usługi Azure Storage obiekty BLOB i kolejki.

> [!NOTE]
> Dla kodu specyficzne dla zestawu SDK zadań Webjob, przejdź do [Program.cs i Functions.cs](#programcs) sekcje.
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon — Ad.cs
Plik Ad.cs definiuje wyliczenia związane z kategoriami reklam i klasą jednostki POCO dla informacji o reklamach.

        public enum Category
        {
            Cars,
            [Display(Name="Real Estate")]
            RealEstate,
            [Display(Name = "Free Stuff")]
            FreeStuff
        }

        public class Ad
        {
            public int AdId { get; set; }

            [StringLength(100)]
            public string Title { get; set; }

            public int Price { get; set; }

            [StringLength(1000)]
            [DataType(DataType.MultilineText)]
            public string Description { get; set; }

            [StringLength(1000)]
            [DisplayName("Full-size Image")]
            public string ImageURL { get; set; }

            [StringLength(1000)]
            [DisplayName("Thumbnail")]
            public string ThumbnailURL { get; set; }

            [DataType(DataType.Date)]
            [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
            public DateTime PostedDate { get; set; }

            public Category? Category { get; set; }
            [StringLength(12)]
            public string Phone { get; set; }
        }

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon — ContosoAdsContext.cs
Klasa ContosoAdsContext Określa, czy klasa Ad jest używany w kolekcji DbSet Entity Framework są przechowywane w bazie danych SQL.

        public class ContosoAdsContext : DbContext
        {
            public ContosoAdsContext() : base("name=ContosoAdsContext")
            {
            }
            public ContosoAdsContext(string connString)
                : base(connString)
            {
            }
            public System.Data.Entity.DbSet<Ad> Ads { get; set; }
        }

Klasa ma dwa konstruktory. Pierwszy jest używany przez projekt sieci web i określa nazwę parametrów połączenia, które są przechowywane w pliku Web.config lub środowisko uruchomieniowe platformy Azure. Drugi konstruktor umożliwia przekazywanie rzeczywistych parametrów połączenia. Są one wymagane projektu zadania WebJob ponieważ nie ma on pliku Web.config. Wcześniej przedstawiono lokalizację przechowywania tych parametrów połączenia. Dalej pokażemy, jak kod pobiera parametry połączenia podczas tworzenia wystąpień klasy DbContext.

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon — BlobInformation.cs
`BlobInformation` Klasa jest używana do przechowywania informacji na temat obiekt blob obrazu w komunikatu w kolejce.

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb — Global.asax.cs
Kod wywoływany z metody `Application_Start` umożliwia tworzenie kontenera obiektów blob *obrazów* i kolejki *obrazów*, jeśli jeszcze nie istnieją. Dzięki temu, że przy każdym uruchomieniu przy użyciu nowego konta magazynu, kolejka i kontener obiektów blob wymagane są tworzone automatycznie.

Kod uzyskuje dostęp do konta magazynu przy użyciu parametrów połączenia magazynu z *Web.config* pliku lub środowisko uruchomieniowe platformy Azure.

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

Następnie pobiera odwołanie do *obrazów* kontenera obiektów blob, tworzy kontener, jeśli jeszcze nie istnieje, i ustawia uprawnienia dostępu w obrębie nowego kontenera. Domyślnie nowe kontenery Zezwalaj tylko klientom z poświadczeniami konta magazynu dostęp do obiektów blob. Aplikacja sieci web musi być publiczne, aby możliwe było wyświetlanie obrazów przy użyciu adresów URL wskazujących na obiekty BLOB obrazów obiekty BLOB.

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

Podobny kod pobiera odwołanie do *thumbnailrequest* kolejki i tworzy nową kolejkę. W takim przypadku nie trzeba zmieniać uprawnień.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb — _Layout.cshtml
Plik *_Layout.cshtml* umożliwia ustawienie nazwy aplikacji w nagłówku i stopce oraz utworzenie wpisu menu „Ads”.

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb — Views\Home\Index.cshtml
Plik *Views\Home\Index.cshtml* umożliwia wyświetlanie linków kategorii na stronie głównej. Linki przekazują wartość całkowitą typu wyliczeniowego `Category` w zmiennej querystring na stronie indeksu reklam.

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb — AdController.cs
W pliku *AdController.cs* konstruktor wywołuje metodę `InitializeStorage` w celu utworzenia obiektów biblioteki klienta usługi Azure Storage, które będą dostarczać interfejs API do pracy z kolejkami i obiektami blob.

Następnie kod pobiera odwołanie do *obrazów* kontenera obiektów blob, jak przedstawiono wcześniej w *Global.asax.cs*. Podczas wykonywania, który, ustawia domyślną [zasady ponawiania](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) odpowiednie dla aplikacji sieci web. Domyślne zasady ponawiania wykładniczego wycofywania mogą powodować zawieszanie aplikacji sieci Web na czas dłuższy niż minuta w przypadku kolejnych prób i wystąpienia błędu przejściowego. Zasady ponawiania określone w tym miejscu powodują oczekiwanie przez trzy sekundy po każdej próbie. Maksymalna liczba prób to trzy.

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

Podobny kod pobiera odwołanie do kolejki *obrazów*.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

Większość kodu kontrolera jest typowa dla pracy z modelem danych platformy Entity Framework za pomocą klasy DbContext. Wyjątkiem jest metoda HttpPost `Create`, która powoduje przekazanie pliku i zapisanie go w magazynie obiektów blob. Integrator modelu udostępnia obiekt [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) w metodzie.

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

Jeśli użytkownik wybrał plik do przekazania, kod powoduje przekazanie pliku, zapisanie go w obiekcie blob i zaktualizowanie rekordu bazy danych Ad przy użyciu adresu URL, który wskazuje obiekt blob.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

Kod, który obsługuje przekazywanie, znajduje się w metodzie `UploadAndSaveBlobAsync`. Powoduje on utworzenie nazwy identyfikatora GUID dla obiektu blob, przekazanie i zapisanie pliku oraz zwraca odwołanie do zapisanego obiektu blob.

        private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
        {
            string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
            CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
            using (var fileStream = imageFile.InputStream)
            {
                await imageBlob.UploadFromStreamAsync(fileStream);
            }
            return imageBlob;
        }

Po HttpPost `Create` metody obiektu blob i aktualizuje bazę danych, tworzy kolejki komunikatów w celu poinformowania procesu zaplecza, że obraz jest gotowy do konwersji na miniaturę.

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

Kod HttpPost `Edit` metoda jest podobny, z wyjątkiem tego, że jeśli użytkownik wybierze nowy plik obrazu, należy usunąć wszystkie obiekty BLOB, które już istnieją dla tej usługi ad.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

Oto kod, który usuwania obiektów blob podczas usuwania reklamy:

        private async Task DeleteAdBlobsAsync(Ad ad)
        {
            if (!string.IsNullOrWhiteSpace(ad.ImageURL))
            {
                Uri blobUri = new Uri(ad.ImageURL);
                await DeleteAdBlobAsync(blobUri);
            }
            if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
            {
                Uri blobUri = new Uri(ad.ThumbnailURL);
                await DeleteAdBlobAsync(blobUri);
            }
        }
        private static async Task DeleteAdBlobAsync(Uri blobUri)
        {
            string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
            CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
            await blobToDelete.DeleteAsync();
        }

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb — Views\Ad\Index.cshtml i Details.cshtml
*Index.cshtml* służy do wyświetlania miniatury z innymi danymi reklamy:

        <img  src="@Html.Raw(item.ThumbnailURL)" />

*Details.cshtml* pliku wyświetla obrazu w pełnym rozmiarze:

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb — Views\Ad\Create.cshtml i Edit.cshtml
Pliki *Create.cshtml* i *Edit.cshtml* określają kodowanie formularzy, które umożliwia kontrolerowi pobieranie obiektu `HttpPostedFileBase`.

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

Element `<input>` informuje przeglądarkę o konieczności udostępnienia okna dialogowego wyboru pliku.

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob - Program.cs
Po uruchomieniu zadania WebJob, `Main` metoda wywołuje zestaw SDK zadań Webjob `JobHost.RunAndBlock` metody, aby rozpocząć wykonywanie wyzwalane funkcje w bieżącym wątku.

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>Metoda GenerateThumbnail ContosoAdsWebJob - Functions.cs-
Zestaw SDK zadań Webjob wywołuje tę metodę w przypadku otrzymania komunikatu w kolejce. Metoda tworzy miniaturę i umieszcza miniatury adres URL w bazie danych.

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within the function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* `QueueTrigger` Atrybut określa, że zestaw SDK zadań Webjob, aby wywołać tę metodę po odebraniu nowej wiadomości w kolejce thumbnailrequest.

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    `BlobInformation` Obiekt kolejki wiadomości jest automatycznie zdeserializowany do `blobInfo` parametru. Po zakończeniu działania metody komunikat z kolejki jest usuwana. W przypadku niepowodzenia przed wykonaniem metody komunikatu w kolejce nie zostanie usunięta; Po wygaśnięciu dzierżawy 10-minutowych komunikat jest wydane do pobrania ponownie i przetworzyć. Ta sekwencja nie należy powtórzyć przez czas nieokreślony, jeśli komunikat zawsze powoduje zgłoszenie wyjątku. Po 5 bez powodzenia próbuje przetworzyć komunikatu, wiadomość zostanie przeniesiona do kolejki o nazwie {queuename}-skażone. Maksymalna liczba prób jest konfigurowalne.
* Dwa `Blob` atrybuty Podaj obiektów, które są powiązane z obiektów blob: jeden do istniejącego obiektu blob obrazu i jeden do nowego blob miniatury, w którym ta metoda tworzy.

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    Nazwy obiektów blob pochodzą z właściwości `BlobInformation` obiektu odebranego w wiadomości w kolejce (`BlobName` i `BlobNameWithoutExtension`). Aby uzyskać pełną funkcjonalność biblioteki klienta usługi Storage, można użyć `CloudBlockBlob` klasy do pracy z obiektami blob. Jeśli chcesz ponownie użyć kodu napisanego do pracy z `Stream` obiekty, można użyć `Stream` klasy.

Aby uzyskać więcej informacji na temat pisania funkcje programu wykorzystujące zestaw SDK zadań Webjob atrybutów zobacz następujące zasoby:

* [Jak używać usługi Azure Queue Storage z zestawem SDK usługi WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Używanie usługi Azure Blob Storage z zestawem SDK zadań WebJob](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Jak używać usługi Azure Table Storage z zestawem SDK usługi WebJobs](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Jak używać usługi Azure Service Bus z zestawem SDK usługi WebJobs](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * Jeśli aplikacja sieci web jest uruchomiony na wiele maszyn wirtualnych, wielu zadań Webjob będzie działać jednocześnie, a w niektórych przypadkach może to spowodować tych samych danych przetwarzana wiele razy. To nie jest problem, korzystając z wbudowanego kolejki, obiektów blob i wyzwalaczy usługi Service Bus. Zestaw SDK gwarantuje, że funkcje będą przetwarzane tylko raz dla każdego komunikatu lub obiektu blob.
> * Informacje o sposobie implementacji bezpiecznego zamknięcia, zobacz [łagodne zamykanie](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
> * Kod w `ConvertImageToThumbnailJPG` — metoda (tego nie pokazano) używa klas w `System.Drawing` przestrzeni nazw dla uproszczenia. Jednak klasy w tej przestrzeni nazw zostały zaprojektowane do użytku z aplikacją Windows Forms. Nie są one obsługiwane w usłudze systemu Windows lub programu ASP.NET. Aby uzyskać więcej informacji o opcjach przetwarzania obrazu, zobacz [Dynamiczne generowanie obrazu](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) i [Bezpośrednie zmienianie rozmiaru obrazu](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="next-steps"></a>Następne kroki
W tym samouczku przedstawiono prostą aplikację wielowarstwową, która korzysta z zestawu SDK zadań Webjob dla przetwarzania wewnętrznej bazy danych. Ta sekcja zawiera sugestie dotyczące dowiedzieć się więcej na temat aplikacje wielowarstwowe platformy ASP.NET i zadań Webjob.

### <a name="missing-features"></a>Brak funkcji
Aplikacja została zachowana proste samouczek ułatwiający Rozpoczynanie pracy. W aplikacji rzeczywistych można zaimplementować [iniekcji zależności](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) i [repozytorium i jednostki pracy wzorce](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), użyj [interfejs umożliwiający rejestrowanie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), użyj [migracje EF Code First](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) do zarządzania zmianami modelu danych, a następnie użyj [elastyczności połączenia platformy EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) do zarządzania błędami sieci.

### <a name="scaling-webjobs"></a>Skalowanie zadania Webjob
Zadania Webjob uruchamiane w kontekście aplikacji sieci web i nie są skalowalne oddzielnie. Na przykład jeśli jedno wystąpienie aplikacji sieci web Standard, można mieć tylko jedno wystąpienie procesu tła uruchomiona, a niektóre zasoby serwera (procesora CPU, pamięć, itp.), które w przeciwnym razie będą dostępne do obsługi zawartości sieci web używa.

Jeśli ruch jest zależna od czasu dzień lub dzień tygodnia i przetwarzania wewnętrznej bazy danych należy poczekać, można zaplanować Twoje zadania Webjob do uruchomienia w czasie mniejszym natężeniu ruchu. Jeżeli obciążenie jest nadal za duża dla tego rozwiązania, w tym celu można uruchomić wewnętrznej bazy danych jako zadanie WebJob w aplikacji sieci web oddzielnych dedykowanych. Aplikacja sieci web wewnętrznej bazy danych można następnie skalować niezależnie z aplikacji sieci web frontonu.

Aby uzyskać więcej informacji, zobacz [skalowanie zadania Webjob](websites-webjobs-resources.md#scale).

### <a name="avoiding-web-app-timeout-shut-downs"></a>Unikanie sieci web aplikacji limit czasu zamykania rozwijanych
Aby upewnić się, zawsze działają z zadań Webjob i uruchomione na wszystkich wystąpień aplikacji sieci web, należy włączyć [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) funkcji.

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a>Przy użyciu zestawu SDK zadań Webjob poza zadań Webjob
Program, który korzysta z zestawu SDK zadań Webjob nie ma do uruchamiania na platformie Azure w zadanie WebJob. Można uruchomić lokalnie i można również uruchomić w innych środowiskach, takich jak usługi w chmurze rola proces roboczy lub usługi systemu Windows. Jednak dostępne tylko zestaw SDK zadań Webjob pulpitu nawigacyjnego za pomocą aplikacji sieci web platformy Azure. Do użycia pulpit nawigacyjny, należy połączyć aplikację sieci web do konta magazynu używane przez ustawienie parametrów połączenia AzureWebJobsDashboard **Konfiguruj** kartę klasycznego portalu. Można następnie uzyskać do pulpitu nawigacyjnego, korzystając z następującego adresu URL:

https://{webappname}.SCM.azurewebsites.NET/azurejobs/#/Functions

Aby uzyskać więcej informacji, zobacz [pobierania pulpitu nawigacyjnego dla wdrożenia lokalnego przy użyciu zestawu SDK zadań Webjob](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ale należy pamiętać, że widoczny jest stara nazwa ciągu połączenia.

### <a name="more-webjobs-documentation"></a>Więcej dokumentacji zadań Webjob
Aby uzyskać więcej informacji, zobacz [zasoby dokumentacji zadań Webjob Azure](http://go.microsoft.com/fwlink/?LinkId=390226).
