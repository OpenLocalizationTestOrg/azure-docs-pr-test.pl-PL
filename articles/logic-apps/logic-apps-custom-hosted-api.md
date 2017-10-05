---
title: "Wdrożenia, wywołaj i uwierzytelniania sieci web API i interfejsów API REST dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 88c62d5ab046d8cf4bce5d23b776e517bb0e1d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>Wdrożenia, wywołaj i uwierzytelniania niestandardowych interfejsów API łączników dla usługi logic apps

Po [Tworzenie niestandardowych interfejsów API](./logic-apps-create-api-app.md) zawierających akcji lub wyzwalaczy do użycia w przepływach pracy aplikacji logiki, swoje interfejsy API należy wdrożyć przed wywołaniem je. I chociaż jakiegokolwiek interfejsu API można wywołać z aplikacji logiki, aby uzyskać najlepsze wyniki, Dodaj [Swagger metadanych](http://swagger.io/specification/) opisujący Twój interfejs API operacji i parametry. Ten plik struktury Swagger pomaga interfejsu API działa lepiej i łatwo zintegrować z usługą logic apps.

Można wdrożyć swoje interfejsy API jako [sieci web aplikacji](../app-service-web/app-service-web-overview.md), ale warto wdrożyć swoje interfejsy API jako [aplikacje interfejsu API](../app-service-api/app-service-api-apps-why-best-platform.md), które mogą ułatwić zadania podczas kompilacji, hosta i korzystanie z interfejsów API w chmurze i lokalnie. Nie trzeba zmieniać żadnego kodu w swoje interfejsy API — wystarczy go wdrożyć kod w aplikacji interfejsu API. Swoje interfejsy API mogą być hostowane na [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md), platformy jako — usługa (PaaS) oferta zapewnia w jednym ze sposobów najlepsze najprostszym i najbardziej skalowalny hosting interfejsu API.

Do uwierzytelnienia wywołania z aplikacji logiki swoje interfejsy API, można ustawić usługę Azure Active Directory w portalu Azure, nie trzeba zaktualizować kodu. Lub może wymagać i wymusić uwierzytelnianie za pomocą kodu Twój interfejs API.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>Wdrażanie aplikacji sieci web lub aplikacji interfejsu API interfejsu API

Przed niestandardowego interfejsu API można wywołać z aplikacji logiki, należy wdrożyć jako aplikacji sieci web lub aplikacji interfejsu API interfejsu API w usłudze Azure App Service. Ponadto odczytywać dokumentu Swagger przez projektanta aplikacji logiki, ustaw właściwości definicji interfejsu API i Włącz [współużytkowanie zasobów między źródłami (CORS) do udostępniania](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) dla aplikacji sieci web lub aplikacji interfejsu API.

1. W portalu Azure wybierz aplikację sieci web lub aplikacji interfejsu API.

2. W bloku, który zostanie otwarty, w obszarze **interfejsu API**, wybierz **definicji interfejsu API**. Ustaw **lokalizacji definicji interfejsu API** na adres URL pliku swagger.json.

   Adres URL pojawia się zwykle w następującym formacie:`https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![Łącze do pliku programu Swagger do niestandardowego interfejsu API](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. W obszarze **interfejsu API**, wybierz **CORS**. Ustawienie zasad CORS dla **dozwolone źródła** do  **"*"** (Zezwalaj na wszystkie).

   Ustawienie to pozwala żądania przy użyciu projektanta aplikacji logiki.

   ![Zezwala na żądania z projektanta aplikacji logiki do niestandardowego interfejsu API](media/logic-apps-custom-hosted-api/custom-api-cors.png)

Aby uzyskać więcej informacji zobacz następujące artykuły:

* [Dodaj metadane programu Swagger dla interfejsów API sieci web ASP.NET](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [Wdrażanie interfejsów API sieci web ASP.NET w usłudze Azure App Service](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Wywoływanie niestandardowego interfejsu API z logiki przepływów pracy aplikacji

Po skonfigurowaniu właściwości definicji interfejsu API i mechanizmu CORS wyzwalacze i akcje niestandardowego interfejsu API powinien być dostępny do uwzględnienia w przepływie pracy aplikacji logiki. 

*  Aby wyświetlić Swagger URL witryn sieci Web, możesz wyszukać subskrypcji witryny sieci Web w Projektancie aplikacji logiki.

*  Aby wyświetlić dostępne akcje i dane wejściowe, wskazując dokumentu Swagger, użyj [HTTP + Swagger akcji](../connectors/connectors-native-http-swagger.md).

*  Aby wywołać jakiegokolwiek interfejsu API, łącznie z interfejsów API, które nie mają lub udostępnianie dokumentu Swagger, zawsze można utworzyć żądania z [akcji HTTP](../connectors/connectors-native-http.md).

## <a name="authenticate-calls-to-your-custom-api"></a>Uwierzytelnienia wywołań do niestandardowego interfejsu API

Możesz zabezpieczyć wywołania do niestandardowego interfejsu API w następujący sposób:

* [Nie zmian w kodzie](#no-code): interfejs API ochrony [usługi Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) za pośrednictwem portalu Azure, więc nie trzeba zaktualizować kodu lub ponownego wdrażania interfejsu API.

  > [!NOTE]
  > Domyślnie uwierzytelniania usługi Azure AD, który można włączyć w portalu Azure nie zapewnia precyzyjną autoryzacji. Na przykład to uwierzytelnianie blokuje interfejsu API do określonych dzierżawy, a nie do określonego użytkownika lub aplikacji. 

* [Zaktualizuj kod Twój interfejs API](#update-code): ochrona interfejsu API przez wymuszenie [uwierzytelnianie certyfikatu](#certificate), [uwierzytelnianie podstawowe](#basic), lub [uwierzytelniania usługi Azure AD](#azure-ad-code) za pomocą kodu.

<a name="no-code"></a>

### <a name="authenticate-calls-to-your-api-without-changing-code"></a>Uwierzytelnianie wywołań interfejsu API bez zmiany kodu

Poniżej przedstawiono ogólne kroki dla tej metody:

1. Utwórz dwa [tożsamości aplikacji usługi Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): jeden dla aplikacji logiki i jeden dla aplikacji sieci web (lub aplikacji interfejsu API).

2. Na potrzeby uwierzytelniania wywołań interfejsu API, Użyj poświadczeń (identyfikator klienta i klucz tajny) dla [nazwy głównej usługi](../app-service-api/app-service-api-dotnet-service-principal-auth.md) która jest skojarzona z tożsamość aplikacji usługi Azure AD dla aplikacji logiki.

3. Zawiera identyfikatorów aplikacji w definicji aplikacji logiki.

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>Część 1: Tworzenie aplikacji logiki tożsamość aplikacji usługi Azure AD

Aplikację logiki używa tego tożsamość aplikacji usługi Azure AD do uwierzytelniania usługi Azure AD. Wystarczy tylko skonfigurować tej tożsamości jeden raz dla katalogu. Na przykład możesz użyć tej samej tożsamości dla wszystkich aplikacji logiki, mimo że można utworzyć unikatowych tożsamości dla każdej aplikacji logiki. Możesz skonfigurować te tożsamości w portalu Azure [klasycznego portalu Azure](#app-identity-logic-classic), lub użyj [PowerShell](#powershell).

**Tworzenie aplikacji logiki tożsamości aplikacji w portalu Azure**

1. W [portalu Azure](https://portal.azure.com "https://portal.azure.com"), wybierz **usługi Azure Active Directory**. 

2. Upewnij się, że jesteś w tym samym katalogu co aplikację sieci web lub aplikacji interfejsu API.

   > [!TIP]
   > Aby przełączyć katalogów, kliknij profil i wybierz inny katalog. Lub wybierz **omówienie** > **katalogu przełącznika**.

3. W menu katalogu w obszarze **Zarządzaj**, wybierz **rejestracji aplikacji** > **nowej rejestracji aplikacji**.

   > [!TIP]
   > Domyślnie lista rejestracji aplikacji zawiera wszystkich rejestracji aplikacji w katalogu. Aby wyświetlić tylko rejestracji aplikacji, w polu wyszukiwania, wybierz **Moje aplikacje**. 

   ![Tworzenie nowej rejestracji aplikacji](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. Nadaj nazwę tożsamości aplikacji, pozostaw **typu aplikacji** ustawioną **aplikacji sieci Web / interfejs API**, Podaj unikatową ciąg w formacie domeny dla **adres URL logowania**i wybierz polecenie **Utwórz**.

   ![Podaj nazwę i logowania jednokrotnego adres URL dla tożsamości aplikacji](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   Tożsamość aplikacji utworzonej dla aplikacji logiki teraz zostanie wyświetlony na liście rejestracji aplikacji.

   ![Tożsamość aplikacji dla aplikacji logiki](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. Na liście rejestracji aplikacji wybierz nowy identyfikator aplikacji. Skopiuj i Zapisz **identyfikator aplikacji** do użycia jako "Identyfikator klienta" aplikację logiki w część 3.

   ![Skopiuj i Zapisz identyfikator aplikacji dla aplikacji logiki](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. Jeśli ustawienia tożsamość aplikacji nie są widoczne, wybierz **ustawienia** lub **wszystkie ustawienia**.

7. W obszarze **dostępu do interfejsu API**, wybierz **klucze**. W obszarze **opis**, podaj nazwę klucza. W obszarze **Expires**, wybierz czas trwania dla klucza.

   Klucz, który tworzysz działa jako tożsamość aplikacji "tajny" lub hasła do aplikacji logiki.

   ![Utwórz klucz tożsamości aplikacji logiki](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. Na pasku narzędzi wybierz **zapisać**. W obszarze **wartość**, klucz zostanie wyświetlone. 
**Upewnij się, że skopiuj i Zapisz klucz** do późniejszego użycia, ponieważ jest ukryta klucz wychodząc klucza bloku.

   Podczas konfigurowania aplikacji logiki w część 3, należy określić ten klucz jako "secret" lub hasło.

   ![Skopiuj i Zapisz klucz do użycia później](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**Utwórz tożsamość aplikacji dla aplikacji logiki w klasycznym portalu Azure**

1. W klasycznym portalu Azure, wybierz [ **usługi Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2. Należy wybrać ten sam katalog, w której korzystasz z aplikacji sieci web lub aplikacji interfejsu API.

3. Na **aplikacji** , wybierz pozycję **Dodaj** w dolnej części strony.

4. Nadaj nazwę tożsamości aplikacji, a następnie wybierz pozycję **dalej** (Strzałka w prawo).

5. W obszarze **właściwości aplikacji**, podaj unikatowy ciąg w formacie domeny **adres URL logowania** i **identyfikator URI aplikacji**i wybierz polecenie **Complete** (znacznikiem wyboru).

6. Na **Konfiguruj** karcie, skopiuj i Zapisz **identyfikator klienta** aplikacji logiki do używania w części 3.

7. W obszarze **klucze**, otwórz **wybierz czas trwania** listy. Wybierz czas trwania dla klucza.

   Klucz, który tworzysz działa jako tożsamość aplikacji "tajny" lub hasła do aplikacji logiki.

8. W dolnej części strony, wybierz **zapisać**. Może być konieczne kilka sekund.

9. W obszarze **klucze**, skopiuj i Zapisz klucz pojawia się która teraz. 

   Podczas konfigurowania aplikacji logiki w część 3, należy określić ten klucz jako "secret" lub hasło.

Aby uzyskać więcej informacji, Dowiedz się, jak [skonfigurować aplikację usługi aplikacji do użycia usługi Azure Active Directory logowania](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

<a name="powershell"></a>

**Tworzenie aplikacji logiki tożsamości aplikacji w programie PowerShell**

Można wykonać tego zadania za pomocą usługi Azure Resource Manager przy użyciu programu PowerShell. W programie PowerShell uruchom następujące polecenia:

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. Upewnij się skopiować **identyfikator dzierżawcy** (identyfikator GUID dla dzierżawy usługi Azure AD), **identyfikator aplikacji**i hasła, który został użyty.

Aby uzyskać więcej informacji, Dowiedz się, jak [Tworzenie nazwy głównej usługi przy użyciu programu PowerShell dostęp do zasobów](../azure-resource-manager/resource-group-authenticate-service-principal.md).

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>Część 2: Tworzenie tożsamość aplikacji usługi Azure AD dla aplikacji sieci web lub aplikacji interfejsu API

Jeśli aplikację sieci web lub aplikacji interfejsu API jest już wdrożone, można włączyć uwierzytelnianie i utworzenia tożsamości aplikacji w portalu Azure. W przeciwnym razie można [włączyć uwierzytelnianie podczas wdrażania z szablonem usługi Azure Resource Manager](#authen-deploy). 

**Utwórz tożsamość aplikacji i włączyć uwierzytelnianie w portalu Azure w przypadku wdrożonej aplikacji**

1. W [portalu Azure](https://portal.azure.com "https://portal.azure.com"), Znajdź i wybierz aplikację sieci web lub aplikacji interfejsu API. 

2. W obszarze **ustawienia**, wybierz **uwierzytelniania/autoryzacji**. W obszarze **aplikacji uwierzytelniania usługi**, Włącz uwierzytelnianie **na**. W obszarze **dostawców uwierzytelniania**, wybierz **usługi Azure Active Directory**.

   ![Włączanie uwierzytelniania](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. Teraz należy utworzyć tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API, jak pokazano poniżej. Na **ustawień usługi Azure Active Directory** ustawić bloku **tryb zarządzania** do **Express**. Wybierz **Utwórz nową aplikację usługi AD**. Nadaj nazwę tożsamości aplikacji, a następnie wybierz pozycję **OK**. 

   ![Utwórz tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. Na **uwierzytelniania / autoryzacji bloku**, wybierz **zapisać**.

Teraz należy znaleźć tożsamości aplikacji, który został skojarzony z aplikacji sieci web lub aplikacji interfejsu API klienta ID oraz Identyfikatora dzierżawcy. Należy użyć tych identyfikatorów w część 3. Aby kontynuować następujące kroki w portalu Azure lub [klasycznego portalu Azure](#find-id-classic).

**Znajdź identyfikator klienta i Identyfikatora dzierżawcy tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API w portalu Azure**

1. W obszarze **dostawców uwierzytelniania**, wybierz **usługi Azure Active Directory**. 

   ![Wybierz polecenie "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. Na **ustawień usługi Azure Active Directory** ustawić bloku **tryb zarządzania** do **zaawansowane**.

3. Kopiuj **identyfikator klienta**i Zapisz ten identyfikator GUID do użycia w część 3.

   > [!TIP] 
   > Jeśli **identyfikator klienta** i **adres Url wystawcy** nie są wyświetlane, spróbuj odświeżyć portalu Azure i powtórz krok 1.

4. W obszarze **adres Url wystawcy**, skopiuj i Zapisz tylko identyfikator GUID dla część 3. Umożliwia także ten identyfikator GUID w aplikacji sieci web lub w szablonie wdrożenia aplikacji interfejsu API, jeśli to konieczne.

   Ten identyfikator GUID jest identyfikatorem GUID dzierżawy określonych ("identyfikator dzierżawy") i powinna być widoczna w tym adresem URL:`https://sts.windows.net/{GUID}`

5. Bez zapisywania zmian, Zamknij **ustawień usługi Azure Active Directory** bloku.

<a name="find-id-classic"></a>

**Znajdź identyfikator klienta i Identyfikatora dzierżawcy tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API w klasycznym portalu Azure**

1. W klasycznym portalu Azure, wybierz [ **usługi Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2.  Wybierz katalog, w której korzystasz z aplikacji sieci web lub aplikacji interfejsu API.

3. W **wyszukiwania** , Znajdź i wybierz tożsamość aplikacji dla aplikacji sieci web lub aplikacji interfejsu API.

4. Na **Konfiguruj** karcie, skopiuj **identyfikator klienta**i Zapisz ten identyfikator GUID do użycia w część 3.

5. Po pobraniu Identyfikatora klienta w dolnej części **Konfiguruj** , wybierz pozycję **wyświetlić punkty końcowe**.

6. Skopiuj adres URL dla **dokument metadanych usług federacyjnych**, a następnie przejdź do tego adresu URL.

7. W dokumencie metadanych można znaleźć katalogu głównego **identyfikator EntityDescriptor** element, który ma **entityID** atrybut w tym formularzu:`https://sts.windows.net/{GUID}` 

      Identyfikator GUID w tym atrybucie jest dzierżawy określonego identyfikatora GUID (identyfikator dzierżawcy).

8. Skopiuj identyfikator dzierżawcy i Zapisz ten identyfikator do użycia w część 3, a także do użycia w aplikacji sieci web lub aplikacji interfejsu API szablonu wdrażania, w razie potrzeby.

Aby uzyskać więcej informacji zobacz następujące tematy:

* [Uwierzytelnianie użytkownika dla aplikacji interfejsu API w usłudze Azure App Service](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Uwierzytelnianie i autoryzację w usłudze Azure App Service](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**Włącz uwierzytelnianie podczas wdrażania z szablonem usługi Azure Resource Manager**

Nadal należy utworzyć tożsamość aplikacji usługi Azure AD dla aplikacji sieci web lub aplikacji interfejsu API, która różni się od tożsamości aplikacji dla aplikacji logiki. Aby utworzyć tożsamość aplikacji, wykonaj poprzednie kroki w część 2 dla portalu Azure. Możesz również wykonaj kroki opisane w części 1, ale pamiętaj korzystać z aplikacji sieci web lub aplikacji interfejsu API rzeczywiste `https://{URL}` dla **adres URL logowania** i **identyfikator URI aplikacji**. Z tych kroków należy zapisać identyfikator klienta i identyfikator dzierżawcy do użytku w szablonie wdrożenia aplikacji, a także dla część 3.

> [!NOTE]
> Podczas tworzenia tożsamość aplikacji usługi Azure AD dla twojej aplikacji sieci web lub aplikacji interfejsu API, musisz użyć portalu Azure lub klasycznego portalu Azure, zamiast programu PowerShell. Polecenia programu PowerShell nie skonfigurować wymagane uprawnienia do logowania się użytkowników do witryny sieci Web.

Po pobraniu klienta identyfikator i identyfikator dzierżawy obejmują tych identyfikatorów jako subresource aplikacji sieci web lub aplikacji interfejsu API w szablonie wdrożenia:

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

Automatyczne wdrażanie aplikacji sieci web puste i aplikacji logiki wraz z uwierzytelniania usługi Azure Active Directory [wyświetlić pełną szablonu tutaj](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), lub kliknij przycisk **wdrażanie na platformie Azure** tutaj:

[![Wdrażanie na platformie Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a>Część 3: Wypełnić sekcję autoryzacji w aplikacji logiki

Poprzedni szablon jest już w tej sekcji autoryzacji, konfigurowanie, ale są bezpośrednie tworzenie aplikacji logiki, należy dołączyć sekcji pełne autoryzacji.

Otwórz definicję aplikacji logiki w widoku kodu, przejdź do **HTTP** sekcji Akcja znaleźć **autoryzacji** , a następnie Dołącz tę linię:

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| Element | Opis |
| ------- | ----------- |
| Dzierżawy |Identyfikator GUID dzierżawy usługi Azure AD |
| grupy odbiorców |Wymagane. Identyfikator GUID zasobu docelowego, który chcesz uzyskać dostęp — identyfikator klienta z tożsamości aplikacji dla aplikacji sieci web lub aplikacji interfejsu API |
| clientId |Identyfikator GUID dla klienta żąda dostępu — identyfikator klienta z tożsamość aplikacji dla aplikacji logiki |
| klucz tajny |Wymagane. Klucz lub hasło z tożsamość aplikacji, gdy klient żąda token dostępu |
| type |Typ uwierzytelniania. Wartość dla uwierzytelniania ActiveDirectoryOAuth jest `ActiveDirectoryOAuth`. |

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

Aby sprawdzić poprawność żądań przychodzących od aplikacji logiki do aplikacji sieci web lub aplikacji interfejsu API, można użyć certyfikatów klienta. Aby skonfigurować swój kod, Dowiedz się [jak skonfigurować uwierzytelnianie wzajemne TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md).

W **autoryzacji** sekcji, Dołącz tę linię: 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| Element | Opis |
| ------- | ----------- |
| type |Wymagane. Typ uwierzytelniania. Dla certyfikatów klienta SSL, wartość musi być `ClientCertificate`. |
| hasło |Wymagane. Hasło do uzyskiwania dostępu do certyfikatu klienta (plik PFX) |
| PFX |Wymagane. Zawartość algorytmem Base64 certyfikatu klienta (plik PFX) |

<a name="basic"></a>

#### <a name="basic-authentication"></a>Uwierzytelnianie podstawowe

Można sprawdzić poprawności przychodzących żądań od aplikacji logiki do aplikacji sieci web lub aplikacji interfejsu API, można użyć uwierzytelnianie podstawowe, takie jak nazwa użytkownika i hasło. Uwierzytelnianie podstawowe jest wspólnego wzorca i może uwierzytelnianie w dowolnym języku używanym do budowania aplikację sieci web lub aplikacji interfejsu API.

W **autoryzacji** sekcji, Dołącz tę linię:

`{"type": "basic", "username": "username", "password": "password"}`.

| Element | Opis |
| --- | --- |
| type |Wymagane. Typ uwierzytelniania. W przypadku uwierzytelniania podstawowego musi być wartością `Basic`. |
| nazwa użytkownika |Wymagane. Nazwa użytkownika do uwierzytelniania |
| hasło |Wymagane. Hasło do uwierzytelniania |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>Azure uwierzytelniania usługi Active Directory przy użyciu kodu

Domyślnie uwierzytelniania usługi Azure AD, który można włączyć w portalu Azure nie zapewnia precyzyjną autoryzacji. Na przykład to uwierzytelnianie blokuje interfejsu API do określonych dzierżawy, a nie do określonego użytkownika lub aplikacji. 

Aby ograniczyć dostęp do interfejsu API do aplikacji logiki do kodu, Wyodrębnij nagłówek, który ma tokenu web JSON (JWT). Sprawdź tożsamość obiektu wywołującego i odrzucanie żądań, które nie są zgodne.

Kontynuowanie, aby zaimplementować uwierzytelnianie całkowicie w swoim własnym kodem, a nie za pomocą portalu Azure, Dowiedz się jak [uwierzytelniania za pomocą lokalnej usługi Active Directory w aplikacji Azure](../app-service-web/web-sites-authentication-authorization.md).

Aby utworzyć tożsamość aplikacji dla aplikacji logiki i użyć tej tożsamości do wywołania interfejsu API, należy wykonać poprzednie kroki.

## <a name="next-steps"></a>Następne kroki

* [Sprawdź wydajność aplikacji logiki z dzienników diagnostycznych i alerty](logic-apps-monitor-your-logic-apps.md)