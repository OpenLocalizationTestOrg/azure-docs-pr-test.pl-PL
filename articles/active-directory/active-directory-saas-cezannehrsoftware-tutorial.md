---
title: 'Samouczek: Azure Active Directory integracji z oprogramowaniem Cezanne HR | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między oprogramowaniem Cezanne HR i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a>Samouczek: Integrowanie usługi Azure Active Directory z oprogramowaniem Cezanne HR

Z tego samouczka, dowiesz się, jak toointegrate Cezanne HR oprogramowania w usłudze Azure Active Directory (Azure AD).

Integracja oprogramowania Cezanne HR z usługą Azure AD zapewnia hello następujące korzyści. Możesz:

- Kontrolowanie w usłudze Azure AD, kto ma dostęp do tooCezanne HR oprogramowania.
- Włączanie logowania tooautomatically użytkowników oprogramowania tooCezanne HR rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD.
- Zarządzanie kont w jednej centralnej lokalizacji: hello portalu Azure.

toolearn więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowania jednokrotnego w usłudze Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z oprogramowaniem Cezanne HR należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Logowanie Jednokrotne włączone subskrypcji oprogramowania Cezanne HR

> [!NOTE]
> Zalecamy tootest hello kroki opisane w tym samouczku, nie używaj do środowiska produkcyjnego.

kroki hello tootest w tym samouczku, wykonaj te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować logowania jednokrotnego programu Azure AD w środowisku testowym. 

Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

* Dodawanie oprogramowania Cezanne HR z galerii hello
* Konfigurowanie i testowania logowania jednokrotnego programu Azure AD

## <a name="add-cezanne-hr-software-from-hello-gallery"></a>Dodawanie oprogramowania Cezanne HR z galerii hello
Integracja hello tooconfigure Cezanne HR oprogramowania do usługi Azure AD, Dodaj oprogramowania Cezanne HR hello galerii tooyour listy zarządzanych aplikacji SaaS.

tooadd Cezanne HR oprogramowania z galerii hello hello następujące:

