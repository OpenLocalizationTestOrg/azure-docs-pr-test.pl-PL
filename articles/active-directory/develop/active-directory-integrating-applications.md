---
title: "aaaIntegrating aplikacji za pomocą usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Szczegółowe informacje o sposobie tooadd, aktualizowanie lub usuwanie aplikacji w usłudze Azure Active Directory (Azure AD)."
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: mbaldwin
ms.assetid: ae637be5-0b71-4b1e-b1fe-b83df3eb4845
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: lenalepa
ms.custom: aaddev
ms.reviewer: luleon
ms.openlocfilehash: c6bf1123bb3a4d78b55c1c55558e684fb844e687
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-applications-with-azure-active-directory"></a>Integrowanie aplikacji z usługą Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Deweloperów w przedsiębiorstwach i dostawców oprogramowania — jako — usługa (SaaS), można opracować komercyjnych usług chmurowych lub aplikacje biznesowe, które można zintegrować z usługą Azure Active Directory (Azure AD) tooprovide bezpiecznego Zaloguj się w i autoryzacji dla ich usługi. toointegrate aplikacji lub usługi z usługą Azure AD, deweloper najpierw należy zarejestrować hello szczegóły aplikacji z usługą Azure AD za pomocą hello klasycznego portalu Azure.

W tym artykule opisano sposób tooadd, zaktualizować lub usunąć aplikację w usłudze Azure AD. Poznasz różne typy aplikacji, które można zintegrować z usługą Azure AD, jak hello tooconfigure tooaccess Twoje aplikacje inne zasoby, takie jak interfejsów API sieci web i inne.

toolearn więcej informacji na temat Witaj dwie usługi Azure AD obiekty reprezentujące zarejestrowanej aplikacji oraz hello relacji między nimi, zobacz [obiekty aplikacji i nazwy głównej usługi](active-directory-application-objects.md); więcej informacji na temat hello znakowania wytyczne toolearn możesz należy używać podczas tworzenia aplikacji w usłudze Azure Active Directory, zobacz [znakowanie wytyczne dotyczące zintegrowanych aplikacji](active-directory-branding-guidelines.md).

## <a name="adding-an-application"></a>Dodawanie aplikacji
Każda aplikacja, która chce toouse hello możliwości usługi Azure AD musi najpierw zostać zarejestrowana w dzierżawie usługi Azure AD. Ten proces rejestracji polega na zapewnieniu usługi Azure AD szczegóły aplikacji, na przykład adres URL hello, gdzie jest zlokalizowany, hello adres URL odpowiedzi toosend po uwierzytelnieniu użytkownika, hello identyfikator URI, który identyfikuje aplikacji hello i tak dalej.

Jeśli tworzysz aplikacji sieci web, wystarczy logowania toosupport dla użytkowników w usłudze Azure AD, można po prostu wykonaj poniższe instrukcje hello. Jeśli aplikacja wymaga poświadczeń lub uprawnienia tooaccess tooa interfejsu API sieci web lub wymaga tooallow użytkowników z innych usługi Azure AD dzierżawy tooaccess, zobacz [aktualizowanie aplikacji](#updating-an-application) toocontinue sekcji konfiguracji aplikacji.

### <a name="tooregister-a-new-application-in-hello-azure-portal"></a>tooregister nową aplikację w portalu Azure hello
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Wybierz dzierżawy usługi Azure AD, wybierając konto w hello prawym górnym rogu strony hello.
3. W okienku nawigacji po lewej stronie powitania, wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**i kliknij przycisk **Dodaj**.
4. Postępuj zgodnie z monitami hello i utworzyć nową aplikację. Jeśli chcesz szczegółowe przykłady dla aplikacji sieci web lub natywnych aplikacji, zapoznaj się naszego [quickstarts](active-directory-developers-guide.md).
  * W przypadku aplikacji sieci Web, podaj hello **adres URL logowania**, która jest hello podstawowy adres URL aplikacji, w którym użytkownicy mogą rejestrować w np. `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Dla natywnych aplikacji, podaj **identyfikator URI przekierowania**, które usługi Azure AD używa tooreturn odpowiedzi tokenu. Wprowadź aplikację tooyour określonej wartości. np.`http://MyFirstAADApp`
5. Po zakończeniu rejestracji usługi Azure AD przypisuje aplikacji identyfikatorem unikatowych klientów hello identyfikator aplikacji. Dodano aplikacji i nastąpi przekierowanie toohello strony Szybki Start dla aplikacji. W zależności od tego, czy aplikacja jest sieci web lub aplikacji natywnej, zobaczysz różne opcje dotyczące sposobu tooadd dodatkowe możliwości tooyour aplikacji. Po dodaniu aplikacji można rozpocząć aktualizowanie Twojej aplikacji tooenable użytkowników toosign w dostępu do interfejsów API sieci web w innych aplikacjach, lub skonfigurować wielodostępnych aplikacji (umożliwia tooaccess innych organizacjach aplikacji).

> [!NOTE]
> Domyślnie Rejestracja aplikacji hello nowo utworzona jest skonfigurowany tooallow użytkownikom toosign Twojego katalogu w tooyour aplikacji.
> 
> 

## <a name="updating-an-application"></a>Aktualizowanie aplikacji
Po zarejestrowaniu aplikacji z usługą Azure AD może wymagać aktualizacji toobe tooprovide dostępu tooweb interfejsów API, dostępne w innych organizacji i inne. W tej sekcji opisano różne sposoby, w których może być konieczne tooconfigure więcej aplikacji. Najpierw firma Microsoft rozpoczyna się od omówienie hello zgody Framework, która jest toounderstand ważne, jeśli tworzysz aplikacje zasobów/interfejsu API, które będą używane przez aplikacje klienckie utworzony przez deweloperów w Twojej organizacji lub inna organizacja.

Aby uzyskać więcej informacji na temat hello działania sposób uwierzytelniania w usłudze Azure AD, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](active-directory-authentication-scenarios.md).

