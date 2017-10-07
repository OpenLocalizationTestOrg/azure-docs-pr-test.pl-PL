---
title: "aaaAccess zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service"
description: "Utwórz połączenie między aplikacji sieci web w usłudze Azure App Service i zasobu lokalnego, który używa portu TCP statycznego"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>Dostęp do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service
Można połączyć z usługi aplikacji Azure tooany lokalnymi zasób aplikacji używającej portu statycznego TCP, takich jak SQL Server, MySQL, interfejsów API sieci Web HTTP i większość niestandardowych usług sieci Web. W tym artykule opisano sposób toocreate połączenie hybrydowe między usługą aplikacji i lokalną bazą danych programu SQL Server.

> [!NOTE]
> Witaj aplikacje sieci Web część funkcji połączeń hybrydowych hello jest dostępna tylko w hello [Azure Portal](https://portal.azure.com). Zobacz toocreate połączenie usługi BizTalk Services [połączeń hybrydowych](http://go.microsoft.com/fwlink/p/?LinkID=397274). 
> 
> Ta zawartość dotyczy również tooMobile aplikacji w usłudze Azure App Service. 
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
* Subskrypcja platformy Azure. Aby uzyskać bezpłatną subskrypcję, zobacz [bezpłatnej wersji próbnej Azure](https://azure.microsoft.com/pricing/free-trial/). 
  
    Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
* toouse lokalnego programu SQL Server lub SQL Server Express bazy danych z połączenia hybrydowego TCP/IP musi toobe włączone portu statycznego. Przy użyciu domyślnego wystąpienia serwera SQL jest zalecane, ponieważ używa portu statycznego 1433. Aby uzyskać informacje na temat instalowania i konfigurowania programu SQL Server Express do użycia z połączeń hybrydowych było możliwe, zobacz [tooan połączenia lokalnego programu SQL Server z Azure witryny sieci web za pomocą połączeń hybrydowych](http://go.microsoft.com/fwlink/?LinkID=397979).
* Witaj komputera, na którym jest instalowany agent Menedżera połączeń hybrydowych lokalne powitania opisane w dalszej części tego artykułu:
  
  * Musi być możliwe tooconnect tooAzure za pośrednictwem portu 5671
  * Musi być w stanie tooreach hello *hostname*:*numer_portu* zasobu lokalnego. 

> [!NOTE]
> Hello opisanych w tym artykule założono, że używasz przeglądarki hello z hello komputer, który będzie hostem agenta połączenia hybrydowego lokalne powitania.
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Tworzenie aplikacji sieci web w hello portalu Azure
> [!NOTE]
> Jeśli utworzono już aplikację sieci web lub zaplecza aplikacji mobilnej w hello mają toouse w tym samouczku portalu Azure, możesz przejść od razu zbyt[Tworzenie połączenia hybrydowego i usługi BizTalk](#CreateHC) i uruchomić stamtąd.
> 
> 

1. W hello lewego górnego rogu hello [Azure Portal](https://portal.azure.com), kliknij przycisk **nowy** > **sieci Web i mobilność** > **aplikacji sieci Web**.
   
    ![Nowa aplikacja sieci web][NewWebsite]
2. Na powitania **aplikacji sieci Web** bloku, podaj adres URL i kliknij przycisk **Utwórz**. 
   
    ![Nazwa witryny sieci Web][WebsiteCreationBlade]
3. Po kilku chwilach hello aplikacji sieci web jest tworzona i pojawia się jego bloku aplikacja sieci web. Blok Hello jest pionowo przewijanego pulpit nawigacyjny, który umożliwia zarządzanie witryną.
   
    ![Witryny sieci Web uruchomionej][WebSiteRunningBlade]
4. Witryna hello tooverify na żywo, można kliknąć hello **Przeglądaj** ikona toodisplay hello domyślnej strony.
   
    ![Kliknij przycisk Przeglądaj toosee aplikacji sieci web][Browse]
   
    ![Domyślna strona aplikacji sieci web][DefaultWebSitePage]

Następnie utworzysz, połączenie hybrydowe i usługi BizTalk hello aplikacji sieci web.

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>Tworzenie połączenia hybrydowego i usługi BizTalk
1. W bloku aplikacja sieci web kliknij **wszystkie ustawienia** > **sieci** > **skonfiguruj punkty końcowe połączenia hybrydowego**.
   
    ![Połączenia hybrydowe][CreateHCHCIcon]
2. W bloku połączeń hybrydowych hello, kliknij **Dodaj**.
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. Witaj **Dodaj połączenie hybrydowe** zostanie otwarty blok.  Ponieważ jest to pierwszy połączenia hybrydowe, hello **nowe połączenie hybrydowe** opcja wyświetlana jest wartość i hello **Tworzenie połączenia hybrydowego** zostanie otwarty blok dla Ciebie.
   
    ![Tworzenie połączenia hybrydowego][TwinCreateHCBlades]
   
    Na powitania **bloku połączenia hybrydowe Utwórz**:
   
   * Aby uzyskać **nazwa**, podaj nazwę hello połączenia.
   * Aby uzyskać **Hostname**, wprowadź nazwę hello hello na lokalnym komputerze, który obsługuje zasobu.
   * Aby uzyskać **portu**, wprowadź numer portu hello używany zasób lokalną (1433 dla domyślnego wystąpienia programu SQL Server).
   * Kliknij przycisk **Biz Talk usługi**
4. Witaj **Utwórz usługę BizTalk** zostanie otwarty blok. Wprowadź nazwę hello usługi BizTalk, a następnie kliknij przycisk **OK**.
   
    ![Utwórz usługę BizTalk][CreateHCCreateBTS]
   
    Witaj **Utwórz usługę BizTalk** bloku zamyka i są zwracane toohello **Tworzenie połączenia hybrydowego** bloku.
5. W bloku połączenia hybrydowe Utwórz hello, kliknij polecenie **OK**. 
   
    ![Kliknij przycisk OK][CreateBTScomplete]
6. Po zakończeniu procesu hello hello obszar powiadomień w hello portalu informuje o pomyślnie utworzono połączenie hello.
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. W bloku aplikacja sieci web hello hello **połączeń hybrydowych** ikona teraz wskazuje, że utworzono połączenie hybrydowe 1.
   
    ![Połączenia hybrydowe jeden utworzone][CreateHCOneConnectionCreated]

W tym momencie została ukończona ważnym elementem hello chmury hybrydowej połączenia infrastruktury. Następnie utworzy odpowiedni element lokalnymi.

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>Zainstaluj hello lokalnego Menedżera połączeń hybrydowych toocomplete hello połączenia
1. W bloku aplikacja sieci web powitania kliknij **wszystkie ustawienia** > **sieci** > **skonfiguruj punkty końcowe połączenia hybrydowego**. 
   
    ![Ikona połączenia hybrydowego][HCIcon]
2. Na powitania **połączeń hybrydowych** bloku, hello **stan** kolumny dla hello niedawno dodano punkt końcowy pokazuje **niepołączone**. Kliknij przycisk tooconfigure połączenia hello go.
   
    ![Nie połączono][NotConnected]
   
    zostanie otwarty blok połączenia hybrydowe Hello.
   
    ![NotConnectedBlade][NotConnectedBlade]
3. W bloku powitania kliknij **konfiguracji odbiornika**.
   
    ![Kliknij przycisk Ustawienia odbiornika][ClickListenerSetup]
4. Witaj **właściwości połączenia hybrydowe** zostanie otwarty blok. W obszarze **Menedżera połączeń hybrydowych lokalnymi**, wybierz **kliknij tutaj tooinstall**.
   
    ![Kliknij tutaj tooinstall][ClickToInstallHCM]
5. Hello uruchamiać aplikacje zabezpieczeń okno dialogowe z ostrzeżeniem, wybierz **Uruchom** toocontinue.
   
    ![Wybierz polecenie Uruchom toocontinue][ApplicationRunWarning]
6. W hello **Kontrola konta użytkownika** okno dialogowe, wybierz **tak**.
   
   ![Wybierz opcję Tak][UAC]
7. Menedżera połączeń hybrydowych Hello jest pobierane i instalowane automatycznie. 
   
    ![Instalowanie][HCMInstalling]
8. Po zakończeniu instalacji powitania kliknij przycisk **Zamknij**.
   
    ![Kliknij przycisk Zamknij][HCMInstallComplete]
   
    Na powitania **połączeń hybrydowych** bloku, hello **stan** zawiera obecnie kolumnę **połączony**. 
   
    ![Stan połączenia][HCStatusConnected]

Po zakończeniu tego połączenia infrastruktura hybrydowa hello można utworzyć aplikacji hybrydowych, która korzysta z niego. 

> [!NOTE]
> Hello następnych sekcjach opisano sposób toouse połączenie hybrydowe z projektu zaplecza .NET aplikacji mobilnej.
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a>Skonfiguruj hello Mobile aplikacji .NET w wewnętrznej bazie danych projektu tooconnect toohello bazy danych SQL Server
W usłudze App Service Mobile Apps na platformie .NET projekt wewnętrznej bazy danych jest tylko aplikacji sieci web platformy ASP.NET z dodatkowe zestawu Mobile Apps SDK zainstalowany i zainicjować. toouse aplikacji sieci web jako zaplecza aplikacji mobilnej musi [pobierania i zainicjuj hello zaplecza Mobile Apps .NET SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).  

Dla aplikacji mobilnych także muszą toodefine ciąg połączenia dla bazy danych lokalne powitania i zmodyfikować hello toouse wewnętrznej bazy danych to połączenie. 

1. W Eksploratorze rozwiązań w programie Visual Studio, hello Otwórz plik Web.config dla zaplecza .NET aplikacji mobilnych, Znajdź hello **connectionStrings** Dodaj nowy wpis SqlClient jak hello poniższe polecenie, które toohello punktów lokalnej SQL Serwer bazy danych:
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    Należy pamiętać, tooreplace `<**secure_password**>` w tym ciągu z hello hasło utworzone dla *HybridConnectionLogin*.
2. Kliknij przycisk **zapisać** w pliku Web.config hello toosave programu Visual Studio.
   
   > [!NOTE]
   > To ustawienie połączenia jest używany podczas uruchamiania komputera lokalnego hello. Podczas uruchamiania na platformie Azure, to ustawienie jest zastąpione przez ustawienie połączenia hello zdefiniowane w portalu hello.
   > 
   > 
3. Rozwiń węzeł hello **modele** folderu i pliku modelu danych otwórz hello, która kończy się *Context.cs*.
4. Modyfikowanie hello **DbContext** toopass konstruktora wystąpienia hello wartość `OnPremisesDBConnection` toohello podstawowej **DbContext** konstruktora, podobne toohello po fragment kodu:
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    Usługa Hello użyje teraz hello nowego połączenia toohello bazy danych SQL Server.

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a>Zaktualizować parametry połączenia lokalne powitania toouse hello aplikacji mobilnej wewnętrznej bazy danych
Następnie należy tooadd ustawienia aplikacji dla tych nowych parametrów połączenia, dzięki czemu mogą być używane z platformy Azure.  

1. Po powrocie do hello [portalu Azure](https://portal.azure.com) w wewnętrznej bazy danych aplikacji kod hello sieci web aplikacji mobilnej kliknij **wszystkie ustawienia**, następnie **ustawienia aplikacji**.
2. W hello **ustawienia aplikacji w sieci Web** bloku, przewiń w dół za**parametry połączenia** i dodać nowe **programu SQL Server** parametrów połączenia o nazwie `OnPremisesDBConnection` o wartości podobnie jak `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    Zastąp `<**secure_password**>` z bezpiecznym hasłem hello lokalnej bazy danych.
   
    ![Parametry połączenia dla lokalnej bazy danych](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. Naciśnij klawisz **zapisać** połączenia hybrydowego hello toosave i parametry połączenia utworzony.

W tym momencie możesz ponownie opublikować projekt serwera hello i przetestować hello nowego połączenia z istniejących klientów Mobile Apps. Dane będą odczytywane i zapisywane toohello lokalną bazą danych przy użyciu połączenia hybrydowego hello.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać informacje dotyczące tworzenia aplikacji sieci web ASP.NET, która używa połączenie hybrydowe, zobacz [tooan połączenia lokalnego programu SQL Server z Azure witryny sieci web za pomocą połączeń hybrydowych](http://go.microsoft.com/fwlink/?LinkID=397979). 

### <a name="additional-resources"></a>Dodatkowe zasoby
[Omówienie połączeń hybrydowych](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Dołączony Josha wprowadza połączeń hybrydowych (wideo z witryny Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Witryna sieci web połączenia hybrydowego](https://azure.microsoft.com/services/biztalk-services/)

[Usługi BizTalk Services: Karty Pulpit nawigacyjny, Monitor skali, konfigurowanie i połączenia hybrydowego](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Tworzenie hybrydowego rzeczywistych chmury chronionej za pomocą bezproblemowe przenośność aplikacji (Channel 9 wideo)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Połącz tooan lokalnego programu SQL Server z usługi Azure Mobile Services za pomocą połączeń hybrydowych (wideo z witryny Channel 9)](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
