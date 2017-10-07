---
title: "aaaConnect tooon lokalnego programu SQL Server z aplikacji sieci web w usłudze Azure App Service przy użyciu połączeń hybrydowych"
description: "Tworzenie aplikacji sieci web w systemie Microsoft Azure i podłącz go tooan lokalną bazą danych programu SQL Server"
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
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>Nawiązywanie połączenia lokalnego tooon programu SQL Server z aplikacji sieci web w usłudze Azure App Service przy użyciu połączeń hybrydowych
Nawiązanie połączenia hybrydowe [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) zasobów tooon lokalnych aplikacji sieci Web, które użycia portu statycznego TCP. Obsługiwane zasoby obejmują programu Microsoft SQL Server, MySQL, interfejsy API protokołu HTTP sieci Web, usługi aplikacji i większość niestandardowych usług sieci Web.

Z tego samouczka, dowiesz się, jak toocreate usługę aplikacji sieci web aplikacji w hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715)Połącz z hello sieci web aplikacji tooyour lokalnego lokalnej bazy danych SQL Server przy użyciu nowej funkcji połączenia hybrydowego hello, Utwórz prosty program ASP.NET Aplikacja, która będzie używać połączenia hybrydowego hello i wdróż toohello aplikacji hello aplikacji sieci web usługi aplikacji. ukończyć powitalnych aplikacji sieci web na platformie Azure są przechowywane poświadczenia użytkownika w bazie danych członkostwa, które jest używane lokalne. Witaj samouczek zakłada nie wcześniejszego doświadczenia w używaniu platformy Azure lub programu ASP.NET.

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> Witaj aplikacje sieci Web część funkcji połączeń hybrydowych hello jest dostępna tylko w hello [Azure Portal](https://portal.azure.com). Zobacz toocreate połączenie usługi BizTalk Services [połączeń hybrydowych](http://go.microsoft.com/fwlink/p/?LinkID=397274).  
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka będziesz potrzebować hello następujące produkty. Dostępne są wszystkie w bezpłatnej wersji, aby rozpocząć tworzenie aplikacji dla platformy Azure i całkowicie bezpłatne.

* **Subskrypcja platformy Azure** — w przypadku bezpłatnej subskrypcji, zobacz [bezpłatnej wersji próbnej Azure](/pricing/free-trial/).
* **Visual Studio 2013** -toodownload bezpłatną wersję próbną programu Visual Studio 2013, zobacz [programu Visual Studio pobiera](http://www.visualstudio.com/downloads/download-visual-studio-vs). Zainstaluj to przed kontynuowaniem.
* **Program Microsoft .NET Framework 3.5 z dodatkiem Service Pack 1** — w przypadku systemu operacyjnego Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 lub Windows Server 2008 R2, możesz je włączyć, w Panelu sterowania > programy i funkcje > Włącz lub wyłącz funkcje systemu Windows. W przeciwnym razie można go pobrać z hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).
* **SQL Server 2014 Express with Tools** — Microsoft SQL Server Express bezpłatnie pobrać na powitania [strona bazy danych platformy sieci Web Microsoft](http://www.microsoft.com/web/platform/database.aspx). Wybierz hello **Express** (nie LocalDB) wersji. Witaj **Express with Tools** wersja obejmuje program SQL Server Management Studio, który będzie używany w tym samouczku.
* **SQL Server Management Studio Express** — jest on dołączony do programu SQL Server 2014 Express hello pobierania narzędzia wymienionych powyżej, ale jeśli potrzebujesz tooinstall go oddzielnie, można pobrać i zainstalować go z hello [programu SQL Server Express strona pobierania](http://www.microsoft.com/web/platform/database.aspx).

Hello samouczku założono, że masz subskrypcję platformy Azure, zainstalowanego programu Visual Studio 2013 i czy masz zainstalowany lub włączony program .NET Framework 3.5. Witaj samouczek pokazuje, jak tooinstall programu SQL Server 2014 Express w konfiguracji, które działa dobrze w przypadku połączeń hybrydowych hello Azure funkcji (domyślnego wystąpienia z portu statycznego TCP). Przed rozpoczęciem samouczka hello, Pobierz program SQL Server 2014 Express with Tools z lokalizacji hello wymienione powyżej, jeśli nie masz zainstalowanego programu SQL Server.

### <a name="notes"></a>Uwagi
toouse lokalnego programu SQL Server lub SQL Server Express bazy danych z połączenia hybrydowego TCP/IP musi toobe włączone portu statycznego. Domyślne wystąpienia w programie SQL Server używać portu statycznego 1433, nazwanych wystąpień nie.

Hello komputera, na którym należy zainstalować agenta menedżera połączeń hybrydowych lokalne powitania:

* Musi mieć łączność wychodząca tooAzure przez:

| Port | Dlaczego |
| --- | --- |
| 80 |**Wymagane** dla portu HTTP dla certyfikatu weryfikacji i opcjonalnie łączności danych. |
| 443 |**Opcjonalne** połączeń danych. Jeśli too443 łączność wychodząca jest niedostępna, jest używany TCP port 80. |
| 5671 i 9352 |**Zalecane** , ale opcjonalne dla połączenia danych. Należy pamiętać, że w tym trybie zwykle zapewnia wyższą przepływność. Jeśli porty toothese łączność wychodząca jest niedostępna, jest używany TCP port 443. |

* Musi być w stanie tooreach hello *hostname*:*numer_portu* zasobu lokalnego.

Hello opisanych w tym artykule założono, że używasz przeglądarki hello z hello komputer, który będzie hostem agenta połączenia hybrydowego lokalne powitania.

Jeśli masz już programu SQL Server zainstalowanego w konfiguracji i w środowisku, które spełnia warunki hello opisane powyżej, możesz przejść od razu i rozpoczynać [Utwórz bazę danych programu SQL Server lokalne](#CreateSQLDB).

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>A. Instalowanie programu SQL Server Express, Włącz protokół TCP/IP i utworzyć lokalnej bazy danych programu SQL Server
W tej sekcji przedstawiono sposób tooinstall programu SQL Server Express, Włącz protokół TCP/IP i utworzyć bazę danych tak, aby aplikacja sieci web będzie działać z hello portalu Azure.

### <a name="install-sql-server-express"></a>Zainstaluj program SQL Server Express
1. tooinstall programu SQL Server Express, uruchom hello **SQLEXPRWT_x64_ENU.exe** lub **SQLEXPR_x86_ENU.exe** pobranego pliku. zostanie wyświetlony Kreator Centrum instalacji programu SQL Server Hello.
   
    ![Instalacja serwera SQL][SQLServerInstall]
2. Wybierz **nowy serwer SQL instalacji autonomicznej lub Dodaj funkcje tooan istniejącej instalacji**. Wykonaj instrukcje hello, akceptując hello opcje domyślne i ustawienia, do momentu uzyskania toohello **Konfiguracja wystąpienia** strony.
3. Na powitania **Konfiguracja wystąpienia** wybierz pozycję **domyślnego wystąpienia**.
   
    ![Wybierz wystąpienie domyślne][ChooseDefaultInstance]
   
    Domyślnie hello domyślnego wystąpienia programu SQL Server nasłuchuje żądań od klientów programu SQL Server na statycznych porcie 1433, czyli jakie hello funkcja wymaga połączeń hybrydowych. Nazwane wystąpienia używać portów dynamicznych i UDP, które nie są obsługiwane przez połączeń hybrydowych było możliwe.
4. Zaakceptuj ustawienia domyślne hello na powitania **konfiguracji serwera** strony.
5. Na powitania **Konfiguracja aparatu bazy danych** w obszarze **tryb uwierzytelniania**, wybierz **trybu mieszanego (uwierzytelnianie programu SQL Server i uwierzytelniania systemu Windows)**i podaj hasło.
   
    ![Wybierz tryb mieszany][ChooseMixedMode]
   
    W tym samouczku będziesz używać uwierzytelniania programu SQL Server. Należy się tooremember hello hasła, ponieważ będzie potrzebny później.
6. Przejrzyj kroki hello reszty hello kreatora toocomplete hello instalacji.

### <a name="enable-tcpip"></a>Włącz protokół TCP/IP
tooenable TCP/IP użyjesz programu SQL Server Configuration Manager, który został zainstalowany przed zainstalowaniem programu SQL Server Express. Wykonaj kroki hello w [Włącz protokół dla programu SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) przed kontynuowaniem.

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>Utwórz bazę danych programu SQL Server lokalne
Aplikacja sieci web programu Visual Studio wymaga Azure można uzyskać dostępu do bazy danych członkostwa. Wymaga to bazy danych programu SQL Server lub SQL Server Express (nie hello bazie danych LocalDB który hello używa szablonu MVC domyślnie), więc następnie utworzysz hello członkostwa w bazie danych.

1. W programu SQL Server Management Studio połącz toohello programu SQL Server został właśnie zainstalowany. (Jeśli hello **połączyć tooServer** okna dialogowego nie zostanie wyświetlone automatycznie, przejdź do zbyt**Eksplorator obiektów** w okienku po lewej stronie powitania kliknij **Connect**, a następnie kliknij przycisk **Bazy danych aparatu**.) ![Połącz tooServer][SSMSConnectToServer]
   
    Aby uzyskać **typ serwera**, wybierz **aparatu bazy danych**. Dla **nazwy serwera**, można użyć **localhost** lub nazwa hello hello komputera, którego używasz. Wybierz **uwierzytelniania programu SQL Server**, a następnie zaloguj się za pomocą hello nazwy użytkownika i hasła hello, utworzony wcześniej.
2. Kliknij prawym przyciskiem myszy nową bazę danych przy użyciu programu SQL Server Management Studio, toocreate **baz danych** w Eksploratorze obiektów, a następnie kliknij przycisk **nową bazę danych**.
   
    ![Utwórz nową bazę danych][SSMScreateNewDB]
3. W hello **nową bazę danych** okna dialogowego, wprowadź MembershipDB hello nazwy bazy danych, a następnie kliknij przycisk **OK**.
   
    ![Podaj nazwę bazy danych][SSMSprovideDBname]
   
    Należy pamiętać, że nie wprowadzisz wszystkie bazy danych toohello zmiany w tym momencie. informacje o członkostwie w Hello zostaną automatycznie później dodane przez aplikację sieci web po uruchomieniu.
4. W Eksploratorze obiektów po rozwinięciu **baz danych**, zobaczysz tej bazy danych członkostwa hello został utworzony.
   
    ![MembershipDB utworzone][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a>B. Tworzenie aplikacji sieci web w hello portalu Azure
> [!NOTE]
> Jeśli utworzono już aplikacji sieci web w hello mają toouse w tym samouczku portalu Azure, możesz przejść od razu zbyt[Tworzenie połączenia hybrydowego i usługi BizTalk](#CreateHC) i kontynuować stamtąd.
> 
> 

1. W hello [Azure Portal](https://portal.azure.com), kliknij przycisk **nowy** > **sieci Web i mobilność** > **aplikacji sieci Web**.
   
    ![Przycisk Nowy][New]
2. Konfigurowanie aplikacji sieci web, a następnie kliknij przycisk **Utwórz**.
   
    ![Nazwa witryny sieci Web][WebsiteCreationBlade]
3. Po kilku chwilach hello aplikacji sieci web jest tworzona i pojawia się jego bloku aplikacja sieci web. Blok Hello jest pionowo przewijanego pulpit nawigacyjny, który umożliwia zarządzanie aplikacji sieci web.
   
    ![Witryny sieci Web uruchomionej][WebSiteRunningBlade]
   
    Aplikacja sieci web hello tooverify jest na żywo, można kliknąć hello **Przeglądaj** ikona toodisplay hello domyślnej strony.

Następnie utworzysz, połączenie hybrydowe i usługi BizTalk hello aplikacji sieci web.

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. Tworzenie połączenia hybrydowego i usługi BizTalk
1. Wstecz w hello portalu, przejdź do pozycji toosettings i kliknij przycisk **sieci** > **skonfiguruj punkty końcowe połączenia hybrydowego**.
   
    ![Połączenia hybrydowe][CreateHCHCIcon]
2. W bloku połączeń hybrydowych hello, kliknij **Dodaj** > **nowe połączenie hybrydowe**.
3. Na powitania **Tworzenie połączenia hybrydowego** bloku:
   
   * Aby uzyskać **nazwa**, podaj nazwę hello połączenia.
   * Aby uzyskać **Hostname**, wpisz nazwę komputera hello komputera-hosta programu SQL Server.
   * Aby uzyskać **portu**, wprowadź 1433 (hello domyślny port dla programu SQL Server).
   * Kliknij przycisk **usługi BizTalk** > **nową usługę BizTalk** , a następnie wprowadź nazwę hello usługi BizTalk.
     
     ![Tworzenie połączenia hybrydowego][TwinCreateHCBlades]
4. Kliknij przycisk **OK** dwa razy.
   
    Gdy hello zakończeniu procesu hello **powiadomienia** obszaru będzie flash zielona **Powodzenie** i hello **połączenia hybrydowego** bloku wyświetli hello nowe połączenie hybrydowe z Witaj statusu **niepołączone**.
   
    ![Połączenia hybrydowe jeden utworzone][CreateHCOneConnectionCreated]

W tym momencie została ukończona ważnym elementem hello chmury hybrydowej połączenia infrastruktury. Następnie utworzy odpowiedni element lokalnymi.

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>D. Zainstaluj hello lokalnego Menedżera połączeń hybrydowych toocomplete hello połączenia
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

Po zakończeniu tego połączenia infrastruktura hybrydowa hello spowoduje utworzenie aplikacji sieci web, która korzysta z niego.

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a>E. Utworzyć podstawowy projekt sieci web ASP.NET, Edytuj parametry połączenia bazy danych hello i uruchomić projekt hello lokalnie
### <a name="create-a-basic-aspnet-project"></a>Tworzenie podstawowego projektu programu ASP.NET
1. W programie Visual Studio na powitania **pliku** menu, Utwórz nowy projekt:
   
    ![Nowy projekt programu Visual Studio][HCVSNewProject]
2. W hello **szablony** sekcji hello **nowy projekt** okno dialogowe, wybierz opcję **sieci Web** i wybierz polecenie **aplikacji sieci Web ASP.NET**, a następnie kliknij przycisk  **OK**.
   
    ![Wybierz aplikację sieci Web ASP.NET][HCVSChooseASPNET]
3. W hello **nowy projekt ASP.NET** okno dialogowe, wybierz **MVC**, a następnie kliknij przycisk **OK**.
   
    ![Wybierz MVC][HCVSChooseMVC]
4. Po utworzeniu projektu hello, zostanie wyświetlona strona readme aplikacji hello. Nie należy jeszcze uruchamiać hello projektu sieci web.
   
    ![Stronę Readme][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a>Edytuj parametry połączenia bazy danych hello aplikacji hello
W tym kroku, Edytuj parametry połączenia hello informujący o posiadanych aplikacji gdzie toofind Twojego lokalny program SQL Server Express bazy danych. Parametry połączenia Hello są w pliku Web.config aplikacji hello, który zawiera informacje dotyczące konfiguracji aplikacji hello.

> [!NOTE]
> tooensure używanych przez aplikację hello bazy danych, utworzony w programu SQL Server Express, a nie hello jedną domyślnej programu Visual Studio LocalDB, ważne jest ukończenia tego kroku przed uruchomieniem projektu.
> 
> 

1. W Eksploratorze rozwiązań kliknij dwukrotnie plik Web.config hello.
   
    ![Web.config][HCVSChooseWebConfig]
2. Edytuj hello **connectionStrings** bazy danych programu SQL Server toohello toopoint sekcji na komputerze lokalnym, składni hello w hello poniższy przykład:
   
    ![Parametry połączenia][HCVSConnectionString]
   
    Tworząc hello parametry połączenia, należy uwzględnić następujące hello:
   
   * Jeśli łączysz tooa nazwanego wystąpienia, a nie wystąpienia domyślnego (na przykład YourServer\SQLEXPRESS), należy skonfigurować porty statycznych toouse programu SQL Server. Informacje dotyczące konfigurowania portów statycznych, zobacz [jak tooconfigure toolisten programu SQL Server na określonym porcie](http://support.microsoft.com/kb/823938). Domyślnie nazwane wystąpienia używają protokołów UDP i porty dynamiczne, które nie są obsługiwane przez połączeń hybrydowych było możliwe.
   * Zaleca się, że podajesz hello portu (1433 domyślnie, jak pokazano w przykładzie hello) na powitania parametry połączenia, dzięki czemu można mieć pewność, że lokalny serwer SQL został włączony protokół TCP i korzysta z poprawnego portu hello.
   * Należy pamiętać, tooconnect uwierzytelniania programu SQL Server toouse, określając hello identyfikator użytkownika i hasło w ciągu połączenia.
3. Kliknij przycisk **zapisać** w pliku Web.config hello toosave programu Visual Studio.

### <a name="run-hello-project-locally-and-register-a-new-user"></a>Uruchom projekt hello lokalnie i zarejestrować nowego użytkownika
1. Teraz Uruchom nowego projektu sieci web lokalnie przez kliknięcie przycisku Przeglądaj hello w obszarze debugowania. W tym przykładzie użyto programu Internet Explorer.
   
    ![Uruchom projekt][HCVSRunProject]
2. Na powitania prawym górnym rogu hello domyślnej strony sieci web, wybierz **zarejestrować** tooregister nowe konto:
   
    ![Zarejestruj nowe konto][HCVSRegisterLocally]
3. Wprowadź nazwę użytkownika i hasło:
   
    ![Wprowadź nazwę użytkownika i hasło][HCVSCreateNewAccount]
   
    Powoduje to automatyczne utworzenie bazy danych na serwerze SQL lokalne powitania informacje członkostwa aplikacji. Jedną z tabel hello (**dbo. AspNetUsers**) poświadczenia użytkownika aplikacji, takich jak te, które zostały wprowadzone hello sieci web blokad. Później w samouczku hello, pojawi się w tej tabeli.
4. Zamknij okno przeglądarki hello hello domyślnej strony sieci web. Powoduje to zatrzymanie aplikacji hello w programie Visual Studio.

Są teraz gotowe do następnego kroku hello, czyli tooAzure aplikacji hello toopublish i przetestować go.

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a>F. Publikowanie tooAzure aplikacji sieci web hello i przetestować go
Teraz, należy opublikować Twojej aplikacji tooyour aplikacji sieci web usługi aplikacji i przetestowanie toosee jak jest połączenie hybrydowe hello skonfigurowane wcześniej są używane tooconnect bazy danych toohello aplikacji sieci web na komputerze lokalnym.

### <a name="publish-hello-web-application"></a>Publikowanie aplikacji sieci web hello
1. Można pobrać profilu publikowania dla aplikacji sieci web usługi aplikacji w portalu Azure hello hello. Na powitania bloku aplikacji sieci web, kliknij przycisk **Get profilu publikowania**, a następnie zapisz hello pliku tooyour komputera.
   
    ![Pobieranie profilu publikowania][PortalDownloadPublishProfile]
   
    Zostanie następnie zaimportować ten plik do aplikacji sieci web programu Visual Studio.
2. W programie Visual Studio, kliknij prawym przyciskiem myszy nazwę projektu hello w Eksploratorze rozwiązań i wybierz **publikowania**.
   
    ![Wybierz publikowania][HCVSRightClickProjectSelectPublish]
3. W hello **publikowanie w sieci Web** okna dialogowego na powitania **profilu** , wybierz pozycję **importu**.
   
    ![Import][HCVSPublishWebDialogImport]
4. Przeglądaj tooyour pobrany profil publikowania, zaznacz go, a następnie kliknij **OK**.
   
    ![Przeglądaj tooprofile][HCVSBrowseToImportPubProfile]
5. Publikowanie informacji jest importowany i wyświetla na powitania **połączenia** kartę hello okna dialogowego.
   
    ![Kliknij przycisk Publikuj][HCVSClickPublish]
   
    Kliknij przycisk **Opublikuj**.
   
    Po ukończeniu publikowania przeglądarki będzie uruchomić i pokazać teraz znanych aplikacji ASP.NET--z tą różnicą, że jest teraz na żywo w hello chmury Azure!

Następnie użyjesz toosee aplikacji sieci web na żywo połączenie hybrydowe w akcji.

### <a name="test-hello-completed-web-application-on-azure"></a>Test hello ukończone aplikacji sieci web na platformie Azure
1. U góry powitania po prawej stronie sieci web na platformie Azure, wybierz **Zaloguj**.
   
    ![Dziennik testu w][HCTestLogIn]
2. Usługi aplikacji, których aplikacja sieci web jest teraz połączona bazy danych członkostwa aplikacji sieci web tooyour na komputerze lokalnym. tooverify, zaloguj się przy użyciu tych samych poświadczeń, które należy wprowadzić w lokalne powitania bazy danych wcześniej hello.
   
    ![Witaj pozdrowienia][HCTestHelloContoso]
3. toofurther przetestuj nowe połączenie hybrydowe, wylogować się z aplikacji sieci web platformy Azure i Zarejestruj się jako inny użytkownik. Podaj nową nazwę użytkownika i hasło, a następnie kliknij przycisk **zarejestrować**.
   
    ![Test zarejestrować innego użytkownika][HCTestRegisterRelecloud]
4. tooverify hello nowe poświadczenia użytkownika były przechowywane w lokalnej bazie danych za pośrednictwem połączenia hybrydowe, Otwórz program SQL Management Studio na komputerze lokalnym. W Eksploratorze obiektów rozwiń hello **MembershipDB** bazy danych, a następnie rozwiń **tabel**. Kliknij prawym przyciskiem myszy hello **dbo. AspNetUsers** członkostwa tabeli i wybierz polecenie **zaznacz 1000 pierwszych wierszy** tooview hello wyników.
   
    ![Wyświetl wyniki hello][HCTestSSMSTree]
5. Członkostwo w lokalnej tabeli teraz zawiera oba konta — Witaj, został utworzony lokalnie i hello został utworzony w hello chmury Azure. Witaj, został utworzony w chmurze hello został zapisany tooyour lokalną bazą danych za pomocą funkcji połączenie hybrydowe platformy Azure.
   
    ![Zarejestrowani użytkownicy w lokalnej bazie danych][HCTestShowMemberDb]

Możesz teraz utworzeniu i wdrożeniu aplikacji sieci web ASP.NET, która używa połączenie hybrydowe między aplikacji sieci web w hello chmury Azure i lokalną bazą danych programu SQL Server. Gratulacje!

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
