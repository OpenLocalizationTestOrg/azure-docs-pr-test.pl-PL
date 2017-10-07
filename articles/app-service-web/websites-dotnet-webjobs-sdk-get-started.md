---
title: "aaaCreate zadanie WebJob platformy .NET w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Utwórz aplikację wielowarstwową przy użyciu platformy ASP.NET MVC i platformy Azure. Hello front end jest uruchamiany w aplikacji sieci web w usłudze Azure App Service i hello powrotem końcowy uruchomień jako zadanie WebJob. Aplikacja Hello korzysta z programu Entity Framework, bazy danych SQL i kolejek usługi Azure storage i obiektów blob."
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
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>Tworzenie zadania WebJob .NET w usłudze Azure App Service
Ten samouczek pokazuje, jak kod toowrite prostą aplikację ASP.NET MVC 5 wielowarstwowej, która używa hello [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md).

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Witaj celem hello [zestaw SDK zadań Webjob](websites-webjobs-resources.md) jest kod hello toosimplify zapisu typowych zadań, które mogą wykonywać zadanie WebJob, takich jak przetwarzania obrazu, przetwarzanie kolejki, agregacja danych RSS, plików obsługi i wysyłania wiadomości e-mail. zestaw SDK zadań Webjob Hello ma wbudowane funkcje do pracy z usługą Azure Storage i usługi Service Bus, planowanie zadań i obsługa błędów i wielu innych typowych scenariuszy. Ponadto ma przeznaczona toobe rozszerzony i jest [repozytorium typu open source dla rozszerzeń](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Witaj Przykładowa aplikacja to reklamowa Tablica ogłoszeń. Użytkowników może przekazywać obrazy dla reklam i procesu zaplecza konwertuje hello toothumbnails obrazów. Strona z listą ad Hello miniatury hello i strony szczegółów ad hello pokazuje hello obrazu w pełnym rozmiarze. Poniżej przedstawiono zrzut ekranu:

![Lista reklam](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

Ta przykładowa aplikacja działa z [kolejek Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) i [obiekty BLOB platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage). Witaj samouczek pokazuje, jak toodeploy hello aplikacji zbyt[usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) i [bazy danych SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).

## <a id="prerequisites"></a>Wymagania wstępne
Witaj samouczka przyjęto założenie, że wiesz, jak toowork z [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projekty w programie Visual Studio.

Samouczek Hello pierwotnie sformatowano dla programu Visual Studio 2013, ale może być używany z nowszej wersji programu Visual Studio. Jeśli używasz programu Visual Studio 2015 lub 2017, zwróć uwagę, że przed uruchomieniem aplikacji hello lokalnie, należy zmienić hello `Data Source` częścią hello parametry połączenia bazy danych LocalDB programu SQL Server w plikach Web.config i App.config hello z `Data Source=(localdb)\v11.0` zbyt`Data Source=(LocalDb)\MSSQLLocalDB`.

> [!NOTE]
> <a name="note"></a>W tym samouczku musi mieć toocomplete konto platformy Azure:
>
> * Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): otrzymasz kredyt, że można użyć tootry limit płatnej usług Azure, a nawet po wyczerpaniu, można zachować hello konto i korzystać z bezpłatnych usług platformy Azure, takich jak witryny sieci Web. Karty kredytowej nigdy nie zostanie obciążona, chyba że jawnie zmienić ustawienia i poproś toobe obciążona.
> * Możesz [aktywowania Azure miesięczne środki dla subskrybentów usługi Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): subskrypcji otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.
>
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
>
>

## <a id="learn"></a>Dowiesz się
Witaj samouczek pokazuje, jak hello toodo następujące zadania:

* Włącz komputer dla rozwoju platformy Azure, instalując hello zestawu SDK platformy Azure (tylko dla programu Visual Studio 2013 i użytkowników 2015).
* Utwórz projekt aplikacji konsoli, która automatycznie wdraża jako zadanie WebJob platformy Azure, podczas wdrażania projektu sieci web skojarzony hello.
* Przetestuj zestaw SDK zadań Webjob wewnętrznej bazy danych lokalnie na komputerze dewelopera hello.
* Publikowanie aplikacji z aplikacją sieci web tooa zadań Webjob wewnętrznej bazy danych w usłudze App Service.
* Przekazywanie plików i przechowywania ich w hello usługi obiektów Blob platformy Azure.
* Za pomocą hello Azure WebJobs SDK toowork obiektów blob i kolejek usługi Azure Storage.

## <a id="contosoads"></a>Architektura aplikacji
Witaj Przykładowa aplikacja korzysta hello [wzorzec skoncentrowane kolejki pracy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff obciążenia roboczego hello użycie Procesora CPU tworzenia miniatur tooa wewnętrznej bazy danych procesu.

Aplikacja Hello przechowuje reklamy w bazie danych SQL przy użyciu programu Entity Framework Code First toocreate hello tabel i uzyskiwanie dostępu do danych hello. W przypadku każdej reklamy baza danych hello zawiera dwa adresy URL: jeden dla hello obrazu w pełnym rozmiarze i jeden dla hello miniatur.

![Tabela reklam](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

Gdy użytkownik przesyła obraz, hello aplikacji sieci web zapisuje obraz powitania w [obiektów blob platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), zawierający informacje ad hello w bazie danych hello adres URL, który wskazuje toohello obiektu blob. At hello sama godzina, zapisuje komunikat tooan kolejki systemu Azure. W ramach procesu zaplecza uruchomiony jako zadanie WebJob platformy Azure hello zestaw SDK zadań Webjob sonduje hello kolejki wiadomości. Gdy pojawi się nowy komunikat, hello zadania WebJob tworzy miniaturę obrazu i aktualizacje hello miniatur pole bazy danych adresu URL dla danej reklamy. Poniżej przedstawiono diagram pokazujący sposób interakcji hello części aplikacji hello:

![Architektura aplikacji Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
instrukcje w samouczku dotyczą Hello zastosować tooAzure zestawu SDK dla platformy .NET 2.7.1 lub nowszej.

## <a id="storage"></a>Tworzenie konta usługi Azure Storage
Konto magazynu platformy Azure udostępnia zasoby do przechowywania danych kolejek i obiektów blob w chmurze hello. Jest on również używany przez hello dane rejestrowania toostore zestaw SDK zadań Webjob dla pulpitu nawigacyjnego hello.

W przypadku aplikacji rzeczywistych można zwykle utworzyć oddzielne konta dla danych aplikacji porównywanych z danymi rejestrowania oraz oddzielne konta dla danych testowych porównywanych z danymi produkcyjnymi. W tym samouczku będzie używane tylko jedno konto.

1. Otwórz hello **Eksploratora serwera** okna w programie Visual Studio.
2. Kliknij prawym przyciskiem myszy hello **Azure** węzeł, a następnie kliknij przycisk **połączyć tooMicrosoft subskrypcji platformy Azure...** .
   
   ![Połącz tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. Zaloguj się przy użyciu poświadczeń konta platformy Azure.
4. Kliknij prawym przyciskiem myszy **magazynu** w obszarze hello Azure węzeł, a następnie kliknij przycisk **Utwórz konto magazynu**.
   
   ![Tworzenie konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. W hello **Utwórz konto magazynu** okna dialogowego, wprowadź nazwę konta magazynu hello.

    Nazwa Hello musi być muszą być unikatowe (inne konto magazynu platformy Azure może mieć hello tej samej nazwy). Jeśli wprowadzona nazwa hello jest już używana, otrzymasz toochange szansy go.

    Witaj tooaccess adres URL konta magazynu będzie *{nazwa}*. core.windows.net.
6. Zestaw hello **Region lub grupę koligacji** tooyou najbliższy region toohello listy rozwijanej.

    To ustawienie określa, w którym Centrum danych Azure będą obsługiwać Twoje konto magazynu. W tym samouczku wybór nie należy to znaczącej różnicy. Jednak w przypadku aplikacji sieci web produkcji ma serwera sieci web i toobe konta magazynu, korzystając z hello tego samego regionu toominimize opóźnienia i danych wyjściowych opłat. Aplikacja sieci web Hello (co należy utworzyć później) powinna być centrum danych, jak to możliwe przeglądarki toohello uzyskiwanie dostępu do aplikacji sieci web hello w kolejności toominimize opóźnienia.
7. Zestaw hello **replikacji** listy rozwijanej liście zbyt**magazyn lokalnie nadmiarowy**.

    Jeśli replikacja geograficzna jest włączona dla konta magazynu, hello przechowywana zawartość jest lokalizacji tooenable dodatkowego centrum danych replikowanych tooa toothat trybu failover w przypadku poważnej awarii w lokalizacji głównej hello. Replikacja geograficzna może pociągnąć za sobą dodatkowe koszty. W przypadku kont testowych i programistycznych zwykle nie chcesz toopay za replikację geograficzną. Aby uzyskać więcej informacji, zobacz temat dotyczący [tworzenia i usuwania konta magazynu oraz zarządzania nim](../storage/common/storage-create-storage-account.md).
8. Kliknij przycisk **Utwórz**.

    ![Nowe konto usługi Storage](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>Pobieranie aplikacji hello
1. Pobierz i Rozpakuj hello [ukończone rozwiązanie](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).
2. Uruchom program Visual Studio.
3. Z hello **pliku** menu wybierz **Otwórz > Projekt/rozwiązanie**, przejdź toowhere pobranego rozwiązania hello, a następnie otwórz plik rozwiązania hello.
4. Naciśnij klawisze CTRL + SHIFT + B toobuild hello rozwiązania.

    Domyślnie program Visual Studio automatycznie przywraca zawartość pakietu NuGet hello, która nie została uwzględniona w hello *.zip* pliku. Jeśli hello pakiety nie zostaną przywrócone, zainstaluj je ręcznie, przechodząc toohello **Zarządzaj pakietami NuGet dla rozwiązania** okno dialogowe i klikając hello **przywrócić** przycisk na powitania w prawym górnym narożniku.
5. W **Eksploratora rozwiązań**, upewnij się, że **ContosoAdsWeb** został wybrany jako projekt startowy hello.

## <a id="configurestorage"></a>Skonfiguruj toouse aplikacji hello konta magazynu
1. Otwórz aplikację hello *Web.config* plik w projekcie ContosoAdsWeb hello.

    Plik Hello zawiera parametry połączenia SQL i parametry połączenia magazynu Azure do pracy z obiektów blob i kolejek.

    Witaj parametrów połączenia SQL punkty tooa [programu SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) bazy danych.

    Parametry połączenia magazynu Hello jest przykład symbole zastępcze hello magazynu konta nazwy i klucza dostępu. Będzie to Zastąp z parametrów połączenia, które ma hello nazwy i klucza konta magazynu.  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    Parametry połączenia magazynu Hello nosi nazwę AzureWebJobsStorage ponieważ jest to hello nazwa hello, używanych przez zestaw SDK zadań Webjob domyślnie. Witaj, tej samej nazwy jest używana w tym miejscu, więc wartość ciągu tylko jedno połączenie tooset hello środowiska platformy Azure.
2. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy konto magazynu w obszarze hello **magazynu** węzeł, a następnie kliknij przycisk **właściwości**.

    ![Kliknij przycisk Właściwości konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. W hello **właściwości** okna, kliknij przycisk **klucze konta magazynu**, a następnie kliknij przycisk wielokropka hello.

    ![Klucze konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. Kopiuj hello **ciąg połączenia**.

    ![Okno dialogowe klucze konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. Zastąp parametry połączenia magazynu hello w hello *Web.config* pliku przy użyciu parametrów połączenia hello został skopiowany. Upewnij się, że zaznaczono wszystkie elementy wewnątrz cudzysłowów hello, ale bez znaków cudzysłowu hello przed wklejeniem.
6. Otwórz hello *App.config* plik w projekcie ContosoAdsWebJob hello.

    Ten plik zawiera dwa parametry połączenia magazynu, jeden dla danych aplikacji i jeden dla rejestrowania. Możesz użyć oddzielny magazyn kont dla danych aplikacji i rejestrowania i można użyć [konta wielu magazynu dla danych](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs). W tym samouczku użyjesz konto jednego magazynu. Parametry połączenia Hello ma symbole zastępcze klucze konta magazynu hello.

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

    Domyślnie parametry połączenia o nazwie AzureWebJobsStorage i AzureWebJobsDashboard szuka hello zestaw SDK zadań Webjob. Alternatywnie, można [przechowywanie parametrów połączenia hello, jednak mają i przekazać go w jawnie toohello `JobHost` obiektu](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).
7. Zastąp parametry połączenia magazynu hello parametry połączenia, które wcześniej zostały skopiowane.
8. Zapisz zmiany.

## <a id="run"></a>Uruchamianie aplikacji hello lokalnie
1. toostart hello sieci web frontonu aplikacji hello, naciśnij kombinację klawiszy CTRL + F5.

    Witaj domyślnej przeglądarce otworzy toohello strony głównej. (hello projektu sieci web jest uruchamiana, ponieważ wprowadzono go hello projekt startowy.)

    ![Strona główna aplikacji contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. toostart hello zadania WebJob zaplecza aplikacji hello, kliknij prawym przyciskiem myszy projekt ContosoAdsWebJob hello w **Eksploratora rozwiązań**, a następnie kliknij przycisk **debugowania** > **Start nowe wystąpienie** .

    Okno aplikacji konsoli otwiera i wyświetla rejestrowanie komunikatów wskazujący, że obiekt JobHost zestawu SDK zadań Webjob hello rozpoczęto toorun.

    ![Okno aplikacji konsoli przedstawiający tego hello wewnętrznej bazy danych jest uruchomiona.](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. W przeglądarce, kliknij przycisk **tworzenia Ad**.
4. Wprowadź dane testowe wybierz tooupload obrazu, a następnie kliknij przycisk **Utwórz**.

    ![Tworzenie strony](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    Aplikacja Hello przechodzi toohello strony indeksu, ale nie wyświetla miniatury nowej reklamy hello, ponieważ przetwarzanie nie zostało jeszcze przeprowadzone.

    W tym samym czasie po krótkim okresie oczekiwania komunikat rejestrowania w oknie aplikacji hello konsoli Pokazuje, że komunikatu w kolejce został odebrany i został przetworzony.

    ![Okno aplikacji konsoli przedstawiający przetworzeniu komunikatu w kolejce](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. Po hello rejestrowanie komunikatów w oknie aplikacji hello konsoli zostanie wyświetlony, Odśwież hello indeksu strony toosee hello miniatur.

    ![Strona indeksu](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. Kliknij przycisk **szczegóły** dla użytkownika ad toosee hello obrazu w pełnym rozmiarze.

    ![Strona szczegółów](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

Działała aplikacja hello na komputerze lokalnym i używa programu SQL Server, bazy danych znajdującej się na komputerze, ale działa w przypadku kolejek i obiektów blob w hello chmury. W następujących sekcji hello uruchomisz aplikacji hello w chmurze hello przy użyciu bazy danych w chmurze, a także chmury obiekty BLOB i kolejki.  

## <a id="runincloud"></a>Uruchamianie aplikacji hello w chmurze hello
Należy to zrobić hello następujące kroki toorun hello aplikacji w chmurze hello:

* Wdrażanie aplikacji tooWeb. Visual Studio automatycznie tworzy nową aplikację sieci web usługi aplikacji i wystąpienie bazy danych SQL.
* Skonfiguruj toouse aplikacji sieci web hello konta magazynu i bazy danych Azure SQL.

Po utworzeniu niektóre reklamy podczas uruchamiania w chmurze hello, zostanie wyświetlona hello rozbudowane funkcje ma toooffer hello toosee pulpitu nawigacyjnego zestaw SDK zadań Webjob.

### <a name="deploy-tooweb-apps"></a>Wdrażanie aplikacji tooWeb

1. Zamknij przeglądarkę hello i okna aplikacji hello konsoli.
2. Wykonaj kroki hello hello [publikowania tooAzure z bazy danych SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) sekcji.
3. Po wykonaniu kroków hello wdrażania, kontynuuj hello pozostałych zadań w tym artykule.

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a>Skonfiguruj toouse aplikacji sieci web hello konta magazynu i bazy danych Azure SQL
Ze względów bezpieczeństwa jest zbyt[należy unikać umieszczania poufne informacje, takie jak parametry połączenia w plikach, które są przechowywane w repozytoriach kodów źródłowych](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets). Platforma Azure udostępnia toodo sposób: można ustawić parametry połączenia i inne wartości ustawień, które znajdują się w hello środowiska platformy Azure i interfejsy API konfiguracji ASP.NET automatyczne pobranie te wartości po uruchomieniu aplikacji hello na platformie Azure. Te wartości zostaną ustawione na platformie Azure, używając **Eksploratora serwera**, hello portalu Azure, programu Windows PowerShell lub hello międzyplatformowego interfejsu wiersza polecenia. Aby uzyskać więcej informacji, zobacz [jak ciągi aplikacji i pracy ciągów połączenia](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).

W tej sekcji użyjesz **Eksploratora serwera** tooset wartości parametrów połączeń na platformie Azure.

1. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy aplikację sieci web, w obszarze **Azure > App Service > {grupie zasobów}**, a następnie kliknij przycisk **ustawienia widoku**.

    Witaj **aplikacji sieci Web Azure** na powitania zostanie otwarte okno **konfiguracji** kartę.
2. Zmień nazwę hello hello połączenia DefaultConnection połączenia ciąg toohello nazwy wybrania podczas konfigurowania bazy danych SQL hello w hello [publikowania tooAzure z bazy danych SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) artykułu.

    Podczas tworzenia aplikacji sieci web hello skojarzona baza danych, ma już wartość ciągu połączenia na odpowiednie hello Azure automatycznie utworzone te parametry połączenia. Zmieniasz właśnie toowhat nazwa hello, który potrzebuje kodu.
3. Dodaj dwa nowe parametry połączenia, o nazwie AzureWebJobsStorage i AzureWebJobsDashboard. Ustaw typ bazy danych hello zbyt**niestandardowy**i samą wartość, należy wcześniej używane dla hello zestaw hello połączenia ciągu wartości toohello *Web.config* i *App.config* plików. (Upewnij się, obejmują hello całego połączenia ciągu, nie tylko klucz dostępu hello i nie zawierają znaki cudzysłowu hello.)

    Te parametry połączenia są używane przez hello zestaw SDK zadań Webjob, jeden dla danych aplikacji i jeden dla rejestrowania. Jak przedstawiono wcześniej, hello, jeden dla danych aplikacji jest również używany przez kod frontonu sieci web hello.
4. Kliknij pozycję **Zapisz**.

    ![Parametry połączenia w portalu Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy hello aplikacji sieci web, a następnie kliknij przycisk **zatrzymać**.
6. Po zatrzymaniu hello aplikacji sieci web, ponownie kliknij prawym przyciskiem myszy hello aplikacji sieci web, a następnie kliknij przycisk **Start**.

   Hello zadania WebJob jest uruchamiana automatycznie, gdy opublikujesz, ale zatrzymuje go po wprowadzeniu zmiany konfiguracji. toorestart, możesz ponownie uruchomić aplikacji sieci web hello, lub uruchom ponownie zadanie WebJob hello w hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Aplikacja sieci web hello toorestart ogólnie zalecane jest po zmianie konfiguracji.
7. Odśwież okno przeglądarki hello zawierający adres URL aplikacji sieci web hello na jego pasku adresu.

    zostanie wyświetlona strona główna Hello.
8. Utwórz reklamę, jak w przypadku należy [uruchomiono lokalnie aplikacji hello](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).

   Strona indeksu Hello pokazuje bez miniatur na początku.
9. Odśwież stronę powitania po kilku sekundach i hello miniatur zostanie wyświetlone.

   Jeśli nie ma miniatury hello, może być toowait minuty hello toorestart zadania WebJob. Jeśli po chwili, nadal nie widać miniatur powitania po odświeżeniu strony hello, hello zadania WebJob może nie został uruchomiony automatycznie. W takim przypadku przejdź toohello **usługi aplikacji** bloku w hello [portalu Azure](https://portal.azure.com/), Znajdź aplikację sieci web, a następnie kliknij przycisk **Start**.

### <a name="view-hello-webjobs-sdk-dashboard"></a>Witaj widoku pulpitu nawigacyjnego zestaw SDK zadań Webjob
1. W hello [portalu Azure](https://portal.azure.com/), wybierz pozycję hello **blok App Services**Znajdź aplikację sieci web i zaznacz **Webjob**.
3. Wybierz hello **dzienniki** kartę.

    ![Karta dzienniki](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    Na nowej karcie przeglądarki zostanie otwarty toohello zestaw SDK zadań Webjob pulpitu nawigacyjnego. pulpit nawigacyjny Hello zawiera ten hello zadania WebJob działa i jest to lista funkcji w kodzie tego hello wyzwolenia przez zestaw SDK zadań Webjob.
4. Kliknij jeden z hello funkcje toosee szczegóły jego wykonywania.

    ![Zestaw SDK zadań Webjob pulpitu nawigacyjnego](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Zestaw SDK zadań Webjob pulpitu nawigacyjnego](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    Witaj **funkcja powtarzania** przycisk powoduje, że zestaw SDK zadań Webjob hello framework toocall hello funkcja ponownie i udostępnia funkcję toohello szansy toochange hello danych przekazanych najpierw.

> [!NOTE]
> Po zakończeniu testowania, rozważ usunięcie aplikacji sieci web hello, konta magazynu i wystąpienie bazy danych SQL. Aplikacja sieci web Hello jest bezpłatne, ale hello konta magazynu SQL i wystąpienie bazy danych Naliczanie opłat (aczkolwiek, minimalna powodu toohello mały rozmiar). Ponadto pozostawienie hello aplikacji sieci web, każda osoba, która znajdzie adres URL można tworzyć i wyświetlać reklamy. 
>
>

### <a name="delete-your-web-app"></a>Usuń aplikację sieci web
W portalu hello Przejdź toohello **usługi aplikacji** bloku, Znajdź i wybierz aplikację sieci web, a następnie kliknij **usunąć**. Wystarczy tootemporarily uniemożliwić innym użytkownikom dostęp do aplikacji sieci web hello, kliknij przycisk **zatrzymać** zamiast tego. W takim przypadku opłaty będą nadal tooaccrue dla hello bazy danych SQL i konto magazynu.

### <a name="delete-your-storage-account"></a>Usuwanie konta magazynu
toodelete Twojego konta magazynu, zobacz [usuwania konta magazynu](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account). 

### <a name="delete-your-database"></a>Usunięcie bazy danych
toodelete Twojego SQL bazy danych, zobacz hello [interfejsu API REST bazy danych SQL Azure](https://docs.microsoft.com/rest/api/sql/) dokumentacji.

## <a id="create"></a>Tworzenie aplikacji hello od początku
W tej sekcji należy wykonać hello następujących zadań:

* Tworzenie rozwiązania Visual Studio z projektu sieci web.
* Dodawanie projektu biblioteki klas danych hello warstwy dostępu, która jest udostępniana między hello frontonu i zaplecza.
* Dodaj projekt aplikacji konsoli hello wewnętrznej bazy danych, z włączonym wdrażaniem zadań Webjob.
* Dodawanie pakietów NuGet.
* Ustawianie odwołań do projektu.
* Skopiuj pliki kodu i konfiguracji aplikacji z aplikacji hello pobrane, który pracuje z hello w poprzedniej sekcji samouczka hello.
* Przejrzyj hello hello istotnych częściach kodu pracy z kolejkami i obiekty BLOB platformy Azure i hello zestaw SDK zadań Webjob.

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>Tworzenie rozwiązań programu Visual Studio z projektu sieci web i projektu biblioteki klas
1. W programie Visual Studio, wybierz **pliku** > **nowy** > **projektu**.
2. W hello **nowy projekt** okno dialogowe, wybierz **Visual C#** > **Web** > **aplikacji sieci Web platformy ASP.NET (.NET Framework)**.
3. Nazwa hello projekt ContosoAdsWeb, nazwa rozwiązania hello ContosoAdsWebJobsSDK (zmienić nazwy rozwiązania hello, jeśli chcesz umieścić go w hello tym samym folderze co hello pobrane rozwiązanie), a następnie kliknij przycisk **OK**.

    ![Nowy projekt](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. W hello **nowej aplikacji sieci Web ASP.NET** okno dialogowe, wybierz szablon MVC hello, a następnie wybierz **Zmień uwierzytelnianie**.

    ![Zmienianie uwierzytelniania](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. W hello **Zmień uwierzytelnianie** okno dialogowe, wybierz **bez uwierzytelniania**, a następnie kliknij przycisk **OK**.

    ![Bez uwierzytelniania](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. W hello **nowej aplikacji sieci Web ASP.NET** okna dialogowego, kliknij przycisk **OK**.

    Program Visual Studio tworzy rozwiązanie hello i hello projektu sieci web.
7. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy rozwiązanie hello (nie projekt hello) i wybierz **Dodaj** > **nowy projekt**.
8. W hello **Dodawanie nowego projektu** okno dialogowe, wybierz **Visual C#** > **Windows Desktop klasycznego** > **klasy biblioteki (.NET Framework)** szablonu.  
9. Nazwa projektu hello *ContosoAdsCommon*, a następnie kliknij przycisk **OK**.

    Ten projekt będzie zawierał hello kontekstu programu Entity Framework i hello modelu danych, które zarówno hello frontonu i użyje zaplecza. Alternatywnie można zdefiniować klasy związane z platformą EF hello w hello projektu sieci web i odwoływać się do tego projektu z projektu zadania WebJob hello. Ale następnie projektu zadania WebJob musi zestawów tooweb odwołań, których nie potrzebuje.

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>Dodaj projekt aplikacji konsoli z włączonym wdrażaniem zadań Webjob
1. Kliknij prawym przyciskiem myszy projekt sieci web hello (nie hello rozwiązania lub projektu biblioteki klas hello), a następnie kliknij przycisk **Dodaj** > **nowy projekt zadania WebJob Azure**.

    ![Nowe zaznaczenie menu projektu zadania WebJob platformy Azure](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. W hello **dodać zadania WebJob Azure** okna dialogowego, wprowadź ContosoAdsWebJob jako zarówno hello **Nazwa projektu** i hello **Nazwa zadania WebJob**. Pozostaw **tryb uruchomienia zadania WebJob** ustawić także**Uruchom stale**.
3. Kliknij przycisk **OK**.

   Program Visual Studio tworzy aplikacja Konsolowa, która jest skonfigurowana toodeploy jako zadanie WebJob zawsze, gdy wdrażanie projektu sieci web hello. toodo, jego wykonanie hello następujące zadania po utworzeniu projektu hello:

   * Dodaje *zadania webjob publikowania settings.json* plików w folderze właściwości projektu zadania WebJob hello.
   * Dodaje *list.json webjob* plików w folderze właściwości projektu sieci web hello.
   * Zainstalowany pakiet Microsoft.Web.WebJobs.Publish NuGet hello w hello projektu zadania WebJob.

   Aby uzyskać więcej informacji na temat tych zmian, zobacz [jak toodeploy zadań Webjob za pomocą programu Visual Studio](websites-dotnet-deploy-webjobs.md).

### <a name="add-nuget-packages"></a>Dodawanie pakietów NuGet
Witaj nowy projekt szablonu projektu zadania WebJob automatycznie instaluje pakiet NuGet zestawu SDK zadań Webjob hello [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) i jego zależności.

Jeden z hello jest zestaw SDK zadań Webjob zależności, które jest instalowane automatycznie w projektu zadania WebJob hello hello Azure magazynu klienta biblioteki (SCL). Jednak należy tooadd go toowork projektu sieci web toohello z obiektów blob i kolejek.

1. Otwórz hello **Zarządzaj pakietami NuGet** okna dialogowego hello rozwiązania.
2. Wybierz w okienku po lewej stronie powitania **zainstalowane pakiety**.
3. Znajdź hello *usługi Azure Storage* pakietu, a następnie kliknij przycisk **Zarządzaj**.
4. W hello **Wybierz projekty** okno, wybierz hello **ContosoAdsWeb** pole wyboru, a następnie kliknij przycisk **OK**.

    Wszystkie trzy projekty za pomocą toowork Entity Framework hello danych w bazie danych SQL.
5. Wybierz w okienku po lewej stronie powitania **Online**.
6. Znajdź hello *EntityFramework* NuGet pakietu, a następnie zainstaluj go we wszystkich trzech projektach.

### <a name="set-project-references"></a>Ustawianie odwołań do projektu
Sieć web i projektów zadania WebJob pracy z hello bazy danych SQL, tak zarówno wymagane odwołanie do projektu ContosoAdsCommon toohello.

1. W projekcie ContosoAdsWeb hello Ustaw odwołanie do projektu ContosoAdsCommon toohello. (Kliknij prawym przyciskiem myszy projekt ContosoAdsWeb hello, a następnie kliknij przycisk **Dodaj** > **odwołania**. 
2. W hello **Menedżera odwołań** okno dialogowe, wybierz opcję **projekty** > **rozwiązania** > **ContosoAdsCommon**, a następnie kliknij przycisk **OK**.)
   
    Witaj projektu zadania WebJob musi odwołania do pracy z obrazami i uzyskać dostęp do parametrów połączenia.

4. W projekcie ContosoAdsWebJob hello Ustaw odwołanie za`System.Drawing` i `System.Configuration`.

### <a name="add-code-and-configuration-files"></a>Dodawanie plików kodu i konfiguracji
W tym samouczku nie pokazuje sposób zbyt[utworzyć przy użyciu funkcji szkieletów widoków i kontrolerów MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), jak za[pisania kodu programu Entity Framework, który współpracuje z baz danych programu SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), lub [hello podstawy Programowanie w programie ASP.NET 4.5 asynchroniczne](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async). Tak, czy pozostaje toodo jest kopiowania kodu i plików konfiguracji z rozwiązania hello pobrane do hello nowego rozwiązania. Po wykonaniu tej czynności, hello sekcje Pokaż i objaśnione części hello kodu.

pliki tooadd tooa projektu lub folderu, kliknij prawym przyciskiem myszy projekt hello lub folderu i kliknij przycisk **Dodaj** > **istniejący element**. Wybierz hello pliki chcesz i kliknij przycisk **Dodaj**. Jeśli zostanie wyświetlone pytanie, czy tooreplace istniejące pliki, kliknij przycisk **tak**.

1. W projekcie ContosoAdsCommon hello Usuń hello *Class1.cs* i Dodaj w jego hello miejsce następujące pliki z projektu hello pobrane.

   * *AD.CS*
   * *ContosoAdscontext.cs*
   * *BlobInformation.cs*
2. W projekcie ContosoAdsWeb hello Dodaj hello następujące pliki z projektu hello pobrane.

   * *Plik Web.config*
   * *Global.asax.CS*  
   * W hello *kontrolerów* folder: *AdController.cs*
   * W hello *Views\Shared* folder: *_Layout.cshtml* pliku
   * W hello *Views\Home* folder: *Index.cshtml*
   * W hello *Views\Ad* folder (najpierw utwórz hello folder): pięć *.cshtml* plików
3. W projekcie ContosoAdsWebJob hello Dodaj hello następujące pliki z projektu hello pobrane.

   * *App.config* (Zmień filtr typu pliku hello zbyt**wszystkie pliki**)
   * *Plik program.CS*
   * *Functions.CS*

Można teraz utworzyć, uruchamiania i wdrażania aplikacji hello zgodnie z instrukcjami podanymi wcześniej w samouczku hello. Przed tym, jednak zatrzymać hello zadania WebJob, który jest nadal uruchomione w hello pierwszej aplikacji sieci web wdrożonej w. W przeciwnym razie wartość tego zadania WebJob będzie przetwarzać komunikaty z kolejki utworzony lokalnie lub przez hello uruchomieniu aplikacji w nowej aplikacji sieci web, ponieważ wszystkie przy użyciu hello sam konta magazynu.

## <a id="code"></a>Kod aplikacji hello przeglądu
Witaj poniższe sekcje zawierają opis kodu hello związane z tooworking z hello zestaw SDK zadań Webjob i obiektów blob magazynu Azure i kolejek.

> [!NOTE]
> Dla hello kodu toohello określonego zestawu SDK zadań Webjob, przejdź toohello [Program.cs i Functions.cs](#programcs) sekcje.
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon — Ad.cs
Witaj plik Ad.cs definiuje wyliczenia związane z kategoriami reklam i klasą jednostki POCO dla informacji o reklamach.

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
Witaj klasa ContosoAdsContext Określa, czy klasa Ad hello jest używany w kolekcji DbSet Entity Framework są przechowywane w bazie danych SQL.

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

Klasa Hello ma dwa konstruktory. najpierw Hello jest używany przez hello projektu sieci web i określa nazwę parametrów połączenia, które są przechowywane w pliku Web.config hello lub środowisko uruchomieniowe Azure hello hello. Witaj drugi Konstruktor umożliwia toopass w hello rzeczywistych parametrów połączenia. Są one wymagane projektu zadania WebJob hello ponieważ nie ma on pliku Web.config. Wcześniej przedstawiono gdzie te parametry połączenia są przechowywane i pojawi się później, jak hello kod pobiera parametry połączenia hello podczas tworzenia wystąpień klasy DbContext hello.

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon — BlobInformation.cs
Witaj `BlobInformation` klasa jest używana toostore informacji na temat obiekt blob obrazu w komunikatu w kolejce.

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
Kod, który jest wywoływany z hello `Application_Start` metoda tworzy *obrazów* kontenera obiektów blob i *obrazów* kolejki, jeśli jeszcze nie istnieje. Dzięki temu, że przy każdym uruchomieniu przy użyciu nowego konta magazynu, hello wymagane, kolejka i kontener obiektów blob są tworzone automatycznie.

Witaj konta magazynu toohello kod pobiera dostępu przy użyciu parametrów połączenia magazynu hello z hello *Web.config* pliku lub środowisko uruchomieniowe platformy Azure.

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

Następnie pobiera toohello odwołanie *obrazów* kontenera obiektów blob, tworzy kontener hello, jeśli jeszcze nie istnieje, i zestawów uprawnień dostępu na powitania nowy kontener. Domyślnie nowe kontenery Zezwalaj tylko klientów z obiektów blob tooaccess poświadczeń konta magazynu. Hello aplikacji sieci web wymaga hello publicznego toobe obiektów blob, aby możliwe było wyświetlanie obrazów przy użyciu adresów URL tego obiekty BLOB obrazów toohello punktu.

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

Podobny kod pobiera odwołanie toohello *thumbnailrequest* kolejki i tworzy nową kolejkę. W takim przypadku nie trzeba zmieniać uprawnień.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb — _Layout.cshtml
Witaj *_Layout.cshtml* plik ustawia nazwę aplikacji hello w hello nagłówku i stopce oraz utworzenie wpisu menu "Ads".

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb — Views\Home\Index.cshtml
Witaj *Views\Home\Index.cshtml* pliku wyświetla linków kategorii na stronie głównej hello. Witaj linki przekazują wartość całkowitą hello hello `Category` wyliczenia na stronie indeksu reklam toohello zmiennej querystring.

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb — AdController.cs
W hello *AdController.cs* plik, hello wywołania konstruktora hello `InitializeStorage` — metoda toocreate biblioteki klienta magazynu Azure obiektów, które zapewniają interfejs API do pracy z obiektów blob i kolejek.

Następnie kod hello pobiera toohello odwołanie *obrazów* kontenera obiektów blob, jak przedstawiono wcześniej w *Global.asax.cs*. Podczas wykonywania, który, ustawia domyślną [zasady ponawiania](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) odpowiednie dla aplikacji sieci web. zasady ponawiania wykładniczego wycofywania domyślne Hello mogą powodować zawieszanie aplikacji sieci web hello przez czas dłuższy niż minuta w przypadku kolejnych prób błędu przejściowego. Witaj zasady ponawiania określone w tym miejscu czeka trzy sekundy po każdej się toothree prób.

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

Podobny kod pobiera odwołanie toohello *obrazów* kolejki.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

Większość kodu kontrolera hello jest typowa dla pracy z modelem danych programu Entity Framework za pomocą klasy DbContext. Wyjątkiem jest hello HttpPost `Create` metodę, która przekazuje plik i zapisuje je w magazynie obiektów blob. udostępnia integratora modelu Hello [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) obiekt toohello metody.

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

Użytkownika hello zaznaczenie tooupload pliku, kod hello hello plik zostanie przesłany, zapisuje go w obiekcie blob i aktualizacji rekordu bazy danych Ad hello adres URL, który wskazuje obiekt blob toohello.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

Witaj kod hello przekazywania jest hello `UploadAndSaveBlobAsync` metody. Tworzy nazwę identyfikatora GUID dla obiektu blob hello, przekazywanie i zapisuje plik hello i zwraca odwołanie do obiektu blob toohello zapisane.

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

Po hello HttpPost `Create` metoda przekazuje obiekt blob i aktualizacje hello bazy danych, tworzy kolejki wiadomości tooinform hello zaplecza proces że obraz jest gotowy do konwersji tooa miniatur.

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

Witaj kod hello HttpPost `Edit` metoda jest podobny, z wyjątkiem tego, że jeśli hello użytkownik wybierze nowy plik obrazu, należy usunąć wszystkie obiekty BLOB, które już istnieją dla tej usługi ad.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

Oto kod hello usuwania obiektów blob podczas usuwania reklamy:

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
Witaj *Index.cshtml* służy do wyświetlania miniatury z hello innymi danymi reklamy:

        <img  src="@Html.Raw(item.ThumbnailURL)" />

Witaj *Details.cshtml* pliku wyświetla obrazu w pełnym rozmiarze hello:

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb — Views\Ad\Create.cshtml i Edit.cshtml
Witaj *Create.cshtml* i *Edit.cshtml* pliki określają kodowanie, że umożliwia hello hello tooget kontrolera formularza `HttpPostedFileBase` obiektu.

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

`<input>` Informuje hello przeglądarki tooprovide okna dialogowego wyboru pliku.

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob - Program.cs
Gdy hello uruchamia zadania WebJob hello `Main` wywołania metody hello zestaw SDK zadań Webjob `JobHost.RunAndBlock` wykonywania toobegin metody funkcji wyzwalanych na powitania bieżącego wątku.

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>Metoda GenerateThumbnail ContosoAdsWebJob - Functions.cs-
zestaw SDK zadań Webjob Hello wywołuje tę metodę po odebraniu komunikatu w kolejce. Metoda Hello tworzy miniaturę i naraża hello miniatur adres URL w hello bazy danych.

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
            // be instantiated and disposed within hello function.
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

* Witaj `QueueTrigger` atrybutu kieruje hello toocall zestaw SDK zadań Webjob tę metodę po odebraniu nowej wiadomości w kolejce thumbnailrequest hello.

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    Witaj `BlobInformation` obiekt hello kolejki wiadomości jest automatycznie zdeserializowany do hello `blobInfo` parametru. Po ukończeniu metody hello, komunikatu w kolejce hello jest usuwana. W przypadku niepowodzenia przed wykonaniem metody hello hello kolejka komunikatów nie zostanie usunięta; Po wygaśnięciu dzierżawy 10-minutowych wiadomość hello jest wydanych toobe pobrana ponownie i przetwarzane. Ta sekwencja nie należy powtórzyć przez czas nieokreślony, jeśli komunikat zawsze powoduje zgłoszenie wyjątku. Po 5 nieudanych próbach tooprocess wiadomości, wiadomość hello jest przeniesionego tooa kolejki o nazwie {queuename}-skażone. konfiguruje się Hello maksymalną liczbę prób.
* Witaj dwie `Blob` atrybuty Podaj obiektów, które są powiązane tooblobs: jeden toohello istniejący obiekt blob obrazu i jeden tooa nowego obiektu blob miniatury tworzącą hello metody.

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    Nazwy obiektów blob pochodzą z właściwości hello `BlobInformation` obiektu otrzymane w wiadomości powitania kolejki (`BlobName` i `BlobNameWithoutExtension`). tooget hello pełną funkcjonalność hello biblioteki klienta usługi Storage, można użyć hello `CloudBlockBlob` toowork klasy z obiektami blob. Jeśli chcesz, aby tooreuse kod, który został zapisany toowork z `Stream` obiekty, można użyć hello `Stream` klasy.

Aby uzyskać więcej informacji na temat sposobu toowrite funkcje, które używane są atrybuty zestaw SDK zadań Webjob, zobacz hello następujące zasoby:

* [Jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Jak toouse Azure tabeli magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [W jaki sposób toouse usługa Azure Service Bus z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * Jeśli aplikacja sieci web jest uruchomiony na wiele maszyn wirtualnych, wielu zadań Webjob będzie działać jednocześnie, a w niektórych przypadkach może to spowodować hello sam danych przetwarzana wiele razy. Nie jest problem użycie hello wbudowanych kolejki, obiektów blob i wyzwalaczy usługi Service Bus. Hello SDK gwarantuje, że funkcje będą przetwarzane tylko raz dla każdego komunikatu lub obiektu blob.
> * Aby uzyskać informacje na temat łagodne zamykanie tooimplement, zobacz [łagodne zamykanie](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
> * Witaj kodu w hello `ConvertImageToThumbnailJPG` — metoda (tego nie pokazano) używa klas w hello `System.Drawing` przestrzeni nazw dla uproszczenia. Jednak klasy hello w tej przestrzeni nazw zostały zaprojektowane do użytku z formularzy systemu Windows. Nie są one obsługiwane w usłudze systemu Windows lub programu ASP.NET. Aby uzyskać więcej informacji o opcjach przetwarzania obrazu, zobacz [Dynamiczne generowanie obrazu](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) i [Bezpośrednie zmienianie rozmiaru obrazu](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="next-steps"></a>Następne kroki
W tym samouczku przedstawiono prostą aplikację wielowarstwową, która używa hello zestaw SDK zadań Webjob dla przetwarzania wewnętrznej bazy danych. Ta sekcja zawiera sugestie dotyczące dowiedzieć się więcej na temat aplikacje wielowarstwowe platformy ASP.NET i zadań Webjob.

### <a name="missing-features"></a>Brak funkcji
Aplikacja Hello została zachowana proste samouczek ułatwiający Rozpoczynanie pracy. W aplikacji rzeczywistych można zaimplementować [iniekcji zależności](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) i hello [repozytorium i jednostki pracy wzorce](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), użyj [interfejs umożliwiający rejestrowanie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), użyj [ Migracje EF Code First](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage danych modelu zmian i użyj [elastyczności połączenia platformy EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage przejściowe błędy sieciowym.

### <a name="scaling-webjobs"></a>Skalowanie zadania Webjob
Zadania Webjob są uruchamiane w kontekście hello aplikacji sieci web i nie są skalowalne oddzielnie. Na przykład jeśli jedno wystąpienie aplikacji sieci web Standard, można mieć tylko jedno wystąpienie procesu tła uruchomiona, a niektóre zasoby serwera hello (procesora CPU, pamięć, itp.), które w przeciwnym razie będą dostępne tooserve zawartości sieci web używa.

Jeśli ruch jest zależna od czasu dzień lub dzień tygodnia i czy zaplecza hello przetwarzania należy poczekać toodo, toorun Twojego zadań Webjob można zaplanować w czasie mniejszym natężeniu ruchu. Jeśli obciążenie hello nadal jest za duża dla tego rozwiązania, w tym celu można uruchomić hello wewnętrznej bazy danych jako zadanie WebJob w aplikacji sieci web oddzielnych dedykowanych. Aplikacja sieci web wewnętrznej bazy danych można następnie skalować niezależnie z aplikacji sieci web frontonu.

Aby uzyskać więcej informacji, zobacz [skalowanie zadania Webjob](websites-webjobs-resources.md#scale).

### <a name="avoiding-web-app-timeout-shut-downs"></a>Unikanie sieci web aplikacji limit czasu zamykania rozwijanych
czy toomake Twojego zadań Webjob zawsze są uruchomione i uruchomione na wszystkich wystąpień aplikacji sieci web, masz tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) funkcji.

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a>Przy użyciu hello zestaw SDK zadań Webjob poza zadań Webjob
Program, który używa hello zestaw SDK zadań Webjob nie ma toorun na platformie Azure w zadanie WebJob. Można uruchomić lokalnie i można również uruchomić w innych środowiskach, takich jak usługi w chmurze rola proces roboczy lub usługi systemu Windows. Jednak dostępne tylko hello zestaw SDK zadań Webjob pulpitu nawigacyjnego za pomocą aplikacji sieci web platformy Azure. pulpit nawigacyjny hello toouse masz tooconnect hello sieci web aplikacji toohello konto magazynu używane przez ustawienie parametrów połączenia AzureWebJobsDashboard hello na powitania **Konfiguruj** kartę hello klasycznego portalu. Następnie można uzyskać toohello pulpitu nawigacyjnego za pomocą hello następującego adresu URL:

https://{webappname}.SCM.azurewebsites.NET/azurejobs/#/Functions

Aby uzyskać więcej informacji, zobacz [pobierania pulpitu nawigacyjnego lokalnego środowiska deweloperskiego przy użyciu zestawu SDK zadań Webjob hello](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ale należy pamiętać, że widoczny jest stara nazwa ciągu połączenia.

### <a name="more-webjobs-documentation"></a>Więcej dokumentacji zadań Webjob
Aby uzyskać więcej informacji, zobacz [zasoby dokumentacji zadań Webjob Azure](http://go.microsoft.com/fwlink/?LinkId=390226).
