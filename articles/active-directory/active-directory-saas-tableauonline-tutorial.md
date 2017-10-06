---
title: "Samouczek: Integracja usługi Azure Active Directory z usługą Tableau Online | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Tableau Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a>Samouczek: Integracja usługi Azure Active Directory z usługą Tableau Online

Z tego samouczka, dowiesz się, jak toointegrate Tableau Online z usługą Azure Active Directory (Azure AD).

Integrowanie Tableau Online z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooTableau Online
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTableau Online (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD Tableau online należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Tableau Online logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Tableau Online z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-tableau-online-from-hello-gallery"></a>Dodawanie Tableau Online z galerii hello
tooconfigure hello integracji Tableau Online z usługą Azure AD, należy tooadd Tableau Online z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Tableau Online z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Tableau Online**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. W panelu wyników hello, wybierz **Tableau Online**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji można skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Tableau Online na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello Tableau online jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w trybie Online Tableau musi toobe ustanowione.

W Tableau w trybie Online, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Tableau Online, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Tableau Online](#creating-a-tableau-online-test-user)**  -toohave odpowiednikiem Simona Britta w Tableau Online, które zostało połączone toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w trybie Online Tableau aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Tableau Online wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **Tableau Online** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. Na powitania **Tableau Online domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    a. W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello:`https://sso.online.tableau.com`

    b. W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://sso.online.tableau.com/public/sp/<instancename>`

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. W oknie innej przeglądarki, logowania jednokrotnego tooyour aplikacji Tableau Online. Przejdź za**ustawienia** , a następnie **uwierzytelniania**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. tooenable SAML, w obszarze **typy uwierzytelniania** sekcji. Sprawdź hello **rejestracji jednokrotnej z SAML** wyboru.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. Przewiń w dół do **Importowanie pliku metadanych do Tableau Online** sekcji.  Kliknij przycisk Przeglądaj i zaimportować plik metadanych hello, które zostały pobrane z usługi Azure AD. Następnie kliknij przycisk **Zastosuj**.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. W hello **odpowiada potwierdzenia** sekcję należy wstawić hello odpowiedniego dostawcy tożsamości potwierdzenia nazwę **adres e-mail**, **imię**, i **nazwisko** . tooget te informacje z usługi Azure AD: 
  
    a. W portalu Azure Witaj, przejdź na powitania **Tableau Online** strony integracja aplikacji.
    
    b. W sekcji atrybuty hello, wybierz hello **"wyświetlić i edytować wszystkie atrybuty użytkowników"** pola wyboru. 
    
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    c. Skopiuj wartość przestrzeni nazw hello tych atrybutów: givenname, poczty e-mail i nazwisko przy użyciu hello następujące kroki:

   ![Azure AD rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    d. Kliknij przycisk **user.givenname** wartości 
    
    e. Skopiuj wartość hello z hello **przestrzeni nazw** pola tekstowego.

   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    f. toocopy hello namesapce wartości hello poczty e-mail i nazwisko wykonaj hello w poprzednich krokach.

    g. Przełącz toohello aplikacji Tableau Online, a następnie ustaw hello **Tableau Online atrybuty** sekcji w następujący sposób:
     * Adres e-mail: **poczty** lub **userprincipalname**
     * Imię: **givenname**
     * Nazwisko: **nazwisko**
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-tableau-online-test-user"></a>Tworzenie użytkownika testowego Tableau Online

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Tableau online.

1. Na **Tableau Online**, kliknij przycisk **ustawienia** , a następnie **uwierzytelniania** sekcji. Przewiń w dół za**Wybieranie: Użytkownicy** sekcji. Kliknij przycisk **dodawania użytkowników** , a następnie **wprowadź adresy E-mail**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. Wybierz **Dodawanie użytkowników do uwierzytelniania rejestracji jednokrotnej (SSO)**. W hello **wprowadź adresy E-mail** Dodaj pole tekstowebritta.simon@contoso.com
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. Kliknij przycisk **Utwórz**.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTableau w trybie Online.

![Przypisz użytkownika][200] 

**tooassign tooTableau Simona Britta w trybie Online, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Tableau Online**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Tableau Online hello w hello Panel dostępu, należy pobrać aplikacji Tableau Online tooyour zalogowane automatycznie.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

