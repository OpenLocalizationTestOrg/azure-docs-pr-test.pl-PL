---
title: 'Samouczek: Integracji Azure Active Directory z Wizergos oprogramowanie | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Wizergos wydajności oprogramowania."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a>Samouczek: Integracji Azure Active Directory z Wizergos wydajności oprogramowania
Celem Hello tego samouczka jest tooshow należy jak toointegrate Wizergos wydajności oprogramowania w usłudze Azure Active Directory (Azure AD).

Integrowanie Wizergos wydajności oprogramowania z usługi Azure AD zapewnia hello następujące korzyści:

* Można kontrolować w usłudze Azure AD, kto ma dostęp tooWizergos oprogramowanie
* Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWizergos oprogramowanie rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD
* Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne
tooconfigure integracji usługi Azure AD z oprogramowaniem wydajność Wizergos należy hello następujące elementy:

* Subskrypcję usługi Azure AD
* Subskrypcja Wizergos wydajności oprogramowania logowanie Jednokrotne włączone

>[!NOTE]
>tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego. 
> 

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

* Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
* Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
Celem Hello tego samouczka jest tooenable możesz tootest logowania jednokrotnego programu Azure AD w środowisku testowym.

Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Wizergos oprogramowanie z galerii hello
2. Konfigurowanie i testowania logowania jednokrotnego programu Azure AD

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a>Dodawanie Wizergos oprogramowanie z galerii hello
tooconfigure hello integracji Wizergos wydajności oprogramowania do usługi Azure AD, należy tooadd Wizergos wydajności oprogramowania z listy tooyour galerii hello zarządzanych aplikacji SaaS.

**tooadd Wizergos oprogramowanie z galerii hello wykonaj hello następujące kroki:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**. 
   
    ![Usługa Active Directory][1]
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Aplikacje][2]
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Aplikacje][3]
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
    ![Aplikacje][4]
6. W polu wyszukiwania hello wpisz **Wizergos oprogramowanie**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. W panelu wyników hello, wybierz **Wizergos wydajności oprogramowania**, a następnie kliknij przycisk **Complete** tooadd hello aplikacji.
   
    ![Wybieranie aplikacji hello w galerii hello](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a>Konfiguracja i testowanie logowania jednokrotnego programu Azure AD
Celem Hello w tej sekcji jest tooshow użytkownika jak tooconfigure i testowania Azure AD z logowania jednokrotnego przy użyciu Wizergos wydajności oprogramowania na podstawie użytkownika testowego o nazwie "Britta Simona".

Dla toowork logowania jednokrotnego usługi Azure AD musi tooknow jest użytkownika odpowiednikiem hello w Wizergos oprogramowanie tooan użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi Wizergos wydajności oprogramowania musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** Wizergos wydajności oprogramowania.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z BynWizergos Softwareder wydajności, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego oprogramowanie Wizergos](#creating-a-wizergos-productivity-software-test-user)**  -toohave odpowiednikiem Simona Britta Wizergos wydajności oprogramowania, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-sso"></a>Konfigurowanie usługi Azure AD logowania jednokrotnego.
W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu klasycznym hello i skonfigurować rejestracji jednokrotnej w aplikacji Wizergos wydajności oprogramowania.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Wizergos oprogramowanie, wykonaj hello następujące kroki:**

1. W klasycznym portalu hello na powitania **oprogramowanie Wizergos** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne**okna dialogowego.
   
    ![Konfigurowanie rejestracji jednokrotnej][6] 
2. Na powitania **jak ma toosign użytkowników na tooWizergos oprogramowanie** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**:
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. Na powitania **Konfigurowanie ustawień aplikacji** strony okna dialogowego, kliknij przycisk **dalej**:
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. Na powitania **skonfigurować logowanie jednokrotne w oprogramowanie Wizergos** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik hello na tym komputerze:
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour Wizergos oprogramowanie dzierżawy z uprawnieniami administratora.
6. Wybierz z hello hamburger menu **Admin**.
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. Na stronie Administracja w menu po lewej stronie wybierz **uwierzytelniania** i wybierz polecenie **usługi Azure AD**.
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. Wykonaj następujące kroki powitania **uwierzytelniania** sekcji.
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. Kliknij przycisk **przekazać** hello tooupload przycisk pobrać certyfikatu z usługi Azure AD. 
  2. W hello **adres URL wystawcy** pole tekstowe umieścić wartość hello **adres URL wystawcy** z Kreatora konfiguracji aplikacji usługi Azure AD.
  3. W hello **URL rejestracji jednokrotnej** pole tekstowe umieścić wartość hello **pojedynczy znak na adres URL usługi** z Kreatora konfiguracji aplikacji usługi Azure AD.
  4. W hello **pojedynczego adresu URL Sign-Out** pole tekstowe umieścić wartość hello **pojedynczy adres URL usługi Sign-out** z Kreatora konfiguracji aplikacji usługi Azure AD.
  5. Kliknij przycisk **zapisać** przycisku.
9. W portalu klasycznym hello, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.
   
    ![Azure AD rejestracji jednokrotnej][10]
10. Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.  
    
    ![Azure AD rejestracji jednokrotnej][11]

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu klasycznym hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][20]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. Jako typ użytkownika wybierz nowego użytkownika w organizacji.
  2. W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.
  3. Kliknij przycisk **Dalej**.
6. Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. W hello **imię** pole tekstowe, typ **Britta**.  
  2. W hello **nazwisko** pole tekstowe, typ **Simona**.
  3. W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.
  4. W hello **roli** listy, wybierz **użytkownika**.
  5. Kliknij przycisk **Dalej**.
7. Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. Zanotuj wartość hello hello **nowe hasło**.
  2. Kliknij przycisk **Complete** (Zakończ).   

### <a name="create-a-wizergos-productivity-software-test-user"></a>Tworzenie użytkownika testowego Wizergos wydajności oprogramowania
W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Wizergos wydajności oprogramowania. Proszę współpracować z zespołem pomocy technicznej Wizergos wydajności oprogramowania za pomocą [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd hello użytkowników hello Wizergos wydajności oprogramowania platformy.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD
Celem Hello w tej sekcji jest tooenabling toouse Simona Britta logowania jednokrotnego Azure przyznać jej dostęp tooWizergos wydajności oprogramowania.

  ![Przypisz użytkownika][200]

**tooassign tooWizergos Simona Britta oprogramowanie, wykonaj hello następujące kroki:**

1. W portalu klasycznym hello, kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Przypisz użytkownika][201]
2. Z listy aplikacji hello wybierz **Wizergos oprogramowanie**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. W menu hello na górze hello, kliknij przycisk **użytkowników**.
   
    ![Przypisz użytkownika][203]
4. Na liście hello użytkowników, wybierz **Simona Britta**.
5. W narzędzi hello na dole powitania kliknij **przypisać**.
   
    ![Przypisz użytkownika][205]

### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej
Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.

Po kliknięciu kafelka oprogramowanie Wizergos hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Wizergos wydajność aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
