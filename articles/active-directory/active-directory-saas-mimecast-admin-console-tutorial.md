---
title: 'Samouczek: Integracji Azure Active Directory z konsoli administracyjnej Mimecast | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Mimecast konsoli administracyjnej."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a>Samouczek: Integracji Azure Active Directory z konsoli administracyjnej Mimecast

Z tego samouczka, dowiesz się, jak Konsola administracyjna Mimecast toointegrate w usłudze Azure Active Directory (Azure AD).

Integrowanie Mimecast konsoli administracyjnej z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMimecast konsoli administracyjnej.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMimecast konsoli administracyjnej (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z konsoli administracyjnej Mimecast należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Konsola administracyjna Mimecast logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Mimecast konsoli administracyjnej z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a>Dodawanie Mimecast konsoli administracyjnej z galerii hello
tooconfigure hello integracji konsoli administracyjnej Mimecast do usługi Azure AD, należy tooadd Mimecast konsoli administracyjnej z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Mimecast konsoli administracyjnej z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **Mimecast konsoli administracyjnej**, wybierz pozycję **Mimecast konsoli administracyjnej** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Konsola administracyjna Mimecast hello listy wyników](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z konsoli administracyjnej Mimecast w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w konsoli administracyjnej Mimecast jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w konsoli administracyjnej Mimecast musi toobe ustanowione.

W konsoli administracyjnej Mimecast, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z konsoli administracyjnej Mimecast, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego konsoli administracyjnej Mimecast](#create-a-mimecast-admin-console-test-user)**  -toohave odpowiednikiem Simona Britta w konsoli administracyjnej Mimecast, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji konsoli administracyjnej Mimecast.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z konsoli administracyjnej Mimecast, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **konsoli administracyjnej Mimecast** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. Na powitania **adresy URL i domeny konsoli administracyjnej Mimecast** sekcji, wykonaj następujące kroki hello:

    ![Adresy URL i domeny konsoli administracyjnej Mimecast pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello:
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > znak Hello na adres URL jest określonym regionie.

4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. Na powitania **Konfiguracja konsoli administratora Mimecast** , kliknij przycisk **skonfigurować konsoli administracyjnej Mimecast** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfiguracja konsoli administratora Mimecast](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się do konsoli administracyjnej Mimecast jako administrator.

8. Przejdź za**usług \> aplikacji**.

    ![Usługi](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "usług")

9. Kliknij przycisk **profile uwierzytelniania**.

    ![Profile uwierzytelniania](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "profile uwierzytelniania")
    
10. Kliknij przycisk **nowy profil uwierzytelniania**.

    ![Nowych profilów uwierzytelniania](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "nowych profilów uwierzytelniania")

11. W hello **profilu uwierzytelniania** sekcji, wykonaj następujące kroki hello:

    ![Profil uwierzytelniania](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "profilu uwierzytelniania")
    
    a. W hello **opis** tekstowym, wpisz nazwę dla danej konfiguracji.
    
    b. Wybierz **wymusić uwierzytelnianie SAML dla konsoli administracyjnej Mimecast**.
    
    c. Jako **dostawcy**, wybierz pozycję **usługi Azure Active Directory**.
    
    d. Wklej **identyfikator jednostki SAML**, która została skopiowana z hello portalu Azure do hello **adres URL wystawcy** pola tekstowego.
    
    e. Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z hello portalu Azure do hello **adres URL logowania** pola tekstowego.

    f. Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z hello portalu Azure do hello **adresu URL wylogowania** pola tekstowego.
    
    >[!NOTE]
    >Witaj wartość adresu URL logowania i wartość adresu URL wylogowania hello są dla hello konsoli administracyjnej Mimecast hello takie same.
    
    g. Otwórz swój certyfikat base-64 pobrany z portalu Azure w programie Notatnik, Usuń pierwszy wiersz hello ("*--*") i hello ostatniego wiersza ("*--*"), hello kopiowania pozostałej zawartości z niego do Schowka a następnie wklej go toohello **certyfikat dostawcy tożsamości (metadanymi)** pola tekstowego.
    
    h. Wybierz **Zezwalaj funkcji logowania jednokrotnego w**.
    
    i. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985) 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-mimecast-admin-console-test-user"></a>Tworzenie użytkownika testowego Mimecast konsoli administracyjnej

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w konsoli administracyjnej Mimecast muszą mieć przydzielone do konsoli administracyjnej Mimecast. W przypadku hello Mimecast konsoli administracyjnej Inicjowanie obsługi to zadanie ręczne.

* Należy tooregister domeny, przed przystąpieniem do tworzenia użytkowników.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. Zaloguj się na tooyour **konsoli administracyjnej Mimecast** jako administrator.
2. Przejdź za**katalogów \> wewnętrzne**.
   
   ![Katalogi](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "katalogów")
3. Kliknij przycisk **zarejestrować nową domenę**.
   
   ![Zarejestrować nową domenę](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "zarejestrować nową domenę")
4. Po utworzeniu nowej domeny, kliknij przycisk **nowy adres**.
   
   ![Nowy adres](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "nowy adres")
5. W hello nowego okna dialogowego adres i wykonaj hello następujące kroki:
   
   ![Zapisz](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Zapisz")
   
   a. Typ hello **adres E-mail**, **globalną nazwę**, **hasło**, i **Potwierdź hasło** atrybutów elementów prawidłową usługi Azure AD konto ma mają tooprovision do hello powiązanych pól tekstowych.

   b. Kliknij pozycję **Zapisz**.

>[!NOTE]
>Można użyć innych narzędzi tworzenia konta użytkownika konsoli administracyjnej Mimecast lub interfejsów API dostarczonych przez konta użytkowników usługi Azure AD tooprovision Mimecast konsoli administracyjnej. 

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMimecast konsoli administracyjnej.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooMimecast Simona Britta konsoli administracyjnej, należy wykonać hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **konsoli administracyjnej Mimecast**.

    ![łącze konsoli administracyjnej Mimecast Hello na liście aplikacji hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka konsoli administracyjnej Mimecast hello w hello Panel dostępu, należy pobrać aplikacji konsoli administracyjnej Mimecast tooyour zalogowane automatycznie.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

