---
title: 'Samouczek: Integracji Azure Active Directory z Sprinklr | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a>Samouczek: Integracji Azure Active Directory z Sprinklr

Z tego samouczka, dowiesz się, jak toointegrate Sprinklr w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Sprinklr zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSprinklr
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSprinklr (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Sprinklr należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Sprinklr jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Sprinklr z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-sprinklr-from-hello-gallery"></a>Dodawanie Sprinklr z galerii hello
tooconfigure hello integracji Sprinklr do usługi Azure AD, należy tooadd Sprinklr z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Sprinklr z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Sprinklr**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. W panelu wyników hello zaznacz **Sprinklr**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Sprinklr na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Sprinklr jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Sprinklr musi toobe ustanowione.

W Sprinklr, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Sprinklr, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Sprinklr](#creating-a-sprinklr-test-user)**  -toohave odpowiednikiem Simona Britta w Sprinklr, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Sprinklr.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Sprinklr, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Sprinklr** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. Na powitania **Sprinklr domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.sprinklr.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.sprinklr.com`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizuj wartość hello z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta Sprinklr](https://www.sprinklr.com/contact-us/) tooget tych wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Sprinklr** kliknij **skonfigurować Sprinklr** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

7. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Sprinklr tooyour jako administrator.

8. Przejdź za**administracji \> ustawienia**.
   
    ![Administracja](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "administracji")

9. Przejdź za**Zarządzanie partnera \> jednokrotnego** na w okienku po lewej stronie powitania.
   
    ![Zarządzanie partnerem](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Zarządzanie partnera")

10. Kliknij przycisk **+ dodatki jednokrotnego**.
   
    ![Pojedynczy prób logowania](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "pojedynczy prób logowania")

11. Na powitania **logowania jednokrotnego** wykonaj hello następujące kroki:
   
    ![Pojedynczy prób logowania](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "pojedynczy prób logowania")

    a. W hello **nazwa** tekstowym, wpisz nazwę konfiguracji (na przykład: *WAADSSOTest*).

    b. Wybierz **włączone**.

    c. Wybierz **korzystania z nowego certyfikatu logowania jednokrotnego**.
             
    e. Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat dostawcy tożsamości** pola tekstowego.

    f. Wklej hello **identyfikator jednostki SAML** wartość, która została skopiowana z portalu Azure do hello **identyfikator jednostki** pola tekstowego.

    g. Wklej hello **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z portalu Azure do hello **adresu URL logowania do dostawcy tożsamości** pola tekstowego.

    h. Wklej hello **Sign-Out URL** wartość, która została skopiowana z portalu Azure do hello **adres URL wylogowania dostawcy tożsamości** pola tekstowego.
     
    i. Jako **typ Identyfikatora użytkownika SAML**, wybierz pozycję **potwierdzenia zawiera użytkownika "s sprinklr.com username**.

    j. Jako **lokalizacji identyfikator użytkownika SAML**, wybierz pozycję **identyfikator użytkownika jest w elemencie identyfikator nazwy hello hello instrukcji podmiotu**.

    k. Kliknij pozycję **Zapisz**.
       
    ![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-sprinklr-test-user"></a>Tworzenie użytkownika testowego Sprinklr

1. Zaloguj się za tooyour Sprinklr witryny firmy jako administrator.

2. Przejdź za**administracji \> ustawienia**.
   
    ![Administracja](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "administracji")

3. Przejdź za**klienta zarządzania \> użytkowników** w okienku po lewej stronie powitania.
   
    ![Ustawienia](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "ustawienia")

4. Kliknij przycisk **dodać użytkownika**.
   
    ![Ustawienia](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "ustawienia")

5. Na powitania **Edycja użytkownika** okna dialogowego, wykonaj następujące kroki hello:
   
    ![Edytowanie użytkownika](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edycja użytkownika") 

    a. W hello **E-mail**, **imię** i **nazwisko** pól tekstowych, informacje o typie hello ma tooprovision konta użytkownika usługi Azure AD.

    b. Wybierz **wyłączone hasło**.

    c. Wybierz **języka**.

    d. Wybierz **typ użytkownika**.

    e. Kliknij przycisk **aktualizacji**.
   
     >[!IMPORTANT]
     >**Wyłączone hasło** musi być wybrany tooenable toolog użytkownika w za pośrednictwem dostawcy tożsamości. 
     
6. Przejdź za**roli**, a następnie wykonaj następujące kroki hello:
   
    ![Partnera ról](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "partnera ról")

    a. Z hello **Global** listy, wybierz **wszystkie\_uprawnienia**.  

    b. Kliknij przycisk **aktualizacji**.

>[!NOTE]
>Możesz użyć innych Sprinklr użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Sprinklr tooprovision kont użytkowników usługi Azure AD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSprinklr.

![Przypisz użytkownika][200] 

**tooassign tooSprinklr Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Sprinklr**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Sprinklr hello w hello panelu dostępu get automatycznie zalogowane tooyour Sprinklr aplikacji, aby uzyskać więcej informacji na temat hello panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

