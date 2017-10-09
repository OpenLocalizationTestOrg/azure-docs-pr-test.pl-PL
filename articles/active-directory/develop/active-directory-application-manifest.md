---
title: Azure Active Directory Manifest aplikacji hello aaaUnderstanding | Dokumentacja firmy Microsoft
description: "Szczegółowe pokrycia manifest aplikacji usługi Azure Active Directory hello, który reprezentuje konfigurację tożsamości aplikacji w dzierżawie usługi Azure AD i jest używane toofacilitate autoryzacji OAuth, środowisko zgody i inne."
services: active-directory
documentationcenter: 
author: sureshja
manager: mbaldwin
editor: 
ms.assetid: 4804f3d4-0ff1-4280-b663-f8f10d54d184
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: sureshja
ms.custom: aaddev
ms.reviewer: elisol
ms.openlocfilehash: 096c9d5501edbfc08731fea670cee559d4442ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-azure-active-directory-application-manifest"></a>Opis manifestu aplikacji hello Azure Active Directory
Aplikacje, które integrują się z usługi Azure Active Directory (AD) musi być zarejestrowana w dzierżawie usługi Azure AD, zapewniając konfiguracji trwałe tożsamości dla aplikacji hello. Ta konfiguracja jest konsultacje w czasie wykonywania, włączanie scenariusze, które umożliwiają toooutsource i brokera uwierzytelniania/autoryzacji aplikacji za pomocą usługi Azure AD. Aby uzyskać więcej informacji na temat modelu aplikacji hello Azure AD, zobacz hello [Dodawanie, aktualizowanie i usuwanie aplikacji] [ ADD-UPD-RMV-APP] artykułu.

## <a name="updating-an-applications-identity-configuration"></a>Trwa aktualizowanie konfiguracji tożsamości aplikacji
Dostępne są faktycznie wiele opcji aktualizowania hello właściwości konfiguracji tożsamości aplikacji, które różnią się w funkcji i stopni trudności w tym następujących hello:

* Witaj  **[portalu Azure] [ AZURE-PORTAL] interfejs użytkownika sieci Web** pozwala tooupdate hello najbardziej typowych właściwości aplikacji. Jest to najszybszy hello i co najmniej błąd podatne sposób aktualizowania właściwości aplikacji, ale nie zapewniają pełny dostęp tooall właściwości, takie jak hello kolejnych dwóch metod.
* Dla bardziej zaawansowanych scenariuszy, w których należy tooupdate właściwości, które nie są widoczne w hello klasycznego portalu Azure, można zmodyfikować hello **manifest aplikacji**. To jest hello fokus w tym artykule i omówiono bardziej szczegółowo począwszy hello następnej sekcji.
* Możliwe jest również zbyt**napisać aplikację, która używa hello [interfejsu API programu Graph] [ GRAPH-API]**  tooupdate aplikacji, co wymaga hello większości wysiłku. Może to być atrakcyjną opcję, jeśli pisania oprogramowanie do zarządzania, lub potrzebujesz właściwości aplikacji tooupdate regularnie w zautomatyzowany sposób.

## <a name="using-hello-application-manifest-tooupdate-an-applications-identity-configuration"></a>Za pomocą tooupdate manifestu aplikacji hello konfiguracji tożsamości aplikacji
Za pomocą hello [portalu Azure][AZURE-PORTAL], można zarządzać konfiguracją tożsamości aplikacji, aktualizując za pomocą edytora manifestu wbudowanego hello manifest aplikacji hello. Można również pobrać i przekaż manifest aplikacji hello w formacie JSON. Nie rzeczywisty plik jest przechowywany w katalogu hello. Hello manifest aplikacji jest jedynie operacji HTTP GET w jednostce aplikacji hello Azure AD Graph API i hello przekazywania jest w jednostce aplikacji hello operacji HTTP PATCH.

W związku z tym w formacie hello toounderstand kolejności i właściwości manifest aplikacji hello, konieczne będzie hello tooreference interfejsu API programu Graph [jednostek aplikacji] [ APPLICATION-ENTITY] dokumentacji. Przykłady aktualizacje, które mogą być wykonywane, chociaż przekazywania manifest aplikacji:

