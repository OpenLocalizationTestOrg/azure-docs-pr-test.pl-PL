---
title: "aaaCreate aplikacji sieci Web w usłudze Azure App Service przy użyciu hello Azure SDK dla języka Java"
description: "Dowiedz się, jak toocreate aplikacji sieci Web w usłudze Azure App Service, programowo przy użyciu hello Azure SDK dla języka Java."
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
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a>Tworzenie aplikacji sieci Web w usłudze Azure App Service przy użyciu hello Azure SDK dla języka Java
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a>Omówienie
W tym przewodniku przedstawiono sposób toocreate zestawu Azure SDK dla aplikacji Java, która tworzy aplikację sieci Web w [usłudze Azure App Service][Azure App Service], następnie wdrożyć tooit aplikacji. Składa się z dwóch części:

* Część 1 pokazuje, jak toobuild aplikacji Java tworzącą aplikacji sieci web.
* Część 2 przedstawiono sposób toocreate proste JSP "Hello World" aplikacji, a następnie użyj FTP klienta toodeploy kodu tooApp usługi.

## <a name="prerequisites"></a>Wymagania wstępne
### <a name="software-installations"></a>Instalacje oprogramowania
Hello AzureWebDemo kod aplikacji, w tym artykule został napisany za pomocą usługi Azure zestawu Java SDK 0.7.0, które można zainstalować przy użyciu hello [Instalatora platformy sieci Web] [ Web Platform Installer] (WebPI). Ponadto należy upewnić się, że najnowszej wersji hello toouse hello [zestawu narzędzi platformy Azure dla programu Eclipse][Azure Toolkit for Eclipse]. Po zainstalowaniu hello zestawu SDK, należy zaktualizować hello zależności w projekcie Eclipse, uruchamiając **zaktualizować indeksu** w **repozytoria Maven**, potem ponownie Dodaj hello najnowsza wersja każdego pakietu w hello  **Zależności** okna. Sprawdź hello wersji zainstalowanego oprogramowania w środowisku Eclipse, klikając **Pomoc > szczegółowe informacje dotyczące instalacji**; powinien mieć co najmniej hello następujące wersje:

* Pakiet dla biblioteki Microsoft Azure dla języka Java 0.7.0.20150309
* Środowisko Eclipse IDE for Java EE Developers 4.4.2.20150219

### <a name="create-and-configure-cloud-resources-in-azure"></a>Tworzenie i konfigurowanie zasobów w chmurze na platformie Azure
Przed rozpoczęciem tej procedury należy toohave aktywną subskrypcją platformy Azure i skonfigurować domyślne Active Directory (AD) na platformie Azure.

### <a name="create-an-active-directory-ad-in-azure"></a>Tworzenie usługi Active Directory (AD) na platformie Azure
W przypadku usługi Active Directory (AD) nie jest już ma w Twojej subskrypcji platformy Azure, zaloguj się do hello [klasycznego portalu Azure] [ Azure classic portal] z kontem Microsoft. Jeśli masz wiele subskrypcji, kliknij przycisk **subskrypcje** i wybierz hello domyślnym katalogiem dla subskrypcji hello ma toouse dla tego projektu. Następnie kliknij przycisk **Zastosuj** Widok subskrypcji toothat tooswitch.

1. Wybierz **usługi Active Directory** hello menu po lewej stronie. **Kliknij przycisk Nowy > katalogu > Utwórz niestandardowy**.
2. W **Dodaj katalog**, wybierz pozycję **Utwórz nowy katalog**.
3. W **nazwa**, wprowadź nazwę katalogu.
4. W **domeny**, wprowadź nazwę domeny. Jest to nazwy domeny podstawowe jest włączone domyślnie z katalogu; ma ona formularza hello `<domain_name>.onmicrosoft.com`. Można określić nazwę na podstawie nazwy katalogu hello lub innego własnej nazwy domeny. Później możesz dodać Twoja organizacja już korzysta z inną nazwą domeny.
5. W **kraj lub region**, wybierz ustawienia regionalne.

Aby uzyskać więcej informacji dotyczących usługi AD, zobacz [co to jest katalog usługi Azure AD][What is an Azure AD directory]?

### <a name="create-a-management-certificate-for-azure"></a>Utwórz certyfikat zarządzania platformy Azure
Hello Azure SDK dla języka Java używa zarządzania certyfikatami tooauthenticate z subskrypcji platformy Azure. Są to certyfikaty X.509 v3, że używasz tooauthenticate aplikacji klienckiej, która używa hello interfejs API zarządzania usługami tooact imieniu hello subskrypcji właściciela toomanage subskrypcji zasobów.

