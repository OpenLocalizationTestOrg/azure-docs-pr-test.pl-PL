---
title: "Tworzenie aplikacji sieci Web w usłudze Azure App Service przy użyciu zestawu Azure SDK dla języka Java"
description: "Dowiedz się, jak utworzyć aplikację sieci Web w usłudze Azure App Service, programowo przy użyciu zestawu Azure SDK dla języka Java."
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 08bb53de8cf437a5a2b1c3b38bce9f81b8349493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-the-azure-sdk-for-java"></a>Tworzenie aplikacji sieci Web w usłudze Azure App Service przy użyciu zestawu Azure SDK dla języka Java
<!-- Azure Active Directory workflow is not yet available on the Azure Portal -->

## <a name="overview"></a>Omówienie
W tym przewodniku przedstawiono sposób tworzenia zestawu Azure SDK dla aplikacji Java, która tworzy aplikację sieci Web w [usłudze Azure App Service][Azure App Service], następnie wdrożyć aplikację do niego. Składa się z dwóch części:

* Część 1 demonstruje sposób tworzenia aplikacji Java, która tworzy aplikację sieci web.
* Część 2 przedstawia sposób tworzenia prostego JSP "Hello World" aplikacji, a następnie użyj FTP klienta można wdrożyć kod w usłudze App Service.

## <a name="prerequisites"></a>Wymagania wstępne
### <a name="software-installations"></a>Instalacje oprogramowania
AzureWebDemo kod aplikacji w tym artykule został napisany za pomocą usługi Azure zestawu Java SDK 0.7.0, które można zainstalować przy użyciu [Instalatora platformy sieci Web] [ Web Platform Installer] (WebPI). Ponadto upewnij się używać najnowszej wersji [zestawu narzędzi platformy Azure dla programu Eclipse][Azure Toolkit for Eclipse]. Po zainstalowaniu zestawu SDK, należy zaktualizować zależności w projekcie Eclipse, uruchamiając **zaktualizować indeksu** w **repozytoria Maven**, potem ponownie Dodaj najnowsza wersja każdego pakietu w  **Zależności** okna. Można sprawdzić wersji zainstalowanego oprogramowania w środowisku Eclipse, klikając **Pomoc > szczegółowe informacje dotyczące instalacji**; wymaga co najmniej następujące wersje:

* Pakiet dla biblioteki Microsoft Azure dla języka Java 0.7.0.20150309
* Środowisko Eclipse IDE for Java EE Developers 4.4.2.20150219

### <a name="create-and-configure-cloud-resources-in-azure"></a>Tworzenie i konfigurowanie zasobów w chmurze na platformie Azure
Przed rozpoczęciem tej procedury, musisz mieć subskrypcję usługi Azure active i ustawić domyślne Active Directory (AD) na platformie Azure.

### <a name="create-an-active-directory-ad-in-azure"></a>Tworzenie usługi Active Directory (AD) na platformie Azure
W przypadku usługi Active Directory (AD) nie jest już ma w Twojej subskrypcji platformy Azure, zaloguj się do [klasycznego portalu Azure] [ Azure classic portal] z kontem Microsoft. Jeśli masz wiele subskrypcji, kliknij przycisk **subskrypcje** i wybierz domyślny katalog dla subskrypcji, którego chcesz użyć dla tego projektu. Następnie kliknij przycisk **Zastosuj** Aby przełączyć się do tego widoku subskrypcji.

1. Wybierz **usługi Active Directory** z menu po lewej stronie. **Kliknij przycisk Nowy > katalogu > Utwórz niestandardowy**.
2. W **Dodaj katalog**, wybierz pozycję **Utwórz nowy katalog**.
3. W **nazwa**, wprowadź nazwę katalogu.
4. W **domeny**, wprowadź nazwę domeny. Jest to nazwy domeny podstawowe jest włączone domyślnie z katalogu; ma on postać `<domain_name>.onmicrosoft.com`. Można określić nazwę na podstawie nazwy katalogu lub innego własnej nazwy domeny. Później możesz dodać Twoja organizacja już korzysta z inną nazwą domeny.
5. W **kraj lub region**, wybierz ustawienia regionalne.

Aby uzyskać więcej informacji dotyczących usługi AD, zobacz [co to jest katalog usługi Azure AD][What is an Azure AD directory]?

