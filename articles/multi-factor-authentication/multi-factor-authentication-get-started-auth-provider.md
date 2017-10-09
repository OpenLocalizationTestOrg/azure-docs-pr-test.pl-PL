---
title: "aaaGet uruchomić dostawcy usługi Azure Multi-Factor Auth | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate dostawcy usługi Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: a7dd5030-7d40-4654-8fbd-88e53ddc1ef5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 00ea967a80b43baff38c1de586c54d95c9abac2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a>Wprowadzenie do dostawcy usługi Azure Multi-Factor Authentication
Weryfikacja dwuetapowa jest domyślnie dostępna dla administratorów globalnych, którzy zarządzają użytkownikami usług Azure Active Directory i Office 365. Jednak jeśli chcesz, aby tootake zaletą [zaawansowane funkcje](multi-factor-authentication-whats-next.md) , a następnie należy zakupić hello pełną wersję usługi Azure Multi-Factor Authentication (MFA).

Dostawcy usługi Azure Multi-Factor Authentication służy tootake korzystać z funkcji udostępnianych przez hello pełną wersję usługi Azure MFA. Jest on przeznaczony dla użytkowników, którzy **nie mają licencji usługi Azure MFA lub Azure AD w wersji Premium ani licencji pakietu Enterprise Mobility + Security (EMS)**.  Azure MFA i Azure AD Premium oraz EMS zawierają hello pełną wersję usługi Azure MFA domyślnie. Jeśli masz te licencje, nie potrzebujesz dostawcy usługi Azure Multi-Factor Authentication.

Dostawca uwierzytelnianie wieloskładnikowe Azure jest wymagany toodownload hello zestawu SDK.

> [!IMPORTANT]
> toodownload hello zestawu SDK, należy toocreate dostawcy usługi Azure Multi-Factor Authentication, nawet jeśli użytkownik ma licencje usługi Azure MFA, usługi AAD Premium lub pakietu EMS.  Jeśli w tym celu należy utworzyć dostawcy uwierzytelniania wieloskładnikowego Azure i mają już licencji, należy się hello toocreate dostawcy z hello **każdego włączonego użytkownika** modelu. Następnie połącz hello dostawcy toohello katalog, który zawiera hello licencje usługi Azure MFA, Azure AD Premium lub pakietu EMS. Taka konfiguracja powoduje, że rozliczenie jest przeprowadzane tylko jeśli masz więcej unikatowych użytkowników, wykonywanie weryfikacji dwuetapowej niż hello liczbę licencji użytkownika.

## <a name="what-is-an-azure-multi-factor-auth-provider"></a>Co to jest dostawca usługi Azure Multi-Factor Authentication?

Jeśli nie masz licencji dla usługi Azure Multi-Factor Authentication, można utworzyć weryfikacji dwuetapowej toorequire dostawcy usługi MFA dla użytkowników. Jeśli opracowujesz aplikację niestandardową i chcesz tooenable usługi Azure MFA, tworzenie dostawcy uwierzytelniania i [Pobierz hello SDK](multi-factor-authentication-sdk.md).

Istnieją dwa typy dostawcy usługi MFA, a różnica hello jest wokół jak jest rozliczana subskrypcji platformy Azure. Opcja na uwierzytelniania Hello oblicza hello liczbę uwierzytelnień wykonane względem dzierżawy w miesiącu. Ta opcja jest przydatna, jeśli masz pewną liczbę użytkowników, którzy uwierzytelniają się tylko czasami, na przykład gdy aplikacja niestandardowa wymaga uwierzytelniania wieloskładnikowego. Opcja użytkownika Hello oblicza hello liczbę osoby w Twojej dzierżawie przeprowadzenia weryfikacji dwuetapowej w ciągu miesiąca. Ta opcja jest najlepiej, jeśli masz w przypadku niektórych użytkowników z licencjami, ale należy tooextend MFA toomore użytkowników poza limitów do licencjonowania.

