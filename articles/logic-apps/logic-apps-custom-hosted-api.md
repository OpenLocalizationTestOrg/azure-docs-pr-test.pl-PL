---
title: "aaaDeploy, wywołaj i uwierzytelniania sieci web API i interfejsów API REST dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Wdrażanie, uwierzytelniania i wywołania interfejsów API i interfejsów API REST w sieci web w przepływach pracy dla systemu integracji z usługą Azure Logic Apps"
keywords: "interfejsy API, interfejsy API REST, łączniki, przepływy pracy, integracji systemu w sieci Web, uwierzytelniania"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>Wdrożenia, wywołaj i uwierzytelniania niestandardowych interfejsów API łączników dla usługi logic apps

Po [Tworzenie niestandardowych interfejsów API](./logic-apps-create-api-app.md) zawierających akcji lub wyzwalaczy toouse logiki aplikacji przepływy pracy, swoje interfejsy API należy wdrożyć przed wywołaniem je. I chociaż jakiegokolwiek interfejsu API można wywołać z aplikacji logiki, aby hello najlepsze wyniki, Dodaj [Swagger metadanych](http://swagger.io/specification/) opisujący Twój interfejs API operacji i parametry. Ten plik struktury Swagger pomaga interfejsu API działa lepiej i łatwo zintegrować z usługą logic apps.

Można wdrożyć swoje interfejsy API jako [sieci web apps](../app-service-web/app-service-web-overview.md), ale warto wdrożyć swoje interfejsy API jako [aplikacje interfejsu API](../app-service-api/app-service-api-apps-why-best-platform.md), które mogą ułatwić zadania podczas kompilacji, hosta i korzystanie z interfejsów API w chmurze hello i lokalnie. Nie można znaleźć toochange dowolny kod swoje interfejsy API — wystarczy go wdrożyć aplikację interfejsu API tooan kodu. Swoje interfejsy API mogą być hostowane na [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md), platformy jako — usługa (PaaS) oferta zapewnia sposoby najlepsze najprostszym i najbardziej skalowalny hello do obsługi interfejsu API.

wywołania tooauthenticate z tooyour aplikacje logiki interfejsów API, można ustawić usługę Azure Active Directory w hello portalu Azure dzięki czemu nie trzeba tooupdate kodu. Lub może wymagać i wymusić uwierzytelnianie za pomocą kodu Twój interfejs API.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>Wdrażanie aplikacji sieci web lub aplikacji interfejsu API interfejsu API

Przed wywołaniem niestandardowego interfejsu API z aplikacji logiki, należy wdrożyć jako aplikacji sieci web lub tooAzure aplikacji interfejsu API usługi aplikacji interfejsu API. Ponadto toomake dokumentu Swagger mógłby odczytać hello projektanta aplikacji logiki, ustaw właściwości definicji hello interfejsu API i Włącz [współużytkowanie zasobów między źródłami (CORS) do udostępniania](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) dla aplikacji sieci web lub aplikacji interfejsu API.

1. W portalu Azure hello wybierz aplikację sieci web lub aplikacji interfejsu API.

2. W bloku hello, który zostanie otwarty, w obszarze **interfejsu API**, wybierz **definicji interfejsu API**. Zestaw hello **lokalizacji definicji interfejsu API** toohello adres URL pliku swagger.json.

   Zwykle adres URL hello pojawia się w następującym formacie:`https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![Plik tooSwagger łącza do niestandardowego interfejsu API](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. W obszarze **interfejsu API**, wybierz **CORS**. Ustaw hello zasad CORS dla **dozwolone źródła** za**"*"** (Zezwalaj na wszystkie).

   Ustawienie to pozwala żądania przy użyciu projektanta aplikacji logiki.

   ![Zezwala na żądania z projektanta aplikacji logiki tooyour niestandardowego interfejsu API](media/logic-apps-custom-hosted-api/custom-api-cors.png)

Aby uzyskać więcej informacji zobacz następujące artykuły:

* [Dodaj metadane programu Swagger dla interfejsów API sieci web ASP.NET](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [Wdrażanie programu ASP.NET web API tooAzure usługi aplikacji](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Wywoływanie niestandardowego interfejsu API z logiki przepływów pracy aplikacji

Po skonfigurowaniu właściwości definicji hello interfejsu API i mechanizmu CORS, niestandardowego interfejsu API wyzwalacze i akcje powinien być możliwy do tooinclude w przepływie pracy aplikacji logiki. 

*  tooview hello witryn sieci Web programu Swagger URL, możesz wyszukać subskrypcji witryny sieci Web w hello projektanta aplikacji logiki.

*  Dostępne akcje tooview i dane wejściowe, wskazując dokumentu Swagger, użyj hello [HTTP + Swagger akcji](../connectors/connectors-native-http-swagger.md).

*  toocall jakiegokolwiek interfejsu API, łącznie z interfejsów API, które nie mają lub udostępnianie dokumentu Swagger, zawsze można utworzyć żądania z hello [akcji HTTP](../connectors/connectors-native-http.md).

## <a name="authenticate-calls-tooyour-custom-api"></a>Niestandardowy interfejs API tooyour wywołania uwierzytelniania

Możesz zabezpieczyć wywołania tooyour niestandardowego interfejsu API w następujący sposób:

* [Nie zmian w kodzie](#no-code): interfejs API ochrony [usługi Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) za pośrednictwem hello portalu Azure, dlatego nie masz tooupdate kodu lub ponownego wdrażania interfejsu API.

  > [!NOTE]
  > Domyślnie hello uwierzytelniania usługi Azure AD, który można włączyć w portalu Azure hello nie zapewnia precyzyjną autoryzacji. Na przykład to uwierzytelnianie blokuje toojust Twojego interfejsu API określonego dzierżawy, nie tooa określonego użytkownika lub aplikacji. 

* [Zaktualizuj kod Twój interfejs API](#update-code): ochrona interfejsu API przez wymuszenie [uwierzytelnianie certyfikatu](#certificate), [uwierzytelnianie podstawowe](#basic), lub [uwierzytelniania usługi Azure AD](#azure-ad-code) za pomocą kodu.

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a>Uwierzytelniania interfejsu API tooyour wywołania bez zmiany kodu

Poniżej przedstawiono ogólne kroki hello tej metody:

1. Utwórz dwa [tożsamości aplikacji usługi Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): jeden dla aplikacji logiki i jeden dla aplikacji sieci web (lub aplikacji interfejsu API).

2. tooauthenticate tooyour wywołań interfejsu API, Użyj poświadczeń hello (identyfikator klienta i klucz tajny) dla hello [nazwy głównej usługi](../app-service-api/app-service-api-dotnet-service-principal-auth.md) która jest skojarzona z hello tożsamość aplikacji usługi Azure AD dla aplikacji logiki.

3. Dołącz aplikacji hello identyfikatorów definicję aplikacji logiki.

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>Część 1: Tworzenie aplikacji logiki tożsamość aplikacji usługi Azure AD

Twoja aplikacja logiki korzysta z tego tooauthenticate tożsamość aplikacji usługi Azure AD w usłudze Azure AD. Masz tylko tooset się tej tożsamości jeden raz dla katalogu. Na przykład można wybrać toouse hello tej samej tożsamości dla wszystkich aplikacji logiki, mimo że można utworzyć unikatowych tożsamości dla każdej aplikacji logiki. Możesz skonfigurować te tożsamości w hello portalu Azure, [klasycznego portalu Azure](#app-identity-logic-classic), lub użyj [PowerShell](#powershell).

**Utwórz tożsamość aplikacji hello aplikacji logiki w hello portalu Azure**

1. W hello [portalu Azure](https://portal.azure.com "https://portal.azure.com"), wybierz **usługi Azure Active Directory**. 

2. Upewnij się, że jesteś w hello tym samym katalogu co aplikację sieci web lub aplikacji interfejsu API.

   > [!TIP]
   > katalogi tooswitch kliknij profilu i wybierz inny katalog. Lub wybierz **omówienie** > **katalogu przełącznika**.

3. Menu hello katalogu w obszarze **Zarządzaj**, wybierz **rejestracji aplikacji** > **nowej rejestracji aplikacji**.

   > [!TIP]
   > Domyślnie listy rejestracji aplikacji hello zawiera wszystkich rejestracji aplikacji w katalogu. Wybierz tylko aplikacji rejestracji, toohello pola wyszukiwania i tooview **Moje aplikacje**. 

   ![Tworzenie nowej rejestracji aplikacji](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. Nadaj nazwę tożsamości aplikacji, pozostaw **typu aplikacji** ustawić także**aplikacji sieci Web / interfejsu API**, podaj unikatowy ciąg w formacie domeny dla **adres URL logowania**i wybierz polecenie  **Utwórz**.

   ![Podaj nazwę i logowania jednokrotnego adres URL dla tożsamości aplikacji](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   tożsamość aplikacji Hello utworzonej dla aplikacji logiki teraz pojawia się na liście rejestracji aplikacji hello.

   ![Tożsamość aplikacji dla aplikacji logiki](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. Na liście rejestracji aplikacji hello wybierz nowy identyfikator aplikacji. Skopiuj i Zapisz hello **identyfikator aplikacji** toouse jako Witaj "identyfikator klienta" aplikacji logiki w część 3.

   ![Skopiuj i Zapisz identyfikator aplikacji dla aplikacji logiki](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. Jeśli ustawienia tożsamość aplikacji nie są widoczne, wybierz **ustawienia** lub **wszystkie ustawienia**.

7. W obszarze **dostępu do interfejsu API**, wybierz **klucze**. W obszarze **opis**, podaj nazwę klucza. W obszarze **Expires**, wybierz czas trwania dla klucza.

   Witaj klucz, który tworzysz działa jako tożsamość aplikacji hello "tajny" lub hasła do aplikacji logiki.

   ![Utwórz klucz tożsamości aplikacji logiki](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. Na pasku narzędzi hello, wybierz **zapisać**. W obszarze **wartość**, klucz zostanie wyświetlone. 
**Upewnij się, że toocopy i zapisać klucz** do późniejszego użycia, ponieważ klucz hello jest ukryty wychodząc hello klucza bloku.

   Po skonfigurowaniu aplikacji logiki w części 3 Określ ten klucz jako Witaj "tajny" lub hasło.

   ![Skopiuj i Zapisz klucz do użycia później](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**Utwórz tożsamość aplikacji hello aplikacji logiki w hello klasycznego portalu Azure**

1. W hello klasycznego portalu Azure, wybierz [ **usługi Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2. Wybierz hello tym samym katalogu, w której korzystasz z aplikacji sieci web lub aplikacji interfejsu API.

3. Na powitania **aplikacji** , wybierz pozycję **Dodaj** u dołu hello hello strony.

4. Nadaj nazwę tożsamości aplikacji, a następnie wybierz pozycję **dalej** (Strzałka w prawo).

5. W obszarze **właściwości aplikacji**, podaj unikatowy ciąg w formacie domeny **adres URL logowania** i **identyfikator URI aplikacji**i wybierz polecenie **Complete** (znacznikiem wyboru).

6. Na powitania **Konfiguruj** karcie, skopiuj i Zapisz hello **identyfikator klienta** dla Twojego toouse aplikacji logiki w część 3.

7. W obszarze **klucze**, otwórz hello **wybierz czas trwania** listy. Wybierz czas trwania dla klucza.

   Witaj klucz, który tworzysz działa jako tożsamość aplikacji hello "tajny" lub hasła do aplikacji logiki.

8. U dołu hello hello strony, wybierz **zapisać**. Toowait może mieć kilka sekund.

9. W obszarze **klucze**, upewnij się, że toocopy i zapisać klucz hello, który pojawi się teraz. 

   Po skonfigurowaniu aplikacji logiki w części 3 Określ ten klucz jako Witaj "tajny" lub hasło.

Aby uzyskać więcej informacji, Dowiedz się, jak za [skonfigurować Logowanie usługi Azure Active Directory toouse aplikacji usługi App Service](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

<a name="powershell"></a>

**Utwórz tożsamość aplikacji hello aplikacji logiki w programie PowerShell**

Można wykonać tego zadania za pomocą usługi Azure Resource Manager przy użyciu programu PowerShell. W programie PowerShell uruchom następujące polecenia:

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. Upewnij się, że hello toocopy **identyfikator dzierżawcy** hello (identyfikator GUID dla dzierżawy usługi Azure AD), **identyfikator aplikacji**i hello hasła, który został użyty.

Aby uzyskać więcej informacji, Dowiedz się, jak za [utworzyć nazwy głównej usługi za pomocą programu PowerShell tooaccess zasobów](../azure-resource-manager/resource-group-authenticate-service-principal.md).

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>Część 2: Tworzenie tożsamość aplikacji usługi Azure AD dla aplikacji sieci web lub aplikacji interfejsu API

Jeśli aplikację sieci web lub aplikacji interfejsu API jest już wdrożone, należy włączyć uwierzytelnianie i Utwórz tożsamość aplikacji hello w hello portalu Azure. W przeciwnym razie można [włączyć uwierzytelnianie podczas wdrażania z szablonem usługi Azure Resource Manager](#authen-deploy). 

**Utwórz tożsamość aplikacji hello i włączyć uwierzytelnianie w portalu Azure do wdrożonych aplikacji hello**

1. W hello [portalu Azure](https://portal.azure.com "https://portal.azure.com"), Znajdź i wybierz aplikację sieci web lub aplikacji interfejsu API. 

2. W obszarze **ustawienia**, wybierz **uwierzytelniania/autoryzacji**. W obszarze **aplikacji uwierzytelniania usługi**, Włącz uwierzytelnianie **na**. W obszarze **dostawców uwierzytelniania**, wybierz **usługi Azure Active Directory**.

   ![Włączanie uwierzytelniania](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. Teraz należy utworzyć tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API, jak pokazano poniżej. Na powitania **ustawień usługi Azure Active Directory** ustawić bloku **tryb zarządzania** za**Express**. Wybierz **Utwórz nową aplikację usługi AD**. Nadaj nazwę tożsamości aplikacji, a następnie wybierz pozycję **OK**. 

   ![Utwórz tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. Na powitania **uwierzytelniania / autoryzacji bloku**, wybierz **zapisać**.

Teraz należy znaleźć hello identyfikator klienta i Identyfikatorem dzierżawy tożsamości aplikacji hello, który został skojarzony z aplikacji sieci web lub aplikacji interfejsu API. Należy użyć tych identyfikatorów w część 3. Dlatego kontynuować czynności w celu hello portalu Azure lub [klasycznego portalu Azure](#find-id-classic).

**Znajdź identyfikator klienta tożsamości aplikacji i Identyfikatorem dzierżawy dla aplikacji sieci web lub aplikacji interfejsu API w hello portalu Azure**

1. W obszarze **dostawców uwierzytelniania**, wybierz **usługi Azure Active Directory**. 

   ![Wybierz polecenie "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. Na powitania **ustawień usługi Azure Active Directory** ustawić bloku **tryb zarządzania** za**zaawansowane**.

3. Kopiuj hello **identyfikator klienta**i Zapisz ten identyfikator GUID do użycia w część 3.

   > [!TIP] 
   > Jeśli **identyfikator klienta** i **adres Url wystawcy** nie są wyświetlane, spróbuj odświeżyć hello portalu Azure i powtórz krok 1.

4. W obszarze **adres Url wystawcy**, skopiuj i Zapisz tylko hello identyfikatora GUID dla część 3. Umożliwia także ten identyfikator GUID w aplikacji sieci web lub w szablonie wdrożenia aplikacji interfejsu API, jeśli to konieczne.

   Ten identyfikator GUID jest identyfikatorem GUID dzierżawy określonych ("identyfikator dzierżawy") i powinna być widoczna w tym adresem URL:`https://sts.windows.net/{GUID}`

5. Bez zapisywania zmian, zamknij hello **ustawień usługi Azure Active Directory** bloku.

<a name="find-id-classic"></a>

**Znajdź identyfikator klienta tożsamości aplikacji i Identyfikatorem dzierżawy dla aplikacji sieci web lub aplikacji interfejsu API w hello klasycznego portalu Azure**

1. W hello klasycznego portalu Azure, wybierz [ **usługi Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2.  Wybierz katalog hello, której korzystasz z aplikacji sieci web lub aplikacji interfejsu API.

3. W hello **wyszukiwania** , Znajdź i zaznacz hello tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API.

4. Na powitania **Konfiguruj** kartę, hello kopiowania **identyfikator klienta**i Zapisz ten identyfikator GUID do użycia w część 3.

5. Po pobraniu Identyfikatora klienta hello, u dołu hello hello **Konfiguruj** , wybierz pozycję **wyświetlić punkty końcowe**.

6. Skopiuj adres URL hello **dokument metadanych usług federacyjnych**, a następnie przejdź do adresu URL toothat.

7. W dokumencie metadanych hello otwiera, Znajdź głównego hello **identyfikator EntityDescriptor** element, który ma **entityID** atrybut w tym formularzu:`https://sts.windows.net/{GUID}` 

      Witaj identyfikator GUID w tym atrybucie jest dzierżawy określonego identyfikatora GUID (identyfikator dzierżawcy).

8. Skopiuj identyfikator dzierżawcy hello i Zapisz ten identyfikator do użycia w część 3 i toouse w aplikacji sieci web lub aplikacji interfejsu API szablonu wdrażania, w razie potrzeby.

Aby uzyskać więcej informacji zobacz następujące tematy:

* [Uwierzytelnianie użytkownika dla aplikacji interfejsu API w usłudze Azure App Service](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Uwierzytelnianie i autoryzację w usłudze Azure App Service](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**Włącz uwierzytelnianie podczas wdrażania z szablonem usługi Azure Resource Manager**

Nadal należy utworzyć tożsamość aplikacji usługi Azure AD dla aplikacji sieci web lub aplikacji interfejsu API, która różni się od tożsamości aplikacji hello aplikacji logiki. tożsamość aplikacji hello toocreate, hello wykonaj poprzednie kroki w część 2 dla hello portalu Azure. Możesz również kroków hello w części 1, ale upewnij się, że toouse Twojej aplikacji sieci web lub aplikacji interfejsu API rzeczywiste `https://{URL}` dla **adres URL logowania** i **identyfikator URI aplikacji**. Z tych kroków masz toosave zarówno powitania klienta identyfikator i identyfikator dzierżawcy do użytku w szablonie wdrożenia aplikacji, a także dla część 3.

> [!NOTE]
> Podczas tworzenia tożsamości aplikacji hello Azure AD dla aplikacji sieci web lub aplikacji interfejsu API, należy użyć hello portalu Azure lub klasycznego portalu Azure, a nie programu PowerShell. polecenia programu PowerShell Hello nie skonfigurować hello wymagane uprawnienia toosign użytkowników do witryny sieci Web.

Po uzyskaniu hello Identyfikatora klienta oraz Identyfikatora dzierżawy obejmują tych identyfikatorów jako subresource aplikacji sieci web lub aplikacji interfejsu API w szablonie wdrożenia:

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

tooautomatically wdrażanie aplikacji sieci web puste i aplikacji logiki wraz z uwierzytelniania usługi Azure Active Directory [Wyświetl hello pełny szablon tutaj](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), lub kliknij przycisk **wdrażanie tooAzure** tutaj:

[![Wdrażanie tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a>Część 3: Wypełnić hello autoryzacji części aplikacji logiki

Hello poprzedni szablon jest już w tej sekcji autoryzacji, konfigurowanie, ale są bezpośrednie tworzenie aplikacji logiki hello, należy dołączyć hello pełni autoryzowane sekcji.

Otwórz definicję aplikacji logiki w widoku kodu, przejdź toohello **HTTP** sekcji akcja, Znajdź hello **autoryzacji** , a następnie Dołącz tę linię:

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| Element | Opis |
| ------- | ----------- |
| Dzierżawy |Witaj identyfikatora GUID dla dzierżawcy hello Azure AD |
| grupy odbiorców |Wymagany. Witaj identyfikatora GUID dla zasobu docelowego hello, które mają tooaccess - hello identyfikator klienta z hello tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API |
| clientId |Witaj identyfikatora GUID dla klienta hello żądania access - hello identyfikator klienta z tożsamości aplikacji hello aplikacji logiki |
| klucz tajny |Wymagany. Witaj klucza lub hasła z tożsamości aplikacji hello powitania klienta żąda hello token dostępu |
| type |Typ uwierzytelniania Hello. W przypadku uwierzytelniania ActiveDirectoryOAuth wartość hello jest `ActiveDirectoryOAuth`. |

Na przykład:

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a>Bezpieczne wywołania interfejsu API przy użyciu kodu

<a name="certificate"></a>

#### <a name="certificate-authentication"></a>Uwierzytelnianie certyfikatu

toovalidate hello przychodzących żądań od aplikacji sieci web tooyour aplikacji logiki lub aplikacji interfejsu API, można użyć certyfikatów klienta. tooset się kodu, Dowiedz się [jak wzajemnego uwierzytelniania TLS tooconfigure](../app-service-web/app-service-web-configure-tls-mutual-auth.md).

W hello **autoryzacji** sekcji, Dołącz tę linię: 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| Element | Opis |
| ------- | ----------- |
| type |Wymagany. Typ uwierzytelniania Hello. W przypadku certyfikatów SSL klienta hello wartość musi być `ClientCertificate`. |
| hasło |Wymagany. hasło Hello dla uzyskiwania dostępu do certyfikatu klienta hello (plik PFX) |
| PFX |Wymagany. Zawartość algorytmem Base64 certyfikatu klienta hello (plik PFX) |

<a name="basic"></a>

#### <a name="basic-authentication"></a>Uwierzytelnianie podstawowe

toovalidate żądań przychodzących od aplikacji sieci web tooyour aplikacji logiki lub aplikacji interfejsu API, można użyć uwierzytelniania podstawowego, takie jak nazwa użytkownika i hasło. Uwierzytelnianie podstawowe jest wspólnym wzorcem i użyć tego uwierzytelnienia w dowolnym toobuild język używany aplikacji sieci web lub aplikacji interfejsu API.

W hello **autoryzacji** sekcji, Dołącz tę linię:

`{"type": "basic", "username": "username", "password": "password"}`.

| Element | Opis |
| --- | --- |
| type |Wymagany. Typ uwierzytelniania Hello. W przypadku uwierzytelniania podstawowego hello wartość musi być `Basic`. |
| nazwa użytkownika |Wymagany. Witaj użytkownika dla uwierzytelniania |
| hasło |Wymagany. Witaj hasła do uwierzytelnienia |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>Azure uwierzytelniania usługi Active Directory przy użyciu kodu

Domyślnie hello uwierzytelniania usługi Azure AD, który można włączyć w portalu Azure hello nie zapewnia precyzyjną autoryzacji. Na przykład to uwierzytelnianie blokuje toojust Twojego interfejsu API określonego dzierżawy, nie tooa określonego użytkownika lub aplikacji. 

Aplikacja logiki tooyour dostępu toorestrict interfejsu API za pomocą kodu, Wyodrębnij nagłówek hello tokenu web hello JSON (JWT). Sprawdź tożsamość obiektu wywołującego hello i odrzucanie żądań, które nie są zgodne.

Kontynuowanie tooimplement to uwierzytelnianie w całości własnego kodu i nie hello Użyj portalu Azure, Dowiedz się, jak za [uwierzytelniania za pomocą lokalnej usługi Active Directory w aplikacji Azure](../app-service-web/web-sites-authentication-authorization.md).

tożsamość aplikacji dla aplikacji logiki toocreate i korzystanie z interfejsu API toocall tej tożsamości, należy wykonać poprzednie kroki hello.

## <a name="next-steps"></a>Następne kroki

* [Sprawdź wydajność aplikacji logiki z dzienników diagnostycznych i alerty](logic-apps-monitor-your-logic-apps.md)