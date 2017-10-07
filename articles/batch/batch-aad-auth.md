---
title: "rozwiązań usług partii zadań Azure tooauthenticate usługi Azure Active Directory aaaUse | Dokumentacja firmy Microsoft"
description: "Wsadowe obsługuje usługi Azure AD do uwierzytelniania z hello usługa partia zadań."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a>Uwierzytelnianie partii rozwiązań usług w usłudze Active Directory

Partia zadań Azure obsługuje uwierzytelnianie za pomocą [usługi Azure Active Directory] [ aad_about] (Azure AD). Usługi Azure AD jest katalog wielu dzierżawców w chmurze firmy Microsoft i tożsamość usługi zarządzania. Azure sam używa usługi Azure AD tooauthenticate swoich klientów, Administratorzy usługi i użytkowników w organizacji.

Jeśli używasz uwierzytelniania usługi Azure AD z partii zadań Azure, można uwierzytelniać się w jednym z dwóch sposobów:

- Za pomocą **zintegrowane uwierzytelnianie** tooauthenticate użytkownika, do którego prowadzi interakcję z aplikacji hello. Aplikacji przy użyciu zintegrowanego uwierzytelniania zbiera poświadczeń użytkownika i używa tych poświadczeń tooauthenticate dostępu tooBatch zasobów.
- Za pomocą **nazwy głównej usługi** tooauthenticate nienadzorowanej aplikacji. Nazwy głównej usługi definiuje hello zasad i uprawnień dla aplikacji w aplikacji hello toorepresent kolejności podczas uzyskiwania dostępu do zasobów w czasie wykonywania.