### <a name="overview-of-hello-consent-framework"></a>Omówienie hello zgody framework
Framework zgody usługi Azure AD umożliwia łatwe toodevelop wielu dzierżawców w sieci web i interfejsów API zabezpieczone przez dzierżawę usługi Azure AD, inne niż hello jedną rejestracji powitania klienta aplikacji sieci web aplikacji klientami, które muszą tooaccess. Te interfejsy API sieci web obejmują hello interfejsu API programu Microsoft Graph (tooaccess usługi Azure Active Directory, Intune i usług w usłudze Office 365) i innych usług firmy Microsoft interfejsy API, oprócz tooyour właścicielem interfejsów API sieci web. Hello framework jest oparta na użytkownika lub administratora nadanie zgody tooan aplikacji, która żąda toobe zarejestrowanych w ich katalogu, które mogą dotyczyć uzyskiwanie dostępu do danych katalogu.

Na przykład jeśli w aplikacji klienta sieci web wymaga tooread kalendarza informacje o użytkowniku hello z usługi Office 365, ten użytkownik będzie wymagane tooconsent toohello klienta aplikacji. Po zgody, powitania klienta aplikacji można toocall stanie hello interfejsu API programu Graph firmy Microsoft w imieniu użytkownika hello i użyj hello informacji kalendarza, zgodnie z potrzebami. Witaj [interfejsu API programu Microsoft Graph](https://graph.microsoft.io) zapewnia toodata dostępu w usłudze Office 365 (na przykład kalendarzy i komunikaty z programu Exchange, witryn i list programu SharePoint, dokumentów z usługi OneDrive, notesy zadania planowania i skoroszytów w programie OneNote W programie Excel, itp.), a także użytkowników i grup z usługi Azure AD i innych obiektów danych z więcej usług chmurowych firmy Microsoft. 

framework zgody Hello jest zbudowany na OAuth 2.0 i jego różnych przepływów, takie jak kod autoryzacji poświadczenia grant i klienta umożliwiają, za pomocą publicznego lub poufnych klientów. Za pomocą protokołu OAuth 2.0, usługi Azure AD, ułatwia toobuild możliwych wiele różnych typów aplikacji klienckich, takich jak na telefon, typu tablet serwera lub aplikacji sieci web i uzyskanie dostępu toohello wymagane zasoby.

Aby uzyskać szczegółowe informacje o hello zgody framework, zobacz [OAuth 2.0 w usłudze Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx), [scenariusze uwierzytelniania dla usługi Azure AD](active-directory-authentication-scenarios.md)oraz informacje dotyczące pobierania autoryzowanego dostępu tooOffice 365 za pomocą Program Microsoft Graph, zobacz [uwierzytelniania aplikacji za pomocą programu Microsoft Graph](https://graph.microsoft.io/docs/authorization/auth_overview).

#### <a name="example-of-hello-consent-experience"></a>Przykład hello zgody środowisko
Hello następujące kroki opisano sposób działania hello zgody środowisko dla deweloperów aplikacji hello i użytkownika.

1. Na stronie konfiguracji aplikacji klienta sieci web w portalu Azure hello uprawnienia hello wymaganych przez aplikację przy użyciu menu hello w hello sekcji wymaganych uprawnień.
   
    ![Uprawnienia aplikacji tooother](./media/active-directory-integrating-applications/requiredpermissions.png)
2. Należy wziąć pod uwagę uprawnienia aplikacji zostały zaktualizowane, jest uruchomiona aplikacja hello, czy użytkownik jest o toouse dla powitania po raz pierwszy. Jeśli aplikacja hello nie uzyskał jeszcze dostępu lub odświeżania tokenu, hello aplikacji musi tooobtain punktu końcowego autoryzacji tooAzure toogo AD przez kod autoryzacji, które mogą być używane tooacquire nowe dostępu i token odświeżania.
3. Jeśli hello użytkownika nie jest już uwierzytelniony, zostanie poproszony toosign w tooAzure AD.
   
    ![Użytkownik lub administrator logowania tooAzure AD](./media/active-directory-integrating-applications/usersignin.png)
4. Po zalogowaniu się użytkownika hello, usługi Azure AD określi, jeśli użytkownik hello powinien toobe pokazano strony zgody. To jest na podstawie tego, czy użytkownika hello (lub jego organizację administratora) już udzielił zgody aplikacji hello. Jeśli zgody nie ma już udzielone, usługi Azure AD wyświetli monit o zgodę użytkownika hello i spowoduje wyświetlenie hello wymaganych uprawnień, musi on toofunction. Hello zestaw uprawnień, który jest wyświetlany w oknie dialogowym zgody hello są hello taki sam jak co zostało wybrane w hello delegowane uprawnienia w hello portalu Azure.
   
    ![Środowisko zgody użytkownika](./media/active-directory-integrating-applications/consent.png)
5. Po użytkownika hello przyznaje zgody, tooyour aplikacji, które można przeznaczonych tooacquire token dostępu i token odświeżania zostanie zwrócony kod autoryzacji. Aby uzyskać więcej informacji na temat tego przepływu, zobacz hello [sieci web sekcji tooweb interfejsu API aplikacji](active-directory-authentication-scenarios.md#web-application-to-web-api) sekcji [scenariusze uwierzytelniania dla usługi Azure AD](active-directory-authentication-scenarios.md).

6. Jako administrator może również zgoda tooan aplikacji uprawnień delegowanych w imieniu wszystkich użytkowników hello w dzierżawie. Dla każdego użytkownika w dzierżawie powitalnych uniemożliwi hello zgody w oknie dialogowym. Można to zrobić z hello [portalu Azure](https://portal.azure.com) ze strony aplikacji. Z hello **ustawienia** bloku dla aplikacji, kliknij przycisk **wymagane uprawnienia** i kliknij na powitania **udzielanie uprawnień** przycisku. 

    ![Udzielanie uprawnień o wyrażenie zgody jawnej administratora](./media/active-directory-integrating-applications/grantpermissions.png)
    
> [!NOTE]
> Udzielania zgody jawnej przy użyciu hello **udzielanie uprawnień** przycisk jest obecnie wymagane dla aplikacji jednej strony (SPA) za pomocą ADAL.js, żądaną hello tokena dostępu bez monit o zgodę, który zakończy się niepowodzeniem, jeśli nie jest zgoda już przydzielone.   

### <a name="configuring-a-client-application-tooaccess-web-apis"></a>Konfigurowanie klienta aplikacji tooaccess interfejsów API sieci web
Aby sieci web/poufne klienta aplikacji toobe stanie tooparticipate przepływu grant autoryzacji, który wymaga uwierzytelniania (i Uzyskaj token dostępu) jego ustanawiania bezpiecznych poświadczeń. Witaj domyślną metodą uwierzytelniania obsługiwanych przez hello Azure portal jest identyfikator klienta i klucz symetryczny. W tej sekcji opisano hello konfiguracji kroki wymagane tooprovide hello tajny klucz poświadczeń klienta.

Ponadto przed klient może dostępu interfejs API sieci web udostępniany przez aplikację zasobów (ie: Microsoft Graph API), hello zgody zapewnią powitania klienta uzyskuje Udziel uprawnienia hello uprawnienia wymagane, na podstawie hello żądanie. Domyślnie wszystkie aplikacje można wybrać uprawnienia z usługi Azure Active Directory (interfejs API programu Graph) i interfejs API zarządzania usługami Azure, z uprawnieniem "Włącz logowania i profilu użytkownika odczytu" hello Azure AD już wybrane domyślnie. Jeśli aplikacja kliencka jest rejestrowana w dzierżawie usługi Azure AD usługi Office 365, interfejsów API sieci web i uprawnienia do usługi Exchange Online i SharePoint będzie także dostępna do wyboru. Możesz wybrać z [dwa typy uprawnień](active-directory-dev-glossary.md#permissions) w hello menu rozwijanych potrzeby dalej toohello sieci web interfejsu API:

* Uprawnienia aplikacji: Aplikacja kliencka musi interfejsu API sieci web hello tooaccess bezpośrednio jako samego (bez kontekstu użytkownika). Ten typ uprawnień wymaga zgody administratora i nie jest również dostępna dla aplikacji klienckich natywnego.
* Delegowane uprawnienia: Aplikacja kliencka musi interfejsu API sieci web hello tooaccess jako hello zalogowanego użytkownika, ale dostęp ograniczony przez hello zaznaczone uprawnienia. Ten typ uprawnień może zostać przydzielony przez użytkownika, chyba że uprawnienie hello jest skonfigurowany jako wymaganie zgody administratora. 

> [!NOTE]
> Dodawanie aplikacji tooan delegowane uprawnienia nie automatycznie udziela zgody toohello użytkowników w ramach dzierżawy hello, tak jak w hello klasycznego portalu Azure. Witaj użytkowników musi nadal ręcznie wyrazić zgodę dla hello dodane delegowane uprawnienia w czasie wykonywania, chyba że hello administrator kliknie hello **udzielanie uprawnień** przycisk od hello **wymagane uprawnienia** sekcji strony aplikacji hello hello portalu Azure. 

#### <a name="tooadd-credentials-or-permissions-tooaccess-web-apis"></a>poświadczenia tooadd lub tooaccess uprawnienia interfejsów API sieci web
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Wybierz dzierżawy usługi Azure AD, wybierając konto w hello prawym górnym rogu strony hello.
3. W menu u góry hello, wybierz polecenie **usługi Azure Active Directory**, kliknij przycisk **rejestracji aplikacji**, a następnie kliknij przycisk aplikacji hello ma tooconfigure. To spowoduje przejście strony Szybki Start toohello aplikacji, jak również otwarcie bloku ustawień aplikacji hello hello.
4. tooadd klucz tajny dla aplikacji sieci web poświadczenia, kliknij sekcję "Klucze" hello w bloku ustawienia hello.  
   
   * Dodaj opis klucza i wybierz opcję 1 lub 2 lata, okres. 
   * Witaj prawej kolumna będzie zawierać wartości klucza hello, po zapisaniu zmian konfiguracji hello. Toocome się wstecz sekcji toothis i skopiuj go po naciśnięciu przycisku Zapisz, dlatego trzeba go używać w aplikacji klienta podczas uwierzytelniania w czasie wykonywania.
5. uprawnienia tooadd tooaccess zasobów interfejsy API z klienta, kliknij sekcję "Wymagane uprawnienia" hello w bloku ustawienia hello. 
   
   * Po pierwsze kliknij przycisk "Dodaj" hello.
   * Kliknij przycisk "Wybierz interfejsu API" tooselect hello typów zasobów, które mają toopick z.
   * Przeglądać listę dostępnych interfejsach API hello, lub użyj tooselect pole wyszukiwania hello z aplikacji dostępnych zasobów hello w katalogu, które udostępniają interfejs API sieci web. Kliknij zasób hello są zainteresowani, następnie kliknij przycisk **wybierz**.
   * Po wybraniu można przenieść toohello **wybierz uprawnienia** menu, w którym można wybrać hello "uprawnienia aplikacji" i "Delegowane uprawnienia" dla aplikacji.
   
6. Po zakończeniu kliknij przycisk hello **gotowe** przycisku.

> [!NOTE]
> Kliknięcie przycisku hello **gotowe** przycisk również automatycznie ustawia hello uprawnień dla aplikacji w katalogu na podstawie hello uprawnień tooother aplikacji, które można skonfigurować.  Te uprawnienia aplikacji można wyświetlić, sprawdzając aplikacji hello **ustawienia** bloku.
> 
> 

### <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Konfigurowanie zasobów aplikacji tooexpose interfejsów API sieci web
Mogą tworzyć interfejs API sieci web i stał się dostępny tooclient aplikacji przez Udostępnianie dostępu [zakresy](active-directory-dev-glossary.md#scopes) i [ról](active-directory-dev-glossary.md#roles). Interfejs API sieci web poprawnie skonfigurowana staje się dostępny, podobnie jak inne Microsoft interfejsów API sieci web, w tym hello interfejsu API programu Graph hello i hello interfejsami API usługi Office 365. Zakresy dostępu i ról są dostępne za pośrednictwem sieci [manifest aplikacji](active-directory-dev-glossary.md#application-manifest), czyli pliku JSON, który reprezentuje konfigurację tożsamości aplikacji.  

powitania po sekcji opisano sposób dostępu tooexpose zakresów, modyfikując manifest aplikacji hello zasobów.

#### <a name="adding-access-scopes-tooyour-resource-application"></a>Dodawanie aplikacji zasobów tooyour zakresy dostępu
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Wybierz dzierżawy usługi Azure AD, wybierając konto w hello prawym górnym rogu strony hello.
3. W menu u góry hello, wybierz polecenie **usługi Azure Active Directory**, kliknij przycisk **rejestracji aplikacji**, a następnie kliknij przycisk aplikacji hello ma tooconfigure. To spowoduje przejście strony Szybki Start toohello aplikacji, jak również otwarcie bloku ustawień aplikacji hello hello.
4. Kliknij przycisk **manifestu** z hello aplikacji tooopen hello wbudowanego manifestu Edytor stron. 
5. Zastąp węzeł "oauth2Permissions" hello po fragment kodu JSON. Ta Wstawka kodu jest przykładem jak tooexpose zakres znana jako "personifikacji użytkownika", dzięki czemu aplikacja kliencka toogive właściciela zasobu typu delegowanego dostępu tooa zasobów. Upewnij się, zmień tekst hello i wartości dla swojej aplikacji:
   
        "oauth2Permissions": [
        {
            "adminConsentDescription": "Allow hello application full access toohello Todo List service on behalf of hello signed-in     user",
            "adminConsentDisplayName": "Have full access toohello Todo List service",
            "id": "b69ee3c9-c40d-4f2a-ac80-961cd1534e40",
            "isEnabled": true,
            "type": "User",
            "userConsentDescription": "Allow hello application full access toohello todo service on your behalf",
            "userConsentDisplayName": "Have full access toohello todo service",
            "value": "user_impersonation"
            }
        ],
   
    wartość identyfikatora Hello musi być nowe generowanym identyfikatorze GUID, który utworzono przy użyciu [narzędzia do generowania identyfikatora GUID](https://msdn.microsoft.com/library/ms241442%28v=vs.80%29.aspx) lub programowo. Reprezentuje unikatowy identyfikator uprawnienie hello jest udostępniana przez interfejs API sieci web hello. Gdy klient jest skonfigurowany prawidłowo toorequest dostępu tooyour interfejsu API sieci web i wywołania interfejsu API sieci web Witaj, przedstawi token OAuth 2.0 JWT, który ma hello (scp) oświadczenie set toohello wartość zakresu powyżej, w tym przypadku jest user_impersonation.
   
   > [!NOTE]
   > Pozwala udostępnić dodatkowe zakresy, później niezbędne. Należy wziąć pod uwagę, że interfejs API sieci web może udostępniać wielu zakresów skojarzone z wieloma różnymi funkcjami. Teraz można kontrolować dostęp toohello interfejsu API sieci web przy użyciu hello zakresu (scp) oświadczenia hello Odebrano tokenu OAuth 2.0 JWT.
   > 
   > 
6. Kliknij przycisk **zapisać** toosave hello manifestu. Sieci web, które interfejs API jest teraz skonfigurowane toobe używane przez inne aplikacje w katalogu.

#### <a name="tooverify-hello-web-api-is-exposed-tooother-applications-in-your-directory"></a>tooverify interfejsu API sieci web hello jest narażonych tooother aplikacje w katalogu
1. W menu u góry hello, kliknij polecenie **rejestracji aplikacji**, wybierz pozycję hello wymaganą aplikację kliencką mają tooconfigure dostępu toohello — interfejs API sieci web i przejdź do bloku ustawienia toohello.
2. Z hello **wymagane uprawnienia** wybierz hello interfejsu API sieci web, który właśnie widoczne uprawnienie. Z menu rozwijanego delegowane uprawnienia hello wybierz nowe uprawnienie hello.

![Lista czynności do wykonania uprawnienia są wyświetlane.](./media/active-directory-integrating-applications/todolistpermissions.png)

#### <a name="more-on-hello-application-manifest"></a>Więcej informacji na temat manifest aplikacji hello
manifest aplikacji Hello faktycznie służy jako mechanizm aktualizacji jednostki aplikacji hello, który definiuje wszystkie atrybuty konfiguracji tożsamość aplikacji usługi Azure AD, w tym hello zakresy dostępu interfejsu API, które rozmawialiśmy. Aby uzyskać więcej informacji na powitania Jednostka aplikacji, zobacz hello [dokumentacji jednostek aplikacji interfejsu API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity). W ramach tego można znaleźć informacje pełną dokumentację na uprawnienia jednostek aplikacji hello toospecify członków używany do interfejsu API:  

* element członkowski appRoles Hello, który jest kolekcją z [roli aplikacji](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type) jednostek, które mogą być używane toodefine hello **uprawnienia aplikacji** dla interfejsu API sieci web  
* element członkowski oauth2Permissions Hello, który jest kolekcją z [OAuth2Permission](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type) jednostek, które mogą być używane toodefine hello **delegowane uprawnienia** dla interfejsu API sieci web

Aby uzyskać więcej informacji na temat aplikacji manifestu pojęcia ogólnie rzecz biorąc, można znaleźć zbyt[manifest aplikacji usługi Azure Active Directory hello opis](active-directory-application-manifest.md).

### <a name="accessing-hello-azure-ad-graph-and-office-365-via-microsoft-graph-apis"></a>Uzyskiwanie dostępu do hello Azure AD Graph i usługi Office 365 za pomocą programu Microsoft Graph API  
Jak wspomniano wcześniej, oprócz tooexposing/uzyskiwanie dostępu do interfejsów API aplikacji zasobów należy zaktualizować Twojego tooaccess aplikacji klienta interfejsach API udostępnianych przez zasoby firmy Microsoft.  Witaj Microsoft interfejsu API programu Graph, który jest nazywany "Microsoft Graph" hello liście uprawnień tooother aplikacji, jest dostępna lub wszystkie aplikacje, które są zarejestrowane w usłudze Azure AD. W przypadku rejestracji aplikacji klienckiej w dzierżawie usługi Azure AD, które zostało udostępnione przez usługę Office 365, można również przejść, wszystkie uprawnienia hello udostępnianych przez hello toovarious Microsoft Graph API usługi Office 365, zasobów.

Szczegółowe omówienie na zakresy dostępu udostępnianych przez interfejs API programu Graph firmy Microsoft, zobacz hello [zakresy uprawnień | Pojęcia dotyczące interfejsu API programu Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes) artykułu.

> [!NOTE]
> Ze względu na bieżące ograniczenia tooa aplikacje klienckie natywnego można wywołać tylko w hello Azure AD Graph API użycie uprawnienia "Dostęp do katalogu organizacji" hello.  To ograniczenie nie ma zastosowania dla aplikacji sieci web.
> 
> 

### <a name="configuring-multi-tenant-applications"></a>Konfigurowanie aplikacji z wieloma dzierżawcami
Podczas dodawania aplikacji tooAzure AD, możesz toobe Twojej aplikacji, dostępny tylko dla użytkowników w organizacji. Alternatywnie możesz toobe Twojej aplikacji, dostęp użytkownicy w organizacjach zewnętrznych. Typy dwóch aplikacji są nazywane pojedynczej dzierżawy i aplikacje wielodostępne. Można zmodyfikować konfigurację hello toomake aplikacji pojedynczej dzierżawy go aplikacji wielodostępne w tej sekcji omówiono poniżej.

Jest ważne toonote hello różnice między pojedynczej dzierżawy i wielodostępnych aplikacji:  

* Stosowanie pojedynczej dzierżawy jest przeznaczony do użytku w jednej z organizacji. Są one zazwyczaj biznesowych z aplikacji (LoB), zapisane przez dewelopera przedsiębiorstwa. Stosowanie pojedynczej dzierżawy musi tylko toobe dostępne dla użytkowników w jednym katalogu, i w związku z tym tylko musi toobe udostępniane w jednym katalogu.
* Aplikacja wielodostępne, przeznaczone do użytku w wielu organizacjach. Są one oprogramowanie jako usługa (SaaS) aplikacji sieci web zwykle napisane przez niezależnego dostawcy oprogramowania (ISV). Aplikacje wielodostępne muszą toobe udostępniane w każdym katalogu gdzie będą one używane, co wymaga tooregister zgody użytkownika lub administratora ich obsługiwane za pośrednictwem framework zgody hello Azure AD. Należy zauważyć, że wszystkie aplikacje klienckie natywnego wielodostępne domyślnie, które są instalowane na urządzeniu właściciel zasobu hello. Zobacz hello omówienie hello zgody Framework sekcji powyżej, aby uzyskać więcej informacji na powitania zgody framework.

#### <a name="enabling-external-users-toogrant-your-application-access-tootheir-resources"></a>Włączanie toogrant użytkowników zewnętrznych zasobów tootheir dostępu do aplikacji
Jeśli piszesz aplikację mają toomake dostępne tooyour klientów lub partnerów spoza organizacji, konieczne będzie definicji aplikacji hello tooupdate w hello portalu Azure.

> [!NOTE]
> Podczas włączania wielu dzierżawców, należy się upewnić, że identyfikator URI aplikacji aplikacji należy w zweryfikowanej domeny. Ponadto hello zwrotny adres URL musi rozpoczynać się od https://. Aby uzyskać więcej informacji, zobacz [obiekty aplikacji i nazwy głównej usługi](active-directory-application-objects.md).
> 
> 

tooenable aplikacji tooyour dostępu dla użytkowników zewnętrznych: 

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Wybierz dzierżawy usługi Azure AD, wybierając konto w hello prawym górnym rogu strony hello.
3. W menu u góry hello, wybierz polecenie **usługi Azure Active Directory**, kliknij przycisk **rejestracji aplikacji**, a następnie kliknij przycisk aplikacji hello ma tooconfigure. To spowoduje przejście strony Szybki Start toohello aplikacji, jak również otwarcie bloku ustawień aplikacji hello hello.
4. W bloku ustawienia hello, kliknij **właściwości** i przerzucania hello **dzierżawcza Multi** przełącznika zbyt**tak**.

Po dokonaniu hello zmienić powyżej, użytkowników i administratorów z innych organizacji będą mogli toogrant katalogu tootheir dostęp do aplikacji i innych danych.

#### <a name="triggering-hello-azure-ad-consent-framework-at-runtime"></a>Wyzwolenie framework zgody hello Azure AD w czasie wykonywania
toouse hello zgody framework, aplikacje klienckie wielodostępne musi żądać autoryzacji przy użyciu protokołu OAuth 2.0. [Przykłady kodu](https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multi-tenant) są dostępne tooshow jak aplikacji sieci web, aplikacji natywnej lub autoryzacji żądania aplikacji serwera/demon kodów i dostęp do tokenów toocall interfejsów API sieci web.

Aplikacja sieci web mogą także oferować rejestracji środowisko dla użytkowników. Jeśli oferujesz środowisko tworzenia konta, oczekuje się, ten użytkownik hello będzie, kliknij na rejestracji przycisk czy toohello przeglądarki hello przekierowania usługi Azure AD OAuth2.0 autoryzacji punktu końcowego lub punkt końcowy protokołu OpenID Connect informacje o użytkowniku. Te punkty końcowe umożliwiają hello aplikacji tooget informacji o hello nowego użytkownika sprawdzając hello żądaniu. Po rejestracji fazy hello hello użytkownika zostanie wyświetlone zgody monitu o podobnych toohello pokazano powyżej w hello omówienie hello sekcji Framework zgodę.

Alternatywnie aplikacji sieci web mogą także oferować środowisko, które pozwala administratorom zbyt "Zarejestruj mojej firmy". To środowisko będzie również przekierować toohello użytkownika hello Azure AD OAuth 2.0 punktu końcowego autoryzacji. W takim przypadku jednak przekazać wiersz = admin_consent toohello parametr autoryzacji punktu końcowego tooforce hello administratora zgody doświadczenia, gdy hello administrator będzie udzielić zgody w imieniu swojej organizacji. Tylko użytkownik, który dokonuje uwierzytelnień przy użyciu konta należącego do roli administratora globalnego toohello zapewniają zgody; inne spowoduje wystąpienie błędu. Na pomyślne zgody hello odpowiedź będzie zawierać admin_consent = true. Gdy realizowanie tokenu dostępu, otrzymasz również żądaniu, który dostarcza informacji o organizacji Witaj i administrator hello, która zarejestrowała się w usłudze aplikacji.

### <a name="enabling-oauth-20-implicit-grant-for-single-page-applications"></a>Włączanie OAuth 2.0 niejawne Przyznaj dla jednej strony aplikacji
Jednej strony aplikacji (źródła) są zwykle struktury z JavaScript ciężki fronton, który jest uruchamiany w przeglądarce hello wywołuje tooperform zaplecza interfejsu API sieci web aplikacji hello jej logiki biznesowej. Dla źródła hostowanych w usłudze Azure AD, OAuth 2.0 niejawne Przyznaj tooauthenticate hello użytkownika za pomocą usługi Azure AD i uzyskania tokenu można użyć toosecure z aplikacji hello JavaScript klienta tooits ponownie wywołuje interfejs API sieci web zakończenia. Po udzieleniu zgody użytkownika hello tego samego protokołu uwierzytelniania mogą być używane tooobtain tokenów toosecure wywołań między powitania klienta i innych zasobów interfejsu API sieci web skonfigurowana dla aplikacji hello. Zobacz toolearn więcej informacji na temat udzielania autoryzacji niejawne hello i pomoc można zdecydować, czy odpowiednie dla danego scenariusza aplikacji [hello opis OAuth2 niejawne Przyznaj przepływu w usłudze Azure Active Directory ](active-directory-dev-understanding-oauth2-implicit-grant.md).

Domyślnie niejawne Przyznaj OAuth 2.0 jest wyłączone dla aplikacji. Można włączyć protokołu OAuth 2.0 niejawne Przyznaj aplikacji hello ustawienie `oauth2AllowImplicitFlow` wartości w jego [manifest aplikacji](active-directory-application-manifest.md), czyli pliku JSON, który reprezentuje konfigurację tożsamości aplikacji.

#### <a name="tooenable-oauth-20-implicit-grant"></a>niejawne Przyznaj tooenable OAuth 2.0
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Wybierz dzierżawy usługi Azure AD, wybierając konto w hello prawym górnym rogu strony hello.
3. W menu u góry hello, wybierz polecenie **usługi Azure Active Directory**, kliknij przycisk **rejestracji aplikacji**, a następnie kliknij przycisk aplikacji hello ma tooconfigure. To spowoduje przejście strony Szybki Start toohello aplikacji, jak również otwarcie bloku ustawień aplikacji hello hello.
4. Ze strony aplikacji hello, kliknij przycisk **manifestu** tooopen hello wbudowanego manifestu edytora.
   Zlokalizuj i ustaw wartość "oauth2AllowImplicitFlow" hello zbyt "true". Domyślnie jest "false".
   
    `"oauth2AllowImplicitFlow": true,`
5. Zapisz hello zaktualizować manifestu. Po zapisaniu sieci web, które interfejs API jest teraz skonfigurowane toouse OAuth 2.0 niejawne Przyznaj tooauthenticate użytkowników.


## <a name="removing-an-application"></a>Usuwanie aplikacji
W tej sekcji opisano, jak tooremove aplikacji za pomocą usługi Azure AD dzierżawy.

### <a name="removing-an-application-authored-by-your-organization"></a>Usuwanie aplikacji przypisany przez organizację
Są to aplikacje hello wyświetlana w obszarze filtru "Aplikacje Moja firma jest właścicielem" hello na głównej stronie "Aplikacji" hello dla dzierżawy usługi Azure AD. Pod względem technicznym te są aplikacje, które są rejestrowane ręcznie za pośrednictwem hello klasycznego portalu Azure lub programistycznie za pomocą programu PowerShell lub hello interfejsu API programu Graph. W szczególności są one reprezentowane przez zarówno aplikacji i nazwy głównej usługi obiekt w dzierżawie. Zobacz [obiekty aplikacji i nazwy głównej usługi](active-directory-application-objects.md) Aby uzyskać więcej informacji.

#### <a name="tooremove-a-single-tenant-application-from-your-directory"></a>tooremove pojedynczej dzierżawy aplikacji z katalogu
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Wybierz dzierżawy usługi Azure AD, wybierając konto w hello prawym górnym rogu strony hello.
3. W menu u góry hello, wybierz polecenie **usługi Azure Active Directory**, kliknij przycisk **rejestracji aplikacji**, a następnie kliknij przycisk aplikacji hello ma tooconfigure. To spowoduje przejście strony Szybki Start toohello aplikacji, jak również otwarcie bloku ustawień aplikacji hello hello.
4. Ze strony aplikacji hello, kliknij przycisk **usunąć**.
5. Kliknij przycisk **tak** w hello komunikat potwierdzenia.

#### <a name="tooremove-a-multi-tenant-application-from-your-directory"></a>tooremove wielodostępnych aplikacji z katalogu
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Wybierz dzierżawy usługi Azure AD, wybierając konto w hello prawym górnym rogu strony hello.
3. W menu u góry hello, wybierz polecenie **usługi Azure Active Directory**, kliknij przycisk **rejestracji aplikacji**, a następnie kliknij przycisk aplikacji hello ma tooconfigure. To spowoduje przejście strony Szybki Start toohello aplikacji, jak również otwarcie bloku ustawień aplikacji hello hello.
4. W bloku ustawienia hello, wybierz **właściwości** i przerzucania hello **dzierżawcza Multi** przełącznika zbyt**nr**. Spowoduje to przekonwertowanie pojedynczej aplikacji dzierżawy w toobe, ale aplikacji hello nadal zostanie umieszczony w organizacji, którzy już zgodził tooit.
5. Polecenie hello **usunąć** przycisk ze strony aplikacji hello.
6. Kliknij przycisk **tak** w hello komunikat potwierdzenia.

### <a name="removing-a-multi-tenant-application-authorized-by-another-organization"></a>Usuwanie aplikacji wielodostępnych, autoryzowany w innej organizacji
Są to podzbiór aplikacji hello, wyświetlanych w obszarze filtru "Korzysta z aplikacji firmy" hello, na stronie głównej "aplikacji" hello dla dzierżawy usługi Azure AD, w szczególności hello te, które nie są wymienione pod listą "Aplikacje Moja firma jest właścicielem" hello. Aplikacje wielodostępne zarejestrowane podczas procesu zgody hello są pod względem technicznym. W szczególności są one reprezentowane przez tylko obiekt nazwy głównej usługi w dzierżawie. Zobacz [obiekty aplikacji i nazwy głównej usługi](active-directory-application-objects.md) Aby uzyskać więcej informacji.

W celu tooremove katalogu tooyour dostępu aplikacji wielodostępne (po udzielenia zgody), administrator firmy hello musi mieć dostęp tooremove subskrypcji platformy Azure za pośrednictwem hello portalu Azure. Alternatywnie administrator firmy hello użyć hello [poleceń cmdlet programu Azure AD PowerShell](http://go.microsoft.com/fwlink/?LinkId=294151) tooremove dostępu.

## <a name="next-steps"></a>Następne kroki
* Zobacz hello [znakowanie wytyczne dotyczące zintegrowanych aplikacji](active-directory-branding-guidelines.md) dotyczące visual wskazówki dotyczące aplikacji.
* Więcej szczegółów na powitania relacji między obiektów aplikacji i nazwę główną usługi dla aplikacji, zobacz [obiekty aplikacji i nazwy głównej usługi](active-directory-application-objects.md).
* Zobacz toolearn więcej informacji na temat hello roli hello aplikacji manifestu odtwarza, [manifest aplikacji usługi Azure Active Directory hello opis](active-directory-application-manifest.md)
* Zobacz hello [słownik dewelopera usługi Azure AD](active-directory-dev-glossary.md) definicji niektórych koncepcje dla deweloperów usługi Azure Active Directory (AD) core hello.
* Odwiedź hello [przewodnik dewelopera usługi Active Directory](active-directory-developers-guide.md) przegląd wszystkich deweloperów związane z zawartością.

