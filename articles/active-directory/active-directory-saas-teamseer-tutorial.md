---
title: 'Samouczek: Integracji Azure Active Directory z TeamSeer | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i TeamSeer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 876d13e446115acd50b01c7f44db99357045e429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a>Samouczek: Integracji Azure Active Directory z TeamSeer

Z tego samouczka, dowiesz się, jak toointegrate TeamSeer w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD TeamSeer zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTeamSeer
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTeamSeer (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z TeamSeer należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- TeamSeer jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie TeamSeer z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-teamseer-from-hello-gallery"></a>Dodawanie TeamSeer z galerii hello
tooconfigure hello integracji TeamSeer w tooAzure AD, należy tooadd TeamSeer z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd TeamSeer z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **TeamSeer**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. W panelu wyników hello zaznacz **TeamSeer**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TeamSeer na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w TeamSeer jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w TeamSeer musi toobe ustanowione.

W TeamSeer, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z TeamSeer, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego TeamSeer](#creating-a-teamseer-test-user)**  -toohave odpowiednikiem Simona Britta w TeamSeer, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji TeamSeer.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z TeamSeer, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **TeamSeer** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. Na powitania **TeamSeer domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.teamseer.com/<companyid>`

    > [!NOTE] 
    > wartość Hello nie jest prawdziwe. Wartość hello aktualizacji z hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta TeamSeer](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget hello wartość. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji TeamSeer** kliknij **skonfigurować TeamSeer** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy TeamSeer tooyour jako administrator.

8. Przejdź za**HR Admin**.
   
    ![Administrator HR](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR administratora")

9. Kliknij przycisk **Instalatora**.
   
    ![Instalator](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Instalatora")

10. Kliknij przycisk **konfigurowanie szczegóły dostawcy SAML**.
   
    ![Ustawienia SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "ustawienia SAML")

11. W sekcji Szczegóły dostawcy SAML hello wykonaj hello następujące kroki:
   
    ![Ustawienia SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "ustawienia SAML")   

    a. Wklej hello **pojedynczy znak na adres URL usługi** wartość toohello **adres URL** pola tekstowego.
          
    b. Otwórz certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go w Schowku tooyour, a następnie wklej go toohello **certyfikatu publicznego IdP** pola tekstowego.

12. Witaj toocomplete SAML dostawcy konfiguracji, należy wykonać hello następujące kroki:
    
    ![Ustawienia SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "ustawienia SAML") 

    a. W hello **Test adresy E-mail**, wpisz adres e-mail użytkownika testowego hello. 
  
    b. W hello **wystawcy** pole tekstowe, typ hello adres URL wystawcy hello dostawcy usług. 
  
    c. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-teamseer-test-user"></a>Tworzenie użytkownika testowego TeamSeer

toolog użytkowników tooenable usługi Azure AD w tooTeamSeer, muszą mieć przydzielone w tooShiftPlanning. W przypadku hello TeamSeer Inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour **TeamSeer** witryny firmy jako administrator.

2. Wykonaj następujące kroki hello:
   
    ![Administrator HR](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR administratora")  
 
    a. Przejdź za**HR Admin \> użytkowników**.
  
    b. Kliknij przycisk **Uruchom Kreatora nowego użytkownika hello**.

3. W hello **szczegóły użytkownika** sekcji, wykonaj następujące kroki hello:
   
    ![Szczegóły użytkownika](./media/active-directory-saas-teamseer-tutorial/ic789641.png "szczegóły użytkownika")

    a. Typ hello **imię**, **nazwisko**, **nazwę użytkownika (adres E-mail)** z prawidłowego konta usługi AAD ma tooprovision w toohello związane z pól tekstowych.
  
    b. Kliknij przycisk **Dalej**.

4. Wykonaj hello na ekranie instrukcje dotyczące dodawania nowego użytkownika, a następnie kliknij przycisk **Zakończ**.

>[!NOTE]
>Możesz użyć innych TeamSeer użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez TeamSeer tooprovision kont użytkowników usługi Azure AD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTeamSeer.

![Przypisz użytkownika][200] 

**tooassign tooTeamSeer Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **TeamSeer**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

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



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

