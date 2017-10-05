---
title: 'Samouczek: Integracji Azure Active Directory z Benefitsolver | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak używać Benefitsolver usłudze Azure Active Directory w celu włączenia logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>Samouczek: Integracji Azure Active Directory z Benefitsolver
Celem tego samouczka jest pokazanie integracji Azure i Benefitsolver.  

Scenariusz opisany w tym samouczku założono, że już następujące elementy:

* Ważnej subskrypcji platformy Azure
* Benefitsolver rejestracji jednokrotnej (SSO) włączone subskrypcji

Ten samouczek użytkowników usługi Azure AD, zostały przypisane do Benefitsolver będzie można funkcji logowania jednokrotnego do aplikacji przy użyciu [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).

Scenariusz opisany w tym samouczku składa się z następujących bloków konstrukcyjnych:

1. Włączanie integracji aplikacji dla Benefitsolver
2. Konfigurowanie rejestracji jednokrotnej (SSO)
3. Konfigurowanie Inicjowanie obsługi użytkowników
4. Przypisywanie użytkowników

![Scenariusz](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "scenariusza")

## <a name="enabling-the-application-integration-for-benefitsolver"></a>Włączanie integracji aplikacji dla Benefitsolver
Celem tej sekcji jest przedstawiają sposób włączania integracji aplikacji dla Benefitsolver.

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a>Aby włączyć integrację aplikacji dla Benefitsolver, wykonaj następujące czynności:
1. W klasycznym portalu Azure, w okienku nawigacji po lewej stronie kliknij **usługi Active Directory**.
   
   ![Usługi Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "usługi Active Directory")
2. Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.
3. Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.
   
   ![Aplikacje](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "aplikacji")
4. Kliknij przycisk **Dodaj** w dolnej części strony.
   
   ![Dodaj aplikację](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Dodaj aplikację")
5. Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.
   
   ![Dodawanie aplikacji z gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "dodać aplikację z gallerry")
6. W **pole wyszukiwania**, typ **Benefitsolver**.
   
   ![Galerii aplikacji](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "galerii aplikacji")
7. W okienku wyników wybierz **Benefitsolver**, a następnie kliknij przycisk **Complete** można dodać aplikację.
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>Konfigurowanie rejestracji jednokrotnej

Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie na Benefitsolver do swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.  

Aplikacja Benefitsolver oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do Twojej **atrybuty tokenu saml** konfiguracji. 

Poniższy zrzut ekranu przedstawia przykład tego.

![Atrybuty](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "atrybutów")

**Aby skonfigurować rejestrację jednokrotną, wykonaj następujące czynności:**

1. W klasycznym portalu Azure na **Benefitsolver** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować rejestrację jednokrotną** okna dialogowego.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "skonfigurować logowanie jednokrotne")
2. Na **jak chcesz użytkownikom zalogować się na Benefitsolver** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "skonfigurować logowanie jednokrotne")
3. Na **Konfigurowanie ustawień aplikacji** wykonaj następujące czynności:
   
   ![Konfiguruj ustawienia aplikacji](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Konfiguruj ustawienia aplikacji")
   
   1. W **na adres URL logowania** pole tekstowe, typ **http://azure.benefitsolver.com**.
   2. W **adres URL odpowiedzi** pole tekstowe, typ **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.  
   3. Kliknij przycisk **Dalej**.
4. Na **skonfigurować logowanie jednokrotne w Benefitsolver** , aby pobrać metadane, kliknij przycisk **pobierania metadanych**, a następnie zapisz plik metadanych lokalnie na komputerze.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "skonfigurować logowanie jednokrotne")
5. Wyślij plik metadanych pobranych Benefitsolver zespołowi pomocy technicznej.
   
   >[!NOTE]
   >Z zespołem pomocy technicznej Benefitsolver ma robić rzeczywista konfiguracja logowania jednokrotnego. Otrzymasz powiadomienie podczas logowania jednokrotnego została włączona dla Twojej subskrypcji.
   >

6. W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **Complete** zamknąć **skonfigurować rejestrację jednokrotną** okna dialogowego.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "skonfigurować logowanie jednokrotne")
7. W menu u góry kliknij **atrybuty** otworzyć **atrybuty tokenu SAML** okna dialogowego.
   
   ![Atrybuty](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "atrybutów")
8. Aby dodać mapowania wymaganego atrybutu, wykonaj następujące czynności:
   
   ![Atrybuty](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "atrybutów")
   
   | Nazwa atrybutu | Wartość atrybutu |
   | --- | --- |
   | ClientID |Należy pobrać tę wartość z zespołem pomocy technicznej Benefitsolver. |
   | ClientKey |Należy pobrać tę wartość z zespołem pomocy technicznej Benefitsolver. |
   | LogoutURL |Należy pobrać tę wartość z zespołem pomocy technicznej Benefitsolver. |
   | Identyfikator pracownika |Należy pobrać tę wartość z zespołem pomocy technicznej Benefitsolver. |
   
   1. Dla każdego wiersza danych w tabeli powyżej, kliknij przycisk **Dodaj atrybut użytkownika**.
   2. W **nazwa atrybutu** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.
   3. W **wartość atrybutu** pole tekstowe, wybierz wartość atrybutu wyświetlany dla danego wiersza.
   4. Kliknij przycisk **Complete** (Zakończ).
9. Kliknij przycisk **Zastosuj zmiany**.

## <a name="configure-user-provisioning"></a>Skonfiguruj Inicjowanie obsługi użytkowników
Aby włączyć użytkowników usługi Azure AD zalogować się do Benefitsolver, musi być przygotowana do Benefitsolver.  

W przypadku Benefitsolver pracownika danych jest w aplikacji wypełniać za pomocą pliku spisu z systemu HRIS (zazwyczaj co noc).  

>[!NOTE]
>Możesz użyć innych Benefitsolver użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Benefitsolver do kont użytkowników usługi AAD. 
> 

## <a name="assigning-users"></a>Przypisywanie użytkowników
Aby przetestować konfigurację, musisz przyznać użytkowników usługi Azure AD, czy chcesz zezwolić, używając przypisywania do nich dostęp aplikacji do niego.

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a>Do przypisywania użytkowników do Benefitsolver, wykonaj następujące czynności:
1. W klasycznym portalu Azure Utwórz konto testu.
2. Na ** Benefitsolver ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.
   
   ![Przypisywanie użytkowników](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "przypisywanie użytkowników")
3. Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** o potwierdzenie przypisania.
   
   ![Tak](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "tak")

Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).

