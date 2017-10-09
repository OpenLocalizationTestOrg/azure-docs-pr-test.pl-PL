---
title: 'Samouczek: Integracji Azure Active Directory z Hightail | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Hightail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a>Samouczek: Integracji Azure Active Directory z Hightail

Z tego samouczka, dowiesz się, jak toointegrate Hightail z usługą Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Hightail zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooHightail
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooHightail (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Hightail należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Hightail logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Hightail z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-hightail-from-hello-gallery"></a>Dodawanie Hightail z galerii hello
tooconfigure hello integracji Hightail do usługi Azure AD, należy tooadd Hightail z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Hightail z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Hightail**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. W panelu wyników hello zaznacz **Hightail**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Hightail w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Hightail jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Hightail musi toobe ustanowione.

W Hightail, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Hightail, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Hightail](#creating-a-hightail-test-user)**  -toohave odpowiednikiem Simona Britta w Hightail, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Hightail.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Hightail, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Hightail** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. Na powitania **Hightail domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     W hello **adres URL odpowiedzi** pole tekstowe, wprowadź adres URL hello jako:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`

    > [!NOTE] 
    > Witaj poprzedniego wartość nie jest prawdziwe. Wartość hello zostanie zaktualizowany hello rzeczywiste odpowiedzi adresu URL, który znajduje się w dalszej części samouczka hello.
 
4. Na powitania **Hightail domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **SP zainicjował tryb**, wykonaj następujące kroki hello:
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    a. Kliknij przycisk hello **Pokaż zaawansowane ustawienia adresu URL**.

    b. W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello jako:`https://www.hightail.com/loginSSO`

4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. Hightail aplikacji oczekuje potwierdzenia SAML hello w określonym formacie. Skonfiguruj powitania po oświadczeń dla tej aplikacji. Można zarządzać hello wartości tych atrybutów z hello **"Atrribute"** kartę aplikacji hello. powitania po zrzut ekranu przedstawia przykład tego. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:
    
    | Nazwa atrybutu | Wartość atrybutu |
    | ------------------- | -------------------- |
    | Imię | User.givenName |
    | Nazwisko | User.surname |
    | Adres e-mail | User.mail |    
    | Tożsamości użytkownika | User.mail |
    
    a. Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    b. W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.

    c. Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.

    d. Pozostaw hello **Namespace** puste.
    
    e. Kliknij przycisk **OK**.

7. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. Na powitania **Hightail konfiguracji** kliknij **skonfigurować Hightail** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    >Przed skonfigurowaniem hello rejestracji jednokrotnej w aplikacji Hightail, białą listę domenę poczty e-mail z Hightail zespołu, aby hello wszystkich użytkowników, którzy korzystają z tej domeny można Użyj funkcji rejestracji jednokrotnej.


9. tooget logowania jednokrotnego skonfigurowane dla aplikacji, należy na toosign tooyour Hightail dzierżawy z uprawnieniami administratora.
   
    a. W menu hello na górze powitania kliknij hello **konta** i wybierz **skonfigurować SAML**.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    b. Zaznacz pole wyboru hello z **Włącz uwierzytelnianie SAML**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    c. Otwieranie certyfikatu zakodowanego base-64 w Notatniku pobrany z portalu Azure, hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **SAML certyfikat podpisywania tokenu** pola tekstowego.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    d. W hello **SAML urzędu (dostawcy tożsamości)** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** skopiowany z portalu Azure.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    e. Jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb** wybierz **"Dostawcy tożsamości (IdP) zainicjował logowania"**. Jeśli **SP zainicjował tryb** wybierz **"Dostawcy usług (SP) zainicjował logowania"**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    f. Skopiuj adres URL klienta SAML hello wystąpienia i wklej go w **adres URL odpowiedzi** textbox w **Hightail domeny i adres URL** sekcji z portalu Azure.
    
    g. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-hightail-test-user"></a>Tworzenie użytkownika testowego Hightail

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Hightail. 

Nie ma elementu akcji można w tej sekcji. Hightail obsługuje użytkownika w czasie inicjowania obsługi administracyjnej oparta na powitania oświadczenia niestandardowe. Jeśli skonfigurowano hello oświadczenia niestandardowe, jak pokazano w sekcji hello  **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  powyżej, użytkownik zostanie automatycznie utworzone w aplikacji hello go jeszcze nie istnieje. 

>[!NOTE]
>Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [zespołem pomocy technicznej Hightail](mailto:support@hightail.com). 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooHightail.

![Przypisz użytkownika][200] 

**tooassign tooHightail Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Hightail**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.

Po kliknięciu kafelka Hightail hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Hightail aplikacji.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

