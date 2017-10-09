---
title: 'Samouczek: Azure Active Directory integracji z pakietem BPM Questetra | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>Samouczek: Azure Active Directory integracji z pakietem BPM Questetra
Celem Hello tego samouczka jest tooshow należy jak toointegrate Suite BPM Questetra w usłudze Azure Active Directory (Azure AD).  
Integracja z usługą Azure AD Questetra BPM Suite udostępnia hello następujące korzyści: 

* Można kontrolować w usłudze Azure AD, kto ma dostęp tooQuestetra BPM Suite 
* Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooQuestetra Suite BPM (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
* Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne
tooconfigure integracji usługi Azure AD z pakietem BPM Questetra należy hello następujące elementy:

* Subskrypcję usługi Azure AD
* [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) jednokrotnego włączone subskrypcji

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

1. Dodawanie pakietu BPM Questetra z galerii hello 
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a>Dodawanie pakietu BPM Questetra z galerii hello
tooconfigure hello integracji pakietu BPM Questetra do usługi Azure AD, należy tooadd Questetra BPM pakiet z listy tooyour galerii hello zarządzanych aplikacji SaaS.

**tooadd Questetra BPM pakiet z galerii hello wykonaj hello następujące kroki:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**. 
   
    ![Usługa Active Directory][1]

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Aplikacje][2]

4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Aplikacje][3]

5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
    ![Aplikacje][4]

6. W polu wyszukiwania hello wpisz **Questetra BPM Suite**.
   
    ![Aplikacje][5]

7. W okienku wyników hello, wybierz **Questetra BPM Suite**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
Celem Hello w tej sekcji jest tooshow użytkownika jak tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z pakietem BPM Questetra na podstawie użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jest odpowiednikiem hello użytkownika w pakiet BPM Questetra tooan użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi pakietu BPM Questetra musi toobe ustanowione.  
Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** pakietu BPM Questetra.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z pakietem BPM Questetra, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego zestawu BPM Questetra](#creating-a-questetra-bpm-suite-test-user)**  -toohave odpowiednikiem Simona Britta pakietu BPM Questetra, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej
Celem Hello w tej sekcji jest tooenable usługi Azure AD rejestracji jednokrotnej w hello klasycznego portalu Azure i tooconfigure rejestracji jednokrotnej w Questetra BPM pakietu aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z pakietem BPM Questetra, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure na powitania **Questetra BPM Suite** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne**  okno dialogowe.
   
    ![Konfigurowanie rejestracji jednokrotnej][8]

2. Na powitania **jak ma toosign użytkowników na tooQuestetra BPM Suite** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Azure AD rejestracji jednokrotnej][9]

3. W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **Questetra BPM Suite** witryny firmy jako administrator.

4. W menu hello na górze hello, kliknij przycisk **ustawienia systemu**. 
   
    ![Azure AD rejestracji jednokrotnej][10]

5. Witaj tooopen **SingleSignOnSAML** kliknij przycisk **logowania jednokrotnego (SAML)**. 
   
    ![Azure AD rejestracji jednokrotnej][11]

6. W hello klasycznego portalu Azure na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj hello następujące kroki: 
   
    ![Konfiguruj ustawienia aplikacji][13]
   
    a. W przypadku **Questetra BPM Suite** witryna firmy, w sekcji informacji SP hello, hello kopiowania **adres URL usługi ACS**, a następnie wklej go do hello **na adres URL logowania** pola tekstowego.
   
    b. W przypadku **Questetra BPM Suite** witryna firmy, w sekcji informacji SP hello, hello kopiowania **identyfikator jednostki**i wklej go do hello **adres URL wystawcy** pola tekstowego.
   
    c. W przypadku **Questetra BPM Suite** witryna firmy, w sekcji informacji SP hello, hello kopii **adres URL usługi ACS**, a następnie wklej go do hello **adres URL odpowiedzi** pole tekstowe.
   
    d. Kliknij przycisk **Dalej**.

7. Na powitania **skonfigurować logowanie jednokrotne w pakiet BPM Questetra** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu hello lokalnie na komputerze.
   
    ![Konfigurowanie rejestracji jednokrotnej][14]