### <a name="create-a-management-certificate-for-azure"></a>Utwórz certyfikat zarządzania platformy Azure
Zestaw Azure SDK for Java korzysta z certyfikatów zarządzania do uwierzytelniania za pomocą subskrypcji platformy Azure. Są to certyfikaty X.509 v3, który używany do uwierzytelniania aplikacji klienckiej, która wykorzystuje interfejs API zarządzania usługami działać w imieniu właściciela subskrypcji do zarządzania zasobami subskrypcji.

Kod w tej procedurze używa certyfikatu z podpisem własnym do uwierzytelniania w usłudze Azure. Do wykonania tej procedury, należy utworzyć certyfikat i przekaż go do [klasycznego portalu Azure] [ Azure classic portal] wcześniej. Obejmuje to następujące czynności:

* Generowanie pliku PFX reprezentujący Twój certyfikat klienta i zapisz ją lokalnie.
* Wygeneruj certyfikat zarządzania (plik CER) z pliku PFX.
* Przekaż plik CER do subskrypcji platformy Azure.
* Konwertowanie pliku PFX JKS, ponieważ Java użyje tego formatu do uwierzytelniania za pomocą certyfikatów.
* Napisać kod uwierzytelniania aplikacji, która odwołuje się do pliku lokalnego JKS.

Po zakończeniu tej procedury, certyfikat CER będą znajdować się w Twojej subskrypcji platformy Azure i certyfikat JKS będą znajdować się na lokalnym dysku. Aby uzyskać więcej informacji o certyfikatach zarządzania, zobacz [tworzenie i przekazywanie certyfikatu zarządzania platformy Azure][Create and Upload a Management Certificate for Azure].

#### <a name="create-a-certificate"></a>Tworzenie certyfikatu
Aby utworzyć własny certyfikat z podpisem własnym, otwórz konsolę polecenia w systemie operacyjnym i uruchom następujące polecenia.

> **Uwaga:** komputera, na którym uruchomiono polecenie muszą mieć zainstalowany zestaw JDK. Ponadto ścieżka do keytool zależy od lokalizacji, w którym chcesz zainstalować zestaw JDK. Aby uzyskać więcej informacji, zobacz [klucza i certyfikat zarządzania narzędzia (Narzędzie klucza)] [ Key and Certificate Management Tool (keytool)] w dokumentów online Java.
> 
> 

Aby utworzyć plik PFX:

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

Aby utworzyć plik .cer:

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

Gdzie:

* `<java-install-dir>`to ścieżka do katalogu, w którym zainstalowano Java.
* `<keystore-id>`jest to identyfikator wpisu magazynu kluczy (na przykład `AzureRemoteAccess`).
* `<cert-store-dir>`jest to ścieżka do katalogu, w którym mają być przechowywane certyfikaty (na przykład `C:/Certificates`).
* `<cert-file-name>`to nazwa pliku certyfikatu (na przykład `AzureWebDemoCert`).
* `<password>`to hasło, które chcesz chronić certyfikat; musi być co najmniej 6 znaków. Hasło nie można wprowadzić, chociaż nie jest to zalecane.
* `<dname>`to nazwa wyróżniająca X.500 ma zostać skojarzony z aliasem i jest używany jako pola wystawcy i podmiotu certyfikatu z podpisem własnym.

Aby uzyskać więcej informacji, zobacz [tworzenie i przekazywanie certyfikatu zarządzania platformy Azure][Create and Upload a Management Certificate for Azure].

#### <a name="upload-the-certificate"></a>Przekaż certyfikat
Aby przekazać certyfikat z podpisem własnym na platformie Azure, przejdź do **ustawienia** w portalu klasycznym, a następnie kliknij przycisk **certyfikaty zarządzania** kartę. Kliknij przycisk **przekazać** w dolnej części strony i przejdź do lokalizacji pliku CER został utworzony.

#### <a name="convert-the-pfx-file-into-jks"></a>Konwertowanie pliku PFX JKS
W wierszu polecenia systemu Windows (uruchomionego jako administrator), dysk cd do katalogu zawierającego certyfikaty i uruchom następujące polecenie, gdzie `<java-install-dir>` jest katalogiem zainstalowane Java na komputerze:

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. Po wyświetleniu monitu wprowadź hasło magazynu kluczy docelowej. są to hasło dla pliku JKS.
2. Po wyświetleniu monitu wprowadź hasło źródła magazynu kluczy. jest to hasło określone dla pliku PFX.

Dwa hasła nie mają być takie same. Hasło nie można wprowadzić, chociaż nie jest to zalecane.

