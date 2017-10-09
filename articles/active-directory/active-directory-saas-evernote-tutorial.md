---
title: 'Samouczek: Integracji Azure Active Directory z Evernote | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Evernote."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a>Samouczek: Integracji Azure Active Directory z Evernote

Z tego samouczka, dowiesz się, jak toointegrate Evernote w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Evernote zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooEvernote.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooEvernote (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Evernote należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Evernote logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Evernote z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-evernote-from-hello-gallery"></a>Dodawanie Evernote z galerii hello
tooconfigure hello integracji Evernote do usługi Azure AD, należy tooadd Evernote z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Evernote z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **Evernote**, wybierz pozycję **Evernote** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Evernote hello listy wyników](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Evernote w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Evernote jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Evernote musi toobe ustanowione.

W Evernote, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Evernote, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Evernote](#create-an-evernote-test-user)**  -toohave odpowiednikiem Simona Britta w Evernote, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Evernote.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Evernote, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Evernote** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. Na powitania **Evernote domeny i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz tooconfigure aplikacji hello w rozszerzeniu IDP zainicjował tryb hello:

    ![Adresy URL i domeny Evernote pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://www.evernote.com/saml2`

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonywać powitania po kroku, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:

    ![Adresy URL i domeny Evernote pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    W hello **Zaloguj się na adres URL** pole tekstowe, wprowadź adres URL hello:`https://www.evernote.com/Login.action`   

5. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. Na powitania **konfiguracji Evernote** kliknij **skonfigurować Evernote** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfiguracja Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Evernote jako administrator.

9. Przejdź do zbyt**"Konsoli administracyjnej"**

    ![Konsola administracyjna](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. Z hello **"Konsoli administracyjnej"**, przejdź zbyt**"Zabezpieczenia"** i wybierz **"Logowanie jednokrotne"**

    ![Ustawienia logowania jednokrotnego](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. Skonfiguruj hello następujące wartości:

    ![Ustawienia certyfikatów](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    a.  **Włącz logowanie Jednokrotne:** rejestracji Jednokrotnej jest domyślnie włączona (kliknij **wyłączyć logowanie jednokrotne** wymaganie rejestracji Jednokrotnej hello tooremove)

    b. Wklej **SAML rejestracji jednokrotnej adres URL usługi** wartość, która została skopiowana z hello portalu Azure do hello **adres URL żądania HTTP SAML** pola tekstowego.

    c. Otwórz hello certyfikat pobrany z usługi Azure AD w programie Notatnik i skopiuj zawartości hello tym "BEGIN certyfikatu" i "END CERTIFICATE" i wklej go do hello **certyfikatu X.509** pola tekstowego. 

    d.Click **zapisać zmiany**

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-an-evernote-test-user"></a>Tworzenie użytkownika testowego Evernote

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Evernote muszą mieć przydzielone do Evernote.  
W przypadku hello Evernote Inicjowanie obsługi to zadanie ręczne.

**tooprovision kont użytkowników, wykonaj hello następujące kroki:**

1. Zaloguj się za tooyour Evernote witryny firmy jako administrator.

2. Kliknij przycisk hello **"Konsoli administracyjnej"**.

    ![Konsola administracyjna](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. Z hello **"Konsoli administracyjnej"**, przejdź do zbyt**"Dodawanie użytkowników"**.

    ![Dodaj testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. **Dodawanie członków zespołu** w hello **E-mail** pole tekstowe, wpisz adres e-mail hello konta użytkownika i kliknij przycisk **zaprosić.**

    ![Dodaj testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. Po wysłaniu zaproszenia, właścicielem konta usługi Azure Active Directory hello otrzymają wiadomość e-mail z zaproszeniem hello tooaccept.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooEvernote.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooEvernote Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Evernote**.

    ![łącze Evernote Hello na liście aplikacji hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Evernote hello w hello Panel dostępu, należy pobrać zalogowane tooyour Evernote aplikacji. Można będzie można logować się jako konta organizacji, ale następnie toolog muszą się przy użyciu konta osobistego. 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

