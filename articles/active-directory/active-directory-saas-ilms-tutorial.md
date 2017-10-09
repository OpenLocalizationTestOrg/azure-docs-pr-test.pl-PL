---
title: 'Samouczek: Integracji Azure Active Directory z iLMS | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a>Samouczek: Integracji Azure Active Directory z iLMS

Z tego samouczka, dowiesz się, jak iLMS toointegrate w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD iLMS zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooiLMS
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooiLMS (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z iLMS należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- ILMS jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie iLMS z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-ilms-from-hello-gallery"></a>Dodawanie iLMS z galerii hello
tooconfigure hello integracji iLMS do usługi Azure AD, należy iLMS tooadd z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**iLMS tooadd z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **iLMS**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. Wybierz w panelu wyników hello **iLMS**, następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z iLMS w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w iLMS jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w iLMS musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w iLMS.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z iLMS, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego iLMS](#creating-an-ilms-test-user)**  -toohave odpowiednikiem Simona Britta w iLMS, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji iLMS.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z iLMS, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **iLMS** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. Na powitania **iLMS domeny i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    a. W hello **identyfikator** pole tekstowe, Wklej hello **identyfikator** wartość skopiować z **usługodawcy** sekcji SAML ustawień w portalu administracyjnym iLMS.

    b. W hello **adres URL odpowiedzi** pole tekstowe, Wklej hello **(adres URL punktu końcowego)** wartość skopiować z **usługodawcy** sekcji SAML ustawień w portalu administratora iLMS o następujących hello wzorzec`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`

    >[!Note]
    >Ta 123456 jest Przykładowa wartość identyfikatora.

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    W hello **adres URL logowania** pole tekstowe, Wklej hello **(adres URL punktu końcowego)** wartość skopiować z **usługodawcy** sekcji SAML ustawień w portalu administracyjnym iLMS jako`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`     

5. tooenable JIT inicjowania obsługi administracyjnej, iLMS aplikacji oczekuje potwierdzenia SAML hello w określonym formacie. Skonfiguruj powitania po oświadczeń dla tej aplikacji. Można zarządzać hello wartości tych atrybutów z hello **atrybuty użytkownika** sekcji na stronie integracji aplikacji. powitania po zrzut ekranu przedstawia przykład tego.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/4.png)
    
    Utwórz **działu, Region** i **dzielenia** atrybutów, a następnie dodaj nazwę hello tych atrybutów w iLMS. Te atrybuty pokazanym powyżej są wymagane.    

    > [!NOTE] 
    > Masz tooenable **Utwórz konto użytkownika Un-recognized** w iLMS toomap te atrybuty. Postępuj zgodnie z instrukcjami hello [tutaj](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget pomysł na powitania atrybuty konfiguracji.

6. W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w powyższy obraz powitania i wykonywać hello następujące kroki:
    
    | Nazwa atrybutu | Wartość atrybutu |
    | ---------------| --------------- |    
    | dzielenie | User.Department |
    | Region | User.state |
    | Dział | User.jobtitle |

    a. Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    b. W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.
    
    c. Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.
    
    d. Kliknij przycisk **Ok**

7. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. W oknie przeglądarki innej witryny sieci web, zaloguj się za tooyour **portalu administracyjnego iLMS** jako administrator.

10. Kliknij przycisk **SSO:SAML** w obszarze **ustawienia** karcie Ustawienia SAML tooopen i wykonywać hello następujące kroki:
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/1.png) 

    a. Rozwiń węzeł hello **usługodawcy** hello sekcji i skopiuj **identyfikator** i **(adres URL punktu końcowego)** wartość.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/2.png) 

    b. W obszarze **dostawcy tożsamości** kliknij **Importowanie metadanych**.
    
    c. Wybierz hello **metadanych** plik pobrany z portalu Azure z **certyfikat podpisywania SAML** sekcji.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    d. Jeśli chcesz, aby tooenable JIT inicjowania obsługi administracyjnej toocreate iLMS kont un-rozpoznaje użytkowników, wykonaj następujące czynności:
        
       - Sprawdź **utworzyć konto użytkownika nie jest rozpoznawaną**.
       
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  Mapowanie atrybutów hello w usłudze Azure AD z atrybutami hello w iLMS. W kolumnie atrybutu hello Określ hello atrybutów nazwy lub hello wartości domyślnej.

    e. Przejdź za**reguły biznesowe** karcie i wykonywać hello następujące kroki: 
        
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/5.png)

       - Sprawdź **Tworzenie regionów Un-recognized, działów i działów** toocreate regionach, działów i działów, które jeszcze nie istnieją w czasie hello rejestracji jednokrotnej.
        
       - Sprawdź **aktualizacji użytkownika profilu podczas logowania** toospecify Określa, czy profil użytkownika hello jest aktualizowany przy każdej rejestracji jednokrotnej. 
        
       - Jeśli hello **"Aktualizacji puste wartości dla innych niż obowiązkowego pola w profilu użytkownika"** opcja jest zaznaczona, profil opcjonalne pola, które są puste podczas logowania zostanie także spowodować profil iLMS użytkownika hello toocontain puste wartości dla tych pól.
        
       - Sprawdź **Wyślij E-mail z powiadomieniem błąd** , a następnie wprowadź adres e-mail użytkownika hello hello miejscu tooreceive hello błąd powiadomienia e-mail.

11. Kliknij przycisk **zapisać** przycisk toosave hello ustawienia.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
    
### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-ilms-test-user"></a>Tworzenie użytkownika testowego iLMS

Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji hello. JIT będzie działać, jeśli kliknięto hello **Utwórz konto użytkownika Un-recognized** wyboru podczas SAML ustawienie konfiguracji w portalu administracyjnym iLMS.

Jeśli potrzebujesz toocreate użytkownika ręcznie, wykonaj następujące czynności:

1. Zaloguj się w witrynie firmy iLMS tooyour jako administrator.

2. Kliknij przycisk **"Zarejestruj użytkownika"** w obszarze **użytkowników** karcie tooopen **zarejestrować użytkownika** strony. 
   
   ![Dodawanie pracownika](./media/active-directory-saas-ilms-tutorial/3.png)

3. Na powitania **"Zarejestruj użytkownika"** wykonaj następujące kroki hello.

    ![Dodawanie pracownika](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    a. W hello **imię** pole tekstowe, typ hello imię Britta.
   
    b. W hello **nazwisko** pole tekstowe, typ hello nazwisko Simona.

    c. W hello **identyfikator wiadomości E-mail** pole tekstowe, adres e-mail hello typu Simona Britta konta.

    d. W hello **Region** listy rozwijanej wybierz hello wartość dla regionu.

    e. W hello **dzielenia** listy rozwijanej wybierz hello wartość podziału.

    f. W hello **działu** listy rozwijanej wybierz hello wartość dla działu.

    g. Kliknij pozycję **Zapisz**.

    > [!NOTE] 
    > Możesz wysłać toouser poczty rejestracji, wybierając **wysłać wiadomość E-mail rejestracji** wyboru.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooiLMS dostępu.

![Przypisz użytkownika][200] 

**tooassign tooiLMS Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **iLMS**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu powitalne iLMS kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour iLMS aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

