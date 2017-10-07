---
title: 'Samouczek: Integracji Azure Active Directory z pomocy Scout | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Scout pomocy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a>Samouczek: Integracji Azure Active Directory z Scout pomocy

Z tego samouczka dowiesz się, jak toointegrate pomóc Scout w usłudze Azure Active Directory (Azure AD).

Możesz uzyskać hello następujące korzyści z integracji z usługą Azure AD Scout pomocy:

- W usłudze Azure AD można kontrolować, kto ma dostęp do tooHelp Scout.
- W Twojej tooHelp użytkowników Scout może automatycznie podpisywać za pomocą rejestracji jednokrotnej i konta usługi Azure AD.
- Możesz zarządzać kont w jednej, centralnej lokalizacji, hello portalu Azure.

toolearn więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooset się integracji usługi Azure AD z Scout pomocy, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Subskrypcja Scout pomocy, z logowanie jednokrotne włączone 

> [!NOTE]
> W przypadku testowania czynności hello w tym samouczku, zaleca się nie przetestować ich w środowisku produkcyjnym.

Zalecenia dotyczące testowania czynności hello w tym samouczku:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [Pobierz bezpłatną wersję próbną miesięcznego](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. 

Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodaj Scout pomocy z galerii hello.
2. Instalowanie i testowanie usługi Azure AD rejestracji jednokrotnej.

## <a name="add-help-scout-from-hello-gallery"></a>Dodawanie pomocy Scout z galerii hello
tooset się hello integracji Pomocy Scout z usługą Azure AD w galerii hello Dodaj pomocy Scout tooyour listę zarządzanych aplikacji SaaS.

tooadd pomocy Scout z galerii hello:

1. W hello [portalu Azure](https://portal.azure.com), w menu po lewej stronie Witaj, wybierz **usługi Azure Active Directory**. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.

    ![Strona aplikacji Hello Enterprise][2]
    
3. tooadd nowej aplikacji, wybierz **nowej aplikacji**.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **pomocy Scout**. W wynikach wyszukiwania hello, wybierz **pomocy Scout**, a następnie wybierz **Dodaj**.

    ![Pomoc Scout hello listy wyników](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a>Instalowanie i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji możesz zdefiniować i test usługi Azure AD rejestracji jednokrotnej z Scout pomoc w oparciu o nazwie użytkownika testowego *Simona Britta*.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello Azure AD odpowiednikiem użytkownika w Scout pomocy. Należy ustanowić relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Scout pomocy.

Witaj tooestablish łączy relacji w pomocy Scout dla **Username**, przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z pomocy Scout pełną hello następujące zadania:

1. [Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#set-up-azure-ad-single-sign-on). Konfiguruje toouse użytkownika tej funkcji.
2. [Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user). Testy usługi Azure AD rejestracji jednokrotnej z użytkownikiem hello Simona Britta.
3. [Tworzenie użytkownika testowego pomocy Scout](#create-a-help-scout-test-user). Tworzy odpowiednikiem Simona Britta Scout pomocy, który jest połączony toohello reprezentacja hello użytkownika usługi Azure AD.
4. [Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user). Konfiguruje toouse Simona Britta usługi Azure AD rejestracji jednokrotnej.
5. [Test rejestracji jednokrotnej](#test-single-sign-on). Sprawdza, czy konfiguracja tego hello działa.

### <a name="set-up-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można skonfigurować usługi Azure AD rejestracji jednokrotnej w hello portalu Azure. Następnie skonfigurowaniu rejestracji jednokrotnej w aplikacji Scout pomocy.

tooset się usługi Azure AD rejestracji jednokrotnej z Scout pomocy:

1. W portalu Azure na powitania hello **pomocy Scout** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.
 
    ![Konfigurowanie łącza rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** strony, dla **tryb**, wybierz pozycję **na języku SAML logowania jednokrotnego**.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. W obszarze **pomocy domeny Scout i adres URL**, jeśli chcesz tooset się hello aplikację w trybie inicjowanych przez dostawców tożsamości, pełną hello następujące kroki:

    1. W hello **identyfikator** wprowadź adres URL, który ma hello następującego wzorca:`urn:auth0:helpscout:<instancename>`

    2. W hello **adres URL odpowiedzi** wprowadź adres URL, który ma hello następującego wzorca:`https://helpscout.auth0.com/login/callback?connection=<instancename>`

    ![Adresy URL i domeny Scout pojedynczego logowania jednokrotnego informacje pomocy](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. Tooset się hello aplikację w trybie zainicjował SP, zaznacz hello **Pokaż zaawansowane ustawienia adresu URL** pole wyboru, a następnie hello następujące:

    * W hello **Zaloguj się na adres URL** wprowadź adres URL, który ma hello następującego formatu:`https://secure.helpscout.net/members/login/`

    ![Adresy URL i domeny Scout pojedynczego logowania jednokrotnego informacje pomocy](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > wartości Hello w tych adresów URL dotyczą tylko pokaz. Zaktualizuj wartości hello hello rzeczywisty identyfikator URL i adresu URL odpowiedzi. Skontaktuj się z tych wartości, tooget [Scout pomoc techniczną](mailto:help@helpscout.com). 

5. W obszarze **certyfikat podpisywania SAML**, wybierz pozycję **XML metadanych**, a następnie zapisz plik metadanych hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. Wybierz pozycję **Zapisz**.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. tooset się jednym logowania po stronie pomocy Scout hello, Wyślij toohello pliku XML metadanych hello pobrane [Scout pomoc techniczną](mailto:help@helpscout.com). zespołem pomocy technicznej pomocy Scout Hello dotyczy to ustawienie, aby hello SAML logowania jednokrotnego połączenie jest prawidłowo po obu stronach.

> [!TIP]
> Możesz przeczytać zwięzły wersji tych instrukcji w hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji! Po dodaniu aplikacji hello wybierając **usługi Active Directory** > **aplikacje dla przedsiębiorstw**, wybierz pozycję hello **rejestracji jednokrotnej** kartę. Dostęp można uzyskać dokumentację hello osadzone w hello **konfiguracji** sekcji u dołu hello hello strony. Aby uzyskać więcej informacji, zobacz [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

W tej sekcji w hello portalu Azure utworzysz użytkownika testu o nazwie Simona Britta.

![Tworzenie użytkownika testowego usługi Azure AD][100]

toocreate użytkownika testowego w usłudze Azure AD:

1. W portalu Azure, w menu po lewej stronie powitania hello wybierz **usługi Azure Active Directory**.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, wybierz opcję **użytkowników i grup**, a następnie wybierz **wszyscy użytkownicy**.

    ![Wybierz użytkowników i grup, a następnie wybierz opcję Wszyscy użytkownicy](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe u góry hello hello **wszyscy użytkownicy** wybierz pozycję **Dodaj**.

    ![przycisk Dodaj Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okno dialogowe, pełną hello następujące kroki:

    1. W hello **nazwa** wprowadź **BrittaSimon**.

    2. W hello **nazwy użytkownika** wprowadź adres e-mail użytkownika Simona Britta hello.

    3. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    4. Wybierz pozycję **Utwórz**.

        ![okno dialogowe Hello użytkownika](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a>Tworzenie użytkownika testowego Scout pomocy

Witaj w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Scout pomocy. Pomoc Scout obsługuje just in time (JIT) inicjowania obsługi, które jest domyślnie włączona.

W tej sekcji nie ma żadnych toocomplete akcji lub zadań. Jeśli użytkownik nie istnieje w pomocy Scout, nowy jest tworzony podczas próby tooaccess Scout pomocy.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz umożliwia użytkownikowi hello Simona Britta toouse usługi Azure AD rejestracji jednokrotnej, przyznając hello użytkownika konta dostępu tooHelp Scout.

![Przypisanie roli użytkownika hello][200] 

tooassign tooHelp Simona Britta Scout:

1. W portalu Azure hello Otwórz widok aplikacji hello, a następnie przejdź toohello widok katalogu. Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **pomocy Scout**.

    ![łącza pomocy Scout Hello na liście aplikacji hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. W menu po lewej stronie powitania wybierz **użytkowników i grup**.

    ![Hello użytkowników i grup łącza][202]

4. Wybierz pozycję **Dodaj**. Następnie na powitania **Dodaj przydziału** wybierz pozycję **użytkowników i grup**.

    ![Okienko Dodaj przypisania Hello][203]

5. Na powitania **użytkowników i grup** strony w hello listę użytkowników, wybierz opcję **Simona Britta**.

6. Na powitania **użytkowników i grup** wybierz pozycję **wybierz**.

7. Na powitania **Dodaj przydziału** wybierz pozycję **przypisać**.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować przy użyciu panelu dostępu hello konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego.

Po wybraniu kafelka pomocy Scout hello w panelu dostępu hello powinny być automatycznie zalogowano tooyour pomocy Scout aplikacji.

Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [panelu dostępu toohello wprowadzenie](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

