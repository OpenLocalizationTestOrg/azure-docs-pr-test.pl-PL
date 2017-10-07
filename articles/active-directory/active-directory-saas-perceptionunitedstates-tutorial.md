---
title: "Samouczek: Integracji Azure Active Directory z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Stanów Zjednoczonych z punktu widzenia użytkownika (Non-UltiPro)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a>Samouczek: Integracji Azure Active Directory z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro)

Z tego samouczka, dowiesz się, jak toointegrate wrażenie Stanów Zjednoczonych (Non-UltiPro) w usłudze Azure Active Directory (Azure AD).

Integrowanie z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro) z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooPerception Stanów Zjednoczonych (Non-UltiPro).
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPerception Stanów Zjednoczonych (Non-UltiPro) (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z punktu widzenia użytkownika Stany Zjednoczone (inne niż UltiPro), należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro) logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie z galerii hello wrażenie Stany Zjednoczone (Non-UltiPro)
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a>Dodawanie z galerii hello wrażenie Stany Zjednoczone (Non-UltiPro)
tooconfigure hello integracji z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro) do usługi Azure AD, należy tooadd wrażenie Stany Zjednoczone (Non-UltiPro) z listy tooyour galerii hello zarządzanych aplikacji SaaS.

**tooadd wrażenie Stany Zjednoczone (Non-UltiPro) z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W hello wyszukiwania wpisz **wrażenie Stany Zjednoczone (Non-UltiPro)**, wybierz pozycję **wrażenie Stany Zjednoczone (Non-UltiPro)** z panelu wyników kliknięcie **Dodaj** tooadd przycisk Aplikacja Hello.

    ![Z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro) na liście wyników hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z punktu widzenia użytkownika Stanów Zjednoczonych (Non-UltiPro) w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello używanego w Stanach Zjednoczonych z punktu widzenia użytkownika (Non-UltiPro) jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Stanach Zjednoczonych z punktu widzenia użytkownika (Non-UltiPro) musi toobe ustanowione.

W wrażenie Stanów Zjednoczonych (inne niż UltiPro), przypisz wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z punktu widzenia użytkownika Stany Zjednoczone (inne niż UltiPro), należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave odpowiednikiem Simona Britta w wrażenie Stanów Zjednoczonych (inne niż UltiPro), który jest odpowiednikiem połączonych toohello usługi Azure AD użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro).

**tooconfigure usługi Azure AD rejestracji jednokrotnej z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro), wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **wrażenie Stany Zjednoczone (Non-UltiPro)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. Na powitania **domeny wrażenie Stany Zjednoczone (Non-UltiPro) i adresy URL** sekcji, wykonaj następujące kroki hello:

    ![Z punktu widzenia użytkownika domeny Stanów Zjednoczonych (Non-UltiPro) i adres URL z jednym informacje logowania jednokrotnego](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    a. W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://perception.kanjoya.com/sp`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://perception.kanjoya.com/sso?idp=<entity_id>`

    > [!NOTE] 
    > wartość Hello nie jest prawdziwe. Wartość hello zostanie zaktualizowany hello rzeczywiste odpowiedzi adresu URL, który znajduje się w dalszej części samouczka hello.
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji wrażenie Stany Zjednoczone (Non-UltiPro)** , kliknij przycisk **skonfigurować wrażenie Stany Zjednoczone (Non-UltiPro)** tooopen **Konfigurowanie logowania jednokrotnego** okno. Kopiuj hello **SAML identyfikator jednostki** z hello **sekcji krótkimi opisami.**

    a. Hello **wrażenie Stany Zjednoczone (Non-UltiPro)** aplikacja wymaga hello **identyfikator jednostki SAML** kodowany identyfikator uri toobe wartość, która została skopiowana,. wartość identyfikatora uri zakodowane hello tooget, użyj hello łącza:**http://www.url-encode-decode.com/**.

    b. Po pierwsze hello uri zakodowaną wartość połączyć ją z hello **adres URL odpowiedzi** wymienionych poniżej -

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    c. Wklej hello większa niż wartość w hello **adres URL odpowiedzi** textbox w **domeny wrażenie Stany Zjednoczone (Non-UltiPro) i adresy URL** sekcji.

    ![Konfiguracja Stanów Zjednoczonych (z systemem innym niż UltiPro) z punktu widzenia użytkownika](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. W innym oknie przeglądarki Zaloguj się w witrynie firmy wrażenie Stany Zjednoczone (Non-UltiPro) tooyour jako administrator.

8. Witaj głównym pasku narzędzi, kliknij przycisk **ustawienia konta**.

    ![Użytkownik Stanów Zjednoczonych (Non-UltiPro) z punktu widzenia użytkownika](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. Na powitania **ustawienia konta** wykonaj hello następujące kroki:

    ![Użytkownik Stanów Zjednoczonych (Non-UltiPro) z punktu widzenia użytkownika](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    a. W hello **nazwa firmy** pole tekstowe, nazwa typu hello hello **firmy**.
    
    b. W hello **nazwa konta** pole tekstowe, nazwa typu hello hello **konta**.

    c. W **domyślne odpowiedzi tooEmail** pole tekstowe, hello typu, prawidłową **E-mail**.

    d. Wybierz **dostawcy tożsamości logowania jednokrotnego** jako **SAML 2.0**.

10. Na powitania **konfiguracji logowania jednokrotnego** wykonaj hello następujące kroki:

    ![SSOConfig Stanów Zjednoczonych (z systemem innym niż UltiPro) z punktu widzenia użytkownika](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    a. Wybierz **typu NameID SAML** jako **E-mail**.

    b. W hello **Nazwa konfiguracji logowania jednokrotnego** pole tekstowe, nazwa typu hello Twojej **konfiguracji**.
    
    c. W **Nazwa dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure. 

    d. W **textbox domeny SAML**, wprowadź domenę hello, takich jak  **@contoso.com** .

    e. Polecenie **Przekaż ponownie** tooupload hello **XML metadanych** pliku.

    f. Kliknij przycisk **aktualizacji**.


> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a>Tworzenie użytkownika testowego z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro)

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Stanach Zjednoczonych z punktu widzenia użytkownika (Non-UltiPro). Praca z [zespołem pomocy technicznej z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) użytkowników hello tooadd hello wrażenie Stany Zjednoczone (Non-UltiPro) platformy.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPerception Stany Zjednoczone (Non-UltiPro).

![Przypisanie roli użytkownika hello][200] 

**tooassign Simona Britta tooPerception Stany Zjednoczone (Non-UltiPro), wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **wrażenie Stany Zjednoczone (Non-UltiPro)**.

    ![łącze wrażenie Stany Zjednoczone (Non-UltiPro) Hello na liście aplikacji hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka wrażenie Stany Zjednoczone (Non-UltiPro) hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro).
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

