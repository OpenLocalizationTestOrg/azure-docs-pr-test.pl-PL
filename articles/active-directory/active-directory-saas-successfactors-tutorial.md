---
title: 'Samouczek: Integracji Azure Active Directory z SuccessFactors | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse SuccessFactors z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a>Samouczek: Integracji Azure Active Directory z SuccessFactors
Celem Hello tego samouczka jest tooshow należy jak toointegrate SuccessFactors w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD SuccessFactors zapewnia hello następujące korzyści:

* Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSuccessFactors
* Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSuccessFactors (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
* Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne
tooconfigure integracji z usługą Azure AD z SuccessFactors należy hello następujące elementy:

* Ważnej subskrypcji platformy Azure
* Dzierżawcy w SuccessFactors

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.
> 
> 

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

* Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
* Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
Celem Hello tego samouczka jest tooenable możesz tootest usługi Azure AD rejestracji jednokrotnej w środowisku testowym.

Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie SuccessFactors z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-successfactors-from-hello-gallery"></a>Dodawanie SuccessFactors z galerii hello
tooconfigure hello integracji SuccessFactors do usługi Azure AD, należy tooadd SuccessFactors z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd SuccessFactors z galerii hello, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure, na panelu nawigacyjnym po lewej stronie powitania kliknij **usługi Active Directory**.
   
    ![Konfigurowanie rejestracji jednokrotnej][1]
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Konfigurowanie rejestracji jednokrotnej][2]
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Aplikacje][3]
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
    ![Konfigurowanie rejestracji jednokrotnej][4]
6. W hello **pole wyszukiwania**, typ **SuccessFactors**.
   
    ![Konfigurowanie rejestracji jednokrotnej][5]
7. W panelu wyników hello, wybierz **SuccessFactors**, a następnie kliknij przycisk **Complete** tooadd hello aplikacji.
   
    ![Konfigurowanie rejestracji jednokrotnej][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
Celem Hello w tej sekcji jest tooshow użytkownika jak tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SuccessFactors na podstawie użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jest odpowiednikiem hello użytkownika w SuccessFactors tooan użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w SuccessFactors musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w SuccessFactors.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SuccessFactors, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego SuccessFactors](#creating-a-successfactors-test-user)**  -toohave odpowiednikiem Simona Britta w SuccessFactors, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu klasycznym hello i skonfigurować logowanie jednokrotne w aplikacji SuccessFactors.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z SuccessFactors, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure na powitania **SuccessFactors** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okno dialogowe.
   
    ![Konfigurowanie rejestracji jednokrotnej][7]
2. Na powitania **jak ma toosign użytkowników na tooSuccessFactors** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Konfigurowanie rejestracji jednokrotnej][8]
3. Na powitania **Konfigurowanie adresu URL aplikacji** , wykonaj następujące kroki hello, a następnie kliknij przycisk **dalej**.
   
    ![Konfigurowanie rejestracji jednokrotnej][9]
   
    a. W hello **na adres URL logowania** tekstowym, wpisz adres URL przy użyciu jednej z powitania po wzorców: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL przy użyciu jednej z powitania po wzorców: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    c. Kliknij przycisk **Dalej**. 

    > [!NOTE]
    > Należy pamiętać, że nie są one hello wartości rzeczywistych. Masz tooupdate tych wartości za pomocą hello rzeczywiste na adres URL logowania i odpowiedzi adresu URL. Skontaktuj się z tych wartości, tooget [SuccessFactors obsługuje zespołu](https://www.successfactors.com/en_us/support.html).

1. Na powitania **skonfigurować logowanie jednokrotne w SuccessFactors** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu hello lokalnie na komputerze.
   
    ![Konfigurowanie rejestracji jednokrotnej][10]

2. W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **portalu administracyjnego SuccessFactors** jako administrator.

3. Odwiedź stronę **zabezpieczeń aplikacji** i natywne zbyt**pojedynczy znak w funkcji**. 

4. Umieść wszystkie wartości w hello **zresetować tokenu** i kliknij przycisk **zapisać tokenu** tooenable logowania jednokrotnego SAML.
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji][11]

    > [!NOTE] 
    > Ta wartość jest używana tylko jako hello wyłącznik. Po zapisaniu wartości hello logowania jednokrotnego SAML jest włączone. Po zapisaniu pustego hello logowania jednokrotnego SAML został WYŁĄCZONY.

