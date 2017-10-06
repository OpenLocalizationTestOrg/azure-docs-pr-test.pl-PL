---
title: 'Samouczek: Integracji Azure Active Directory z Workstars | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Workstars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a>Samouczek: Integracji Azure Active Directory z Workstars

Z tego samouczka, dowiesz się, jak toointegrate Workstars w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Workstars zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooWorkstars.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWorkstars (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Workstars należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Workstars logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Workstars z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-workstars-from-hello-gallery"></a>Dodawanie Workstars z galerii hello
tooconfigure hello integracji Workstars do usługi Azure AD, należy tooadd Workstars z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Workstars z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **Workstars**, wybierz pozycję **Workstars** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Workstars hello listy wyników](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Workstars w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Workstars jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Workstars musi toobe ustanowione.

W Workstars, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Workstars, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Workstars](#create-a-workstars-test-user)**  -toohave odpowiednikiem Simona Britta w Workstars, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Workstars.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Workstars, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Workstars** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. Na powitania **Workstars domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Adresy URL i domeny Workstars pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    a. W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://workstars.com`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.workstars.com/saml/login_check`

    > [!NOTE] 
    > wartość Hello nie jest prawdziwe. Wartość hello aktualizacji z hello rzeczywisty adres URL odpowiedzi. Skontaktuj się z [Workstars obsługuje zespołu](https://support.workstars.com) tooget hello wartość.
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Workstars** kliknij **skonfigurować Workstars** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfiguracja Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. W innym oknie przeglądarki Zaloguj się w witrynie firmy Workstars tooyour jako administrator.

8. Witaj głównym pasku narzędzi, kliknij przycisk **ustawienia**.

    ![Ustaw Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. Przejdź za**Sign On** > **ustawienia**.

    ![Logować Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Ustawienia Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. Na powitania **pojedynczy znak na (SAML) — ustawienia** wykonaj hello następujące kroki:
    
    ![Workstars saml](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    a. W **Nazwa dostawcy tożsamości** pole tekstowe, typ **usługi Office 365**.

    b. W hello **identyfikator jednostki dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.

    c. Kopiowanie zawartości hello hello pliku pobranego certyfikatu w programie Notatnik, a następnie wklej go do hello **x509 certyfikatu** pola tekstowego. 

    d. W hello **adres URL logowania jednokrotnego SAML** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.
    
    e. W hello **zdalnego adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL**, które zostały skopiowane z portalu Azure. 

    f. Wybierz **Identyfikatora nazwy** jako **poczty E-mail (ustawienie domyślne)**.

    g. Kliknij przycisk **potwierdzić**.
    
> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
  
### <a name="create-a-workstars-test-user"></a>Tworzenie użytkownika testowego Workstars

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Workstars. Praca z [Workstars obsługuje zespołu](https://support.workstars.com) użytkowników hello tooadd hello Workstars platformy.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWorkstars.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooWorkstars Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Workstars**.

    ![łącze Workstars Hello na liście aplikacji hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu powitalne Workstars kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Workstars aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

