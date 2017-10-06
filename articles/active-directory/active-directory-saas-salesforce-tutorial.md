---
title: "Samouczek: Integracji Azure Active Directory z usług Salesforce | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a>Samouczek: Integracji Azure Active Directory z usług Salesforce

Z tego samouczka, dowiesz się, jak toointegrate Salesforce z usługą Azure Active Directory (Azure AD).

Integrowanie usługi Salesforce z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSalesforce
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSalesforce (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z usług Salesforce, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Salesforce jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie usługi Salesforce z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-salesforce-from-hello-gallery"></a>Dodawanie usługi Salesforce z galerii hello
tooconfigure hello integracji usługi Salesforce z usługą Azure AD, należy tooadd Salesforce z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Salesforce z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Salesforce**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. W panelu wyników hello, wybierz **Salesforce**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Salesforce na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w usłudze Salesforce jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w usłudze Salesforce musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w usłudze Salesforce.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usług Salesforce, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Salesforce](#creating-a-salesforce-test-user)**  -toohave odpowiednikiem Simona Britta w usłudze Salesforce, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Salesforce.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z usług Salesforce, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Salesforce** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. Na powitania **domeny Salesforce i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    W hello **adres URL logowania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca: 
   * Konto przedsiębiorstwa:`https://<subdomain>.my.salesforce.com`
   * Konta dewelopera:`https://<subdomain>-dev-ed.my.salesforce.com`

    > [!NOTE] 
    > Wartości te nie są hello prawdziwe. Z hello rzeczywisty adres URL logowania, należy zaktualizować te wartości. Skontaktuj się z [zespołem pomocy technicznej klienta usług Salesforce](https://help.salesforce.com/support) tooget tych wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Salesforce** , kliknij przycisk **skonfigurować Salesforce** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.** 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS>
7.  Otwórz nową kartę w przeglądarce i zaloguj tooyour konto administratora usług Salesforce.

8.  W obszarze hello **administratora** okienka nawigacji kliknij **kontroli bezpieczeństwa** tooexpand hello związane z sekcji. Następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  Na powitania **ustawień rejestracji jednokrotnej** kliknij przycisk hello **Edytuj** przycisku.
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)

      > [!NOTE]
      > Jeśli użytkownik tooenable rejestracji jednokrotnej ustawienia konta usług Salesforce, może być konieczne toocontact [zespołem pomocy technicznej klienta usług Salesforce](https://help.salesforce.com/support). 

10. Wybierz **włączone SAML**, a następnie kliknij przycisk **zapisać**.

      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. tooconfigure SAML pojedynczego logowania jednokrotnego ustawienia, kliknij przycisk **nowy**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. Na powitania **SAML pojedynczego logowania jednokrotnego ustawienie Edytuj** upewnij hello następujące konfiguracje:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    a. Dla hello **nazwa** wpisz przyjazną nazwę dla tej konfiguracji. Wartość dla **nazwa** automatycznie wypełnić hello **Nazwa interfejsu API** pola tekstowego.

    b. Wklej **identyfikator jednostki SMAL** wartości do hello **wystawcy** w Salesforce.

    c. W hello **textbox identyfikator jednostki**, wpisz nazwę domeny witryny Salesforce przy użyciu hello następującego wzorca:
      
      * Konto przedsiębiorstwa:`https://<subdomain>.my.salesforce.com`
      * Konta dewelopera:`https://<subdomain>-dev-ed.my.salesforce.com`
      
    d. Kliknij przycisk **Przeglądaj** lub **wybierz plik** tooopen hello **tooUpload wybierz plik** okno dialogowe, wybierz certyfikat usług Salesforce, a następnie kliknij przycisk **Otwórz**tooupload hello certyfikatu.

    e. Dla **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera użytkownika witryny salesforce.com**.

    f. Dla **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentifier hello hello instrukcji podmiotu**

    g. Wklej **pojedynczy znak na adres URL usługi** do hello **adresu URL logowania do dostawcy tożsamości** w Salesforce.
    
    h. Dla **dostawcy zainicjował żądanie powiązania usługi**, wybierz pozycję **przekierowywanie HTTP**.
    
    i. Na koniec kliknij **zapisać** tooapply SAML pojedynczego logowania jednokrotnego ustawień.

13. W okienku nawigacji po lewej stronie powitania w usłudze Salesforce kliknij **Zarządzanie domenami** tooexpand hello powiązanych sekcji, a następnie kliknij przycisk **Moje domeny**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. Przewiń w dół toohello **konfiguracji uwierzytelniania** sekcji, a następnie kliknij polecenie hello **Edytuj** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. W hello **usługi uwierzytelniania** sekcji wybierz hello przyjazną nazwę konfiguracji logowania jednokrotnego SAML, a następnie kliknij przycisk **zapisać**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > Jeśli zostanie wybrana więcej niż jedna usługa uwierzytelniania, użytkownicy są zostanie wyświetlony monit o tooselect usługi uwierzytelniania, która ich, takich jak toosign się podczas inicjowania środowiska usług Salesforce tooyour rejestracji jednokrotnej. Jeśli nie chcesz toohappen, a następnie wykonaj następujące czynności **pozostawienie jej niezaznaczonej innych usług uwierzytelniania**.
<CE>    
> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W okienku nawigacji po lewej stronie powitania w hello **portalu Azure**, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-salesforce-test-user"></a>Tworzenie użytkownika testowego usług Salesforce

W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w Salesforce. SalesForce obsługę w czasie, który jest domyślnie włączona.
Nie ma elementu akcji można w tej sekcji. Jeśli użytkownik nie istnieje w usłudze Salesforce, nowy jest tworzony podczas próby tooaccess Salesforce.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSalesforce.

![Przypisz użytkownika][200] 

**tooassign tooSalesforce Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Salesforce**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

tootest pojedynczego logowania jednokrotnego ustawienia, otwórz hello panelu dostępu pod adresem [https://myapps.microsoft.com](https://myapps.microsoft.com/), następnie zaloguj się do konta testowego hello i kliknij przycisk **Salesforce**.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Skonfiguruj Inicjowanie obsługi użytkowników](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

