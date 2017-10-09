---
title: 'Samouczek: Integracji Azure Active Directory z Dropbox dla firm | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i skrzynki dla firm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a>Samouczek: Integracji Azure Active Directory z Dropbox dla firm

Z tego samouczka, dowiesz się, jak toointegrate Dropbox dla firm z usługą Azure Active Directory (Azure AD).

Integrowanie usługi Dropbox dla firm z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooDropbox dla firm
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooDropbox dla firm (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z Dropbox dla firm, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Dropbox dla firm logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie skrzynki dla firm z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-dropbox-for-business-from-hello-gallery"></a>Dodawanie skrzynki dla firm z galerii hello
integracji hello tooconfigure Dropbox dla firm z usługą Azure AD, należy tooadd Dropbox dla firm z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Dropbox dla firm z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Dropbox dla firm**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. W panelu wyników hello, wybierz **Dropbox dla firm**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Dropbox dla firm na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow w Dropbox dla firm użytkownika odpowiednikiem hello jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Dropbox dla firm musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Dropbox dla firm.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Dropbox dla firm, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie skrzynki dla użytkownika testowego firm](#creating-a-dropbox-for-business-test-user)**  -toohave odpowiednikiem Simona Britta w Dropbox dla firm, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowania jednokrotnego w usłudze Dropbox dla aplikacji biznesowych.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Dropbox dla firm, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Dropbox dla firm** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. Na powitania **Dropbox domeny biznesowych i adresów URL** sekcji, wykonaj następujące kroki hello:

    a. Zaloguj się na tooyour Dropbox dla dzierżawy biznesowych. 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "skonfigurować logowanie jednokrotne")
   
    b. W okienku nawigacji hello po lewej stronie powitania kliknij **konsoli administracyjnej**. 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "skonfigurować logowanie jednokrotne")
   
    c. Na powitania **konsoli administracyjnej**, kliknij przycisk **uwierzytelniania** w okienku nawigacji po lewej stronie powitania. 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "skonfigurować logowanie jednokrotne")
   
    d. W hello **logowanie jednokrotne** zaznacz **Włącz rejestrację jednokrotną**, a następnie kliknij przycisk **więcej** tooexpand w tej sekcji.  
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "skonfigurować logowanie jednokrotne")
   
    e. Skopiuj adres URL hello obok zbyt**użytkownicy mogą rejestrować wprowadź swój adres e-mail lub można przejść bezpośrednio do**. 
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    f. W portalu Azure w hello hello **adres URL logowania** pole tekstowe, wklej adres URL z hello.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.dropbox.com/sso/<id>`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Zaktualizuj wartość hello z hello rzeczywisty adres URL logowania otrzymasz od jednej sekcji logowania jednokrotnego. Skontaktuj się z [Dropbox dla zespołu pomocy technicznej klienta Business](https://www.dropbox.com/business/contact) tooget tej wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. Na powitania **Dropbox konfiguracji Business** , kliknij przycisk **Konfigurowanie skrzynki dla firm** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. tooconfigure rejestracji jednokrotnej w **Dropbox dla firm** po stronie znajduje się w usłudze Dropbox dla dzierżawy biznesowych, w hello **logowanie jednokrotne** sekcji hello **uwierzytelniania** strony, wykonaj następujące kroki hello: 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "skonfigurować logowanie jednokrotne")
   
    a. Kliknij przycisk **wymagane**.
   
    b. W portalu Azure na powitania hello **Konfigurowanie logowania jednokrotnego** okna, hello kopiowania **SAML pojedynczy znak na adres URL usługi** wartość, a następnie wklej go do hello **adres URL logowania** pola tekstowego.

    c. Kliknij przycisk **wybierz certyfikat**, a następnie przejdź tooyour **pliku zakodowanego certyfikatu Base64**.

    d. Kliknij przycisk **zapisać zmiany** toocomplete hello konfiguracji w usłudze DropBox dla dzierżawy biznesowych.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-dropbox-for-business-test-user"></a>Tworzenie skrzynki dla firm użytkownika testowego

W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w Dropbox dla firm. Dropbox dla firm obsługę w czasie, który jest domyślnie włączona.

Nie ma elementu akcji można w tej sekcji. Jeśli użytkownik nie istnieje w Dropbox dla firm, nowy jest tworzony podczas próby tooaccess Dropbox dla firm.

>[!Note]
>Jeśli potrzebujesz toocreate użytkownik ręcznie, skontaktuj się z [Dropbox dla zespołu pomocy technicznej klienta biznesowa](https://www.dropbox.com/business/contact) 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooDropbox dla firm.

![Przypisz użytkownika][200] 

**tooassign tooDropbox Simona Britta dla firm, wykonaj następujące kroki hello:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Dropbox dla firm**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello skrzynki dla firm kafelka w hello Panel dostępu, należy pobrać strony logowania o usłudze Dropbox dla aplikacji biznesowych.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Skonfiguruj Inicjowanie obsługi użytkowników](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

