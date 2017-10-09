---
title: "aaaConfigure usługi Zarządzanie interfejsami API przy użyciu narzędzia Git - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosave i skonfigurować konfiguracji usługi Zarządzanie interfejsami API przy użyciu narzędzia Git."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a>Jak toosave i skonfigurować konfiguracji usługi Zarządzanie interfejsami API przy użyciu narzędzia Git
> 
> 

Każde wystąpienie usługi Zarządzanie interfejsami API utrzymuje bazę danych konfiguracji, który zawiera informacje o konfiguracji hello i metadanych dla wystąpienia usługi hello. Można wprowadzać zmiany wystąpienie usługi toohello przez zmianę ustawień w portalu wydawcy hello, za pomocą polecenia cmdlet programu PowerShell lub wywołania interfejsu API REST. Ponadto toothese metod, można również zarządzać konfiguracji wystąpienia usługi przy użyciu narzędzia Git, takie jak włączanie scenariusze zarządzania usługi:

* Przechowywanie wersji konfiguracji — Pobierz i przechowywać różne wersje konfiguracji usługi
* Zbiorcze zmiany konfiguracji — zmiany toomultiple części konfiguracji usługi w lokalnym repozytorium i integracji serwera zapasowego toohello zmiany hello z jednej operacji
* Znanego łańcuch narzędzi Git i przepływ pracy - Użyj narzędzia Git hello i przepływów pracy, które znasz już

powitania po diagram zawiera omówienie tooconfigure różne sposoby hello wystąpienia usługi Zarządzanie interfejsami API.

![Skonfiguruj Git][api-management-git-configure]

Podczas wprowadzania zmian usługi tooyour przy użyciu portalu wydawcy hello, poleceń cmdlet programu PowerShell lub interfejsu API REST hello zarządza bazą danych konfiguracji usługi za pomocą hello `https://{name}.management.azure-api.net` punktu końcowego, jak pokazano na powitania po prawej stronie powitania diagramu. Hello lewej hello diagram ilustruje sposób zarządzania konfiguracji usługi przy użyciu narzędzia Git i repozytorium Git dla usługi znajduje się w `https://{name}.scm.azure-api.net`.

Witaj, wykonaj czynności udostępnia przegląd zarządzania wystąpienia usługi Zarządzanie interfejsami API przy użyciu narzędzia Git.

1. Konfiguracja Git dostępu w usłudze
2. Zapisz repozytorium Git tooyour bazy danych konfiguracji usługi
3. Klonowanie maszyny lokalnej tooyour repozytorium Git hello
4. Pobierać najnowsze repozytorium hello dół tooyour komputera lokalnego i zatwierdzania i wypychania repozytorium wstecz tooyour zmiany
5. Wdrażanie hello zmiany z Twojego repozytorium do bazy danych konfiguracji usługi

W tym artykule opisano sposób tooenable znajdują się informacje na powitania pliki i foldery w repozytorium Git hello i użyj Git toomanage konfiguracji usługi.

## <a name="access-git-configuration-in-your-service"></a>Konfiguracja Git dostępu w usłudze
Wyświetlając ikonę Git hello w hello prawym górnym rogu portalu wydawcy hello można szybko wyświetlić stan hello konfiguracji Git. W tym przykładzie hello komunikatu o stanie wskazuje, że istnieją niezapisane zmiany toohello repozytorium. Jest to spowodowane hello bazy danych konfiguracji usługi API Management nie został jeszcze zapisany toohello repozytorium.

![Stan Git][api-management-git-icon-enable]

tooview i skonfigurować ustawienia konfiguracji Git, możesz kliknąć ikonę Git hello, lub kliknij hello **zabezpieczeń** menu i przejdź toohello **repozytorium konfiguracji** kartę.

![Włącz GIT][api-management-enable-git]

> [!IMPORTANT]
> Wszystkie klucze tajne, które nie są zdefiniowane jako właściwości będą przechowywane w repozytorium hello i pozostanie w jego historii dopóki Wyłącz i ponownie włączyć dostęp Git. Właściwości zapewniają toomanage bezpiecznym miejscu stałych wartości ciągów, tym klucze tajne, we wszystkich Konfiguracja interfejsu API i zasady, dzięki czemu nie trzeba toostore bezpośrednio w deklaracji z zasad. Aby uzyskać więcej informacji, zobacz [jak właściwości toouse w ramach zasad usługi Azure API Management](api-management-howto-properties.md).
> 
> 