Kod Hello w tej procedurze używa tooauthenticate certyfikatu z podpisem własnym z platformy Azure. Dla tej procedury należy toocreate certyfikatu i przekaż go toohello [klasycznego portalu Azure] [ Azure classic portal] wcześniej. Obejmuje to hello następujące kroki:

* Generowanie pliku PFX reprezentujący Twój certyfikat klienta i zapisz ją lokalnie.
* Wygeneruj certyfikat zarządzania (plik CER) z pliku PFX hello.
* Przekaż tooyour pliku CER hello subskrypcji platformy Azure.
* Konwertowanie pliku PFX hello JKS, ponieważ Java używa tego tooauthenticate format za pomocą certyfikatów.
* Napisać kod uwierzytelniania aplikacji hello, która odwołuje się lokalnego pliku JKS toohello.

Po zakończeniu tej procedury hello CER certyfikatu będzie znajdować się w ramach subskrypcji platformy Azure i hello JKS certyfikatu będzie znajdować się na dysku lokalnym. Aby uzyskać więcej informacji o certyfikatach zarządzania, zobacz [tworzenie i przekazywanie certyfikatu zarządzania platformy Azure][Create and Upload a Management Certificate for Azure].

#### <a name="create-a-certificate"></a>Tworzenie certyfikatu
toocreate własny certyfikat z podpisem własnym, otwórz konsolę polecenia w systemie operacyjnym i uruchom następujące polecenia hello.

> **Uwaga:** hello komputera, na którym uruchomiono to polecenie musi mieć hello JDK zainstalowane. Ponadto hello ścieżki toohello keytool zależy od hello lokalizacji, w którym chcesz zainstalować hello JDK. Aby uzyskać więcej informacji, zobacz [klucza i certyfikat zarządzania narzędzia (Narzędzie klucza)] [ Key and Certificate Management Tool (keytool)] w hello dokumentów online dotyczących Java.
> 
> 

plik PFX hello toocreate:

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

plik .cer hello toocreate:

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

Gdzie:

* `<java-install-dir>`jest hello ścieżka toohello katalog, w którym zainstalowano Java.
* `<keystore-id>`Identyfikator wpisu magazynu kluczy hello jest (na przykład `AzureRemoteAccess`).
* `<cert-store-dir>`jest hello ścieżka toohello katalog, w którym mają certyfikaty toostore (na przykład `C:/Certificates`).
* `<cert-file-name>`jest nazwą hello hello pliku certyfikatu (na przykład `AzureWebDemoCert`).
* `<password>`to hasło hello wybrania certyfikatu hello tooprotect; musi być co najmniej 6 znaków. Hasło nie można wprowadzić, chociaż nie jest to zalecane.
* `<dname>`jest skojarzony z aliasem toobe nazwy wyróżniającej x 500 hello i jest używany jako Witaj wystawca i pola podmiot certyfikatu z podpisem własnym hello.

Aby uzyskać więcej informacji, zobacz [tworzenie i przekazywanie certyfikatu zarządzania platformy Azure][Create and Upload a Management Certificate for Azure].

#### <a name="upload-hello-certificate"></a>Przekaż certyfikat hello
tooupload tooAzure certyfikatu z podpisem własnym, przejdź toohello **ustawienia** strony w portalu klasycznym hello, a następnie kliknij przycisk hello **certyfikaty zarządzania** kartę. Kliknij przycisk **przekazać** u dołu hello hello strony i przejdź toohello lokalizację pliku CER hello został utworzony.

#### <a name="convert-hello-pfx-file-into-jks"></a>Konwertowanie pliku PFX hello JKS
Hello wiersza polecenia systemu Windows (uruchomionego jako administrator), dysk cd toohello katalog zawierający hello certyfikatów i uruchamiania hello następujące polecenie, gdzie `<java-install-dir>` jest katalogiem hello zainstalowane Java na komputerze:

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. Po wyświetleniu monitu wprowadź hasło magazynu kluczy docelowej hello; są to hasło hello hello JKS pliku.
2. Po wyświetleniu monitu wprowadź hasło keystore źródła hello; to hasło hello hello pliku PFX.

dwa hasła Hello nie mają toobe hello takie same. Hasło nie można wprowadzić, chociaż nie jest to zalecane.

## <a name="build-a-web-app-creation-application"></a>Tworzenie aplikacji do tworzenia aplikacji sieci Web
### <a name="create-hello-eclipse-workspace-and-maven-project"></a>Utwórz hello Eclipse obszaru roboczego i projekt Maven
W tej sekcji utworzysz obszaru roboczego i projekt Maven hello aplikacji sieci web aplikacji tworzenia o nazwie AzureWebDemo.

