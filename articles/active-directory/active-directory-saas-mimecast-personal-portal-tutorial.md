---
title: 'Samouczek: Azure Active Directory integracji z portalu osobiste Mimecast | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między Mimecast osobistych portalu i usługi Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a>Samouczek: Integracji Azure Active Directory z Mimecast osobistych portalu

Z tego samouczka, dowiesz się, jak toointegrate Mimecast Portal osobiste z usługą Azure Active Directory (Azure AD).

Integrowanie portalu osobiste Mimecast z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooMimecast osobistych portalu
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMimecast osobistych Portal (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z portalu osobiste Mimecast należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Mimecast osobistych portalu rejestracji jednokrotnej włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie portalu osobiste Mimecast z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a>Dodawanie portalu osobiste Mimecast z galerii hello
tooconfigure hello integrację Mimecast osobistych portalu usługi Azure AD, należy tooadd Mimecast Portal osobistych z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Mimecast Portal osobistych z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Portal osobiste Mimecast**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. W panelu wyników hello, wybierz **Mimecast osobistych portalu**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z portalem osobiste Mimecast w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w portalu osobiste Mimecast jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w portalu osobiste Mimecast musi toobe ustanowione.

W portalu osobiste Mimecast, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i test usługi Azure AD rejestracji jednokrotnej z portalu osobiste Mimecast należy hello toocomplete po bloków konstrukcyjnych:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego portalu osobiste Mimecast](#creating-a-mimecast-personal-portal-test-user)**  -toohave odpowiednikiem Simona Britta w portalu osobiste Mimecast, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji Portal osobiste Mimecast.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Mimecast osobistych portalu, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **Portal osobiste Mimecast** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. Na powitania **Mimecast osobistych portalu domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca: 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej osobiste klienta portalu Mimecast](https://www.mimecast.com/customer-success/technical-support/) tooget tych wartości. 
 


4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. Na powitania **Mimecast osobistych konfiguracji portalu** kliknij **skonfigurować Portal osobiste Mimecast** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się do portalu osobiste Mimecast jako administrator.

8. Przejdź za**usług \> aplikacji**.
   
    ![Aplikacje](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "aplikacji")

9. Kliknij przycisk **profile uwierzytelniania**.
   
    ![Profile uwierzytelniania](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "profile uwierzytelniania")

10. Kliknij przycisk **nowy profil uwierzytelniania**.
   
    ![Nowy profil uwierzytelniania](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "nowy profil uwierzytelniania")

11. W hello **profilu uwierzytelniania** sekcji, wykonaj następujące kroki hello:
   
    ![Profil uwierzytelniania](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "profilu uwierzytelniania")
   
    a. W hello **opis** tekstowym, wpisz nazwę dla danej konfiguracji.
   
    b. Wybierz **wymusić uwierzytelnianie SAML portalu osobiste Mimecast**.
   
    c. Jako **dostawcy**, wybierz pozycję **usługi Azure Active Directory**.
   
    d. W **adres URL wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.
   
    e. W **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.
   
    f. W **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.

    g. Otwórz z **base-64** zakodowany certyfikat w Notatniku pobrany z portalu Azure, hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat dostawcy tożsamości (metadanymi)** pole tekstowe.

    h. Wybierz **Zezwalaj funkcji logowania jednokrotnego w**.
   
    i. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a>Tworzenie użytkownika testowego Mimecast osobistych portalu

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do portalu osobiste Mimecast muszą mieć przydzielone do portalu osobiste Mimecast. W przypadku hello Mimecast osobistych portalu inicjowania obsługi administracyjnej jest zadanie ręczne.

Należy tooregister domeny, przed przystąpieniem do tworzenia użytkowników.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. Zaloguj się na tooyour **Portal osobiste Mimecast** jako administrator.

2. Przejdź za**katalogów \> wewnętrzne**.
   
    ![Katalogi](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "katalogów")

3. Kliknij przycisk **zarejestrować nową domenę**.
   
    ![Zarejestrować nową domenę](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "zarejestrować nową domenę")

4. Po utworzeniu nowej domeny, kliknij przycisk **nowy adres**.
   
    ![Nowy adres](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "nowy adres")

5. W hello nowego okna dialogowego adres i wykonaj następujące kroki prawidłowy Azure hello konta AD ma tooprovision:
   
    ![Zapisz](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Zapisz")
   
    a. W hello **adres E-mail** pole tekstowe, typ **adres E-mail** hello użytkownika jako  **BrittaSimon@contoso.com** .
    
    b. W hello **globalną nazwę** pole tekstowe, hello typu **username** jako **BrittaSimon**.

    c. W hello **hasło**, i **Potwierdź hasło** pól tekstowych, hello typu **hasło** hello użytkownika.
   
    b. Kliknij pozycję **Zapisz**.

>[!NOTE]
>Można użyć dowolnego inne narzędzia do tworzenia konta użytkownika portalu osobiste Mimecast lub interfejsów API dostarczonych przez konta użytkowników usługi Azure AD tooprovision Mimecast osobistych portalu. 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMimecast osobistych portalu.

![Przypisz użytkownika][200] 

**tooassign tooMimecast Simona Britta osobistych portalu, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Portal osobiste Mimecast**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej
W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka portalu osobiste Mimecast hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Portal osobiste Mimecast aplikacji. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