## <a name="create-a-multi-factor-auth-provider"></a>Tworzenie dostawcy usługi Multi-Factor Authentication
Użyj hello następujące kroki toocreate dostawcy usługi Azure Multi-Factor Authentication. Dostawcy usługi MFA w usłudze Azure Multi-Factor można tworzyć tylko w hello klasycznego portalu Azure. Jeśli nie możesz zarejestrować toohello klasycznego portalu Azure, sprawdź, czy toomake się, że dzierżawy usługi Azure AD jest [skojarzone z subskrypcją platformy Azure](../active-directory/active-directory-how-subscriptions-associated-directory.md). 

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) jako administrator.
2. Po lewej stronie powitania, wybierz **usługi Active Directory**.
3. Na stronie usługi Active Directory hello u góry hello zaznacz **dostawców uwierzytelniania wieloskładnikowego**.
   
   ![Tworzenie dostawcy usługi MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. U dołu powitania kliknij **nowy**.
   
   ![Tworzenie dostawcy usługi MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. W obszarze App Services wybierz pozycję **Dostawca usługi Multi-Factor Authentication**
   
   ![Tworzenie dostawcy usługi MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. Wybierz pozycję **Szybkie tworzenie**.
   
   ![Tworzenie dostawcy usługi MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. Wypełnij następujące pola hello i wybierz **Utwórz**.
   1. **Nazwa** — Witaj nazwa hello dostawcy uwierzytelniania wieloskładnikowego.
   2. **Model użycia** – wybierz jedną z dwóch opcji:
      * Za uwierzytelnienie — model zakupu z opłatami za każde uwierzytelnienie. Zazwyczaj używany w scenariuszach, w których usługa Azure Multi-Factor Authentication jest używana w aplikacjach udostępnianych klientom.
      * Za włączonego użytkownika – model zakupu z opłatami za każdego włączonego użytkownika. Zwykle używany w przypadku pracowników tooapplications dostępu, takich jak Office 365. Wybierz tę opcję, jeśli niektórzy z Twoich użytkowników mają już licencje usługi Azure MFA.
   3. **Katalog** — Witaj, tego dostawcy uwierzytelniania wieloskładnikowego jest skojarzony z dzierżawy hello Azure Active Directory. Należy pamiętać o następujących hello:
      * Nie trzeba toocreate katalogu usługi Azure AD dostawcy uwierzytelniania wieloskładnikowego. Pozostaw to pole puste, jeśli jest planowane tylko toodownload powitania serwera usługi Azure Multi-Factor Authentication lub zestawu SDK.
      * Dostawca uwierzytelniania MFA Hello musi być skojarzony z usługi Azure AD directory tootake zaletą hello zaawansowane funkcje.
      * Z każdym katalogiem usługi Azure AD może być skojarzony tylko jeden dostawca usługi Multi-Factor Auth.  
      ![Tworzenie dostawcy usługi MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. Po kliknięciu przycisku Utwórz, hello jest utworzony dostawca uwierzytelniania MFA i powinien zostać wyświetlony komunikat informacją: **pomyślnie utworzono dostawcę uwierzytelniania wieloskładnikowego**. Kliknij przycisk **OK**.  
   
   ![Tworzenie dostawcy usługi MFA](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a>Zarządzanie dostawcą usługi Multi-Factor Auth

Nie można zmienić użycia hello modelu (każdego włączonego użytkownika lub każde uwierzytelnianie), po utworzeniu dostawca usługi MFA. Jednak można usunąć dostawcy usługi MFA hello, a następnie utworzyć jeden z modelem użycia innego.

Jeśli hello bieżącego dostawcy uwierzytelniania wieloskładnikowego jest skojarzony z katalogiem Azure AD (znanej także jako dzierżawa usługi Azure AD), można bezpiecznie usunąć dostawcę usługi MFA hello i utworzyć jest toohello połączonej usługi Azure AD w tej samej dzierżawy. Alternatywnie Jeśli zakupione za mało MFA, Azure AD Premium lub Enterprise Mobility + Security (EMS) licencji toocover wszystkich użytkowników, którzy są włączone dla usługi MFA, można usunąć dostawca usługi MFA hello całkowicie.

Jeśli dostawcy usługi MFA jest dzierżawy tooan połączonej usługi Azure AD lub połączyć dzierżawy tooa różne usługi Azure AD dostawcy usługi MFA hello nowe, opcje konfiguracji i ustawień użytkownika nie są przenoszone. Ponadto istniejących serwerów usługi Azure MFA muszą toobe ponownie aktywować przy użyciu poświadczeń aktywacji wygenerowane za pośrednictwem hello nowy dostawca usługi MFA. Ponowne uaktywnianie hello serwerów MFA toolink ich toohello nowy dostawca usługi MFA bez wpływu połączeń telefonicznych i uwierzytelniania wiadomości tekstowych, ale aplikacji mobilnej powiadomienia przestanie działać dla wszystkich użytkowników, do czasu ich ponowne uaktywnianie hello aplikacji mobilnej.

## <a name="next-steps"></a>Następne kroki

[Pobierz hello SDK usługi Multi-Factor Authentication](multi-factor-authentication-sdk.md)

[Konfigurowanie ustawień usługi Multi-Factor Authentication](multi-factor-authentication-whats-next.md)
