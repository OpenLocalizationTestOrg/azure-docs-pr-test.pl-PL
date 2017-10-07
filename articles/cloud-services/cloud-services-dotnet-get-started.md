---
title: "aaaGet do korzystania z usług Azure Cloud Services i programu ASP.NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate aplikację wielowarstwową przy użyciu platformy ASP.NET MVC i platformy Azure. Aplikacja Hello jest uruchamiana w usługi w chmurze z rolą sieci web i roli proces roboczy. Używa platformy Entity Framework, bazy danych SQL Database oraz obiektów blob i kolejek usługi Azure Storage."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a>Wprowadzenie do usług Azure Cloud Services i programu ASP.NET

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak toocreate wielowarstwową aplikację .NET z frontonem ASP.NET MVC frontonu, a następnie wdrożyć go tooan [usługi w chmurze Azure](cloud-services-choose-me.md). Aplikacja używa Hello [bazy danych SQL Azure](http://msdn.microsoft.com/library/azure/ee336279), hello [usługi obiektów Blob platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)i hello [usługi kolejek platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern). Możesz [pobrać projekt programu Visual Studio hello](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) z hello galerii kodu MSDN.

Witaj samouczek pokazuje, jak toobuild i uruchom hello aplikację lokalnie, jak toodeploy go tooAzure i hello uruchamiania w chmurze i w jaki sposób toobuild ją od podstaw. Można rozpocząć od kompilowania aplikacji od początku i hello testu i wdrożyć kroki później, jeśli wolisz.

## <a name="contoso-ads-application"></a>Aplikacja Contoso Ads
Aplikacja Hello jest reklamowa Tablica ogłoszeń. Aby utworzyć reklamę, użytkownicy muszą wpisać tekst i przesłać obraz. Widzą listę reklam z miniaturami obrazów i będą mogli wyświetlać obrazu w pełnym rozmiarze hello wybranie ad toosee hello szczegóły.

![Lista reklam](./media/cloud-services-dotnet-get-started/list.png)

Aplikacja Hello używa hello [wzorzec skoncentrowane kolejki pracy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff obciążenia roboczego hello użycie Procesora CPU tworzenia procesu zaplecza tooa miniatur.

## <a name="alternative-architecture-websites-and-webjobs"></a>Architektura alternatywna: witryny sieci Web i zadania WebJob
Ten samouczek pokazuje, jak toorun frontonu i zaplecza na platformie Azure w chmurze usługi. Alternatywą jest hello toorun frontonu w [witryny sieci Web Azure](/services/web-sites/) i użyj hello [Webjob](http://go.microsoft.com/fwlink/?LinkId=390226) funkcji (obecnie w wersji zapoznawczej) dla zaplecza hello. Samouczek korzystającym z zadań Webjob, zobacz [wprowadzenie hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md). Aby uzyskać informacji na temat sposobu toochoose hello usług najlepiej dopasować danego scenariusza, zobacz [porównanie witryn sieci Web platformy Azure, usługi w chmurze i maszyn wirtualnych](../app-service-web/choose-web-site-cloud-service-vm.md).

## <a name="what-youll-learn"></a>Zawartość
* Jak tooenable komputer dla rozwoju platformy Azure, instalując hello Azure SDK.
* Jak toocreate Visual Studio cloud projektu usługi z rolą sieci web platformy ASP.NET MVC i roli proces roboczy.
* Jak tootest hello projekt usługi w chmurze lokalnie, przy użyciu emulatora magazynu Azure hello.
* Jak toopublish hello chmury projektu tooan Azure usługa w chmurze i przetestować go przy użyciu konta magazynu platformy Azure.
* Jak tooupload pliki i przechowywać je w usłudze Azure Blob hello.
* Jak toouse hello usługi kolejek platformy Azure do komunikacji między warstwami.

## <a name="prerequisites"></a>Wymagania wstępne
Witaj samouczka przyjęto założenie, że rozumiesz [podstawowe pojęcia dotyczące usługi Azure cloud services](cloud-services-choose-me.md) takich jak *roli sieci web* i *roli procesu roboczego* terminologii.  Założono również, że wiesz, jak toowork z [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) lub [formularzy sieci Web](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projekty w programie Visual Studio. Hello Przykładowa aplikacja korzysta MVC, ale większość hello samouczka odnosi się także tooWeb formularzy.

Można uruchomić aplikacji hello lokalnie bez subskrypcji platformy Azure, ale należy jedna chmura toohello aplikacji hello toodeploy. Jeśli nie masz konta, możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) lub [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).

Hello instrukcje w samouczku dotyczą pracy z jednym z hello następujące produkty:

* Program Visual Studio 2013
* Visual Studio 2015
* Visual Studio 2017

Jeśli nie masz jeden z nich, Visual Studio może być zainstalowana automatycznie po zainstalowaniu hello Azure SDK.

## <a name="application-architecture"></a>Architektura aplikacji
Aplikacja Hello przechowuje reklamy w bazie danych SQL przy użyciu programu Entity Framework Code First toocreate hello tabel i uzyskiwanie dostępu do danych hello. W przypadku każdej reklamy hello bazy danych magazynów dwa adresy URL: jeden dla hello obrazu w pełnym rozmiarze i jeden do miniatury hello.

![Tabela reklam](./media/cloud-services-dotnet-get-started/adtable.png)

Gdy użytkownik przesyła obraz, hello fronton uruchomiony w roli sieć web zapisuje obraz powitania w [obiektów blob platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), zawierający informacje ad hello w bazie danych hello adres URL, który wskazuje toohello obiektu blob. At hello sama godzina, zapisuje komunikat tooan kolejki systemu Azure. Proces zaplecza uruchomiony w roli proces roboczy okresowo sonduje kolejkę hello nowych wiadomości. Gdy pojawi się nowy komunikat, hello roli proces roboczy tworzy miniaturę obrazu i aktualizacje hello miniatur pole bazy danych adresu URL dla danej reklamy. Witaj Poniższy diagram przedstawia interakcje hello części aplikacji hello.

![Architektura aplikacji Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a>Pobieranie i uruchamianie rozwiązania hello ukończone
1. Pobierz i Rozpakuj hello [ukończone rozwiązanie](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).
2. Uruchom program Visual Studio.
3. Z hello **pliku** menu wybierz **Otwórz projekt**, przejdź toowhere pobranego rozwiązania hello, a następnie otwórz plik rozwiązania hello.
4. Naciśnij klawisze CTRL + SHIFT + B toobuild hello rozwiązania.

    Domyślnie program Visual Studio automatycznie przywraca zawartość pakietu NuGet hello, która nie została uwzględniona w hello *.zip* pliku. Jeśli hello pakiety nie zostaną przywrócone, zainstaluj je ręcznie, przechodząc toohello **Zarządzaj pakietami NuGet dla rozwiązania** okno dialogowe i klikając hello **przywrócić** przycisk na powitania w prawym górnym narożniku.
5. W **Eksploratora rozwiązań**, upewnij się, że **ContosoAdsCloudService** został wybrany jako projekt startowy hello.
6. Jeśli używasz programu Visual Studio 2015 lub nowszego, Zmień parametry połączenia SQL Server hello w aplikacji hello *Web.config* pliku hello projektu ContosoAdsWeb i w hello *ServiceConfiguration.Local.cscfg* pliku projektu ContosoAdsCloudService hello. W każdym przypadku Zmień "(localdb) \v11.0" za "(localdb) \MSSQLLocalDB".
7. Naciśnij klawisze CTRL + F5 toorun hello aplikacji.

    Po uruchomieniu projektu usługi w chmurze lokalnie, Visual Studio automatycznie wywołuje hello Azure *emulator obliczeń* i Azure *emulatora magazynu*. Witaj obliczeniowe emulatora używa roli sieci web hello toosimulate zasoby komputera i środowisk roli procesu roboczego. Witaj emulator magazynu używa [programu SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) bazy danych magazynu w chmurze Azure toosimulate.

    Witaj pierwszego uruchomienia projektu usługi w chmurze, czas minuty toostart emulatory hello w górę. Po zakończeniu uruchamiania emulatora hello domyślnej przeglądarki powoduje otwarcie strony głównej aplikacji toohello.

    ![Architektura aplikacji Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. Kliknij przycisk **Create an Ad** (Utwórz reklamę).
9. Wprowadź dane testowe i wybierz *.jpg* tooupload obrazu, a następnie kliknij przycisk **Utwórz**.

    ![Tworzenie strony](./media/cloud-services-dotnet-get-started/create.png)

    Aplikacja Hello przechodzi toohello strony indeksu, ale nie wyświetla miniatury nowej reklamy hello, ponieważ przetwarzanie nie zostało jeszcze przeprowadzone.
10. Poczekaj chwilę, a następnie Odśwież hello indeksu strony toosee hello miniatur.

     ![Strona indeksu](./media/cloud-services-dotnet-get-started/list.png)
11. Kliknij przycisk **szczegóły** dla użytkownika ad toosee hello obrazu w pełnym rozmiarze.

     ![Strona szczegółów](./media/cloud-services-dotnet-get-started/details.png)

Działała aplikacja hello całkowicie na komputerze lokalnym, bez połączenia toohello chmury. Witaj emulator magazynu przechowuje hello kolejki i danych obiektów blob w bazie danych programu SQL Server Express LocalDB, a aplikacja hello przechowuje dane ad hello w innej bazie danych LocalDB. Bazy danych Entity Framework Code First automatycznie utworzone hello ad hello pierwszej aplikacji sieci web hello nastąpiła tooaccess go.

W powitania po sekcji skonfigurujesz hello rozwiązania toouse zasobów w chmurze Azure dla kolejek, obiektów blob i bazy danych aplikacji hello po uruchomieniu na powitania chmury. Jeśli poszukiwany toorun toocontinue lokalnie, ale użycia zasobów magazynu i bazy danych w chmurze, możesz to zrobić. Jest to jedynie ustawienia parametrów połączenia — pokażemy, jak toodo.

## <a name="deploy-hello-application-tooazure"></a>Wdrażanie tooAzure aplikacji hello
Należy to zrobić hello następujące kroki toorun hello aplikacji w chmurze hello:

* Utworzenie usługi w chmurze platformy Azure.
* Utworzenie bazy danych SQL Azure.
* Utworzenie konta magazynu platformy Azure.
* Skonfiguruj toouse rozwiązania hello bazy danych Azure SQL po uruchomieniu na platformie Azure.
* Skonfiguruj toouse rozwiązania hello konta magazynu Azure po uruchomieniu na platformie Azure.
* Wdróż hello projektu tooyour usługi w chmurze Azure.

### <a name="create-an-azure-cloud-service"></a>Tworzenie usługi w chmurze platformy Azure
Usługi w chmurze Azure to aplikacja hello środowiska hello jest uruchamiana w.

1. W przeglądarce otwórz hello [portalu Azure](https://portal.azure.com).
2. Kliknij kolejno pozycje **Nowe > Obliczenia > Usługa w chmurze**.

3. W hello DNS nazwy wejściowe wpisz prefiks adresu URL dla usługi w chmurze hello.

    Ten adres URL ma toobe unikatowy.  Zostanie wyświetlony komunikat o błędzie, jeśli prefiksu hello jest już używana.
4. Określ nową grupę zasobów dla usługi hello. Kliknij przycisk **Utwórz nowy** , a następnie wpisz nazwę w hello zasobów wejściowych pole grupy, takie jak CS_contososadsRG.

5. Wybierz region hello miejscu aplikacji hello toodeploy.

    To pole określa centrum danych, w którym będzie hostowana usługa w chmurze. W przypadku aplikacji produkcyjnej warto wybrać hello region najbliższy tooyour klientów. W tym samouczku wybierz hello region najbliższy tooyou.
5. Kliknij przycisk **Utwórz**.

    W hello po obrazu tworzona jest hello CSvccontosoads.cloudapp.net adres URL usługi w chmurze.

    ![Nowa usługa w chmurze](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a>Tworzenie bazy danych SQL Azure
Po uruchomieniu aplikacji hello w chmurze hello, będzie on używać bazy danych opartej na chmurze.

1. W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **nowy > baz danych > SQL Database**.
2. W hello **Nazwa bazy danych** wprowadź *contosoads*.
3. W hello **grupy zasobów**, kliknij przycisk **Użyj istniejącego** i grupy zasobów wybierz hello używane dla usługi w chmurze hello.
4. Na powitania po obrazu, kliknij **serwera — Skonfiguruj wymagane ustawienia** i **Utwórz nowy serwer**.

    ![Serwer toodatabase tunelu](./media/cloud-services-dotnet-get-started/newdb.png)

    Alternatywnie Jeśli subskrypcja obejmuje już serwer, z listy rozwijanej hello można wybrać tego serwera.
5. W hello **nazwy serwera** wprowadź *csvccontosodbserver*.

6. Wprowadź wartość **Nazwa logowania** i **Hasło** dla administratora.

    W przypadku wybrania opcji **Utwórz nowy serwer** nie wprowadzasz w tym miejscu istniejącej nazwy i hasła. Podajesz nową nazwę i hasło, że definiujesz teraz toouse później podczas uzyskiwania dostępu hello bazy danych. W przypadku wybrania wcześniej utworzonego serwera zostanie wyświetlony monit dla hello hasła toohello konta użytkownika administracyjnego już utworzone.
7. Wybierz hello sam **lokalizacji** wybraną hello usłudze w chmurze.

    Jeśli usługa w chmurze hello i bazy danych są w różnych centrach danych (różnych regionach), zwiększy się opóźnienie i możesz będą naliczane opłaty dotyczące przepustowości poza centrum danych hello. Przepustowość w centrum danych jest bezpłatna.
8. Sprawdź **Zezwalaj usługom platformy azure tooaccess serwera**.
9. Kliknij przycisk **wybierz** hello nowego serwera.

    ![Nowy serwer usługi SQL Database](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. Kliknij przycisk **Utwórz**.

### <a name="create-an-azure-storage-account"></a>Tworzenie konta usługi Azure Storage
Konto magazynu platformy Azure udostępnia zasoby do przechowywania danych kolejek i obiektów blob w chmurze hello.

W rzeczywistych aplikacjach przeważnie tworzy się oddzielne konta dla danych aplikacji porównywanych z danymi rejestrowania oraz oddzielne konta dla danych testowych porównywanych z danymi produkcyjnymi. W tym samouczku będzie używane tylko jedno konto.

1. W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **nowy > magazynu > Konto magazynu — obiekt blob, plików, tabeli, kolejki**.
2. W hello **nazwa** wpisz prefiks adresu URL.

    Ten prefiks i hello tekst wyświetlony w polu hello będzie konto magazynu tooyour unikatowy adres URL hello. Jeśli hello prefiks został już użyty przez innego użytkownika, będziesz mieć toochoose inny prefiks.
3. Zestaw hello **modelu wdrażania** za*klasycznego*.

4. Zestaw hello **replikacji** listy rozwijanej liście zbyt**magazyn lokalnie nadmiarowy**.

    Jeśli replikacja geograficzna jest włączona dla konta magazynu, hello przechowywana zawartość jest trybu failover tooenable dodatkowego centrum danych replikowanych tooa w przypadku poważnej awarii w lokalizacji głównej hello. Replikacja geograficzna może pociągnąć za sobą dodatkowe koszty. W przypadku kont testowych i programistycznych zwykle nie chcesz toopay za replikację geograficzną. Aby uzyskać więcej informacji, zobacz temat dotyczący [tworzenia i usuwania konta magazynu oraz zarządzania nim](../storage/common/storage-create-storage-account.md).

5. W hello **grupy zasobów**, kliknij przycisk **Użyj istniejącego** i grupy zasobów wybierz hello używane dla usługi w chmurze hello.
6. Zestaw hello **lokalizacji** toohello listy rozwijanej region wybrany dla usługi w chmurze hello wcześniej.

    Jeśli hello chmury usługi i konto magazynu są obsługiwane w różnych centrach danych (różnych regionach), zwiększy się opóźnienie i możesz będą naliczane opłaty dotyczące przepustowości poza centrum danych hello. Przepustowość w centrum danych jest bezpłatna.

    Grupy koligacji Azure udostępniają mechanizm toominimize hello odległości między zasobami w centrum danych, co może zmniejszyć opóźnienia. Ten samouczek nie korzysta z grup koligacji. Aby uzyskać więcej informacji, zobacz [jak tooCreate koligacji grupy w usłudze Azure](http://msdn.microsoft.com/library/jj156209.aspx).
7. Kliknij przycisk **Utwórz**.

    ![Nowe konto usługi Storage](./media/cloud-services-dotnet-get-started/newstorage.png)

    W obrazie hello utworzeniu konta magazynu z adresem URL hello `csvccontosoads.core.windows.net`.

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a>Skonfiguruj toouse rozwiązania hello bazy danych Azure SQL po uruchomieniu na platformie Azure
Witaj projektu sieci web i hello projektu roli proces roboczy każdy ma własne parametry połączenia bazy danych, a każdy z nich musi bazy danych Azure SQL toohello toopoint po uruchomieniu aplikacji hello na platformie Azure.

Użyjesz [przekształcenie pliku Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) dla roli sieci web hello i ustawienia środowiska usługi chmury hello roli procesu roboczego.

> [!NOTE]
> W tej sekcji i hello kolejnej sekcji poświadczenia są przechowywane w plikach projektu. [Nie należy przechowywać poufnych danych w publicznych repozytoriach kodów źródłowych](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).
>
>

1. W projekcie ContosoAdsWeb hello Otwórz hello *Web.Release.config* pliku transformacji dla aplikacji hello *Web.config* pliku, Usuń blok komentarza hello, który zawiera `<connectionStrings>` i Wklej Witaj następującego kodu w tym miejscu.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    Pozostaw hello plik jest otwarty do edycji.
2. W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **baz danych SQL** w okienku po lewej stronie powitania kliknij hello bazy danych utworzonej w ramach tego samouczka, a następnie kliknij **Pokaż parametry połączenia**.

    ![Pokazywanie parametrów połączeń](./media/cloud-services-dotnet-get-started/showcs.png)

    Hello portal zawiera parametry połączeń oraz symbol zastępczy hello hasła.

    ![Parametry połączeń](./media/cloud-services-dotnet-get-started/connstrings.png)
3. W hello *Web.Release.config* pliku przekształcenia, Usuń `{connectionstring}` i Wklej w jego miejscu hello parametrów połączenia ADO.NET z hello portalu Azure.
4. W parametrach połączenia hello wklejonych w hello *Web.Release.config* pliku przekształcenia, Zastąp `{your_password_here}` z hello hasło utworzone dla hello nowej bazy danych SQL.
5. Zapisz plik hello.  
6. Zaznacz i skopiuj parametry połączenia hello (bez hello znaki cudzysłowu otaczające) do użycia w hello następujące kroki dotyczące konfigurowania projektu roli proces roboczy hello.
7. W **Eksploratora rozwiązań**w obszarze **ról** w hello projekt usługi w chmurze, kliknij prawym przyciskiem myszy **ContosoAdsWorker** , a następnie kliknij przycisk **właściwości**.

    ![Właściwości roli](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. Kliknij przycisk hello **ustawienia** kartę.
9. Zmień **konfiguracji usługi** za**chmury**.
10. Wybierz hello **wartość** dla hello pole `ContosoAdsDbConnectionString` ustawienia, a następnie wklej parametry połączenia hello, które zostały skopiowane z poprzedniej sekcji samouczka hello hello.

     ![Parametry połączenia bazy danych dla roli Proces roboczy](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. Zapisz zmiany.  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a>Skonfiguruj toouse rozwiązania hello konta magazynu Azure po uruchomieniu na platformie Azure
Parametry połączenia konta magazynu platformy Azure dla projektu roli sieć web hello i projektu roli proces roboczy hello są przechowywane w ustawieniach środowiska w hello projekt usługi w chmurze. Dla każdego projektu istnieje osobny zestaw ustawień toobe używane po uruchomieniu aplikacji hello lokalnie, a po uruchomieniu na platformie hello chmury. Ustawienia środowiska chmury hello projektów ról sieć web i proces roboczy będzie aktualizowana.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **ContosoAdsWeb** w obszarze **ról** w hello **ContosoAdsCloudService** projektu, a następnie kliknij przycisk **Właściwości**.

    ![Właściwości roli](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. Kliknij przycisk hello **ustawienia** kartę. W hello **konfiguracji usługi** listy rozwijanej wybierz pozycję **chmury**.

    ![Konfiguracja chmury](./media/cloud-services-dotnet-get-started/sccloud.png)
3. Wybierz hello **StorageConnectionString** wpis, aby zobaczyć wielokropek (**... **) przycisk na prawym końcu wiersza hello hello. Kliknij przycisk hello tooopen przycisk wielokropka hello **Tworzenie parametrów połączenia konta magazynu** okno dialogowe.

    ![Otwieranie okna Tworzenie parametrów połączenia](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. W hello **utworzyć parametry połączenia magazynu** okno dialogowe, kliknij przycisk **subskrypcji**, wybierz konto magazynu hello, który został utworzony wcześniej, a następnie kliknij przycisk **OK**. Jeśli nie zalogowano się, zostanie wyświetlony monit o podanie poświadczeń konta systemu platformy Azure.

    ![Tworzenie parametrów połączenia usługi Storage](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. Zapisz zmiany.
6. Wykonaj hello same procedury, która została użyta w przypadku hello `StorageConnectionString` hello tooset ciąg połączenia `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` parametry połączenia.

    Te parametry są używane do rejestrowania.
7. Wykonaj hello same procedury, która została użyta w przypadku hello **ContosoAdsWeb** tooset roli parametry połączeń dla hello **ContosoAdsWorker** roli. Nie zapomnij tooset **konfiguracji usługi** za**chmury**.

ustawienia środowiska roli Hello skonfigurowane przy użyciu interfejsu użytkownika programu Visual Studio hello są przechowywane w hello następujące pliki w projekcie ContosoAdsCloudService hello:

* *ServiceDefinition.csdef* — definiuje nazwy ustawień hello.
* *ServiceConfiguration.Cloud.cscfg* — udostępnia wartości w przypadku uruchamiania aplikacji hello w chmurze hello.
* *ServiceConfiguration.Local.cscfg* — udostępnia wartości podczas uruchamiania aplikacji hello lokalnie.

Na przykład hello ServiceDefinition.csdef zawiera następujące definicje hello:

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

I hello *ServiceConfiguration.Cloud.cscfg* plik zawiera wartości hello wprowadzone dla tych ustawień w programie Visual Studio.

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

Witaj `<Instances>` ustawienie określa liczbę hello maszyn wirtualnych, które platforma Azure uruchomi proces roboczy hello kod roli na. Witaj [następne kroki](#next-steps) sekcja zawiera linki toomore informacji na temat skalowania usługi w chmurze

### <a name="deploy-hello-project-tooazure"></a>Wdrażanie hello tooAzure projektu
1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **ContosoAdsCloudService** projekt w chmurze, a następnie wybierz **publikowania**.

   ![Menu Publikowanie](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. W hello **Zaloguj** krok hello **publikowanie aplikacji platformy Azure** kreatora, kliknij przycisk **dalej**.

    ![Krok Logowanie](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. W hello **ustawienia** kroku kreatora powitania kliknij przycisk **dalej**.

    ![Krok Ustawienia](./media/cloud-services-dotnet-get-started/pubsettings.png)

    Witaj ustawienia domyślne w hello **zaawansowane** kartę są wystarczające w przypadku tego samouczka. Aby uzyskać informacje o karcie Zaawansowane hello, zobacz [Kreator publikowania aplikacji Azure](http://msdn.microsoft.com/library/hh535756.aspx).
4. W hello **Podsumowanie** kroku, kliknij przycisk **publikowania**.

    ![Krok Podsumowanie](./media/cloud-services-dotnet-get-started/pubsummary.png)

   Witaj **dziennika aktywności platformy Azure** w programie Visual Studio zostanie otwarte okno.
5. Kliknij przycisk Szczegóły wdrożenia hello tooexpand ikona hello strzałki w prawo.

    Witaj wdrażania może potrwać too5 minut lub więcej toocomplete.

    ![Okno Dziennik aktywności platformy Azure](./media/cloud-services-dotnet-get-started/waal.png)
6. Po zakończeniu stan wdrożenia powitania kliknij hello **adres URL aplikacji sieci Web** toostart hello aplikacji.
7. Teraz możesz przetestować aplikacji hello tworzenia, wyświetlając i edytując niektóre reklamy, tak jak po uruchomieniu aplikacji hello lokalnie.

> [!NOTE]
> Po zakończeniu testowania Usuń lub Zatrzymaj hello usługi w chmurze. Nawet jeśli nie używasz usługi w chmurze hello, jest Naliczanie opłat, ponieważ zasoby maszyny wirtualnej są zastrzeżone dla niego. Jeśli usługa będzie działać, każda osoba, która znajdzie adres URL, będzie mogła tworzyć i wyświetlać reklamy. W hello [portalu Azure](https://portal.azure.com), przejdź toohello **omówienie** dla usługi w chmurze, a następnie kliknij pozycję hello **usunąć** przycisk u góry hello hello strony. Wystarczy tootemporarily uniemożliwić innym użytkownikom dostęp do witryny hello, kliknij przycisk **zatrzymać** zamiast tego. W takim przypadku opłaty będą nadal tooaccrue. Po ich nie są już potrzebne, można wykonać podobne hello toodelete procedury konto magazynu i bazy danych SQL.
>
>

## <a name="create-hello-application-from-scratch"></a>Tworzenie aplikacji hello od początku
Jeśli nie pobrano jeszcze [aplikacji hello ukończone](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), zrób to teraz. Do nowego projektu hello będzie skopiuj pliki z projektu hello pobrane.

Tworzenie aplikacji Contoso Ads hello obejmuje hello następujące kroki:

* Tworzenie rozwiązania usługi w chmurze w programie Visual Studio.
* Aktualizowanie i dodawanie pakietów NuGet.
* Ustawianie odwołań do projektu.
* Konfigurowanie parametrów połączenia.
* Dodawanie plików kodu.

Po utworzeniu hello rozwiązania można przejrzeć kod hello projektów usług toocloud unikatowy i obiekty BLOB platformy Azure i kolejki.

### <a name="create-a-cloud-service-visual-studio-solution"></a>Tworzenie rozwiązania usługi w chmurze w programie Visual Studio
1. W programie Visual Studio, wybierz **nowy projekt** z hello **pliku** menu.
2. W okienku po lewej stronie powitania hello **nowy projekt** okna dialogowego rozwiń **Visual C#** i wybierz polecenie **chmury** szablony, a następnie wybierz pozycję hello **usługi w chmurze Azure** szablonu.
3. Nazwa projektu hello i rozwiązanie ContosoAdsCloudService, a następnie kliknij przycisk **OK**.

    ![Nowy projekt](./media/cloud-services-dotnet-get-started/newproject.png)
4. W hello **nową usługę w chmurze Azure** okno dialogowe Dodaj rolę sieci web i roli proces roboczy. Nazwa hello rolę sieć web ContosoAdsWeb i nazwę hello roli proces roboczy ContosoAdsWorker. (Użyj ikony ołówka hello w hello w okienku po prawej stronie toochange hello domyślne nazwy ról hello.)

    ![Projekt nowej usługi w chmurze](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. Po wyświetleniu hello **nowy projekt ASP.NET** okno dialogowe dla roli sieci web hello, wybierz szablon MVC hello, a następnie kliknij przycisk **Zmień uwierzytelnianie**.

    ![Zmienianie uwierzytelniania](./media/cloud-services-dotnet-get-started/chgauth.png)
6. W hello **Zmień uwierzytelnianie** oknie dialogowym wybierz **bez uwierzytelniania**, a następnie kliknij przycisk **OK**.

    ![Bez uwierzytelniania](./media/cloud-services-dotnet-get-started/noauth.png)
7. W hello **nowy projekt ASP.NET** okna dialogowego, kliknij przycisk **OK**.
8. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello rozwiązanie (nie jeden z projektów hello) i wybierz **Dodaj — nowy projekt**.
9. W hello **Dodawanie nowego projektu** okno dialogowe Wybierz **Windows** w obszarze **Visual C#** w lewym okienku hello, a następnie kliknij hello **biblioteki klas** szablon.  
10. Nazwa projektu hello *ContosoAdsCommon*, a następnie kliknij przycisk **OK**.

    Należy tooreference hello Entity Framework kontekstu i hello modelu danych z projektów ról sieć web i proces roboczy. Alternatywnie można zdefiniować klasy związane z platformą EF hello w projekcie roli sieci web hello i odwoływać się do tego projektu z projektu roli proces roboczy hello. Ale hello o innym podejściu, projektu roli proces roboczy musi zestawów tooweb odwołań, które nie należy go.

### <a name="update-and-add-nuget-packages"></a>Aktualizowanie i dodawanie pakietów NuGet
1. Otwórz hello **Zarządzaj pakietami NuGet** okno dialogowe hello rozwiązania.
2. U góry hello okna hello, zaznacz pole wyboru **aktualizacje**.
3. Wyszukaj hello *WindowsAzure.Storage* pakietu, a jeśli znajduje się liście hello, zaznacz go i wybierz tooupdate projektów sieci web i proces roboczy hello go, a następnie kliknij przycisk **aktualizacji**.

    Biblioteka klienta usługi storage Hello jest aktualizowana częściej niż szablony projektów Visual Studio, dlatego często okazuje tej wersji hello w nowo utworzonego projektu toobe potrzeb, zaktualizowane.
4. U góry hello okna hello, zaznacz pole wyboru **Przeglądaj**.
5. Znajdź hello *EntityFramework* NuGet pakietu, a następnie zainstaluj go we wszystkich trzech projektach.
6. Znajdź hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet pakietu, a następnie zainstaluj go w projekcie roli proces roboczy hello.

### <a name="set-project-references"></a>Ustawianie odwołań do projektu
1. W projekcie ContosoAdsWeb hello Ustaw odwołanie do projektu ContosoAdsCommon toohello. Kliknij prawym przyciskiem myszy projekt ContosoAdsWeb hello, a następnie kliknij przycisk **odwołania** - **Dodaj odwołania**. W hello **Menedżera odwołań** okno dialogowe, wybierz opcję **rozwiązanie — projekty** wybierz w okienku po lewej stronie powitania **ContosoAdsCommon**, a następnie kliknij przycisk **OK**.
2. W hello w projekcie ContosoAdsWorker Ustaw odwołanie do projektu Contosoadscommon toohello.

    Projekt ContosoAdsCommon będzie zawierać hello Entity Framework danych klasę kontekstu i model, które będą używane przez oba hello frontonu i zaplecza.
3. W projekcie ContosoAdsWorker hello Ustaw odwołanie za`System.Drawing`.

    Ten zestaw jest używany przez toothumbnails obrazów tooconvert zaplecza hello.

### <a name="configure-connection-strings"></a>Konfigurowanie parametrów połączenia
W tej sekcji będziesz konfigurować parametry połączenia usługi Azure Storage i danych SQL na potrzeby testowania lokalnego. instrukcje dotyczące wdrażania Hello wcześniej w samouczku hello wyjaśniają, jak tooset hello połączenie ciągów dla uruchomienie hello aplikacji w chmurze hello.

1. W projekcie ContosoAdsWeb hello, hello Otwórz plik Web.config i Wstaw następujący hello `connectionStrings` elementu po hello `configSections` elementu.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Jeśli korzystasz z programu Visual Studio 2015 lub nowszego, zastąp element „v11.0” elementem „MSSQLLocalDB”.
2. Zapisz zmiany.
3. W projekcie ContosoAdsCloudService hello, kliknij prawym przyciskiem myszy ContosoAdsWeb w obszarze **ról**, a następnie kliknij przycisk **właściwości**.

    ![Właściwości roli](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. W hello **contosadsweb — [rola]** okna właściwości, kliknij przycisk hello **ustawienia** , a następnie kliknij pozycję **Dodaj ustawienie**.

    Pozostaw **konfiguracji usługi** ustawić także**wszystkie konfiguracje**.
5. Dodaj ustawienie o nazwie *StorageConnectionString*. Ustaw **typu** za*ConnectionString*i ustaw **wartość** za*UseDevelopmentStorage = true*.

    ![Nowe parametry połączenia](./media/cloud-services-dotnet-get-started/scall.png)
6. Zapisz zmiany.
7. Wykonaj hello tej samej procedury tooadd parametry połączenia magazynu w właściwości roli ContosoAdsWorker hello.
8. Nadal w hello **ContosoAdsWorker — [rola]** okna właściwości, Dodaj inny ciąg połączenia:

   * Nazwa: ContosoAdsDbConnectionString
   * Typ: ciąg
   * Wartość: Wklej hello takie same parametry połączenia używane dla projektu roli sieć web hello. (hello poniższy przykład dotyczy programu Visual Studio 2013. Nie zapomnij hello toochange źródła danych, jeśli kopiujesz ten przykład i korzystasz z programu Visual Studio 2015 lub nowszego.)

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a>Dodawanie plików kodu
W tej sekcji skopiujesz pliki kodu z rozwiązania hello pobrane do hello nowego rozwiązania. Witaj sekcje będzie Pokaż i objaśnione części tego kodu.

pliki tooadd tooa projektu lub folderu, kliknij prawym przyciskiem myszy projekt hello lub folderu i kliknij przycisk **Dodaj** - **istniejący element**. Wybierz pliki hello, a następnie kliknij przycisk **Dodaj**. Jeśli zostanie wyświetlone pytanie, czy tooreplace istniejące pliki, kliknij przycisk **tak**.

1. W projekcie ContosoAdsCommon hello Usuń hello *Class1.cs* i Dodaj w jego miejscu hello *Ad.cs* i *ContosoAdscontext.cs* pobrane pliki z hello projektu.
2. W projekcie ContosoAdsWeb hello Dodaj hello następujące pliki z projektu hello pobrane.

   * *Global.asax.cs*.  
   * W hello *Views\Shared* folder: * \_Layout.cshtml*.
   * W hello *Views\Home* folder: *Index.cshtml*.
   * W hello *kontrolerów* folder: *AdController.cs*.
   * W hello *Views\Ad* folder (najpierw utwórz hello folder): pięć *.cshtml* plików.
3. W projekcie ContosoAdsWorker hello Dodaj *WorkerRole.cs* z hello pobrany projekt.

Teraz możesz skompilować i uruchomić aplikację hello, zgodnie z instrukcjami podanymi wcześniej w samouczku hello, a aplikacja hello będzie używać lokalnej bazy danych i zasobów emulatora magazynu.

Witaj poniższe sekcje zawierają opis kodu hello tooworking powiązane z hello środowiska platformy Azure, obiekty BLOB i kolejek. W tym samouczku opisano, jak kontrolerów MVC toocreate i widoków przy użyciu funkcji szkieletów, jak toowrite kodu programu Entity Framework działające z baz danych programu SQL Server lub hello podstaw programowania asynchronicznego w programie ASP.NET 4.5. Aby uzyskać informacje dotyczące tych tematów zobacz następujące zasoby hello:

* [Wprowadzenie do programu MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Wprowadzenie do programów EF 6 i MVC 5](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* [Wprowadzenie tooasynchronous programowania w programie .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon — Ad.cs
Witaj plik Ad.cs definiuje wyliczenia związane z kategoriami reklam i klasą jednostki POCO dla informacji o reklamach.

```csharp
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
```

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon — ContosoAdsContext.cs
Witaj klasa ContosoAdsContext Określa, czy klasa Ad hello jest używany w kolekcji DbSet Entity Framework będą przechowywane w bazie danych SQL.

```csharp
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
```

Klasa Hello ma dwa konstruktory. Witaj pierwszy z nich jest używany przez hello projektu sieci web i określa nazwę parametrów połączenia, które są przechowywane w pliku Web.config hello hello. Witaj drugi Konstruktor umożliwia toopass w hello rzeczywistych parametrów połączenia używane przez projekt roli proces roboczy hello, ponieważ nie ma on pliku Web.config. Wcześniej przedstawiono gdzie te parametry połączenia są przechowywane i pojawi się później, jak hello kod pobiera parametry połączenia hello podczas tworzenia wystąpień klasy DbContext hello.

### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb — Global.asax.cs
Kod, który jest wywoływany z hello `Application_Start` metoda tworzy *obrazów* kontenera obiektów blob i *obrazów* kolejki, jeśli jeszcze nie istnieje. Daje to pewność, że zawsze, gdy rozpoczynasz pracę przy użyciu nowego konta magazynu, czy przy użyciu emulatora magazynu hello na nowym komputerze, kolejka i kontener wymaganego obiektu blob hello zostaną utworzone automatycznie.

Witaj konta magazynu toohello kod pobiera dostępu przy użyciu parametrów połączenia magazynu hello z hello *.cscfg* pliku.

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

Następnie pobiera toohello odwołanie *obrazów* kontenera obiektów blob, tworzy kontener hello, jeśli jeszcze nie istnieje, i zestawów uprawnień dostępu na powitania nowy kontener. Domyślnie nowe kontenery tylko zezwolić klientom z kontem magazynu obiektów blob tooaccess poświadczeń. Hello witryny sieci Web wymaga hello publicznego toobe obiektów blob, aby możliwe było wyświetlanie obrazów przy użyciu adresów URL tego obiekty BLOB obrazów toohello punktu.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

Podobny kod pobiera odwołanie toohello *obrazów* kolejki i tworzy nową kolejkę. W takim przypadku nie trzeba zmieniać uprawnień.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb — \_Layout.cshtml
Witaj *_Layout.cshtml* plik ustawia nazwę aplikacji hello w hello nagłówku i stopce oraz utworzenie wpisu menu "Ads".

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb — Views\Home\Index.cshtml
Witaj *Views\Home\Index.cshtml* pliku wyświetla linków kategorii na stronie głównej hello. Witaj linki przekazują wartość całkowitą hello hello `Category` wyliczenia na stronie indeksu reklam toohello zmiennej querystring.

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb — AdController.cs
W hello *AdController.cs* plik, hello wywołania konstruktora hello `InitializeStorage` — metoda toocreate biblioteki klienta magazynu Azure obiektów, które zapewniają interfejs API do pracy z obiektów blob i kolejek.

Następnie hello kod pobiera odwołanie toohello *obrazów* kontenera obiektów blob, jak przedstawiono wcześniej w *Global.asax.cs*. W tym czasie ustawiane są domyślne [zasady ponawiania](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) odpowiednie dla aplikacji sieci Web. zasady ponawiania wykładniczego wycofywania domyślne Hello mogą powodować zawieszanie aplikacji sieci web hello przez czas dłuższy niż minuta w przypadku kolejnych prób błędu przejściowego. Witaj zasady ponawiania określone w tym miejscu czeka trzy sekundy po każdej się toothree prób.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

Podobny kod pobiera odwołanie toohello *obrazów* kolejki.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

Większość kodu kontrolera hello jest typowa dla pracy z modelem danych programu Entity Framework za pomocą klasy DbContext. Wyjątkiem jest hello HttpPost `Create` metodę, która przekazuje plik i zapisuje je w magazynie obiektów blob. udostępnia integratora modelu Hello [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) obiekt toohello metody.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

Użytkownika hello zaznaczenie tooupload pliku, kod hello hello plik zostanie przesłany, zapisuje go w obiekcie blob i aktualizacji rekordu bazy danych Ad hello adres URL, który wskazuje obiekt blob toohello.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

Witaj kod hello przekazywania jest hello `UploadAndSaveBlobAsync` metody. Tworzy nazwę identyfikatora GUID dla obiektu blob hello, przekazywanie i zapisuje plik hello i zwraca odwołanie do obiektu blob toohello zapisane.

```csharp
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
```

Po hello HttpPost `Create` metoda przekazuje obiekt blob i aktualizacje hello bazy danych, tworzy tooinform komunikat kolejki tego procesu zaplecza, że obraz jest gotowy do konwersji tooa miniatur.

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

Witaj kod hello HttpPost `Edit` metoda jest podobna z tą różnicą, że jeśli hello użytkownik wybierze nowy plik obrazu należy usunąć wszystkie obiekty BLOB, które już istnieją.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

Witaj kolejnym przykładzie pokazano kod hello usuwania obiektów blob podczas usuwania reklamy.

```csharp
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
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb — Views\Ad\Index.cshtml i Details.cshtml
Witaj *Index.cshtml* służy do wyświetlania miniatury z hello innymi danymi reklamy.

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

Witaj *Details.cshtml* pliku wyświetla hello obrazu w pełnym rozmiarze.

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb — Views\Ad\Create.cshtml i Edit.cshtml
Witaj *Create.cshtml* i *Edit.cshtml* pliki określają kodowanie, że umożliwia hello hello tooget kontrolera formularza `HttpPostedFileBase` obiektu.

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

`<input>` Informuje hello przeglądarki tooprovide okna dialogowego wyboru pliku.

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a>ContosoAdsWorker — WorkerRole.cs — metoda OnStart
środowisko roli procesu roboczego platformy Azure Hello wywołuje hello `OnStart` metoda hello `WorkerRole` klasy, gdy rola proces roboczy hello jest wprowadzenie i wywołuje hello `Run` metodą podczas hello `OnStart` zakończeniu działania metody.

Witaj `OnStart` metoda pobiera parametry połączenia bazy danych hello z hello *.cscfg* i przekazuje je toohello klasy Entity Framework DbContext. Dostawca SQLClient Hello jest używany domyślnie, więc hello dostawca nie ma toobe określony.

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

Po wykonaniu tej hello metoda pobiera odwołanie do konta magazynu toohello i tworzy hello kontenera obiektów blob i kolejki, jeśli nie istnieją. Kod Hello tej jest podobne toowhat był już wyświetlany w roli sieci web hello `Application_Start` metody.

### <a name="contosoadsworker---workerrolecs---run-method"></a>ContosoAdsWorker — WorkerRole.cs — metoda Run
Witaj `Run` metoda jest wywoływana, gdy hello `OnStart` metoda zakończy się inicjowanie. Witaj metoda wykonuje nieskończoną pętlę, która oczekuje na nowe komunikaty w kolejce i przetwarza je po nadejściu.

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

Po każdej iteracji pętli hello Jeśli komunikatu w kolejce nie został znaleziony, hello program zostanie uśpiony na sekundę. Zapobiega to ponoszenia nadmiernych kosztów Procesora czas i Magazyn transakcji hello roli procesu roboczego. Witaj zespół doradczy klientów firmy Microsoft opowiada historię o deweloperze, który zapomniał tooinclude, wdrożyć tooproduction i wyjechał na urlop. Gdy zorientował się ponownie, jego poniesione koszty były wyższe niż koszty urlopu hello.

Czasami zawartość komunikatu w kolejce hello powoduje błąd podczas przetwarzania. Ta metoda jest wywoływana *Trująca wiadomość*, a jeśli właśnie zarejestrowano błąd i ponownym uruchomieniu pętli hello można nieskończoność ponawiać próby tooprocess tej wiadomości.  W związku z tym hello blok catch zawiera if instrukcji, która sprawdza toosee ile razy aplikacja hello podjął tooprocess hello bieżącego komunikatu, a jeśli został on więcej niż 5 razy, wiadomość hello jest usuwane z kolejki hello.

`ProcessQueueMessage` — ten element jest wywoływany po znalezieniu komunikatu w kolejce.

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

Ten kod odczytuje adres URL obrazu hello hello bazy danych tooget, konwertuje hello obrazu tooa miniatur, zapisuje miniaturę hello w obiekcie blob, aktualizuje bazę danych hello z adresem URL obiektu blob miniatury hello i usuwa komunikat z kolejki hello.

> [!NOTE]
> Witaj kodu w hello `ConvertImageToThumbnailJPG` metoda używa klas w przestrzeni nazw System.Drawing powitania dla uproszczenia. Jednak klasy hello w tej przestrzeni nazw zostały zaprojektowane do użytku z formularzy systemu Windows. Nie są one obsługiwane w usłudze systemu Windows lub programu ASP.NET. Aby uzyskać więcej informacji o opcjach przetwarzania obrazu, zobacz [Dynamiczne generowanie obrazu](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) i [Bezpośrednie zmienianie rozmiaru obrazu](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="troubleshooting"></a>Rozwiązywanie problemów
W przypadku, gdy coś nie działa podczas postępujesz zgodnie z instrukcjami hello w tym samouczku, poniżej przedstawiono niektóre typowe błędy i w jaki sposób tooresolve je.

### <a name="serviceruntimeroleenvironmentexception"></a>ServiceRuntime.RoleEnvironmentException
Witaj `RoleEnvironment` obiektu jest dostarczany przez platformę Azure po uruchomieniu aplikacji na platformie Azure lub po uruchomieniu lokalnie przy użyciu emulatora obliczeń platformy Azure hello.  Jeśli ten błąd wystąpi, jeśli są uruchomione lokalnie, upewnij się, że ustawiono projektu ContosoAdsCloudService hello jako projekt startowy hello. Konfiguruje hello toorun projektu przy użyciu emulatora obliczeń platformy Azure hello.

Jest jeden z elementów hello zastosowań aplikacji hello hello Azure RoleEnvironment dla wartości parametrów połączeń hello tooget, które są przechowywane w hello *.cscfg* pliki, więc inną przyczyną tego wyjątku jest Brak parametrów połączenia. Upewnij się, utworzony hello ustawienie StorageConnectionString w chmurze i lokalnej w projekcie ContosoAdsWeb hello i utworzyć parametry połączenia dla obydwu konfiguracji w projekcie ContosoAdsWorker hello. Jeśli chcesz **Znajdź wszystkie** wyszukiwania dla elementu StorageConnectionString w całym rozwiązaniu hello, powinny pojawić się on znaleziony 9 razy w 6 plikach.

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a>Nie można zastąpić tooport xxx. Nowy port poniżej minimalnej dozwolonej wartości 8080 dla protokołu HTTP
Spróbuj zmienić hello numeru portu używanego przez hello projektu sieci web. Kliknij prawym przyciskiem myszy projekt ContosoAdsWeb hello, a następnie kliknij przycisk **właściwości**. Kliknij przycisk hello **Web** karcie, a następnie zmień numer portu hello w hello **adres Url projektu** ustawienie.

Kolejny alternatywny sposób rozwiązania problemu hello Zobacz hello następujących sekcji.

### <a name="other-errors-when-running-locally"></a>Inne błędy po uruchomieniu w środowisku lokalnym
W chmurze nowego domyślnego projektów usług Użyj hello obliczeń platformy Azure emulator express toosimulate hello środowiska platformy Azure. Jest to Uproszczona wersja hello pełnego emulatora obliczeń, a w niektórych warunkach hello pełnego emulatora będzie działać, gdy hello wersja ekspresowa nie.  

toochange hello projektu toouse hello pełnego emulatora, kliknij prawym przyciskiem myszy projekt ContosoAdsCloudService hello, a następnie kliknij przycisk **właściwości**. W hello **właściwości** oknie kliknij hello **Web** , a następnie kliknij pozycję hello **użyj pełnego emulatora** przycisk radiowy.

Kolejność aplikacji hello toorun z pełnego emulatora hello masz tooopen programu Visual Studio z uprawnieniami administratora.

## <a name="next-steps"></a>Następne kroki
Witaj aplikacja Contoso Ads została celowo uproszczona samouczek ułatwiający Rozpoczynanie pracy. Na przykład nie implementuje [iniekcji zależności](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) lub hello [repozytorium i jednostki pracy wzorce](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), nie [używa interfejsu do rejestrowania](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), nie używa [ Migracje EF Code First](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) zmiany modelu danych toomanage lub [elastyczności połączenia platformy EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage przejściowe błędy sieciowe i tak dalej.

Poniżej przedstawiono niektóre przykładowe aplikacje usług chmury których zastosowano więcej praktyk kodowania rzeczywistych, w kolejności od mniej złożona toomore złożonych:

* [PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31). Podobna tooContoso Ads, ale z zaimplementowaną większą liczbą funkcji i więcej rzeczywistych praktyk kodowania.
* [Wielowarstwowa aplikacja usługi w chmurze Azure z tabelami, kolejkami i obiektami blob](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36). Obejmuje tabele usługi Azure Storage, a także obiekty blob i kolejki. Oparty na starszej wersji hello Azure SDK dla platformy .NET, będą musieli niektórych toowork modyfikacje hello bieżącej wersji.
* [Podstawy usługi w chmurze na platformie Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Kompleksowy przykład przedstawiający szeroki zakres najlepszych rozwiązań tworzonych przez grupę Microsoft Patterns and Practices hello.

Aby uzyskać ogólne informacje o tworzeniu aplikacji hello chmury, zobacz [tworzenia rzeczywistych aplikacji w chmurze platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).

Dla tooAzure wideo z wprowadzeniem magazynu najlepszych rozwiązań i wzorców, zobacz [Microsoft Azure Storage — nowości nowy, najlepsze rozwiązania i wzorce](http://channel9.msdn.com/Events/Build/2014/3-628).

Aby uzyskać więcej informacji zobacz następujące zasoby hello:

* [Azure Cloud Services, część 1: wprowadzenie](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [W jaki sposób toomanage usług w chmurze](cloud-services-how-to-manage.md)
* [Azure Storage](/documentation/services/storage/)
* [Jak dostawca usług chmury toochoose](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