1. W hello  **[portalu Azure](https://portal.azure.com)**, w lewym okienku hello, wybierz hello **usługi Azure Active Directory** przycisku. 

    ![przycisk "Azure Active Directory" Hello][1]

2. Wybierz **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.

    ![Witaj link "Wszystkie aplikacje"][2]
    
3. tooadd nową aplikację, u góry hello hello **wszystkie aplikacje** okno dialogowe, wybierz opcję **nowej aplikacji**.

    ![Witaj "Nowej aplikacji" przycisku][3]

4. W polu wyszukiwania hello wpisz **Cezanne HR oprogramowania**.

    ![pole wyszukiwania Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. Na liście wyników hello, wybierz **Cezanne HR oprogramowania** , a następnie wybierz hello **Dodaj** przycisk tooadd hello aplikacji.

    ![Lista wyników Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji możesz skonfigurować i przetestować logowania jednokrotnego programu Azure AD z oprogramowaniem Cezanne HR oparte na koncie użytkownika testu o nazwie "Britta Simona".

Aby toowork logowania jednokrotnego usługi Azure AD musi użytkownika usługi Azure AD toohello odpowiednikiem oprogramowania tooknow hello Cezanne HR. Innymi słowy musi ustanowić relację łącza między użytkownika usługi Azure AD i hello użytkownikowi, w hello Cezanne HR oprogramowania.

Relacja linku hello tooestablish, przypisz hello oprogramowania Cezanne HR **nazwy użytkownika** wartość jako hello Azure AD **Username** wartość.

tooconfigure i testowania Azure AD logowania jednokrotnego za pomocą oprogramowania Cezanne HR, pełną powitania po bloków konstrukcyjnych.

### <a name="configure-azure-ad-sso"></a>Konfigurowanie usługi Azure AD logowania jednokrotnego.

W tej sekcji możesz włączenia funkcji logowania jednokrotnego usługi Azure AD w portalu Azure hello i konfigurowanie logowania jednokrotnego w używanej aplikacji Cezanne HR hello następujący:

1. W portalu Azure na powitania hello **oprogramowania HR Cezanne** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.

    ![Witaj "Logowanie jednokrotne" polecenia][4]

2. tooenable logowanie Jednokrotne, w hello **logowanie jednokrotne** okno dialogowe, wybierz opcję hello **tryb** jako **na języku SAML logowania jednokrotnego**.
 
    ![pole "Tryb" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. W obszarze **Cezanne HR oprogramowania domeny i adres URL**, hello następujące:

    ![Witaj w sekcji "Cezanne HR oprogramowania domeny i adresy URL"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    a. W hello **adres URL logowania** wpisz adres URL, który ma hello następującej składni:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`

    b. W hello **adres URL odpowiedzi** wpisz adres URL, który ma hello następującej składni:`https://w3.cezanneondemand.com:443/<tenantid>`    
     
    > [!NOTE] 
    > Witaj poprzedniej wartości nie są prawdziwe. Zaktualizuj je z adresu URL odpowiedzi rzeczywiste hello i hello adres URL logowania. wartości hello tooobtain, skontaktuj się z pomocą hello [Cezanne HR oprogramowanie klienta z pomocą techniczną](mailto:info@cezannehr.com).

4. W obszarze **SAML certyfikat podpisywania**, wybierz pozycję **certyfikatu (Base64)**, a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Witaj sekcji "Certyfikat podpisywania SAML"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. Wybierz pozycję **Zapisz**.

    ![przycisk "Zapisz" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. W obszarze **konfiguracji oprogramowania HR Cezanne**, wybierz pozycję **Konfigurowanie oprogramowania HR Cezanne** tooopen hello **Konfigurowanie logowania jednokrotnego** okna. Hello kopiowania **identyfikator jednostki SAML** i **SAML logowania jednokrotnego usługi pojedynczej** adresu URL z hello **krótkimi opisami** sekcji.

    ![Witaj w sekcji "Konfiguracja oprogramowania HR Cezanne"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. W oknie przeglądarki sieci web inną logowania tooyour Cezanne HR oprogramowania dzierżawy z uprawnieniami administratora.

8. Wybierz w okienku po lewej stronie powitania **konfiguracji systemu**. Wybierz **ustawienia zabezpieczeń** > **pojedynczy konfiguracji logowania jednokrotnego**.

    ![łącze "Pojedynczego logowania jednokrotnego konfiguracji" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. W hello **Zezwalaj toolog użytkowników za pomocą powitania po jednym logowania jednokrotnego (SSO) usług** okienku, wybierz hello **SAML 2.0** pole wyboru i wybierz hello **Advanced Configuration** Opcja.

    ![Opcje logowania jednokrotnego usług](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. Wybierz **Dodawanie nowych**.

    ![przycisk "Dodaj nowy" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. W obszarze **dostawców tożsamości SAML 2.0**, hello następujące:

    ![Witaj sekcji "Dostawców tożsamości SAML 2.0"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    a. W hello **Nazwa wyświetlana** wprowadź nazwę hello dostawcy tożsamości.

    b. W hello **identyfikator** Wklej hello **identyfikator jednostki SAML** skopiowany z hello portalu Azure. 

    c. W hello **powiązanie SAML** pola listy, wybierz opcję **POST**.

    d. W hello **punktu końcowego usługi tokenu zabezpieczającego** Wklej hello **SAML logowania jednokrotnego usługi pojedynczej** adresu URL skopiowanego z hello portalu Azure. 
    
    e. W hello **nazwa atrybutu ID użytkownika** wprowadź `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    f. tooupload hello pobrać certyfikatu z usługi Azure AD, wybierz hello **przekazać** przycisku.
    
    g. Kliknij przycisk **OK**. 

12. Wybierz pozycję **Zapisz**.

    ![przycisk "Zapisz" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> Po skonfigurowaniu aplikacji hello może odczytywać zwięzły wersji hello poprzedzających instrukcji w hello [portalu Azure](https://portal.azure.com). Po dodaniu aplikacji hello z hello **usługi Active Directory** > **aplikacje dla przedsiębiorstw** sekcji, wybierz hello **logowanie jednokrotne** kartę. Hello dostęp osadzone dokumentacji z hello **konfiguracji** sekcji. 

toolearn więcej informacji na temat hello osadzonych dokumentacji funkcji, zobacz [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
W tej sekcji utworzysz użytkownika testowego Simona Britta w hello portalu Azure.

![użytkownika testowego Hello Simona Britta][100]

toocreate użytkownika testowego w usłudze Azure AD, hello następujące:

1. W hello **portalu Azure**, w lewym okienku hello, wybierz hello **usługi Azure Active Directory** przycisku.

    ![przycisk "Azure Active Directory" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, wybierz opcję **użytkowników i grup** > **wszyscy użytkownicy**.
    
    ![Witaj link "Wszyscy użytkownicy"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    Witaj **wszyscy użytkownicy** zostanie otwarte okno dialogowe.

3. Witaj tooopen **użytkownika** okno dialogowe, wybierz opcję **Dodaj**.
 
    ![przycisk "Dodaj" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. W hello **użytkownika** okna dialogowego pozycję hello następujące:
 
    ![okno dialogowe "Użytkownika" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** wpisz użytkownika Britta Simona **adres e-mail**.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie wartość hello Uwaga, który został wygenerowany w hello **hasło** pole.

    d. Wybierz pozycję **Utwórz**.
 
### <a name="create-a-cezanne-hr-software-test-user"></a>Tworzenie użytkownika testowego Cezanne HR oprogramowania

tooenable usługi Azure AD użytkownicy toosign tooCezanne HR oprogramowania, muszą mieć przydzielone do Cezanne HR oprogramowania. W przypadku hello Cezanne HR oprogramowania Inicjowanie obsługi to zadanie ręczne.

Ustanowienie konta użytkownika, wykonując następujące hello:

1.  Zaloguj się tooyour Cezanne HR witrynę firmy jako administrator.

2.  Wybierz w okienku po lewej stronie powitania **konfiguracji systemu** > **Zarządzanie użytkownikami** > **Dodaj nowego użytkownika**.

    ![łącze "Dodaj nowego użytkownika" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "nowego użytkownika")

3.  W obszarze **dane osobowe**, hello następujące:

    ![sekcja "Dane osobowe" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "nowego użytkownika")
    
    a. Ustaw **wewnętrznego użytkownika** jako **OFF**.
    
    b. W hello **imię** okno, typ hello imię użytkownika, na przykład **Britta**.  
 
    c. W hello **nazwisko** okno, typ hello nazwisko użytkownika, na przykład **Simona**.
    
    d. W hello **E-mail** wpisz adres e-mail użytkownika hello, na przykład Brittasimon@contoso.com.

4.  W obszarze **informacje o koncie**, hello następujące:

    ![sekcja "Informacje o koncie" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "nowego użytkownika")
    
    a. W hello **Username** wpisz adres e-mail użytkownika hello, na przykład Brittasimon@contoso.com.
    
    b. W hello **hasło** wpisz hasło użytkownika hello.
    
    c. W hello **roli zabezpieczeń** wybierz opcję **HR Professional**.
    
    d. Kliknij przycisk **OK**.

5. Na powitania **logowanie jednokrotne** na karcie hello **SAML 2.0 identyfikatory** zaznacz **Dodaj nowy**.

    ![przycisk "Dodaj nowy" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "użytkownika")

6. W hello **dostawcy tożsamości** pola listy, wybierz dostawcy tożsamości. W hello **identyfikator użytkownika** wprowadź adres e-mail hello Simona testu użytkownika Britta konta.

    ![Witaj pola "Dostawcy tożsamości" i "Identyfikator użytkownika"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "użytkownika")
    
7. Wybierz pozycję **Zapisz**.

    ![przycisk "Zapisz" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "użytkownika")

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć użytkownika testowego toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCezanne HR oprogramowania.

![Dostęp użytkownika testowego][200] 

1. W portalu Azure hello Otwórz widok aplikacji hello, a następnie przejdź toohello widok katalogu. Wybierz **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.

    ![Witaj link "Wszystkie aplikacje"][201] 

2. Z listy aplikacji hello wybierz **Cezanne HR oprogramowania**.

    ![listę "Aplikacji" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. W menu hello powitania po lewej stronie wybierz **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Wybierz pozycję **Dodaj**. Następnie w hello **Dodaj przydziału** okno dialogowe, wybierz opcję **użytkowników i grup**.

    ![Łącze "Użytkownicy i grupy"][203]

5. W hello **użytkowników i grup** okno dialogowe, w hello **użytkowników** listy, wybierz **Simona Britta**.

6. W hello **użytkowników i grup** okno dialogowe, wybierz opcję **wybierz**.

7. W hello **Dodaj przydziału** okno dialogowe, wybierz opcję **przypisać**.
    
### <a name="test-sso"></a>Test rejestracji Jednokrotnej

W tej sekcji możesz przetestować konfigurację programu Azure AD z logowania jednokrotnego przy użyciu hello panelu dostępu.

Po wybraniu kafelka oprogramowania Cezanne HR hello w hello panelu dostępu logowania jest automatycznie tooyour Cezanne HR aplikacji.

## <a name="next-steps"></a>Następne kroki

* [Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowania jednokrotnego w usłudze Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

