---
title: 'Samouczek: Integracji Azure Active Directory z Bynder | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>Samouczek: Integracji Azure Active Directory z Bynder
Celem Hello tego samouczka jest tooshow należy jak toointegrate Bynder w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Bynder zapewnia hello następujące korzyści:

* Można kontrolować w usłudze Azure AD, kto ma dostęp do tooBynder
* Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBynder rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD
* Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne
tooconfigure integracji z usługą Azure AD z Bynder należy hello następujące elementy:

* Subskrypcję usługi Azure AD
* Subskrypcja włączone Bynder jednokrotnego (SSO)

>[!NOTE]
>tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego. 
> 

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

* Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
* Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
Celem Hello tego samouczka jest tooenable możesz tootest Usługa rejestracji Jednokrotnej w Microsoft Azure AD w środowisku testowym.

Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Bynder z galerii hello
2. Konfigurowanie i testowania Usługa rejestracji Jednokrotnej w Microsoft Azure AD

## <a name="add-bynder-from-hello-gallery"></a>Dodaj Bynder z galerii hello
tooconfigure hello integracji Bynder do usługi Azure AD, należy tooadd Bynder z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Bynder z galerii hello, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**. 
   
    ![Usługa Active Directory][1]
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Aplikacje][2]
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Aplikacje][3]
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
    ![Aplikacje][4]
6. W polu wyszukiwania hello wpisz **Bynder**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. W panelu wyników hello, wybierz **Bynder**, a następnie kliknij przycisk **Complete** tooadd hello aplikacji.
   
    ![Wybieranie aplikacji hello w galerii hello](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Konfiguracja i testowanie Usługa rejestracji Jednokrotnej w Microsoft Azure AD
Celem Hello w tej sekcji jest tooshow użytkownika jak tooconfigure i testowania programu Microsoft Azure AD usługa rejestracji Jednokrotnej z Bynder na podstawie użytkownika testowego o nazwie "Britta Simona".

Aby toowork logowania jednokrotnego usługi Azure AD musi tooknow jest odpowiednikiem hello użytkownika w Bynder tooan użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Bynder musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Bynder.

tooconfigure i testowania programu Microsoft Azure AD usługa rejestracji Jednokrotnej z Bynder, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Microsoft Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Microsoft Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Bynder](#creating-a-bynder-test-user)**  -toohave odpowiednikiem Simona Britta w Bynder, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable toouse Simona Britta usługi Microsoft Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-microsoft-azure-ad-sso"></a>Konfigurowanie logowania jednokrotnego usługi AD platformy Microsoft Azure
W tej sekcji można włączyć Usługa rejestracji Jednokrotnej w Microsoft Azure AD w klasycznym portalu hello i skonfigurować logowanie Jednokrotne w aplikacji Bynder.

**tooconfigure programu Microsoft Azure AD usługa rejestracji Jednokrotnej z Bynder, wykonaj następujące kroki hello:**

1. W klasycznym portalu hello na powitania **Bynder** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne** okna dialogowego.
   
    ![Konfigurowanie rejestracji jednokrotnej][6] 
2. Na powitania **jak ma toosign użytkowników na tooBynder** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. Na powitania **Konfigurowanie ustawień aplikacji** strony okna dialogowego, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb**, wykonaj następujące kroki hello i kliknij przycisk **dalej**:
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. Kliknij przycisk **Dalej**.
4. Jeśli chcesz, aby aplikacja hello tooconfigure w **SP zainicjował tryb** na powitania **Konfigurowanie ustawień aplikacji** strony okna dialogowego, a następnie kliknij polecenie hello **"Pokaż zaawansowane ustawienia (opcjonalnie)"**, a następnie wprowadź hello **na adres URL logowania** i kliknij przycisk **dalej**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. W hello **na adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.getbynder.com/login/`
  2. Kliknij przycisk **Dalej**.
  
   >[!NOTE]
   >wartość Hello hello na adres URL logowania, w tym samouczku jest po prostu placeholfer. tooget hello rzeczywiste vlaue dla danego środowiska, skontaktuj się z Bynder.
   >

5. Na powitania **skonfigurować logowanie jednokrotne w Bynder** , wykonaj następujące kroki hello i kliknij przycisk **dalej**:
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. Kliknij przycisk **pobierania metadanych**, a następnie zapisz plik hello na tym komputerze.
  2. Kliknij przycisk **Dalej**.
6. tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, skontaktuj się z zespołem pomocy technicznej Bynder. Dołącz plik metadanych pobranych hello i udostępniać je tooset zespołu Bynder się rejestracji Jednokrotnej w bok.
7. W portalu klasycznym hello, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.
   
    ![Azure AD rejestracji jednokrotnej][10]
8. Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.  
   
    ![Azure AD rejestracji jednokrotnej][11]

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu klasycznym hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][20]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. Jako typ użytkownika wybierz nowego użytkownika w organizacji.
  2. W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.
  3. Kliknij przycisk **Dalej**.
6. Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. W hello **imię** pole tekstowe, typ **Britta**.  
  2. W hello **nazwisko** pole tekstowe, typ **Simona**. 
  3. W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.
  4. W hello **roli** listy, wybierz **użytkownika**.
  5. Kliknij przycisk **Dalej**.
7. Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. Zanotuj wartość hello hello **nowe hasło**.
   2. Kliknij przycisk **Complete** (Zakończ).   

### <a name="create-a-bynder-test-user"></a>Tworzenie użytkownika testowego Bynder
Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Bynder. Bynder obsługę w czasie, który jest domyślnie włączone.

Nie ma elementu akcji można w tej sekcji. Nowy użytkownik zostanie utworzony podczas próby tooaccess Bynder, jeśli go jeszcze nie istnieje.

>[!NOTE]
>Należy ręcznie toocreate użytkownika, należy najpierw toocontact hello Bynder z pomocą techniczną. 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD
Celem Hello w tej sekcji jest tooenabling toouse Simona Britta Azure logowania jednokrotnego, przyznając jej tooBynder dostępu.

   ![Przypisz użytkownika][200]

**tooassign tooBynder Simona Britta wykonaj hello następujące kroki:**

1. W portalu klasycznym hello, kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Przypisz użytkownika][201]
2. Z listy aplikacji hello wybierz **Bynder**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. W menu hello na górze hello, kliknij przycisk **użytkowników**.
   
    ![Przypisz użytkownika][203]
4. Na liście hello użytkowników, wybierz **Simona Britta**.
5. W narzędzi hello na dole powitania kliknij **przypisać**.
   
    ![Przypisz użytkownika][205]

### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej
Celem Hello w tej sekcji jest tootest Twojego systemu Microsoft Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Bynder hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Bynder aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
