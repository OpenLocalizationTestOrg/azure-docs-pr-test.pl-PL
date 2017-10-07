---
title: "Dostosowywanie interfejsu użytkownika za pomocą niestandardowych zasad — usługi Azure AD B2C | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat dostosowywania interfejsu użytkownika (UI), gdy użycie zasad niestandardowych w usłudze Azure AD B2C."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a>Usługa Azure Active Directory B2C: Konfigurowanie dostosowywania interfejsu użytkownika w zasadach niestandardowych

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Po zakończeniu pracy w tym artykule, konieczne będzie rejestracji i logowania zasady niestandardowe marki i wyglądu. Z usługi Azure Active Directory B2C (Azure AD B2C), możesz uzyskać prawie pełną kontrolę nad zawartość HTML i CSS hello który został przedstawiony toousers. Użycie zasad niestandardowych, należy skonfigurować dostosowywania interfejsu użytkownika w XML, zamiast za pomocą formantów w hello portalu Azure. 

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem należy wykonać [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md). Powinien mieć pracy niestandardowych zasad rejestracji i logowania z kontami lokalnymi.

## <a name="page-ui-customization"></a>Dostosowywanie interfejsu użytkownika strony

Za pomocą funkcji dostosowywania interfejsu użytkownika strony hello, można dostosować hello wygląd i działanie dowolne zasady niestandardowe. Można również utrzymać marki i wizualne spójności między aplikacji i usługi Azure AD B2C.