* **Deklarowanie zakresy uprawnień (oauth2Permissions)** udostępnianych przez interfejs API sieci web. Zobacz temat "TooOther aplikacji ujawnianie interfejsów API sieci Web" hello w [integracji aplikacji z usługą Azure Active Directory] [ INTEGRATING-APPLICATIONS-AAD] informacje dotyczące implementacji personifikacji użytkownika za pomocą hello oauth2Permissions delegowane uprawnienia zakresu. Jak wspomniano wcześniej, właściwości jednostki aplikacji są udokumentowane w hello interfejsu API programu Graph [jednostki i typ złożony] [ APPLICATION-ENTITY] odwołanie do artykułu, w tym hello oauth2Permissions właściwość, która jest Kolekcja typu [OAuth2Permission][APPLICATION-ENTITY-OAUTH2-PERMISSION].
* **Deklarowanie ról aplikacji (appRoles) udostępniany przez aplikację**. Witaj Jednostka aplikacji appRoles właściwość jest kolekcją typu [roli aplikacji][APPLICATION-ENTITY-APP-ROLE]. Zobacz hello [oparta na rolach kontrola dostępu w aplikacji w chmurze przy użyciu usługi Azure AD] [ RBAC-CLOUD-APPS-AZUREAD] artykule przykład implementacji.
* **Deklarowanie znane klienta aplikacji (knownClientApplications)**, co pozwala użytkownikowi toologically grupie równych wartości hello zgodą hello określony klienta aplikacji toohello zasobów/interfejs API sieci web.
* **Żądania członkostwa w grupach tooissue usługi Azure AD oświadczeń** dla hello zalogowany użytkownik (groupMembershipClaims).  Może to być również skonfigurowany tooissue oświadczenia dotyczące użytkownika hello katalogu ról członkostwa. Zobacz hello [autoryzacji w aplikacji w chmurze za pomocą grup usługi AD] [ AAD-GROUPS-FOR-AUTHORIZATION] artykule przykład implementacji.
* **Zezwalaj OAuth 2.0 niejawne aplikacji grant w toosupport** przepływów (oauth2AllowImplicitFlow). Ten typ przepływu grant jest używany osadzony stron sieci web JavaScript lub jednej strony aplikacji JEDNOSTRONICOWEJ. Aby uzyskać więcej informacji na powitania udzielania autoryzacji niejawne, zobacz [hello opis OAuth2 niejawne Przyznaj przepływu w usłudze Azure Active Directory][IMPLICIT-GRANT].
* **Zezwalaj na używanie X509 certyfikatów jako klucz tajny hello** (keyCredentials). Zobacz hello [tworzenie aplikacji usługi i demon w usłudze Office 365] [ O365-SERVICE-DAEMON-APPS] i [tooauth przewodnik dewelopera programu z interfejsu API usługi Azure Resource Manager] [ DEV-GUIDE-TO-AUTH-WITH-ARM] artykuły Przykłady implementacji.
* **Dodaj nowy identyfikator URI aplikacji** aplikacji (identifierURIs[]). Identyfikatory URI Identyfikatora aplikacji są używane toouniquely zidentyfikować aplikację, w ramach swojej dzierżawy usługi Azure AD (lub między wiele dzierżaw usługi Azure AD, dla wielodostępnych scenariusze, w których kwalifikowana za pomocą zweryfikowanej domeny niestandardowej). Są one używane podczas żądania aplikacji zasobów tooa uprawnień, lub uzyskiwanie tokenu dostępu do zasobów aplikacji. Podczas aktualizacji tego elementu hello tę samą aktualizację następuje jednostki usługi odpowiedniego toohello servicePrincipalNames [] kolekcji znajduje się w aplikacji hello macierzystego dzierżawy.

Witaj manifest aplikacji zawiera również tootrack dobrze hello stanu rejestracji aplikacji. Ponieważ jest ona dostępna w formacie JSON, można sprawdzić reprezentacji pliku hello do kontroli źródła, wraz z kodu źródłowego aplikacji.

## <a name="step-by-step-example"></a>Krok przykładzie kroku
Teraz umożliwia przeprowadzenie tooupdate wymagane kroki hello konfiguracji tożsamości aplikacji za pomocą hello w manifeście aplikacji. Wyróżnione jedną hello poprzedzających przykłady, przedstawiający sposób toodeclare nowe uprawnienie zakresu w aplikacji zasobów:

