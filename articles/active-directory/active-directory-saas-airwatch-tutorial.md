---
title: 'Samouczek: Integracji Azure Active Directory z AirWatch | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i AirWatch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a>Samouczek: Integracji Azure Active Directory z AirWatch

Z tego samouczka, dowiesz się, jak toointegrate AirWatch w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD AirWatch zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAirWatch
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAirWatch (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z AirWatch należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- AirWatch jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie AirWatch z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-airwatch-from-hello-gallery"></a>Dodawanie AirWatch z galerii hello
tooconfigure hello integracji AirWatch do usługi Azure AD, należy tooadd AirWatch z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd AirWatch z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **AirWatch**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. W panelu wyników hello zaznacz **AirWatch**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AirWatch na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w AirWatch jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w AirWatch musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w AirWatch.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z AirWatch, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego AirWatch](#creating-a-airwatch-test-user)**  -toohave odpowiednikiem Simona Britta w AirWatch, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji AirWatch.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z AirWatch, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **AirWatch** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. Na powitania **AirWatch domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`

    b. W hello **identyfikator** pole tekstowe, wartość hello typu jako`AirWatch`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe hello. Zaktualizuj tę wartość przy hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta AirWatch](http://www.air-watch.com/company/contact-us/) tooget tej wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. Na powitania **konfiguracji AirWatch** kliknij **skonfigurować AirWatch** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS>
7. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy AirWatch tooyour jako administrator.

8. W okienku nawigacji po lewej stronie powitania kliknij **kont**, a następnie kliknij przycisk **Administratorzy**.
   
   ![Administratorzy](./media/active-directory-saas-airwatch-tutorial/ic791920.png "administratorów")

9. Rozwiń węzeł hello **ustawienia** menu, a następnie kliknij przycisk **usług katalogowych**.
   
   ![Ustawienia](./media/active-directory-saas-airwatch-tutorial/ic791921.png "ustawienia")

10. Kliknij przycisk hello **użytkownika** na karcie hello **bazowa nazwa Wyróżniająca** tekstowym, wpisz nazwę domeny, a następnie kliknij przycisk **zapisać**.
   
   ![Użytkownik](./media/active-directory-saas-airwatch-tutorial/ic791922.png "użytkownika")

11. Kliknij przycisk hello **serwera** kartę.
   
   ![Serwer](./media/active-directory-saas-airwatch-tutorial/ic791923.png "serwera")

12. Wykonaj następujące kroki hello:
    
    ![Przekaż](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Przekaż")   
    
    a. Jako **typ katalogu**, wybierz pozycję **Brak**.

    b. Wybierz **SAML jest używany do uwierzytelniania**.

    c. tooupload hello pobranego certyfikatu, kliknij przycisk **przekazać**.

13. W hello **żądania** sekcji, wykonaj następujące kroki hello:
    
    ![Żądanie](./media/active-directory-saas-airwatch-tutorial/ic791925.png "żądania")  

    a. Jako **żądania typu powiązania**, wybierz pozycję **POST**.

    b. W portalu Azure na powitania hello **skonfigurować logowanie jednokrotne w Airwatch** strony okna dialogowego, hello kopiowania **SAML pojedynczy znak na adres URL usługi** wartość, a następnie wklej go do hello **dostawcy tożsamości Pojedynczy znak na adres URL** pola tekstowego.

    c. Jako **NameID Format**, wybierz pozycję **adres E-mail**.

    d. Kliknij pozycję **Zapisz**.

14. Kliknij przycisk hello **użytkownika** karcie ponownie.
    
    ![Użytkownik](./media/active-directory-saas-airwatch-tutorial/ic791926.png "użytkownika")

15. W hello **atrybutu** sekcji, wykonaj następujące kroki hello:
    
    ![Atrybut](./media/active-directory-saas-airwatch-tutorial/ic791927.png "atrybutu")

    a. W hello **identyfikator obiektu** pole tekstowe, typ **http://schemas.microsoft.com/identity/claims/objectidentifier**.

    b. W hello **Username** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    c. W hello **Nazwa wyświetlana** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    d. W hello **imię** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    e. W hello **nazwisko** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

    f. W hello **E-mail** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    g. Kliknij pozycję **Zapisz**.

<CE>

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z Simona Britta.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-airwatch-test-user"></a>Tworzenie użytkownika testowego AirWatch

toolog użytkowników tooenable usługi Azure AD w tooAirWatch, muszą mieć przydzielone w tooAirWatch.

* Gdy AirWatch, inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour **AirWatch** witryny firmy jako administrator.
2. W okienku nawigacji hello po lewej stronie powitania kliknij **kont**, a następnie kliknij przycisk **użytkowników**.
   
   ![Użytkownicy](./media/active-directory-saas-airwatch-tutorial/ic791929.png "użytkowników")
3. W hello **użytkowników** menu, kliknij przycisk **widok listy**, a następnie kliknij przycisk **Dodaj \> Dodaj użytkownika**.
   
   ![Dodaj użytkownika](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Dodaj użytkownika")
4. Na powitania **Dodaj / Edytuj użytkownika** okna dialogowego, wykonaj następujące kroki hello:

   ![Dodaj użytkownika](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Dodaj użytkownika")   
   1. Typ hello **Username**, **hasło**, **Potwierdź hasło**, **imię**, **nazwisko**,  **Adres e-mail** prawidłowy Azure związanych z kontem usługi Active Directory, mają tooprovision w hello pól tekstowych.
   2. Kliknij pozycję **Zapisz**.

>[!NOTE]
>Możesz użyć innych AirWatch użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez AirWatch tooprovision kont użytkowników usługi AAD.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAirWatch.

![Przypisz użytkownika][200] 

**tooassign tooAirWatch Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **AirWatch**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

