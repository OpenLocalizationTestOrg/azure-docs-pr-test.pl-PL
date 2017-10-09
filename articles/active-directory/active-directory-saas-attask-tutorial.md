---
title: 'Samouczek: Integracji Azure Active Directory z @Task| Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a>Samouczek: Integracji Azure Active Directory z@Task
Celem Hello tego samouczka jest tooshow należy jak toointegrate @Task z usługą Azure Active Directory (Azure AD).  
Integrowanie @Task z usługą Azure AD zapewnia hello następujące korzyści: 

* Można kontrolować w usłudze Azure AD, który ma dostęptoo@Task
* Umożliwia użytkownikom uzyskać tooautomatically zalogowane too@Task (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
* Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne
Integracja tooconfigure usługi Azure AD z @Task, potrzebujesz hello następujące elementy:

* Subskrypcję usługi Azure AD
* @Task Jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.
> 
> 

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

* Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
* Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Opis scenariusza
Celem Hello tego samouczka jest tooenable możesz tootest usługi Azure AD rejestracji jednokrotnej w środowisku testowym.  
Scenariusz Hello opisane w tym samouczku składa się z trzech głównych bloków konstrukcyjnych:

1. Dodawanie @Task z galerii hello 
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-task-from-hello-gallery"></a>Dodawanie @Task z galerii hello
Integracja hello tooconfigure @Task do usługi Azure AD, należy tooadd @Task z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd @Task z galerii hello wykonywać hello następujące kroki:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**. 
   
    ![Usługa Active Directory][1] 
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Aplikacje][2] 
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Aplikacje][3] 
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
    ![Aplikacje][4] 
6. W polu wyszukiwania hello wpisz  **@Task** .
   
    ![Aplikacje][5] 
7. Wybierz w okienku wyników hello  **@Task** , a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
    ![Aplikacje][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
Witaj celem tej sekcji jest tooshow należy jak pojedynczy tooconfigure i testowych usługi Azure AD logowania z @Task w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork, usługi Azure AD wymaga tooknow użytkownika odpowiednikiem hello w @Task jest tooan użytkownika w usłudze Azure AD. Innymi słowy, relacja linku między użytkownika usługi Azure AD i hello użytkownikowi w @Task musi toobe ustanowione.   
Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w @Task.

tooconfigure i testowych usługi Azure AD logowanie jednokrotne z @Task, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie @Tasktest użytkownika](#creating-a-halogen-software-test-user)**  -toohave a odpowiednikiem Simona Britta w @Taskthat jej reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej
Celem Hello w tej sekcji jest tooenable usługi Azure AD rejestracji jednokrotnej w hello klasycznego portalu Azure i tooconfigure rejestracji jednokrotnej w sieci @Task aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z @Task, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure na powitania  **@Task**  strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne**  okno dialogowe.
   
    ![Konfigurowanie rejestracji jednokrotnej][6] 
2. Na powitania **jak ma toosign użytkowników na too@Task**  wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Azure AD rejestracji jednokrotnej][7] 
3. Na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj hello następujące kroki:
   
    ![Konfiguruj ustawienia aplikacji][8] 
   
     a. W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używane przez użytkowników z toosign na tooyour @Task aplikacji (np.:*https://<Tenant name>.attask ondemand.com*).
   
     b. Kliknij przycisk **Dalej**.
4. Na powitania **skonfigurować logowanie jednokrotne w @Task**  kliknij przycisk **pobierania metadanych**, Zapisz plik metadanych hello lokalnie na komputerze, a następnie kliknij przycisk **dalej**.
   
    ![Co to jest program Azure AD Connect][9] 
5. Logowania jednokrotnego tooyour @Task witryny firmy jako administrator.
6. Przejdź za**pojedynczy znak w konfiguracji**.
7. Na powitania **rejestracji jednokrotnej** okna dialogowego, wykonaj następujące kroki hello
   
    ![Konfigurowanie rejestracji jednokrotnej][23]
   
    a. Jako **typu**, wybierz pozycję **SAML 2.0**.
   
    b. Wybierz **usługi identyfikator dostawcy**.
   
    c. Na powitania klasycznego portalu Azure, skopiuj hello **zdalnego adresu URL logowania**i wklej go do hello **adresu URL logowania do portalu** pola tekstowego.
   
    d. Na powitania klasycznego portalu Azure, skopiuj hello **pojedynczy adres URL usługi Sign-Out**, a następnie wklej go do hello **Sign-Out URL** pola tekstowego.
   
    e. Hello klasycznego portalu Azure, skopiuj hello **Zmień adres URL hasła**, a następnie wklej go do hello **Zmień adres URL hasła** pole tekstowe.
   
    f. Kliknij pozycję **Zapisz**.
8. Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**. 
   
    ![Co to jest program Azure AD Connect][10]
9. Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.  
   
    ![Co to jest program Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego w hello klasycznego portalu Azure o nazwie Simona Britta.  

![Tworzenie użytkowników usługi Azure AD][20]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**. 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki: 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    a. Jako typ użytkownika wybierz nowego użytkownika w organizacji.
   
    b. W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.
   
    c. Kliknij przycisk **Dalej**.
6. Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki: 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    a. W hello **imię** pole tekstowe, typ **Britta**.  
   
    b. W hello **nazwisko** pole tekstowe, typ **Simona**.
   
    c. W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.
   
    d. W hello **roli** listy, wybierz **użytkownika**.

    e. Kliknij przycisk **Dalej**.

7. Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    a. Zanotuj wartość hello hello **nowe hasło**.
   
    b. Kliknij przycisk **Complete** (Zakończ).   

### <a name="creating-an-task-test-user"></a>Tworzenie @Task użytkownika testowego
Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w @Task.

**toocreate użytkownika o nazwie Simona Britta w @Task, wykonaj następujące kroki hello:**

1. Zaloguj się na tooyour @Task witryny firmy jako administrator.
2. W menu hello na górze hello, kliknij przycisk **osób**.
3. Kliknij przycisk **nowej osoby**. 
4. W oknie dialogowym nowej osoby hello wykonaj następujące kroki hello:
   
    ![Utwórz @Task użytkownika testowego][21] 
   
    a. W hello **imię** tekstowym, wpisz "Britta".
   
    b. W hello **nazwisko** tekstowym, wpisz "Simona".
   
    c. W hello **adres E-mail** tekstowym, wpisz adres e-mail Simona Britta w usłudze Azure Active Directory.
   
    d. Kliknij przycisk **Dodaj osobę**.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD
Celem Hello w tej sekcji jest tooenabling toouse Simona Britta Azure rejestracji jednokrotnej przez udostępnienie jej too@Task.

![Przypisz użytkownika][200] 

**tooassign Simona Britta too@Task, wykonaj następujące kroki hello:**

1. Na hello Azure kliknij klasycznego portalu, widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Przypisz użytkownika][201] 
2. Z listy aplikacji hello wybierz  **@Task** .
   
    ![Przypisz użytkownika][202] 
3. W menu hello na górze hello, kliknij przycisk **użytkowników**.
   
    ![Przypisz użytkownika][203] 
4. Na liście hello użytkowników, wybierz **Simona Britta**.
5. W narzędzi hello na dole powitania kliknij **przypisać**.
   
    ![Przypisz użytkownika][205]

### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej
Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.  
Po kliknięciu hello @Task kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour @Task aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






