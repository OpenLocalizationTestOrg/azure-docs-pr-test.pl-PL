---
title: 'Samouczek: Integracji Azure Active Directory z Pantheon | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Pantheon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3f4ac1db2ee83d9f9fcb375d0fb7c40ad21c4688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a>Samouczek: Integracji Azure Active Directory z Pantheon

Z tego samouczka dowiesz się integrowanie Pantheon z usługi Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Pantheon zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do Pantheon
- Umożliwia użytkownikom automatycznie pobrać zalogowane do Pantheon (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z Pantheon, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Pantheon logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Pantheon z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-pantheon-from-the-gallery"></a>Dodawanie Pantheon z galerii
Aby skonfigurować integrację usługi Azure AD Pantheon, należy dodać Pantheon z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać Pantheon z galerii, wykonaj następujące czynności:**

1. W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania wpisz **Pantheon**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. W panelu wyników wybierz **Pantheon**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pantheon w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Pantheon jest dla użytkownika, w usłudze Azure AD. Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Pantheon musi się.

W Pantheon, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pantheon, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Pantheon](#creating-a-pantheon-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Pantheon połączonego z usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Pantheon.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Pantheon, wykonaj następujące czynności:**

1. W portalu Azure na **Pantheon** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. Na **Pantheon domeny i adres URL** sekcji, wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    a. W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`urn:auth0:pantheon:<orgname>-SSO`

    b. W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości. Skontaktuj się z [zespołem pomocy technicznej Pantheon](https://pantheon.io/docs/getting-support/) uzyskać te wartości.

4. Aplikacja pantheon oczekuje potwierdzenia języka SAML w określonym formacie, który należy ustawić wartość atrybutu UserIdentifier z adresu e-mail użytkownika. Domyślnie usługi Azure AD używa właściwości UserPrincipalName UserIdentifier atrybutu. Jednak dla pomyślnej integracji musisz dostosować tę wartość do dopasowania z adresu e-mail użytkownika. Integracja działa tylko po wykonaniu poprawne mapowania.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. Na **konfiguracji Pantheon** , kliknij przycisk **skonfigurować Pantheon** otworzyć **Konfigurowanie logowania jednokrotnego** okna. Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. Aby skonfigurować logowanie jednokrotne w **Pantheon** stronie, musisz wysłać pobrany **certyfikatu** i **SAML pojedynczy znak na adres URL usługi** do [Pantheon obsługuje zespołu](https://pantheon.io/docs/getting-support/).

     > [!Note]
     > Należy również zawierają informacje domeny poczty E-mail oraz Data i godzina, gdy chcesz włączyć tego połączenia. Można znaleźć więcej szczegółów na temat z [tutaj](https://pantheon.io/docs/sso-organizations/)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu. Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    a. W **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-pantheon-test-user"></a>Tworzenie użytkownika testowego Pantheon

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Pantheon. Wykonaj następujące czynności, aby dodać użytkownika w Pantheon. 

>[!NOTE] 
>Do logowania jednokrotnego pracować użytkownik musi najpierw należy utworzyć w Pantheon.

1. Zaloguj się do Pantheon przy użyciu poświadczeń administratora.

2. Przejdź do **organizacji** strony pulpitu nawigacyjnego.
 
3. Kliknij przycisk **osób**.

4. Kliknij przycisk **Dodaj użytkownika**.

5. Wprowadź adres e-mail użytkownika.

6. Wybierz rolę użytkownika.

7. Kliknij przycisk **Dodaj użytkownika**.

### <a name="assigning-the-azure-ad-test-user"></a>Przypisanie użytkownika testowego usługi Azure AD

W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Pantheon.

![Przypisz użytkownika][200] 

**Aby przypisać Simona Britta Pantheon, wykonaj następujące czynności:**

1. W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **Pantheon**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Po kliknięciu kafelka Pantheon w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Pantheon.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

