---
title: Logowanie w obszarze hello Azure Active Directory aaaCustomize | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooadd strony toohello Azure logowania w znakowaniu firmy"
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
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a>Dodaj firmowe tooyour strony logowania w hello Azure Active Directory
tooavoid pomyłek, w wielu firmach tooapply spójny wygląd i zachowanie we wszystkich hello witryn sieci Web i usługach, którymi zarządzają. Azure Active Directory obsługuje tę funkcję, umożliwiając toocustomize wygląd hello hello strony logowania z logo firmy i niestandardowych schematów kolorów. Strona logowania Hello jest hello strona wyświetlana podczas logowania tooOffice 365 lub innych aplikacji opartych na sieci web, które używają usługi Azure AD jako dostawcy tożsamości. Użytkownik interakcji z tej strony tooenter swoje poświadczenia.

Jeśli chcesz tooshow swoje firmowe oznaczenia, kolory i inne dostosowywalne elementy na tej stronie, zobacz następujące obrazy toounderstand hello różnicę między obydwoma środowiskami hello hello.

Witaj, wykonując zrzut ekranu przedstawia oraz przykład dla usługi Office 365 hello strony logowania na komputerze stacjonarnym **przed** dostosowaniem:

![Strona logowania usługi Office 365 przed dostosowaniem](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

Witaj, wykonując zrzut ekranu przedstawia oraz przykład dla usługi Office 365 hello strony logowania na komputerze stacjonarnym **po** dostosowaniem:

![Strona logowania usługi Office 365 po dostosowaniu](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a>Dostosowywanie strony logowania hello
Zwykle dostęp za pośrednictwem przeglądarki tooyour chmury aplikacji i usług, które subskrybuje Twoja organizacja, należy użyć hello strony logowania.

Jeśli strona logowania tooyour zmiany zostały zastosowane, może potrwać do godziny tooan hello tooappear zmiany.

Strona logowania z oznaczeniami firmowymi jest wyświetlana tylko podczas odwiedzania usługi za pomocą adresu URL specyficznego dla dzierżawy, takiego jak https://outlook.com/**contoso**.com lub https://mail.**contoso**.com.

W przypadku odwiedzania usługi za pomocą adresów URL innych niż specyficzne dla dzierżawy (np. https://mail.office365.com) wyświetlana jest strona logowania bez firmowego znakowania. W takim przypadku znakowanie zostanie wyświetlone po wprowadzeniu identyfikatora użytkownika lub wybraniu kafelka użytkownika.

> [!NOTE]
> * Nazwa domeny musi występować jako "Aktywna" w hello **domen** część hello portalu Azure, w którym skonfigurowano znakowanie. Aby uzyskać więcej informacji, zobacz [Dodawanie niestandardowych nazw domen](active-directory-domains-add-azure-portal.md).
> * Znakowanie strony logowania nie jest przenoszone toohello konsumenta logowania firmy Microsoft. Jeśli możesz zalogować się przy użyciu konta Microsoft, mogą zobaczyć lista kafelków użytkowników renderowana przez usługę Azure AD, ale hello znakowanie organizacji nie ma zastosowania toohello strony logowania na koncie Microsoft.
>
>

Na stronie logowania hello **wylogowuj mnie** wyboru pozwala tooremain użytkownik zalogowany po ich zamknięcie i ponowne otwarcie przeglądarki.

   ![Nie wylogowuj mnie](./media/active-directory-branding-custom-signon-azure-portal/01.png)

Opcja nie ma wpływu na okres istnienia sesji. Pole wyboru hello na stronę logowania w usłudze Azure Active Directory hello można ukryć.
Określa, czy pole wyboru hello jest wyświetlane zależy od ustawienia hello **wylogowuj mnie wyłączone**.

   ![Nie wylogowuj mnie](./media/active-directory-branding-custom-signon-azure-portal/02.png)

toohide wyboru hello, skonfiguruj to ustawienie zbyt**tak**.

> [!NOTE]
> Niektóre funkcje pakietu Office 2010 i SharePoint Online są zależne od użytkownicy będą mogli toocheck tego pola. Jeśli konfigurujesz toohidden to ustawienie, dodatkowe i nieoczekiwane monity toosign w może widzą użytkownicy.
>
>

**tooadd znakowania tooyour katalogu firmy:**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Na powitania **użytkowników i grup** bloku, wybierz opcję **firmy znakowania**.
4. Na powitania **użytkowników i grup - firmy znakowania** bloku, wybierz hello **Edytuj** polecenia.

    ![Edytuj niestandardowe znakowanie](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Zmodyfikuj elementy hello ma toocustomize. Wszystkie elementy są opcjonalne.
6. Kliknij pozycję **Zapisz**.

Może potrwać godzinę tooan dla wszystkie zmiany dokonane toohello logowania strony tooappear znakowania.

## <a name="next-steps"></a>Następne kroki
[Dodać znakowanie firmowe specyficzne dla języka](active-directory-branding-localize-azure-portal.md)
