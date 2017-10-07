---
title: 'Samouczek: Integracji Azure Active Directory z obrazu przekazywania | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i przekazywania obrazu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a>Samouczek: Integracji Azure Active Directory z przekaźnika obrazu

Z tego samouczka, dowiesz się, jak toointegrate przekazywania obrazu w usłudze Azure Active Directory (Azure AD).

Integrowanie przekazywania obrazu z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooImage przekazywania
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooImage przekazywania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z przekaźnika obrazu należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Obraz przekazywania logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie obrazu przekazywania z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-image-relay-from-hello-gallery"></a>Dodawanie obrazu przekazywania z galerii hello
tooconfigure hello integrację przekaźnika obrazu usługi Azure AD, należy tooadd przekazywania obrazu z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd przekazywania obrazu z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **przekazywania obrazu**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. W panelu wyników hello, wybierz **przekazywania obrazu**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przekaźnika obraz w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w przekazywania obrazu jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w przekazywania obrazu musi toobe ustanowione.

W przekazywania obrazu, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z przekaźnika obrazu, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego przekazywania obrazu](#creating-an-image-relay-test-user)**  -toohave odpowiednikiem Simona Britta w przekazywania obrazu, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji przekaźnika obrazu.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z obrazu przekazywania, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **przekazywania obrazu** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. Na powitania **obrazu przekazywania domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.imagerelay.com/`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.imagerelay.com/sso/metadata`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta przekazywania obrazu](http://support.imagerelay.com/) tooget tych wartości. 
 


4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. Na powitania **Konfiguracja przekazywania obrazu** kliknij **Konfigurowanie przekazywania obrazu** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL usługi i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. W innym oknie przeglądarki Zaloguj się w witrynie firmy przekazywania obrazu tooyour jako administrator.

8. Witaj pasku narzędzi u góry hello, kliknij przycisk hello **użytkowników i uprawnienia** obciążenia.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. Kliknij przycisk **utworzyć nowe uprawnienie**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. W hello **pojedynczy znak na ustawienia** obciążenie, wybierz hello **tej grupie można tylko logowania za pomocą rejestracji jednokrotnej** pole wyboru, a następnie kliknij przycisk **zapisać**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. Przejdź za**ustawienia konta**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. Przejdź toohello **pojedynczy znak na ustawienia** obciążenia.
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. Na powitania **ustawienia SAML** okna dialogowego, wykonaj następujące kroki hello:
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    a. W **adres URL logowania** pole tekstowe, Wklej wartość hello **pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.

    b. W **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **pojedynczy adres URL usługi Sign-Out** którego została skopiowana z portalu Azure.

    c. Jako **Format identyfikatora nazwy**, wybierz pozycję **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.

    d. Jako **powiązanie opcje dla żądań z hello dostawcy usług (obraz przekazywania)**, wybierz pozycję **powiązanie POST**.

    e. W obszarze **certyfikatu x.509**, kliknij przycisk **certyfikatu aktualizacji**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    f. Otwórz w Notatniku hello pobrany certyfikat, skopiuj zawartość hello i wklej go w pole tekstowe certyfikatu x.509 hello.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    g. W **Inicjowanie obsługi użytkowników just in Time** sekcji, wybierz hello **włączyć just in Time Inicjowanie obsługi użytkowników**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    h. Grupy uprawnień wybierz hello (na przykład **logowania jednokrotnego podstawowe**) co jest dozwolone toosign w tylko za pośrednictwem rejestracji jednokrotnej.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    i. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-image-relay-test-user"></a>Tworzenie użytkownika testowego przekazywania obrazu

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w przekazywania obrazu.

**toocreate użytkownika o nazwie Simona Britta w przekazywania obrazu, należy wykonać hello następujące kroki:**

1. Logowania jednokrotnego tooyour przekazywania obrazu witryny firmy jako administrator.

2. Przejdź za**użytkowników i uprawnienia** i wybierz **Tworzenie użytkownika logowania jednokrotnego**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. Wprowadź hello **E-mail**, **imię**, **nazwisko**, i **firmy** hello użytkownika ma tooprovision i wybierz hello uprawnień grupy (na przykład logowania jednokrotnego podstawowe) czyli hello grupę, której można zalogować się tylko za pośrednictwem rejestracji jednokrotnej.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. Kliknij przycisk **Utwórz**.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooImage przekazywania.

![Przypisz użytkownika][200] 

**tooassign tooImage Simona Britta przekazywania, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **przekazywania obrazu**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.    

Po kliknięciu kafelka przekazywania obraz powitania w hello panelu dostępu, należy pobrać automatycznie zalogowane tooyour obrazu przekazywania aplikacji.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

