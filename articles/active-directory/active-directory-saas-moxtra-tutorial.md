---
title: 'Samouczek: Integracji Azure Active Directory z Moxtra | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a>Samouczek: Integracji Azure Active Directory z Moxtra

Z tego samouczka, dowiesz się, jak toointegrate Moxtra w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Moxtra zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMoxtra
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMoxtra (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Moxtra należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Moxtra logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Moxtra z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-moxtra-from-hello-gallery"></a>Dodawanie Moxtra z galerii hello
tooconfigure hello integracji Moxtra do usługi Azure AD, należy tooadd Moxtra z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Moxtra z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Moxtra**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. W panelu wyników hello zaznacz **Moxtra**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Moxtra w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Moxtra jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Moxtra musi toobe ustanowione.

W Moxtra, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Moxtra, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Moxtra](#creating-a-moxtra-test-user)**  -toohave odpowiednikiem Simona Britta w Moxtra, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Moxtra.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Moxtra, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Moxtra** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. Na powitania **Moxtra domeny i adres URL** sekcji, wykonaj powitania po kroku:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL jako:`https://www.moxtra.com/service/#login`

4. Aplikacja Moxtra oczekuje potwierdzenia SAML hello w określonym formacie. Skonfiguruj powitania po oświadczeń dla tej aplikacji. Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji. powitania po zrzut ekranu przedstawia przykład dla tej konfiguracji. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:
    
    | Nazwa atrybutu | Wartość atrybutu |
    | ------------------- | -------------------- |    
    | Imię | User.givenName |
    | nazwisko | User.surname |
    | idpid    | < Identyfikator jednostki SAML > 

    > [!Note]
    > Witaj wartość **idpid** atrybut nie jest prawdziwe. Można uzyskać wartość rzeczywista hello z **krótkimi opisami** w obszarze **Moxtra konfiguracji**.
    
    a. Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    b. W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    c. Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.

    d. Kliknij przycisk **OK**.
    
5. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. Na powitania **konfiguracji Moxtra** kliknij **skonfigurować Moxtra** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. W innym oknie przeglądarki Zaloguj się w witrynie firmy Moxtra tooyour jako administrator.

9. Na powitania narzędzi po lewej stronie powitania kliknij **konsoli administracyjnej > SAML logowania jednokrotnego**, a następnie kliknij przycisk **nowy**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. Na powitania **SAML** wykonaj hello następujące kroki:
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    a. W hello **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: *SAML*). 
  
    b. W hello **identyfikator jednostki IdP** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure. 
 
    c. W **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure. 
 
    d. W hello **AuthnContextClassRef** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:ac:classes:Password**. 
 
    e. W hello **NameID Format** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**. 
 
    f. Otwórz certyfikat, który został pobrany z portalu Azure w programie Notatnik, skopiuj zawartość hello i wkleić go do hello **certyfikatu** pola tekstowego.    
 
    g. W hello SAML e-mail domeny tekstowym wpisz domenę poczty e-mail SAML.    
  
    >[!NOTE]
    >toosee hello kroki tooverify hello domeny, kliknij przycisk hello "**i**" poniżej.

    h. Kliknij przycisk **aktualizacji**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-moxtra-test-user"></a>Tworzenie użytkownika testowego Moxtra

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Moxtra.

**toocreate użytkownika o nazwie Simona Britta w Moxtra, wykonaj następujące kroki hello:**

1. Rejestracja tooyour Moxtra witryny firmy jako administrator.

2. Na powitania narzędzi po lewej stronie powitania kliknij **konsoli administracyjnej > Zarządzanie użytkownikami**, a następnie **Dodaj użytkownika**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. Na powitania **Dodaj użytkownika** okna dialogowego, wykonaj następujące kroki hello:
  
    a. W hello **imię** pole tekstowe, typ **Britta**.
  
    b. W hello **nazwisko** pole tekstowe, typ **Simona**.
  
    c. W hello **E-mail** tekstowym, wpisz adres e-mail firmy Britta identyczny z portalu Azure.
  
    d. W hello **dzielenia** pole tekstowe, typ **deweloperów**.
  
    e. W hello **działu** pole tekstowe, typ **IT**.
  
    f. Wybierz **administratora**.
  
    g. Kliknij pozycję **Dodaj**.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMoxtra.

![Przypisz użytkownika][200] 

**tooassign tooMoxtra Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Moxtra**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Moxtra hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Moxtra aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

