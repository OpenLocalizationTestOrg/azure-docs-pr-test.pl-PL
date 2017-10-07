---
title: "aaaAdd specyficzny dla języka firmowe tooyour strony logowania w hello Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd określonego języka firmy znakowania obrazy i tekst strony tooan Azure logowania"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 1e33c31abc242e8455290beb1f03760be7b9ac42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-language-specific-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a>Dodaj specyficzne dla języka firmowe tooyour strony logowania w hello Azure Active Directory
tooavoid pomyłek, w wielu firmach tooapply spójny wygląd i zachowanie we wszystkich hello witryn sieci Web i usługach, którymi zarządzają. Azure Active Directory obsługuje tę funkcję, umożliwiając toocustomize wygląd hello hello strony logowania z logo firmy i niestandardowych schematów kolorów. Strona logowania Hello jest hello strona wyświetlana podczas logowania tooOffice 365 lub innych aplikacji opartych na sieci web, które używają usługi Azure AD jako dostawcy tożsamości. Użytkownik interakcji z tej strony tooenter swoje poświadczenia.

## <a name="customizing-hello-sign-in-page-for-another-language"></a>Dostosowywanie hello strony logowania dla innego języka
Można dodać elementy specyficzne dla języka tooyour niestandardowe strony logowania, tylko wtedy, gdy zostały już utworzone niestandardowe strony logowania, zgodnie z opisem w [dodać znakowanie strony logowania tooyour firmowe](active-directory-branding-custom-signon-azure-portal.md). Można skonfigurować jedną logowania stronę na katalog domyślny zestaw elementów dostosowywalnych. Po skonfigurowaniu hello domyślny zestaw elementów strony, można skonfigurować więcej wersji dla różnych ustawień regionalnych. Możesz także mieszać i dopasowywać różne elementy. Na przykład można:

* Tworzy domyślny **logowania obraz strony** czy działającą dla wszystkich języków, następnie utworzyć specyficzne wersje dla angielskiego i francuskiego. Po ustawieniu tooone Twojego przeglądarki z tych dwóch języków obraz specyficzny dla języka hello pojawia się, gdy ilustracja domyślna hello będzie wyświetlana dla wszystkich pozostałych języków.
* Skonfigurować różne wersje logo dla organizacji (np. wersję japońską lub hebrajską).

Firma Microsoft zaleca zachowywanie hello liczby wersji języka niski, ze względu na konserwacji i wydajności.

**tooadd znakowania tooyour katalogu firmy:**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. Na powitania **użytkowników i grup** bloku, wybierz opcję **firmy znakowania**.
4. Na powitania **użytkowników i grup - firmy znakowania** bloku, wybierz hello **Dodaj język** polecenia.

    ![Dodawanie znakowania elementy specyficzne dla języka](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Zmodyfikuj elementy hello ma toocustomize. Wszystkie elementy są opcjonalne.
6. Kliknij pozycję **Zapisz**.

Może potrwać godzinę tooan dla wszystkie zmiany dokonane toohello logowania strony tooappear znakowania.

## <a name="next-steps"></a>Następne kroki
[Dodaj firmowe tooyour strony logowania](active-directory-branding-custom-signon-azure-portal.md)
