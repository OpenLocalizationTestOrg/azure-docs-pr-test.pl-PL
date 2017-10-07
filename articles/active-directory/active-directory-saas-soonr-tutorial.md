---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy Soonr | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Soonr w miejscu pracy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a>Samouczek: Integracji Azure Active Directory z Soonr w miejscu pracy

Celem Hello tego samouczka jest tooshow należy jak toointegrate Soonr pracy z usługą Azure Active Directory (Azure AD).  
Integrowanie Soonr miejsca pracy z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooSoonr miejsca pracy
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSoonr pracy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z miejsca pracy Soonr należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Obszar roboczy Soonr jednokrotnego włączone subskrypcji


> [!NOTE] 
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.


tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Opis scenariusza
Celem Hello tego samouczka jest tooenable możesz tootest usługi Azure AD rejestracji jednokrotnej w środowisku testowym.  
Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie miejsca pracy Soonr z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne


## <a name="adding-soonr-workplace-from-hello-gallery"></a>Dodawanie miejsca pracy Soonr z galerii hello
tooconfigure hello integracji Soonr dołączanie do usługi Azure AD, należy tooadd Soonr miejsca pracy z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Soonr w miejscu pracy na powitania galerii, wykonaj hello następujące kroki:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**. 

    ![Usługa Active Directory][1]

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.

    ![Aplikacje][2]

4. Kliknij przycisk **Dodaj** u dołu hello hello strony.

    ![Aplikacje][3]

5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
 
    ![Aplikacje][4]

6. W polu wyszukiwania hello wpisz **pracy Soonr**.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. Wybierz w okienku wyników hello **Soonr w miejscu pracy**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
Celem Hello w tej sekcji jest tooshow użytkownika jak tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Soonr w miejscu pracy na podstawie użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jest odpowiednikiem hello użytkownika w miejscu pracy Soonr tooan użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w miejscu pracy Soonr musi toobe ustanowione.  

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w miejscu pracy Soonr.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Soonr w miejscu pracy, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego pracy Soonr](#creating-a-soonr-workplace-test-user)**  -toohave odpowiednikiem Simona Britta w miejscu pracy Soonr, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu klasycznym hello i skonfigurować logowanie jednokrotne w miejscu pracy Soonr aplikacji.


**tooconfigure usługi Azure AD rejestracji jednokrotnej z miejsca pracy Soonr, wykonaj hello następujące kroki:**

1. W hello klasycznego portalu Azure na powitania **pracy Soonr** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne**  okno dialogowe.

    ![Konfigurowanie rejestracji jednokrotnej][6] 

2. Na powitania **jak ma toosign użytkowników w miejscu pracy tooSoonr** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. Na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj następujące kroki hello:.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    a. W hello **na adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.

    b. Kliknij przycisk **Dalej**.

    > [!NOTE] 
    > Należy pamiętać, że nie jest hello rzeczywistą wartość. Masz tooupdate tej wartości z rzeczywistego hello Zaloguj się na adres URL. Skontaktuj się z tooget zespołu pomocy technicznej pracy Soonr tej wartości.

4. Na powitania **skonfigurować logowanie jednokrotne w miejscu pracy Soonr** kliknij przycisk **pobierania metadanych** , a następnie zapisz plik hello na tym komputerze:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, skontaktuj się z zespołem pomocy technicznej Soonr miejsca pracy i podaj następujący hello: 

    • hello pobrane **metadanych** pliku

    • hello **adres URL wystawcy**

    • hello **adres URL logowania jednokrotnego SAML**

    • hello **pojedynczy adres URL usługi Sign-Out**

    >[!NOTE]
    >Ta aplikacja została zastąpiona nowszą <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">pracy Autotask</a> i może odnosić się <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">to</a> samouczka do konfigurowania aplikacji hello z usługą Azure AD.
   
6. W hello klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.

    ![Azure AD rejestracji jednokrotnej][10]

7. Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.  
  
    ![Azure AD rejestracji jednokrotnej][11]



### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego w hello klasycznego portalu Azure o nazwie Simona Britta.  

![Tworzenie użytkowników usługi Azure AD][20]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    a. Jako typ użytkownika wybierz nowego użytkownika w organizacji.

    b. W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.

    c. Kliknij przycisk **Dalej**.

6.  Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    a. W hello **imię** pole tekstowe, typ **Britta**.  

    b. W hello **nazwisko** pole tekstowe, typ **Simona**.

    c. W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.

    d. W hello **roli** listy, wybierz **użytkownika**.

    e. Kliknij przycisk **Dalej**.

7. Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    a. Zanotuj wartość hello hello **nowe hasło**.

    b. Kliknij przycisk **Complete** (Zakończ).   



### <a name="creating-a-soonr-workplace-test-user"></a>Tworzenie użytkownika testowego Soonr w miejscu pracy

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w miejscu pracy Soonr. Należy skontaktować się z toocreate zespołu pomocy technicznej Soonr w miejscu pracy użytkownika hello platformy. Można zwiększyć hello biletu pomocy technicznej z Soonr z <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">tutaj</a>.


### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

Celem Hello w tej sekcji jest tooenabling toouse Simona Britta Azure rejestracji jednokrotnej, przyznając jej tooSoonr dostępu do miejsca pracy.

![Przypisz użytkownika][200] 

**tooassign tooSoonr Simona Britta miejsca pracy, należy wykonać hello następujące kroki:**

1. Na hello Azure kliknij klasycznego portalu, widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **pracy Soonr**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. W menu hello na górze hello, kliknij przycisk **użytkowników**.

    ![Przypisz użytkownika][203] 

1. Na liście hello użytkowników, wybierz **Simona Britta**.

2. W narzędzi hello na dole powitania kliknij **przypisać**.

    ![Przypisz użytkownika][205]



### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.  
Po kliknięciu hello pracy Soonr kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Soonr pracy aplikacji.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
