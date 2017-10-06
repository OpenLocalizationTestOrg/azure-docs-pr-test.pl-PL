---
title: "Samouczek: Integracji Azure Active Directory przy użyciu konta Adobe | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Adobe logowania."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a>Samouczek: Integracji Azure Active Directory przy użyciu konta Adobe

Z tego samouczka, dowiesz się, jak toointegrate Adobe zarejestrować w usłudze Azure Active Directory (Azure AD).

Integracji Podpisz Adobe z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooAdobe logowania
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAdobe logowania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD przy użyciu konta Adobe należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Adobe logowania jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Adobe logowania z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-adobe-sign-from-hello-gallery"></a>Dodawanie Adobe logowania z galerii hello
tooconfigure hello integracji Podpisz Adobe do usługi Azure AD, należy tooadd Adobe logowania z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Adobe logowania z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **znak Adobe**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. W panelu wyników hello, wybierz **znak Adobe**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej znakiem Adobe oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello Adobe rejestracja jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi rejestracja Adobe musi toobe ustanowione.

W Adobe logowania, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i test usługi Azure AD logowania jednokrotnego przy użyciu konta Adobe należy hello toocomplete po bloków konstrukcyjnych:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego znak Adobe](#creating-an-adobe-sign-test-user)**  -toohave odpowiednikiem Simona Britta w Adobe znaku, który jest odpowiednikiem połączonych toohello usługi Azure AD użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji Adobe logowania.

**tooconfigure usługi Azure AD logowania jednokrotnego przy użyciu konta Adobe wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **znak Adobe** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. Na powitania **Adobe logowania domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.echosign.com/`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.echosign.com`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta logowania Adobe](https://helpx.adobe.com/in/contact/support.html) tooget tych wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji logowania Adobe** kliknij **Konfigurowanie rejestrowania programu Adobe** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Adobe znak tooyour jako administrator.

8. Hello menu u góry hello, kliknij przycisk **konta**, a następnie w okienku nawigacji powitania po lewej stronie powitania kliknij **ustawienia SAML** w obszarze **ustawienia konta**.
   
   ![Konto](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "konta")

9. W sekcji Ustawienia SAML hello wykonaj następujące kroki hello:
   
   ![Ustawienia SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "ustawienia SAML")
   
   a. Jako **tryb SAML**, wybierz pozycję **SAML obowiązkowe**.
   
   b. Wybierz **toolog Zezwalaj EchoSign Administratorzy konta przy użyciu swoich poświadczeń EchoSign**.
   
   c. Jako **Tworzenie użytkownika**, wybierz pozycję **automatyczne dodawanie użytkowników uwierzytelnionych za pośrednictwem SAML**.

10. Przenieś, wykonywanie hello następujące kroki:

       ![Ustawienia SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "ustawienia SAML")

    a. Wklej **SAML identyfikator jednostki**, która została skopiowana z portalu Azure do hello **identyfikator jednostki IdP** pole tekstowe.
    
    b. Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z portalu Azure do hello **adres URL logowania IdP** pole tekstowe.
   
    c. Wklej **Sign-Out adres URL**, która została skopiowana z portalu Azure do hello **adresu URL wylogowania IdP** pola tekstowego.

    d. Otwórz z pobranego **Certificate(Base64)** pliku w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu IdP** pole tekstowe

    e. Kliknij przycisk **zapisać zmiany**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-adobe-sign-test-user"></a>Tworzenie użytkownika testowego Adobe logowania

toolog użytkowników tooenable usługi Azure AD w tooAdobe logowania, muszą mieć przydzielone do programu Adobe logowania. W przypadku hello Adobe logowania Inicjowanie obsługi to zadanie ręczne.

>[!NOTE]
>Możesz użyć innych Adobe logowania użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Adobe logowania konta użytkownika usługi AAD. 

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour **znak Adobe** witryny firmy jako administrator.

2. Hello menu u góry hello, kliknij przycisk **konta**, a następnie w okienku nawigacji powitania po lewej stronie powitania kliknij **użytkownicy i grupy**, a następnie kliknij przycisk **utworzenie nowego użytkownika**.
   
   ![Konto](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "konta")
   
3. W hello **Tworzenie nowego użytkownika** sekcji, wykonaj następujące kroki hello:
   
   ![Utwórz użytkownika](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Tworzenie użytkownika")
   
   a. Typ hello **adres E-mail**, **imię**, i **nazwisko** z prawidłowego konta usługi AAD mają tooprovision w hello związane z pól tekstowych.
   
   b. Kliknij przycisk **Utwórz użytkownika**.

>[!NOTE]
>Właściciel konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail zawierającą łącze tooconfirm hello konta, zanim staje się aktywny. 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAdobe logowania.

![Przypisz użytkownika][200] 

**tooassign tooAdobe Simona Britta logowania, należy wykonać hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **znak Adobe**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Po kliknięciu powitalne znak Adobe kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Adobe logowania aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

