---
title: "aaaHow tooMigrate i opublikuj tooan aplikacji sieci Web chmury Azure usługi w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomigrate i opublikować tooan aplikacji sieci web usługi w chmurze Azure za pomocą programu Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: a2832c37d2ebdbc1e69a307d16b65b1c87e9070c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-migrate-and-publish-a-web-application-tooan-azure-cloud-service-from-visual-studio"></a>Porady: migracja i publikowanie aplikacji sieci Web tooan usługi w chmurze Azure w programie Visual Studio
Zaletą tootake hello hostingu usług i skalowalność Azure, może być toomigrate i publikowanie usługi w chmurze Azure tooan aplikacji sieci web. Przy minimalnych zmianach tooyour istniejącą aplikację można uruchomić aplikacji sieci web na platformie Azure.

> [!NOTE]
> Ten temat dotyczy wdrażania usług toocloud, nie tooweb witryny. Informacje o wdrażaniu witryny tooweb, zobacz [wdrażanie aplikacji sieci web w usłudze Azure App Service](app-service-web/web-sites-deploy.md).
>
>

Lista określonych szablonów, które są obsługiwane zarówno dla programu Visual C# i Visual Basic, zobacz sekcję hello **obsługiwane szablony projektów** dalszej części tego tematu.

Należy najpierw włączyć aplikacji sieci web dla platformy Azure w programie Visual Studio. Hello następującej ilustracji przedstawiono toopublish klucza kroki hello istniejącej aplikacji sieci web przez dodanie toouse projektu platformy Azure dla wdrożenia. Ten proces powoduje dodanie projektu z rozwiązania tooyour roli hello wymagane w sieci web platformy Azure. Zaktualizowane zgodnie z hello typie projektu sieci web, czy masz, właściwości projektu hello zestawy są także jeśli pakiet usługi hello wymaga następującej liczby dodatkowych zestawów do wdrożenia.

![Publikowanie tooMicrosoft aplikacji sieci Web Azure](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC748917.png)

> [!NOTE]
> Witaj **przekonwertować**, **przekonwertować tooAzure projekt usługi w chmurze** polecenia są wyświetlane tylko dla projektu sieci web hello w rozwiązaniu. Na przykład polecenie hello nie jest dostępna dla projektu Silverlight w rozwiązaniu.
> Podczas tworzenia pakietu usług lub opublikować tooAzure Twojej aplikacji, ostrzeżeń lub błędów mogą wystąpić. Te ostrzeżenia i błędy może pomóc rozwiązać problemy przed wdrożeniem tooAzure. Na przykład może pojawić się ostrzeżenie o brakować zestawu. Aby uzyskać więcej informacji na temat tootreat wszystkie ostrzeżenia jako błędy, zobacz temat [skonfigurować projekt usługi w chmurze Azure z programem Visual Studio](vs-azure-tools-configuring-an-azure-project.md). Jeśli skompilować aplikację, uruchom lokalnie przy użyciu emulatora obliczeń hello lub opublikować go tooAzure mogą pojawić następujący błąd w hello hello **listy błędów** okna: **hello określona ścieżka, nazwa pliku lub obie jest zbyt długa** . Ten błąd występuje, ponieważ hello hello nazwy FQDN projektu platformy Azure jest za długa. Hello nazwy projektu hello, wraz z pełną ścieżką hello, nie może być więcej niż 146 znaków. Na przykład jest hello projektu Pełna nazwa tym ścieżki plików dla projektu platformy Azure, który jest tworzony dla aplikacji Silverlight: `c:\users\<user name>\documents\visual studio 2015\Projects\SilverlightApplication4\SilverlightApplication4.Web.Azure.ccproj`. Konieczne może być toomove katalogu różnych tooa rozwiązania o krótszej ścieżce tooreduce hello długości hello projektu w pełni kwalifikowanej nazwy.
>
>

toomigrate i opublikować tooAzure aplikacji sieci web, z programu Visual Studio, wykonaj następujące kroki.

