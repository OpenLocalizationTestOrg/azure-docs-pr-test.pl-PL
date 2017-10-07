---
title: 'Samouczek: Integracji Azure Active Directory z LearnUpon | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a>Samouczek: Integracji Azure Active Directory z LearnUpon

Z tego samouczka, dowiesz się, jak toointegrate LearnUpon w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD LearnUpon zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLearnUpon
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLearnUpon (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z LearnUpon należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- LearnUpon logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie LearnUpon z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-learnupon-from-hello-gallery"></a>Dodawanie LearnUpon z galerii hello
tooconfigure hello integracji LearnUpon do usługi Azure AD, należy tooadd LearnUpon z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd LearnUpon z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **LearnUpon**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. W panelu wyników hello zaznacz **LearnUpon**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LearnUpon w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w LearnUpon jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w LearnUpon musi toobe ustanowione.

W LearnUpon, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z LearnUpon, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego LearnUpon](#creating-a-learnupon-test-user)**  -toohave odpowiednikiem Simona Britta w LearnUpon, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji LearnUpon.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z LearnUpon, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **LearnUpon** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. Na powitania **LearnUpon domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.learnupon.com/saml/consumer`

    > [!NOTE] 
    > Należy pamiętać, że nie jest hello rzeczywistą wartość. masz tooupdate tej wartości z adresem URL hello rzeczywiste odpowiedzi. Skontaktuj się z tej wartości tooget [zespołem pomocy technicznej LearnUpon](https://www.learnupon.com/features/support/).



4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Raw)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji LearnUpon** kliknij **skonfigurować LearnUpon** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. Otwórz innego wystąpienia przeglądarki i zaloguj do LearnUpon przy użyciu konta administratora. 

8. Kliknij przycisk hello **ustawienia** kartę.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. Kliknij przycisk **rejestracji jednokrotnej - SAML**, a następnie kliknij przycisk **ustawienia ogólne** tooconfigure SAML ustawienia.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. W hello **ustawienia ogólne** sekcji, wykonaj następujące kroki hello:
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    a. Wybierz **włączone**.

    b. Wybierz **wersji** jako **2.0**.

    c. Wybierz **pominąć warunki** jako **nr**.

    d. W hello **Post tokenu SAML nazwę param** pole tekstowe, nazwa typu hello żądania post parametru toohello adres URL klienta SAML wymienionych powyżej zawierający hello potwierdzenia języka SAML toobe zweryfikowane i uwierzytelniony — na przykład  **SAMLResponse**.

    e. W hello **Format identyfikatora nazwy** pole tekstowe, typ hello wartość, która wskazuje, gdzie w użytkownikom hello potwierdzenia języka SAML identyfikator (adres E-mail) znajduje się — na przykład **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.
  
    f. W hello **zidentyfikować lokalizacji dostawcy** pole tekstowe, typ hello wartość, która wskazuje, gdzie hello użytkownicy są wysyłane tooif kliknij przycisk z przekazanego ikonę z ekranu logowania do portalu Azure.
  
    g. W hello **Wyloguj adresu URL** pole tekstowe, Wklej hello **Sign-Out URL** którego została skopiowana z hello portalu Azure.
    
    h. Kliknij przycisk **Zarządzanie odbitek palca**, a następnie przekaż hello odcisk palca certyfikatu pobrane.

11. Kliknij przycisk **ustawienia użytkownika**, a następnie wykonaj następujące kroki hello:
   
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    a. W hello **Format identyfikatora imię** pole tekstowe, typ hello wartość, która informuje NAS w Twoje imię potwierdzenia języka SAML hello użytkowników znajduje się — na przykład: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.
  
    b. W hello **ostatniego Format identyfikatora nazwy** pole tekstowe, typ hello wartość, która informuje NAS w Twoje nazwisko potwierdzenia języka SAML hello użytkowników znajduje się — na przykład: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-learnupon-test-user"></a>Tworzenie użytkownika testowego LearnUpon

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w LearnUpon. LearnUpon obsługę w czasie, który jest domyślnie włączone.

Nie ma elementu akcji można w tej sekcji. Nowy użytkownik zostanie utworzony podczas próby tooaccess LearnUpon, jeśli go jeszcze nie istnieje. [Konfigurowanie usługi Azure AD jednokrotnej](#configuring-azure-ad-single-single-sign-on).

>[!NOTE]
>Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact [zespołem pomocy technicznej LearnUpon](https://www.learnupon.com/features/support/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLearnUpon.

![Przypisz użytkownika][200] 

**tooassign tooLearnUpon Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **LearnUpon**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka LearnUpon hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour LearnUpon aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

