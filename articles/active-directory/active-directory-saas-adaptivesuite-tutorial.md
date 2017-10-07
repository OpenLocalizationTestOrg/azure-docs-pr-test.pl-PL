---
title: "Samouczek: Azure Active Directory integracji z pakietem adaptacyjną | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i adaptacyjną Suite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a>Samouczek: Integracji Azure Active Directory z adaptacyjną Suite

Z tego samouczka, dowiesz się, jak toointegrate adaptacyjną Suite w usłudze Azure Active Directory (Azure AD).

Integrowanie adaptacyjną pakiet z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooAdaptive Suite
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAdaptive Suite (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z adaptacyjną Suite należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Pakiet adaptacyjną jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie pakietu adaptacyjną z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-adaptive-suite-from-hello-gallery"></a>Dodawanie pakietu adaptacyjną z galerii hello
tooconfigure hello zintegrowania pakietu adaptacyjną usługi Azure AD, należy tooadd adaptacyjną pakiet z listy tooyour galerii hello zarządzanych aplikacji SaaS.

**tooadd adaptacyjną pakiet z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Suite adaptacyjną**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. W panelu wyników hello, wybierz **Suite adaptacyjną**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z adaptacyjną pakietu na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello użytkownika odpowiednikiem pakietu adaptacyjną jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi pakietu adaptacyjną musi toobe ustanowione.

Adaptacyjną pakietu, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i test usługi Azure AD rejestracji jednokrotnej z adaptacyjną Suite należy hello toocomplete po bloków konstrukcyjnych:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego adaptacyjną Suite](#creating-an-adaptive-suite-test-user)**  -toohave odpowiednikiem Simona Britta pakietu adaptacyjną, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne adaptacyjną pakietu aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z adaptacyjną pakiet, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **Suite adaptacyjną** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. Na powitania **adaptacyjną domeny Suite i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`

    >[!NOTE]
    > Tę wartość można uzyskać od hello adaptacyjną Suite **ustawienia logowania jednokrotnego SAML** strony.
    >  

4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. Na powitania **adaptacyjną konfiguracji pakietu** kliknij **skonfigurować pakiet adaptacyjną** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy adaptacyjną Suite tooyour jako administrator.

8. Przejdź za**Admin**.
   
    ![Administrator](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "administratora")

9. W hello **użytkownikami i rolami** kliknij **Zarządzaj ustawieniami logowania jednokrotnego SAML**.
   
    ![Zarządzanie ustawieniami logowania jednokrotnego SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Zarządzanie ustawieniami logowania jednokrotnego SAML")

10. Na powitania **ustawienia logowania jednokrotnego SAML** wykonaj hello następujące kroki:
   
    ![Ustawienia logowania jednokrotnego SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "ustawienia logowania jednokrotnego SAML")

    a. W hello **Nazwa dostawcy tożsamości** tekstowym, wpisz nazwę dla danej konfiguracji.
    
    b. Wklej hello **identyfikator jednostki SAML** wartość skopiowany z portalu Azure do hello **dostawcy tożsamości identyfikator jednostki** pola tekstowego.
  
    c. Wklej hello **SAML pojedynczy znak na adres URL usługi** wartość skopiowany z portalu Azure do hello **dostawcy tożsamości adresu URL logowania jednokrotnego** pola tekstowego.
  
    d. Wklej hello **SAML pojedynczy znak na adres URL usługi** wartość skopiowany z portalu Azure do hello **niestandardowy adres URL wylogowania** pola tekstowego.
  
    e. tooupload pobranego certyfikatu, kliknij przycisk **wybierz plik**.
  
    f. Wybierz poniżej powitania dla:
    * **Identyfikator użytkownika SAML**, wybierz pozycję **nazwy użytkownika adaptacyjną Insights**.
    * **Lokalizacja identyfikator użytkownika SAML**, wybierz pozycję **identyfikatora użytkownika w NameID podmiotu**.
    * **Format SAML NameID**, wybierz pozycję **adres E-mail**.
    * **Włącz SAML**, wybierz pozycję **Zezwalaj logowania jednokrotnego SAML i bezpośrednie logowanie adaptacyjną Insights**.
    
    g. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-adaptive-suite-test-user"></a>Tworzenie użytkownika testowego adaptacyjną Suite

toolog użytkowników tooenable usługi Azure AD w tooAdaptive Suite muszą mieć przydzielone do adaptacyjnego Suite.  

* W przypadku hello pakietu adaptacyjną Inicjowanie obsługi to zadanie ręczne.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:** 

1. Zaloguj się za tooyour **Suite adaptacyjną** witryny firmy jako administrator.
2. Przejdź za**Admin**.
   
   ![Administrator](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "administratora")
3. W hello **użytkownikami i rolami** kliknij **Dodaj użytkownika**.
   
   ![Dodaj użytkownika](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Dodaj użytkownika")
4. W hello **nowego użytkownika** sekcji, wykonaj następujące kroki hello:
   
   ![Przedstawia](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "przesyłania")   

   a. Hello typu **nazwa**, **logowania**, **E-mail**, **hasło** z prawidłowym użytkownikiem usługi Azure Active Directory ma tooprovision do hello powiązane pola tekstowe.
  
   b. Wybierz **roli**.
  
   c. Kliknij przycisk **przesłać**.

>[!NOTE]
>Możesz użyć innych adaptacyjną Suite użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Suite adaptacyjną kont użytkowników usługi AAD.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAdaptive Suite.

![Przypisz użytkownika][200] 

**tooassign tooAdaptive Simona Britta pakiet, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Suite adaptacyjną**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest z usługi Microsoft Azure AD rejestracji jednokrotnej konfiguracji przy użyciu hello panelu dostępu.

Po kliknięciu kafelka adaptacyjną Suite hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour adaptacyjną pakietu aplikacji.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