Aby uzyskać informacji na temat włączania lub wyłączania dostępu Git przy użyciu hello interfejsu API REST, zobacz [Włączanie lub wyłączanie dostępu Git przy użyciu interfejsu API REST hello](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a>repozytorium Git toohello toosave hello usługi konfiguracji
pierwszym krokiem Hello przed klonowanie repozytorium hello jest toosave hello bieżący stan hello usługi konfiguracji toohello repozytorium. Kliknij przycisk **Zapisz konfigurację toorepository**.

![Zapisywanie konfiguracji][api-management-save-configuration]

Żądane zmiany na ekranie potwierdzenia hello, a następnie kliknij przycisk **Ok** toosave.

![Zapisywanie konfiguracji][api-management-save-configuration-confirm]

Po kilku chwilach konfiguracji hello jest zapisywana i wyświetlany jest stan konfiguracji hello hello repozytorium, w tym hello Data i godzina ostatniej zmiany konfiguracji hello i hello ostatniej synchronizacji konfiguracji usługi hello hello repozytorium.

![Stan konfiguracji][api-management-configuration-status]

Po zapisaniu repozytorium toohello hello konfiguracji mogą być klonowane.

Informacje na wykonanie tej operacji przy użyciu hello interfejsu API REST, zobacz [konfiguracji zatwierdzania migawki za pomocą interfejsu API REST hello](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).

## <a name="tooclone-hello-repository-tooyour-local-machine"></a>komputer lokalny tooyour tooclone hello repozytorium
tooclone repozytorium należy hello adresu URL tooyour repozytorium, nazwę użytkownika i hasła. Witaj nazwę użytkownika i adres URL są wyświetlane u góry hello hello **repozytorium konfiguracji** kartę.

![Klonowania Git][api-management-configuration-git-clone]

Witaj hasło jest generowane u dołu hello hello **repozytorium konfiguracji** kartę.

![Generowanie hasła][api-management-generate-password]

toogenerate hasła, najpierw upewnij się, że hello **wygaśnięcia** ustawić toohello potrzeby datę i godzinę wygaśnięcia, a następnie kliknij przycisk **Generuj Token**.

![Hasło][api-management-password]

> [!IMPORTANT]
> Zanotuj to hasło. Po wyjściu to hasło hello strona nie zostanie ponownie wyświetlone.
> 
> 

Następujące przykłady użycia hello Git Bash Hello narzędzia z [Git dla systemu Windows](http://www.git-scm.com/downloads) , ale można użyć dowolnego narzędzia Git, które znasz.

Otwórz narzędzie Git w folderze żądaną hello i uruchom hello następujące polecenia tooclone hello git repozytorium tooyour komputera lokalnego, za pomocą polecenia hello udostępnionych przez portal wydawcy hello.

```
git clone https://bugbashdev4.scm.azure-api.net/
```

Podaj hello nazwę użytkownika i hasło po wyświetleniu monitu.

Jeśli wystąpią błędy, spróbuj zmodyfikować Twoje `git clone` polecenia tooinclude hello użytkownika nazwę i hasło, jak pokazano w hello poniższy przykład.

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

Jeśli to zawiera błąd, spróbuj kodowania hello hasła część polecenia hello URL. Jeden toodo szybko to tooopen programu Visual Studio, a problem hello następujące polecenie w hello **oknie bezpośrednim**. tooopen hello **oknie bezpośrednim**, otwórz dowolnego rozwiązania lub projektu w programie Visual Studio (lub Utwórz nową aplikację konsoli puste) i wybierz polecenie **Windows**, **Immediate** z Witaj **debugowania** menu.

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

Użyj hasła hello zakodowany oraz użytkownika nazwę i repozytorium lokalizacji tooconstruct hello git polecenia.

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

Gdy jest sklonować repozytorium hello można przeglądać i pracę z nią w lokalnym systemie plików. Aby uzyskać więcej informacji, zobacz [plików i folderów odniesienia lokalnego repozytorium Git struktury](#file-and-folder-structure-reference-of-local-git-repository).

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a>tooupdate repozytorium lokalne powitania najbardziej bieżącej konfiguracji wystąpienia usługi
Jeśli wystąpienie usługi Zarządzanie interfejsami API tooyour zmian w portalu wydawcy hello lub przy użyciu interfejsu API REST hello, musisz zapisać te zmiany toohello repozytorium przed zaktualizowaniem lokalnym repozytorium z hello najnowsze zmiany. toodo tego, kliknij **Zapisz konfigurację toorepository** na powitania **repozytorium konfiguracji** karcie w portalu wydawcy hello, a następnie wystawiania hello następujące polecenie w lokalnym repozytorium.

```
git pull
```

Przed uruchomieniem `git pull` upewnij się, że są w folderze hello dla lokalnego repozytorium. Jeśli został ukończony hello `git clone` polecenia, a następnie należy zmienić hello katalogu tooyour repozytorium, uruchamiając polecenie, takie jak następujące hello.

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a>zmiany toopush Twojego repozytorium lokalnego repozytorium toohello serwera
toopush zmiany z repozytorium lokalnego repozytorium toohello serwera, należy zatwierdzić zmiany, a następnie Wypchnij je toohello serwera repozytorium. toocommit zmiany, otwórz Git narzędzia polecenia przełącznika toohello katalogu lokalnego repozytorium, a problem hello następujące polecenia.

```
git add --all
git commit -m "Description of your changes"
```

zatwierdza wszystkie hello toohello serwera Uruchom toopush hello następujące polecenia.

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a>toodeploy wszystkie wystąpienia usługi konfiguracji zmiany toohello zarządzanie interfejsami API usługi
Po zatwierdzeniu zmiany lokalne repozytorium serwera toohello zatwierdzonej i wypychanie, można je wdrożyć wystąpienie usługi Zarządzanie interfejsami API tooyour.

![Wdrażanie][api-management-configuration-deploy]

Informacje na wykonanie tej operacji przy użyciu hello interfejsu API REST, zobacz [wdrażanie Git zmienia tooconfiguration bazy danych przy użyciu interfejsu API REST hello](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a>Odwołanie struktury plików i folderów z lokalnego repozytorium Git
Hello pliki i foldery w repozytorium git lokalne powitania zawierają hello informacji konfiguracyjnych dotyczących hello wystąpienie usługi.

| Element | Opis |
| --- | --- |
| Folder główny zarządzanie interfejsami api |Zawiera konfigurację najwyższego poziomu hello wystąpienia usługi |
| interfejsy API folderu |Zawiera konfigurację hello hello interfejsów API w wystąpieniu usługi hello |
| folder grupy |Zawiera konfigurację hello hello grup w wystąpieniu usługi hello |
| folder zasady |Zawiera zasady hello w wystąpieniu usługi hello |
| portalStyles folder |Zawiera konfigurację hello Dostosowywanie portalu deweloperów hello w wystąpieniu usługi hello |
| folder produktów |Zawiera konfigurację hello hello produktów w wystąpieniu usługi hello |
| folder szablonów |Zawiera konfigurację hello hello szablonów wiadomości e-mail w wystąpieniu usługi hello |

Każdego folderu może zawierać jeden lub więcej plików, a w niektórych przypadkach jeden lub więcej folderów, na przykład folderu dla każdego interfejsu API, produktu lub grupy. Hello pliki w tych folderach są specyficzne dla typu jednostki hello opisanego przez hello nazwę folderu.

| Typ pliku | Przeznaczenie |
| --- | --- |
| JSON |Informacje o konfiguracji dotyczące hello odpowiednich jednostek |
| HTML |Opisy jednostek hello, często są wyświetlane w portalu dla deweloperów hello |
| xml |Instrukcje zasad |
| CSS |Arkusze stylów do dostosowania portalu dla deweloperów |

Tych plików można można utworzyć, usunąć edytować i zarządzane w lokalnym systemie plików, a zmiany hello wdrożone wstecz toohello wystąpienia usługi Zarządzanie interfejsami API.

> [!NOTE]
> Witaj następujące jednostek nie są zawarte w repozytorium Git hello i nie można skonfigurować przy użyciu narzędzia Git.
> 
> * Użytkownicy
> * Subskrypcje
> * Właściwości
> * Jednostek portalu deweloperów innych niż style
> 
> 

### <a name="root-api-management-folder"></a>Folder główny zarządzanie interfejsami api
główny Hello `api-management` folder zawiera `configuration.json` plik zawierający informacje najwyższego poziomu o wystąpienie usługi hello w hello zgodny z formatem.

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

Witaj pierwsze cztery ustawienia (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, i `UserRegistrationTermsConsentRequired`) mapy toohello następujące ustawienia na powitania **tożsamości** kartę w hello **zabezpieczeń** sekcji.

| Ustawienia tożsamości | Mapuje zbyt|
| --- | --- |
| RegistrationEnabled |**Przekierować użytkowników anonimowych toosign w stronę** wyboru |
| UserRegistrationTerms |**Warunki użytkowania w rejestracji użytkownika** pole tekstowe |
| UserRegistrationTermsEnabled |**Pokaż warunki użytkowania na stronie rejestracja** wyboru |
| UserRegistrationTermsConsentRequired |**Wymagaj zgody** wyboru |

![Ustawienia tożsamości][api-management-identity-settings]

Witaj obok czterech ustawień (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, i `DelegationValidationKey`) mapy toohello następujące ustawienia na powitania **delegowania** kartę w hello **zabezpieczeń** sekcji.

| Ustawienie delegowania | Mapuje zbyt|
| --- | --- |
| DelegationEnabled |**Delegat logowania & zapisywania** wyboru |
| DelegationUrl |**Adres URL punktu końcowego delegowania** pole tekstowe |
| DelegatedSubscriptionEnabled |**Delegowanie subskrypcji produktu** wyboru |
| DelegationValidationKey |**Delegowanie klucz sprawdzania poprawności** pole tekstowe |

![Ustawienia delegowania][api-management-delegation-settings]

Witaj końcowego ustawienie `$ref-policy`, mapy pliku instrukcje globalne zasady toohello hello wystąpienia usługi.

### <a name="apis-folder"></a>interfejsy API folderu
Witaj `apis` folder zawiera folder dla każdego interfejsu API w wystąpieniu usługi hello zawierającą hello następujące elementy.

* `apis\<api name>\configuration.json`-to jest Konfiguracja hello hello interfejsu API i zawiera informacje o operacji hello i adres URL usługi zaplecza hello. Jest to hello informacje, które będzie zwracany, jeśli zostały toocall [pobrania określonego interfejsu API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) z `export=true` w `application/json` format.
* `apis\<api name>\api.description.html`-to jest opis hello hello interfejsu API i odpowiada toohello `description` właściwości hello [jednostki interfejsu API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).
* `apis\<api name>\operations\`— Ten folder zawiera `<operation name>.description.html` plików, które mapują toohello operacje w hello interfejsu API. Każdy plik zawiera opis hello jednej operacji w hello interfejsu API, który mapuje toohello `description` właściwości hello [operacji jednostki](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) w hello interfejsu API REST.

### <a name="groups-folder"></a>folder grupy
Witaj `groups` folder zawiera folder dla każdej grupy zdefiniowanej w hello wystąpienie usługi.

* `groups\<group name>\configuration.json`-to jest Konfiguracja hello hello grupy. Jest to hello informacje, które będzie zwracany, jeśli zostały toocall hello [pobrać określonej grupy](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operacji.
* `groups\<group name>\description.html`-to jest hello opis grupy hello i odpowiada toohello `description` właściwości hello [grupy jednostki](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).

### <a name="policies-folder"></a>folder zasady
Witaj `policies` folder zawiera hello zasad instrukcje dla swojego wystąpienia usługi.

* `policies\global.xml`-zawiera zasady zdefiniowane w zakresie globalnym wystąpienia usługi.
* `policies\apis\<api name>\`— Jeśli masz wszystkie zasady zdefiniowane w zakresie interfejsu API są zawarte w tym folderze.
* `policies\apis\<api name>\<operation name>\`folder — Jeśli masz wszystkie zasady zdefiniowane w zakresie operacji są zawarte w tym folderze `<operation name>.xml` plików, które mapują toohello deklaracji zasad dla każdej operacji.
* `policies\products\`— Jeśli masz wszystkie zasady zdefiniowane w zakresie produktu są zawarte w tym folderze, który zawiera `<product name>.xml` plików, które mapują toohello deklaracji zasad dla każdego produktu.

### <a name="portalstyles-folder"></a>portalStyles folder
Witaj `portalStyles` folder zawiera konfigurację i styl arkusze Dostosowywanie portalu deweloperów hello wystąpienia usługi.

* `portalStyles\configuration.json`-zawiera nazwy hello arkuszy stylów hello używane przez hello portalu dla deweloperów
* `portalStyles\<style name>.css`-każdego `<style name>.css` plik zawiera style portalu dla deweloperów hello (`Preview.css` i `Production.css` domyślnie).

### <a name="products-folder"></a>folder produktów
Witaj `products` folder zawiera folder dla każdego produktu zdefiniowane w hello wystąpienie usługi.

* `products\<product name>\configuration.json`-to jest Konfiguracja hello hello produktu. Jest to hello informacje, które będzie zwracany, jeśli zostały toocall hello [pobrania określonego produktu](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operacji.
* `products\<product name>\product.description.html`-to jest opis hello hello produktu i odpowiada toohello `description` właściwości hello [jednostki produktu](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) w hello interfejsu API REST.

### <a name="templates"></a>szablonów
Witaj `templates` folder zawiera konfigurację hello [szablonów wiadomości e-mail](api-management-howto-configure-notifications.md) hello wystąpienia usługi.

* `<template name>\configuration.json`-to jest Konfiguracja hello hello szablonu wiadomości e-mail.
* `<template name>\body.html`-to jest treść hello hello szablon wiadomości e-mail.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać informacje o innych sposobów toomanage wystąpienia usługi, zobacz:

* Zarządzanie za pomocą następującego polecenia cmdlet programu PowerShell hello wystąpienia usługi
  * [Wdrożenie usługi dokumentacji poleceń cmdlet programu PowerShell](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [Zarządzanie usługami dokumentacji poleceń cmdlet programu PowerShell](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* Zarządzaj w portalu wydawcy hello wystąpienia usługi
  * [Zarządzanie pierwszym interfejsem API](api-management-get-started.md)
* Zarządzanie za pomocą interfejsu API REST hello wystąpienia usługi
  * [Dokumentacja interfejsu API REST zarządzania interfejsu API](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a>Obejrzyj film wideo
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




