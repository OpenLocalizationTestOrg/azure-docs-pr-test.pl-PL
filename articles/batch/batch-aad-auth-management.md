---
title: "rozwiązania do zarządzania partii tooauthenticate aaaUse usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Aplikacji skompilowanej za pomocą usługi Azure resource manager i dostawca zasobów partii hello uwierzytelniania za pomocą usługi Azure AD."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a>Uwierzytelnianie rozwiązań do zarządzania partii z usługą Active Directory

Aplikacje, które wywołują usługi zarządzania usługi partia zadań Azure hello uwierzytelniania za pomocą [usługi Azure Active Directory] [ aad_about] (Azure AD). Usługi Azure AD jest katalog wielu dzierżawców w chmurze firmy Microsoft i tożsamość usługi zarządzania. Azure sam używa usługi Azure AD do uwierzytelniania hello swoich klientów, Administratorzy usługi i użytkowników w organizacji.

Biblioteka zarządzania partiami platformy .NET Hello ujawnia typy do pracy z kontami partii, klucze konta, aplikacje i pakiety aplikacji. Biblioteka zarządzania partiami platformy .NET Hello jest klientem dostawcy zasobów platformy Azure i jest używany razem z [usługi Azure Resource Manager] [ resman_overview] toomanage tych zasobów programowo. Usługi Azure AD jest żądań tooauthenticate wymagane przez dowolnego klienta dostawcy zasobów platformy Azure, w tym hello biblioteki zarządzania partiami platformy .NET oraz [usługi Azure Resource Manager][resman_overview].

W tym artykule firma Microsoft eksplorowania przy użyciu usługi Azure AD tooauthenticate przez aplikacje korzystające z biblioteki zarządzania partiami platformy .NET hello. Zostanie przedstawiony sposób tooauthenticate toouse usługi Azure AD administratora subskrypcji lub administratora współpracującego przy użyciu zintegrowanego uwierzytelniania. Używamy hello [AccountManagment] [ acct_mgmt_sample] przykładowy projekt, dostępne w witrynie GitHub, toowalk hello biblioteki zarządzania partiami platformy .NET przy użyciu usługi Azure AD.

toolearn więcej informacji na temat przy użyciu biblioteki zarządzania partiami platformy .NET hello i przykładowe AccountManagement hello, zobacz [konta usługi partia zadań zarządzania i przydziały hello biblioteki klienta usługi partia zadań zarządzania dla platformy .NET](batch-management-dotnet.md).

## <a name="register-your-application-with-azure-ad"></a>Zarejestrować aplikację w usłudze Azure AD

