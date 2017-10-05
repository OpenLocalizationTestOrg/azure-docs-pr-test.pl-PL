---
title: 'Samouczek: Azure Active Directory integracji z pakietem BPM Questetra | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Questetra BPM Suite."
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
ms.openlocfilehash: 7ae75446c9d19ce15a82caa9604658a528ab9941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>Samouczek: Azure Active Directory integracji z pakietem BPM Questetra
Celem tego samouczka jest pokazanie sposobu integracji Questetra BPM pakietu z usługi Azure Active Directory (Azure AD).  
Integracja z usługą Azure AD Questetra BPM Suite zapewnia następujące korzyści: 

* Można kontrolować w usłudze Azure AD, który ma dostęp do zestawu BPM Questetra 
* Umożliwia użytkownikom automatycznie pobrać zalogowane Questetra BPM pakietu (logowanie jednokrotne) z konta usługi Azure AD
* Możesz zarządzać kont w jednej centralnej lokalizacji - klasycznego portalu Azure

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne
Aby skonfigurować integrację usługi Azure AD z pakietem BPM Questetra, potrzebne są następujące elementy:

* Subskrypcję usługi Azure AD
* [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) jednokrotnego włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.
> 
> 

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

* Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
* Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Opis scenariusza
Celem tego samouczka jest umożliwienie umożliwia testowanie usługi Azure AD rejestracji jednokrotnej w środowisku testowym.  
Scenariusz opisany w tym samouczku składa się z trzech głównych bloków konstrukcyjnych:

1. Dodawanie pakietu BPM Questetra z galerii 
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-questetra-bpm-suite-from-the-gallery"></a>Dodawanie pakietu BPM Questetra z galerii
Aby skonfigurować integrację usługi Azure AD Questetra BPM pakietu, należy dodać pakiet BPM Questetra z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać pakiet BPM Questetra z galerii, wykonaj następujące czynności:**

1. W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**. 
   
    ![Usługa Active Directory][1]

2. Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.

3. Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.
   
    ![Aplikacje][2]

4. Kliknij przycisk **Dodaj** w dolnej części strony.
   
    ![Aplikacje][3]

5. Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.
   
    ![Aplikacje][4]

6. W polu wyszukiwania wpisz **Questetra BPM Suite**.
   
    ![Aplikacje][5]

7. W okienku wyników wybierz **Questetra BPM Suite**, a następnie kliknij przycisk **Complete** można dodać aplikację.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
Jest celem tej sekcji opisano, jak skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z pakietem BPM Questetra w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, co to jest odpowiednikiem użytkownikowi pakietu BPM Questetra użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi pakietu BPM Questetra musi określone.  
Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** Questetra BPM pakietu.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z pakietem BPM Questetra, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego zestawu BPM Questetra](#creating-a-questetra-bpm-suite-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Questetra BPM pakiet, który jest połączony z jej reprezentacji usługi Azure AD.
4. **[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej
Celem tej sekcji jest można włączyć usługi Azure AD rejestracji jednokrotnej w klasycznym portalu Azure i skonfigurować logowanie jednokrotne w Questetra BPM pakietu aplikacji.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z pakietem BPM Questetra, wykonaj następujące czynności:**

1. W klasycznym portalu Azure na **Questetra BPM Suite** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować logowanie jednokrotne** okna dialogowego.
   
    ![Konfigurowanie rejestracji jednokrotnej][8]

2. Na **jak chcesz użytkownikom zalogować się do zestawu BPM Questetra** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Azure AD rejestracji jednokrotnej][9]

3. W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **Questetra BPM Suite** witryny firmy jako administrator.

4. W menu u góry kliknij **ustawienia systemu**. 
   
    ![Azure AD rejestracji jednokrotnej][10]

5. Aby otworzyć **SingleSignOnSAML** kliknij przycisk **logowania jednokrotnego (SAML)**. 
   
    ![Azure AD rejestracji jednokrotnej][11]

6. W klasycznym portalu Azure na **Konfigurowanie ustawień aplikacji** okna dialogowego strony, należy wykonać następujące czynności: 
   
    ![Konfiguruj ustawienia aplikacji][13]
   
    a. W przypadku **Questetra BPM Suite** witryna firmy, w sekcji informacji SP kopii **adres URL usługi ACS**i wklej go do **na adres URL logowania** pola tekstowego.
   
    b. W przypadku **Questetra BPM pakiet** witryna firmy, w sekcji informacji SP kopii **identyfikator jednostki**, a następnie wklej go do **adres URL wystawcy** pole tekstowe.
   
    c. W przypadku **Questetra BPM Suite** witryna firmy, w sekcji informacji SP kopii **adres URL usługi ACS**i wklej go do **adres URL odpowiedzi służący** pola tekstowego.
   
    d. Kliknij przycisk **Dalej**.

7. Na **skonfigurować logowanie jednokrotne w pakiet BPM Questetra** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu lokalnie na komputerze.
   
    ![Konfigurowanie rejestracji jednokrotnej][14]

8. W przypadku **Questetra BPM Suite** firmy, witryny, należy wykonać następujące czynności: 
   
    ![Konfigurowanie rejestracji jednokrotnej][15]
   
    a. Wybierz **Włącz rejestrację jednokrotną**.
   
    b. W klasycznym portalu Azure, skopiuj **adres URL wystawcy** wartość, a następnie wklej ją do **identyfikator jednostki** pola tekstowego.
   
    c. W klasycznym portalu Azure, skopiuj **pojedynczy znak na adres URL usługi** wartość, a następnie wklej ją do **adres URL logowania strony** pola tekstowego.
   
    d. W klasycznym portalu Azure, skopiuj **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej ją do **adres URL strony wylogowania** pola tekstowego.
   
    e. W **NameID format** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.

    f. Utwórz plik zakodowany base-64 z pobranego certyfikatu. 

    >[!TIP] 
    >Aby uzyskać więcej informacji, zobacz [sposób konwertowania binarne certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o).

    g. Otwórz w Notatniku certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu weryfikacji** pola tekstowego. 

    h. Kliknij pozycję **Zapisz**.

1. W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **dalej**. 
   
    ![Co to jest program Azure AD Connect][17]

2. Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.  
   
    ![Co to jest program Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem tej sekcji jest tworzenie użytkownika testowego w klasycznym portalu Azure o nazwie Simona Britta.

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD][100] 

2. Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.

3. Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD][101] 

4. Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**. 
   
    ![Tworzenie użytkownika testowego usługi Azure AD][102] 

5. Na **Poinformuj nas o tym użytkowniku** okna dialogowego strony, należy wykonać następujące czynności:
   
    ![Tworzenie użytkownika testowego usługi Azure AD][103]
   
    a. Jako **typ użytkownika**, wybierz pozycję **nowy użytkownik w organizacji**.
   
    b. W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.
   
    c. Kliknij przycisk Dalej.

6. Na **profilu użytkownika** okna dialogowego strony, należy wykonać następujące czynności: 
   
    ![Tworzenie użytkownika testowego usługi Azure AD][104] 
   
    a. W **imię** pole tekstowe, typ **Britta**. 
   
    b. W **nazwisko** pole tekstowe, typ **Simona**.
   
    c. W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.
   
    d. W **roli** listy, wybierz **użytkownika**.
   
    e. Kliknij przycisk **Dalej**.

7. Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD][105]  

8. Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:
   
    ![Tworzenie użytkownika testowego usługi Azure AD][106]   
   
    a. Zanotuj wartość **nowe hasło**.
   
    b. Kliknij przycisk **Complete** (Zakończ).   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>Tworzenie użytkownika testowego Questetra BPM Suite
Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta Questetra BPM pakietu.

**Aby utworzyć użytkownika o nazwie Simona Britta pakietu BPM Questetra, wykonaj następujące kroki:**

1. Logowanie do witryny firmy Questetra BPM Suite jako administrator.
2. Przejdź do **ustawienia systemu > listy użytkowników > Nowy użytkownik**. 
3. W oknie dialogowym Nowy użytkownik wykonaj następujące czynności: 
   
    ![Tworzenie użytkownika testowego][300] 
   
    a. W **nazwa** tekstowym, wpisz nazwę użytkownika w Britta w usłudze Azure AD.
   
    b. W **E-mail** tekstowym, wpisz nazwę użytkownika w Britta w usłudze Azure AD.
   
    c. W **hasło** tekstowym, wpisz hasło.

4. Kliknij przycisk **Dodaj nowego użytkownika**.

### <a name="assigning-the-azure-ad-test-user"></a>Przypisanie użytkownika testowego usługi Azure AD
Celem tej sekcji jest włączenie Simona Britta na udostępnienie jej do zestawu BPM Questetra za pomocą usługi Azure rejestracji jednokrotnej.

![Co to jest program Azure AD Connect][200]

**Aby przypisać Simona Britta Questetra BPM pakietu, wykonaj następujące czynności:**

1. W klasycznym portalu Azure, aby otworzyć widok aplikacji, w widoku katalogu, kliknij polecenie **aplikacji** w menu u góry.
   
    ![Co to jest program Azure AD Connect][201]
2. Na liście aplikacji zaznacz **Questetra BPM Suite**.
   
    ![Co to jest program Azure AD Connect][205]
3. W menu u góry kliknij **użytkowników**.
   
    ![Co to jest program Azure AD Connect][202]
4. Na liście użytkowników wybierz **Simona Britta**.
   
    ![Co to jest program Azure AD Connect][203]
5. Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.
   
    ![Co to jest program Azure AD Connect][204]

### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej
Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.  
Po kliknięciu kafelka Questetra BPM Suite w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane Questetra BPM pakiet aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
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