1. Utwórz nowy projekt Maven. Kliknij przycisk **Plik > Nowy > Projekt Maven**. W **nowy projekt Maven**, wybierz pozycję **Tworzenie prostego projektu** i **Użyj domyślnej lokalizacji obszaru roboczego**.
2. Na drugiej stronie powitania z **nowy projekt Maven**, określ następujące hello:
   
   * Identyfikator grupy:`com.<username>.azure.webdemo`
   * Identyfikator artefaktu: AzureWebDemo
   * Wersja: 0.0.1-SNAPSHOT
   * Pakowanie: jar
   * Nazwa: AzureWebDemo
     
     Kliknij przycisk **Zakończ**.
3. Otwórz plik pom.xml hello nowy projekt w Eksploratorze projektu. Wybierz hello **zależności** kartę. Jak jest to nowy projekt, wymieniono jeszcze żadnych pakietów.
4. Wyświetl Otwórz hello Maven repozytoriów. **Kliknij przycisk okna > Pokaż widok > Inne > Maven > repozytoria Maven** i kliknij przycisk **OK**. Witaj **repozytoria Maven** widok będzie wyświetlany u dołu hello hello IDE.
5. Otwórz **globalne repozytoria**, powitania kliknij prawym przyciskiem myszy **centralnej** repozytorium, a następnie wybierz **Rebuild Index**.
   
    ![][1]
   
    Ten krok może potrwać kilka minut w zależności od prędkości hello połączenia. Podczas odtwarza hello indeksu, powinny być widoczne hello pakietów Microsoft Azure w hello **centralnej** Maven repozytorium.
6. W **zależności**, kliknij przycisk **Dodaj**. W **wprowadź identyfikator grupy...**  wprowadź `azure-management`. Wybierz pakiety hello bmc i zarządzania aplikacjami sieci Web usługi aplikacji:
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > **Uwaga:** Jeśli aktualizujesz zależności powitania po wydaniu nowej wersji, należy toore — Dodaj wszystkie zależności hello na tej liście.
   > Po kliknięciu **Dodaj** i wybierz poszczególne zależności, prawdopodobnie z hello nowego numeru wersji w hello **zależności** listy.
   > 
   > 

Kliknij przycisk **OK**. Witaj pakietów platformy Azure, a następnie wyświetlane w hello **zależności** listy.

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a>Pisanie kodu języka Java tooCreate aplikacji sieci Web przy hello wywoływania zestawu Azure SDK
Następnie należy napisać kod hello, który wywołuje interfejsy API w hello Azure SDK dla języka Java toocreate hello aplikacji sieci web usługi aplikacji.

1. Tworzenie Java klasy toocontain hello główny wpis punktu kodu. W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **nowy > klasy**.
2. W **Nowa Klasa Java**, nazwa klasy hello `WebCreator` i sprawdź hello **publiczne statyczne void main** wyboru. Opcje Hello powinna wyglądać następująco:
   
    ![][2]
3. Kliknij przycisk **Zakończ**. Plik WebCreator.java Hello jest widoczny w Eksploratorze projektu.

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a>Wywoływanie tooCreate interfejsu API Azure hello aplikację usługi aplikacji sieci Web
#### <a name="add-necessary-imports"></a>Dodaj niezbędne importów
W WebCreator.java Dodaj powitania po importów; Importy te zawierają tooclasses dostępu w hello biblioteki zarządzania służący do konsumowania interfejsów API usługi Azure:

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


#### <a name="define-hello-main-entry-point-class"></a>Zdefiniuj hello główny wpis punktu klasy
Ponieważ hello hello aplikacji AzureWebDemo służy toocreate aplikację usługi sieci Web aplikacji, nazwy klasy głównym hello dla tej aplikacji `WebAppCreator`. Ta klasa udostępnia hello główny wpis punktu kod, który wywołuje aplikacji hello toocreate hello interfejs API zarządzania usługami Azure w sieci web.

Dodaj następujące definicje parametr przestrzeni sieci Web i aplikacji sieci web hello hello. Konieczne będzie tooprovide własnych informacji identyfikator i certyfikatu subskrypcji platformy Azure.

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

