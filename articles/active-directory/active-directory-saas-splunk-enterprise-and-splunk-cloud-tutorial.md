---
title: "Samouczek: Integracji usługi Azure Active Directory z Splunk przedsiębiorstwa i w chmurze Splunk | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługi Azure Active Directory i Splunk Enterprise i Splunk chmury."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a>Samouczek: Integracji usługi Azure Active Directory z Splunk przedsiębiorstwa i w chmurze Splunk

Z tego samouczka, dowiesz się, jak toointegrate Splunk przedsiębiorstwa i w chmurze Splunk w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Splunk przedsiębiorstwa i w chmurze Splunk zapewnia hello następujące korzyści:

- TooSplunk Enterprise i Splunk chmury można kontrolować w usłudze Azure AD, który ma dostęp
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSplunk przedsiębiorstwa i w chmurze Splunk rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z Splunk przedsiębiorstwa i w chmurze Splunk należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Splunk Enterprise lub logowania jednokrotnego chmury Splunk włączone subskrypcji


>[!NOTE]
>tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.
>

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.

Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Splunk przedsiębiorstwa i w chmurze Splunk z galerii hello
2. Konfigurowanie i testowania logowania jednokrotnego programu Azure AD


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a>Dodaj Splunk przedsiębiorstwa i w chmurze Splunk z galerii hello
tooconfigure hello integracji przedsiębiorstwa Splunk i Splunk chmury do usługi Azure AD, potrzebujesz tooadd Splunk przedsiębiorstwa oraz Splunk chmury hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Splunk przedsiębiorstwa i w chmurze Splunk z galerii hello wykonaj hello następujące kroki:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.

    ![Usługa Active Directory][1]

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.

    ![Aplikacje][2]

4. Kliknij przycisk **Dodaj** u dołu hello hello strony.

    ![Aplikacje][3]

5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.

    ![Aplikacje][4]

6. W polu wyszukiwania hello wpisz **Splunk przedsiębiorstwa lub w chmurze Splunk**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. Wybierz w okienku wyników hello **Splunk przedsiębiorstwa i w chmurze Splunk**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Splunk przedsiębiorstwa i Splunk chmury oparte na użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jakie hello odpowiednikiem użytkownik w organizacji Splunk i w chmurze Splunk jest tooa w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w organizacji Splunk i w chmurze Splunk musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **nazwy użytkownika** Splunk przedsiębiorstwa i Splunk chmury.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Splunk przedsiębiorstwa i w chmurze Splunk, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Splunk przedsiębiorstwa i w chmurze Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave odpowiednikiem Simona Britta w przedsiębiorstwie Splunk i w chmurze Splunk, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji włączenia funkcji logowania jednokrotnego usługi Azure AD w klasycznym portalu hello i konfigurowanie logowania jednokrotnego w aplikacji przedsiębiorstwa Splunk i Splunk chmury.


**tooconfigure usługi Azure AD rejestracji jednokrotnej z Splunk przedsiębiorstwa i Splunk chmury, wykonaj hello następujące kroki:**

1. W klasycznym portalu hello na powitania **Splunk przedsiębiorstwa i w chmurze Splunk** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne** okna dialogowego.
     
    ![Konfigurowanie rejestracji jednokrotnej][6] 

2. Na powitania **jak chcesz toosign użytkowników na tooSplunk przedsiębiorstwa i w chmurze Splunk** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. Na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj hello następujące kroki:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używane przez użytkowników na toosign tooyour Splunk przedsiębiorstwa i aplikacji w chmurze Splunk przy użyciu hello następującego wzorca:`https://<splunkserverUrl>/en-US/app/launcher/home`
  2. W hello **identyfikator** pole tekstowe, wprowadź adres URL powitania serwera Splunk.
  3. W hello **adres URL odpowiedzi** pole tekstowe, wprowadź adres URL hello z hello następującego wzorca:`https://<splunkserver>/saml/acs`
  4. Kliknij przycisk **Dalej**.
 
4. Na powitania **skonfigurować logowanie jednokrotne w Splunk przedsiębiorstwa i w chmurze Splunk** wykonaj hello następujące kroki:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. Kliknij przycisk **pobierania metadanych**, a następnie zapisz plik hello na tym komputerze.
  2. Kliknij przycisk **Dalej**.

5. tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, skontaktuj się z Splunk przedsiębiorstwa i Splunk chmury z pomocą techniczną i podaj następujące hello:

    * Witaj pobrane **federaton metadanych**
6. W portalu klasycznym hello, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.
    
    ![Azure AD rejestracji jednokrotnej][10]

7. Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.  
 
    ![Azure AD rejestracji jednokrotnej][11]

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
W tej sekcji Tworzenie użytkownika testowego w portalu klasycznym hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][20]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. Jako typ użytkownika wybierz nowego użytkownika w organizacji.
  2. W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.
  3. Kliknij przycisk **Dalej**.

6.  Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:
  
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. W hello **imię** pole tekstowe, typ **Britta**.  
  2. W hello **nazwisko** pole tekstowe, typ **Simona**.
  3. W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.
  4. W hello **roli** listy, wybierz **użytkownika**.
  5. Kliknij przycisk **Dalej**.

7. Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. Zanotuj wartość hello hello **nowe hasło**.
  2. Kliknij przycisk **Complete** (Zakończ).   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a>Tworzenie Splunk przedsiębiorstwa i chmury Splunk użytkownika testowego

W tej sekcji utworzysz użytkownika o nazwie Simona Britta w przedsiębiorstwie Splunk i Splunk chmury. We współpracy z Splunk przedsiębiorstwa i w chmurze Splunk pomocy technicznej zespół tooadd hello użytkowników w hello Splunk Enterprise Splunk platforma i chmury.


### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji można włączyć toouse Simona Britta SSOy Azure udzielanie jej Enterprise tooSplunk dostępu i Splunk chmury.

![Przypisz użytkownika][200] 

**tooassign Simona Britta tooSplunk przedsiębiorstwa i Splunk chmury, wykonaj hello następujące kroki:**

1. W portalu klasycznym hello, kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Splunk przedsiębiorstwa i w chmurze Splunk**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. W menu hello na górze hello, kliknij przycisk **użytkowników**.

    ![Przypisz użytkownika][203]

4. Na liście hello użytkowników, wybierz **Simona Britta**.

5. W narzędzi hello na dole powitania kliknij **przypisać**.

    ![Przypisz użytkownika][205]

### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować programu Azure AD SSOonfiguration, przy użyciu hello panelu dostępu.

Po kliknięciu hello Splunk przedsiębiorstwa i chmury Splunk kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Splunk przedsiębiorstwa i w chmurze Splunk aplikacji.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
