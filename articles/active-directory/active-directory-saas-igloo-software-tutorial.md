---
title: 'Samouczek: Azure Active Directory integracji z oprogramowaniem Igloo | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między oprogramowaniem Igloo i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a>Samouczek: Azure Active Directory integracji z oprogramowaniem Igloo

Z tego samouczka, dowiesz się, jak toointegrate Igloo oprogramowania w usłudze Azure Active Directory (Azure AD).

Integracja oprogramowania Igloo z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooIgloo oprogramowania
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooIgloo oprogramowania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z oprogramowaniem Igloo należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Oprogramowanie Igloo logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie oprogramowania Igloo z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-igloo-software-from-hello-gallery"></a>Dodawanie oprogramowania Igloo z galerii hello
tooconfigure hello integracji Igloo oprogramowania do usługi Azure AD, należy tooadd Igloo oprogramowania z listy tooyour galerii hello zarządzanych aplikacji SaaS.

**tooadd Igloo oprogramowania z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **oprogramowania Igloo**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. W panelu wyników hello, wybierz **oprogramowania Igloo**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Igloo w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w oprogramowaniu Igloo jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w oprogramowaniu Igloo musi toobe ustanowione.

W oprogramowaniu Igloo, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Igloo, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego oprogramowania Igloo](#creating-an-igloo-software-test-user)**  -toohave odpowiednikiem Simona Britta Igloo oprogramowania, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w używanej aplikacji Igloo.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Igloo wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **oprogramowania Igloo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. Na powitania **Igloo oprogramowania domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.igloocommmunities.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.igloocommmunities.com/saml.digest`

    c. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.igloocommmunities.com/saml.digest`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta oprogramowania Igloo](https://www.igloosoftware.com/services/support) tooget tych wartości. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. Na powitania **konfiguracji oprogramowania Igloo** kliknij **Konfigurowanie oprogramowania Igloo** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy oprogramowania Igloo tooyour jako administrator.

8. Przejdź toohello **Panelu sterowania**.
   
     ![Panel sterowania](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Panel sterowania")

9. W hello **członkostwa** , kliknij pozycję **znak ustawień**.
   
    ![Zaloguj się w ustawieniach](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Zaloguj ustawienia")

10. W sekcji konfiguracji SAML hello, kliknij przycisk **skonfigurować uwierzytelnianie SAML**.
   
    ![Konfiguracja SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Konfiguracja SAML")
   
11. W hello **Konfiguracja ogólna** sekcji, wykonaj następujące kroki hello:
   
    ![Konfiguracja ogólna](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "konfiguracji ogólnej")

    a. W hello **nazwa połączenia** tekstowym, wpisz nazwę niestandardową dla danej konfiguracji.
   
    b. W hello **adres URL logowania IdP** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.
   
    c. W hello **adresu URL wylogowania IdP** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.
    
    d. Wybierz **wylogowania odpowiedzi i żądania HTTP typu** jako **POST**.
   
    e. Otwórz z **base-64** zakodowany certyfikat w Notatniku pobrany z portalu Azure, hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu publicznego** pola tekstowego.
    
12. W hello **odpowiedzi i konfiguracji uwierzytelniania**, wykonaj następujące kroki hello:
    
    ![Odpowiedź i konfiguracji uwierzytelniania](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "odpowiedzi i konfiguracji uwierzytelniania")
  
      a. Jako **dostawcy tożsamości**, wybierz pozycję **Microsoft ADFS**.
      
      b. Jako **typ identyfikatora**, wybierz pozycję **adres E-mail**. 

      c. W hello **atrybut poczty E-mail** pole tekstowe, typ **emailaddress**.

      d. W hello **atrybutu imię** pole tekstowe, typ **givenname**.

      e. W hello **ostatniego atrybutu Name** pole tekstowe, typ **nazwisko**.

13. Wykonaj następujące kroki toocomplete hello konfiguracji hello:
    
    ![Tworzenie użytkownika na logowania](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Tworzenie użytkownika na logowania") 

     a. Jako **Tworzenie użytkownika na logowania**, wybierz pozycję **utworzenie nowego użytkownika w swojej witrynie, po zalogowaniu**.

     b. Jako **Zaloguj ustawienia**, wybierz pozycję **SAML użyj przycisku na ekranie "Zaloguj"**.

     c. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-igloo-software-test-user"></a>Tworzenie użytkownika testowego Igloo oprogramowania

Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooIgloo oprogramowania.  

Gdy toolog prób przypisany użytkownik za pomocą oprogramowania tooIgloo hello panel dostępu, Igloo oprogramowania sprawdza, czy użytkownik hello istnieje.  Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez oprogramowanie Igloo.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooIgloo oprogramowania.

![Przypisz użytkownika][200] 

**tooassign tooIgloo Simona Britta oprogramowania, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **oprogramowania Igloo**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka oprogramowania Igloo hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Igloo aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