1. Zrzut ekranu toobelow macierzystego i wykonaj następujące akcje hello.
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji][12]
   
    a. Wybierz hello **logowania jednokrotnego SAML v2** przycisku radiowego
   
    b. Ustaw hello Name(e.g. SAml issuer + company name) strona zostanie SAML.
   
    c. W hello **wystawcy SAML** pole tekstowe umieścić wartość hello **adres URL wystawcy** z Kreatora konfiguracji aplikacji usługi Azure AD.
   
    d. Wybierz **odpowiedzi (odbiorcy wygenerowanych/IdP/AP)** jako **wymagają podpisu obowiązkowe**.
   
    e. Wybierz **włączone** jako **Włącz flagę SAML**.
   
    f. Wybierz **nr** jako **podpisu żądania logowania (rz wygenerowanych/SP/RP)**.
   
    g. Wybierz **profilu przeglądarki lub używanego po** jako **profilu SAML**.
   
    h. Wybierz **nr** jako **wymusić nieprawidłowy okres certyfikatu**.
   
    i. Kopiowanie zawartości hello hello pliku pobranego certyfikatu, a następnie wklej go do hello **certyfikatu weryfikacji SAML** pola tekstowego.

    > [!NOTE] 
    > zawartość certyfikatu Hello musi mieć rozpocząć certyfikatu i na końcu tagi certyfikatu.

1. Przejdź tooSAML V2, a następnie wykonaj następujące kroki hello:
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji][13]
   
    a. Wybierz **tak** jako **inicjowane SP wylogowania globalnego obsługują**.
   
    b. W hello **globalne wylogowania adres URL usługi (LogoutRequest docelowy)** pole tekstowe umieścić wartość hello **zdalnego adresu URL wylogowania** z Kreatora konfiguracji aplikacji usługi Azure AD.
   
    c. Wybierz **nr** jako **wymagają sp należy szyfrować wszystkie element NameID**.
   
    d. Wybierz **nieokreślony** jako **NameID Format**.
   
    e. Wybierz **tak** jako **Włącz sp zainicjował logowania (AuthnRequest)**.
   
    f. W hello **żądanie wysłania jako wystawca firmie** pole tekstowe umieścić wartość hello **zdalnego adresu URL logowania** z Kreatora konfiguracji aplikacji usługi Azure AD.
2. Wykonaj następujące kroki, jeśli chcesz, aby toomake hello logowania użytkowników bez uwzględniania wielkości liter,.
   
    a. Odwiedź stronę **ustawienia firmy**(dolnej hello).
   
    b. Zaznacz pole wyboru obok **włączyć Username Non-uwzględniana wielkość liter**.
   
    c.Click **zapisać**.
   
    ![Konfigurowanie rejestracji jednokrotnej][29]

    > [!NOTE] 
    > Jeśli spróbujesz tooenable to, hello system sprawdza, czy spowoduje utworzenie zduplikowanej nazwy logowania SAML. Na przykład nazwy użytkowników Użytkownik1 i Użytkownik1 ma powitania klienta. Zdjęciu uwzględniana wielkość liter powoduje, że te duplikaty. Hello system otrzymasz komunikat o błędzie i nie dają hello funkcji. powitania klienta należy toochange jedną z nazw użytkowników hello tak faktycznie Pisownia jest inny. 

1. Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
   
    ![Aplikacje][14]
2. Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.
   
    ![Aplikacje][15]

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu klasycznym hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][16]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD][17]
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD][18]
4. Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD][19]
5. Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD][20]
   
    a. Jako typ użytkownika wybierz nowego użytkownika w organizacji.
   
    b. W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.
   
    c. Kliknij przycisk **Dalej**.
6. Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD][21]
   
    a. W hello **imię** pole tekstowe, typ **Britta**.  
   
    b. W hello **nazwisko** pole tekstowe, typ **Simona**.
   
    c. W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.
   
    d. W hello **roli** listy, wybierz **użytkownika**.
   
    e. Kliknij przycisk **Dalej**.
7. Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD][22]
8. Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD][23]
   
    a. Zanotuj wartość hello hello **nowe hasło**.
   
    b. Kliknij przycisk **Complete** (Zakończ).  

### <a name="creating-a-successfactors-test-user"></a>Tworzenie użytkownika testowego SuccessFactors
W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do SuccessFactors muszą mieć przydzielone do SuccessFactors.  
W przypadku hello SuccessFactors Inicjowanie obsługi to zadanie ręczne.

Użytkownicy tooget utworzone w SuccessFactors, potrzebujesz toocontact hello [SuccessFactors obsługuje zespołu](https://www.successfactors.com/en_us/support.html).

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD
Celem Hello w tej sekcji jest tooenabling toouse Simona Britta Azure rejestracji jednokrotnej, przyznając jej tooSuccessFactors dostępu.

![Przypisz użytkownika][24]

**tooassign tooSuccessFactors Simona Britta wykonaj hello następujące kroki:**

1. W portalu klasycznym hello, kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Przypisz użytkownika][25]
2. Z listy aplikacji hello wybierz **SuccessFactors**.
   
    ![Konfigurowanie rejestracji jednokrotnej][26]
3. W menu hello na górze hello, kliknij przycisk **użytkowników**.
   
    ![Przypisz użytkownika][27]
4. Na liście hello użytkowników, wybierz **Simona Britta**.
5. W narzędzi hello na dole powitania kliknij **przypisać**.
   
    ![Przypisz użytkownika][28]

### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej
Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.

Po kliknięciu powitalne SuccessFactors kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SuccessFactors aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
