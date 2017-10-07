---
title: 'Samouczek: Integracji Azure Active Directory z TimeOffManager | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a>Samouczek: Integracji Azure Active Directory z TimeOffManager

Z tego samouczka, dowiesz się, jak toointegrate TimeOffManager w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD TimeOffManager zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTimeOffManager
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTimeOffManager (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z TimeOffManager należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- TimeOffManager logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodaj TimeOffManager z galerii hello
2. Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

## <a name="add-timeoffmanager-from-hello-gallery"></a>Dodaj TimeOffManager z galerii hello
tooconfigure hello integracji TimeOffManager do usługi Azure AD, należy tooadd TimeOffManager z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd TimeOffManager z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **TimeOffManager**, wybierz pozycję **TimeOffManager** z panelu wyników, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Dodaj z galerii](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TimeOffManager w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w TimeOffManager jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w TimeOffManager musi toobe ustanowione.

W TimeOffManager, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z TimeOffManager, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave odpowiednikiem Simona Britta w TimeOffManager, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji TimeOffManager.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z TimeOffManager, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **TimeOffManager** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![SAML na podstawie logowania jednokrotnego](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. Na powitania **TimeOffManager domeny i adres URL** sekcji, wykonaj następujące hello:

     ![Sekcja TimeOffManager domeny i adresy URL](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Zaktualizuj tę wartość przy hello rzeczywisty adres URL odpowiedzi służący. Można uzyskać wartość tego parametru **logowania jednokrotnego strony ustawień** którym znajduje się w dalszej części samouczka hello lub skontaktuj się z [zespołem pomocy technicznej TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooTimeOffManger do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.
    
    Aplikacja TimeOffManger oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji. powitania po zrzut ekranu przedstawia przykład tego.

    ![atrybuty tokenu SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "atrybuty tokenu saml")
    
    | Nazwa atrybutu | Wartość atrybutu |
    | --- | --- |
    | Imię |User.givenName |
    | nazwisko |User.surname |
    | Adres e-mail |User.mail |
    
    a.  Dla każdego wiersza danych w powyższej tabeli powitania kliknij **Dodaj atrybut użytkownika**.
    
    ![atrybuty tokenu SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "atrybuty tokenu saml")
    
    ![atrybuty tokenu SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "atrybuty tokenu saml")
    
    b.  W hello **nazwa atrybutu** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.
    
    c.  W hello **wartość atrybutu** pole tekstowe, wartość atrybutu hello wybierz wyświetlanego dla tego wiersza.
    
    d.  Kliknij przycisk **OK**.
    
6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. Na powitania **konfiguracji TimeOffManager** kliknij **skonfigurować TimeOffManager** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Sekcja konfiguracji TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy TimeOffManager jako administrator.

9. Przejdź za**konta \> opcje konta \> ustawień rejestracji jednokrotnej**.
   
   ![Single Sign-On ustawienia](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On ustawienia")
7. W hello **ustawień rejestracji jednokrotnej** sekcji, wykonaj następujące kroki hello:
   
   ![Single Sign-On ustawienia](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On ustawienia")
   
   a. Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej hello cały certyfikat do **certyfikatu X.509** pola tekstowego.
   
   b. W **wystawcy Idp** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.
   
   c. W **adres URL punktu końcowego IdP** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.
   
   d. Jako **wymusić SAML**, wybierz pozycję **nr**.
   
   e. Jako **automatyczne tworzenie użytkowników**, wybierz pozycję **tak**.
   
   f. W **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.
   
   g. Kliknij przycisk **zapisać zmiany**.

11. W **logowania jednokrotnego ustawienia** strony wartość hello kopiowania **adres URL usługi klienta potwierdzenia** i wklej go w hello **adres URL odpowiedzi** pole tekstowe w obszarze **TimeOffManager Adresy URL i domeny** sekcji w portalu Azure. 

      ![Single Sign-On ustawienia](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On ustawienia")

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Użytkownicy i grupy--> Wszyscy użytkownicy](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Dodawanie przycisku](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Strony okna dialogowego użytkownika](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-timeoffmanager-test-user"></a>Tworzenie użytkownika testowego TimeOffManager

Użytkownicy usługi Azure AD toolog kolejności tooenable do TimeOffManager muszą być tooTimeOffManager elastycznie.  

TimeOffManager obsługuje tylko w czasie Inicjowanie obsługi użytkowników. Nie ma elementu akcji dla Ciebie.  

Witaj użytkownicy są automatycznie dodawane podczas logowania pierwszy hello przy użyciu rejestracji jednokrotnej w.

>[!NOTE]
>Możesz użyć innych TimeOffManager użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez TimeOffManager tooprovision kont użytkowników usługi Azure AD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTimeOffManager.

![Przypisz użytkownika][200] 

**tooassign tooTimeOffManager Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **TimeOffManager**.

    ![TimeOffManager listy aplikacji](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka TimeOffManager hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour TimeOffManager aplikacji. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

