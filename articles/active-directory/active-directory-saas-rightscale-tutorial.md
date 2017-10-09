---
title: 'Samouczek: Integracji Azure Active Directory z Rightscale | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Rightscale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a>Samouczek: Integracji Azure Active Directory z Rightscale

Z tego samouczka, dowiesz się, jak toointegrate Rightscale w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Rightscale zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooRightscale
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooRightscale (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Rightscale należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Rightscale logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Rightscale z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-rightscale-from-hello-gallery"></a>Dodawanie Rightscale z galerii hello
tooconfigure hello integracji Rightscale do usługi Azure AD, należy tooadd Rightscale z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Rightscale z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Rightscale**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. W panelu wyników hello zaznacz **Rightscale**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Rightscale w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Rightscale jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Rightscale musi toobe ustanowione.

W Rightscale, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Rightscale, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Rightscale](#creating-a-rightscale-test-user)**  -toohave odpowiednikiem Simona Britta w Rightscale, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Rightscale.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Rightscale, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Rightscale** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. Na powitania **domeny Rightscale i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb** nie masz tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. Na powitania **domeny Rightscale i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **SP zainicjował tryb**, wykonaj następujące kroki hello:
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    a. Polecenie hello **Pokaż zaawansowane ustawienia adresu URL**.

    b. W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello:`https://login.rightscale.com/`

5. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. Na powitania **konfiguracji Rightscale** kliknij **skonfigurować Rightscale** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS>
8. tooget logowania jednokrotnego skonfigurowane dla aplikacji, należy na toosign tooyour RightScale dzierżawy z uprawnieniami administratora.

    a. W menu hello na górze powitania kliknij hello **ustawienia** i wybierz **rejestracji jednokrotnej**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    b. Kliknij przycisk hello "**nowe**" tooadd przycisk **Your dostawców tożsamości SAML**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    c. W polu tekstowym hello z **Nazwa wyświetlana**, wprowadź nazwę swojej firmy.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    d. Wybierz **inicjowane Zezwalaj RightScale logowania jednokrotnego, używając wskazówki odnajdywania** i wejściowego z **nazwy domeny** w hello poniżej pola tekstowego.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    e. Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** , które zostały skopiowane z portalu Azure do **punktu końcowego logowania jednokrotnego SAML** w RightScale.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    f. Wklej wartość hello **identyfikator jednostki SAML** , które zostały skopiowane z portalu Azure do **SAML EntityID** w RightScale.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    g. Kliknij przycisk **przeglądarki** przycisk tooupload hello certyfikatu, który został pobrany z portalu Azure.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    h. Kliknij pozycję **Zapisz**.
<CE>
> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-rightscale-test-user"></a>Tworzenie użytkownika testowego Rightscale

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w RightScale. Praca z [zespołem pomocy technicznej klienta Rightscale](mailto:support@rightscale.com) tooadd hello użytkowników hello RightScale platformy.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooRightscale.

![Przypisz użytkownika][200] 

**tooassign tooRightscale Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Rightscale**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.  

Po kliknięciu kafelka RightScale hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour RightScale aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

