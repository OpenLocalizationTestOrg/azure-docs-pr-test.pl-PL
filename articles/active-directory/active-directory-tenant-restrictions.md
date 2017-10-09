---
title: "aaaManage dostępu toocloud aplikacji poprzez ograniczenie dzierżaw - Azure | Dokumentacja firmy Microsoft"
description: "Jak toouse toomanage ograniczenia dzierżawy, którzy użytkownicy mają dostęp do aplikacji w oparciu swojej dzierżawy usługi Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: kgremban
ms.openlocfilehash: 6470fa217738b29104353ae17a2f53216f825c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-tenant-restrictions-toomanage-access-toosaas-cloud-applications"></a>Używanie ograniczeń dzierżawy toomanage dostępu tooSaaS chmury aplikacji

Dużych organizacjach, które wyróżnić zabezpieczeń mają toomove toocloud usług, takich jak usługi Office 365, ale tooknow potrzeba, dostępnej użytkowników tylko zatwierdzone zasobów. Tradycyjnie firm ograniczyć nazwy domeny lub adresów IP podczas toomanage dostępu. Takie podejście kończy się niepowodzeniem w świecie, gdzie hostowane są aplikacji SaaS w chmurze publicznej, w systemie nazw domen udostępnionego, takich jak outlook.office.com i login.microsoftonline.com. Blokowanie tych adresów może uniemożliwić użytkownikom uzyskiwanie dostępu do programu Outlook w sieci web hello całkowicie, zamiast jedynie ograniczenie, tooapproved tożsamości i zasobów.

Żądanie toothis rozwiązania Azure usługi Active Directory jest funkcję ograniczenia dzierżawy. Dzierżawy ograniczenia umożliwia organizacjom toocontrol dostępu tooSaaS chmury aplikacje oparte na powitania usługi Azure AD dzierżawy hello aplikacji na użytek logowania jednokrotnego. Na przykład można tooallow dostępu tooyour aplikacji używanych w organizacji usługi Office 365, zapobiegając organizacje tooother dostęp do wystąpień te same aplikacje.  

Ograniczenia dzierżawy zawiera organizacje hello możliwości toospecify hello listę użytkowników mogą tooaccess dzierżaw. Następnie usługi Azure AD tylko udziela dostępu toothese dozwolone dzierżaw.

