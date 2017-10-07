---
title: "Usługa Azure Active Directory B2C: Narzędzie Pomocnik dostosowania strony interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Narzędzie Pomocnik użyć funkcji dostosowywania toodemonstrate hello strony interfejsu użytkownika w usłudze Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: ae935d52-3520-4a94-b66e-b35bb40e7514
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: swkrish
ms.openlocfilehash: 5137ac112019369b4244a925df1acb96fefb758f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-a-helper-tool-used-toodemonstrate-hello-page-user-interface-ui-customization-feature"></a>Usługa Azure Active Directory B2C: Narzędzie Pomocnik użyć funkcji dostosowanie interfejsu użytkownika strony toodemonstrate hello
W tym artykule jest toohello Pomocnika [główny artykuł dostosowania interfejsu użytkownika](active-directory-b2c-reference-ui-customization.md) w usłudze Azure Active Directory (Azure AD) B2C. Witaj poniższych krokach opisano sposób tooexercise przy użyciu zawartość HTML i CSS przykładową, która przygotowaliśmy hello funkcji dostosowywania interfejsu użytkownika strony.

## <a name="get-an-azure-ad-b2c-tenant"></a>Uzyskiwanie dzierżawy usługi Azure AD B2C
Przed dostosowaniem niczego, konieczne będzie zbyt[uzyskać dzierżawę usługi Azure AD B2C](active-directory-b2c-get-started.md) Jeśli nie został wcześniej.

