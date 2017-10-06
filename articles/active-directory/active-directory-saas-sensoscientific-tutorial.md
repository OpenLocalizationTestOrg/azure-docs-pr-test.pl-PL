---
title: 'Samouczek: Integracji Azure Active Directory z SensoScientific bezprzewodowej temperatury monitorowania systemu | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między SensoScientific bezprzewodowej temperatury monitorowania systemu i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a>Samouczek: Integracji Azure Active Directory z SensoScientific bezprzewodowej temperatury monitorowania systemu

Z tego samouczka, dowiesz się, jak toointegrate SensoScientific bezprzewodowej temperatury monitorowania systemu z usługą Azure Active Directory (Azure AD).

Integracja z usługą Azure AD SensoScientific bezprzewodowej temperatury monitorowania systemu zawiera hello następujące korzyści:

- Można kontrolować w usłudze Azure AD mającego tooSensoScientific dostępu bezprzewodowego temperatury monitorowania systemu
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSensoScientific bezprzewodowej temperatury monitorowania systemu (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z SensoScientific bezprzewodowej temperatury monitorowania systemu, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- SensoScientific bezprzewodowej temperatury monitorowania systemu jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie SensoScientific bezprzewodowej temperatury monitorowania systemu z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a>Dodawanie SensoScientific bezprzewodowej temperatury monitorowania systemu z galerii hello
tooconfigure hello integracji SensoScientific bezprzewodowej temperatury monitorowania systemu do usługi Azure AD, należy tooadd SensoScientific bezprzewodowej temperatury monitorowania systemu z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd SensoScientific bezprzewodowej temperatury monitorowania systemu z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **SensoScientific bezprzewodowej temperatury monitorowania systemu**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. W panelu wyników hello, wybierz **SensoScientific bezprzewodowej temperatury monitorowania systemu**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej SensoScientific bezprzewodowej temperatury monitorowania systemu, na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello SensoScientific bezprzewodowej temperatury monitorowania systemu jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi SensoScientific bezprzewodowej temperatury monitorowania systemu musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** SensoScientific bezprzewodowej temperatury monitorowania systemu.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SensoScientific bezprzewodowej temperatury monitorowania systemu, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego SensoScientific bezprzewodowej temperatury monitorowania systemu](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave odpowiednikiem Simona Britta w SensoScientific bezprzewodowej temperatury monitorowania systemu, który jest połączony reprezentacja toohello usługi Azure AD użytkownik.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji SensoScientific bezprzewodowej temperatury monitorowania systemu.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z SensoScientific bezprzewodowej temperatury monitorowania systemu, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **SensoScientific bezprzewodowej temperatury monitorowania systemu** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. Na powitania **adresy URL i monitorowania domeny systemu SensoScientific bezprzewodowej temperatury** sekcji nie tooperform potrzeba żadnych czynności jako aplikacji hello już jest wstępna Integracja z usługą Azure:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. Na powitania **monitorowania konfiguracji systemu SensoScientific bezprzewodowej temperatury** kliknij **Konfiguruj SensoScientific bezprzewodowej temperatury monitorowania System** tooopen  **Konfigurowanie logowania jednokrotnego** okna. Witaj kopii **Sign-Out adres URL, identyfikator jednostki SAML** i **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. Zaloguj się na tooyour SensoScientific bezprzewodowej temperatury monitorowania systemu aplikacji jako administrator.

8. W menu nawigacji hello na górze powitania kliknij **konfiguracji** i przejdź do **Konfiguruj** w obszarze **rejestracji jednokrotnej** tooopen hello pojedynczy znak na ustawienia.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. W **pojedynczy znak na ustawienia** formularza wykonać hello następujące kroki:
 
    a. Wybierz **Nazwa wystawcy** jako usługi Azure AD.
    
    b. Wklej hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure w tekstowym adres URL wystawcy.
    
    c. Wklej hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure w pole tekstowe pojedynczy znak na adres URL usługi.

    d. Wklej hello **Sign-Out URL** którego została skopiowana z portalu Azure do pojedynczego adresu URL usługi Sign-Out pola tekstowego.

    e. Przeglądaj hello certyfikatu, który został pobrany z portalu Azure i przekaż go tutaj.
    
    f. Kliknij pozycję **Zapisz**.
  
> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a>Tworzenie użytkownika testowego SensoScientific bezprzewodowej temperatury monitorowania systemu

toolog użytkowników tooenable usługi Azure AD w tooSensoScientific bezprzewodowej temperatury monitorowania systemu, muszą mieć przydzielone do SensoScientific bezprzewodowej temperatury monitorowania systemu. Praca z [zespołem pomocy technicznej SensoScientific bezprzewodowej temperatury monitorowania systemu](https://www.sensoscientific.com/contact-us/) Aby dodać użytkowników hello hello platforma SensoScientific bezprzewodowej temperatury monitorowania systemu. Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej. 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie tooSensoScientific dostępu bezprzewodowego temperatury monitorowania systemu.

![Przypisz użytkownika][200] 

**tooassign tooSensoScientific Simona Britta bezprzewodowej temperatury monitorowania systemu, należy wykonać hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **SensoScientific bezprzewodowej temperatury monitorowania systemu**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu. Kliknij Kafelek SensoScientific bezprzewodowej temperatury monitorowania systemu hello w hello Panel dostępu, można automatycznie zalogowane tooyour SensoScientific bezprzewodowej temperatury systemu monitorowania aplikacji. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