## <a name="enable-a-web-application-for-deployment-tooazure"></a>Włączanie aplikacji sieci Web dla tooAzure wdrożenia
### <a name="tooenable-a-web-application-for-deployment-tooazure"></a>tooenable aplikacji sieci web dla tooAzure wdrożenia
1. tooenable aplikacji sieci web dla wdrożenia tooAzure, hello Otwórz menu skrótów dla sieci web projektu w rozwiązaniu i wybierz polecenie Dodaj projektu wdrożenia platformy Azure.

    wykonywane Hello następujące akcje:

   * Projekt platformy Azure o nazwie `<name of hello web project>.Azure` zostanie dodany toohello rozwiązanie dla aplikacji.
   * Rolę sieci web dla projektu sieci web hello jest dodawana toothis projektu platformy Azure.
   * Witaj **Kopiuj lokalnie** właściwość ma wartość tootrue dla dowolne zestawy, które są wymagane dla MVC 2, MVC 3, MVC 4 i aplikacji biznesowych Silverlight. Spowoduje to dodanie tych zestawów toohello usługi pakietu, który służy do wdrażania.

   > [!IMPORTANT]
   > Jeśli masz inne zestawy lub pliki, które są wymagane dla tej aplikacji sieci web, należy ręcznie ustawić właściwości hello tych plików. Aby uzyskać informacje o tooset te właściwości, zobacz temat hello sekcji **pliki dołączane w hello pakiet usługi** dalszej części tego artykułu.
   >
   > [!NOTE]
   > Jeśli rolę sieci web dla określonego projektu sieci web już istnieje w projekcie platformy Azure w rozwiązaniu hello **przekonwertować**, **przekonwertować projekt usługi w chmurze tooAzure** nie jest wyświetlany w menu skrótów powitania dla tego projektu sieci web .
   >
   >

   Jeśli wybrano wiele projektów sieci web w aplikacji sieci web i chcesz toocreate role sieci web dla każdego projektu sieci web, należy wykonać kroki hello w tej procedurze dla każdego projektu sieci web. Spowoduje to utworzenie oddzielnych projektów platformy Azure dla każdej roli sieci web. Każdy projekt sieci web mogą być publikowane oddzielnie. Alternatywnie można ręcznie dodać innego projektu roli sieć web tooan istniejących Azure w aplikacji sieci web. toodo tego hello Otwórz menu skrótów hello **ról** folderu w projekcie platformy Azure, wybierz **Dodaj**, następnie **projektu roli sieć Web w rozwiązaniu**, wybierz hello tooadd projektu jako sieci web Rola, a następnie wybierz pozycję hello **OK** przycisku.

## <a name="use-an-azure-sql-database-for-your-application"></a>Użyj bazy danych Azure SQL dla aplikacji
Jeśli parametry połączenia aplikacji sieci web, która używa bazy danych programu SQL Server, która znajduje się na lokalne powitania, należy zmienić ten toouse ciąg połączenia wystąpienie bazy danych SQL obsługującego Azure zamiast tego.

