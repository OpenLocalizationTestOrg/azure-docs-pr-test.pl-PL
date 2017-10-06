---
title: 'Samouczek: Integracji Azure Active Directory z Zscaler ZSCloud | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Zscaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a>Samouczek: Integracji Azure Active Directory z Zscaler ZSCloud

Z tego samouczka, dowiesz się, jak toointegrate Zscaler ZSCloud w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Zscaler ZSCloud zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooZscaler ZSCloud
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooZscaler ZSCloud (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z Zscaler ZSCloud należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Zscaler ZSCloud logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Zscaler ZSCloud z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a>Dodawanie Zscaler ZSCloud z galerii hello
tooconfigure hello integracji Zscaler ZSCloud do usługi Azure AD, należy tooadd Zscaler ZSCloud z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Zscaler ZSCloud z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Zscaler ZSCloud**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. W panelu wyników hello, wybierz **Zscaler ZSCloud**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Zscaler ZSCloud oparte na użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Zscaler ZSCloud jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Zscaler ZSCloud musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Zscaler ZSCloud.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Zscaler ZSCloud, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Konfigurowanie ustawień serwera proxy](#configuring-proxy-settings)**  — ustawienia serwera proxy hello tooconfigure w programie Internet Explorer
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  -toohave odpowiednikiem Simona Britta w Zscaler ZSCloud, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Zscaler ZSCloud.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Zscaler ZSCloud wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **Zscaler ZSCloud** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. Na powitania **Zscaler ZSCloud domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello używany przez Twoje użytkowników toosign na tooyour ZScaler ZSCloud aplikacji.
    
    > [!NOTE] 
    > Masz tooupdate tej wartości z hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta ZSCloud Zscaler](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget tej wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji ZSCloud Zscaler** kliknij **skonfigurować Zscaler ZSCloud** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się za tooyour ZScaler ZSCloud witryny firmy jako administrator.

8. W menu hello na górze hello, kliknij przycisk **administracji**.
   
    ![Administracja](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "administracji")

9. W obszarze **administratorom zarządzanie & role**, kliknij przycisk **Zarządzanie użytkownikami & uwierzytelniania**.   
            
    ![Zarządzaj użytkownikami & uwierzytelniania](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "zarządzania użytkownikami i uwierzytelniania")

10. W hello **wybierz opcje uwierzytelniania dla Twojej organizacji** sekcji, wykonaj następujące kroki hello:   
                
    ![Uwierzytelnianie](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "uwierzytelniania")
   
    a. Wybierz **uwierzytelnianie przy użyciu SAML logowania jednokrotnego**.

    b. Kliknij przycisk **skonfigurować SAML pojedynczego logowania jednokrotnego parametry**.

11. Na powitania **skonfigurować SAML pojedynczych logowania jednokrotnego parametrów** strony okna dialogowego, wykonaj następujące kroki hello, a następnie kliknij **gotowe**

    ![Logowanie jednokrotne](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "logowanie jednokrotne")
    
    a. Wklej hello **SAML pojedynczy znak na adres URL usługi** wartości do hello **adres URL hello SAML portalu toowhich użytkowników są wysyłane do uwierzytelniania** pola tekstowego.
    
    b. W hello **atrybutu zawierającego nazwę logowania** pole tekstowe, typ **NameID**.
    
    c. tooupload pobranego certyfikatu, kliknij przycisk **Zscaler pem**.
    
    d. Wybierz **Włącz SAML automatycznego inicjowania obsługi**.

12. Na powitania **skonfigurować uwierzytelnianie użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![Administracja](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "administracji")
    
    a. Kliknij pozycję **Zapisz**.

    b. Kliknij przycisk **Aktywuj teraz**.

## <a name="configuring-proxy-settings"></a>Konfigurowanie ustawień serwera proxy
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>ustawienia serwera proxy hello tooconfigure w programie Internet Explorer

1. Uruchom **programu Internet Explorer**.

2. Wybierz **Opcje internetowe** z hello **narzędzia** menu Otwórz hello **Opcje internetowe** okna dialogowego.   
    
     ![Opcje internetowe](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Opcje internetowe")

3. Kliknij przycisk hello **połączeń** kartę.   
  
     ![Połączenia](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "połączeń")

4. Kliknij przycisk **ustawienia sieci LAN** tooopen hello **ustawienia sieci LAN** okna dialogowego.

5. W sekcji serwer Proxy hello wykonaj hello następujące kroki:   
   
    ![Serwer proxy](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "serwera Proxy")

    a. Wybierz **Użyj serwera proxy dla sieci LAN**.

    b. W polu tekstowym adres hello, wpisz **gateway.zscalerone.net**.

    c. W polu tekstowym portu hello, wpisz **80**.

    d. Wybierz **używaj serwera proxy dla adresów lokalnych**.

    e. Kliknij przycisk **OK** tooclose hello **ustawienia sieci lokalnej (LAN)** okna dialogowego.

6. Kliknij przycisk **OK** tooclose hello **Opcje internetowe** okna dialogowego.

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.

### <a name="creating-a-zscaler-zscloud-test-user"></a>Tworzenie użytkownika testowego Zscaler ZSCloud

tooenable usługi Azure AD użytkownicy toolog tooZScaler ZSCloud, muszą być elastycznie tooZScaler ZSCloud.  
W przypadku hello ZScaler ZSCloud Inicjowanie obsługi to zadanie ręczne.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:

1. Zaloguj się za tooyour **Zscaler** dzierżawy.

2. Kliknij przycisk **administracji**.   
   
    ![Administracja](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "administracji")

3. Kliknij przycisk **Zarządzanie użytkownikami**.   
        
     ![Dodaj](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Dodaj")

4. W hello **użytkowników** , kliknij pozycję **Dodaj**.
      
    ![Dodaj](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Dodaj")

5. W sekcji Dodaj użytkownika hello wykonaj hello następujące kroki:
        
    ![Dodaj użytkownika](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Dodaj użytkownika")
   
    a. Hello typu **UserID**, **Nazwa wyświetlana użytkownika**, **hasło**, **Potwierdź hasło**, a następnie wybierz **grup**i hello **działu** ma tooprovision poprawnego konta usługi AAD.

    b. Kliknij pozycję **Zapisz**.

> [!NOTE]
> Możesz użyć innych ZScaler ZSCloud użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision ZScaler ZSCloud kont użytkowników usługi AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooZscaler ZSCloud.

![Przypisz użytkownika][200] 

**tooassign tooZscaler Simona Britta ZSCloud, wykonaj następujące kroki hello:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Zscaler ZSCloud**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.

Po kliknięciu hello Zscaler ZSCloud kafelka w hello Panel dostępu, należy pobrać zalogowane automatycznie tooyour Zscaler ZSCloud aplikacji.

Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

