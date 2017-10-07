---
title: 'Samouczek: Integracji Azure Active Directory z Velpic SAML | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Velpic SAML."
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
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a>Samouczek: Integracji Azure Active Directory z Velpic SAML

Z tego samouczka, dowiesz się, jak toointegrate SAML Velpic w usłudze Azure Active Directory (Azure AD).

Integrację Velpic SAML z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooVelpic SAML
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooVelpic SAML (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z Velpic SAML należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Velpic SAML jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Velpic SAML z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-velpic-saml-from-hello-gallery"></a>Dodawanie Velpic SAML z galerii hello
tooconfigure hello integrację Velpic SAML usługi Azure AD, należy tooadd Velpic SAML z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd SAML Velpic z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Velpic SAML**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. W panelu wyników hello, wybierz **Velpic SAML**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Velpic SAML w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Velpic SAML jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Velpic SAML musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Velpic SAML.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Velpic SAML, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave odpowiednikiem Simona Britta w SAML Velpic, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji Velpic SAML.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Velpic SAML wykonaj hello następujące kroki:**

1. W portalu zarządzania Azure hello na powitania **Velpic SAML** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. Wprowadź szczegóły hello w hello **Velpic SAML domeny i adres URL** sekcji -

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    a. W hello **adres URL logowania** pole tekstowe, wartość hello typu jako:`https://<sub-domain>.velpicsaml.net`

    b. W hello **identyfikator** pole tekstowe, Wklej hello **"Rejestracja jednokrotna w adresie URL"** wartość`https://auth.velpic.com/saml/v2/<entity-id>/login`
    
    > [!NOTE]
    > Należy pamiętać, że hello znaku w adresie URL, które będą udostępniane przez hello Velpic SAML zespołu i wartość identyfikatora będzie dostępna po skonfigurowaniu hello wtyczki logowania jednokrotnego Velpic SAML strony. Należy toocopy, który ze strony aplikacji Velpic SAML i wklej ją tutaj.

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. W sekcji konfiguracji SAML Velpic hello kliknij polecenie skonfigurować SAML Velpic tooopen Konfigurowanie logowania jednokrotnego okna. Skopiuj hello identyfikator jednostki SAML z hello sekcji krótkimi opisami.

7. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Velpic SAML jako administrator.

8. Polecenie **Zarządzaj** karcie i przejść za**integracji** sekcji, w którym należy tooclick na **wtyczek** przycisk toocreate nowej wtyczki dla logowania.

    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. Polecenie hello **"Dodawanie wtyczki"** przycisku.
    
    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. Polecenie hello **SAML** kafelka w hello strona Dodawanie wtyczek.
    
    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. Wprowadź nazwę nowej wtyczki SAML hello hello, a następnie kliknij przycisk hello **"Dodaj"** przycisku.

    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. Wprowadź szczegóły hello w następujący sposób:

    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    a. W hello **nazwa** pole tekstowe, nazwa typu hello wtyczki SAML.

    b. W hello **adres URL wystawcy** pole tekstowe, Wklej hello **identyfikator jednostki SAML** skopiowany z hello **Konfigurowanie logowania jednokrotnego** okna hello portalu Azure.

    c. W hello **dostawcy metadanych konfiguracji** przekazać hello pliku XML metadanych, który został pobrany z portalu Azure.

    d. Możesz również tooenable SAML tylko w czasie inicjowania obsługi administracyjnej, należy włączyć hello **"Automatyczne tworzenie nowych użytkowników"** pola wyboru. Jeśli użytkownik nie istnieje w Velpic i ta flaga nie jest włączona, hello logowania z platformy Azure nie powiedzie się. Jeśli flaga hello jest automatycznie włączone hello użytkownika zostanie zainicjowana w Velpic w czasie hello nazwy logowania. 

    e. Kopiuj hello **Rejestracja jednokrotna w adresie URL** z pola tekstowego hello i wklej go w hello portalu Azure.
    
    f. Kliknij pozycję **Zapisz**.

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-velpic-saml-test-user"></a>Tworzenie użytkownika testowego Velpic SAML

Ten krok zazwyczaj nie jest wymagane jako aplikacji hello obsługuje tylko w czasie Inicjowanie obsługi użytkowników. Jeśli nie włączono hello użytkownika automatycznego inicjowania obsługi administracyjnej tworzenie ręczne użytkownika można wykonać zgodnie z poniższym opisem.

Zaloguj się do witryny firmy Velpic SAML jako administrator i wykonać następujące kroki:
    
1. Kliknij na karcie Zarządzanie przejdź do sekcji tooUsers, a następnie kliknij nowy przycisk tooadd użytkowników.

    ![Dodaj użytkownika](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. Na powitania **"Tworzenie nowego użytkownika"** okna dialogowego wykonaj następujące kroki hello.

    ![Użytkownika](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    a. W hello **imię** pole tekstowe, typ hello imię Simona Britta.

    b. W hello **nazwisko** pole tekstowe, typ hello nazwisko Simona Britta.

    c. W hello **nazwy użytkownika** pole tekstowe, nazwę użytkownika hello typu Simona Britta.

    d. W hello **E-mail** pole tekstowe, adres e-mail hello typu Simona Britta konta.

    e. Pozostałe informacje hello jest opcjonalny, możesz wpisać ją w razie potrzeby.
    
    f. Kliknij przycisk **SAVE** (Zapisz).  

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooVelpic dostępu SAML.

![Przypisz użytkownika][200] 

**tooassign tooVelpic Simona Britta SAML, wykonaj następujące kroki hello:**

1. W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Velpic SAML**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

1. Po kliknięciu hello Velpic SAML kafelka w hello Panel dostępu, należy pobrać strony logowania Velpic SAML aplikacji. Powinny pojawić się hello **"Zaloguj się za pomocą usługi Azure AD"** przycisk na powitania stronę logowania.

    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. Polecenie hello **"Zaloguj się za pomocą usługi Azure AD"** toolog przycisk w tooVelpic przy użyciu konta usługi Azure AD.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

