---
title: 'Samouczek: Azure Active Directory integracji z logowaniem Jednokrotnym Kantega dla zlewiska | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego Kantega dla zlewiska."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d0d99c14-a6ca-45f2-bb84-633126095e7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: b35eb8757e41e86228a3a9ee10869086cc801c9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-confluence"></a>Samouczek: Azure Active Directory integracji z logowaniem Jednokrotnym Kantega dla zlewiska

Z tego samouczka, dowiesz się, jak toointegrate Kantega Usługa rejestracji Jednokrotnej dla zlewiska z usługi Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Kantega Usługa rejestracji Jednokrotnej dla zlewiska zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooKantega logowania jednokrotnego dla zlewiska
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooKantega logowania jednokrotnego dla zlewiska (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z logowania jednokrotnego Kantega dla zlewiska należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Kantega Usługa rejestracji Jednokrotnej dla zlewiska logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie logowania jednokrotnego Kantega dla zlewiska z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-kantega-sso-for-confluence-from-hello-gallery"></a>Dodawanie logowania jednokrotnego Kantega dla zlewiska z galerii hello
Integracja hello tooconfigure Kantega sesji rejestracji jednokrotnej dla zlewiska do usługi Azure AD, należy tooadd Kantega logowania jednokrotnego dla zlewiska z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Kantega Usługa rejestracji Jednokrotnej dla zlewiska z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Kantega Usługa rejestracji Jednokrotnej dla zlewiska**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_search.png)

5. W panelu wyników hello, wybierz **Kantega Usługa rejestracji Jednokrotnej dla zlewiska**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega dla zlewiska w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w rejestracji Jednokrotnej Kantega dla zlewiska jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w rejestracji Jednokrotnej Kantega dla zlewiska musi toobe ustanowione.

W Kantega logowania jednokrotnego dla zlewiska, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowanie usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega zlewiska, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie Kantega Usługa rejestracji Jednokrotnej dla użytkownika testowego zlewiska](#creating-a-kantega-sso-for-confluence-test-user)**  -toohave odpowiednikiem Simona Britta w rejestracji Jednokrotnej Kantega dla zlewiska, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w Twojej rejestracji Jednokrotnej Kantega zlewiska aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega dla zlewiska, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Kantega Usługa rejestracji Jednokrotnej dla zlewiska** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_samlbase.png)

3. W **IDP** inicjowane tryb na powitania **logowania jednokrotnego Kantega zlewiska domeny i adresów URL** sekcji wykonać powitania po kroku:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url1.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. W **SP** inicjowane trybie wyboru **Pokaż zaawansowane ustawienia adresu URL** i wykonywać powitania po kroku:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url2.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania. Te wartości są odbierane podczas konfigurowania hello zlewiska wtyczki, który znajduje się w dalszej części samouczka hello.

5. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_400.png)
    
7. W oknie przeglądarki innej witryny sieci web, zaloguj się za tooyour **portalu administracyjnego zlewiska** jako administrator.

8. Umieść kursor na koło zębate, a następnie kliknij przycisk hello **dodatki**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon1.png)

9. W obszarze **ATLASSIAN MARKETPLACE** , kliknij pozycję **znaleźć nowe dodatki**. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon.png)

10. Wyszukiwanie **Kantega Usługa rejestracji Jednokrotnej dla protokołu Kerberos SAML zlewiska** i kliknij przycisk **zainstalować** tooinstall przycisk hello nowej wtyczki SAML.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon2.png)

11. rozpoczyna się instalacja dodatku Hello.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon3.png)

12. Po zakończeniu instalacji hello. Kliknij przycisk **Zamknij**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon33.png)

13. Kliknij pozycję **Zarządzaj**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon34.png)
    
14. Kliknij przycisk **Konfiguruj** tooconfigure hello nowej wtyczki.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon35.png)

15. Tej nowej wtyczki można także znaleźć w obszarze **użytkowników i zabezpieczenia** kartę.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon36.png)
    
