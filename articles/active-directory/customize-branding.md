---
title: Logowanie w obszarze hello Azure Active Directory aaaCustomize | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooadd strony toohello Azure logowania w znakowaniu firmy"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: 7a7ccdeef0764f6cf9e9e224acd4350983031fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-company-branding-tooyour-sign-in-page-in-azure-ad"></a>Szybki Start: Dodawanie firmowe tooyour strony logowania w usłudze Azure AD
tooavoid pomyłek, w wielu firmach tooapply spójny wygląd i zachowanie we wszystkich hello witryn sieci Web i usługach, którymi zarządzają. Azure Active Directory (Azure AD) zapewnia tę funkcję, umożliwiając toocustomize wygląd hello hello strony logowania z logo firmy i niestandardowych schematów kolorów. Strona logowania Hello jest hello strona wyświetlana podczas logowania tooOffice 365 lub innych aplikacji opartych na sieci web, które używają usługi Azure AD jako dostawcy tożsamości. Użytkownik interakcji z tej strony tooenter swoje poświadczenia.

> [!NOTE]
> * Logo firmy jest dostępna tylko w przypadku uaktualnienia toohello Premium lub podstawowa edition usługi Azure AD lub ma licencji usługi Office 365. toolearn, jeśli funkcja jest obsługiwana przez użytkownika typu licencji Sprawdź hello [cenową strona informacji o usłudze Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).
> 
> * Azure Active Directory Premium i podstawowa wydań są dostępne dla klientów w Chinach przy użyciu hello na całym świecie wystąpienia usługi Azure Active Directory. Azure Active Directory Premium i podstawowa wersje nie są obecnie obsługiwane w hello Microsoft Azure świadczonej przez 21Vianet w Chinach. Aby uzyskać więcej informacji, skontaktuj się z nami na powitania [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="customizing-hello-sign-in-page"></a>Dostosowywanie strony logowania hello

<!--You can customize hello following elements on hello sign-in page: <attach image>-->

Dostosowywanie znakowania na stronie są wyświetlane hello Azure AD logowania, gdy użytkownicy uzyskują dostęp do adresu URL specyficznego dla dzierżawy takich jak firmy [ *https://outlook.com/contoso.com*](https://outlook.com/contoso.com).

Podczas odwiedzania ogólnego adresu URL, takie jak www.office.com, strony logowania hello nie zawiera firmowe dostosowań, ponieważ hello system nie może ustalić, który użytkownik hello jest. Logo firmy będą wyświetlane po użytkowników, wprowadź swój identyfikator użytkownika lub wybierz kafelka użytkownika.

> [!NOTE]
> * Nazwa domeny musi występować jako "Aktywna" w hello **domen** część hello portalu Azure, w którym skonfigurowano znakowanie. Aby uzyskać więcej informacji, zobacz [Dodawanie niestandardowej nazwy domeny](add-custom-domain.md).
> * Znakowanie strony logowania nie jest przenoszone toohello strony logowania do osobistego konta Microsoft. Jeśli firm gości lub pracowników, na których Zaloguj się za pomocą osobistego konta Microsoft, ich strony logowania nie odzwierciedla hello znakowanie organizacji.


### <a name="banner-logo"></a>Baner logo 

Opis | Ograniczenia | Zalecenia
------- | ------- | ----------
Witaj Baner logo jest wyświetlany na powitania rejestrowania i strony panelu dostępu hello.<br>Na powitania strony logowania oznacza to po określeniu organizacji użytkownika hello zwykle, po wprowadzeniu nazwy hello użytkownika.  | Przezroczysty JPG lub PNG<br>Maksymalna wysokość: 36 pikseli<br>Maksymalna szerokość: 245 pikseli | W tym miejscu użyć logo organizacji.<br>Użyj przezroczystego obrazu. Nie wolno zakładać, że będzie białe tło hello.<br>Nie dodawaj wypełnienia wokół logo hello obraz lub logo będzie wyglądać nieproporcjonalnie małe.

### <a name="username-hint"></a>Wskazówka dotycząca nazwy użytkownika   
Opis | Ograniczenia | Zalecenia
------- | ------- | ----------
Dostosowuje to tekst podpowiedzi hello hello pole nazwy użytkownika. | Tekst Unicode w górę too64 znaków<br>Tylko zwykły tekst | Zaleca się, czy nie zostały ustawione to jeśli oczekujesz gości spoza Twojej organizacji toosign w tooyour aplikacji.
            
### <a name="sign-in-page-text"></a>Tekst strony logowania   
Opis | Ograniczenia | Zalecenia
------- | ------- | ----------
To jest wyświetlany u dołu hello hello logowania w postaci i mogą być używane toocommunicate informacje dodatkowe, takie jak hello phone liczba tooyour pomocy technicznej lub klauzulę prawną. | Tekst Unicode w górę too256 znaków<br>Tylko zwykły tekst (bez linków lub tagów HTML) 

### <a name="sign-in-page-image"></a>Obraz strony logowania  
Opis | Ograniczenia | Zalecenia
------- | ------- | ----------
Pojawia się w tle hello hello logowania strony Centrum toohello zakotwiczony widoczne miejsca hello, będzie skalować i przycinanie toofill hello okna przeglądarki.  <br>Ten obraz nie jest wyświetlany na wąskich ekranach takich jak telefony komórkowe.<br>Czarne maski z 0.55 nieprzezroczystość zostaną zastosowane za pośrednictwem tego obrazu przez naszego kodu po załadowaniu hello strony. | JPG lub PNG<br>Wymiary obrazu: 1920 x 1080 pikseli<br>Rozmiar pliku: &gt; 300 KB | <br>Obrazy w przypadku, gdy nie ma fokusu silne podmiotu. Witaj nieprzezroczyste logowania formularz pojawia się za pośrednictwem Centrum hello tego obrazu i może obejmować dowolną część obraz powitania w zależności od wielkości hello hello okna przeglądarki.<br>Zachowaj rozmiar pliku hello możliwie najmniejsze możliwe tooensure szybkie ładować. 

### <a name="background-color"></a>Kolor tła
Opis | Ograniczenia | Zalecenia
------- | ------- | ----------
Kolor używany zamiast obraz tła hello połączeń o niskiej przepustowości. |   Kolor RGB w formacie szesnastkowym (przykład: #FFFFFF | Zaleca się przy użyciu podstawowego koloru hello hello Baner logo lub kolor Twojej organizacji.

### <a name="show-option-tooremain-signed-in"></a>Pokaż opcję tooremain zalogowany
Opis | Ograniczenia | Zalecenia
------- | ------- | ----------
Azure AD logowania zapewnia hello użytkownika hello opcja tooremain zalogowany po ich zamknięcie i ponowne otwarcie przeglądarki. Użyj tego toohide tej opcji.<br>Ustaw tę wartość za "nie" toohide tej opcji od użytkowników. | &nbsp; | Nie ma to wpływu na okres istnienia sesji.<br>Niektóre funkcje usługi SharePoint Online i Office 2010, zależą od użytkownicy będą mogli toochoose tooremain zalogowany. Jeśli ustawisz ten toobe ukryte, dodatkowe i nieoczekiwane monity toosign w może widzą użytkownicy.

> [!NOTE]
> Wszystkie elementy są opcjonalne. Na przykład jeśli określisz Baner logo z żadnego obrazu tła strony logowania hello wyświetli Twojego logo i hello obraz tła dla lokacji docelowej hello (na przykład usługi Office 365).

## <a name="add-company-branding-tooyour-directory"></a>Dodaj firmowe tooyour katalogu

1. Zaloguj się za[hello portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Na powitania **użytkowników i grup** bloku, wybierz opcję **firmy znakowania**.
4. Na powitania **użytkowników i grup - firmy znakowania** bloku, wybierz hello **Edytuj** polecenia.

    ![Edytuj niestandardowe znakowanie](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Zmodyfikuj elementy hello ma toocustomize. Wszystkie elementy są opcjonalne.
6. Kliknij pozycję **Zapisz**.

Może potrwać godzinę tooan dla wszystkie zmiany dokonane toohello logowania strony tooappear znakowania.

## <a name="add-language-specific-company-branding-tooyour-directory"></a>Dodaj katalog tooyour firmowe specyficzne dla języka

1. Zaloguj się toohello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. Na powitania **użytkowników i grup** bloku, wybierz opcję **firmy znakowania**.
4. Na powitania **użytkowników i grup - firmy znakowania** bloku, wybierz hello **Dodaj język** polecenia.

    ![Dodawanie znakowania elementy specyficzne dla języka](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Zmodyfikuj elementy hello ma toocustomize. Wszystkie elementy są opcjonalne.
6. Kliknij pozycję **Zapisz**.

Może potrwać godzinę tooan dla wszystkie zmiany dokonane toohello logowania strony tooappear znakowania.

## <a name="next-steps"></a>Następne kroki
W tym szybkiego startu kiedy znasz już jak tooadd firmy znakowania katalogu tooyour usługi Azure AD. 

Możesz użyć hello następujące łącze tooconfigure znakowaniu firmy na platformie Azure AD z hello portalu Azure.

> [!div class="nextstepaction"]
> [Configure company branding (Konfigurowanie oznaczenia marką firmy)](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 