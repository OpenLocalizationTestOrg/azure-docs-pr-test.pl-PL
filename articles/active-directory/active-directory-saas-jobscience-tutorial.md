---
title: 'Samouczek: Integracji Azure Active Directory z Jobscience | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a>Samouczek: Integracji Azure Active Directory z Jobscience

Z tego samouczka, dowiesz się, jak toointegrate Jobscience w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Jobscience zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooJobscience
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooJobscience (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Jobscience należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Jobscience logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Jobscience z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-jobscience-from-hello-gallery"></a>Dodawanie Jobscience z galerii hello
tooconfigure hello integracji Jobscience do usługi Azure AD, należy tooadd Jobscience z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Jobscience z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Jobscience**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. W panelu wyników hello zaznacz **Jobscience**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Jobscience na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Jobscience jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Jobscience musi toobe ustanowione.

W Jobscience, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Jobscience, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Jobscience](#creating-a-jobscience-test-user)**  -toohave odpowiednikiem Simona Britta w Jobscience, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Jobscience.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Jobscience, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Jobscience** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. Na powitania **Jobscience domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://<company name>.my.salesforce.com`
    
    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania. Uzyskać tę wartość za pomocą [zespołem pomocy technicznej klienta Jobscience](https://www.jobscience.com/support) lub z profilu rejestracji Jednokrotnej hello zostanie utworzona, który znajduje się w dalszej części samouczka hello. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Jobscience** kliknij **skonfigurować Jobscience** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. Zaloguj się za tooyour Jobscience witryny firmy jako administrator.

8. Przejdź za**Instalatora**.
   
   ![Instalator](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Instalatora")

9. W okienku nawigacji po lewej stronie powitania w hello **Administruj** , kliknij przycisk **Zarządzanie domenami** tooexpand hello powiązanych sekcji, a następnie kliknij przycisk **Moje domeny** tooopen hello  **Mojej domeny** strony. 
   
   ![Mojej domeny](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mojej domeny")

10. tooverify, który domeny nie został skonfigurowany prawidłowo, upewnij się, że jest on "**krok 4 wdrożone tooUsers**" i zapoznaj się z "**Moje ustawienia domeny**".

    ![Domeny wdrożono tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser wdrożone domeny")

11. W witrynie hello Jobscience firmy, kliknij przycisk **kontroli bezpieczeństwa**, a następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.
    
    ![Opcje zabezpieczeń](./media/active-directory-saas-jobscience-tutorial/ic784364.png "środki zabezpieczające.")

12. W hello **ustawień rejestracji jednokrotnej** sekcji, wykonaj następujące kroki hello:
    
    ![Single Sign-On ustawienia](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On ustawienia")
    
    a. Wybierz **SAML włączone**.

    b. Kliknij przycisk **Nowy**.

13. Na powitania **SAML pojedynczego logowania jednokrotnego ustawienie Edytuj** okna dialogowego, wykonaj następujące kroki hello:
    
    ![SAML pojedynczy znak na ustawienie](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML pojedynczy znak na ustawienie")
    
    a. W hello **nazwa** tekstowym, wpisz nazwę dla danej konfiguracji.

    b. W **wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.

    c. W hello **identyfikator jednostki** pole tekstowe, typ`https://salesforce-jobscience.com`

    d. Kliknij przycisk **Przeglądaj** tooupload certyfikat usługi Azure AD.

    e. Jako **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera hello identyfikator federacyjnej z obiektu użytkownika hello**.

    f. Jako **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentfier hello hello instrukcji podmiotu**.

    g. W **adresu URL logowania do dostawcy tożsamości** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.

    h. W **adres URL wylogowania dostawcy tożsamości** pole tekstowe, Wklej wartość hello **Sign-Out adres URL**, które zostały skopiowane z portalu Azure.

    i. Kliknij pozycję **Zapisz**.

14. W okienku nawigacji po lewej stronie powitania w hello **Administruj** , kliknij przycisk **Zarządzanie domenami** tooexpand hello powiązanych sekcji, a następnie kliknij przycisk **Moje domeny** tooopen hello  **Mojej domeny** strony. 
    
    ![Mojej domeny](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mojej domeny")

15. Na powitania **Moje domeny** strony w hello **znakowanie strony logowania** kliknij **Edytuj**.
    
    ![Znakowanie strony logowania](./media/active-directory-saas-jobscience-tutorial/ic767826.png "znakowanie strony logowania")

16. Na powitania **znakowanie strony logowania** strony w hello **usługi uwierzytelniania** sekcji, hello nazwę Twojej **ustawienia logowania jednokrotnego SAML** jest wyświetlany. Wybierz go, a następnie kliknij przycisk **zapisać**.
    
    ![Znakowanie strony logowania](./media/active-directory-saas-jobscience-tutorial/ic784366.png "znakowanie strony logowania")

17. tooget hello SP zainicjował jednokrotnego kliknij adres URL logowania na powitania **ustawień rejestracji jednokrotnej** w hello **kontroli bezpieczeństwa** części menu.

    ![Opcje zabezpieczeń](./media/active-directory-saas-jobscience-tutorial/ic784368.png "środki zabezpieczające.")
    
    Kliknij profil rejestracji Jednokrotnej hello, utworzony w poprzednim kroku hello. Na tej stronie znajduje hello rejestracji jednokrotnej adres URL dla Twojej firmy (na przykład [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).    

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-jobscience-test-user"></a>Tworzenie użytkownika testowego Jobscience

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w tooJobscience muszą mieć przydzielone do Jobscience. W przypadku hello Jobscience Inicjowanie obsługi to zadanie ręczne.

>[!NOTE]
>Możesz użyć innych Jobscience użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Jobscience usługi Azure Active Directory kont użytkowników.
>  
        
**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. Zaloguj się za tooyour **Jobscience** witryny firmy jako administrator.

2. Przejdź tooSetup.
   
   ![Instalator](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Instalatora")
3. Przejdź za**Zarządzanie użytkownikami \> użytkowników**.
   
   ![Użytkownicy](./media/active-directory-saas-jobscience-tutorial/ic784369.png "użytkowników")
4. Kliknij przycisk **nowego użytkownika**.
   
   ![Wszyscy użytkownicy](./media/active-directory-saas-jobscience-tutorial/ic784370.png "wszyscy użytkownicy")
5. Na powitania **Edytowanie użytkownika** okna dialogowego, wykonaj następujące kroki hello:
   
   ![Edycja użytkownika](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Edycja użytkownika")
   
   a. W hello **imię** tekstowym, wpisz imię użytkownika hello, takich jak Britta.
   
   b. W hello **nazwisko** tekstowym, wpisz nazwisko użytkownika hello, takich jak Simona.
   
   c. W hello **Alias** tekstowym, wpisz nazwę aliasu hello użytkownika, takich jak brittas.

   d. W hello **E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.

   e. W hello **nazwy użytkownika** tekstowym, wpisz nazwę użytkownika użytkownika, takich jak Brittasimon@contoso.com.

   f. W hello **pseudonim** tekstowym, wpisz nazwę użytkownika, takich jak Simona nick.

   g. Kliknij pozycję **Zapisz**.

    
> [!NOTE]
> Właściciel konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail i następuje tooconfirm łącze swojego konta, zanim staje się aktywny.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooJobscience.

![Przypisz użytkownika][200] 

**tooassign tooJobscience Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Jobscience**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Jobscience hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Jobscience aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