* `<subscription-id>`jest identyfikator subskrypcji platformy Azure hello, w której ma zostać toocreate hello zasobów.
* `<certificate-store-path>`jest hello ścieżkę i nazwę pliku toohello JKS plik w katalogu magazynu lokalnego certyfikatu. Na przykład `C:/Certificates/CertificateName.jks` dla systemu Linux i `C:\Certificates\CertificateName.jks` dla systemu Windows.
* `<certificate-password>`jest hello hasło podczas tworzenia certyfikatu JKS.
* `webAppName`może być dowolna nazwa, którą wybierzesz; Ta procedura używa nazwy hello `WebDemoWebApp`. Witaj Pełna nazwa domeny jest hello `webAppName` z hello `domainName` dołączone, w tym przypadku pełną domenę hello jest `webdemowebapp.azurewebsites.net`.
* `domainName`należy określić, jak pokazano powyżej.
* `webSpaceName`musi mieć jedną z wartości hello zdefiniowanych w hello [WebSpaceNames] [ WebSpaceNames] klasy.
* `appServicePlanName`należy określić, jak pokazano powyżej.

> **Uwaga:** zawsze uruchomić tę aplikację, konieczne wartość hello toochange `webAppName` i `appServicePlanName` (lub usunąć aplikacji sieci web hello na powitania Azure Portal) przed uruchomieniem aplikacji hello ponownie. W przeciwnym razie wykonanie zakończy się niepowodzeniem, ponieważ hello sam zasób już istnieje na platformie Azure.
> 
> 

#### <a name="define-hello-web-creation-method"></a>Zdefiniuj metodę tworzenia hello sieci web
Następnie określ aplikację sieci web hello toocreate metody. Ta metoda `createWebApp`, określa parametry hello hello aplikacji sieci web i hello przestrzeni sieci Web. Również tworzy i konfiguruje hello aplikacji usługi sieci Web aplikacji zarządzania klienta, który jest zdefiniowany przez hello [WebSiteManagementClient] [ WebSiteManagementClient] obiektu. Klient zarządzania Hello jest klucza toocreating aplikacji sieci Web. Zapewnia usługi sieci web RESTful, które pozwalają aplikacji sieci web (wykonywanie operacji, takich jak tworzenie, update i delete) toomanage aplikacji przez wywołanie interfejsu API zarządzania usługami hello.

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
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
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

Kod Hello dane wyjściowe obejmują hello stanu HTTP odpowiedzi hello oznaczający powodzenie lub niepowodzenie, a jeśli to się powiedzie, dane wyjściowe obejmują nazwę hello hello utworzono aplikację sieci web.

#### <a name="define-hello-main-method"></a>Zdefiniuj metodę main() hello
Podaj kod metody main() hello tej aplikacji sieci web wywołania createWebApp() toocreate hello.

Na koniec wywołania `createWebApp` z `main`:

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a>Uruchamianie aplikacji hello i sprawdź tworzenie aplikacji sieci web
tooverify działającą aplikację, kliknij przycisk **Uruchom > Uruchom**. Po zakończeniu działania aplikacji hello powinny być widoczne następujące dane wyjściowe w konsoli programu Eclipse hello hello:

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

Zaloguj się do klasycznego portalu Azure hello i kliknij przycisk **aplikacje sieci Web**. Hello nowej aplikacji sieci web powinna zostać wyświetlona na liście aplikacji sieci Web hello w ciągu kilku minut.

## <a name="deploying-an-application-toohello-web-app"></a>Wdrażanie aplikacji toohello aplikacji sieci Web
Po uruchomiono AzureWebDemo i utworzyć hello nowej aplikacji sieci web, zaloguj się do klasycznego portalu hello kliknij **aplikacje sieci Web**i wybierz **WebDemoWebApp** w hello **aplikacje sieci Web** listy. Na stronie pulpitu nawigacyjnego aplikacji sieci web powitania kliknij **Przeglądaj** (lub kliknij adres URL hello, `webdemowebapp.azurewebsites.net`) toonavigate tooit. Zostanie wyświetlona strona pusty symbol zastępczy, ponieważ żadna zawartość jeszcze został toohello opublikowanej aplikacji sieci web.

Następnie utworzysz aplikację "Hello World" i wdrożyć aplikację sieci web toohello.

### <a name="create-a-jsp-hello-world-application"></a>Utwórz aplikację JSP Hello World
#### <a name="create-hello-application"></a>Tworzenie aplikacji hello
W kolejności toodemonstrate jak toodeploy sieci web toohello aplikacji hello procedury przedstawiono toocreate prostą aplikację "Hello World" w języku Java i przekaż go toohello aplikację usługi sieci Web aplikacji utworzony w aplikacji.