> [!IMPORTANT]
> Subskrypcję należy włączyć toouse bazy danych SQL. Jeśli dostęp do Twojej subskrypcji hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), można określić, jakie usługi oferuje subskrypcji. Witaj mają zastosowanie następujące instrukcje toohello wydane [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885). Jeśli używasz hello [portalu Azure](http://portal.microsoft.com), Pomiń toohello następnej procedury.
>
>

### <a name="toouse-a-sql-database-instance-in-your-web-role-for-your-connection-string"></a>toouse wystąpienie bazy danych SQL w roli sieci web dla parametrów połączenia
1. wystąpienie bazy danych SQL w hello toocreate [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), wykonaj kroki hello hello poniższego artykułu: [utworzyć serwer bazy danych SQL](http://go.microsoft.com/fwlink/?LinkId=225109).

   > [!NOTE]
   > Po skonfigurowaniu hello reguły zapory dla swojego wystąpienia bazy danych SQL, należy wybrać hello **Zezwól temu serwerowi tooaccess innych usług Azure** pole wyboru.
   >
   >
2. toocreate instancję toouse bazy danych SQL dla parametrów połączenia, wykonaj kroki hello w następnej sekcji hello poniższego artykułu hello: [Utwórz bazę danych SQL](http://go.microsoft.com/fwlink/?LinkId=225110).
3. toouse ADO.NET hello toocopy ciągu połączenia dla parametrów połączenia, wykonaj następujące kroki w hello hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885).  

   1. Wybierz hello **bazy danych** przycisk, a następnie otwórz hello węzła subskrypcji hello używane toocreate wystąpienia bazy danych SQL.
   2. toodisplay hello dostępnych wystąpień bazy danych SQL, wybierz hello **baz danych SQL** węzła.
   3. właściwości hello toodisplay hello bazy danych, wybierz hello bazy danych. Witaj **właściwości** zostanie wyświetlony widok.

      > [!NOTE]
      > Jeśli hello **właściwości** widoku nie jest wyświetlane, może być konieczne tooopen go za pomocą hello podziału.
      >
      >
   4. Parametry połączenia hello toodisplay, wybierz tooView dalej przycisk wielokropka (...) hello.

      Witaj **parametry połączenia** zostanie wyświetlone okno dialogowe.
   5. toocopy hello parametrów połączenia ADO.NET, zaznacz tekst hello, a następnie wybierz pozycję hello klawiszy Ctrl + C.
   6. tooclose hello w oknie dialogowym Wybierz hello **Zamknij** przycisku.
4. tooreplace hello połączenia ciąg w toouse pliku web.config hello tego wystąpienia bazy danych SQL, otwórz plik web.config hello, zaznacz hello istniejący wpis ciąg połączenia, a następnie wybierz klawiszy Ctrl + V hello. Witaj parametrów połączenia ADO.NET dla wystąpienia bazy danych SQL hello zastępuje hello istniejących parametrów połączenia.
5. Należy również dodać parametr hello `MultipleActiveResultSets=True` toohello parametry połączenia. Parametry połączenia Hello powinny mieć hello następującego formatu:

    ```
    connectionString=”Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"
    ```
6. (Opcjonalnie) Ciąg połączenia alternatywną metodą toochanging hello bezpośrednio w pliku web.config hello jest tooadd sekcji do jednego z plików transformacji pliku web.config hello, w zależności od konfiguracji kompilacji hello Użyj toocreate pakietu usług. Otwórz plik Web.Debug.Config hello lub hello Web.Release.Config pliku. Dodaj powitania po sekcji do tego pliku:

    ```
    XMLCopy<connectionStrings><addname="DefaultConnection"connectionString="Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"xdt:Transform="SetAttributes"xdt:Locator="Match(name)"/></connectionStrings>
    ```
7. Zapisz plik hello, które zostały zmodyfikowane i ponownie opublikować aplikację.

### <a name="toouse-an-instance-of-sql-database-by-using-hello-azure-classic-portal"></a>toouse wystąpienie bazy danych SQL za pomocą hello klasycznego portalu Azure
1. W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), wybierz hello węzła bazy danych SQL.

   * Jeśli zostanie wyświetlony hello wystąpienie bazy danych SQL, które mają toouse, wybrać tooopen go.
   * Jeśli nie utworzono żadnych wystąpień, wybierz odpowiednie łącze hello, a następnie utwórz wystąpienie.
2. Po otwarciu lub Utwórz wystąpienie bazy danych, wybierz hello **parametry połączenia** łącza.
3. U dołu hello hello strony wybierz hello łącze tooconfigure w ustawieniach zapory i zaakceptuj wartości domyślne hello lub hello wartości, które należy skonfigurować.
4. Skopiuj parametry połączenia ADO.NET hello, wklej go do pliku web.config na powitania stary połączenia ciąg hello lokalną bazą danych i można się tooadd `MultipleActiveResultSets=True`.

## <a name="publish-a-web-application-tooazure"></a>Publikowanie tooAzure aplikacji sieci Web
### <a name="toopublish-a-web-application-tooazure"></a>toopublish tooAzure aplikacji sieci Web
1. Aplikacja hello tootest w środowisku projektowym lokalne powitania przy użyciu emulatora obliczeń platformy Azure hello, projekt dla roli sieci web hello hello Otwórz menu skrótów hello Azure i wybierz pozycję **Ustaw jako projekt startowy**. Następnie wybierz pozycję **debugowania**, **Rozpocznij debugowanie** (klawiatury: **F5**).

    Witaj **Start hello Azure debugowania środowiska** zostanie otwarte okno dialogowe i uruchamiania aplikacji hello w przeglądarce hello. Aby uzyskać szczegółowe informacje na temat sposobu toostart każdego typu aplikacji sieci web w hello emulator obliczeń, w tej sekcji tabela hello.
2. tooset hello usług dla twojej aplikacji toopublish tooAzure, muszą mieć konta Microsoft i subskrypcji platformy Azure. Użyj hello etapami powitania po tooset tematu z usług: [przygotowania toopublish albo wdrożyć aplikację Azure w programie Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md).
3. toopublish tooAzure aplikacji sieci web hello, otwórz menu skrótów hello hello projektu sieci web i wybierz polecenie **publikowania tooAzure**.

    Witaj **publikowanie aplikacji platformy Azure** zostanie otwarte okno dialogowe i Visual Studio rozpoczyna proces wdrażania hello. Aby uzyskać więcej informacji o sposobie toopublish hello aplikacji, zobacz sekcję hello **opublikować aplikację Azure w programie Visual Studio** w [publikowania usługi w chmurze przy użyciu narzędzia Azure hello](vs-azure-tools-publishing-a-cloud-service.md).

   > [!NOTE]
   > Można również opublikować aplikację sieci web hello z hello Azure projektu. toodo, otwórz menu skrótów hello hello Azure projektu i wybierz polecenie **publikowania**.
   >
   >
4. postęp hello toosee hello wdrożenia, możesz wyświetlić hello **dziennika aktywności platformy Azure** okna. Ten dziennik jest automatycznie wyświetlana podczas uruchamiania procesu wdrażania hello. Można rozwinąć hello pozycji w dzienniku aktywności hello tooshow szczegółowe informacje, jak pokazano w hello następującej ilustracji:

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)
5. Proces wdrażania hello toocancel (opcjonalnie), otwórz menu skrótów hello hello pozycji w dzienniku aktywności hello i wybierz polecenie **Anuluj i Usuń**. Powoduje to zatrzymanie procesu wdrażania hello i usuwa środowisko wdrażania hello z platformy Azure.

   > [!NOTE]
   > tooremove to środowisko wdrażania po nim została wdrożona, należy użyć hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
   >
   >
