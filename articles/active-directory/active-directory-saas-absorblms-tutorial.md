---
title: "Samouczek: Integracji Azure Active Directory z przyjęcia LMS | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i przyjęcia LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 3c68c3ac7d6be593476d419f8c015931b206eead
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a>Samouczek: Integracji Azure Active Directory z przyjęcia LMS

Z tego samouczka dowiesz się integrowanie LMS przyjęcia w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD przyjęcia LMS zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do przyjęcia LMS
- Umożliwia użytkownikom automatycznie pobrać zalogowane do przyjęcia LMS (logowanie jednokrotne) z konta usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz. [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z przyjęcia LMS, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Przyjęcia LMS jednokrotnego włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie przyjęcia LMS z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-absorb-lms-from-the-gallery"></a>Dodawanie przyjęcia LMS z galerii
Aby skonfigurować integrację przyjęcia LMS w usłudze Azure AD, należy dodać przyjęcia LMS z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać przyjęcia LMS z galerii, wykonaj następujące czynności:**

1. W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Przycisk usługi Azure Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.

    ![Nowy przycisk aplikacji][3]

4. W polu wyszukiwania wpisz **przyjęcia LMS**, wybierz pozycję **przyjęcia LMS** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.

    ![Przyjęcia LMS na liście wyników](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przyjęcia LMS oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w przyjęcia LMS jest dla użytkownika, w usłudze Azure AD. Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w przyjęcia LMS musi się.

Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w LMS przyjęcia.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przyjęcia LMS, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego przyjęcia LMS](#create-an-absorb-lms-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta przyjęcia LMS połączonego z usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji LMS przyjęcia.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z przyjęcia LMS, wykonaj następujące czynności:**

1. W portalu Azure na **przyjęcia LMS** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. Na **adresy URL i przyjęcia domeny LMS** sekcji, wykonaj następujące czynności:

    ![Przyjęcia LMS domeny i adres URL pojedynczego logowania jednokrotnego informacji](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    a. W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.myabsorb.com/Account/SAML`

    b. W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.myabsorb.com/Account/SAML`
     
    > [!NOTE] 
    > Wartości te nie są rzeczywistych. Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości. Skontaktuj się z [zespołem pomocy technicznej klienta LMS przyjęcia](https://www.absorblms.com/support) uzyskać te wartości. 

4. Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. Na **przyjęcia konfiguracji LMS** , kliknij przycisk **skonfigurować LMS przyjęcia** otworzyć **Konfigurowanie logowania jednokrotnego** okna. Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**

    ![Przyjęcia LMS konfiguracji](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do przyjęcia LMS witryny firmy.

9. Kliknij przycisk **ikonę konta** w interfejsie administratora. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/1.png)

10. Kliknij przycisk **ustawienia portalu**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. Kliknij przycisk **użytkowników** kartę.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/3.png)

12. Wykonaj poniższe kroki, aby uzyskać dostępu do pola konfiguracji rejestracji jednokrotnej:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/4.png)

    a. Wybierz odpowiednie **tryb**.

    b. Usuń certyfikat został już pobrany z portalu Azure w programie Notatnik Otwórz **---BEGIN CERTIFICATE---** i **---END CERTIFICATE---** tag, a następnie wklej zawartość pozostałych **klucza** pola tekstowego.
    
    c. W **właściwość identyfikatora**, wybierz odpowiedni atrybut, który skonfigurowano jako identyfikator użytkownika w usłudze Azure AD (na przykład, jeśli wybrano userprinciplename w usłudze Azure AD, a następnie zaznaczony tutaj nazwę użytkownika.)

    d. W **adres URL logowania**, Wklej **"SAML pojedynczy znak na adres URL usługi"** wartość została skopiowana z **Konfigurowanie logowania jednokrotnego** okna portalu Azure.

    e. W **adresu URL wylogowania**, Wklej **"Adres URL Sign-Out"** wartość została skopiowana z **Konfigurowanie logowania jednokrotnego** okna portalu Azure.

13. Włącz **"Zezwalaj tylko na logowanie SSO"**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/5.png)

14. Kliknij przycisk **"Zapisz".**

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu. Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.

![Tworzenie użytkownika testowego usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.
 
    ![Przycisk Dodaj](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    a. W **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.

    d. Kliknij przycisk **Utwórz**.

### <a name="create-an-absorb-lms-test-user"></a>Tworzenie użytkownika testowego przyjęcia LMS

Aby umożliwić użytkownikom usługi Azure AD zalogować się do przyjęcia LMS, ich należy udostępnić w celu przyjęcia LMS.  
W przypadku przyjęcia LMS inicjowania obsługi administracyjnej jest zadanie ręczne.

**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**

1. Zaloguj się do witryny firmy przyjęcia LMS jako administrator.

2. Kliknij przycisk **użytkowników** kartę.

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. Kliknij przycisk **użytkowników** w obszarze **użytkowników** kartę.

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  Wybierz **użytkownika** z **Dodaj nowy** listy rozwijanej.

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. Na **Dodaj użytkownika** wykonaj następujące czynności:

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/user.png)

    a. W **imię** pole tekstowe, nazwa typu pierwszy, takich jak Britta.

    b. W **nazwisko** tekstowym, wpisz nazwisko, takich jak Simona.
    
    c. W **Username** tekstowym, wpisz nazwę użytkownika, takich jak Simona Britta.

    d. W **hasło** tekstowym, wpisz hasło Simona Britta.

    e. W **Potwierdź hasło** tekstowym, wpisz to samo hasło.
    
    f. Należy go jako **ACTIVE**.   

6. Kliknij przycisk **"Zapisz".**
 
### <a name="assign-the-azure-ad-test-user"></a>Przypisz użytkownika testowego usługi Azure AD

W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do przyjęcia LMS.

![Przypisanie roli użytkownika][200]

**Aby przypisać Simona Britta do przyjęcia LMS, wykonaj następujące czynności:**

1. W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **przyjęcia LMS**.

    ![Łącze przyjęcia LMS na liście aplikacji](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Łącze "Użytkownicy i grupy"][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![W okienku Dodaj przydziału][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Kliknij Kafelek LMS przyjęcia w panelu dostępu, użytkownik będzie uzyskać automatycznie zalogowane do przyjęcia LMS aplikacji. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

