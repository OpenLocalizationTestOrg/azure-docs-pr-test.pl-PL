---
title: "Połączenie z lokalnym programem SQL Server z aplikacji sieci web w usłudze Azure App Service przy użyciu połączeń hybrydowych"
description: "Tworzenie aplikacji sieci web w systemie Microsoft Azure i połącz go z lokalną bazą danych programu SQL Server"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 12456ef3e2aecfa7a03cca97de2ff6ffd9602357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>Połączenie z lokalnym programem SQL Server z aplikacji sieci web w usłudze Azure App Service przy użyciu połączeń hybrydowych
Nawiązanie połączenia hybrydowe [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web z lokalnymi zasobami, które użycia portu statycznego TCP. Obsługiwane zasoby obejmują programu Microsoft SQL Server, MySQL, interfejsy API protokołu HTTP sieci Web, usługi aplikacji i większość niestandardowych usług sieci Web.

Z tego samouczka, dowiesz sposób tworzenia aplikacji sieci web usługi aplikacji w [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), połączenia z bazą danych programu SQL Server lokalne lokalnymi, przy użyciu nowych funkcji hybrydowych połączenia aplikacji sieci web, utworzyć prostą aplikację ASP.NET do użycia przez połączenie hybrydowe, a wdrożenie aplikacji w aplikacji sieci web usługi aplikacji. Aplikacja sieci web ukończone na platformie Azure przechowuje poświadczenia użytkownika w bazie danych członkostwa, które jest używane lokalne. W samouczku założono nie wcześniejszego doświadczenia w używaniu platformy Azure lub programu ASP.NET.

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> Aplikacje sieci Web część funkcji połączeń hybrydowych było możliwe jest dostępna tylko w [Azure Portal](https://portal.azure.com). Aby utworzyć połączenie w usługi BizTalk Services, zobacz [połączeń hybrydowych](http://go.microsoft.com/fwlink/p/?LinkID=397274).  
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Do ukończenia tego samouczka należy następujące produkty. Dostępne są wszystkie w bezpłatnej wersji, aby rozpocząć tworzenie aplikacji dla platformy Azure i całkowicie bezpłatne.

* **Subskrypcja platformy Azure** — w przypadku bezpłatnej subskrypcji, zobacz [bezpłatnej wersji próbnej Azure](/pricing/free-trial/).
* **Visual Studio 2013** — Aby pobrać bezpłatną wersję próbną programu Visual Studio 2013, zobacz [programu Visual Studio pobiera](http://www.visualstudio.com/downloads/download-visual-studio-vs). Zainstaluj to przed kontynuowaniem.
* **Program Microsoft .NET Framework 3.5 z dodatkiem Service Pack 1** — w przypadku systemu operacyjnego Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 lub Windows Server 2008 R2, możesz je włączyć, w Panelu sterowania > programy i funkcje > Włącz lub wyłącz funkcje systemu Windows. W przeciwnym razie możesz pobrać go z [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).
* **SQL Server 2014 Express with Tools** — Microsoft SQL Server Express bezpłatnie pobrać na [strona bazy danych platformy sieci Web Microsoft](http://www.microsoft.com/web/platform/database.aspx). Wybierz **Express** (nie LocalDB) wersji. **Express with Tools** wersja obejmuje program SQL Server Management Studio, który będzie używany w tym samouczku.
* **SQL Server Management Studio Express** — jest on dołączony do programu SQL Server 2014 Express pobierania narzędzia wymienionych powyżej, ale jeśli musisz zainstalować oddzielnie, można pobrać i zainstalować go z [strony pobierania programu SQL Server Express](http://www.microsoft.com/web/platform/database.aspx).

Samouczka przyjęto założenie, że masz subskrypcję platformy Azure, zainstalowanego programu Visual Studio 2013 i czy masz zainstalowany lub włączony program .NET Framework 3.5. Samouczek przedstawia sposób instalowania programu SQL Server 2014 Express w konfiguracji, które działa dobrze z funkcją Azure połączeń hybrydowych (domyślnego wystąpienia z portu statycznego TCP). Przed rozpoczęciem tego samouczka, Pobierz program SQL Server 2014 Express with Tools z lokalizacji wymienionych powyżej, jeśli nie masz zainstalowanego programu SQL Server.

### <a name="notes"></a>Uwagi
Aby użyć lokalnego programu SQL Server lub SQL Server Express bazy danych z połączenia hybrydowego, TCP/IP musi być włączona na portu statycznego. Domyślne wystąpienia w programie SQL Server używać portu statycznego 1433, nazwanych wystąpień nie.

Komputer, na którym należy zainstalować agenta menedżera połączeń hybrydowych lokalnie:

* Musi mieć łączność wychodząca Azure za pośrednictwem:

| Port | Dlaczego |
| --- | --- |
| 80 |**Wymagane** dla portu HTTP dla certyfikatu weryfikacji i opcjonalnie łączności danych. |
| 443 |**Opcjonalne** połączeń danych. Jeśli łączność wychodząca 443 jest niedostępna, jest używany TCP port 80. |
| 5671 i 9352 |**Zalecane** , ale opcjonalne dla połączenia danych. Należy pamiętać, że w tym trybie zwykle zapewnia wyższą przepływność. Jeśli łączność wychodząca tych portów jest niedostępna, jest używany TCP port 443. |

* Musi być możliwe nawiązanie łączności *hostname*:*numer_portu* zasobu lokalnego.

Kroki opisane w tym artykule założono, że używasz przeglądarki z komputera, który będzie hostem agenta połączenia hybrydowego lokalnymi.

Jeśli masz już programu SQL Server zainstalowanego w konfiguracji i w środowisku, które spełnia warunki opisane powyżej, możesz przejść od razu i rozpoczynać [Utwórz bazę danych programu SQL Server lokalne](#CreateSQLDB).

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>A. Instalowanie programu SQL Server Express, Włącz protokół TCP/IP i utworzyć lokalnej bazy danych programu SQL Server
W tej sekcji przedstawiono sposób instalowania programu SQL Server Express, Włącz protokół TCP/IP i utworzyć bazę danych, aby działały aplikacji sieci web przy użyciu portalu Azure.

### <a name="install-sql-server-express"></a>Zainstaluj program SQL Server Express
1. Aby zainstalować program SQL Server Express, uruchom **SQLEXPRWT_x64_ENU.exe** lub **SQLEXPR_x86_ENU.exe** pobranego pliku. Zostanie wyświetlony Kreator Centrum instalacji programu SQL Server.
   
    ![Instalacja serwera SQL][SQLServerInstall]
2. Wybierz **nowy serwer SQL instalacji autonomicznej lub Dodaj funkcje do istniejącej instalacji**. Postępuj zgodnie z instrukcjami, przyjmuje opcje domyślne i ustawienia, aż do **Konfiguracja wystąpienia** strony.
3. Na **Konfiguracja wystąpienia** wybierz pozycję **domyślnego wystąpienia**.
   
    ![Wybierz wystąpienie domyślne][ChooseDefaultInstance]
   
    Domyślnie domyślnego wystąpienia programu SQL Server nasłuchuje żądań od klientów programu SQL Server na statycznych porcie 1433, czyli wymaga funkcji połączeń hybrydowych było możliwe. Nazwane wystąpienia używać portów dynamicznych i UDP, które nie są obsługiwane przez połączeń hybrydowych było możliwe.
4. Zaakceptuj wartości domyślne na **konfiguracji serwera** strony.
5. Na **Konfiguracja aparatu bazy danych** w obszarze **tryb uwierzytelniania**, wybierz **trybu mieszanego (uwierzytelnianie programu SQL Server i uwierzytelniania systemu Windows)**i podaj hasło.
   
    ![Wybierz tryb mieszany][ChooseMixedMode]
   
    W tym samouczku będziesz używać uwierzytelniania programu SQL Server. Należy zapamiętać hasło, które zostaną podane, ponieważ będzie potrzebny później.
6. Kroków opisanych w pozostałej części kreatora w celu ukończenia instalacji.

### <a name="enable-tcpip"></a>Włącz protokół TCP/IP
Aby włączyć protokół TCP/IP, używasz programu SQL Server Configuration Manager, który został zainstalowany przed zainstalowaniem programu SQL Server Express. Postępuj zgodnie z instrukcjami [Włącz protokół dla programu SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) przed kontynuowaniem.

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>Utwórz bazę danych programu SQL Server lokalne
Aplikacja sieci web programu Visual Studio wymaga Azure można uzyskać dostępu do bazy danych członkostwa. Wymaga to bazy danych programu SQL Server lub SQL Server Express (nie LocalDB bazy danych, która domyślnie używa szablonu MVC), więc następnie utworzysz bazie danych członkostwa.

1. W programu SQL Server Management Studio nawiąż połączenie z programem SQL Server został właśnie zainstalowany. (Jeśli **Połącz z serwerem** okna dialogowego nie zostanie wyświetlone automatycznie, przejdź do **Eksplorator obiektów** w okienku po lewej stronie kliknij **Connect**, a następnie kliknij przycisk **aparatu bazy danych**.) ![Połączyć się z serwerem][SSMSConnectToServer]
   
    Aby uzyskać **typ serwera**, wybierz **aparatu bazy danych**. Aby uzyskać **nazwy serwera**, można użyć **localhost** lub nazwę komputera, którego używasz. Wybierz **uwierzytelniania programu SQL Server**, a następnie zaloguj się za pomocą nazwy użytkownika i hasła, który został utworzony wcześniej.
2. Aby utworzyć nową bazę danych przy użyciu programu SQL Server Management Studio, kliknij prawym przyciskiem myszy **baz danych** w Eksploratorze obiektów, a następnie kliknij przycisk **nową bazę danych**.
   
    ![Utwórz nową bazę danych][SSMScreateNewDB]
3. W **nową bazę danych** okna dialogowego, wprowadź MembershipDB dla nazwy bazy danych, a następnie kliknij przycisk **OK**.
   
    ![Podaj nazwę bazy danych][SSMSprovideDBname]
   
    Należy pamiętać, że użytkownik nie wprowadzaj żadnych zmian w bazie danych w tym momencie. Informacje o członkostwie zostaną automatycznie później dodane przez aplikację sieci web po jej uruchomieniu.
4. W Eksploratorze obiektów po rozwinięciu **baz danych**, zobaczysz, że utworzono bazy danych członkostwa.
   
    ![MembershipDB utworzone][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a>B. Tworzenie aplikacji sieci web w portalu Azure
> [!NOTE]
> Jeśli utworzono już aplikacji sieci web w portalu Azure, który ma być używany na potrzeby tego samouczka, możesz przejść od razu do [Tworzenie połączenia hybrydowego i usługi BizTalk](#CreateHC) i kontynuować stamtąd.
> 
> 

1. W [Azure Portal](https://portal.azure.com), kliknij przycisk **nowy** > **sieci Web i mobilność** > **aplikacji sieci Web**.
   
    ![Przycisk Nowy][New]
2. Konfigurowanie aplikacji sieci web, a następnie kliknij przycisk **Utwórz**.
   
    ![Nazwa witryny sieci Web][WebsiteCreationBlade]
3. Po kilku chwilach aplikacji sieci web jest tworzona i pojawia się jego bloku aplikacja sieci web. Blok jest pionowo przewijanego pulpit nawigacyjny, który umożliwia zarządzanie aplikacji sieci web.
   
    ![Witryny sieci Web uruchomionej][WebSiteRunningBlade]
   
    Aby potwierdzić, aplikacji sieci web na żywo, można kliknąć **Przeglądaj** ikonę, aby wyświetlić stronę domyślną.

Następnie utworzysz połączenie hybrydowe i usługa BizTalk aplikacji sieci web.

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. Tworzenie połączenia hybrydowego i usługi BizTalk
1. Wstecz w portalu, przejdź do ustawień i kliknij przycisk **sieci** > **skonfiguruj punkty końcowe połączenia hybrydowego**.
   
    ![Połączenia hybrydowe][CreateHCHCIcon]
2. W bloku połączeń hybrydowych, kliknij **Dodaj** > **nowe połączenie hybrydowe**.
3. Na **Tworzenie połączenia hybrydowego** bloku:
   
   * Aby uzyskać **nazwa**, podaj nazwę dla połączenia.
   * Aby uzyskać **Hostname**, wpisz nazwę komputera komputera-hosta programu SQL Server.
   * Aby uzyskać **portu**, wprowadź 1433 (port domyślny dla programu SQL Server).
   * Kliknij przycisk **usługi BizTalk** > **nową usługę BizTalk** , a następnie wprowadź nazwę usługi BizTalk.
     
     ![Tworzenie połączenia hybrydowego][TwinCreateHCBlades]
4. Kliknij przycisk **OK** dwa razy.
   
    Po zakończeniu tego procesu, **powiadomienia** obszaru będzie flash zielona **Powodzenie** i **połączenia hybrydowego** bloku zostaną wyświetlone nowe połączenie hybrydowe o stanie jako **niepołączone**.
   
    ![Połączenia hybrydowe jeden utworzone][CreateHCOneConnectionCreated]

W tym momencie została ukończona ważnym elementem infrastruktury połączenia hybrydowe w chmurze. Następnie utworzy odpowiedni element lokalnymi.

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a>D. Zainstaluj Menedżera połączeń hybrydowych lokalnego, aby nawiązać połączenie
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

Teraz, infrastruktura hybrydowa połączenie zostanie zakończone, spowoduje utworzenie aplikacji sieci web, która korzysta z niego.

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a>E. Tworzenie podstawowego projektu sieci web programu ASP.NET, Edytuj parametry połączenia bazy danych i uruchamianie projektu lokalnie
### <a name="create-a-basic-aspnet-project"></a>Tworzenie podstawowego projektu programu ASP.NET
1. W programie Visual Studio na **pliku** menu, Utwórz nowy projekt:
   
    ![Nowy projekt programu Visual Studio][HCVSNewProject]
2. W **szablony** sekcji **nowy projekt** okno dialogowe, wybierz opcję **sieci Web** i wybierz polecenie **aplikacji sieci Web ASP.NET**, a następnie kliknij przycisk **OK**.
   
    ![Wybierz aplikację sieci Web ASP.NET][HCVSChooseASPNET]
3. W **nowy projekt ASP.NET** okno dialogowe, wybierz **MVC**, a następnie kliknij przycisk **OK**.
   
    ![Wybierz MVC][HCVSChooseMVC]
4. Po utworzeniu projektu, zostanie wyświetlona strona readme aplikacji. Nie należy jeszcze uruchamiać projektu sieci web.
   
    ![Stronę Readme][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a>Edytuj parametry połączenia bazy danych dla aplikacji
W tym kroku możesz edytować parametry połączenia, które informuje aplikacji, gdzie można znaleźć lokalnej bazy danych programu SQL Server Express. Parametry połączenia są w pliku Web.config aplikacji, który zawiera informacje o konfiguracji dla aplikacji.

> [!NOTE]
> Aby upewnić się, że aplikacja korzysta z bazy danych utworzonej w programu SQL Server Express, a nie do domyślnej programu Visual Studio LocalDB, ważne jest ukończenia tego kroku przed uruchomieniem projektu.
> 
> 

1. W Eksploratorze rozwiązań kliknij dwukrotnie plik Web.config.
   
    ![Web.config][HCVSChooseWebConfig]
2. Edytuj **connectionStrings** sekcji, aby wskazywał bazy danych programu SQL Server na komputerze lokalnym, składni w następującym przykładzie:
   
    ![Parametry połączenia][HCVSConnectionString]
   
    Podczas tworzenia ciągu połączenia, należy pamiętać następujące czynności:
   
   * Jeśli łączysz się z wystąpieniem nazwanym, a wystąpienia domyślnego (na przykład YourServer\SQLEXPRESS), należy skonfigurować program SQL Server do korzystania z portów statycznych. Informacje dotyczące konfigurowania portów statycznych, zobacz [sposób konfigurowania programu SQL Server do nasłuchiwania na konkretnym porcie](http://support.microsoft.com/kb/823938). Domyślnie nazwane wystąpienia używają protokołów UDP i porty dynamiczne, które nie są obsługiwane przez połączeń hybrydowych było możliwe.
   * Zalecane jest, aby określić port (1433 domyślnie, jak pokazano w przykładzie) w parametrach połączenia, dzięki czemu użytkownik może upewnij się, że lokalny serwer SQL został włączony protokół TCP i używa poprawnego portu.
   * Pamiętaj, aby używać uwierzytelniania programu SQL Server do połączenia, określenie Identyfikatora użytkownika i hasła w ciągu połączenia.
3. Kliknij przycisk **zapisać** w programie Visual Studio można zapisać pliku Web.config.

### <a name="run-the-project-locally-and-register-a-new-user"></a>Uruchamianie projektu lokalnie i zarejestrować nowego użytkownika
1. Teraz Uruchom nowego projektu sieci web lokalnie, klikając przycisk przeglądania w obszarze debugowania. W tym przykładzie użyto programu Internet Explorer.
   
    ![Uruchom projekt][HCVSRunProject]
2. W prawym górnym rogu domyślnej strony sieci web, wybierz polecenie **zarejestrować** zarejestrować nowe konto:
   
    ![Zarejestruj nowe konto][HCVSRegisterLocally]
3. Wprowadź nazwę użytkownika i hasło:
   
    ![Wprowadź nazwę użytkownika i hasło][HCVSCreateNewAccount]
   
    Powoduje to automatyczne utworzenie bazy danych na serwerze SQL lokalnej, która przechowuje informacje o członkostwie dla aplikacji. Jedną z tabel (**dbo. AspNetUsers**) blokad sieci web poświadczenia użytkownika aplikacji, takich jak te, które zostały wprowadzone. Zobaczysz tej tabeli później w samouczku.
4. Zamknij okno przeglądarki domyślnej strony sieci web. Powoduje to zatrzymanie aplikacji w programie Visual Studio.

Teraz można przystąpić do następnego kroku, która umożliwia publikowanie aplikacji na platformie Azure i przetestować go.

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a>F. Publikowanie aplikacji sieci web na platformie Azure i przetestować go
Teraz będziesz opublikować aplikację do aplikacji sieci web usługi aplikacji, a następnie sprawdź go, aby sprawdzić, jak jest używane przez skonfigurowane wcześniej połączenie hybrydowe także łączenie aplikacji sieci web do bazy danych na komputerze lokalnym.

### <a name="publish-the-web-application"></a>Publikowanie aplikacji sieci web
1. Można pobrać profilu publikowania dla aplikacji sieci web usługi aplikacji w portalu Azure. W bloku aplikacja sieci web, kliknij przycisk **profilu publikowania Get**, a następnie zapisz plik na komputerze.
   
    ![Pobieranie profilu publikowania][PortalDownloadPublishProfile]
   
    Zostanie następnie zaimportować ten plik do aplikacji sieci web programu Visual Studio.
2. W programie Visual Studio, kliknij prawym przyciskiem myszy nazwę projektu w Eksploratorze rozwiązań i wybierz **publikowania**.
   
    ![Wybierz publikowania][HCVSRightClickProjectSelectPublish]
3. W **publikowanie w sieci Web** okna dialogowego na **profilu** , wybierz pozycję **importu**.
   
    ![Import][HCVSPublishWebDialogImport]
4. Przejdź do pobrany profil publikowania, zaznacz go, a następnie kliknij **OK**.
   
    ![Przejdź do profilu][HCVSBrowseToImportPubProfile]
5. Publikowanie informacji jest importowany i wyświetla na **połączenia** karcie okna dialogowego.
   
    ![Kliknij przycisk Publikuj][HCVSClickPublish]
   
    Kliknij przycisk **Opublikuj**.
   
    Po ukończeniu publikowania przeglądarki będzie uruchomić i pokazać teraz znanych aplikacji ASP.NET--z tą różnicą, że jest teraz na żywo w chmurze Azure!

Następnie użyje aplikacji sieci web na żywo aby zobaczyć jego połączenia hybrydowego, w akcji.

### <a name="test-the-completed-web-application-on-azure"></a>Testowanie ukończonej aplikacji sieci web na platformie Azure
1. U góry po prawej stronie sieci web na platformie Azure, wybierz **Zaloguj**.
   
    ![Dziennik testu w][HCTestLogIn]
2. Aplikacja sieci web usługi aplikacji jest teraz połączenie bazy danych członkostwa aplikacji sieci web na komputerze lokalnym. Aby to sprawdzić, zaloguj się za pomocą tych samych poświadczeń, które wcześniej wprowadzony w lokalnej bazie danych.
   
    ![Witaj pozdrowienia][HCTestHelloContoso]
3. Dodatkowo sprawdź nowe połączenie hybrydowe, wylogować się z aplikacji sieci web platformy Azure i Zarejestruj się jako inny użytkownik. Podaj nową nazwę użytkownika i hasło, a następnie kliknij przycisk **zarejestrować**.
   
    ![Test zarejestrować innego użytkownika][HCTestRegisterRelecloud]
4. Aby zweryfikować, że poświadczenia nowego użytkownika były przechowywane w lokalnej bazie danych za pośrednictwem połączenia hybrydowe, Otwórz program SQL Management Studio na komputerze lokalnym. W Eksploratorze obiektów rozwiń **MembershipDB** bazy danych, a następnie rozwiń **tabel**. Kliknij prawym przyciskiem myszy **dbo. AspNetUsers** członkostwa tabeli i wybierz polecenie **zaznacz 1000 pierwszych wierszy** , aby wyświetlić wyniki.
   
    ![Wyświetlenie wyników][HCTestSSMSTree]
5. Członkostwo w lokalnej tabeli teraz zawiera oba konta — ten, który został utworzony lokalnie, a ten, który został utworzony w chmurze Azure. Ten, który został utworzony w chmurze zostały zapisane w lokalnej bazie danych za pomocą funkcji połączenie hybrydowe platformy Azure.
   
    ![Zarejestrowani użytkownicy w lokalnej bazie danych][HCTestShowMemberDb]

Możesz teraz utworzeniu i wdrożeniu aplikacji sieci web ASP.NET, która używa połączenie hybrydowe między aplikacji sieci web w chmurze platformy Azure i lokalną bazą danych programu SQL Server. Gratulacje!

## <a name="see-also"></a>Zobacz też
[Omówienie połączeń hybrydowych](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Dołączony Josha wprowadza połączeń hybrydowych (wideo z witryny Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Omówienie połączeń hybrydowych](/services/biztalk-services/)

[Usługi BizTalk Services: Karty Pulpit nawigacyjny, Monitor skali, konfigurowanie i połączenia hybrydowego](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Tworzenie hybrydowego rzeczywistych chmury chronionej za pomocą bezproblemowe przenośność aplikacji (Channel 9 wideo)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Dostęp do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service](web-sites-hybrid-connection-get-started.md)

[Tożsamość platformy ASP.NET — omówienie](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