## <a name="build-a-web-app-creation-application"></a>Tworzenie aplikacji do tworzenia aplikacji sieci Web
### <a name="create-the-eclipse-workspace-and-maven-project"></a>Tworzenie obszaru roboczego Eclipse i projekt Maven
W tej sekcji utworzysz obszaru roboczego i projekt Maven aplikacji tworzenia aplikacji sieci web, o nazwie AzureWebDemo.

1. Utwórz nowy projekt Maven. Kliknij przycisk **Plik > Nowy > Projekt Maven**. W **nowy projekt Maven**, wybierz pozycję **Tworzenie prostego projektu** i **Użyj domyślnej lokalizacji obszaru roboczego**.
2. Na drugiej stronie **nowy projekt Maven**, podaj następujące informacje:
   
   * Identyfikator grupy:`com.<username>.azure.webdemo`
   * Identyfikator artefaktu: AzureWebDemo
   * Wersja: 0.0.1-SNAPSHOT
   * Pakowanie: jar
   * Nazwa: AzureWebDemo
     
     Kliknij przycisk **Zakończ**.
3. Otwórz plik pom.xml nowy projekt w Eksploratorze projektu. Wybierz **zależności** kartę. Jak jest to nowy projekt, wymieniono jeszcze żadnych pakietów.
4. Otwórz widok repozytoria Maven. **Kliknij przycisk okna > Pokaż widok > Inne > Maven > repozytoria Maven** i kliknij przycisk **OK**. **Repozytoria Maven** widoku będą wyświetlane w dolnej części IDE.
5. Otwórz **globalne repozytoria**, kliknij prawym przyciskiem myszy **centralnej** repozytorium, a następnie wybierz **Rebuild Index**.
   
    ![][1]
   
    Ten krok może potrwać kilka minut w zależności od prędkości połączenia. Jeśli spowoduje odbudowanie indeksu, powinny pojawić się pakietów Microsoft Azure w **centralnej** Maven repozytorium.
6. W **zależności**, kliknij przycisk **Dodaj**. W **wprowadź identyfikator grupy...**  wprowadź `azure-management`. Wybierz pakiety do zarządzania podstawowej i zarządzania aplikacjami sieci Web usługi aplikacji:
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > **Uwaga:** Jeśli aktualizujesz zależności po wydaniu nowej wersji, należy ponownie dodać wszystkich zależności na tej liście.
   > Po kliknięciu **Dodaj** i wybierz poszczególne zależności wydaje się przy użyciu nowego numeru wersji w **zależności** listy.
   > 
   > 

Kliknij przycisk **OK**. Następnie Azure pakiety są wyświetlane w **zależności** listy.

### <a name="writing-java-code-to-create-a-web-app-by-calling-the-azure-sdk"></a>Pisanie kodu języka Java do utworzenia aplikacji sieci Web przez wywołanie metody Azure SDK
Następnie należy napisać kod, który wywołuje interfejsy API w zestawie SDK Azure dla języka Java można utworzyć aplikacji sieci web usługi aplikacji.

1. Utwórz klasę języka Java, zawiera kod punktu wejścia głównego. W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy węzeł projektu i wybierz **nowy > klasy**.
2. W **Nowa Klasa Java**, nazwa klasy `WebCreator` i sprawdź **publiczne statyczne void main** wyboru. Wybór powinna wyglądać następująco:
   
    ![][2]
3. Kliknij przycisk **Zakończ**. Plik WebCreator.java pojawia się w obszarze Eksplorator projektów.

### <a name="calling-the-azure-api-to-create-an-app-service-web-app"></a>Wywołanie interfejsu API Azure do utworzenia aplikacji sieci Web usługi aplikacji
#### <a name="add-necessary-imports"></a>Dodaj niezbędne importów
W WebCreator.java Dodaj następujące instrukcje importu; Importy te zapewniają dostęp do klas w bibliotekach zarządzania służący do konsumowania interfejsów API usługi Azure:

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-the-main-entry-point-class"></a>W definicji klasy punktu wejścia głównego
Ponieważ aplikacja AzureWebDemo ma na celu utworzyć aplikację usługi aplikacji sieci Web, nazw klasy głównym dla tej aplikacji `WebAppCreator`. Ta klasa zawiera kod punktu wejścia głównego, który wywołuje interfejs API zarządzania usługami Azure do utworzenia aplikacji sieci web.

Dodaj następujące definicje parametr przestrzeni sieci Web i aplikacji sieci web. Należy podać informacje identyfikator i certyfikat własne subskrypcji platformy Azure.

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

Gdzie:

