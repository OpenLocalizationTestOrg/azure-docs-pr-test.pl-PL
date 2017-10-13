---
title: 'Samouczek: Integracji Azure Active Directory z Citrix ShareFile | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: b85680104fe4f33638c559b2a12483a2312a4476
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a>Samouczek: Integracji Azure Active Directory z Citrix ShareFile

Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) Citrix ShareFile.

Integracja z usługą Azure AD Citrix ShareFile zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do Citrix ShareFile.
- Umożliwia użytkownikom automatycznie pobrać zalogowane do Citrix ShareFile (logowanie jednokrotne) z konta usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z Citrix ShareFile, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Citrix ShareFile logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodaj Citrix ShareFile z galerii
2. Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

## <a name="add-citrix-sharefile-from-the-gallery"></a>Dodaj Citrix ShareFile z galerii
Aby skonfigurować integrację usługi Azure AD Citrix ShareFile, należy dodać Citrix ShareFile z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać Citrix ShareFile z galerii, wykonaj następujące czynności:**

1. W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Przycisk usługi Azure Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.

    ![Nowy przycisk aplikacji][3]

4. W polu wyszukiwania wpisz **Citrix ShareFile**, wybierz pozycję **Citrix ShareFile** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.

    ![Citrix ShareFile na liście wyników](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Citrix ShareFile w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Citrix ShareFile jest dla użytkownika, w usłudze Azure AD. Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Citrix ShareFile.

W Citrix ShareFile, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Citrix ShareFile, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Citrix ShareFile, połączonej z usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Citrix ShareFile.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Citrix ShareFile, wykonaj następujące czynności:**

1. W portalu Azure na **Citrix ShareFile** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. Na **Citrix ShareFile domeny i adres URL** sekcji, wykonaj następujące czynności:

    ![Adresy URL i domeny ShareFile Citrix pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.sharefile.com/saml/login`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Zaktualizuj tę wartość przy rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta ShareFile Citrix](https://www.citrix.co.in/products/sharefile/support.html) aby zyskać tę wartość. 

4. Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. Na **konfigurację serwera Citrix ShareFile** , kliknij przycisk **skonfigurować Citrix ShareFile** otworzyć **Konfigurowanie logowania jednokrotnego** okna. Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**

    ![Konfiguracja Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **Citrix ShareFile** witryny firmy jako administrator.

8. Na pasku narzędzi u góry kliknij **Admin**.

9. W lewym okienku nawigacji, wybierz **skonfigurować logowanie jednokrotne**.
   
    ![Konto administracji](./media/active-directory-saas-sharefile-tutorial/ic773627.png "konta administracji")

10. Na **rejestracji jednokrotnej / Konfiguracja SAML 2.0** strony okna dialogowego, w obszarze **podstawowe ustawienia**, wykonaj następujące czynności:
   
    ![Logowanie jednokrotne](./media/active-directory-saas-sharefile-tutorial/ic773628.png "logowanie jednokrotne")
   
    a. Kliknij przycisk **Włącz SAML**.
    
    b. W **Your wystawcy IDP / identyfikator jednostki** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.

    c. Kliknij przycisk **zmiany** obok **certyfikatu X.509** pola, a następnie przekaż certyfikat pobrany z portalu Azure.
    
    d. W **adres URL logowania** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.
    
    e. W **adresu URL wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL** którego została skopiowana z portalu Azure.

11. Kliknij przycisk **zapisać** w portalu zarządzania Citrix ShareFile.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu. Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.

    ![Przycisk Dodaj](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. W **użytkownika** okna dialogowego wykonaj następujące czynności:

    ![Okno dialogowe użytkownika](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    a. W **nazwa** wpisz **BrittaSimon**.

    b. W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.

    c. Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-citrix-sharefile-test-user"></a>Tworzenie użytkownika testowego Citrix ShareFile

Aby włączyć użytkowników usługi Azure AD zalogować się do Citrix ShareFile, musi być przygotowana do Citrix ShareFile. W przypadku Citrix ShareFile Inicjowanie obsługi to zadanie ręczne.

**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**

1. Zaloguj się do Twojego **Citrix ShareFile** dzierżawy.

2. Kliknij przycisk **Zarządzanie użytkownikami \> Zarządzanie główną użytkowników \> + Tworzenie pracownika**.
   
   ![Tworzenie pracownika](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Tworzenie pracownika")

3. Na **podstawowe informacje** sekcji, wykonaj następujące czynności:
   
   ![Podstawowe informacje](./media/active-directory-saas-sharefile-tutorial/IC799951.png "podstawowe informacje")
   
   a. W **adres E-mail** tekstowym, wpisz adres e-mail Simona Britta jako  **brittasimon@contoso.com** .
   
   b. W **imię** pole tekstowe, typ **imię** użytkownika jako **Britta**.
   
   c. W **nazwisko** pole tekstowe, typ **nazwisko** użytkownika jako **Simona**.

4. Kliknij przycisk **dodać użytkownika**.
  
   >[!NOTE]
   >Właścicielem konta usługi Azure AD otrzymasz wiadomość e-mail, a następnie kliknij łącze, aby potwierdzić swoje konto, zanim staje się aktywny. Inne narzędzia do tworzenia konta użytkownika Citrix ShareFile lub interfejsów API dostarczonych przez Citrix ShareFile można użyć do udostępnienia konta użytkownika usługi Azure AD.

### <a name="assign-the-azure-ad-test-user"></a>Przypisz użytkownika testowego usługi Azure AD

W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Citrix ShareFile.

![Przypisanie roli użytkownika][200] 

**Aby przypisać Simona Britta Citrix ShareFile, wykonaj następujące czynności:**

1. W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **Citrix ShareFile**.

    ![Łącze Citrix ShareFile na liście aplikacji](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Łącze "Użytkownicy i grupy"][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![W okienku Dodaj przydziału][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Po kliknięciu kafelka Citrix ShareFile w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Citrix ShareFile.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