6. (Opcjonalnie) Po uruchomiona wystąpienia roli, Visual Studio zawiera automatycznie środowiska wdrażania hello hello **rozwiązań usługi obliczenia Azure** w węźle **Eksplorator chmury** lub **Eksploratora serwera**. W tym miejscu można wyświetlić stan hello hello wystąpień poszczególnych ról.

    Witaj poniższej ilustracji przedstawiono hello wystąpień roli w **Eksploratora serwera** gdy są one nadal w stanie inicjowanie hello:

    ![VST_DeployComputeNode](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744134.png)
7. tooaccess aplikacji po wdrożeniu, wybierz hello strzałkę dalej tooyour wdrożenia podczas stan **Ukończono** pojawia się w hello **dziennik aktywności platformy Azure**. Spowoduje to wyświetlenie hello adres URL aplikacji sieci web na platformie Azure. Zobacz hello w poniższej tabeli hello szczegółowe informacje na temat sposobu toostart określony typ aplikacji sieci web na platformie Azure.

    Hello w poniższej tabeli wymieniono hello szczegóły dotyczące sposobu toostart określonych aplikacji z platformy Azure lub toorun sieci web lub debugowanie aplikacji sieci web lokalnie przy użyciu hello obliczeniowe emulatora usługi Azure:

   | Typ aplikacji sieci Web | Witaj uruchomienia/debugowania lokalnie za pomocą emulatora obliczeniowe | działające na platformie Azure |
   | --- | --- | --- |
   | Aplikacja sieci Web ASP.NET |Na pasku menu hello, wybierz **debugowania**, **Rozpocznij debugowanie** (klawiatury: Wybierz hello **F5** klucza.). |Wybierz hello hyperlink adres URL wyświetlany w hello **wdrożenia** kartę hello **dziennik aktywności platformy Azure** strony początkowej hello tooload w przeglądarce hello. |
   | Aplikacja sieci Web platformy ASP.NET MVC 2 |Na pasku menu hello, wybierz **debugowania**, **Rozpocznij debugowanie** (klawiatury: Wybierz hello **F5** klucza.). |Wybierz hello hyperlink adres URL wyświetlany w hello **wdrożenia** kartę hello **dziennik aktywności platformy Azure** strony początkowej hello tooload w przeglądarce hello. |
   | Aplikacja sieci Web platformy ASP.NET MVC 3 |Na pasku menu hello, wybierz **debugowania**, **Rozpocznij debugowanie** (klawiatury: Wybierz hello **F5** klucza.). |Wybierz hello hyperlink adres URL wyświetlany w hello **wdrożenia** kartę hello **dziennik aktywności platformy Azure** strony początkowej hello tooload w przeglądarce hello. |
   | Aplikacja sieci Web platformy ASP.NET MVC 4 |Na pasku menu hello, wybierz **debugowania**, **Rozpocznij debugowanie** (klawiatury: Wybierz hello **F5** klucza.). |Wybierz hello hyperlink adres URL wyświetlany w hello **wdrożenia** kartę hello **dziennik aktywności platformy Azure** strony początkowej hello tooload w przeglądarce hello. |
   | ASP.NET pusta aplikacja sieci Web |Należy dodać stronę .aspx w aplikacji, która zostanie ustawiony jako stronę startową powitania dla projektu sieci web. Następnie na pasku menu hello, wybierz pozycję **debugowania**, **Rozpocznij debugowanie** (klawiatury: Wybierz hello **F5** klucza.). |Jeśli masz domyślną stronę .aspx w aplikacji, wybierz hello hyperlink adres URL wyświetlany w hello **wdrożenia** kartę hello **dziennik aktywności platformy Azure** i załadowaniu tę stronę w przeglądarce hello. Jeśli masz strony .aspx różnych należy toonavigate toothis określonej strony przy użyciu następującego formatu dla danego adresu url hello:`<url for deployment>/<name of page>.aspx` |
   | Aplikacji Silverlight |Na pasku menu hello, wybierz **debugowania**, **Rozpocznij debugowanie** (klawiatury: Wybierz hello **F5** klucza.). |Należy określona strona toohello toonavigate aplikacji przy użyciu następującego formatu dla danego adresu url hello:`<url for deployment>/<name of page>.aspx` |
   | Aplikacja biznesowa Silverlight |Na pasku menu hello, wybierz **debugowania**, **Rozpocznij debugowanie** (klawiatury: Wybierz hello **F5** klucza.). |Należy określona strona toohello toonavigate aplikacji przy użyciu następującego formatu dla danego adresu url hello:`<url for deployment>/<name of page>.aspx` |
   | Aplikacja nawigacji Silverlight |Na pasku menu hello, wybierz **debugowania**, **Rozpocznij debugowanie** (klawiatury: Wybierz hello **F5** klucza.). |Należy określona strona toohello toonavigate aplikacji przy użyciu następującego formatu dla danego adresu url hello:`<url for deployment>/<name of page>.aspx` |
   | Aplikacja usługi WCF |Pliku svc hello musi być ustawiona jako hello początkowy strony projektu usługi WCF. Następnie na pasku menu hello, wybierz pozycję **debugowania**, **Rozpocznij debugowanie** (klawiatury: Wybierz hello **F5** klucza.). |Należy pliku svc toohello toonavigate aplikacji przy użyciu następującego formatu dla danego adresu url hello:`<url for deployment>/<name of service file>.svc` |
   | Aplikacja usługi przepływu pracy WCF |Pliku svc hello musi być ustawiona jako hello początkowy strony projektu usługi WCF. Następnie na pasku menu hello, wybierz pozycję **debugowania**, **Rozpocznij debugowanie** (klawiatury: Wybierz hello **F5** klucza.). |Należy pliku svc toohello toonavigate aplikacji przy użyciu następującego formatu dla danego adresu url hello:`<url for deployment>/<name of service file>.svc` |
   | ASP.NET Dynamic jednostek |Na pasku menu hello, wybierz **debugowania**, **Rozpocznij debugowanie** (klawiatury: Wybierz hello **F5** klucza.). |Należy zaktualizować parametry połączenia hello (zobacz następną sekcję). Należy również toonavigate toohello określonej strony aplikacji przy użyciu następującego formatu dla danego adresu url hello:`<url for deployment>/<name of page>.aspx` |
   | TooSQL Linq danych dynamicznych platformy ASP.NET |Na pasku menu hello, wybierz **debugowania**, **Rozpocznij debugowanie** (klawiatury: Wybierz hello **F5** klucza.). |Należy wykonać kroki hello w tej procedurze: Użyj bazy danych SQL Azure dla aplikacji (zobacz wcześniejszą sekcję w tym temacie). Należy również toonavigate toohello określonej strony aplikacji przy użyciu następującego formatu dla danego adresu url hello:`<url for deployment>/<name of page>.aspx` |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>Zaktualizuj parametry połączenia dla jednostek ASP.NET Dynamic
