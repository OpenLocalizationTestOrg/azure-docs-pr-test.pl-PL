---
title: "Dostosowywanie strony logowania w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać znakowanie firmowe do platformy Azure strony logowania"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 27590c018ea55e9793246c7a4cab10f934ea502b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a>Dodawanie znakowania firmowego do strony logowania w usłudze Azure Active Directory
Aby uniknąć nieporozumień, wiele firm chce zastosować spójny wygląd i zachowanie we wszystkich witrynach sieci Web i usługach, którymi zarządzają. Usługa Azure Active Directory obsługuje tę funkcję, umożliwiając dostosowanie wyglądu strony logowania z logo firmy i niestandardowych schematów kolorów. Strona logowania jest to strona wyświetlana podczas logowania się do usługi Office 365 lub innych aplikacji opartych na sieci web, które używają usługi Azure AD jako dostawcy tożsamości. Użytkownik interakcji z tej strony, aby wprowadzić swoje poświadczenia.

Jeśli chcesz wyświetlać swoje firmowe oznaczenia, kolory i inne dostosowywalne elementy na tej stronie, zobacz następujące ilustracje, aby zrozumieć różnicę między obydwoma środowiskami.

Poniższy zrzut ekranu przedstawia przykład strony logowania usługi Office 365 na komputerze stacjonarnym **przed** dostosowaniem:

![Strona logowania usługi Office 365 przed dostosowaniem](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

Poniższy zrzut ekranu przedstawia przykład strony logowania usługi Office 365 na komputerze stacjonarnym **po** dostosowaniu:

![Strona logowania usługi Office 365 po dostosowaniu](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-the-sign-in-page"></a>Dostosowywanie strony logowania
Zwykle na potrzeby dostępu opartego na przeglądarce do aplikacji i usług w chmurze subskrybowanych przez organizację używana jest strona logowania.

W przypadku zastosowania zmian do strony logowania uwzględnienie ich może zająć godzinę.

Strona logowania z oznaczeniami firmowymi jest wyświetlana tylko podczas odwiedzania usługi za pomocą adresu URL specyficznego dla dzierżawy, takiego jak https://outlook.com/**contoso**.com lub https://mail.**contoso**.com.

W przypadku odwiedzania usługi za pomocą adresów URL innych niż specyficzne dla dzierżawy (np. https://mail.office365.com) wyświetlana jest strona logowania bez firmowego znakowania. W takim przypadku znakowanie zostanie wyświetlone po wprowadzeniu identyfikatora użytkownika lub wybraniu kafelka użytkownika.

> [!NOTE]
> * Nazwa domeny musi występować jako "Aktywna" w **domen** części portalu Azure, w którym skonfigurowano znakowanie. Aby uzyskać więcej informacji, zobacz [Dodawanie niestandardowych nazw domen](active-directory-domains-add-azure-portal.md).
> * Znakowanie strony logowania nie jest przenoszone na stronę logowania klienta firmy Microsoft. Jeśli możesz zalogować się przy użyciu konta Microsoft, mogą zobaczyć lista kafelków użytkowników renderowana przez usługę Azure AD, ale znakowanie organizacji nie ma zastosowania do konta Microsoft Zaloguj strony.
>
>

Na stronie logowania pole wyboru **Nie wylogowuj mnie** umożliwia użytkownikom zachowanie stanu zalogowania w przypadku zamknięcia i ponownego otworzenia przeglądarki.

   ![Nie wylogowuj mnie](./media/active-directory-branding-custom-signon-azure-portal/01.png)

Opcja nie ma wpływu na okres istnienia sesji. Pole wyboru na stronie logowania usługi Azure Active Directory możesz ukryć.
Określa, czy jest wyświetlane pole wyboru zależy od ustawienia **wylogowuj mnie wyłączone**.

   ![Nie wylogowuj mnie](./media/active-directory-branding-custom-signon-azure-portal/02.png)

Aby ukryć pole wyboru, należy skonfigurować to ustawienie, aby **tak**.

> [!NOTE]
> Niektóre funkcje usługi SharePoint Online oraz pakietu Office 2010 zależą od możliwości skorzystania z tego pola wyboru przez użytkowników. Jeśli skonfigurujesz to ustawienia na wartość „Ukryte”, użytkownicy mogą otrzymywać dodatkowe i nieoczekiwane monity o logowanie.
>
>

**Aby dodać znakowanie firmowe do katalogu:**

1. Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.
2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w polu tekstowym, a następnie wybierz **Enter**.

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Na **użytkowników i grup** bloku, wybierz opcję **firmy znakowania**.
4. Na **użytkowników i grup - firmy znakowania** bloku, wybierz opcję **Edytuj** polecenia.

    ![Edytuj niestandardowe znakowanie](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Zmodyfikuj elementy, które chcesz dostosować. Wszystkie elementy są opcjonalne.
6. Kliknij pozycję **Zapisz**.

Może potrwać do godziny wszelkie zmiany wprowadzone do strony logowania znakowania na.

## <a name="next-steps"></a>Następne kroki
[Dodać znakowanie firmowe specyficzne dla języka](active-directory-branding-localize-azure-portal.md)