* `<subscription-id>`jest identyfikator subskrypcji platformy Azure, w którym chcesz utworzyć zasobu.
* `<certificate-store-path>`to ścieżka i nazwa pliku JKS w katalogu magazynu lokalnego certyfikatu. Na przykład `C:/Certificates/CertificateName.jks` dla systemu Linux i `C:\Certificates\CertificateName.jks` dla systemu Windows.
* `<certificate-password>`jest to hasło określone podczas tworzenia certyfikatu JKS.
* `webAppName`może być dowolna nazwa, którą wybierzesz; Ta procedura używa nazwy `WebDemoWebApp`. Pełna nazwa domeny jest `webAppName` z `domainName` dołączone, w tym przypadku pełną domenę jest `webdemowebapp.azurewebsites.net`.
* `domainName`należy określić, jak pokazano powyżej.
* `webSpaceName`musi mieć jedną z wartości zdefiniowanych w [WebSpaceNames] [ WebSpaceNames] klasy.
* `appServicePlanName`należy określić, jak pokazano powyżej.

> **Uwaga:** zawsze uruchomić tę aplikację, należy zmienić wartość `webAppName` i `appServicePlanName` (lub usunąć aplikacji sieci web w portalu Azure) przed uruchomieniem aplikacji ponownie. W przeciwnym razie wykonanie zakończy się niepowodzeniem, ponieważ istnieje już tego samego zasobu na platformie Azure.
> 
> 

