---
title: 'Samouczek: Integracji Azure Active Directory z Pingboard | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a>Samouczek: Integracji Azure Active Directory z Pingboard

Z tego samouczka, dowiesz się, jak toointegrate Pingboard w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Pingboard zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPingboard
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPingboard (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Pingboard należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Pingboard jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Pingboard z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-pingboard-from-hello-gallery"></a>Dodawanie Pingboard z galerii hello
tooconfigure hello integracji Pingboard do usługi Azure AD, należy tooadd Pingboard z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Pingboard z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Pingboard**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. W panelu wyników hello zaznacz **Pingboard**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pingboard w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Pingboard jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Pingboard musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Pingboard.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Pingboard, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Pingboard](#creating-a-pingboard-test-user)**  -toohave odpowiednikiem Simona Britta w Pingboard, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji Pingboard.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Pingboard, wykonaj następujące kroki hello:**

1. W portalu zarządzania Azure hello na powitania **Pingboard** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. Na powitania **Pingboard domeny i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    a. W hello **identyfikator** pole tekstowe, wartość hello typu jako:`http://<entity-id>.pingboard.com/sp`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<entity-id>.pingboard.com/auth/saml/consume`

    > [!NOTE] 
    > Należy pamiętać, że nie są one hello wartości rzeczywistych. Masz tooupdate tych wartości za pomocą hello rzeczywisty identyfikator i odpowiedzi adresu URL. W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta Pingboard](https://support.pingboard.com/) tooget tych wartości. 

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    a. W hello **adres URL logowania** pole tekstowe, wartość hello typu jako:`http://<sub-domain>.pingboard.com/sign_in`
     
5. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. tooconfigure logowania jednokrotnego po stronie Pingboard, Otwórz nowe okno przeglądarki i zaloguj tooyour Pingboard konta. Tooset admin Pingboard się funkcji logowania jednokrotnego musi być na.

8. Wybierz z górnego menu hello **aplikacji > integracji**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  Na powitania **integracji** pozycję Znajdź hello **"Azure Active Directory"** Kafelek, a następnie kliknij go.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. W hello modalne, kliknij poniżej **"Konfiguruj"**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. Na powitania po stronie można zauważyć, że "Integracja z usługą Azure rejestracji Jednokrotnej jest włączona.". Otwórz hello pobrany plik XML metadanych w hello Notatnik i Wklej zawartość **metadanych IDP**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. Plik Hello zostanie zweryfikowany, a jeśli wszystko jest poprawny, logowania jednokrotnego zostanie ono włączone

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-pingboard-test-user"></a>Tworzenie użytkownika testowego Pingboard

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Pingboard muszą mieć przydzielone do Pingboard.  
W przypadku hello Pingboard Inicjowanie obsługi to zadanie ręczne.

**tooprovision kont użytkowników, wykonaj hello następujące kroki:**

1. Zaloguj się za tooyour Pingboard witryny firmy jako administrator.

2. Kliknij przycisk **"Dodaj pracownika"** znajdującego się na **katalogu** strony.

    ![Dodawanie pracownika](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. Na powitania **"Dodaj pracownika"** okna dialogowego wykonaj następujące kroki hello.

    ![Zaproś inne osoby](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    a. W hello **imię i nazwisko** pole tekstowe, hello Pełna nazwa typu Simona Britta.

    b. W hello **E-mail** pole tekstowe, adres e-mail hello typu Simona Britta konta.

    c. W hello **stanowisko** pole tekstowe, typ hello stanowisko Simona Britta.

    d. W hello **lokalizacji** listy rozwijanej wybierz hello lokalizację Simona Britta.
    
    e. Kliknij pozycję **Dodaj**.   

4. Ekran potwierdzenia, zostanie wyświetlone tooconfirm hello dodawania użytkownika.
    
    ![Upewnij się](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > właścicielem konta usługi Azure Active Directory Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooPingboard dostępu.

![Przypisz użytkownika][200] 

**tooassign tooPingboard Simona Britta wykonaj hello następujące kroki:**

1. W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Pingboard**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Pingboard hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Pingboard aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
