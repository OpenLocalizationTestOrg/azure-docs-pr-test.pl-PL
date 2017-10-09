---
title: 'Samouczek: Azure Active Directory integracji z oprogramowaniem Rally | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między oprogramowaniem Rally i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a>Samouczek: Azure Active Directory integracji z oprogramowaniem Rally

Z tego samouczka, dowiesz się, jak toointegrate Rally oprogramowania z usługą Azure Active Directory (Azure AD).

Integrowanie Rally oprogramowania z usługi Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooRally oprogramowania.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooRally oprogramowania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z oprogramowaniem Rally należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Oprogramowanie Rally logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie oprogramowania Rally z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-rally-software-from-hello-gallery"></a>Dodawanie oprogramowania Rally z galerii hello
tooconfigure hello integracji Rally oprogramowania do usługi Azure AD, należy tooadd Rally oprogramowania z listy tooyour galerii hello zarządzanych aplikacji SaaS.

**tooadd Rally oprogramowania z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **Rally oprogramowania**, wybierz pozycję **Rally oprogramowania** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Rally oprogramowania hello listy wyników](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Rally w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello Rally oprogramowania jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w oprogramowaniu Rally musi toobe ustanowione.

Rally oprogramowania, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Rally, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Rally oprogramowania](#create-a-rally-software-test-user)**  -toohave odpowiednikiem Simona Britta Rally oprogramowania, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji Rally oprogramowania.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Rally, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **Rally oprogramowania** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. Na powitania **Rally domeny oprogramowania i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Rally domeny oprogramowania i adres URL pojedynczego logowania jednokrotnego informacji](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.rally.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.rally.com`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta oprogramowania Rally](https://help.rallydev.com/) tooget tych wartości. 
 


4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. Na powitania **Rally konfiguracji oprogramowania** kliknij **Konfigurowanie oprogramowania Rally** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopia hello **Sign-Out adresu URL i identyfikator jednostki SAML** z hello **sekcji krótkimi opisami.**

    ![Rally konfiguracji oprogramowania](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. Zaloguj się za tooyour **Rally oprogramowania** dzierżawy.

8. Witaj pasku narzędzi u góry hello, kliknij przycisk **Instalatora**, a następnie wybierz **subskrypcji**.
   
    ![Subskrypcja](./media/active-directory-saas-rally-software-tutorial/ic769531.png "subskrypcji")

9. Kliknij przycisk hello **akcji** przycisku. Wybierz **edytować subskrypcji** na powitania górnym rogu paska narzędzi hello.

10. Na powitania **subskrypcji** strony okna dialogowego, wykonaj następujące kroki hello, a następnie kliknij **Zapisz i Zamknij**:
   
    ![Uwierzytelnianie](./media/active-directory-saas-rally-software-tutorial/ic769542.png "uwierzytelniania")
   
    a. Wybierz **uwierzytelniania Rally lub logowania jednokrotnego** z listy rozwijanej uwierzytelniania.

    b. W hello **adres URL dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure. 

    c. W hello **wylogowania logowania jednokrotnego** pole tekstowe, Wklej hello wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-rally-software-test-user"></a>Tworzenie użytkownika testowego Rally oprogramowania

Dla usługi Azure AD użytkownicy toobe stanie toosign w muszą być elastycznie toohello Rally aplikacji przy użyciu nazwy użytkowników usługi Azure Active Directory.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. Zaloguj się za tooyour dzierżawy Rally oprogramowania.

2. Przejdź za**Instalator \> użytkowników**, a następnie kliknij przycisk **+ Dodaj nowy**.
   
    ![Użytkownicy](./media/active-directory-saas-rally-software-tutorial/ic781039.png "użytkowników")

3. Wpisz nazwę hello w hello nowego użytkownika w polu tekstowym, a następnie kliknij przycisk **Dodaj szczegóły**.

4. W hello **Tworzenie użytkownika** sekcji, wykonaj następujące kroki hello:
   
    ![Utwórz użytkownika](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Tworzenie użytkownika")

    a. W hello **nazwy użytkownika** pole tekstowe, nazwę użytkownika, takie jak hello typu **Brittsimon**.
   
    b. W **adres E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .

    c. W **imię** tekst Wprowadź hello imię użytkownika, takich jak **Britta**.

    d. W **nazwisko** tekst Wprowadź hello nazwisko użytkownika, takich jak **Simona**.

    e. Kliknij przycisk **Zapisz i Zamknij**.

   >[!NOTE]
   >Możesz użyć innych Rally oprogramowania użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Rally oprogramowania kont użytkowników usługi Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooRally oprogramowania.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooRally Simona Britta oprogramowania, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Rally oprogramowania**.

    ![łącze Rally oprogramowania Hello na liście aplikacji hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.

Po kliknięciu kafelka Rally oprogramowania hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Rally aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