#### <a name="define-the-web-creation-method"></a>Zdefiniuj metodę tworzenia sieci web
Następnie określ metodę, aby utworzyć aplikację sieci web. Ta metoda `createWebApp`, określa parametry przestrzeni sieci Web i aplikacji sieci web. Również tworzy i konfiguruje klienta zarządzania aplikacji usługi sieci Web aplikacji, który jest zdefiniowany przez [WebSiteManagementClient] [ WebSiteManagementClient] obiektu. Klient zarządzania jest kluczem do tworzenia aplikacji sieci Web. Zapewnia usługi sieci web RESTful, które umożliwiają aplikacji do zarządzania aplikacjami sieci web (wykonywanie operacji, takich jak tworzenie, update i delete) przez wywołanie interfejsu API zarządzania usługami.

    private static void createWebApp() throws Exception {

        // Specify configuration settings for the App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path to the JKS file
            keyStorePassword,  // Password for the JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create the App Service Web Apps management client to call Azure APIs
        // and pass it the App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for the web app with the specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that the server farm name takes the Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define the web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create the web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output the HTTP status code of the response; 200 indicates the request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output the name of the web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

Kod stanu HTTP odpowiedzi wskazujący powodzenie lub niepowodzenie dane wyjściowe obejmują i w razie powodzenia dane wyjściowe obejmują nazwę utworzonej aplikacji sieci web.

#### <a name="define-the-main-method"></a>Zdefiniuj metodę main()
Podaj kod metody main(), który wywołuje createWebApp() do utworzenia aplikacji sieci web.

Na koniec wywołania `createWebApp` z `main`:

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-the-application-and-verify-web-app-creation"></a>Uruchom aplikację i sprawdzić, tworzenie aplikacji sieci web
Aby sprawdzić, czy aplikacja działa, kliknij przycisk **Uruchom > Uruchom**. Po zakończeniu działania aplikacji powinny być widoczne następujące dane wyjściowe w konsoli programu Eclipse:

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

Zaloguj się do klasycznego portalu Azure i kliknij przycisk **aplikacje sieci Web**. W nowej aplikacji sieci web powinna zostać wyświetlona na liście aplikacji sieci Web w ciągu kilku minut.

## <a name="deploying-an-application-to-the-web-app"></a>Wdrażanie aplikacji w aplikacji sieci Web
Po uruchomiono AzureWebDemo i utworzyć nową aplikację sieci web, zaloguj się do klasycznego portalu kliknij **aplikacje sieci Web**i wybierz **WebDemoWebApp** w **aplikacje sieci Web** listy. Na stronie pulpitu nawigacyjnego aplikacji sieci web, kliknij przycisk **Przeglądaj** (lub kliknij adres URL, `webdemowebapp.azurewebsites.net`) można przejść do niego. Zostanie wyświetlona strona pusty symbol zastępczy, ponieważ żadna zawartość została opublikowana do aplikacji sieci web jeszcze.

Następnie utworzysz aplikację "Hello World" i wdrażanie dla aplikacji sieci web.

### <a name="create-a-jsp-hello-world-application"></a>Utwórz aplikację JSP Hello World
#### <a name="create-the-application"></a>Tworzenie aplikacji
W celu zaprezentowania sposobu wdrażania aplikacji w sieci Web, Poniższa procedura pokazuje sposób tworzenia prostej aplikacji Java "Hello World" i przekaż go do aplikacji sieci Web usługi aplikacji utworzony w aplikacji.

1. Kliknij przycisk **Plik > Nowy > Projekt sieci Web dynamiczne**. Nadaj jej nazwę `JSPHello`. Nie trzeba zmienić ustawienia w tym oknie dialogowym. Kliknij przycisk **Zakończ**.
   
    ![][3]
2. W obszarze Eksplorator projektów rozwiń **JSPHello** projektu, kliknij prawym przyciskiem myszy **WebContent**, następnie kliknij przycisk **nowy > pliku JSP**. W oknie dialogowym Nowy plik JSP nazwę nowego pliku `index.jsp`. Kliknij przycisk **Dalej**.
3. W **wybierz szablon JSP** zaznacz pozycję **New JSP File (html)** i kliknij przycisk **Zakończ**.
4. W index.jsp, Dodaj następujący kod w `<head>` i `<body>` tagu sekcje:
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, the time is <%= date %> 
        </body>

#### <a name="run-the-hello-world-application-in-localhost"></a>Uruchamianie aplikacji Hello World w localhost
Przed uruchomieniem tej aplikacji, musisz skonfigurować kilka właściwości.

1. Kliknij prawym przyciskiem myszy **JSPHello** projekt i wybierz **właściwości**.
2. W **właściwości** okna dialogowego: Wybierz **ścieżka kompilacji języka Java**, wybierz pozycję **kolejność i eksportowanie** karcie wyboru **biblioteka systemu środowiska JRE**, następnie kliknij przycisk **Się** Aby przenieść go na początku listy.
   
    ![][4]
3. Również w **właściwości** okna dialogowego: Wybierz **docelowe środowiska uruchomieniowe** i kliknij przycisk **nowy**.
4. W **nowe środowisko uruchomieniowe serwera** okno dialogowe, wybierz serwer, takich jak **Apache Tomcat v7.0** i kliknij przycisk **dalej**. W **serwera Tomcat** okno dialogowe, zestaw **nazwa** do `Apache Tomcat v7.0`i ustaw **katalog instalacyjny serwera Tomcat** do katalogu, w którym zainstalowano wersję serwera Tomcat serwer, którego chcesz użyć.
   
    ![][5]
   
    Kliknij przycisk **Zakończ**.
5. Następnie wróć do **docelowe środowiska uruchomieniowe** strony **właściwości** okna dialogowego. Wybierz **Apache Tomcat v7.0**, następnie kliknij przycisk **OK**.
   
    ![][6]
6. W środowisku Eclipse **Uruchom** menu, kliknij przycisk **Uruchom**. W **Uruchom jako** okno dialogowe, wybierz opcję **Uruchom na serwerze**. W **Uruchom na serwerze** okno dialogowe, wybierz opcję **Tomcat v7.0 Server**:
   
    ![][7]
   
    Kliknij przycisk **Zakończ**.
7. Gdy aplikacja zostanie uruchomiona, powinny pojawić się **JSPHello** strony są wyświetlane w oknie localhost w środowisku Eclipse (`http://localhost:8080/JSPHello/`), wyświetlanie następujący komunikat:
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-the-application-as-a-war"></a>Wyeksportować aplikację jako plik WAR
Wyeksportuj pliki projektu sieci web jako plik archiwum (plik WAR) w sieci web tak, aby umożliwić jej wdrażanie aplikacji sieci web. Następujące pliki projektu sieci web znajdują się w folderze WebContent:

    META-INF
    WEB-INF
    index.jsp

1. Kliknij prawym przyciskiem myszy WebContent folder i wybierz **wyeksportować**.
2. W **eksportu wybierz** okna dialogowego, kliknij przycisk **sieci Web > WAR** pliku, a następnie kliknij przycisk **dalej**.
3. W **wyeksportować plik WAR** okno dialogowe, wybierz katalog src w bieżącym projekcie i zawierać nazwę pliku WAR na końcu. Na przykład:
   
    `<project-path>/JSPHello/src/JSPHello.war`

Aby uzyskać więcej informacji na temat wdrażania WAR plików, zobacz [dodawania aplikacji Java do aplikacji sieci Web usługi aplikacji Azure](web-sites-java-add-app.md).

### <a name="deploying-the-hello-world-application-using-ftp"></a>Wdrażanie aplikacji World Hello za pomocą protokołu FTP
Wybierz klienta FTP innych firm, aby opublikować aplikację. W tej procedurze opisano dwie opcje: konsoli Kudu wbudowanych w środowisku Azure. i FileZilla, narzędzie popularnych o wygodny graficznego interfejsu użytkownika.

> **Uwaga:** zestawu narzędzi platformy Azure dla programu Eclipse obsługuje wdrażanie do kont magazynu i chmury usługi, ale nie obsługuje obecnie wdrożenia w aplikacji sieci web. Można wdrożyć do kont magazynu i usług przy użyciu projektu wdrożenia platformy Azure, zgodnie z opisem w chmurze [tworzenia aplikacji Hello World na platformie Azure w programie Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), ale nie do aplikacji sieci web. Użyj innych metod, takich jak FTP lub GitHub do transferu plików do aplikacji sieci web.
> 
> **Uwaga:** nie zaleca się używania protokołu FTP z wiersza polecenia systemu Windows (narzędzie wiersza polecenia FTP.EXE jest dostarczana z systemem Windows). Klienci FTP, którzy używają active FTP, takich jak FTP.EXE, często nie działać za pośrednictwem zapór. Aktywne FTP określa wewnętrzny adres sieci LAN, do którego serwer FTP prawdopodobnie nie będzie można połączyć.
> 
> 

Aby uzyskać więcej informacji na wdrożenia dla aplikacji sieci web usługi aplikacji za pomocą protokołu FTP zobacz następujące tematy:

* [Wdrażanie przy użyciu narzędzia FTP](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a>Konfigurowanie poświadczeń wdrożenia
Upewnij się, że została uruchomiona **AzureWebDemo** aplikacji w celu utworzenia aplikacji sieci web. Przenieś pliki do tej lokalizacji.

1. Zaloguj się do klasycznego portalu i kliknij przycisk **aplikacje sieci Web**. Upewnij się, że **WebDemoWebApp** pojawią się na liście aplikacji sieci web i upewnij się, że jest uruchomiona. Kliknij przycisk **WebDemoWebApp** aby otworzyć jego **pulpitu nawigacyjnego** strony.
2. Na **pulpitu nawigacyjnego** w obszarze **szybki przegląd**, kliknij przycisk **skonfigurować poświadczenia wdrażania** (Jeśli masz już poświadczenia wdrażania, odczytuje  **Resetowanie poświadczeń wdrażania**).
   
    Wdrożenie poświadczenia są skojarzone z kontem Microsoft. Należy określić nazwę użytkownika i hasło, które można wdrożyć przy użyciu usługi Git i FTP. Te poświadczenia można użyć do wdrożenia do wszystkich aplikacji sieci web w ramach wszystkich subskrypcji platformy Azure skojarzonych z Twoim kontem Microsoft. Podaj poświadczenia wdrożenia usługi Git i FTP, w oknie dialogowym i Zapisz nazwę użytkownika i hasło do użycia w przyszłości.

#### <a name="get-ftp-connection-information"></a>Uzyskiwanie informacji o połączeniu FTP
Aby użyć FTP do wdrażania plików aplikacji do nowo utworzonej aplikacji sieci web, należy uzyskać informacje o połączeniu. Istnieją dwie metody uzyskiwania informacji o połączeniu. Jednym ze sposobów jest odwiedzać aplikacji sieci web **pulpitu nawigacyjnego** strony; inny sposób jest do pobrania w sieci web w aplikacji profilu publikowania. Profil publikowania jest plik XML, który zawiera informacje, takie jak hosta FTP poświadczenia nazwy i logowania dla aplikacji sieci web w usłudze Azure App Service. Do wdrożenia do wszystkich aplikacji sieci web w ramach wszystkich subskrypcji skojarzonych z konta platformy Azure, a nie tylko ten jeden, można użyć tej nazwy użytkownika i hasła.

Aby uzyskać informacje o połączeniu FTP w bloku aplikacja sieci web w [Azure Portal][Azure Portal]:

1. W obszarze **Essentials**, należy znaleźć i skopiować **nazwa hosta FTP**. Jest to podobne do identyfikatora URI `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.
2. W obszarze **Essentials**, należy znaleźć i skopiować **nazwy użytkownika serwera FTP/wdrożenia**. Będzie to mieć postać *webappname\deployment-username*, na przykład `WebDemoWebApp\deployer77`.

Aby uzyskać informacje o połączeniu FTP z profil publikowania:

1. W bloku aplikacja sieci web kliknij **profilu publikowania Get**. Pobierze plik .publishsettings na dysk lokalny.
2. Otwórz plik .publishsettings w edytorze XML lub edytorze tekstów i Znajdź `<publishProfile>` zawierający element `publishMethod="FTP"`. Jego wygląd powinien być podobne do poniższych:
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. Należy pamiętać, że aplikacja sieci web `publishProfile` ustawienia mapy w celu ustawienia Menedżera lokacji FileZilla w następujący sposób:

* `publishUrl`jest taka sama jak **nazwa hosta FTP**, wartość ustawiona w **hosta**.
* `publishMethod="FTP"`oznacza, że ustawisz **protokołu** do **FTP - File Transfer Protocol**, i **szyfrowania** do **za pomocą zwykłego FTP**.
* `userName`i `userPWD` są klucze rzeczywistej nazwy użytkownika i określone podczas resetowania poświadczenia wdrażania wartości hasła. `userName`jest taka sama jak **wdrożenia / FTP użytkownika**. Są one wykonywane na **użytkownika** i **hasło** w FileZilla.
* `ftpPassiveMode="True"`oznacza, że witryna FTP używa pasywnym transferu FTP; Wybierz **pasywnym** na **ustawienia transferu** kartę.

#### <a name="configure-the-web-app-to-host-a-java-application"></a>Konfigurowanie aplikacji sieci Web na potrzeby hostowania aplikacji języka Java
Przed opublikowaniem aplikacji, musisz zmienić kilka ustawień konfiguracji, aby aplikacja sieci web mogą obsługiwać aplikacji Java.

1. W klasycznym portalu, przejdź do aplikacji sieci web **pulpitu nawigacyjnego** i kliknij przycisk **Konfiguruj**. Na **Konfiguruj** określ następujące ustawienia.
2. W **wersję Java** wartość domyślna to **poza**; wybierz wersję Java celów aplikacji, na przykład 1.7.0_51. Po wykonaniu tej czynności również upewnij się, że **kontener sieci Web** jest ustawiona na wersję serwera Tomcat.
3. W **dokumenty domyślne**, Dodaj index.jsp i przenieść ją do początku listy. (Domyślnego pliku dla aplikacji sieci web jest hostingstart.html).
4. Kliknij pozycję **Zapisz**.

#### <a name="publish-your-application-using-kudu"></a>Publikowanie aplikacji przy użyciu Kudu
Jest jednym ze sposobów publikowania aplikacji do użycia konsoli debugowania aparatu Kudu wbudowanych w platformy Azure. Program kudu jest znany jako stabilny i spójny z aplikacji sieci Web usługi aplikacji i serwer Tomcat. Aby dostęp do konsoli dla aplikacji sieci web przechodząc do adresu URL mają następującą postać:

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. Do wykonania tej procedury konsoli Kudu znajduje się pod adresem URL; Przejdź do tej lokalizacji:
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. Wybierz z górnego menu **konsoli debugowania > CMD**.
3. W wierszu polecenia konsoli przejdź do `/site/wwwroot` (lub kliknij przycisk `site`, następnie `wwwroot` w katalogu widoku w górnej części strony):
   
    `cd /site/wwwroot`
4. Po określeniu **wersję Java**, serwer Tomcat należy utworzyć katalogu webapps. W wierszu polecenia konsoli przejdź do katalogu webapps:
   
    `mkdir webapps`
   
    `cd webapps`
5. Przeciągnij JSPHello.war z `<project-path>/JSPHello/src/` i upuść go w widoku katalogu Kudu w `/site/wwwroot/webapps`. Nie przeciągnij go do obszaru "Przeciągnij tutaj, aby przekazać i zip", ponieważ Tomcat będzie Rozpakuj go.
   
   ![][8]

W pierwszym JSPHello.war pojawia się w obszarze Katalog samodzielnie:

  ![][9]

W krótkim czasie (prawdopodobnie mniej niż 5 minut) serwer Tomcat będzie Rozpakuj plik WAR do rozpakowanego katalogu JSPHello. Kliknij katalog główny, aby sprawdzić, czy index.jsp zostało rozpakowane i skopiować. Jeśli tak, przejdź do katalogu webapps, aby sprawdzić, czy rozpakowanego katalogu JSPHello została utworzona. Jeśli te elementy nie jest widoczny, poczekaj i powtórz.

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a>Publikowanie aplikacji przy użyciu FileZilla (opcjonalnie)
Innego narzędzia używanego do publikowania aplikacji jest FileZilla, popularnych klient FTP innych firm z wygodny graficznego interfejsu użytkownika. Można pobrać i zainstalować FileZilla z [http://filezilla-project.org/](http://filezilla-project.org/) Jeśli użytkownik nie ma jeszcze go. Aby uzyskać więcej informacji na temat używania klienta, zobacz [dokumentacji FileZilla](https://wiki.filezilla-project.org/Documentation) i ten wpis w blogu na [klienci FTP — część 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).

1. W FileZilla, kliknij przycisk **Plik > Menedżer lokacji**.
2. W **Menedżer lokacji** okna dialogowego, kliknij przycisk **nowej lokacji**. Nowa, pusta witryna FTP będą wyświetlane w **wybierz wpis** monitowania użytkownika o podanie nazwy. Do wykonania tej procedury, nadaj mu nazwę `AzureWebDemo-FTP`.
   
    Na **ogólne** karcie, określ następujące ustawienia:
   
   * **Host:** Enter **nazwa hosta FTP** skopiowany z poziomu pulpitu nawigacyjnego.
   * **Port:** (to pole pozostanie puste, jak to przeniesienie pasywny oraz określić port używany serwer.)
   * **Protokół:** protokół transferu plików FTP
   * **Szyfrowanie:** za pomocą zwykłego FTP
   * **Typ logowania:** normalny
   * **Użytkownik:** wprowadzić rozmieszczenia / FTP użytkownika, które zostały skopiowane z poziomu pulpitu nawigacyjnego. Jest to pełna username FTP, która ma postać *webappname\username*.
   * **Hasło:** wprowadź hasło określone podczas ustawiania poświadczeń wdrożenia.
     
     Na **ustawienia transferu** wybierz opcję **pasywnym**.
3. Kliknij przycisk **Połącz**. Jeśli powodzenia FileZilla na konsoli zostanie wyświetlony `Status: Connected` komunikat i problem `LIST` polecenie, aby wyświetlić listę zawartości katalogu.
4. W **lokalnego** lokacji panelu, wybierz katalog źródłowy, w którym znajduje się plik JSPHello.war; ścieżka będzie podobny do następującego:
   
    `<project-path>/JSPHello/src/`
5. W **zdalnego** lokacji panelu, wybierz folder docelowy. Zostanie wdrożona plik WAR do `webapps` katalog główny aplikacji sieci web. Przejdź do `/site/wwwroot`, kliknij prawym przyciskiem myszy `wwwroot`i wybierz **Utwórz katalog**. Nazwa katalogu `webapps` , a następnie wprowadź tego katalogu.
6. Transfer JSPHello.war do `/site/wwwroot/webapps`. Wybierz JSPHello.war w **lokalnego** listy plików, kliknij prawym przyciskiem myszy na nim i wybierz **przekazać**. Powinny pojawić się ją na `/site/wwwroot/webapps`.
7. Po skopiowaniu JSPHello.war do katalogu webapps serwera Tomcat zostanie automatycznie Rozpakuj (Rozpakuj) plików w pliku WAR. Mimo że serwer Tomcat rozpoczyna się rozpakowanie niemal natychmiast, może trwać bardzo długo czas (prawdopodobnie godz. dla plików, które mają być widoczne w klient FTP).

#### <a name="run-the-hello-world-application-on-the-web-app"></a>Uruchamianie aplikacji Hello World w aplikacji sieci Web
1. Po przekazany plik WAR i zweryfikować, że serwer Tomcat utworzył rozpakowanego `JSPHello` katalogu, przejdź do `http://webdemowebapp.azurewebsites.net/JSPHello` do uruchomienia aplikacji.
   
   > **Uwaga:** kliknięcie **Przeglądaj** z klasycznego portalu można uzyskać domyślnej strony sieci Web, informujący o tym "tej aplikacji sieci web Java na podstawie został pomyślnie utworzony." Może być konieczne odświeżania strony sieci Web, aby wyświetlić dane wyjściowe aplikacji zamiast domyślnej strony sieci Web.
   > 
   > 
2. Po uruchomieniu aplikacji, powinny być widoczne strony sieci web z następujących danych wyjściowych:
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a>Oczyszczanie zasobów platformy Azure
Ta procedura powoduje utworzenie aplikacji sieci web usługi aplikacji. Opłaty będą naliczane zasobu tak długo, jak istnieje. Jeśli nie chcesz nadal używać do testowania lub rozwoju aplikacji sieci web, należy rozważyć zatrzymanie lub usunięcie go. Aplikacja sieci web, który został zatrzymany nadal spowoduje naliczenie opłaty mały, ale w dowolnym momencie można uruchomić go ponownie. Usunięcie aplikacji sieci web spowoduje usunięcie wszystkich danych, które zostały przekazane do niej.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
