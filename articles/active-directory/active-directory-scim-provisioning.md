---
title: "aaaUsing systemu do zarządzania tożsamościami międzydomenowego automatycznej aprowizacji użytkowników i grup z usługi Azure Active Directory tooapplications | Dokumentacja firmy Microsoft"
description: "Usługa Azure Active Directory mogą automatycznie obsługiwać użytkowników i grup tooany aplikacji lub tożsamości sklepu, która jest fronted przez usługę sieci web z interfejsem hello zdefiniowane w hello Specyfikacja protokołu SCIM"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a>Zarządzanie tożsamościami międzydomenowego tooautomatically udostępniania użytkowników i grup z usługi Azure Active Directory tooapplications przy użyciu systemu

## <a name="overview"></a>Omówienie
Azure Active Directory (Azure AD), mogą automatycznie obsługiwać użytkowników i grup tooany aplikacji lub tożsamości sklepu, która jest fronted przez usługę sieci web z interfejsem hello zdefiniowane w hello [systemu do innej domeny zarządzania tożsamości (SCIM) 2.0 Specyfikacja protokołu](https://tools.ietf.org/html/draft-ietf-scim-api-19). Usługa Azure Active Directory można wysłać żądania toocreate, zmodyfikować lub usunąć przypisanych użytkowników i grup usługi toohello w sieci web. usługi sieci web Hello może dokonywać translacji te żądania na operacje na magazynu tożsamości hello docelowego. 

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. 



![][0]
*Rysunek 1: Inicjowanie obsługi administracyjnej z magazynu tożsamości tooan usługi Azure Active Directory za pośrednictwem usługi sieci web*

Ta możliwość może służyć w połączeniu z możliwością "bring własną aplikację" hello, w usłudze Azure AD tooenable rejestracji jednokrotnej i użytkownika automatyczne Inicjowanie obsługi administracyjnej dla aplikacji, które zapewniają lub są fronted przez usługę sieci web SCIM.

Istnieją dwa przypadki użycia przy użyciu SCIM w usłudze Azure Active Directory:

* **Inicjowanie obsługi użytkowników i grup tooapplications, która obsługuje SCIM** aplikacji, które obsługują SCIM 2.0 i używają tokenów elementu nośnego OAuth dla działania uwierzytelniania w usłudze Azure AD bez konfiguracji.
* **Skompiluj rozwiązanie inicjowania obsługi administracyjnej dla aplikacji, które obsługę innych oparty na interfejsach API** dla aplikacji z systemem innym niż SCIM, można utworzyć tootranslate punktu końcowego SCIM między punktu końcowego usługi Azure AD SCIM hello i wszelkie obsługuje aplikacji hello interfejsu API do inicjowania obsługi użytkowników. Tworzenie punktu końcowego SCIM toohelp, udostępniamy infrastruktury języka wspólnego (CLI) bibliotek oraz przykłady kodu, przedstawiających sposób toodo Podaj punkt końcowy SCIM i tłumaczenie SCIM wiadomości.  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a>Inicjowanie obsługi administracyjnej użytkowników i grup tooapplications, która obsługuje SCIM
Usługi Azure AD może być skonfigurowany tooautomatically należy przypisać użytkowników i grup tooapplications który implementuje [systemu do zarządzania tożsamościami międzydomenowego 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) usługi sieci web i zaakceptować tokenów elementu nośnego OAuth dla uwierzytelniania . W specyfikacji hello SCIM 2.0 aplikacji musi spełniać następujące wymagania:

* Obsługuje tworzenie użytkowników i grupy, zgodnie z sekcji 3.3 hello SCIM protokołu.  
* Obsługa modyfikowania użytkowników i/lub grup z żądaniami poprawki zgodnie z sekcji 3.5.2 hello SCIM protokołu.  
* Obsługuje pobieranie znanych zasobów zgodnie z sekcji 3.4.1 hello SCIM protokołu.  
* Obsługa zapytań użytkowników i grupy, zgodnie z sekcji 3.4.2 hello SCIM protokołu.  Domyślnie użytkownicy są proszeni przez externalId i grup są żądanych przez Nazwa wyświetlana.  
* Obsługa zapytań użytkownika według Identyfikatora i przez Menedżera zgodnie z sekcji 3.4.2 hello SCIM protokołu.  
* Obsługa zapytań grup według Identyfikatora i przez członka zgodnie z sekcji 3.4.2 hello SCIM protokołu.  
* Akceptuje tokenów elementu nośnego OAuth dla autoryzacji zgodnie z sekcji 2.1 hello SCIM protokołu.

Skontaktuj się z dostawcą aplikacji lub dokumentacji dostawcy aplikacji dla instrukcji zgodność z tych wymagań.

### <a name="getting-started"></a>Wprowadzenie
Aplikacje, które obsługują profilu SCIM hello opisane w tym artykule może być tooAzure podłączonej usługi Active Directory za pomocą funkcji hello "z systemem innym niż galerii aplikacji" w galerii aplikacji hello Azure AD. Po uruchomieniu połączone, Azure AD proces synchronizacji co 20 minut, gdy wysyła zapytanie punktu końcowego SCIM aplikacji hello przypisanych użytkowników i grup i tworzy lub modyfikuje je zgodnie z toohello Szczegóły przypisania.

**tooconnect aplikacji, która obsługuje SCIM:**

1. Zaloguj się za[hello portalu Azure](https://portal.azure.com). 
2. Przeglądaj zbyt ** usługi Azure Active Directory > aplikacje dla przedsiębiorstw, a następnie wybierz **nowej aplikacji > wszystkie > Non galerii aplikacji**.
3. Wprowadź nazwę aplikacji, a następnie kliknij przycisk **Dodaj** toocreate ikona obiektu aplikacji.
    
  ![][1]
  *Rysunek 2: Galerii aplikacji usługi Azure AD*
    
4. Na ekranie wynikowy hello wybierz hello **inicjowania obsługi administracyjnej** kartę w lewej kolumnie hello.
5. W hello **inicjowania obsługi trybu** menu, wybierz opcję **automatyczne**.
    
  ![][2]
  *Rysunek 3: Konfigurowanie inicjowania obsługi w hello portalu Azure*
    
6. W hello **adres URL dzierżawy** wprowadź adres URL punktu końcowego SCIM aplikacji hello hello. Przykład: https://api.contoso.com/scim/v2/
7. Jeśli punkt końcowy SCIM hello wymaga tokenu elementu nośnego OAuth od wystawcy innego niż Azure AD, a następnie hello kopiowania wymagany token elementu nośnego OAuth do hello opcjonalne **klucz tajny tokenu** pola. Jeśli to pole pozostanie puste, usługi Azure AD uwzględnione tokenu elementu nośnego OAuth wystawione przez usługi Azure AD z każdym żądaniem. Aplikacje, które używają usługi Azure AD jako dostawca tożsamości może sprawdzić poprawność tej usługi Azure AD-wystawiony token.
8. Kliknij przycisk hello **Testuj połączenie** przycisk toohave usługi Azure Active Directory próba tooconnect toohello SCIM punktu końcowego. W przypadku awarii próby hello, wyświetlane informacje o błędzie.  
9. W przypadku powodzenia hello prób tooconnect toohello aplikacji, następnie kliknij przycisk **zapisać** poświadczeń administratora hello toosave.
10. W hello **mapowania** sekcji, istnieją dwa zestawy wybieranych mapowań atrybutów: jeden dla obiektów użytkownika i jeden dla obiektów grupy. Wybierz każdego jeden atrybuty hello tooreview, które są synchronizowane z usługą Azure Active Directory tooyour aplikacji. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello użytkowników i grup w aplikacji dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

    >[!NOTE]
    >Opcjonalnie możesz wyłączyć synchronizację obiektów grupy przez wyłączenie hello "grupy" mapowania. 

11. W obszarze **ustawienia**, hello **zakres** pola definiuje, które użytkownicy i grupy są synchronizowane. Wybieranie "Synchronizacji tylko przypisane użytkowników i grup" (zalecane) zsynchronizuje tylko użytkownicy i grupy przypisane w hello **użytkowników i grup** kartę.
12. Po zakończeniu konfiguracji zmienić hello **stan inicjowania obsługi administracyjnej** za**na**.
13. Kliknij przycisk **zapisać** toostart hello inicjowania obsługi usługi Azure AD. 
14. Przydzielenia synchronizowanie tylko użytkownicy i grupy (zalecane), należy się hello tooselect **użytkowników i grup** karcie i przypisz hello użytkowników i/lub grup, które chcesz toosync.

Po rozpoczęciu hello wstępnej synchronizacji, można użyć hello **dzienniki inspekcji** karcie postępu toomonitor, który zawiera wszystkie akcje wykonywane przez hello świadczenie usługi w aplikacji. Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

>[!NOTE]
>Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello. 


## <a name="building-your-own-provisioning-solution-for-any-application"></a>Tworzenie rozwiązania inicjowania obsługi administracyjnej dla dowolnej aplikacji
Tworząc interfejsy usługi sieci web SCIM z usługi Azure Active Directory, można włączyć pojedynczego użytkownika logowania jednokrotnego i automatyczne Inicjowanie obsługi praktycznie dowolnej aplikacji, która zawiera użytkownika inicjowania obsługi interfejsu API REST lub protokołu SOAP.

Oto jak to działa:

1. Usługa Azure AD zapewnia o nazwie biblioteki wspólnej infrastruktury języka [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/). Deweloperów i integratorów systemów. platforma można użyć tej biblioteki toocreate i wdrożyć punkt końcowy usługi sieci web opartych na SCIM może nawiązywać połączenia magazynu tożsamości aplikacji tooany usługi Azure AD.
2. Mapowania są implementowane w hello sieci web usługi toomap hello standardowych użytkowników schematu toohello użytkowników schematu i wymagane przez aplikację hello protokołu.
3. adres URL punktu końcowego Hello jest zarejestrowany w usłudze Azure AD w ramach niestandardowych aplikacji w galerii aplikacji hello.
4. Użytkownicy i grupy są przypisywane toothis aplikacji w usłudze Azure AD. Po przypisania są umieszczane w aplikacji docelowej toohello toobe synchronizowane kolejki. proces synchronizacji Hello obsługi kolejki hello jest uruchamiana co 20 minut.

### <a name="code-samples"></a>Przykłady kodu
toomake to przetwarzanie łatwiej, grupy [przykłady kodu](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) pod warunkiem że utworzyć SCIM punkt końcowy usługi sieci web i Wykaż, automatyczne udostępnianie. Przykład jest dostawcy, który przechowuje plik z wierszami z wartościami rozdzielonymi przecinkami reprezentująca użytkowników i grup.  jest Hello innego dostawcy, który działa na powitania usługi Amazon Web Services tożsamość i zarządzanie dostępem.  

**Wymagania wstępne**

* Visual Studio 2013 lub nowszy
* [Zestaw Azure SDK dla platformy .NET](https://azure.microsoft.com/downloads/)
* Urządzenia z systemem Windows, które obsługuje hello ASP.NET framework 4.5 toobe używane jako hello SCIM punktu końcowego. Tego komputera muszą być dostępne z chmury hello
* [Subskrypcja platformy Azure w wersji próbnej lub licencjonowanej wersji programu Azure AD Premium](https://azure.microsoft.com/services/active-directory/)
* przykład Amazon AWS Hello wymaga bibliotek hello [usług AWS narzędzi dla programu Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html). Aby uzyskać więcej informacji, zobacz plik README hello pliku dołączonego hello próbki.

### <a name="getting-started"></a>Wprowadzenie
Witaj Najprostszym sposobem tooimplement SCIM punktu końcowego, który może zaakceptować inicjowania obsługi żądań z usługi Azure AD jest toobuild i wdrażanie hello przykładowy kod, który plik wartości rozdzielanych przecinkami (CSV) tooa użytkowników elastycznie hello.

**toocreate punktu końcowego SCIM próbki:**

1. Pobierz przykładowy kod hello na [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)
2. Rozpakuj pakiet hello i umieść go na komputerze z systemem Windows w lokalizacji, takich jak C:\AzureAD-BYOA-Provisioning-Samples\.
3. W tym folderze uruchom program hello FileProvisioningAgent rozwiązania w programie Visual Studio.
4. Wybierz **Narzędzia > Menedżer pakietów biblioteki > konsoli Menedżera pakietów**i wykonaj następujące polecenia dotyczące hello FileProvisioningAgent tooresolve hello rozwiązania odwołania hello:
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. Tworzenie projektu FileProvisioningAgent hello.
6. Uruchamianie hello wiersza polecenia aplikacji w systemie Windows (jako Administrator), a następnie użyj hello **cd** polecenia toochange hello katalogu tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folderu.
7. Witaj uruchom następujące polecenie, zastępując < adres ip > hello IP adresu lub nazwy domeny komputera z systemem Windows hello:
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. W systemie Windows w obszarze **ustawienia systemu Windows > Sieć i Internet ustawienia**, wybierz pozycję hello **zapory systemu Windows > Zaawansowane ustawienia**i Utwórz **reguły ruchu przychodzącego** który Umożliwia dostęp przychodzący tooport 9000.
9. W przypadku komputera z systemem Windows hello za routerem, hello router potrzeb toobe skonfigurowane tooperform tłumaczenia dostępu do sieci między portu 9000 będący narażonych toohello internet i port 9000 na komputerze z systemem Windows hello. Jest to wymagane dla usługi Azure AD toobe stanie tooaccess tego punktu końcowego w chmurze hello.

**tooregister hello próbki SCIM punktu końcowego w usłudze Azure AD:**

1. Zaloguj się za[hello portalu Azure](https://portal.azure.com). 
2. Przeglądaj zbyt ** usługi Azure Active Directory > aplikacje dla przedsiębiorstw, a następnie wybierz **nowej aplikacji > wszystkie > Non galerii aplikacji**.
3. Wprowadź nazwę aplikacji, a następnie kliknij przycisk **Dodaj** toocreate ikona obiektu aplikacji. utworzony obiekt aplikacji Hello jest aplikacji docelowej hello zamierzonego toorepresent czy udostępniania tooand implementacja punktu końcowego SCIM pojedynczego hello jednokrotne, a nie tylko.
4. Na ekranie wynikowy hello wybierz hello **inicjowania obsługi administracyjnej** kartę w lewej kolumnie hello.
5. W hello **inicjowania obsługi trybu** menu, wybierz opcję **automatyczne**.
    
  ![][2]
  *Rysunek 4: Konfigurowanie inicjowania obsługi w hello portalu Azure*
    
6. W hello **adres URL dzierżawy** wprowadź adres URL hello udostępniane przez internet i port punktu końcowego SCIM. Będzie to coś jak http://testmachine.contoso.com:9000 lub http://<ip-address>:9000/, gdzie < adres ip > jest hello internet widoczne IP adres.  
7. Jeśli punkt końcowy SCIM hello wymaga tokenu elementu nośnego OAuth od wystawcy innego niż Azure AD, a następnie hello kopiowania wymagany token elementu nośnego OAuth do hello opcjonalne **klucz tajny tokenu** pola. Jeśli to pole pozostanie puste, usługi Azure AD będą zawierać tokenu elementu nośnego OAuth wystawione przez usługi Azure AD z każdym żądaniem. Aplikacje, które używają usługi Azure AD jako dostawca tożsamości może sprawdzić poprawność tej usługi Azure AD-wystawiony token.
8. Kliknij przycisk hello **Testuj połączenie** przycisk toohave usługi Azure Active Directory próba tooconnect toohello SCIM punktu końcowego. W przypadku awarii próby hello, wyświetlane informacje o błędzie.  
9. W przypadku powodzenia hello prób tooconnect toohello aplikacji, następnie kliknij przycisk **zapisać** poświadczeń administratora hello toosave.
10. W hello **mapowania** sekcji, istnieją dwa zestawy wybieranych mapowań atrybutów: jeden dla obiektów użytkownika i jeden dla obiektów grupy. Wybierz każdego jeden atrybuty hello tooreview, które są synchronizowane z usługą Azure Active Directory tooyour aplikacji. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello użytkowników i grup w aplikacji dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.
11. W obszarze **ustawienia**, hello **zakres** pola definiuje, które użytkownicy i grupy są synchronizowane. Wybieranie "Synchronizacji tylko przypisane użytkowników i grup" (zalecane) zsynchronizuje tylko użytkownicy i grupy przypisane w hello **użytkowników i grup** kartę.
12. Po zakończeniu konfiguracji zmienić hello **stan inicjowania obsługi administracyjnej** za**na**.
13. Kliknij przycisk **zapisać** toostart hello inicjowania obsługi usługi Azure AD. 
14. Przydzielenia synchronizowanie tylko użytkownicy i grupy (zalecane), należy się hello tooselect **użytkowników i grup** karcie i przypisz hello użytkowników i/lub grup, które chcesz toosync.

Po rozpoczęciu hello wstępnej synchronizacji, można użyć hello **dzienniki inspekcji** karcie postępu toomonitor, który zawiera wszystkie akcje wykonywane przez hello świadczenie usługi w aplikacji. Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

Ostatnim krokiem Hello podczas weryfikowania próbki hello jest hello tooopen TargetFile.csv plików w folderze \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug hello na komputerze z systemem Windows. Po uruchomieniu procesu udostępniania hello ten plik zawiera szczegóły hello wszystkich przypisane i udostępnione użytkowników i grup.

### <a name="development-libraries"></a>Biblioteki programistyczne
toodevelop własnej usługi sieci web, zgodne ze specyfikacją SCIM toohello, najpierw zapoznać się z następującej biblioteki dostarczony przez firmę Microsoft toohelp przyspieszyć proces tworzenia hello hello: 

1. Wspólne biblioteki języka infrastruktury (CLI) dostępnych do użycia z językami oparte na infrastruktury, takich jak C#. Jeden z tych bibliotek [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), deklaruje interfejsu Microsoft.SystemForCrossDomainIdentityManagement.IProvider, pokazano na następującej ilustracji hello: A Developer przy użyciu bibliotek hello czy implementuje ten interfejs z klasy, która może być określone, objęty dostawcę. biblioteki Hello umożliwiają toodeploy developer hello odpowiada specyfikacji SCIM toohello usługi sieci web. usługi sieci web Hello może być obsługiwany albo w ramach Internetowe usługi informacyjne lub dowolnego pliku wykonywalnego zestawu wspólną infrastrukturę języka. Żądanie jest przetłumaczyć dostawcy toohello wywołania metody, które może być programowane za toooperate developer hello na niektórych magazynu tożsamości.
  
  ![][3]
  
2. [Express obsługi trasy](http://expressjs.com/guide/routing.html) są dostępne na potrzeby analizowania reprezentujący wywołań (jak określono w specyfikacji SCIM hello), usługa sieci web node.js tooa obiektów żądania node.js.   

### <a name="building-a-custom-scim-endpoint"></a>Tworzenie punktu końcowego niestandardowych SCIM
Przy użyciu biblioteki interfejsu wiersza polecenia hello, deweloperzy przy użyciu tych bibliotek mogą być hostowane swoich usług w dowolnym pliku wykonywalnego zestawu wspólną infrastrukturę języka lub do internetowych usług informacyjnych. Poniżej przedstawiono przykładowy kod w celu hostowania usługi w zestawie pliku wykonywalnego, pod adresem hello http://localhost:9000: 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

Ta usługa musi mieć HTTP adres i serwera uwierzytelniania certyfikat które hello główny urząd certyfikacji jest jedną z następujących hello: 

* CNNIC
* Comodo
* CyberTrust
* DigiCert
* GeoTrust
* GlobalSign
* Go Daddy
* VeriSign
* WoSign

Certyfikat uwierzytelniania serwera może być powiązane tooa portu na hoście z systemem Windows przy użyciu narzędzia powłoki sieciowej hello: 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

W tym miejscu wartość hello argumentu parametrów certhash hello jest hello odcisk palca certyfikatu hello, podczas hello wartość podana dla argumentu appid hello jest umownym identyfikatorem globalnie unikatowe.  

usługi hello toohost w usługach IIS, deweloper może kompilacji zestawem CLA kod biblioteki z klasy o nazwie uruchamiania w domyślnej przestrzeni nazw hello hello zestawu.  Oto przykład takiego klasy: 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a>Obsługa punktu końcowego uwierzytelniania
Żądania z usługi Azure Active Directory zawierać tokenu elementu nośnego OAuth 2.0.   Wszystkie żądania obsługi odbierania hello powinna uwierzytelniać Witaj wystawca jako imieniu hello oczekiwano dzierżawy usługi Azure Active Directory, dla toohello dostępu do usługi sieci web Azure Active Directory Graph usługi Azure Active Directory.  W tokenie hello wystawcy hello jest identyfikowany przez oświadczenie iss, takich jak "iss": "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".  W tym przykładzie adres podstawowy hello hello wartości oświadczenia, https://sts.windows.net, identyfikuje usługi Azure Active Directory, jak Witaj wystawca, gdy hello adres względny segmentu, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, jest unikatowy identyfikator hello Azure Active Katalog dzierżawy, w imieniu którego hello token został wystawiony.  Jeśli hello token został wystawiony dla uzyskiwania dostępu do usługi sieci web Azure Active Directory Graph hello, następnie identyfikator hello tej usługi 00000002-0000-0000-c000-000000000000, powinny być hello wartość tokenu hello lub oświadczeń.  

Deweloperzy przy użyciu bibliotek CLA hello obsługiwane przez firmę Microsoft do tworzenia usługi SCIM może uwierzytelnić żądania z usługi Azure Active Directory przy użyciu pakietu Microsoft.Owin.Security.ActiveDirectory hello, wykonując następujące czynności: 

1. U dostawcy należy zaimplementować właściwości Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior hello przez właśnie zwrócić toobe — metoda, wywoływana, gdy jest uruchomiona usługa hello: 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. Dodaj wszystkie żądania tooany punktów końcowych usługi hello uwierzytelniony jako mając token wystawiony przez usługę Azure Active Directory w imieniu określonego dzierżawcę, dla toohello dostępu do usługi sieci web Azure AD Graph hello następującego kodu toothat metody toohave: 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a>Schemat użytkowników i grup
Usługa Azure Active Directory można udostępnić dwa typy usług sieci web tooSCIM zasobów.  Te typy zasobów są użytkowników i grup.  

Zasoby użytkownika są identyfikowane za pomocą identyfikatora schematu hello, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, który jest dostępny w tej specyfikacji protokołu: http://tools.ietf.org/html/draft-ietf-scim-core-schema.  Witaj domyślne mapowanie atrybutów hello użytkowników w usłudze Azure Active Directory toohello atrybutów zasobów urn: ietf:params:scim:schemas:extension:enterprise:2.0:User znajduje się w tabeli 1, poniżej.  

Grupy zasobów są identyfikowane za pomocą identyfikatora schematu hello, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  Tabela 2, poniżej przedstawiono hello domyślne mapowanie atrybutów hello grup w usłudze Azure Active Directory toohello atrybuty http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group zasobów.  

### <a name="table-1-default-user-attribute-mapping"></a>Tabela 1: Domyślne mapowanie atrybutu użytkownika
| Azure użytkownika usługi Active Directory | urn: ietf:params:scim:schemas:extension:enterprise:2.0:User |
| --- | --- |
| IsSoftDeleted |Aktywne |
| Nazwa wyświetlana |Nazwa wyświetlana |
| TelephoneNumber faksu |.value phoneNumbers [eq typu "faks"] |
| Imię |name.givenName |
| Stanowisko |Tytuł |
| Poczty |.value wiadomości e-mail [eq typu "Praca"] |
| mailNickname |externalId |
| Menedżer |Menedżer |
| Telefon komórkowy |.value phoneNumbers [eq typu "mobile"] |
| Identyfikator obiektu |id |
| KodPocztowy |.postalCode adresów [eq typu "Praca"] |
| Adresy serwerów proxy |wiadomości e-mail [Wpisz eq "other"]. Wartość |
| Physical dostarczania-OfficeName |adresy [Wpisz eq "other"]. Sformatowany |
| Adres |.streetAddress adresów [eq typu "Praca"] |
| nazwisko |name.familyName |
| Numer telefonu |.value phoneNumbers [eq typu "Praca"] |
| PrincipalName użytkownika |Nazwa użytkownika |

### <a name="table-2-default-group-attribute-mapping"></a>Tabela 2: Domyślne grupy atrybutów mapowanie
| Grupa usługi Active Directory systemu Azure | http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group |
| --- | --- |
| Nazwa wyświetlana |externalId |
| Poczty |.value wiadomości e-mail [eq typu "Praca"] |
| mailNickname |Nazwa wyświetlana |
| Elementy członkowskie |Elementy członkowskie |
| Identyfikator obiektu |id |
| proxyAddresses |wiadomości e-mail [Wpisz eq "other"]. Wartość |

## <a name="user-provisioning-and-de-provisioning"></a>Inicjowanie obsługi użytkowników i anulowanie obsługi.
Witaj następujące wiadomości powitania ilustracji przedstawiono z usługi Azure Active Directory i wysyła tooa SCIM toomanage hello cyklu życia usług użytkownika w innym magazynie tożsamości. Hello diagram pokazuje też, jak usługa SCIM implementowane przy użyciu biblioteki interfejsu wiersza polecenia hello obsługiwane przez firmę Microsoft do tworzenia, się, że takie usługi tłumaczenia te żądania na wywołania metody toohello dostawcy.  

![][4]
*Rysunek 5: Użytkownik aprowizację i anulowanie obsługi sekwencji*

1. Azure zapytań usługi Active Directory hello usługi dla użytkownika z wartością atrybutu externalId dopasowania wartości atrybutu mailNickname hello użytkownika w usłudze Azure AD. Zapytanie Hello jest wyrażony jako żądania protokołu HTTP (Hypertext Transfer), np. w tym przykładzie, w którym jyoung znajduje się przykład mailNickname użytkownika w usłudze Azure Active Directory: 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  Jeśli usługa hello został zbudowany przy użyciu bibliotek wspólną infrastrukturę języka hello obsługiwane przez firmę Microsoft dla implementacji usługi SCIM, Żądanie hello jest przetłumaczony na toohello wywołanie metody zapytania hello usługodawcy.  Oto podpisu hello tej metody: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  Oto hello definicji interfejsu Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters hello: 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  W następujące przykładowe zapytania dla użytkownika z danej wartości dla atrybutu externalId hello hello wartości hello Argumenty przekazane toohello metoda zapytania są: 
  * Parametry. AlternateFilters.Count: 1
  * Parametry. AlternateFilters.ElementAt(0). AttributePath: "externalId"
  * Parametry. AlternateFilters.ElementAt(0). OperatorPorównania: ComparisonOperator.Equals
  * Parametry. AlternateFilter.ElementAt(0). ComparisonValue: "jyoung"
  * correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin. Identyfikator żądania"] 

2. Jeśli hello odpowiedzi tooa zapytania toohello usługi sieci web dla użytkownika z wartością atrybutu externalId odpowiadającą wartości atrybutu mailNickname hello użytkownika nie zwraca żadnych użytkowników, następnie usługi Azure Active Directory żąda tego hello usług świadczonych przez użytkownika odpowiednie toohello co w usłudze Azure Active Directory.  Oto przykład takiego żądania: 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  obsługiwane przez firmę Microsoft dla implementacji usługi SCIM bibliotek wspólną infrastrukturę języka Hello przekłada to żądanie do toohello wywołanie metody Create hello usługodawcy.  Witaj metody Create ma podpis: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  W tooprovision żądania użytkownika hello wartość argumentu zasobów hello jest wystąpieniem hello Microsoft.SystemForCrossDomainIdentityManagement. Klasa Core2EnterpriseUser zdefiniowany w bibliotece Microsoft.SystemForCrossDomainIdentityManagement.Schemas hello.  Jeśli hello żądania tooprovision hello użytkownika zakończy się powodzeniem, następnie hello implementacja metody hello jest oczekiwany tooreturn wystąpienia hello Microsoft.SystemForCrossDomainIdentityManagement. Klasa Core2EnterpriseUser, z hello wartość właściwości identyfikator hello ustawić toohello Unikatowy identyfikator użytkownika nowo aprowizowanej hello.  

3. tooupdate użytkownika znane tooexist w magazynie tożsamości przez SCIM usługi Azure Active Directory będzie kontynuowane, żądając hello bieżący stan tego użytkownika z usługi hello z żądaniem, takich jak: 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  W usłudze utworzony przy użyciu bibliotek wspólną infrastrukturę języka hello obsługiwane przez firmę Microsoft dla implementacji usługi SCIM Żądanie hello jest przetłumaczyć toohello wywołanie metody pobierania hello usługodawcy.  Oto hello podpis metody pobierania hello: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  W przykładzie hello żądania tooretrieve hello bieżącego stanu użytkownika hello wartości właściwości hello obiektu hello dostarczonych jako wartość hello argumentu parametrów hello są następujące: 
  
  * Identyfikator: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"

4. Jeśli atrybut odwołania jest toobe zaktualizowane, następnie usługi Azure Active Directory zapytania hello usługi toodetermine czy hello bieżącą wartość atrybutu odwołania hello w magazynie tożsamości hello fronted przez usługę hello pasuje już hello wartość tego atrybutu w usłudze Azure Active Directory. W przypadku użytkowników hello tylko z których hello bieżąca wartość jest poddawany kwerendzie w ten sposób jest hello Menedżera atrybutem. Oto przykład toodetermine żądania czy hello Menedżera atrybut obiektu określonego użytkownika aktualnie ma określoną wartość: 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  Witaj wartość parametru zapytania atrybuty hello, identyfikator, oznacza, że jeśli obiekt użytkownika istnieje odpowiadającej dostarczonego jako wartość parametru zapytania filtru hello hello wyrażenia hello, a następnie usługa hello jest oczekiwany toorespond z urn: ietf:params:scim:schemas: podstawowe: 2.0:User lub urn: ietf:params:scim:schemas:extension:enterprise:2.0:User zasobów łącznie tylko hello wartość atrybutu id tego zasobu.  Witaj wartość hello **identyfikator** atrybut nosi toohello obiektu żądającego. Znajduje się on w hello wartość parametru zapytania filtru hello; pyta celem Hello jest rzeczywiście toorequest minimalnego reprezentację z zasobem, który spełnia wyrażenie filtru hello jako ze wskazaniem, czy jakikolwiek obiekt istnieje.   

  Jeśli usługa hello został zbudowany przy użyciu bibliotek wspólną infrastrukturę języka hello obsługiwane przez firmę Microsoft dla implementacji usługi SCIM, Żądanie hello jest przetłumaczony na toohello wywołanie metody zapytania hello usługodawcy. wartość Hello hello właściwości obiektu hello dostarczonych jako wartość hello argumentu parametrów hello są następujące: 
  
  * Parametry. AlternateFilters.Count: 2
  * Parametry. AlternateFilters.ElementAt(x). AttributePath: "id"
  * Parametry. AlternateFilters.ElementAt(x). OperatorPorównania: ComparisonOperator.Equals
  * Parametry. AlternateFilter.ElementAt(x). ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * Parametry. AlternateFilters.ElementAt(y). AttributePath: "manager"
  * Parametry. AlternateFilters.ElementAt(y). OperatorPorównania: ComparisonOperator.Equals
  * Parametry. AlternateFilter.ElementAt(y). ComparisonValue: "2819c223-7f76-453a-919d-413861904646"
  * Parametry. RequestedAttributePaths.ElementAt(0): "id"
  * Parametry. SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"

  W tym miejscu hello wartość indeksu hello x może być 0 i hello wartość y o indeksie hello może być 1, lub hello wartość x może być równa 1 i hello wartość y może mieć wartość 0, w zależności od kolejności hello wyrażeń hello parametru zapytania filtru hello.   

5. Oto przykład żądania z usługi Azure Active Directory tooan SCIM usługi tooupdate użytkownika: 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  Implementowanie usług SCIM biblioteki wspólną infrastrukturę języka Microsoft Hello przekłada hello żądania do toohello wywołanie metody aktualizacji hello usługodawcy. Oto hello podpis hello metody aktualizacji: 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    W przykładzie hello tooupdate żądania użytkownika dostarczony jako wartość argumentu poprawki hello hello obiekt hello ma wartości tych właściwości: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"
  * (PatchRequest jako PatchRequest2). Operations.Count: 1
  * (PatchRequest jako PatchRequest2). Operations.ElementAt(0). OperationName: OperationName.Add
  * (PatchRequest jako PatchRequest2). Operations.ElementAt(0). Path.AttributePath: "manager"
  * (PatchRequest jako PatchRequest2). Operations.ElementAt(0). Value.Count: 1
  * (PatchRequest jako PatchRequest2). Operations.ElementAt(0). Value.ElementAt(0). Odwołanie: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646
  * (PatchRequest jako PatchRequest2). Operations.ElementAt(0). Value.ElementAt(0). Wartość: 2819c223-7f76-453a-919d-413861904646

6. toode-provision użytkownika z magazynu tożsamości fronted przez usługę SCIM, takich jak wysyła żądanie usługi Azure AD: 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Jeśli usługa hello został zbudowany przy użyciu bibliotek wspólną infrastrukturę języka hello obsługiwane przez firmę Microsoft dla implementacji usługi SCIM, Żądanie hello jest przetłumaczony na toohello wywołanie metody Delete hello usługodawcy.   Ta metoda ma podpis: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  dostarczony jako wartość argumentu resourceIdentifier hello hello obiekt Hello ma wartości tych właściwości w przykładzie hello żądania toode-przepisu użytkownika: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"

## <a name="group-provisioning-and-de-provisioning"></a>Grupy aprowizację i anulowanie obsługi
Witaj następujące wiadomości powitania przedstawiono na ilustracji Azure AcD i wysyła tooa SCIM toomanage hello cyklu życia usług grupy w innym magazynie tożsamości.  Te komunikaty różnią się od wiadomości powitania dotyczące toousers na trzy sposoby: 

* Schemat Hello zasób grupy jest rozpoznawany jako http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  
* Żądania wysyłane grup tooretrieve określać atrybutu członków hello jest toobe wykluczone z dowolnego zasobu podany w żądaniu toohello odpowiedzi.  
* Określa, czy jest atrybut odwołania ma określoną wartość są żądania dotyczące hello elementy członkowskie atrybutu toodetermine żądań.  

![][5]
*Rysunek 6: Grupy aprowizację i anulowanie obsługi sekwencji*

## <a name="related-articles"></a>Pokrewne artykuły:
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Automatyzowanie inicjowania obsługi administracyjnej użytkowników/anulowania zastrzeżenia tooSaaS aplikacji](active-directory-saas-app-provisioning.md)
* [Dostosowywanie mapowań atrybutów do inicjowania obsługi użytkowników](active-directory-saas-customizing-attribute-mappings.md)
* [Tworzenie wyrażeń na potrzeby mapowań atrybutów](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtry zakresu dla Inicjowanie obsługi użytkowników](active-directory-saas-scoping-filters.md)
* [Powiadomienia aprowizacji kont](active-directory-saas-account-provisioning-notifications.md)
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
