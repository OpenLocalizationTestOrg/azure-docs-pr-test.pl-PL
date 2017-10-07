---
title: "Samouczek: Integracji Azure Active Directory z usługi GitHub | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a>Samouczek: Integracji Azure Active Directory z usługi GitHub

Z tego samouczka, dowiesz się, jak toointegrate GitHub z usługą Azure Active Directory (Azure AD).

Integracja z usługą Azure AD GitHub udostępnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooGitHub
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooGitHub (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z usługi GitHub należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- GitHub jednokrotnego włączone subskrypcji


> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.


tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie GitHub z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne


## <a name="adding-github-from-hello-gallery"></a>Dodawanie GitHub z galerii hello
tooconfigure hello integracji GitHub z usługą Azure AD, należy tooadd GitHub z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd GitHub z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **witryną GitHub.com**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. W panelu wyników hello zaznacz **GitHub**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi GitHub w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w usłudze GitHub jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w serwisie GitHub musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w serwisie GitHub.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usługi GitHub, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego GitHub](#creating-a-GitHub-test-user)**  -toohave odpowiednikiem Simona Britta w usłudze GitHub, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji GitHub.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z usługi GitHub, wykonaj hello następujące kroki:**

1. W portalu zarządzania Azure hello na powitania **GitHub** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. Na powitania **GitHub domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    a. W hello **adres URL logowania** pole tekstowe, wartość hello typu jako:`https://github.com/orgs/<entity-id>/sso`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://github.com/orgs/<entity-id>`

    > [!NOTE] 
    > Należy pamiętać, że nie są one hello wartości rzeczywistych. Masz tooupdate tych wartości za pomocą hello rzeczywiste uwagi na adres URL i identyfikator. W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator. Przejdź tooretrieve sekcji administracyjnej tooGitHub tych wartości. 

4. Na powitania **atrybuty użytkownika** zaznacz **identyfikator użytkownika** jako user.mail.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. Na powitania **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. Na powitania **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza hello i wybierz **Data wygaśnięcia**. Następnie kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. Na powitania **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. W oknie podręcznym hello **certyfikat przerzucania** okna, kliknij przycisk **OK**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. Na powitania **konfiguracji GitHub** kliknij **skonfigurować GitHub** tooopen **Konfigurowanie logowania jednokrotnego** okna.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny GitHub organizacji jako administrator.

12. Przejdź za**ustawienia** i kliknij przycisk **zabezpieczeń**

    ![Ustawienia](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. Sprawdź hello **uwierzytelnianie Włącz SAML** pole ujawniania hello rejestracji jednokrotnej pola konfiguracji. Następnie należy użyć hello pojedynczego adresu URL wartość tooupdate hello pojedynczego logowania jednokrotnego adres URL logowania w konfiguracji usługi Azure AD.

    ![Ustawienia](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. Skonfiguruj hello następujące pola:

    a. **Zaloguj się na adres URL**: wprowadź **SAML rejestracji jednokrotnej adres URL usługi** z hello **skonfigurować GitHub** sekcję na temat usługi Azure AD

    b. **Wystawca**: wprowadź **identyfikator jednostki SAML** z hello **skonfigurować GitHub** sekcję na temat usługi Azure AD

    c. **Certyfikat publiczny**: Otwórz hello pobrać certyfikatu z usługi Azure AD w programie Notatnik i skopiuj zawartości hello tym "BEGIN certyfikatu" i "END CERTIFICATE"

    ![Ustawienia](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. Polecenie **konfiguracji testu SAML** tooconfirm że nie wystąpiły błędy sprawdzania poprawności lub błędy podczas rejestracji Jednokrotnej.

    ![Ustawienia](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. Kliknij przycisk **Zapisz**

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**. 


### <a name="creating-a-github-test-user"></a>Tworzenie użytkownika testowego GitHub

W kolejności tooenable usługi Azure AD użytkownicy toolog w witrynie GitHub muszą mieć przydzielone w witrynie GitHub.  
W przypadku hello GitHub Inicjowanie obsługi to zadanie ręczne.

**tooprovision kont użytkowników, wykonaj hello następujące kroki:**

1. Zaloguj się za tooyour GitHub witryny firmy jako administrator.

2. Kliknij przycisk **osób**.

    ![Osoby](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "osób")

3. Kliknij przycisk **Członkowskie zaproszenia**.

    ![Zaprosić użytkowników](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "zaprosić użytkowników")

4. Na powitania **Członkowskie zaproszenia** okna dialogowego wykonaj hello następujące kroki:

    a. W hello **E-mail** pole tekstowe, adres e-mail hello typu Simona Britta konta.

    ![Zaproś inne osoby](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Zaproś inne osoby")
    
    b. Kliknij przycisk **wysłać zaproszenie**.

    ![Zaproś inne osoby](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Zaproś inne osoby")

    > [!NOTE]
    > właścicielem konta usługi Azure Active Directory Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny.


### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooGitHub dostępu.

![Przypisz użytkownika][200] 

**tooassign tooGitHub Simona Britta wykonaj hello następujące kroki:**

1. W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **witryną GitHub.com**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    


### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka GitHub hello w hello Panel dostępu, należy pobrać zalogowane tooyour GitHub aplikacji. Można będzie można logować się jako konta organizacji, ale następnie toolog muszą się przy użyciu konta osobistego.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