Oto jak to działa: usługi Azure AD B2C kod w przeglądarce klienta, korzysta z podejścia nowoczesnych o nazwie [udostępniania zasobów między źródłami (CORS)](http://www.w3.org/TR/cors/). Najpierw należy określić adres URL w zasadach niestandardowych hello z dostosowana zawartość HTML. Usługa Azure AD B2C scala elementy interfejsu użytkownika z hello zawartość HTML, który jest ładowany z danego adresu URL, a następnie wyświetla hello strony toohello klienta.

## <a name="create-your-html5-content"></a>Tworzenie sieci HTML5 zawartości

Tworzenie zawartości o nazwie markę produktu HTML w tytule hello.

1. Skopiuj powitania po fragment kodu HTML. Jest poprawnie sformułowanym HTML5 z pustego elementu o nazwie  *\<div id = "interfejsu api"\>\</DIV\>*  znajdujących się na powitania  *\<treści\>*  tagów. Ten element wskazuje, gdzie zawartość usługi Azure AD B2C jest toobe dodaje.

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   >Ze względów bezpieczeństwa hello użycie JavaScript jest obecnie zablokowany do dostosowania.

2. Wklej skopiowane hello fragment w edytorze tekstu, a następnie zapisz plik hello jako *dostosować ui.html*.

## <a name="create-an-azure-blob-storage-account"></a>Tworzenie konta magazynu obiektów Blob platformy Azure

>[!NOTE]
> W tym artykule używamy toohost magazynu obiektów Blob platformy Azure zawartość. Można wybrać toohost zawartości na serwerze sieci web, ale należy [włączenia CORS na serwerze sieci web](https://enable-cors.org/server.html).

toohost tę zawartość HTML w magazynie obiektów Blob hello następujące:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na powitania **Centrum** menu, wybierz opcję **nowy** > **magazynu** > **konta magazynu**.
3. Wprowadź unikatową **nazwa** dla konta magazynu.
4. **Model wdrażania** może pozostawać **Resource Manager**.
5. Zmień **rodzaj konta** za**magazynu obiektów Blob**.
6. **Wydajność** może pozostawać **standardowe**.
7. **Replikacja** może pozostawać **RA-GRS**.
8. **Warstwa dostępu** może pozostawać **gorąca**.
9. **Szyfrowanie usługi Magazyn** może pozostawać **wyłączone**.
10. Wybierz **subskrypcji** dla konta magazynu.
11. Utwórz **grupy zasobów** lub wybierz istniejący.
12. Wybierz hello **lokalizacji geograficznej** dla konta magazynu.
13. Kliknij przycisk **Utwórz** konta magazynu hello toocreate.  
    Po zakończeniu wdrażania hello hello **konta magazynu** automatycznie zostanie otwarty blok.

## <a name="create-a-container"></a>Tworzenie kontenera

toocreate publicznego kontenera w magazynie obiektów Blob hello następujące:

1. Kliknij przycisk hello **omówienie** kartę.
2. Kliknij przycisk **kontenera**.
3. Aby uzyskać **nazwa**, typ **$root**.
4. Ustaw **dostęp typu** za**obiektu Blob**.
5. Kliknij przycisk **$root** tooopen hello nowego kontenera.
6. Kliknij pozycję **Przekaż**.
7. Kliknij ikonę folderu hello obok zbyt**wybierz plik**.
8. Przejdź za**dostosować ui.html**, który został utworzony we wcześniejszej części hello [dostosowywania interfejsu użytkownika strony](#the-page-ui-customization-feature) sekcji.
9. Kliknij pozycję **Przekaż**.
10. Wybierz obiekt blob dostosować ui.html hello, który został przekazany.
11. Następny zbyt**adres URL**, kliknij przycisk **kopiowania**.
12. W przeglądarce hello Wklej skopiowany adres URL i odwiedź witrynę toohello. Jeśli witryna hello jest niedostępny, upewnij się, typ dostępu do kontenera hello ustawiono zbyt**obiektu blob**.

## <a name="configure-cors"></a>Konfigurowanie mechanizmu CORS

Skonfiguruj magazyn obiektów Blob współużytkowania zasobów między źródłami, wykonując następujące hello:

>[!NOTE]
>Chcesz tootry limit funkcji dostosowanie hello interfejsu użytkownika za pomocą naszej próbki zawartość HTML i CSS? Przygotowaliśmy [Narzędzie Pomocnik proste](active-directory-b2c-reference-ui-customization-helper-tool.md) który przekazuje i konfiguruje zawartość przykładowej na koncie magazynu obiektów Blob. Jeśli narzędzie hello przejść od razu zbyt[zmodyfikować zasady niestandardowe rejestracji i logowania](#modify-your-sign-up-or-sign-in-custom-policy).

1. Na powitania **magazynu** bloku, w obszarze **ustawienia**, otwórz **CORS**.
2. Kliknij pozycję **Dodaj**.
3. Aby uzyskać **dozwolone źródła**, wpisz znak gwiazdki (\*).
4. W hello **dozwolonych zleceń** listy rozwijanej, wybierz **UZYSKAĆ** i **opcje**.
5. Aby uzyskać **dozwolone nagłówki**, wpisz znak gwiazdki (\*).
6. Aby uzyskać **widoczne nagłówki**, wpisz znak gwiazdki (\*).
7. Aby uzyskać **maksymalny wiek (w sekundach)**, typ **200**.
8. Kliknij pozycję **Dodaj**.

## <a name="test-cors"></a>Test CORS

Sprawdź, czy wszystko jest gotowe, wykonując następujące hello:

1. Przejdź toohello [cors.org testu](http://test-cors.org/) witryny sieci Web, a następnie wklej hello adres URL hello **zdalnego adresu URL** pole.
2. Kliknij przycisk **wysłać żądania**.  
    Jeśli wystąpi błąd, upewnij się, że Twoje [ustawień specyfikacji CORS](#configure-cors) są poprawne. Może być również konieczne tooclear pamięć podręczną przeglądarki lub Otwórz sesji przeglądania w trybie prywatnym, naciskając klawisze Ctrl + Shift + P.

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a>Modyfikowanie zasad niestandardowych rejestracji i logowania

W obszarze hello najwyższego poziomu  *\<TrustFrameworkPolicy\>*  tagu, należy odnaleźć  *\<BuildingBlocks\>*  tagu. W ramach hello  *\<BuildingBlocks\>*  Dodaj tagi,  *\<ContentDefinitions\>*  tag przez skopiowanie hello poniższy przykład. Zastąp *your_storage_account* hello nazwą konta magazynu.

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a>Przekaż zaktualizowany zasad niestandardowych

1. W hello [portalu Azure](https://portal.azure.com), [przełącznika w kontekście hello dzierżawy usługi Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md), a następnie otwórz hello **usługi Azure AD B2C** bloku.
2. Kliknij przycisk **wszystkich zasad**.
3. Kliknij przycisk **przekazywać zasady**.
4. Przekaż `SignUpOrSignin.xml` z hello  *\<ContentDefinitions\>*  tag, który wcześniej został dodany.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Test przy użyciu zasad niestandardowych hello **Uruchom teraz**

1. Na powitania **usługi Azure AD B2C** bloku Przejdź zbyt**wszystkie zasady**.
2. Wybierz zasady niestandardowe hello, który został przekazany, a następnie kliknij przycisk hello **Uruchom teraz** przycisku.
3. Należy toosign stanie się przy użyciu adresu e-mail.

## <a name="reference"></a>Dokumentacja

Przykładowe szablonów można znaleźć do dostosowania interfejsu użytkownika w tym miejscu:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

folder sample_templates/wingtip Hello zawiera następujące pliki HTML hello:

| Szablon HTML5 | Opis |
|----------------|-------------|
| *phonefactor.HTML* | Użyj tego pliku jako szablonu dla strony uwierzytelniania wieloskładnikowego. |
| *ResetPassword.HTML* | Użyj tego pliku jako szablonu dla nie pamiętasz hasła strony. |
| *selfasserted.HTML* | Użyj tego pliku jako szablonu dla kont społecznościowych stronę tworzenia konta, stronę tworzenia konta lokalnego konta lub stronę logowania konta lokalnego. |
| *Unified.HTML* | Użyj tego pliku jako szablonu ujednoliconego strony rejestracji lub logowania. |
| *updateprofile.HTML* | Użyj tego pliku jako szablonu strony aktualizacji profilu. |

W hello [zmodyfikować sekcji rejestracji i logowania zasady niestandardowe](#modify-your-sign-up-or-sign-in-custom-policy), skonfigurowany definicji zawartości hello `api.idpselections`. pełny zestaw zawartości definicja identyfikatorów, które są rozpoznawane przez framework obsługi tożsamości hello Azure AD B2C i ich opisy Hello znajdują się w hello w poniższej tabeli:

| Identyfikator definicji zawartości | Opis | 
|-----------------------|-------------|
| *API.error* | **Strona błędu**. Ta strona jest wyświetlana po napotkaniu wyjątku lub wystąpił błąd. |
| *API.idpselections* | **Strona wyboru dostawcy tożsamości**. Ta strona zawiera listę tożsamość, którą można wybrać dostawców, którzy hello użytkownika podczas logowania. Te opcje są enterprise dostawców tożsamości, dostawców tożsamości społecznościowych, takich jak Facebook i Google + lub kont lokalnych. |
| *API.idpselections.Signup* | **Wybór dostawcy tożsamości dla rejestracji**. Ta strona zawiera listę dostawców, którzy hello użytkownika można wybrać podczas tworzenia konta tożsamości. Te opcje są enterprise dostawców tożsamości, dostawców tożsamości społecznościowych, takich jak Facebook i Google + lub kont lokalnych. |
| *API.localaccountpasswordreset* | **Nie pamiętasz hasła strony**. Ta strona zawiera formularza hello konieczne przeprowadzenie tooinitiate resetowania hasła.  |
| *API.localaccountsignin* | **Strona logowania konta lokalnego**. Ta strona zawiera formularz logowania dla logowania przy użyciu konta lokalnego, która jest oparta na adres e-mail lub nazwę użytkownika. Formularz Hello może zawierać pola do wprowadzania tekstu, a w polu wprowadzania hasła. |
| *API.localaccountsignup* | **Stronę tworzenia konta lokalnego konta**. Ta strona zawiera formularz zapisów do skorzystania z konta lokalnego, która jest oparta na adres e-mail lub nazwę użytkownika. Formularz Hello może zawierać różne kontrolki wejściowe, takich jak pola do wprowadzania tekstu, pole wprowadzania hasła przycisk radiowy, jednokrotnym zaznaczeniem pola listy rozwijanej i pól wyboru wielokrotnego wyboru. |
| *API.phonefactor* | **Strona uwierzytelniania wieloskładnikowego**. Na tej stronie użytkownicy mogą sprawdzić swoje numery telefonów (przy użyciu tekstowych lub głosowych) podczas tworzenia konta lub logowania. |
| *API.selfasserted* | **Strony rejestracji społecznościowych konta**. Ta strona zawiera wypełnieniu formularza, który użytkownicy muszą wykonać podczas logowania przy użyciu istniejącego konta od dostawcy tożsamości społecznościowych, takich jak Facebook lub Google +. Ta strona jest podobne toohello poprzedzających strony rejestracji społecznościowych konta, z wyjątkiem pól wprowadzania hasła hello. |
| *API.selfasserted.profileupdate* | **Strona aktualizacji profilu**. Ta strona zawiera formularza, w których użytkownicy mogą używać tooupdate swój profil. Ta strona jest podobne toohello kont społecznościowych stronę tworzenia konta, z wyjątkiem pól wprowadzania hasła hello. |
| *API.signuporsignin* | **Ujednolicone stronę tworzenia konta lub logowania**. Ta strona obsługuje zarówno hello rejestracji i logowania użytkowników, którzy można używać w organizacji dostawcy tożsamości, dostawców tożsamości społecznościowych, takich jak Facebook lub Google + lub kont lokalnych.  |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać dodatkowe informacje na temat elementy interfejsu użytkownika, które można dostosowywać, zobacz [Podręcznik do dostosowania interfejsu użytkownika dla zasad wbudowany](active-directory-b2c-reference-ui-customization.md).