8. W przypadku **Questetra BPM Suite** firmy, witryny, wykonaj następujące kroki hello: 
   
    ![Konfigurowanie rejestracji jednokrotnej][15]
   
    a. Wybierz **Włącz rejestrację jednokrotną**.
   
    b. Na powitania klasycznego portalu Azure, skopiuj hello **adres URL wystawcy** wartość, a następnie wklej go do hello **identyfikator jednostki** pola tekstowego.
   
    c. Na powitania klasycznego portalu Azure, skopiuj hello **pojedynczy znak na adres URL usługi** wartość, a następnie wklej go do hello **adres URL logowania strony** pola tekstowego.
   
    d. Na powitania klasycznego portalu Azure, skopiuj hello **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej go do hello **adres URL strony wylogowania** pola tekstowego.
   
    e. W hello **NameID format** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.

    f. Utwórz plik zakodowany base-64 z pobranego certyfikatu. 

    >[!TIP] 
    >Aby uzyskać więcej informacji, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o).

    g. Otwórz certyfikatu zakodowanego base-64 w Notatniku, hello kopiowania zawartości go do Schowka, a następnie wklej go do hello **certyfikatu weryfikacji** pola tekstowego. 

    h. Kliknij pozycję **Zapisz**.

1. Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**. 
   
    ![Co to jest program Azure AD Connect][17]

2. Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.  
   
    ![Co to jest program Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego w hello klasycznego portalu Azure o nazwie Simona Britta.

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD][100] 

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD][101] 

4. Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**. 
   
    ![Tworzenie użytkownika testowego usługi Azure AD][102] 

5. Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD][103]
   
    a. Jako **typ użytkownika**, wybierz pozycję **nowy użytkownik w organizacji**.
   
    b. W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.
   
    c. Kliknij przycisk Dalej.

6. Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki: 
   
    ![Tworzenie użytkownika testowego usługi Azure AD][104] 
   
    a. W hello **imię** pole tekstowe, typ **Britta**. 
   
    b. W hello **nazwisko** pole tekstowe, typ **Simona**.
   
    c. W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.
   
    d. W hello **roli** listy, wybierz **użytkownika**.
   
    e. Kliknij przycisk **Dalej**.

7. Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD][105]  

8. Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD][106]   
   
    a. Zanotuj wartość hello hello **nowe hasło**.
   
    b. Kliknij przycisk **Complete** (Zakończ).   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>Tworzenie użytkownika testowego Questetra BPM Suite
Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta Questetra BPM pakietu.

**Użytkownik o nazwie Simona Britta pakietu BPM Questetra toocreate wykonaj hello następujące kroki:**

1. Logowania jednokrotnego tooyour Questetra BPM Suite witryna firmy jako administrator.
2. Przejdź za**ustawienia systemu > listy użytkowników > Nowy użytkownik**. 
3. W oknie dialogowym Nowy użytkownik hello wykonaj następujące kroki hello: 
   
    ![Tworzenie użytkownika testowego][300] 
   
    a. W hello **nazwa** tekstowym, wpisz nazwę użytkownika w Britta w usłudze Azure AD.
   
    b. W hello **E-mail** tekstowym, wpisz nazwę użytkownika w Britta w usłudze Azure AD.
   
    c. W hello **hasło** tekstowym, wpisz hasło.

4. Kliknij przycisk **Dodaj nowego użytkownika**.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD
Celem Hello w tej sekcji jest tooenabling toouse Simona Britta Azure rejestracji jednokrotnej, przyznając jej tooQuestetra dostępu BPM Suite.

![Co to jest program Azure AD Connect][200]

**tooassign tooQuestetra Simona Britta BPM Suite wykonaj hello następujące kroki:**

1. Na hello Azure kliknij klasycznego portalu, widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Co to jest program Azure AD Connect][201]
2. Z listy aplikacji hello wybierz **Questetra BPM Suite**.
   
    ![Co to jest program Azure AD Connect][205]
3. W menu hello na górze hello, kliknij przycisk **użytkowników**.
   
    ![Co to jest program Azure AD Connect][202]
4. Na liście hello użytkowników, wybierz **Simona Britta**.
   
    ![Co to jest program Azure AD Connect][203]
5. W narzędzi hello na dole powitania kliknij **przypisać**.
   
    ![Co to jest program Azure AD Connect][204]

### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej
Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.  
Po kliknięciu kafelka Questetra BPM Suite hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Questetra BPM pakietu aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