### <a name="tooupdate-a-connection-string-for-aspnet-dynamic-entities"></a>tooUpdate ciąg połączenia dla jednostek dynamicznych platformy ASP.NET
1. toocreate bazy danych SQL Azure, która może służyć do aplikacji sieci web ASP.NET dynamiczne jednostek, wykonaj kroki hello w procedurze hello **użyć bazy danych SQL Azure dla aplikacji** wcześniej w tym temacie.
2. Dodawanie hello tabel i pól, które należy dla tej bazy danych z hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
3. Witaj parametry połączenia dla tego typu aplikacji ma hello zgodny z formatem w pliku web.config hello:  

    ```
    <addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

    Aktualizacja hello *connectionString* wartości z hello parametrów połączenia ADO.NET dla bazy danych SQL Azure w następujący sposób:

    ```
    XMLCopy<addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```
4. plik web.config hello toosave z wprowadzone toohello parametry połączenia, na pasku menu hello Wybierz zmiany hello **pliku**, **zapisać pliku web.config**.

## <a name="supported-project-templates"></a>Szablony projektów obsługiwanych
toopublish tooAzure aplikacji sieci web, aplikacji hello muszą używać jednej z hello szablony projektów C# lub Visual Basic, który znajduje się w poniższej tabeli hello.

| Grupa szablonu projektu | Szablon projektu |
| --- | --- |
| Sieć Web |Aplikacja sieci Web ASP.NET |
| Sieć Web |Aplikacja sieci Web platformy ASP.NET MVC 2 |
| Sieć Web |Aplikacja sieci Web platformy ASP.NET MVC 3 |
| Sieć Web |Aplikacja sieci Web platformy ASP.NET MVC 4 |
| Sieć Web |ASP.NET pusta aplikacja sieci Web |
| Sieć Web |Aplikacja pusty sieci Web platformy ASP.NET MVC 2 |
| Sieć Web |Aplikacja sieci Web ASP.NET Dynamic Data Entities |
| Sieć Web |TooSQL Linq danych dynamicznych ASP.NET aplikacji sieci Web |
| Silverlight |Aplikacji Silverlight |
| Silverlight |Aplikacja biznesowa Silverlight |
| Silverlight |Aplikacja nawigacji Silverlight |
| WCF |Aplikacja usługi WCF |
| WCF |Aplikacja usługi przepływu pracy WCF |
| Przepływ pracy |Aplikacja usługi przepływu pracy WCF |

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji dotyczących publikowania, zobacz [przygotowania tooPublish albo wdrożyć aplikację Azure w programie Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md). Sprawdź również [ustawienie zapasową o nazwie poświadczenia uwierzytelniania](vs-azure-tools-setting-up-named-authentication-credentials.md).
