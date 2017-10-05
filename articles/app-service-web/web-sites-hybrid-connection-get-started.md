---
title: "Dostęp do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service"
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
ms.openlocfilehash: fbd22e6e285c5ddaef2a473671d4a06a97384b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>Dostęp do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service
Możesz połączyć aplikację usługi aplikacji Azure do dowolnego zasobu lokalnego, który korzysta z portu statycznego TCP, takich jak SQL Server, MySQL, interfejsów API sieci Web HTTP i większość niestandardowych usług sieci Web. W tym artykule przedstawiono sposób utworzyć połączenie hybrydowe między usługą aplikacji i lokalną bazą danych programu SQL Server.

> [!NOTE]
> Aplikacje sieci Web część funkcji połączeń hybrydowych było możliwe jest dostępna tylko w [Azure Portal](https://portal.azure.com). Aby utworzyć połączenie w usługi BizTalk Services, zobacz [połączeń hybrydowych](http://go.microsoft.com/fwlink/p/?LinkID=397274). 
> 
> Ta zawartość dotyczy również Mobile Apps w usłudze Azure App Service. 
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
* Subskrypcja platformy Azure. Aby uzyskać bezpłatną subskrypcję, zobacz [bezpłatnej wersji próbnej Azure](https://azure.microsoft.com/pricing/free-trial/). 
  
    Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
* Aby użyć lokalnego programu SQL Server lub SQL Server Express bazy danych z połączenia hybrydowego, TCP/IP musi być włączona na portu statycznego. Przy użyciu domyślnego wystąpienia serwera SQL jest zalecane, ponieważ używa portu statycznego 1433. Aby uzyskać informacje na temat instalowania i konfigurowania programu SQL Server Express do użycia z połączeń hybrydowych było możliwe, zobacz [Połącz z lokalnego serwera SQL z Azure witryny sieci web za pomocą połączeń hybrydowych](http://go.microsoft.com/fwlink/?LinkID=397979).
* Komputer, na którym instalowany agenta menedżera połączeń hybrydowych lokalnymi opisane w dalszej części tego artykułu:
  
  * Musi mieć możliwość połączenia z platformą Azure za pośrednictwem portu 5671
  * Musi być możliwe nawiązanie łączności *hostname*:*numer_portu* zasobu lokalnego. 

> [!NOTE]
> Kroki opisane w tym artykule założono, że używasz przeglądarki z komputera, który będzie hostem agenta połączenia hybrydowego lokalnymi.
> 
> 

## <a name="create-a-web-app-in-the-azure-portal"></a>Tworzenie aplikacji sieci web w portalu Azure
> [!NOTE]
> Jeśli utworzono już aplikację sieci web lub zaplecza aplikacji mobilnej w portalu Azure, który ma być używany na potrzeby tego samouczka, możesz przejść od razu do [Tworzenie połączenia hybrydowego i usługi BizTalk](#CreateHC) i uruchomić stamtąd.
> 
> 

1. W lewym górnym rogu [Azure Portal](https://portal.azure.com), kliknij przycisk **nowy** > **sieci Web i mobilność** > **aplikacji sieci Web**.
   
    ![Nowa aplikacja sieci web][NewWebsite]
2. Na **aplikacji sieci Web** bloku, podaj adres URL i kliknij przycisk **Utwórz**. 
   
    ![Nazwa witryny sieci Web][WebsiteCreationBlade]
3. Po kilku chwilach aplikacji sieci web jest tworzona i pojawia się jego bloku aplikacja sieci web. Blok jest pionowo przewijanego pulpit nawigacyjny, który umożliwia zarządzanie witryną.
   
    ![Witryny sieci Web uruchomionej][WebSiteRunningBlade]
4. Aby sprawdzić, witryna jest na żywo, można kliknąć **Przeglądaj** ikonę, aby wyświetlić stronę domyślną.
   
    ![Kliknij przycisk Przeglądaj, aby wyświetlić aplikację sieci web][Browse]
   
    ![Domyślna strona aplikacji sieci web][DefaultWebSitePage]

Następnie utworzysz połączenie hybrydowe i usługa BizTalk aplikacji sieci web.

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>Tworzenie połączenia hybrydowego i usługi BizTalk
1. W bloku aplikacja sieci web kliknij **wszystkie ustawienia** > **sieci** > **skonfiguruj punkty końcowe połączenia hybrydowego**.
   
    ![Połączenia hybrydowe][CreateHCHCIcon]
2. W bloku połączeń hybrydowych, kliknij **Dodaj**.
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. **Dodaj połączenie hybrydowe** zostanie otwarty blok.  Ponieważ jest to pierwsze połączenie hybrydowe, **nowe połączenie hybrydowe** wyświetlana jest wartość i **Tworzenie połączenia hybrydowego** zostanie otwarty blok dla Ciebie.
   
    ![Tworzenie połączenia hybrydowego][TwinCreateHCBlades]
   
    Na **bloku połączenia hybrydowe Utwórz**:
   
   * Aby uzyskać **nazwa**, podaj nazwę dla połączenia.
   * Aby uzyskać **Hostname**, wprowadź nazwę komputera lokalnego, który obsługuje zasobu.
   * Aby uzyskać **portu**, wprowadź numer portu używany zasób lokalną (1433 dla domyślnego wystąpienia programu SQL Server).
   * Kliknij przycisk **Biz Talk usługi**
4. **Utwórz usługę BizTalk** zostanie otwarty blok. Wprowadź nazwę usługi BizTalk, a następnie kliknij przycisk **OK**.
   
    ![Utwórz usługę BizTalk][CreateHCCreateBTS]
   
    **Utwórz usługę BizTalk** bloku zamyka i nastąpi powrót do **Tworzenie połączenia hybrydowego** bloku.
5. W bloku Utwórz hybrydowe połączenia, kliknij polecenie **OK**. 
   
    ![Kliknij przycisk OK][CreateBTScomplete]
6. Po zakończeniu tego procesu, obszar powiadomień, w portalu informuje o pomyślnie utworzono połączenie.
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in the dogfood portal. I switch to the classic portal
    (full portal) and created the BizTalk service but it doesn't seem to let you connnect them - When you finish the
    Create hybrid conn step, you get the following error
    Failed to create hybrid connection RelecIoudHC. The 
    resource type could not be found in the namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    The error indicates it couldn't find the type, not the instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. W bloku aplikacja sieci web **połączeń hybrydowych** ikona teraz wskazuje, że utworzono połączenie hybrydowe 1.
   
    ![Połączenia hybrydowe jeden utworzone][CreateHCOneConnectionCreated]

W tym momencie została ukończona ważnym elementem infrastruktury połączenia hybrydowe w chmurze. Następnie utworzy odpowiedni element lokalnymi.

<a name="InstallHCM"></a>

## <a name="install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a>Zainstaluj Menedżera połączeń hybrydowych lokalnego, aby nawiązać połączenie
1. W bloku aplikacja sieci web, kliknij przycisk **wszystkie ustawienia** > **sieci** > **skonfiguruj punkty końcowe połączenia hybrydowego**. 
   
    ![Ikona połączenia hybrydowego][HCIcon]
2. Na **połączeń hybrydowych** bloku **stan** kolumny dla przedstawia ostatnio dodany punkt końcowy **niepołączone**. Kliknij połączenie, aby go skonfigurować.
   
    ![Nie połączono][NotConnected]
   
    Zostanie otwarty blok połączeń hybrydowych.
   
    ![NotConnectedBlade][NotConnectedBlade]
3. W bloku, kliknij **konfiguracji odbiornika**.
   
    ![Kliknij przycisk Ustawienia odbiornika][ClickListenerSetup]
4. **Właściwości połączenia hybrydowe** zostanie otwarty blok. W obszarze **Menedżera połączeń hybrydowych lokalnymi**, wybierz **kliknij tutaj, aby zainstalować**.
   
    ![Kliknij tutaj, aby zainstalować][ClickToInstallHCM]
5. W oknie Uruchamianie aplikacji Ostrzeżenie zabezpieczeń wybierz **Uruchom** aby kontynuować.
   
    ![Wybierz polecenie Uruchom, aby kontynuować][ApplicationRunWarning]
6. W **Kontrola konta użytkownika** okno dialogowe, wybierz **tak**.
   
   ![Wybierz opcję Tak][UAC]
7. Menedżera połączeń hybrydowych jest pobierane i instalowane automatycznie. 
   
    ![Instalowanie][HCMInstalling]
8. Po zakończeniu instalacji kliknij przycisk **Zamknij**.
   
    ![Kliknij przycisk Zamknij][HCMInstallComplete]
   
    Na **połączeń hybrydowych** bloku **stan** zawiera obecnie kolumnę **połączony**. 
   
    ![Stan połączenia][HCStatusConnected]

Teraz, infrastruktura hybrydowa połączenie zostanie zakończone, można utworzyć aplikacji hybrydowych, która korzysta z niego. 

> [!NOTE]
> Poniższe sekcje pokazują, jak użyć połączenie hybrydowe z projektu zaplecza .NET aplikacji mobilnej.
> 
> 

## <a name="configure-the-mobile-app-net-backend-project-to-connect-to-the-sql-server-database"></a>Konfigurowanie projektu zaplecza .NET aplikacji mobilnej do łączenia z bazą danych programu SQL Server
W usłudze App Service Mobile Apps na platformie .NET projekt wewnętrznej bazy danych jest tylko aplikacji sieci web platformy ASP.NET z dodatkowe zestawu Mobile Apps SDK zainstalowany i zainicjować. Aby korzystać z aplikacji sieci web jako zaplecza aplikacji mobilnej, należy najpierw [pobierania i zainicjuj zaplecza Mobile Apps .NET SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).  

Dla aplikacji mobilnych należy również określić parametry połączenia dla lokalnej bazy danych i modyfikować wewnętrznej bazy danych dla tego połączenia. 

1. W Eksploratorze rozwiązań w programie Visual Studio Otwórz plik Web.config dla zaplecza .NET aplikacji mobilnych, odszukaj **connectionStrings** Dodaj nowy wpis SqlClient podobnie do poniższego, która wskazuje na lokalną bazą danych programu SQL Server:
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    Pamiętaj, aby zastąpić `<**secure_password**>` w tym ciągu z hasła utworzonego dla *HybridConnectionLogin*.
2. Kliknij przycisk **zapisać** w programie Visual Studio można zapisać pliku Web.config.
   
   > [!NOTE]
   > To ustawienie połączenia jest używany podczas uruchamiania komputera lokalnego. Podczas uruchamiania na platformie Azure, to ustawienie jest zastąpione przez ustawienie połączenia zdefiniowane w portalu.
   > 
   > 
3. Rozwiń węzeł **modele** folderu i Otwórz plik modelu danych kończy się *Context.cs*.
4. Modyfikowanie **DbContext** konstruktora wystąpienia, aby przekazać wartość `OnPremisesDBConnection` podstawy **DbContext** konstruktora, podobny do następującego fragmentu kodu:
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    Usługa będzie teraz używać nowego połączenia z bazą danych programu SQL Server.

## <a name="update-the-mobile-app-backend-to-use-the-on-premises-connection-string"></a>Zaktualizuj zaplecza aplikacji mobilnej do używania ciągu połączenia lokalnego
Następnie należy dodać ustawienie aplikacji dla tych nowych parametrów połączenia, dzięki czemu mogą być używane z platformy Azure.  

1. W [portalu Azure](https://portal.azure.com) w aplikacji mobilnej kodu zaplecza aplikacji sieci web kliknij **wszystkie ustawienia**, następnie **ustawienia aplikacji**.
2. W **ustawienia aplikacji w sieci Web** bloku, przewiń w dół do **parametry połączenia** i dodać nowe **programu SQL Server** parametrów połączenia o nazwie `OnPremisesDBConnection` o wartości podobnie jak `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    Zastąp `<**secure_password**>` z bezpiecznym hasłem lokalnej bazy danych.
   
    ![Parametry połączenia dla lokalnej bazy danych](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. Naciśnij klawisz **zapisać** zapisać hybrydowego połączenia i połączenia ciągu właśnie utworzony.

W tym momencie możesz ponownie opublikować projekt serwera i przetestować nowego połączenia z klientami istniejące aplikacje mobilne. Dane będą odczytywane i zapisywane w lokalną bazą danych przy użyciu połączenia hybrydowego.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać informacje dotyczące tworzenia aplikacji sieci web ASP.NET, która używa połączenie hybrydowe, zobacz [Połącz z lokalnego serwera SQL z Azure witryny sieci web za pomocą połączeń hybrydowych](http://go.microsoft.com/fwlink/?LinkID=397979). 

### <a name="additional-resources"></a>Dodatkowe zasoby
[Omówienie połączeń hybrydowych](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Dołączony Josha wprowadza połączeń hybrydowych (wideo z witryny Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Witryna sieci web połączenia hybrydowego](https://azure.microsoft.com/services/biztalk-services/)

[Usługi BizTalk Services: Karty Pulpit nawigacyjny, Monitor skali, konfigurowanie i połączenia hybrydowego](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Tworzenie hybrydowego rzeczywistych chmury chronionej za pomocą bezproblemowe przenośność aplikacji (Channel 9 wideo)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Nawiązywanie połączenia lokalnego serwera SQL z usług Azure Mobile Services za pomocą połączeń hybrydowych (wideo z witryny Channel 9)](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

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