## <a name="create-a-sign-up-or-sign-in-policy"></a>Tworzenie zasad rejestracji i logowania
Hello zawartość przykładową przygotowaliśmy mogą być używane toocustomze dwóch stron w [zasad rejestracji i logowania](active-directory-b2c-reference-policies.md): hello [ujednoliconego strony logowania](active-directory-b2c-reference-ui-customization.md) i hello [własnym potwierdzona atrybuty strony](active-directory-b2c-reference-ui-customization.md). Gdy [tworzenia zasad dotyczących tworzenia konta lub logowanie](active-directory-b2c-reference-policies.md#create-a-sign-up-or-sign-in-policy), Dodaj konta lokalnego (adres e-mail), Facebook, Google i Microsoft jako **dostawców tożsamości**. Są one hello tylko IDPs akceptujących naszej próbki zawartość HTML.  Jeśli chcesz, możesz także dodać podzbiór tych IDPs.

## <a name="register-an-application"></a>Rejestrowanie aplikacji
Konieczne będzie zbyt[zarejestrować aplikację](active-directory-b2c-app-registration.md) w Twojej B2C dzierżawy, który może być używane tooexecute zgodnie z zasadami. Po zarejestrowaniu aplikacji, masz kilka opcji służy tooactually Uruchom zasadach rejestracji:

* Tworzenie jednej z aplikacji szybki start opisane w sekcji hello "wprowadzenie" hello Azure AD B2C [podpisywania i logowanie użytkowników w twoich aplikacjach](active-directory-b2c-overview.md#get-started).
* Użyj hello wstępnie skompilowany [Plac zabaw dla usługi Azure AD B2C](https://aadb2cplayground.azurewebsites.net) aplikacji. Jeśli wybierzesz toouse hello Plac zabaw dla musi zarejestrować aplikację w dzierżawie usługi B2C przy użyciu hello **identyfikator URI przekierowania** `https://aadb2cplayground.azurewebsites.net/`.
* Użyj hello **Uruchom teraz** przycisk na zasady w hello [portalu Azure](https://portal.azure.com/).

## <a name="customize-your-policy"></a>Dostosuj zasady
toocustomize hello wyglądu i działania zasad, należy toofirst tworzenie plików HTML i CSS przy użyciu określonych konwencji hello Azure Active Directory B2C. Następnie możesz przekazać Twojej lokalizacji publicznej statycznej zawartości tooa tak, aby usługi Azure AD B2C do niego dostęp. Może być własną dedykowanym serwerze sieci web, magazyn obiektów Blob Azure, Azure Content Delivery Network lub wszelkie inne statyczne hosting zasobów dostawcy. Jedynymi wymogami Hello są czy zawartość jest dostępna za pośrednictwem protokołu HTTPS i jest możliwy przy użyciu mechanizmu CORS. Po zostały uwidocznione statycznej zawartości sieci hello web, można edytować zasady toopoint toothis lokalizacji, a które zawartości tooyour klientów. Witaj [główny artykuł dostosowania interfejsu użytkownika](active-directory-b2c-reference-ui-customization.md) opisano szczegółowo, jak działa funkcja dostosowywania hello Azure AD B2C.

Do celów tego samouczka hello opracowaliśmy już niektóre przykłady i hostowanej go w magazynie obiektów Blob Azure. zawartość przykładowej Hello jest bardzo proste dostosowania w motywie hello fikcyjnej firmy "Wingtip Toys". tootry go określone we własnych zasad, wykonaj następujące kroki:

1. Zaloguj się w dzierżawie tooyour na powitania [portalu Azure](https://portal.azure.com/) i przejdź do bloku funkcji toohello B2C.
2. Kliknij przycisk **zasad rejestracji i logowania** a następnie kliknij pozycję zasady (na przykład "b2c\_1\_znak\_się\_znak\_w").
3. Kliknij przycisk **dostosowywania interfejsu użytkownika strony** , a następnie **stronę tworzenia konta lub logowanie Unified**.
4. Przełącz hello **niestandardowe strony** przełącznika zbyt**tak**. W hello **strony niestandardowego identyfikatora URI** wprowadź `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/unified.html`. Kliknij przycisk **OK**.
5. Kliknij przycisk **stronę tworzenia konta lokalnego konta**. Przełącz hello **Użyj niestandardowego szablonu** przełącznika zbyt**tak**. W hello **strony niestandardowego identyfikatora URI** wprowadź `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/selfasserted.html`.
6. Hello Powtórz krok sam hello **strony rejestracji społecznościowych konta**.
   Kliknij przycisk **OK** dwukrotnie tooclose hello interfejsu użytkownika dostosowywanie bloków.
7. Kliknij pozycję **Zapisz**.

Teraz można wypróbować zasady niestandardowe. Jeśli chcesz, ale mogą także po prostu kliknij hello można użyć własnych aplikacji lub hello Azure AD B2C Plac zabaw dla **Uruchom teraz** polecenia w bloku zasad hello. Wybierz aplikację w polu listy rozwijanej hello i wybierz hello odpowiedniej przekierowania URI. Kliknij przycisk hello **Uruchom teraz** przycisku. Zostanie otwarty na nowej karcie przeglądarki i można uruchomić za pomocą interfejsu użytkownika hello skorzystania z aplikacji przy użyciu hello nowej zawartości w miejscu!

## <a name="upload-hello-sample-content-tooazure-blob-storage"></a>Przekazywanie zawartości tooAzure próbki hello magazynu obiektów Blob
Jeśli chcesz toohost magazynu obiektów Blob Azure toouse strony zawartości, można utworzyć konta magazynu i użyć naszych tooupload Narzędzie Pomocnik B2C plików.

### <a name="create-a-storage-account"></a>Tworzenie konta magazynu
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Kliknij przycisk **+ nowy** > **dane i magazyn** > **konta magazynu**. Konieczne będzie toocreate subskrypcji platformy Azure konta magazynu obiektów Blob Azure. Możesz utworzyć konto bezpłatnej wersji próbnej na powitania [witryny sieci Web Azure](https://azure.microsoft.com/pricing/free-trial/).
3. Podaj **nazwa** hello konta magazynu (na przykład "contoso") i wybierz hello opcji odpowiednich dla **warstwa cenowa**, **grupy zasobów** i  **Subskrypcja**. Upewnij się, że masz hello **tooStartboard numeru Pin** zaznaczoną opcją. Kliknij przycisk **Utwórz**.
4. Przejdź wstecz toohello tablicy startowej, a następnie kliknij przycisk hello konta magazynu, który został właśnie utworzony.
5. W hello **Podsumowanie** kliknij **kontenery**, a następnie kliknij przycisk **+ Dodaj**.
6. Podaj **nazwa** hello kontenera (na przykład "b2c") i wybierz **obiektu Blob** jako hello **dostęp typu**. Kliknij przycisk **OK**.
7. na liście hello na powitania pojawi się Hello kontenera, w którym utworzono **obiekty BLOB** bloku. Zanotuj adres URL hello kontenera hello; na przykład jego wygląd powinien być podobny zbyt`https://contoso.blob.core.windows.net/b2c`. Zamknij hello **obiekty BLOB** bloku.
8. W bloku konto magazynu hello, kliknij polecenie **klucze** i zanotuj wartości hello hello **nazwy konta magazynu** i **podstawowy klucz dostępu** pola.

> [!NOTE]
> **Podstawowy klucz dostępu** jest ważne poświadczenie zabezpieczeń.
> 
> 

### <a name="download-hello-helper-tool-and-sample-files"></a>Pobierz pliki narzędzia i próbki pomocnika hello
Możesz pobrać hello [magazyn obiektów Blob Azure pliki narzędzia i próbki pomocnika jako plik .zip](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip) lub sklonować go z witryny GitHub:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

To repozytorium zawiera `sample_templates\wingtip` katalogu, który zawiera przykład HTML, CSS i obrazy. W przypadku tych szablonów tooreference własnego konta magazynu obiektów Blob Azure będzie potrzebny tooedit hello HTML plików. Otwórz `unified.html` i `selfasserted.html` i Zastąp wszystkie wystąpienia `https://localhost` z adresem URL hello własne kontenera zapisaną w poprzednich krokach hello. Należy użyć hello ścieżka bezwzględna plików HTML, ponieważ w takim przypadku hello HTML zostanie obsłużona przez usługę Azure AD w domenie hello hello `https://login.microsoftonline.com`.

### <a name="upload-hello-sample-files"></a>Przekaż hello przykładowych plików
W hello na tym samym repozytorium, Rozpakuj `B2CAzureStorageClient.zip` i wykonywania hello `B2CAzureStorageClient.exe` pliku w ciągu. Ten program po prostu przekazać wszystkie pliki hello w katalogu hello Określ konto magazynu tooyour i włączyć CORS dostęp do tych plików. Po wykonaniu powyższych kroków hello hello HTML i pliki CSS będzie teraz wskazywać tooyour konta magazynu. Należy pamiętać, że hello nazwy konta magazynu należy hello poprzedzający `blob.core.windows.net`, na przykład `contoso`. Możesz sprawdzić, czy zawartość hello został przesłany poprawnie podejmując tooaccess `https://{storage-account-name}.blob.core.windows.net/{container-name}/wingtip/unified.html` w przeglądarce. Również użyć [http://test-cors.org/](http://test-cors.org/) toomake się, że zawartość hello jest teraz włączonego mechanizmu CORS. (Wyszukaj "stan XHR: 200" w wyniku hello.)

### <a name="customize-your-policy-again"></a>Dostosuj zasady, ponownie
Teraz, gdy przekazanego konta magazynu własnych zawartości tooyour próbki hello, należy edytować tooreference Twojego zasad rejestracji go. Powtórz kroki hello z hello ["Dostosować zgodnie z zasadami"](#customize-your-policy) sekcji powyżej, przy użyciu adresów URL swoje konto magazynu. Na przykład Witaj lokalizację użytkownika `unified.html` plik może być `<url-of-your-container>/wingtip/unified.html`.

Teraz można używać hello **Uruchom teraz** przycisku lub tooexecute własnych aplikacji z zasadami ponownie. Witaj wyników, należy poszukać prawie dokładnie hello sam — możesz użyć hello sam przykładowy HTML i CSS w obu przypadkach. Jednak zasad odwołuje się teraz wystąpienia magazynu obiektów Blob Azure i są tooedit wolnego i należy przekazać pliki hello ponownie jako. Dla więcej informacji na temat dostosowywania hello HTML i CSS, można znaleźć toohello [główny artykuł dostosowania interfejsu użytkownika](active-directory-b2c-reference-ui-customization.md).

