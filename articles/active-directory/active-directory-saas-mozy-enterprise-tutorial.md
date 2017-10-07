---
title: "Samouczek: Integrację usługi Azure Active Directory ze Mozy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Mozy Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a>Samouczek: Integrację usługi Azure Active Directory ze Mozy

Z tego samouczka, dowiesz się, jak toointegrate Mozy przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).

Integrowanie Mozy organizacji z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMozy przedsiębiorstwa
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMozy przedsiębiorstwa (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z Mozy Enterprise należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Mozy Enterprise logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Mozy przedsiębiorstwa z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-mozy-enterprise-from-hello-gallery"></a>Dodawanie Mozy przedsiębiorstwa z galerii hello
tooconfigure hello integracji Mozy przedsiębiorstwa w usłudze Azure Active Directory, należy tooadd Mozy przedsiębiorstwa z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Mozy przedsiębiorstwa z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Mozy Enterprise**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. W panelu wyników hello, wybierz **Mozy Enterprise**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Mozy przedsiębiorstwa w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w przedsiębiorstwie Mozy jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w przedsiębiorstwie Mozy musi toobe ustanowione.

W przedsiębiorstwie Mozy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Mozy przedsiębiorstwa, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  -toohave odpowiednikiem Simona Britta w przedsiębiorstwie Mozy, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować rejestracji jednokrotnej w aplikacji Mozy przedsiębiorstwa.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Mozy przedsiębiorstwa, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **Mozy Enterprise** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. Na powitania **Mozy domeny przedsiębiorstwa i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.Mozyenterprise.com`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta Enterprise Mozy](http://support.mozy.com/) tooget tej wartości.

4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracja dla przedsiębiorstw Mozy** , kliknij przycisk **skonfigurować Mozy Enterprise** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Mozy Enterprise jako administrator.

8. W hello **konfiguracji** kliknij **zasady uwierzytelniania**.
   
   ![Zasady uwierzytelniania](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "zasady uwierzytelniania")

9. Na powitania **zasady uwierzytelniania** sekcji, wykonaj następujące kroki hello:
   
   ![Zasady uwierzytelniania](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "zasady uwierzytelniania")
   
   a. Wybierz **usługi katalogowej** jako **dostawcy**.
   
   b. Wybierz **wypychania LDAP**.
   
   c. Kliknij przycisk hello **uwierzytelnianie SAML** kartę.
   
   d. Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z hello portalu Azure do hello **adres URL uwierzytelniania** pola tekstowego.
   
   e. Wklej **SAML identyfikator jednostki**, która została skopiowana z hello portalu Azure do hello **punktu końcowego SAML** pole tekstowe.
   
   f. Otwórz pobrany zakodowanego certyfikatu base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej hello cały certyfikat do **certyfikatu SAML** pola tekstowego.
   
   g. Wybierz **włączenia logowania jednokrotnego dla administratorów toolog się przy użyciu swoich poświadczeń sieciowych**.
   
   h. Kliknij przycisk **zapisać zmiany**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-mozy-enterprise-test-user"></a>Tworzenie użytkownika testowego Mozy przedsiębiorstwa

W kolejności tooenable usługi Azure AD użytkownicy toolog Mozy w przedsiębiorstwie musi być zainicjowana Mozy w przedsiębiorstwie. W przypadku hello Mozy przedsiębiorstwa Inicjowanie obsługi to zadanie ręczne.

>[!NOTE]
>Możesz użyć innych Mozy Enterprise użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Mozy Enterprise kont użytkowników usługi AAD.

**tooprovision kont użytkowników, wykonaj hello następujące kroki:**

1. Zaloguj się za tooyour **Mozy Enterprise** dzierżawy.

2. Kliknij przycisk **użytkowników**, a następnie kliknij przycisk **Dodaj nowego użytkownika**.
   
   ![Użytkownicy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "użytkowników")
   
   >[!NOTE]
   >Witaj **Dodaj nowego użytkownika** tylko wtedy, gdy tylko jest wyświetlana opcja **Mozy** został wybrany jako dostawca hello w obszarze **zasady uwierzytelniania**. Jeśli skonfigurowano uwierzytelnianie SAML, następnie hello użytkownicy są automatycznie dodawane na ich pierwsze logowanie za pomocą rejestracji jednokrotnej w.
    
3. Witaj nowego okna dialogowego użytkowników i wykonywanie hello następujące kroki:
   
   ![Dodawanie użytkowników](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Dodawanie użytkowników")
   
   a. Z hello **wybierz grupę** listy, wybierz grupę.
   
   b. Z hello **jakiego rodzaju użytkownika** listy, wybierz typ.
   
   c. W hello **Username** pole tekstowe, nazwa typu hello użytkownika hello Azure AD.
   
   d. W hello **E-mail** pole tekstowe, typ hello adres e-mail użytkownika hello Azure AD.
   
   e. Wybierz **wysyłania wiadomości e-mail z instrukcją użytkownika**.
   
   f. Kliknij przycisk **dodać użytkowników**.

     >[!NOTE]
     > Po utworzeniu użytkownika hello, wiadomości e-mail będą wysyłane toohello użytkownika usługi Azure AD, który zawiera konto hello tooconfirm łącza, zanim staje się aktywny.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMozy przedsiębiorstwa.

![Przypisz użytkownika][200] 

**tooassign Simona Britta tooMozy przedsiębiorstwa, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Mozy Enterprise**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello Mozy Enterprise kafelka w hello Panel dostępu, należy pobrać strony logowania organizacji Mozy aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