1. Kliknij przycisk **Plik > Nowy > Projekt sieci Web dynamiczne**. Nadaj jej nazwę `JSPHello`. Nie trzeba toochange inne ustawienia, w tym oknie dialogowym. Kliknij przycisk **Zakończ**.
   
    ![][3]
2. W obszarze Eksplorator projektów rozwiń hello **JSPHello** projektu, kliknij prawym przyciskiem myszy **WebContent**, następnie kliknij przycisk **nowy > pliku JSP**. W oknie dialogowym Nowy plik JSP hello hello nowego pliku o nazwie `index.jsp`. Kliknij przycisk **Dalej**.
3. W hello **wybierz szablon JSP** zaznacz pozycję **New JSP File (html)** i kliknij przycisk **Zakończ**.
4. W index.jsp, Dodaj hello następującego kodu w hello `<head>` i `<body>` tagu sekcje:
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a>Uruchamianie aplikacji Hello World hello w localhost
Aby uruchomić tę aplikację, musisz tooconfigure kilka właściwości.

1. Kliknij prawym przyciskiem myszy hello **JSPHello** projekt i wybierz **właściwości**.
2. W hello **właściwości** okna dialogowego: Wybierz **ścieżka kompilacji języka Java**, wybierz pozycję hello **kolejność i eksportowanie** karcie wyboru **biblioteka systemu środowiska JRE**, następnie kliknij przycisk **Się** toomove on toohello u góry listy hello.
   
    ![][4]
3. Również w hello **właściwości** okna dialogowego: Wybierz **docelowe środowiska uruchomieniowe** i kliknij przycisk **nowy**.
4. W hello **nowe środowisko uruchomieniowe serwera** okno dialogowe, wybierz serwer, takich jak **Apache Tomcat v7.0** i kliknij przycisk **dalej**. W hello **serwera Tomcat** okno dialogowe, zestaw **nazwa** za`Apache Tomcat v7.0`i ustaw **katalog instalacyjny serwera Tomcat** toohello katalogu, w którym zainstalowano wersję hello Serwer Tomcat ma toouse.
   
    ![][5]
   
    Kliknij przycisk **Zakończ**.
5. Następnie wróć toohello **docelowe środowiska uruchomieniowe** strony hello **właściwości** okna dialogowego. Wybierz **Apache Tomcat v7.0**, następnie kliknij przycisk **OK**.
   
    ![][6]
6. W hello Eclipse **Uruchom** menu, kliknij przycisk **Uruchom**. W hello **Uruchom jako** okno dialogowe, wybierz opcję **Uruchom na serwerze**. W hello **Uruchom na serwerze** okno dialogowe, wybierz opcję **Tomcat v7.0 Server**:
   
    ![][7]
   
    Kliknij przycisk **Zakończ**.
7. Gdy hello jest uruchamiana aplikacja, powinny pojawić się hello **JSPHello** strony są wyświetlane w oknie localhost w środowisku Eclipse (`http://localhost:8080/JSPHello/`), wyświetlania hello następujący komunikat:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a>Eksportowanie aplikacji hello jako plik WAR
Pliki projektu sieci web hello należy wyeksportować w postaci pliku archiwum (plik WAR) sieci web, dzięki czemu można wdrożyć aplikację sieci web toohello. Witaj następujące pliki projektu sieci web znajdują się w folderze WebContent hello:

    META-INF
    WEB-INF
    index.jsp

1. Kliknij prawym przyciskiem myszy hello WebContent folder i wybierz **wyeksportować**.
2. W hello **eksportu wybierz** okna dialogowego, kliknij przycisk **sieci Web > WAR** pliku, a następnie kliknij przycisk **dalej**.
3. W hello **wyeksportować plik WAR** okno dialogowe, wybierz katalog src hello w bieżącym projekcie hello i zawierać nazwę pliku WAR hello na końcu hello hello. Na przykład:
   
    `<project-path>/JSPHello/src/JSPHello.war`

Aby uzyskać więcej informacji na temat wdrażania WAR plików, zobacz [dodać tooAzure aplikacji Java aplikacji usługi sieci Web aplikacji](web-sites-java-add-app.md).

### <a name="deploying-hello-hello-world-application-using-ftp"></a>Wdrażanie FTP przy użyciu aplikacji Hello World hello
Wybierz aplikację hello toopublish klienta FTP innych firm. W tej procedurze opisano dwie opcje: hello Kudu konsoli wbudowanych w środowisku Azure. i FileZilla, narzędzie popularnych o wygodny graficznego interfejsu użytkownika.

