---
title: "Dodaj firmowe specyficzne dla języka do strony logowania w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać określonej firmy języka znakowania obrazy i tekst Azure stronę logowania"
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
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a>Dodaj firmowe specyficzne dla języka do strony logowania w usłudze Azure Active Directory
Aby uniknąć nieporozumień, wiele firm chce zastosować spójny wygląd i zachowanie we wszystkich witrynach sieci Web i usługach, którymi zarządzają. Usługa Azure Active Directory obsługuje tę funkcję, umożliwiając dostosowanie wyglądu strony logowania z logo firmy i niestandardowych schematów kolorów. Strona logowania jest to strona wyświetlana podczas logowania się do usługi Office 365 lub innych aplikacji opartych na sieci web, które używają usługi Azure AD jako dostawcy tożsamości. Użytkownik interakcji z tej strony, aby wprowadzić swoje poświadczenia.

## <a name="customizing-the-sign-in-page-for-another-language"></a>Dostosowywanie strony logowania dla innego języka
Możesz dodać elementy specyficzne dla języka do niestandardowej strony logowania tylko wtedy, gdy zostały już utworzone niestandardowe strony logowania, zgodnie z opisem w [dodać znakowanie firmowe do strony logowania](active-directory-branding-custom-signon-azure-portal.md). Można skonfigurować jedną logowania stronę na katalog domyślny zestaw elementów dostosowywalnych. Po skonfigurowaniu domyślny zestaw elementów strony, można skonfigurować więcej wersji dla różnych ustawień regionalnych. Możesz także mieszać i dopasowywać różne elementy. Na przykład można:

* Tworzy domyślny **logowania obraz strony** czy działającą dla wszystkich języków, następnie utworzyć specyficzne wersje dla angielskiego i francuskiego. Po ustawieniu przeglądarek do jednej z tych dwóch języków pojawia się obraz specyficzny dla języka, podczas gdy ilustracja domyślna będzie wyświetlana dla wszystkich pozostałych języków.
* Skonfigurować różne wersje logo dla organizacji (np. wersję japońską lub hebrajską).

Firma Microsoft zaleca zachowywanie liczby wersji języka niski, ze względu na konserwacji i wydajności.

**Aby dodać znakowanie firmowe do katalogu:**

1. Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.
2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w polu tekstowym, a następnie wybierz **Enter**.

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. Na **użytkowników i grup** bloku, wybierz opcję **firmy znakowania**.
4. Na **użytkowników i grup - firmy znakowania** bloku, wybierz opcję **Dodaj język** polecenia.

    ![Dodawanie znakowania elementy specyficzne dla języka](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Zmodyfikuj elementy, które chcesz dostosować. Wszystkie elementy są opcjonalne.
6. Kliknij pozycję **Zapisz**.

Może potrwać do godziny wszelkie zmiany wprowadzone do strony logowania znakowania na.

## <a name="next-steps"></a>Następne kroki
[Dodawanie znakowania firmowego do strony logowania](active-directory-branding-custom-signon-azure-portal.md)
