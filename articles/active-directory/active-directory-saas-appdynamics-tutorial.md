---
title: 'Samouczek: Integracji Azure Active Directory z AppDynamics | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i AppDynamics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9b63afec73d7442e6ac1ce34b511beea6f43ffe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a>Samouczek: Integracji Azure Active Directory z AppDynamics

Z tego samouczka, dowiesz się, jak toointegrate AppDynamics w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD AppDynamics zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAppDynamics
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAppDynamics (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z AppDynamics należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- AppDynamics logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie AppDynamics z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-appdynamics-from-hello-gallery"></a>Dodawanie AppDynamics z galerii hello
tooconfigure hello integracji AppDynamics do usługi Azure AD, należy tooadd AppDynamics z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd AppDynamics z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **AppDynamics**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. W panelu wyników hello zaznacz **AppDynamics**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AppDynamics na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w AppDynamics jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w AppDynamics musi toobe ustanowione.

W AppDynamics, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z AppDynamics, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego AppDynamics](#creating-an-appdynamics-test-user)**  -toohave odpowiednikiem Simona Britta w AppDynamics, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji AppDynamics.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z AppDynamics, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **AppDynamics** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. Na powitania **AppDynamics domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.saas.appdynamics.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.saas.appdynamics.com/controller`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta AppDynamics](https://www.appdynamics.com/support/) tooget tych wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji AppDynamics** kliknij **skonfigurować AppDynamics** tooopen **Konfigurowanie logowania jednokrotnego** okna. Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy AppDynamics tooyour jako administrator.

8. Witaj pasku narzędzi u góry hello, kliknij przycisk **ustawienia**, a następnie kliknij przycisk **administracji**.
   
    ![Administracja](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "administracji")

9. Kliknij przycisk hello **dostawcy uwierzytelniania** kartę.
   
    ![Dostawca uwierzytelniania](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "dostawcy uwierzytelniania")

10. W hello **dostawcy uwierzytelniania** sekcji, wykonaj następujące kroki hello:
   
    ![Konfiguracja SAML](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "Konfiguracja SAML")   

    a. Jako **dostawcy uwierzytelniania**, wybierz pozycję **SAML**.

    b. W hello **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.

    c. W hello **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.
       
    d. Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu** pole tekstowe

    e. Kliknij pozycję **Zapisz**.

     ![Zapisz](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Zapisz")

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-appdynamics-test-user"></a>Tworzenie użytkownika testowego AppDynamics

toolog użytkowników tooenable usługi Azure AD w tooAppDynamics, muszą mieć przydzielone do AppDynamics. W przypadku hello AppDynamics Inicjowanie obsługi to zadanie ręczne.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. Zaloguj się za tooyour AppDynamics witryny firmy jako administrator.

2. Przejdź za**użytkowników**, a następnie kliknij przycisk  **+**  tooopen hello **Tworzenie użytkownika** okna dialogowego.
   
    ![Użytkownicy](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "użytkowników")

3. W hello **Tworzenie użytkownika** sekcji, wykonaj następujące kroki hello:
   
    ![Utwórz użytkownika](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Tworzenie użytkownika")
   
    a. Typ hello **Username**, **nazwa**, **poczty E-mail**, **nowe hasło**, **powtórz nowe hasło** z prawidłową usługi AAD konto ma tooprovision do hello związane z pól tekstowych.

    b. Kliknij pozycję **Zapisz**.

    >[!NOTE]
    >Możesz użyć innych AppDynamics użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez AppDynamics tooprovision kont użytkowników usługi Azure AD.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAppDynamics.

![Przypisz użytkownika][200] 

**tooassign tooAppDynamics Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **AppDynamics**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.

Po kliknięciu powitalne AppDynamics kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour AppDynamics aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