16. W hello **SAML** sekcji. Wybierz **usługi Azure Active Directory (Azure AD)** z hello **dostawcy tożsamości Dodaj** listy rozwijanej.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon4.png)

17. Wybierz poziom subskrypcji jako **podstawowe**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon5.png)       

18. Na powitania **właściwości aplikacji** sekcji, wykonaj następujące kroki: 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon6.png)

    a. Kopiuj hello **identyfikator URI aplikacji** wartości i używać go jako **identyfikator, adres URL odpowiedzi i adres URL logowania** na powitania **logowania jednokrotnego Kantega zlewiska domeny i adresów URL** sekcji w portalu Azure.

    b. Kliknij przycisk **Dalej**.

19. Na powitania **importu metadanych** sekcji, wykonaj następujące kroki: 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon7.png)

    a. Wybierz **pliku metadanych na tym komputerze**i przekazywanie pliku metadanych, który został pobrany z portalu Azure.

    b. Kliknij przycisk **Dalej**.

20. Na powitania **nazwę i logowania jednokrotnego lokalizację** sekcji, wykonaj następujące kroki:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon8.png)
    
    a. Dodaj nazwę hello dostawcy tożsamości w **Nazwa dostawcy tożsamości** pola tekstowego (np. usługi Azure AD).

    b. Kliknij przycisk **Dalej**.

21. Sprawdź hello certyfikatu podpisywania, a następnie kliknij przycisk **dalej**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon9.png)

22. Na powitania **kont użytkowników zlewiska** sekcji, wykonaj następujące kroki:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon10.png)

    a. Wybierz **tworzenie użytkowników w katalogu wewnętrzny zlewiska firmy, w razie potrzeby** , a następnie wprowadź odpowiednią nazwę hello hello grupy użytkowników (może być wiele nie. grup rozdzielone przecinkami).

    b. Kliknij przycisk **Dalej**.

23. Kliknij przycisk **Zakończ**.   

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon11.png)

24. Na powitania **znanych domeny dla usługi Azure AD** sekcji, wykonaj następujące kroki: 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon12.png)

    a. Wybierz **znane domen** z lewego panelu hello hello strony.

    b. Wprowadź nazwę domeny w hello **znane domen** pola tekstowego.

    c. Kliknij pozycję **Zapisz**. 

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-kantega-sso-for-confluence-test-user"></a>Tworzenie Kantega Usługa rejestracji Jednokrotnej dla użytkownika testowego zlewiska

toolog użytkowników tooenable usługi Azure AD w tooConfluence, muszą mieć przydzielone do zlewiska. W przypadku hello Kantega sesji rejestracji jednokrotnej dla zlewiska Inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour logowania jednokrotnego Kantega zlewiska witryny firmy jako administrator.

2. Umieść kursor na koło zębate, a następnie kliknij przycisk hello **Zarządzanie użytkownikami**.

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforconfluence-tutorial/user1.png) 

3. W sekcji Użytkownicy kliknij **Dodaj użytkowników** kartę. Na powitania **"Dodaj użytkownika"** okna dialogowego wykonaj hello następujące kroki:

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforconfluence-tutorial/user2.png) 

    a. W hello **Username** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak Brittasimon@contoso.com.

    b. W hello **imię i nazwisko** pole tekstowe, typ hello pełną nazwę użytkownika, takich jak Simona Britta.

    c. W hello **E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.

    d. W hello **hasło** tekstowym, wpisz hello hasło dla użytkownika.

    e. Kliknij przycisk **Potwierdź hasło** ponownie hello hasła.
    
    f. Kliknij przycisk **Dodaj** przycisku.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooKantega logowania jednokrotnego dla zlewiska.

![Przypisz użytkownika][200] 

**tooassign tooKantega Simona Britta logowania jednokrotnego dla zlewiska, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Kantega Usługa rejestracji Jednokrotnej dla zlewiska**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello Kantega logowania jednokrotnego dla zlewiska kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Kantega logowania jednokrotnego dla aplikacji zlewiska.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_203.png

