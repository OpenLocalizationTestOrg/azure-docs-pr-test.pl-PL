---
title: 'Samouczek: Integracji Azure Active Directory z Netsuite | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a>Samouczek: Integracji Azure Active Directory z Netsuite

Z tego samouczka, dowiesz się, jak toointegrate Netsuite w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Netsuite zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooNetsuite
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooNetsuite (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Netsuite należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Netsuite jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Netsuite z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-netsuite-from-hello-gallery"></a>Dodawanie Netsuite z galerii hello
tooconfigure hello integracji Netsuite do usługi Azure AD, należy tooadd Netsuite z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Netsuite z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Netsuite**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. W panelu wyników hello zaznacz **Netsuite**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Netsuite na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Netsuite jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Netsuite musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Netsuite.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Netsuite, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Netsuite](#creating-a-netsuite-test-user)**  -toohave odpowiednikiem Simona Britta w Netsuite, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Netsuite.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Netsuite, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Netsuite** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. Na powitania **Netsuite domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Wartość hello aktualizacji z hello rzeczywisty adres URL odpowiedzi. Skontaktuj się z [zespołem pomocy technicznej Netsuite](http://www.netsuite.com/portal/services/support.shtml) tooget tej wartości.
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Netsuite** kliknij **skonfigurować Netsuite** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. Otwórz nową kartę w przeglądarce i zaloguj się do witryny firmy Netsuite jako administrator.

8. Hello pasku narzędzi u góry hello hello strony, kliknij przycisk **Instalator**, następnie kliknij przycisk **Menedżer instalacji**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. Z hello **zadań konfiguracyjnych** listy, wybierz **integracji**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. W hello **Zarządzanie uwierzytelniania** kliknij **SAML logowania jednokrotnego**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. Na powitania **Instalatora SAML** wykonaj hello następujące kroki:
   
    a. Kopia hello **SAML pojedynczy znak na adres URL usługi** wartość z **krótkimi opisami** sekcji **Konfigurowanie logowania jednokrotnego** i wklej go do hello **dostawcy tożsamości Strona logowania** w Netsuite.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    b. Netsuite, wybierz **podstawowej metody uwierzytelniania**.

    c. Dla pola hello etykietą **metadanych dostawcy tożsamości SAMLV2**, wybierz pozycję **Przekaż plik metadanych IDP**. Następnie kliknij przycisk **Przeglądaj** tooupload hello metadanych pliku, który został pobrany z portalu Azure.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    d. Kliknij przycisk **przesłać**.

12. W usłudze Azure AD, kliknij **widoku i edytować wszystkie atrybuty użytkowników** pole wyboru i dodać atrybut.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. Dla hello **nazwa atrybutu** wpisz w `account`. Dla hello **wartość atrybutu** wpisz w identyfikatora konta Netsuite Ta wartość jest stała i zmianę konta. Instrukcje dotyczące toofind identyfikator konta znajdują się poniżej:

      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    a. W Netsuite, kliknij przycisk **Instalator** menu górnym menu nawigacyjnym hello.

    b. Kliknięcie w obszarze hello **zadań konfiguracyjnych** sekcji hello menu nawigacji po lewej stronie, wybierz opcję hello **integracji** sekcji, a następnie kliknij polecenie **preferencje usług sieci Web**.

    c. Identyfikator konta Netsuite skopiuj i wklej go do hello **wartość atrybutu** pole w usłudze Azure AD.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. Zanim użytkownicy mogą wykonywać logowania jednokrotnego do Netsuite, ich należy przypisać odpowiednie uprawnienia hello w Netsuite. Wykonaj instrukcje hello poniżej tooassign te uprawnienia.

    a. W menu górnym menu nawigacyjnym powitania kliknij **Instalator**, następnie kliknij przycisk **Menedżer instalacji**.
      
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    b. W menu nawigacji po lewej stronie powitania wybierz **użytkownicy i role**, następnie kliknij przycisk **Zarządzanie rolami**.
      
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    c. Kliknij przycisk **nową rolę**.

    d. Wpisz w **nazwa** nową rolę i wybierz hello **pojedynczego logowania tylko** wyboru.
      
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    e. Kliknij pozycję **Zapisz**.

    f. W menu hello na górze hello, kliknij przycisk **uprawnienia**. Następnie kliknij przycisk **Instalatora**.
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    g. Wybierz **ustawić się SAM rejestracji jednokrotnej**, a następnie kliknij przycisk **Dodaj**.

    h. Kliknij pozycję **Zapisz**.

    i. W menu górnym menu nawigacyjnym powitania kliknij **Instalator**, następnie kliknij przycisk **Menedżer instalacji**.
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    j. W menu nawigacji po lewej stronie powitania wybierz **użytkownicy i role**, następnie kliknij przycisk **Zarządzanie użytkownikami**.
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    k. Wybierz użytkownika testowego. Następnie kliknij przycisk **Edytuj**.
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    l. W oknie dialogowym ról hello, wybierz rolę hello, które zostały utworzone i kliknij przycisk **Dodaj**.
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    m. Kliknij pozycję **Zapisz**.
    
> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**. 

### <a name="creating-a-netsuite-test-user"></a>Tworzenie użytkownika testowego Netsuite

W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w Netsuite. Netsuite obsługę w czasie, który jest domyślnie włączona.
Nie ma elementu akcji można w tej sekcji. Jeśli użytkownik nie istnieje w Netsuite, tworzona jest nowy, podczas próby tooaccess Netsuite.


### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooNetsuite.

![Przypisz użytkownika][200] 

**tooassign tooNetsuite Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Netsuite**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

tootest pojedynczego logowania jednokrotnego ustawienia, otwórz hello panelu dostępu pod adresem [https://myapps.microsoft.com](https://myapps.microsoft.com/), zaloguj się do konta testowego hello i kliknij przycisk **Netsuite**.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Skonfiguruj Inicjowanie obsługi użytkowników](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

