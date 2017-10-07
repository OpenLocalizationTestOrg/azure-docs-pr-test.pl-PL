---
title: 'Samouczek: Azure Active Directory integracji z produktem Workday | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i dzień roboczy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a>Samouczek: Azure Active Directory integracji z produktem Workday

Z tego samouczka, dowiesz się, jak toointegrate produktu Workday w usłudze Azure Active Directory (Azure AD).

Integrowanie pracy z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooWorkday
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWorkday (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z produktem Workday, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Produktu Workday jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie produktu Workday z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-workday-from-hello-gallery"></a>Dodawanie produktu Workday z galerii hello
tooconfigure hello integracji z produktem Workday do usługi Azure AD, należy tooadd produktu Workday z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd produktu Workday z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **produktu Workday**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. W panelu wyników hello zaznacz **produktu Workday**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z produktu Workday oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w produktu Workday jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w pracy musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w pracy.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z produktem Workday, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego produktu Workday](#creating-a-workday-test-user)**  -toohave odpowiednikiem Simona Britta w pracy, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji produktu Workday.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z produktem Workday, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **produktu Workday** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. Na powitania **produktu Workday domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    a. W hello **adres URL logowania** pole tekstowe, wartość hello typu jako:`https://impl.workday.com/<tenant>/login-saml2.htmld`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://impl.workday.com/<tenant>/login-saml.htmld`

    > [!NOTE] 
    > Wartości te nie są hello prawdziwe. Witaj rzeczywisty adres URL logowania i adres URL odpowiedzi, należy zaktualizować te wartości. Adres URL odpowiedzi muszą mieć poddomeny na przykład: www, wd2, wd3, wd3 impl, wd5, wd5 impl). Przy użyciu przypominać "*http://www.myworkday.com*" działa, ale "*http://myworkday.com*" nie ma. Skontaktuj się z [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html) tooget tych wartości. 
 

4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji produktu Workday** kliknij **Konfigurowanie produktu Workday** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS>
7. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy produktu Workday tooyour jako administrator.

