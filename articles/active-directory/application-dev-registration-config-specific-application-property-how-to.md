---
title: "toofill aaaHow limit określonych pól dla aplikacji utworzonych niestandardowych | Dokumentacja firmy Microsoft"
description: "Wskazówki w sposób toofill limit określonych pól podczas rejestrowania aplikacji niestandardowej rozwinięte z usługą Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7e07bc45c58542edb3863db5aad7c845f1a1772e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofill-out-specific-fields-for-a-custom-developed-application"></a>Jak toofill limit określonych pól dla aplikacji utworzonych niestandardowych

W tym artykule umożliwiają krótki opis wszystkich hello dostępne pola formularza rejestracji aplikacji hello w hello [portalu Azure](https://portal.azure.com).

## <a name="register-a-new-application"></a>Zarejestrować nową aplikację

-   tooregister nową aplikację, przejdź toohello [portalu Azure](https://portal.azure.com).

-   W okienku nawigacji po lewej stronie powitania kliknij **usługi Azure Active Directory.**

-   Wybierz **rejestracji aplikacji** i kliknij przycisk **Dodaj**.

-   To otwarcie formularza rejestracji aplikacji hello.

## <a name="fields-in-hello-application-registration-form"></a>Pola formularza rejestracji aplikacji hello


| Pole            | Opis                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| Nazwa             | Nazwa Hello aplikacji hello. Powinien mieć co najmniej cztery znaki.                |
| Typ aplikacji | **Sieci Web aplikacji/interfejs API sieci Web**: aplikacja, która reprezentuje aplikacji sieci web, interfejs API sieci web lub obu 
| |**Natywny**: aplikację, którą można zainstalować na urządzeniu lub komputerze użytkownika           |
| Adres URL logowania      | adres URL Hello, gdzie użytkownicy mogą rejestrować w toouse aplikacji                                  |

Po wypełnieniu hello powyżej pól aplikacji hello został zarejestrowany w hello portalu Azure, oraz być przekierowywane toohello strony aplikacji. Witaj **ustawienia** przycisk w okienku aplikacji hello otwartej stronie ustawień hello, która zawiera więcej pól dla Ciebie toocustomize aplikacji. Witaj w poniższej tabeli opisano wszystkie pola hello na stronie ustawień hello. należy pamiętać, że byłaby widoczna tylko podzbiór tych pól, w zależności od tego, czy podczas tworzenia aplikacji sieci web lub aplikacji natywnej.

| Pole           | Opis                                                                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Identyfikator aplikacji  | Podczas rejestrowania aplikacji usługi Azure AD przypisuje aplikacji identyfikator aplikacji. Identyfikator aplikacji Hello może służyć toouniquely zidentyfikować aplikację w tooAzure żądań uwierzytelniania AD, a także tooaccess zasoby, takie jak hello interfejsu API programu Graph.                                                          |
| Identyfikator URI aplikacji      | Należy to unikatowy identyfikator URI, zazwyczaj formę hello **https://&lt;dzierżawy\_nazwa&gt;/&lt;aplikacji\_nazwa&gt;.** Jest on używany podczas przepływu grant autoryzacji hello, jako unikatowy identyfikator zasobu hello toospecify token hello, które powinny być wystawiane dla. Staje się również oświadczenie hello "lub" hello wystawiony token dostępu. |
| Przekaż nowe logo | Umożliwia to tooupload logo aplikacji. Witaj logo musi być w formacie BMP, jpg lub PNG, a rozmiar pliku hello powinna być mniejsza niż 100KB. Wymiary Hello obrazu hello powinny być 215 x 215 pikseli i wymiary obrazu centralnej 94 x 94 pikseli.                                                       |
| Adres URL strony głównej   | Jest to hello adres URL logowania określony podczas rejestracji aplikacji.                                                                                                                                                                                                                                              |
| Adres URL wylogowania      | Tego hello wylogowania wylogowania pojedynczego adresu URL. Usługi Azure AD wysyła adres URL wylogowania żądania toothis hello wyczyszczenie ich sesji z usługą Azure AD przy użyciu zarejestrowanej aplikacji.                                                                                                                                       |
| Obsługa wielu dzierżawcza  | Ten przełącznik określa, czy aplikacja hello może być używana przez wielu dzierżawców. Zwykle oznacza to, organizacje zewnętrzne można używać aplikacji przez zarejestrowanie go w swojej dzierżawy i udzielanie dostępu tootheir danych organizacji.                                                                   |
| Adresy URL odpowiedzi      | adresy URL odpowiedzi Hello są hello punktów końcowych, gdzie usługi Azure AD zwracać wszystkie tokeny żądań aplikacji.                                                                                                                                                                                                          |
| Identyfikator URI przekierowania   | Dla natywnych aplikacji to gdy użytkownik hello być wysłane toofollowing pomyślnej autoryzacji. Azure AD czy hello przekierowania z dostawy aplikacji hello OAuth 2.0 żądanie pasuje do jednej z wartości hello zarejestrowany w portalu hello identyfikatora URI.                                                            |
| Klucze            | Można utworzyć kluczy tooprogrammatically dostępu do interfejsów API sieci web zabezpieczonych przez usługi Azure AD bez interakcji użytkownika. Z hello \* \*klucze\* \* strony, wprowadź klucza hello ich opisu i daty wygaśnięcia i zapisać klucz hello toogenerate. Upewnij się, że toosave gdzieś bezpieczeństwo, zgodnie z będziesz w stanie tooaccess go później.             |

## <a name="next-steps"></a>Następne kroki
[Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory](active-directory-enable-sso-scenario.md)