> **Uwaga:** hello Azure zestawu narzędzi Eclipse obsługuje konta toostorage wdrożenia i chmury usługi, ale nie obsługuje obecnie wdrożenia tooweb aplikacji. Można wdrożyć toostorage konta i w chmurze usługi przy użyciu projektu wdrożenia platformy Azure, zgodnie z opisem w [tworzenia aplikacji Hello World na platformie Azure w programie Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), ale nie tooweb aplikacji. Użyj innych metod, takich jak FTP lub GitHub tootransfer plików tooyour aplikacji sieci web.
> 
> **Uwaga:** nie zaleca się używania protokołu FTP w wierszu polecenia systemu Windows hello (hello narzędzia wiersza polecenia FTP.EXE dostarczanych z systemem Windows). Klienci FTP, używający active FTP, takich jak FTP.EXE, często nie toowork za pośrednictwem zapór. Active FTP określa wewnętrzny adres sieci LAN, serwer toowhich FTP prawdopodobnie nie powiedzie się tooconnect.
> 
> 

Aby uzyskać więcej informacji dotyczących wdrażania tooan aplikacji usługi sieci web app przy użyciu protokołu FTP Zobacz hello następujące tematy:

* [Wdrażanie przy użyciu narzędzia FTP](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a>Konfigurowanie poświadczeń wdrożenia
Upewnij się, że zostało uruchomione hello **AzureWebDemo** toocreate aplikacji w aplikacji sieci web. Przenieś pliki toothis lokalizacji.

1. Zaloguj się do klasycznego portalu hello i kliknij przycisk **aplikacje sieci Web**. Upewnij się, że **WebDemoWebApp** jest widoczna na liście hello aplikacji sieci web i upewnij się, że jest uruchomiona. Kliknij przycisk **WebDemoWebApp** tooopen jej **pulpitu nawigacyjnego** strony.
2. Na powitania **pulpitu nawigacyjnego** w obszarze **szybki przegląd**, kliknij przycisk **skonfigurować poświadczenia wdrażania** (Jeśli masz już poświadczenia wdrażania, odczytuje  **Resetowanie poświadczeń wdrażania**).
   
    Wdrożenie poświadczenia są skojarzone z kontem Microsoft. Należy toospecify nazwę użytkownika i hasło, których można używać toodeploy przy użyciu usługi Git i FTP. Można użyć tych aplikacji sieci web tooany toodeploy poświadczenia w ramach wszystkich subskrypcji platformy Azure skojarzonych z Twoim kontem Microsoft. Podaj w dialogowym hello i rekordów hello nazwy użytkownika i hasła usługi Git i FTP poświadczenia wdrożenia do użycia w przyszłości.

#### <a name="get-ftp-connection-information"></a>Uzyskiwanie informacji o połączeniu FTP
toouse FTP toodeploy aplikacji pliki toohello nowo utworzona aplikacja sieci web, należy tooobtain informacje o połączeniu. Istnieją dwa sposoby tooobtain informacje o połączeniu. Jednym ze sposobów jest toovisit hello aplikacji sieci web firmy **pulpitu nawigacyjnego** strony; hello inny sposób jest profil publikowania aplikacji toodownload hello sieci web. profil publikowania Hello jest plik XML, który zawiera informacje, takie jak hosta FTP poświadczenia nazwy i logowania dla aplikacji sieci web w usłudze Azure App Service. W ramach wszystkich subskrypcji skojarzonych z hello konto platformy Azure, nie tylko ten jeden, można użyć tej nazwy użytkownika i hasła toodeploy tooany aplikacji sieci web.

informacje o połączeniu tooobtain FTP w bloku aplikacja sieci web hello w hello [Azure Portal][Azure Portal]:

1. W obszarze **Essentials**, znaleźć i skopiować hello **nazwa hosta FTP**. To jest identyfikator URI podobne zbyt`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.
2. W obszarze **Essentials**, należy znaleźć i skopiować **nazwy użytkownika serwera FTP/wdrożenia**. Będzie to mieć formularza hello *webappname\deployment-username*, na przykład `WebDemoWebApp\deployer77`.

profil publikowania informacji o połączeniu FTP tooobtain z hello:

1. W bloku aplikacja sieci web powitania kliknij **profilu publikowania Get**. To spowoduje pobranie .publishsettings pliku tooyour dysk lokalny.
2. Otwórz plik .publishsettings hello w edytorze XML lub edytorze tekstów i Znajdź hello `<publishProfile>` zawierający element `publishMethod="FTP"`. Go powinna wyglądać hello następujące czynności:
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. Należy pamiętać, że hello aplikacji sieci web `publishProfile` ustawienia mapowania toohello FileZilla lokacji Menedżera ustawień w następujący sposób:

* `publishUrl`jest identyczny hello **nazwa hosta FTP**, hello wartość ustawiona w **hosta**.
* `publishMethod="FTP"`oznacza, że ustawisz **protokołu** za**FTP - File Transfer Protocol**, i **szyfrowania** za**za pomocą zwykłego FTP**.
* `userName`i `userPWD` są klucze hello rzeczywiste wartości nazwy użytkownika i hasła określonego podczas resetowania hello poświadczenia wdrożenia. `userName`jest identyczny hello **wdrożenia / FTP użytkownika**. Mapują zbyt**użytkownika** i **hasło** w FileZilla.
* `ftpPassiveMode="True"`oznacza to, że korzysta z tej witryny hello FTP pasywnym transferu FTP; Wybierz **pasywnym** na powitania **ustawienia transferu** kartę.

#### <a name="configure-hello-web-app-toohost-a-java-application"></a>Skonfiguruj hello toohost aplikacji sieci Web aplikacji Java
Przed opublikowaniem aplikacji hello należy toochange kilka ustawień konfiguracji, aby hello aplikacji sieci web mogą obsługiwać aplikacji Java.

1. W klasycznym portalu hello, przejdź do pozycji aplikacji sieci web toohello **pulpitu nawigacyjnego** i kliknij przycisk **Konfiguruj**. Na powitania **Konfiguruj** Określ hello następujące ustawienia.
2. W **wersję Java** hello domyślna to **poza**; wybierz wersję Java hello celów aplikacji, na przykład 1.7.0_51. Po wykonaniu tej czynności również upewnij się, że **kontener sieci Web** ustawiono tooa wersję serwera Tomcat.
3. W **dokumenty domyślne**, Dodaj index.jsp i przesunięty toohello u góry listy hello. (hello domyślnego pliku dla aplikacji sieci web jest hostingstart.html).
4. Kliknij pozycję **Zapisz**.

#### <a name="publish-your-application-using-kudu"></a>Publikowanie aplikacji przy użyciu Kudu
Jednym ze sposobów toopublish aplikacji hello jest hello toouse Kudu debug console wbudowanych w platformy Azure. Program kudu jest znany toobe stabilny i spójny z aplikacji sieci Web usługi aplikacji i serwer Tomcat. Dostęp hello konsoli dla aplikacji sieci web hello przechodząc tooa adres URL hello następującej postaci:

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. Do wykonania tej procedury hello Kudu konsoli znajduje się pod adresem hello następującego adresu URL; Przeglądaj toothis lokalizacji:
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. Wybierz z górnego menu hello **konsoli debugowania > CMD**.
3. W wierszu polecenia konsoli hello, przejdź zbyt`/site/wwwroot` (lub kliknij przycisk `site`, następnie `wwwroot` w widoku katalogu hello u góry strony hello hello):
   
    `cd /site/wwwroot`
4. Po określeniu **wersję Java**, serwer Tomcat należy utworzyć katalogu webapps. W wierszu polecenia konsoli hello Przejdź katalogu webapps toohello:
   
    `mkdir webapps`
   
    `cd webapps`
5. Przeciągnij JSPHello.war z `<project-path>/JSPHello/src/` i upuść go w widoku katalogu Kudu hello w `/site/wwwroot/webapps`. Nie przeciągnij go toohello obszaru "Przeciągnij tutaj tooupload i zip", ponieważ Tomcat będzie Rozpakuj go.
   
   ![][8]

W pierwszym JSPHello.war pojawia się w obszarze katalogu hello samodzielnie:

  ![][9]

W krótkim czasie (prawdopodobnie mniej niż 5 minut) serwer Tomcat będzie Rozpakuj plik WAR hello w rozpakowanym katalogu JSPHello. Kliknij przycisk toosee katalogu głównego hello czy index.jsp zostało rozpakowane i skopiować. Jeśli tak, przejdź wstecz toohello webapps katalogu toosee czy hello rozpakowane JSPHello katalog został utworzony. Jeśli te elementy nie jest widoczny, poczekaj i powtórz.

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a>Publikowanie aplikacji przy użyciu FileZilla (opcjonalnie)
Kolejnym narzędziem za pomocą aplikacji hello toopublish jest FileZilla, popularnych klient FTP innych firm z wygodny graficznego interfejsu użytkownika. Można pobrać i zainstalować FileZilla z [http://filezilla-project.org/](http://filezilla-project.org/) Jeśli użytkownik nie ma jeszcze go. Aby uzyskać więcej informacji na temat używania powitania klienta, zobacz hello [dokumentacji FileZilla](https://wiki.filezilla-project.org/Documentation) i ten wpis w blogu na [klienci FTP — część 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).

1. W FileZilla, kliknij przycisk **Plik > Menedżer lokacji**.
2. W hello **Menedżer lokacji** okna dialogowego, kliknij przycisk **nowej lokacji**. Nowa, pusta witryna FTP będą wyświetlane w **wybierz wpis** monitem tooprovide nazwę. Do wykonania tej procedury, nadaj mu nazwę `AzureWebDemo-FTP`.
   
    Na powitania **ogólne** karcie, określ hello następujące ustawienia:
   
   * **Host:** Enter hello **nazwa hosta FTP** skopiowany z hello pulpitu nawigacyjnego.
   * **Port:** (to pole pozostanie puste, to jest pasywny przeniesienia i powitania serwera określają hello portu toouse.)
   * **Protokół:** protokół transferu plików FTP
   * **Szyfrowanie:** za pomocą zwykłego FTP
   * **Typ logowania:** normalny
   * **Użytkownik:** hello Enter wdrożenia / FTP użytkownika, który został skopiowany z hello pulpitu nawigacyjnego. Jest to pełna username FTP hello, mającej formularza hello *webappname\username*.
   * **Hasło:** wprowadź hasło hello określony podczas ustawiania poświadczeń wdrożenia hello.
     
     Na powitania **ustawienia transferu** wybierz opcję **pasywnym**.
3. Kliknij przycisk **Połącz**. Jeśli powodzenia FileZilla na konsoli zostanie wyświetlony `Status: Connected` komunikat i problem `LIST` polecenia zawartość katalogu hello toolist.
4. W hello **lokalnego** panelu lokacji hello wybierz katalog źródłowy w plik JSPHello.war hello, który znajduje się; ścieżka hello będzie podobne toohello następujące:
   
    `<project-path>/JSPHello/src/`
5. W hello **zdalnego** panelu lokacji, hello wybierz folder docelowy. Zostanie wdrożona toohello pliku WAR hello `webapps` katalog główny aplikacji sieci web hello. Przejdź za`/site/wwwroot`, kliknij prawym przyciskiem myszy `wwwroot`i wybierz **Utwórz katalog**. Nazwa katalogu hello `webapps` , a następnie wprowadź tego katalogu.
6. Transfer JSPHello.war zbyt`/site/wwwroot/webapps`. Wybierz JSPHello.war hello **lokalnego** listy plików, kliknij prawym przyciskiem myszy na nim i wybierz **przekazać**. Powinny pojawić się ją na `/site/wwwroot/webapps`.
7. Po skopiowaniu katalogu webapps toohello JSPHello.war serwera Tomcat zostanie automatycznie Rozpakuj (Rozpakuj) hello plików w pliku WAR hello. Mimo że serwer Tomcat rozpoczyna się rozpakowanie niemal natychmiast, może trwać bardzo długo czas prawdopodobnie dla tooappear plików powitania klienta hello FTP.

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a>Uruchamianie aplikacji Hello World hello na powitania aplikacji sieci Web
1. Po przekazany plik WAR hello i zweryfikować, że serwer Tomcat utworzył rozpakowanego `JSPHello` katalogu, Przeglądaj zbyt`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello aplikacji.
   
   > **Uwaga:** kliknięcie **Przeglądaj** z hello klasyczny portal może spowodować, że hello domyślnej strony sieci Web, informujący o tym "tej aplikacji sieci web Java na podstawie został pomyślnie utworzony." W danych wyjściowych aplikacji hello tooview kolejności zamiast hello domyślnej strony sieci Web może być toorefresh hello strony sieci Web.
   > 
   > 
2. Po uruchomieniu aplikacji hello powinna zostać wyświetlona strona sieci web z hello następujące dane wyjściowe:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a>Oczyszczanie zasobów platformy Azure
Ta procedura powoduje utworzenie aplikacji sieci web usługi aplikacji. Opłaty będą naliczane dla zasobu hello tak długo, jak istnieje. Jeśli nie planujesz toocontinue przy użyciu hello aplikacji sieci web do testowania lub programowanie należy rozważyć zatrzymanie lub usunięcie go. Aplikacja sieci web, który został zatrzymany nadal spowoduje naliczenie opłaty mały, ale w dowolnym momencie można uruchomić go ponownie. Usunięcie aplikacji sieci web spowoduje usunięcie wszystkich danych, które zostały przekazane tooit.

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