1. Zaloguj się toohello [portalu Azure][AZURE-PORTAL].
2. Po uwierzytelniono, wybierz dzierżawy usługi Azure AD, wybierając ją z hello prawym górnym rogu strony hello.
3. Wybierz **usługi Azure Active Directory** rozszerzenia z lewego panelu nawigacji i kliknij na powitania **rejestracji aplikacji**.
4. Znajdź aplikacji hello tooupdate hello na liście i kliknij na nim.
5. Ze strony aplikacji hello, kliknij przycisk **manifestu** tooopen hello wbudowanego manifestu edytora. 
6. Można edytować bezpośrednio manifest hello przy użyciu tego edytora. Uwaga tego manifestu hello następuje hello schematu dla hello [jednostek aplikacji] [ APPLICATION-ENTITY] jak wspomniano wcześniej: na przykład przy założeniu chcemy tooimplement/Uwidacznianie nowe uprawnienie o nazwie "Employees.Read.All" w naszym zasobów aplikacji (API) należy po prostu dodać kolekcję element nowe/sekundę toohello oauth2Permissions ie:
   
        "oauth2Permissions": [
        {
        "adminConsentDescription": "Allow hello application tooaccess MyWebApplication on behalf of hello signed-in user.",
        "adminConsentDisplayName": "Access MyWebApplication",
        "id": "aade5b35-ea3e-481c-b38d-cba4c78682a0",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application tooaccess MyWebApplication on your behalf.",
        "userConsentDisplayName": "Access MyWebApplication",
        "value": "user_impersonation"
        },
        {
        "adminConsentDescription": "Allow hello application toohave read-only access tooall Employee data.",
        "adminConsentDisplayName": "Read-only access tooEmployee records",
        "id": "2b351394-d7a7-4a84-841e-08a6a17e4cb8",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application toohave read-only access tooyour Employee data.",
        "userConsentDisplayName": "Read-only access tooyour Employee records",
        "value": "Employees.Read.All"
        }
        ],
   
    wpis Hello musi być unikatowa, i w związku z tym należy wygenerować nowy globalnie unikatowego Identyfikatora (GUID) dla hello `"id"` właściwości. W takim przypadku ponieważ firma Microsoft określony `"type": "User"`, to uprawnienie można przyzwolenie tooby dowolnego konta uwierzytelnione przez hello dzierżawy usługi Azure AD, w których hello jest zarejestrowana aplikacja zasobów/interfejsu API. Tego przyznaje powitania klienta aplikacji uprawnienia tooaccess go w imieniu hello konta. ciągi Nazwa opis i wyświetlania Hello są używane podczas zgody i wyświetlane w portalu Azure hello.
6. Po zakończeniu aktualizowania manifest powitania kliknij **zapisać** toosave hello manifestu.  
   
Teraz, gdy hello manifestu jest zapisywany, można zezwolić zarejestrowanego klienta aplikacji dostępu toohello nowe dodane powyżej. Ten czas, których można używać hello interfejsu użytkownika sieci Web portalu Azure zamiast edycji manifest aplikacji hello klienta:  

1. Przejdź najpierw toohello **ustawienia** bloku hello toowhich aplikacji klienta mają tooadd dostępu toohello nowy interfejs API, kliknij przycisk **wymagane uprawnienia** i wybierz polecenie **wybierz interfejs API** .
2. Następnie użytkownik zobaczy hello listę zarejestrowanych zasobów aplikacji (API) w dzierżawie powitalnych. Kliknij przycisk hello zasobów aplikacji tooselect lub nazwę typu hello pole wyszukiwania hello aplikacji hello. Po znalezieniu aplikacji hello, kliknij przycisk **wybierz**.  
3. Spowoduje to przejście toohello **wybierz uprawnienia** strony, która wyświetli listę hello uprawnienia aplikacji i delegowane uprawnienia dostępne dla hello zasobów aplikacji. Wybierz hello nowe uprawnienie w kolejności tooadd go klienta toohello żądanej przez listę uprawnień. To nowe uprawnienie będą przechowywane w konfiguracji tożsamości aplikacji klienckiej hello we właściwości kolekcji "requiredResourceAccess" hello.


To już wszystko. Teraz aplikacji będzie uruchamiana za pomocą ich nowej konfiguracji tożsamości.

## <a name="next-steps"></a>Następne kroki
* Więcej szczegółów na powitania relacji między obiektów aplikacji i nazwę główną usługi dla aplikacji, zobacz [aplikacji i usług obiektów principal w usłudze Azure AD][AAD-APP-OBJECTS].
* Zobacz hello [słownik dewelopera usługi Azure AD] [ AAD-DEVELOPER-GLOSSARY] definicji niektórych koncepcje dla deweloperów usługi Azure Active Directory (AD) core hello.

Użyj sekcji komentarzy hello poniżej tooprovide opinii i pomóc nam dostosować i kształtu zawartość.

<!--article references -->
[AAD-APP-OBJECTS]: active-directory-application-objects.md
[AAD-DEVELOPER-GLOSSARY]: active-directory-dev-glossary.md
[AAD-GROUPS-FOR-AUTHORIZATION]: http://www.dushyantgill.com/blog/2014/12/10/authorization-cloud-applications-using-ad-groups/
[ADD-UPD-RMV-APP]: active-directory-integrating-applications.md
[APPLICATION-ENTITY]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[APPLICATION-ENTITY-APP-ROLE]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type
[APPLICATION-ENTITY-OAUTH2-PERMISSION]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type
[AZURE-PORTAL]: https://portal.azure.com
[DEV-GUIDE-TO-AUTH-WITH-ARM]: http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/
[GRAPH-API]: active-directory-graph-api.md
[IMPLICIT-GRANT]: active-directory-dev-understanding-oauth2-implicit-grant.md
[INTEGRATING-APPLICATIONS-AAD]: https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
[O365-PERM-DETAILS]: https://msdn.microsoft.com/office/office365/HowTo/application-manifest
[O365-SERVICE-DAEMON-APPS]: https://msdn.microsoft.com/office/office365/howto/building-service-apps-in-office-365
[RBAC-CLOUD-APPS-AZUREAD]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/

