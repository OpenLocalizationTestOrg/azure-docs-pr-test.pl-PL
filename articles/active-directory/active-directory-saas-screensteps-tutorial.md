---
title: 'Samouczek: Integracji Azure Active Directory z ScreenSteps | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a>Samouczek: Integracji Azure Active Directory z ScreenSteps

Z tego samouczka, dowiesz się, jak toointegrate ScreenSteps w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD ScreenSteps zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooScreenSteps.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooScreenSteps (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z ScreenSteps należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- ScreenSteps logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie ScreenSteps z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-screensteps-from-hello-gallery"></a>Dodawanie ScreenSteps z galerii hello
tooconfigure hello integracji ScreenSteps do usługi Azure AD, należy tooadd ScreenSteps z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd ScreenSteps z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **ScreenSteps**, wybierz pozycję **ScreenSteps** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![ScreenSteps hello listy wyników](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ScreenSteps w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w ScreenSteps jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w ScreenSteps musi toobe ustanowione.

W ScreenSteps, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ScreenSteps, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego ScreenSteps](#create-a-screensteps-test-user)**  -toohave odpowiednikiem Simona Britta w ScreenSteps, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji ScreenSteps.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z ScreenSteps, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **ScreenSteps** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. Na powitania **ScreenSteps domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Adresy URL i domeny ScreenSteps pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.ScreenSteps.com`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Zaktualizuj tę wartość z hello rzeczywisty logowania jednokrotnego adresu URL, który znajduje się w dalszej części tego samouczka. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji ScreenSteps** kliknij **skonfigurować ScreenSteps** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfiguracja ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy ScreenSteps jako administrator.

8. Kliknij przycisk **ustawienia konta**.

    ![Zarządzanie kontami](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Zarządzanie kontami")

9. Kliknij przycisk **logowanie jednokrotne**.

    ![Zdalne uwierzytelnianie](./media/active-directory-saas-screensteps-tutorial/ic778524.png "uwierzytelniania zdalnego")

10. Kliknij przycisk **Tworzenie końcowego rejestracji jednokrotnej**.

    ![Zdalne uwierzytelnianie](./media/active-directory-saas-screensteps-tutorial/ic778525.png "uwierzytelniania zdalnego")

11. W hello **utworzyć jeden znak na punkt końcowy** sekcji, wykonaj następujące kroki hello:

    ![Tworzenie punktu końcowego uwierzytelniania](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Tworzenie punktu końcowego uwierzytelniania")
    
    a. W hello **tytuł** tekstowym, wpisz tytuł.
    
    b. Z hello **tryb** listy, wybierz **SAML**.
    
    c. Kliknij przycisk **Utwórz**.

12. **Edytuj** hello nowy punkt końcowy.

    ![Edytuj punktu końcowego](./media/active-directory-saas-screensteps-tutorial/ic778528.png "edycji punktu końcowego")

13. W hello **edytować jeden znak na punkt końcowy** sekcji, wykonaj następujące kroki hello:

    ![Uwierzytelniania zdalnego punktu końcowego](./media/active-directory-saas-screensteps-tutorial/ic778527.png "uwierzytelniania zdalnego punktu końcowego")

    a. Kliknij przycisk **Przekaż nowy plik certyfikatu SAML**, a następnie przekaż hello certyfikatu, który został pobrany z portalu Azure.
    
    b. Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z hello portalu Azure do hello **zdalnego adresu URL logowania** pola tekstowego.
    
    c. Wklej **Sign-Out URL** wartość, która została skopiowana z hello portalu Azure do hello **adres URL wylogowania** pola tekstowego.
    
    d. Wybierz **grupy** tooassign toowhen użytkowników, które zostały udostępnione.
    
    e. Kliknij przycisk **aktualizacji**.

    f. Witaj kopii **adres URL klienta SAML** toohello Schowka i Wklej w toohello **adres URL logowania** textbox w **ScreenSteps domeny i adres URL** sekcji.
    
    g. Zwraca toohello **edytować jeden znak na punkt końcowy**.
    
    h. Kliknij przycisk hello **domyślnym kontem** przycisk toouse ten punkt końcowy dla wszystkich użytkowników, którzy logują ScreenSteps. Alternatywnie możesz kliknąć hello **dodać tooSite** przycisk toouse ten punkt końcowy dla określonych witryn internetowych w **ScreenSteps**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-screensteps-test-user"></a>Tworzenie użytkownika testowego ScreenSteps

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w ScreenSteps. Praca z [zespołem pomocy technicznej klienta ScreenSteps](https://www.screensteps.com/contact) do dodawania użytkowników hello hello ScreenSteps platformy. Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej. 

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooScreenSteps.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooScreenSteps Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **ScreenSteps**.

    ![łącze ScreenSteps Hello na liście aplikacji hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu powitalne ScreenSteps kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour ScreenSteps aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