Hello Azure [biblioteki uwierzytelniania usługi Active Directory] [ aad_adal] (ADAL) udostępnia interfejs programistyczny tooAzure AD do użycia w aplikacjach. toocall biblioteki ADAL z aplikacji, musisz zarejestrować aplikację w dzierżawie usługi Azure AD. Podczas rejestrowania aplikacji, podanych usługi Azure AD z informacjami o aplikacji, łącznie z jej nazwę w ramach dzierżawy usługi Azure AD hello. Następnie usługi Azure AD zapewnia identyfikator aplikacji używanie tooassociate aplikacji z usługą Azure AD w czasie wykonywania. toolearn więcej informacji na temat hello identyfikator aplikacji, zobacz [aplikacji i usług obiektów principal w usłudze Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

Witaj tooregister AccountManagement przykładowej aplikacji, wykonaj kroki hello hello [Dodawanie aplikacji](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sekcji [Integrowanie aplikacji z usługą Azure Active Directory] [ aad_integrate]. Określ **natywną aplikację kliencką** hello typu aplikacji. Witaj branżowy standard OAuth 2.0 Identyfikator URI hello **identyfikator URI przekierowania** jest `urn:ietf:wg:oauth:2.0:oob`. Jednak można określić dowolny prawidłowy identyfikator URI (takich jak `http://myaccountmanagementsample`) dla hello **identyfikator URI przekierowania**, ponieważ nie jest konieczne toobe rzeczywistych punktu końcowego:

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

Po zakończeniu procesu rejestracji hello zostanie Zobacz identyfikator aplikacji hello oraz hello Identyfikatora obiektu (nazwy głównej usługi) dla aplikacji.  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a>Udzielić aplikacji tooyour dostępu do interfejsu API usługi Azure Resource Manager hello

Następnie należy toodelegate dostępu tooyour aplikacji toohello interfejsu API usługi Azure Resource Manager. Identyfikator Hello Azure AD dla hello interfejs API Menedżera zasobów jest **interfejs API zarządzania usługami Windows Azure**.

Wykonaj następujące kroki w portalu Azure hello:

1. W okienku nawigacji po lewej stronie powitania hello portalu Azure, wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**i kliknij przycisk **Dodaj**.
2. Wyszukaj nazwę aplikacji na liście hello rejestracji aplikacji hello:

    ![Wyszukaj nazwę aplikacji](./media/batch-aad-auth-management/search-app-registration.png)

3. Wyświetl hello **ustawienia** bloku. W hello **dostępu do interfejsu API** zaznacz **wymagane uprawnienia**.
4. Kliknij przycisk **Dodaj** tooadd nowe wymaganych uprawnień. 
5. W kroku 1, wprowadź **interfejs API zarządzania usługami Windows Azure**, wybierz z listy hello wyników tego interfejsu API i kliknij hello **wybierz** przycisku.
6. W kroku 2, wybierz hello pole wyboru obok zbyt**Access Azure klasycznego modelu wdrażania jako użytkowników w organizacji**i kliknij przycisk hello **wybierz** przycisku.
7. Kliknij przycisk hello **gotowe** przycisku.

Witaj **wymagane uprawnienia** bloku teraz pokazuje, że aplikacja tooyour uprawnienia zostały przyznane tooboth hello ADAL i interfejsów API Menedżera zasobów. Uprawnienia są przyznawane tooADAL domyślnie podczas rejestrowania aplikacji z usługą Azure AD.

![Delegowanie uprawnień toohello interfejsu API usługi Azure Resource Manager](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a>Punkty końcowe systemu Azure AD

tooauthenticate Twojego rozwiązania do zarządzania partii z usługą Azure AD, będą potrzebne dwa punkty końcowe dobrze znany.

- Witaj **wspólnego punktu końcowego usługi Azure AD** dostarcza poświadczenia ogólnego zbierania interfejsu po określonym dzierżawcy nie zostanie podany, tak jak przypadku hello zintegrowanego uwierzytelniania:

    `https://login.microsoftonline.com/common`

- Witaj **punktu końcowego usługi Azure Resource Manager** jest używane tooacquire token dla usługi zarządzania partii toohello żądań uwierzytelniania:

    `https://management.core.windows.net/`

Witaj AccountManagement przykładowej aplikacji definiuje stałe dla tych punktów końcowych. Pozostaw te stałe, bez zmian:

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a>Odwołanie do Identyfikatora aplikacji 

Aplikacja kliencka używa tooaccess identyfikator (również określonego tooas hello identyfikator klienta) aplikacji hello Azure AD w czasie wykonywania. Aplikacji został zarejestrowany w portalu Azure hello, zaktualizuj kod toouse hello aplikacji Identyfikatora dostarczane przez usługę Azure AD w zarejestrowany aplikacji. W hello AccountManagement przykładowej aplikacji skopiuj swój identyfikator aplikacji z stała odpowiednie hello toohello portalu Azure:

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
Kopiuje też hello przekierowania URI, które zostały określone podczas procesu rejestracji hello. Witaj przekierowania określony w kodzie identyfikator URI musi być zgodna hello przekierowania URI podane podczas rejestrowania aplikacji hello.

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a>Uzyskanie tokenu uwierzytelniania usługi Azure AD

Po zarejestrować próbkę AccountManagement hello w dzierżawie usługi Azure AD hello i zaktualizować hello przykładowy kod źródłowy własnymi wartościami próbki hello jest gotowy tooauthenticate przy użyciu usługi Azure AD. Po uruchomieniu próbki hello hello ADAL prób tooacquire tokenu uwierzytelniania. W tym kroku monituje o podanie poświadczeń Microsoft: 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

Po podaniu poświadczeń hello przykładowej aplikacji przejść tooissue uwierzytelnić żądania toohello usługa partia zadań zarządzania. 

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat uruchamiania hello [AccountManagement przykładowej aplikacji][acct_mgmt_sample], zobacz [konta usługi partia zadań zarządzania i przydziały hello biblioteki klienta usługi partia zadań zarządzania dla platformy .NET](batch-management-dotnet.md).

toolearn więcej informacji na temat usługi Azure AD, zobacz hello [Azure Active Directory dokumentacji](https://docs.microsoft.com/azure/active-directory/). Szczegółowe przykłady, pokazujący, jak są dostępne w hello toouse ADAL [przykłady kodu Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteki.

aplikacje usług partii tooauthenticate przy użyciu usługi Azure AD, zobacz [rozwiązań usług uwierzytelniania partii z usługą Active Directory](batch-aad-auth.md). 


[aad_about]: ../active-directory/active-directory-whatis.md "Co to jest usługa Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenariusze uwierzytelniania dla usługi Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrowanie aplikacji z usługą Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
