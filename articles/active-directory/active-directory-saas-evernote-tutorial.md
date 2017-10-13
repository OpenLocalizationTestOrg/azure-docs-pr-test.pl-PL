---
title: 'Samouczek: Integracji Azure Active Directory z Evernote | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Evernote."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: be94152a84bbbeacb623d7dd8b540e3981931a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a>Samouczek: Integracji Azure Active Directory z Evernote

Z tego samouczka dowiesz się integrowanie Evernote z usługi Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Evernote zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do Evernote.
- Umożliwia użytkownikom automatycznie pobrać zalogowane do Evernote (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z Evernote, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Evernote logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Evernote z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-evernote-from-the-gallery"></a>Dodawanie Evernote z galerii
Aby skonfigurować integrację usługi Azure AD Evernote, należy dodać Evernote z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać Evernote z galerii, wykonaj następujące czynności:**

1. W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Przycisk usługi Azure Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.

    ![Nowy przycisk aplikacji][3]

4. W polu wyszukiwania wpisz **Evernote**, wybierz pozycję **Evernote** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.

    ![Evernote na liście wyników](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Evernote w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Evernote jest dla użytkownika, w usłudze Azure AD. Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Evernote musi się.

W Evernote, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Evernote, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Evernote](#create-an-evernote-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Evernote połączonego z usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Evernote.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Evernote, wykonaj następujące czynności:**

1. W portalu Azure na **Evernote** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. Na **Evernote domeny i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w trybie IDP inicjowane:

    ![Adresy URL i domeny Evernote pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    W **identyfikator** tekstowym, wpisz adres URL:`https://www.evernote.com/saml2`

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonać następujący krok, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:

    ![Adresy URL i domeny Evernote pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    W **Zaloguj się na adres URL** tekstowym, wpisz adres URL:`https://www.evernote.com/Login.action`   

5. Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. Na **konfiguracji Evernote** , kliknij przycisk **skonfigurować Evernote** otworzyć **Konfigurowanie logowania jednokrotnego** okna. Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**

    ![Konfiguracja Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Evernote jako administrator.

9. Przejdź do **"Konsoli administracyjnej"**

    ![Konsola administracyjna](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. Z **"Konsoli administracyjnej"**, przejdź do **"Zabezpieczenia"** i wybierz **"Logowanie jednokrotne"**

    ![Ustawienia logowania jednokrotnego](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. Skonfiguruj następujące wartości:

    ![Ustawienia certyfikatów](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    a.  **Włącz logowanie Jednokrotne:** rejestracji Jednokrotnej jest domyślnie włączona (kliknij **wyłączyć logowanie jednokrotne** Aby usunąć wymaganie logowania jednokrotnego)

    b. Wklej **SAML rejestracji jednokrotnej adres URL usługi** wartość, która została skopiowana z portalu Azure do **adres URL żądania HTTP SAML** pola tekstowego.

    c. Otwórz certyfikat pobrany z usługi Azure AD w programie Notatnik i skopiuj zawartość, w tym "Certyfikat BEGIN" i "END CERTIFICATE" i wklej ją do **certyfikatu X.509** pola tekstowego. 

    d.Click **zapisać zmiany**

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu. Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.

    ![Przycisk Dodaj](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. W **użytkownika** okna dialogowego wykonaj następujące czynności:

    ![Okno dialogowe użytkownika](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    a. W **nazwa** wpisz **BrittaSimon**.

    b. W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.

    c. Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-an-evernote-test-user"></a>Tworzenie użytkownika testowego Evernote

Aby włączyć użytkowników usługi Azure AD zalogować się do Evernote, musi być przygotowana do Evernote.  
W przypadku Evernote Inicjowanie obsługi to zadanie ręczne.

**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**

1. Zaloguj się do witryny firmy Evernote jako administrator.

2. Kliknij przycisk **"Konsoli administracyjnej"**.

    ![Konsola administracyjna](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. Z **"Konsoli administracyjnej"**, przejdź do **"Dodawanie użytkowników"**.

    ![Dodaj testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. **Dodawanie członków zespołu** w **E-mail** tekstowym, wpisz adres e-mail konta użytkownika i kliknij przycisk **zaprosić.**

    ![Dodaj testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. Po wysłaniu zaproszenia, właścicielem konta usługi Azure Active Directory zostanie wysłana wiadomość e-mail o zaakceptowanie zaproszenia.

### <a name="assign-the-azure-ad-test-user"></a>Przypisz użytkownika testowego usługi Azure AD

W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Evernote.

![Przypisanie roli użytkownika][200] 

**Aby przypisać Simona Britta Evernote, wykonaj następujące czynności:**

1. W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **Evernote**.

    ![Łącze Evernote na liście aplikacji](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Łącze "Użytkownicy i grupy"][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![W okienku Dodaj przydziału][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Po kliknięciu kafelka Evernote w panelu dostępu użytkownik powinien pobrać zalogowane do aplikacji Evernote. Można będzie można logować się jako organizacji konta muszą jednak następnie zaloguj się przy użyciu konta osobistego. 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