8. Przejdź za**Menu \> Workbench**.
   
    ![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")

9. Przejdź za**administrowania kontami**.
   
    ![Konto administracji](./media/active-directory-saas-workday-tutorial/IC782924.png "konta administracji")

10. Przejdź za**Edytuj ustawienia dzierżawy — zabezpieczeń**.
   
    ![Edytuj zabezpieczenia dzierżawy](./media/active-directory-saas-workday-tutorial/IC782925.png "Edytuj zabezpieczenia dzierżawy")

11. W hello **adresów URL przekierowań** sekcji, wykonaj następujące kroki hello:
   
    ![Adresy URL przekierowania](./media/active-directory-saas-workday-tutorial/IC7829581.png "adresów URL przekierowań")
   
    a. Kliknij przycisk **Dodaj wiersz**.
   
    b. W hello **Przekierowywanie adresu URL logowania do** pole tekstowe i hello **adresem URL przekierowania Mobile** pole tekstowe, hello typu **adres URL logowania** wprowadzono hello **produktu Workday domeny i Adresy URL** sekcji hello portalu Azure.
   
    c. W portalu Azure na powitania hello **Konfigurowanie logowania jednokrotnego** okna, hello kopii **Sign-Out URL**, a następnie wklej go do hello **adresem URL przekierowania wylogowania** pola tekstowego.
   
    d.  W **środowiska** pole tekstowe, nazwa środowiska hello typu.  

    >[!NOTE]
    > Witaj wartość atrybutu środowisko hello jest powiązany adres URL dzierżawy hello toohello wartość:  
    >— Czy nazwa domeny hello adres URL dzierżawy produktu Workday hello rozpoczyna się od impl na przykład: *https://impl.workday.com/\<dzierżawy\>/login-saml2.htmld*), hello **środowiska** Atrybut musi być ustawiona tooImplementation.  
    >— Jeśli hello nazwy domeny rozpoczynają się od czegoś innego, należy toocontact [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html) dopasowania hello tooget **środowiska** wartość.

12. W hello **Instalatora SAML** sekcji, wykonaj następujące kroki hello:
   
    ![Instalator SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Instalatora SAML")
   
    a.  Wybierz **włączyć uwierzytelnianie SAML**.
   
    b.  Kliknij przycisk **Dodaj wiersz**.

13. W sekcji dostawców tożsamości SAML hello wykonaj hello następujące kroki:
   
    ![Dostawców tożsamości SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "dostawców tożsamości SAML")
   
    a. W polu tekstowym Nazwa dostawcy tożsamości hello, wpisz nazwę dostawcy (na przykład: *SPInitiatedSSO*).
   
    b. W portalu Azure na powitania hello **Konfigurowanie logowania jednokrotnego** okna, hello kopiowania **identyfikator jednostki SAML** wartość, a następnie wklej go do hello **wystawcy** pola tekstowego.
   
    c. Wybierz **włączyć Workday wylogowania inicjowane**.
   
    d. W portalu Azure na powitania hello **Konfigurowanie logowania jednokrotnego** okna, hello kopiowania **Sign-Out URL** wartość, a następnie wklej go do hello **adresu URL wylogowania żądania** pola tekstowego.

    e. Kliknij przycisk **certyfikatu klucza publicznego dostawcy tożsamości**, a następnie kliknij przycisk **Utwórz**. 

    ![Utwórz](./media/active-directory-saas-workday-tutorial/IC782928.png "tworzenie")

    f. Kliknij przycisk **x509 Utwórz klucz publiczny**. 

    ![Utwórz](./media/active-directory-saas-workday-tutorial/IC782929.png "tworzenie")


14. W hello **klucza publicznego widoku x509** sekcji, wykonaj następujące kroki hello: 
   
    ![Klucz publiczny widoku x509](./media/active-directory-saas-workday-tutorial/IC782930.png "widoku x509 klucza publicznego") 
   
    a. W hello **nazwa** tekstowym, wpisz nazwę dla certyfikatu (na przykład: *ŚOI\_SP*).
   
    b. W hello **ważny od** pole tekstowe, typ hello ważny od wartości atrybutu certyfikatu.
   
    c.  W hello **ważny do** pole tekstowe, wartość prawidłowy tooattribute hello typu certyfikatu.
   
    > [!NOTE]
    > Można odczytać hello prawidłową datę i hello prawidłową toodate z hello pobrany certyfikat, kliknij go dwukrotnie.  Witaj daty są wyświetlane w obszarze hello **szczegóły** kartę.
    > 
    >
   
    d.  Otwórz certyfikatu zakodowanego base-64 w Notatniku i hello kopiowania zawartości z niego.
   
    e.  W hello **certyfikatu** pole tekstowe, hello Wklej zawartość Schowka.
   
    f.  Kliknij przycisk **OK**.

15. Wykonaj następujące kroki hello: 
   
    ![Konfiguracja rejestracji Jednokrotnej](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "konfiguracji logowania jednokrotnego")
   
    a.  Włącz hello **x509 pary klucza prywatnego**.
   
    b.  W hello **identyfikator dostawcy usługi** pole tekstowe, typ **http://www.workday.com**.
   
    c.  Wybierz **Włącz SP zainicjował uwierzytelnianie SAML**.
   
    d.  W portalu Azure na powitania hello **Konfigurowanie logowania jednokrotnego** okna, hello kopiowania **SAML pojedynczy znak na adres URL usługi** wartość, a następnie wklej go do hello **adres URL usługi logowania jednokrotnego IdP** pola tekstowego.
   
    e. Wybierz **nie Deflate żądania uwierzytelnienia zainicjowane SP**.
   
    f. Jako **podpisu żądania uwierzytelnienia**, wybierz pozycję **SHA256**. 
   
    ![Metoda podpisu żądania uwierzytelniania](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "metoda podpisu żądania uwierzytelniania") 
   
    g. Kliknij przycisk **OK**. 
   
    ![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE>

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
>

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-workday-test-user"></a>Tworzenie użytkownika testowego produktu Workday

tooget użytkownika testowego udostępnione do produktu Workday należy toocontact hello [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html).
Witaj [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html) tworzy hello użytkownika.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWorkday.

![Przypisz użytkownika][200] 

**tooassign tooWorkday Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **produktu Workday**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Skonfiguruj Inicjowanie obsługi użytkowników](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