toolearn więcej informacji na temat usługi Azure AD, zobacz hello [Azure Active Directory dokumentacji](https://docs.microsoft.com/azure/active-directory/).

## <a name="authentication-and-pool-allocation-mode"></a>Uwierzytelnianie i puli Tryb alokacji

Podczas tworzenia konta usługi partia zadań można określić, gdzie można przydzielić pule utworzone dla tego konta. Pule tooallocate można wybrać w subskrypcji usługi partii domyślne hello lub w ramach subskrypcji użytkownika. Wybór ma wpływ na sposób uwierzytelniania tooresources dostęp na tym koncie.

- **Partii subskrypcji usługi**. Domyślnie partii pule są przydzielane w ramach subskrypcji usługi partii. Jeśli wybierzesz tę opcję, można uwierzytelniać tooresources dostępu do tego konta za pomocą [klucz wstępny](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) lub za pomocą usługi Azure AD.
- **Subskrypcja użytkownika.** Można wybrać tooallocate pule partii w subskrypcji użytkownika, który określisz. Jeśli wybierzesz tę opcję, musi uwierzytelniać się z usługą Azure AD.

## <a name="endpoints-for-authentication"></a>Punkty końcowe na potrzeby uwierzytelniania

tooauthenticate partii aplikacji z usługą Azure AD, należy tooinclude niektórych dobrze znanych punktów końcowych w kodzie.

### <a name="azure-ad-endpoint"></a>Punktu końcowego platformy Azure AD

Witaj podstawowy punkt końcowy urzędu usługi Azure AD jest:

`https://login.microsoftonline.com/`

tooauthenticate z usługą Azure AD, możesz użyć tego punktu końcowego wraz z hello identyfikator dzierżawcy (identyfikator katalogu). Identyfikator dzierżawy Hello określa toouse dzierżawy usługi Azure AD hello do uwierzytelniania. tooretrieve hello Identyfikatora dzierżawcy, wykonaj czynności hello opisane w temacie [uzyskanie Identyfikatora dzierżawy hello usługi Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> punkt końcowy specyficznego dla dzierżawy Hello jest wymagana podczas uwierzytelniania przy użyciu nazwy głównej usługi. 
> 
> punkt końcowy specyficznego dla dzierżawy Hello jest opcjonalne podczas uwierzytelniania przy użyciu zintegrowanego uwierzytelniania, ale zalecane. Jednak umożliwia także wspólnego punktu końcowego hello Azure AD. Witaj wspólnego punktu końcowego dostarcza poświadczenia ogólnego zbierania interfejsu, gdy nie podano określonych dzierżawy. punkt końcowy wspólnej Hello jest `https://login.microsoftonline.com/common`.
>
>

Aby uzyskać więcej informacji na temat punktów końcowych usługi Azure AD, zobacz [scenariusze uwierzytelniania dla usługi Azure AD][aad_auth_scenarios].

### <a name="batch-resource-endpoint"></a>Punkt końcowy zasobów usługi partia zadań

Użyj hello **punktu końcowego zasobów partii zadań Azure** tooacquire token do uwierzytelniania żądań toohello usługa partia zadań:

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a>Zarejestrować aplikację z dzierżawą

pierwszym krokiem Hello przy użyciu usługi Azure AD tooauthenticate rejestruje aplikację w dzierżawie usługi Azure AD. Rejestrowanie aplikacji umożliwia toocall hello Azure [biblioteki uwierzytelniania usługi Active Directory] [ aad_adal] (ADAL) w kodzie. Witaj ADAL dostarcza interfejs API w celu uwierzytelniania w usłudze Azure AD z aplikacji. Rejestrowanie aplikacji jest wymagany, czy planujesz toouse zintegrowanego uwierzytelniania lub nazwy głównej usługi.

Podczas rejestrowania aplikacji, należy podać informacje o Twojej aplikacji tooAzure AD. Następnie usługi Azure AD zapewnia identyfikator aplikacji używanie tooassociate aplikacji z usługą Azure AD w czasie wykonywania. toolearn więcej informacji na temat hello identyfikator aplikacji, zobacz [aplikacji i usług obiektów principal w usłudze Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

tooregister aplikacji partii, wykonaj kroki hello hello [Dodawanie aplikacji](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sekcji [Integrowanie aplikacji z usługą Azure Active Directory][aad_integrate]. Jeśli zarejestrujesz aplikacji jako aplikacji natywnej, można określić żadnych prawidłowy identyfikator URI dla hello **identyfikator URI przekierowania**. Nie potrzebuje toobe rzeczywistych punktu końcowego.

Po aplikacji został zarejestrowany, zostanie wyświetlony identyfikator aplikacji hello:

![Rejestrowanie aplikacji partii z usługą Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

Aby uzyskać więcej informacji o rejestrowaniu aplikacji z usługą Azure AD, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).

## <a name="get-hello-tenant-id-for-your-active-directory"></a>Uzyskanie Identyfikatora dzierżawy powitania dla usługi Active Directory

Identyfikator dzierżawy Hello określa hello dzierżawy usługi Azure AD, zapewniający uwierzytelnianie usług tooyour aplikacji. tooget hello Identyfikatora dzierżawy, wykonaj następujące kroki:

1. W portalu Azure hello wybierz usługi Active Directory.
2. Kliknij pozycję **Właściwości**.
3. Skopiuj wartość identyfikatora GUID hello identyfikatora hello katalogu. Ta wartość jest również określany jako identyfikator hello dzierżawcy.

![Skopiuj identyfikator katalogu hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a>Uwierzytelnianie zintegrowane

tooauthenticate ze zintegrowanego uwierzytelniania, należy toogrant Twojego toohello tooconnect uprawnienia aplikacji interfejsu API usługi partii. Ten krok umożliwia aplikacji tooauthenticate wywołania toohello partii usługi interfejsu API z usługi Azure AD.

Po wprowadzeniu [zarejestrowana aplikacja](#register-your-application-with-an-azure-ad-tenant), wykonaj następujące kroki w hello Azure portalu toogrant uzyskać dostępu do usługi partia zadań toohello:

1. W okienku nawigacji po lewej stronie powitania hello portalu Azure, wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**.
2. Wyszukaj nazwę aplikacji na liście hello rejestracji aplikacji hello:

    ![Wyszukaj nazwę aplikacji](./media/batch-aad-auth/search-app-registration.png)

3. Otwórz hello **ustawienia** bloku dla aplikacji. W hello **dostępu do interfejsu API** zaznacz **wymagane uprawnienia**.
4. W hello **wymagane uprawnienia** bloku, kliknij przycisk hello **Dodaj** przycisku.
5. W kroku 1 Wyszukaj hello interfejsu API partii. Wyszukiwania dla każdego z tych parametrów do momentu znalezienia hello interfejsu API:
    1. **MicrosoftAzureBatch**.
    2. **Microsoft Azure Batch**. W przypadku nowszych dzierżaw usługi Azure AD może być używana ta nazwa.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** jest identyfikator hello hello interfejsu API partii. 
6. Po znalezieniu hello interfejsu API partii, zaznacz go i kliknij hello **wybierz** przycisku.
6. W kroku 2, wybierz hello pole wyboru obok zbyt**usługa partia zadań Azure dostępu** i kliknij przycisk hello **wybierz** przycisku.
7. Kliknij przycisk hello **gotowe** przycisku.

Witaj **wymagane uprawnienia** bloku teraz wskazuje, że aplikacja Azure AD ma dostęp do tooboth ADAL i hello interfejsu API usługi partii. Uprawnienia są przyznawane tooADAL automatycznie podczas rejestrowania aplikacji z usługą Azure AD.

![Interfejs API Udziel uprawnień](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a>Użyj nazwy głównej usługi 

tooauthenticate aplikację, która działa w instalacji nienadzorowanej, możesz użyć nazwy głównej usługi. Po po zarejestrowaniu aplikacji, wykonaj następujące kroki w hello Azure tooconfigure portalu nazwy głównej usługi:

1. Żądanie klucz tajny aplikacji.
2. Przypisywanie aplikacji tooyour RBAC roli.

### <a name="request-a-secret-key-for-your-application"></a>Żądanie klucz tajny aplikacji

Podczas uwierzytelniania aplikacji z nazwy głównej usługi, wysyła identyfikator aplikacji hello jak tooAzure klucza tajnego usługi AD. Będzie konieczne toocreate i skopiuj toouse klucza tajnego hello w kodzie.

Wykonaj następujące kroki w portalu Azure hello:

1. W okienku nawigacji po lewej stronie powitania hello portalu Azure, wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**.
2. Wyszukaj nazwę hello aplikacji hello liście rejestracji aplikacji.
3. Wyświetl hello **ustawienia** bloku. W hello **dostępu do interfejsu API** zaznacz **klucze**.
4. toocreate klucza, wprowadź opis hello klucza. Następnie wybierz czas trwania dla klucza hello jeden lub dwa lata. 
5. Kliknij przycisk hello **zapisać** przycisk toocreate i wyświetla hello klucza. Skopiuj hello wartość klucza tooa bezpiecznym miejscu, ponieważ będziesz w stanie tooaccess pozostawić ją ponownie po hello bloku. 

    ![Utwórz klucz tajny](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a>Przypisanie roli aplikacji tooyour RBAC

tooauthenticate z nazwy głównej usługi, należy tooassign RBAC roli tooyour aplikacji. Wykonaj następujące kroki:

1. W hello portalu Azure Przejdź konta usługi partia zadań toohello używanych przez aplikację.
2. W hello **ustawienia** bloku dla konta wsadowego hello, wybierz opcję **kontroli dostępu (IAM)**.
3. Kliknij przycisk hello **Dodaj** przycisku. 
4. Z hello **roli** listy rozwijanej, wybierz albo hello _współautora_ lub _czytnika_ roli aplikacji. Aby uzyskać więcej informacji o tych ról, zobacz [wprowadzenie opartej na rolach kontrola dostępu w portalu Azure hello](../active-directory/role-based-access-control-what-is.md).  
5. W hello **wybierz** wprowadź nazwę aplikacji hello. Wybierz aplikację z listy hello, a następnie kliknij przycisk **zapisać**.

Aplikacja powinien zostać wyświetlony w ustawieniach kontroli dostępu z rolą RBAC przypisane. 

![Przypisanie roli aplikacji tooyour RBAC](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a>Uzyskanie Identyfikatora dzierżawy hello usługi Azure Active Directory

Identyfikator dzierżawy Hello określa hello dzierżawy usługi Azure AD, zapewniający uwierzytelnianie usług tooyour aplikacji. tooget hello Identyfikatora dzierżawy, wykonaj następujące kroki:

1. W portalu Azure hello wybierz usługi Active Directory.
2. Kliknij pozycję **Właściwości**.
3. Skopiuj wartość identyfikatora GUID hello identyfikatora hello katalogu. Ta wartość jest również określany jako identyfikator hello dzierżawcy.

![Skopiuj identyfikator katalogu hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a>Przykłady kodu

Przykłady kodu Hello w tej sekcji Pokaż jak tooauthenticate z usługi Azure AD przy użyciu zintegrowanego uwierzytelniania i nazwy głównej usługi. Te przykłady kodu przy użyciu .NET, ale pojęcia hello są podobne dla innych języków.

> [!NOTE]
> Token uwierzytelniania usługi Azure AD wygasa po upływie godziny. Korzystając z długotrwałe **BatchClient** obiektu, firma Microsoft zaleca, aby pobrać token z biblioteki ADAL na każdym tooensure żądania zawsze ma nieprawidłowy token. 
>
>
> tooachieve to w .NET napisanie metody, że pobiera hello tokenu z usługi Azure AD i przekaż tooa tej metody **BatchTokenCredentials** obiektu jako pełnomocnik. Hello delegata metoda jest wywoływana na każdego żądania toohello partii usługi tooensure dostarczonego prawidłowego tokenu. Domyślnie ADAL buforuje tokenów, aby nowy token są pobierane z usługi Azure AD tylko wtedy, gdy jest to konieczne. Aby uzyskać więcej informacji dotyczących tokenów w usłudze Azure AD, zobacz [scenariusze uwierzytelniania dla usługi Azure AD][aad_auth_scenarios].
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a>Przykład kodu: używanie programu Azure AD zintegrowane uwierzytelnianie z partiami platformy .NET

tooauthenticate przy użyciu zintegrowanego uwierzytelniania z partiami platformy .NET, odwołanie hello [Azure partiami platformy .NET](https://www.nuget.org/packages/Azure.Batch/) pakietu i hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pakietu.

Uwzględnij następujące elementy hello `using` instrukcje w kodzie:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Witaj odwołanie do punktu końcowego usługi Azure AD w kodzie, w tym hello dzierżawy identyfikatora. tooretrieve hello Identyfikatora dzierżawcy, wykonaj czynności hello opisane w temacie [uzyskanie Identyfikatora dzierżawy hello usługi Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Odwołanie hello partii zasobu punktu końcowego usługi:

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Odwołanie konta partii zadań:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Określ identyfikator aplikacji hello (identyfikator klienta) dla aplikacji. Identyfikator aplikacji Hello jest dostępny z rejestracji aplikacji w portalu Azure hello:

```csharp
private const string ClientId = "<application-id>";
```

Kopiuje też hello przekierowania URI, które zostały określone podczas procesu rejestracji hello. Witaj przekierowania określony w kodzie identyfikator URI musi być zgodna hello przekierowania URI podane podczas rejestrowania aplikacji hello:

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

Zapis token uwierzytelniania hello tooacquire metody wywołania zwrotnego z usługi Azure AD. Witaj **GetAuthenticationTokenAsync** wywołania metod wywołania zwrotnego pokazane ADAL tooauthenticate użytkownika, który prowadzi interakcję z aplikacji hello. Witaj **AcquireTokenAsync** Metoda podana przez ADAL monity hello ich poświadczenia użytkownika i aplikacji hello będzie kontynuowana po hello użytkownika zapewni im (chyba że ma już pamięci podręcznej poświadczeń):

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

Utworzyć **BatchTokenCredentials** obiekt, który przyjmuje hello delegata jako parametr. Użyj tych poświadczeń tooopen **BatchClient** obiektu. Możesz użyć tych **BatchClient** obiektu dla kolejnych operacji względem hello usługa partia zadań:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a>Przykład kodu: przy użyciu nazwy głównej usługi Azure AD z partiami platformy .NET

tooauthenticate z nazwy głównej usługi z partiami platformy .NET, odwołanie hello [Azure partiami platformy .NET](https://www.nuget.org/packages/Azure.Batch/) pakietu i hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pakietu.

Uwzględnij następujące elementy hello `using` instrukcje w kodzie:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Witaj odwołanie do punktu końcowego usługi Azure AD w kodzie, w tym hello dzierżawy identyfikatora. Przy użyciu nazwy głównej usługi, należy podać punktu końcowego specyficznego dla dzierżawy. tooretrieve hello Identyfikatora dzierżawcy, wykonaj czynności hello opisane w temacie [uzyskanie Identyfikatora dzierżawy hello usługi Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Odwołanie hello partii zasobu punktu końcowego usługi:  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Odwołanie konta partii zadań:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Określ identyfikator aplikacji hello (identyfikator klienta) dla aplikacji. Identyfikator aplikacji Hello jest dostępny z rejestracji aplikacji w portalu Azure hello:

```csharp
private const string ClientId = "<application-id>";
```

Określ klucz tajny hello skopiowany z portalu Azure hello:

```csharp
private const string ClientKey = "<secret-key>";
```

Zapis token uwierzytelniania hello tooacquire metody wywołania zwrotnego z usługi Azure AD. Witaj **GetAuthenticationTokenAsync** metody wywołania zwrotnego pokazane wywołań biblioteki ADAL do uwierzytelniania instalacji nienadzorowanej:

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

Utworzyć **BatchTokenCredentials** obiekt, który przyjmuje hello delegata jako parametr. Użyj tych poświadczeń tooopen **BatchClient** obiektu. Następnie można użyć który **BatchClient** obiektu dla kolejnych operacji względem hello usługa partia zadań:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat usługi Azure AD, zobacz hello [Azure Active Directory dokumentacji](https://docs.microsoft.com/azure/active-directory/). Szczegółowe przykłady, pokazujący, jak są dostępne w hello toouse ADAL [przykłady kodu Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteki.

toolearn więcej informacji na temat nazwy główne usług, zobacz [aplikacji i usług obiektów principal w usłudze Azure Active Directory](../active-directory/develop/active-directory-application-objects.md). toocreate główną usługi za pomocą hello Azure portalu, zobacz [toocreate portalu aplikacji usługi Active Directory i nazwy głównej usługi, który ma dostęp do zasobów](../resource-group-create-service-principal-portal.md). Można również utworzyć nazwy głównej usługi z programu PowerShell lub interfejsu wiersza polecenia platformy Azure. 

aplikacje do zarządzania partii tooauthenticate przy użyciu usługi Azure AD, zobacz [rozwiązań do zarządzania partii uwierzytelniania z usługi Active Directory](batch-aad-auth-management.md). 

[aad_about]: ../active-directory/active-directory-whatis.md "Co to jest usługa Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenariusze uwierzytelniania dla usługi Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrowanie aplikacji z usługą Azure Active Directory"
[azure_portal]: http://portal.azure.com