Ten artykuł dotyczy ograniczenia dzierżawy dla usługi Office 365, ale funkcja hello powinien współpracować z dowolnej aplikacji w chmurze SaaS korzystający z protokołów nowoczesnego uwierzytelniania w usłudze Azure AD dla logowania jednokrotnego. Jeśli używasz SaaS aplikacji za pomocą innej usługi Azure AD dzierżawy dzierżawy hello używane przez usługi Office 365, upewnij się, czy wszystkie wymagane dzierżaw są dozwolone. Aby uzyskać więcej informacji o aplikacji SaaS w chmurze, zobacz hello [Active Directory Marketplace](https://azure.microsoft.com/en-us/marketplace/active-directory/).

## <a name="how-it-works"></a>Jak to działa

Witaj ogólne rozwiązanie obejmuje hello następujące składniki: 

1. **Usługi Azure AD** — Jeśli hello `Restrict-Access-To-Tenants: <permitted tenant list>` jest obecny, Azure AD tylko problemy z tokenów zabezpieczających dla hello dozwolone dzierżaw. 

2. **Lokalnej infrastruktury serwera proxy** — urządzenie serwera proxy do kontroli SSL, skonfigurowanych tooinsert hello nagłówek zawierający listę hello umieszczone dzierżaw w ruch kierowany do usługi Azure AD. 

3. **Oprogramowanie klienckie** — ograniczenia dzierżawy toosupport, oprogramowanie klienckie musi żądać tokeny bezpośrednio z usługi Azure AD, tak, aby ruch może zostać przechwycona przez hello infrastruktury usługi Serwer proxy. Ograniczenia dzierżawy jest obecnie obsługiwane przez aplikacje pakietu Office 365 przeglądarki i klienci Office stosowania nowoczesnego uwierzytelniania (na przykład OAuth 2.0). 

4. **Nowoczesne uwierzytelnianie** — usługi w chmurze, należy użyć toouse nowoczesnego uwierzytelniania ograniczenia dzierżawy i blokowanie dostępu tooall dzierżaw z systemem innym niż dozwolone. Usługi Office 365 chmury musi być skonfigurowany toouse nowoczesnego uwierzytelniania protokołów domyślnie. Witaj najnowszych informacji na temat obsługi usługi Office 365 dla nowoczesnego uwierzytelniania, przeczytaj [nowoczesne uwierzytelnianie usługi Office 365 aktualizacji](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/).

powitania po diagram przedstawia przepływ ruchu wysokiego poziomu hello. Inspekcja SSL jest wymagany tylko na ruch tooAzure AD, nie toohello usługi Office 365 usługi w chmurze. Ta różnica jest ważne, ponieważ wolumin ruchu hello na potrzeby uwierzytelniania tooAzure AD jest zwykle znacznie niższe niż ruchu woluminu tooSaaS aplikacji, takich jak Exchange Online i SharePoint Online.

![Ograniczenia ruchu dzierżawy — diagram](./media/active-directory-tenant-restrictions/traffic-flow.png)

## <a name="set-up-tenant-restrictions"></a>Konfigurowanie ograniczeń dzierżawy

Istnieją dwa tooget kroki pracy z ograniczeń dzierżawy. pierwszym krokiem Hello jest toomake łączenie toohello prawo adresy klientów. Witaj drugi jest tooconfigure infrastruktury serwera proxy.

### <a name="urls-and-ip-addresses"></a>Adresy URL i adresów IP

toouse ograniczenia dzierżawy klientów musi być toohello tooconnect stanie następujące adresy URL usługi Azure AD tooauthenticate: login.microsoftonline.com, login.microsoft.com i login.windows.net. Ponadto tooaccess usługi Office 365, klienci również musi być możliwe tooconnect toohello nazw FQDN/adresy URL i adresów IP zdefiniowanych w [zakresów adresów IP i URL usługi Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2). 

### <a name="proxy-configuration-and-requirements"></a>Konfiguracja serwera proxy i wymagania

powitania po konfiguracji jest wymagana tooenable ograniczenia dzierżawcy przy użyciu infrastruktury serwera proxy. W tych wskazówkach jest ogólny, dlatego należy zapoznać się dokumentacji dostawcy tooyour serwera proxy do wykonania określonych kroków.

#### <a name="prerequisites"></a>Wymagania wstępne

- powitania serwera proxy musi być stanie tooperform SSL zatrzymania, wstawiania nagłówek HTTP oraz filtru docelowych przy użyciu nazw FQDN/adresów URL. 

- Klienci muszą ufać hello łańcucha certyfikatów przedstawiony przez hello proxy dla komunikacji SSL. Na przykład jeśli są używane certyfikaty z wewnętrznej infrastruktury kluczy publicznych, hello wewnętrzny wystawiających certyfikaty głównego urzędu certyfikacji musi być zaufany.

- Ta funkcja jest dostępna w subskrypcji usługi Office 365, ale jeśli chcesz aplikacji SaaS tooother toouse ograniczenia dzierżawy toocontrol dostępu następnie licencji Azure AD Premium 1 są wymagane.

#### <a name="configuration"></a>Konfiguracja

Dla każdego przychodzącego żądania toologin.microsoftonline.com, login.microsoft.com i login.windows.net, Wstaw dwa nagłówki HTTP: *ograniczanie dostępu do dzierżawców* i *ograniczanie dostępu do kontekstu*.

nagłówki Hello powinna zawierać hello następujące elementy: 
- Dla *ograniczanie dostępu do dzierżawców*, wartość \<dozwolone listy dzierżawy\>, która jest rozdzielana przecinkami lista dzierżawców ma tooallow tooaccess użytkowników. Dowolnej domeny, która jest zarejestrowana w usłudze dzierżawcy mogą być używane tooidentify hello dzierżawy na tej liście. Na przykład toopermit dostępu dzierżawcy tooboth Contoso i Fabrikam, hello wygląda pary nazwa/wartość, jak:`Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com` 
- Dla *ograniczanie dostępu do kontekstu*, wartość identyfikatora jednego katalogu deklarowanie dzierżawy, który jest ustawienie hello dzierżawy ograniczenia. Na przykład toodeclare Contoso jako hello dzierżawy, która ustawić hello zasady ograniczeń dzierżawy pary nazwa/wartość hello wyglądają następująco:`Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`  

> [!TIP]
> Identyfikator katalogu można znaleźć w hello [portalu Azure](https://portal.azure.com). Zaloguj się jako administrator, wybierz opcję **usługi Azure Active Directory**, a następnie wybierz pozycję **właściwości**.

tooprevent użytkownikom wstawianie własnych nagłówka HTTP z niezatwierdzonej dzierżawcami, powitania serwera proxy musi tooreplace hello ograniczanie dostępu do dzierżawcy nagłówka, jeśli jest już obecny w hello przychodzące żądanie. 

Klienci muszą być proxy hello toouse wymuszone dla wszystkich żądań toologin.microsoftonline.com login.microsoft.com i login.windows.net. Na przykład jeśli PAC pliki są używane toodirect klientów toouse hello proxy, użytkownicy końcowi nie należy tooedit może być ani wyłączyć hello PAC plików.

## <a name="hello-user-experience"></a>środowisko użytkownika Hello

W tej sekcji przedstawiono hello środowisko dla administratorów i użytkowników końcowych.

### <a name="end-user-experience"></a>Środowisko użytkownika końcowego

Przykład użytkownika znajduje się w sieci firmy Contoso hello, ale próbuje tooaccess hello Fabrikam wystąpienie udostępnione aplikacji SaaS takich jak program Outlook online. Jeśli firma Contoso jest dzierżawca nie jest dozwolone dla tego wystąpienia, hello użytkownik zobaczy następujący hello następujące strony:

![Strona dla użytkowników w dzierżaw z systemem innym niż dozwolone odmowa dostępu](./media/active-directory-tenant-restrictions/end-user-denied.png)

### <a name="admin-experience"></a>Środowisko pracy administratora

Podczas konfiguracji ograniczenia dzierżawy jest wykonywana na powitania infrastruktury firmowy serwer proxy, Administratorzy mogą uzyskiwać dostęp hello ograniczenia dzierżawy raportów w portalu Azure hello bezpośrednio. Witaj tooview raporty, przejdź toohello Omówienie usługi Azure Active Directory, a następnie sprawdź w obszarze innych funkcji.

Witaj, Administratorze dzierżawy hello określony jako dzierżawy hello ograniczony dostęp do kontekstu, można użyć tego toosee raportu wszystkie sesje logowania zablokowane z powodu hello zasady ograniczeń dzierżawy, w tym tożsamości hello używane i katalog docelowy hello identyfikatora.

![Użyj prób logowania Azure tooview portalu ograniczone hello](./media/active-directory-tenant-restrictions/portal-report.png)

Podobnie jak inne raporty w hello portalu Azure możesz użyć filtrów toospecify hello zakres raportu. Można filtrować według określonego użytkownika, aplikacji, klienta lub interwał czasu.

## <a name="office-365-support"></a>Obsługa usługi Office 365

Aplikacje pakietu Office 365 musi spełniać dwa kryteria Obsługa toofully ograniczenia dzierżawy:

1. używaną powitania klienta obsługuje nowoczesnego uwierzytelniania
2. Nowoczesne uwierzytelnianie jest włączony w domyślnym protokołem uwierzytelniania dla usługi w chmurze hello hello.

Odwołuje się zbyt[nowoczesne uwierzytelnianie usługi Office 365 aktualizacji](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) dla hello najnowsze informacje, na które Office klientami obsługuje obecnie nowoczesnego uwierzytelniania. Ta strona zawiera również tooinstructions łączy umożliwiających nowoczesnego uwierzytelniania na określonych usługi Exchange Online i Skype dla firm Online dzierżaw. Domyślnie w usłudze SharePoint Online jest już włączone nowoczesnego uwierzytelniania.

Ograniczenia dzierżawy jest obecnie obsługiwane przez usługi Office 365 aplikacji opartych na przeglądarce (hello SharePoint portalu usługi Office, Yammer, witryn programu Microsoft Outlook na powitania sieci Web itd.). Grubość klientów (program Outlook, Skype dla firm, Word, Excel, PowerPoint, itp.) Ograniczenia dzierżawy są wymuszane tylko, gdy nowoczesnego uwierzytelniania jest używany.  

Outlook i Skype dla firm klientów, którzy obsługują nowoczesnego uwierzytelniania są nadal toouse starszych protokołów przed dzierżaw gdzie nowoczesnego uwierzytelniania nie jest włączone, efektywnie pomijanie ograniczenia dzierżawy. Dla programu Outlook w systemie Windows klienci mogą wybrać ograniczenia tooimplement uniemożliwia użytkownikom dodawanie profilów tootheir kont niezatwierdzonych poczty. Na przykład, zobacz hello [Zapobiegaj dodawanie kont innych niż domyślne Exchange konta](http://gpsearch.azurewebsites.net/default.aspx?ref=1) ustawienie zasad grupy. Dla programu Outlook na platformach z systemem innym niż Windows, a dla usługi Skype dla firm na wszystkich platformach Pełna obsługa ograniczenia dzierżawy nie jest obecnie dostępna.

## <a name="testing"></a>Testowanie

Jeśli chcesz tootry ograniczenia dzierżawy przed rozpoczęciem implementacji dla całej organizacji, dostępne są dwie opcje: podejście oparta na hoście przy użyciu narzędzia, takiego jak Fiddler lub przemieszczanego Wdrażanie ustawień serwera proxy.

### <a name="fiddler-for-a-host-based-approach"></a>Fiddler podejścia oparta na hoście

Fiddler to bezpłatna debugowanie serwera proxy, który można toocapture używane i zmodyfikować ruchu HTTP/HTTPS, w tym Wstawianie nagłówków HTTP sieci web. tooconfigure Fiddler tootest ograniczenia dzierżawy, wykonaj hello następujące kroki:

1.  [Pobierz i zainstaluj Fiddler](http://www.telerik.com/fiddler).
2.  Skonfiguruj Fiddler toodecrypt ruchu HTTPS, na [Fiddler w dokumentacji pomocy](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS).
3.  Skonfiguruj Fiddler tooinsert hello *ograniczanie dostępu do dzierżawców* i *ograniczanie dostępu do kontekstu* nagłówki za pomocą reguł niestandardowych:
  1. W narzędziu Fiddler sieci Web debugera hello, wybierz hello **reguły** menu i wybierz **dostosować zasady...** Plik CustomRules hello tooopen.
  2. Dodaj następujące wiersze na początku hello hello hello *OnBeforeRequest* funkcji. Zastąp \<domena dzierżawy\> z domeną zarejestrowany w dzierżawie, na przykład contoso.onmicrosoft.com. Zastąp \<identyfikator katalogu\> z identyfikatorem Azure AD GUID Twojej dzierżawy.

  ```
  if (oSession.HostnameIs("login.microsoftonline.com") || oSession.HostnameIs("login.microsoft.com") || oSession.HostnameIs("login.windows.net")){      oSession.oRequest["Restrict-Access-To-Tenants"] = "<tenant domain>";      oSession.oRequest["Restrict-Access-Context"] = "<directory ID>";}
  ```

  Tooallow wielu dzierżawców, należy użyć nazwy dzierżawy przecinkami tooseparate hello. Na przykład:

  ```
  oSession.oRequest["Restrict-Access-To-Tenants"] = "contoso.onmicrosoft.com,fabrikam.onmicrosoft.com";
  ```

4. Zapisz i zamknij plik CustomRules hello.

Po skonfigurowaniu Fiddler, można przechwytywać ruch przez przejście toohello **pliku** menu i wybierając **przechwytywania ruchu**.

### <a name="staged-rollout-of-proxy-settings"></a>Wdrażanie przemieszczonych ustawienia serwera proxy

W zależności od możliwości hello infrastruktury serwera proxy może być stanie toostage hello wdrażania ustawień tooyour użytkowników. Poniżej przedstawiono kilka opcji wysokiego poziomu do rozważenia:

1.  Użyj uwierzytelniania PAC pliki toopoint testu użytkowników tooa testu infrastruktury usługi Serwer proxy, normalni użytkownicy nadal infrastruktury usługi Serwer proxy produkcji hello toouse.
2.  Niektóre serwery proxy mogą obsługiwać różne konfiguracje przy użyciu grup.

Zapoznaj się z dokumentacją serwera proxy tooyour szczegółowe informacje.

## <a name="next-steps"></a>Następne kroki

- Przeczytaj informacje o [aktualizacji usługi Office 365 nowoczesnego uwierzytelniania](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)

- Przejrzyj hello [zakresów adresów IP i URL usługi Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
