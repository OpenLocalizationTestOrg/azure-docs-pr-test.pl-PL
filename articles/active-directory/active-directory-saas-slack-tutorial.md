---
title: 'Samouczek: Integracji Azure Active Directory z zapas czasu | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i zapas czasu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a>Samouczek: Integracji Azure Active Directory z zapas czasu

Z tego samouczka, dowiesz się, jak toointegrate Slack z usługą Azure Active Directory (Azure AD).

Integrowanie zapas czasu z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSlack
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSlack (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z zapas czasu, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Slack logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie zapas czasu z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-slack-from-hello-gallery"></a>Dodawanie zapas czasu z galerii hello
integracji hello tooconfigure zapas czasu w usłudze Azure Active Directory, należy tooadd zapas czasu z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd zapas czasu z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Slack**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. W panelu wyników hello zaznacz **zapas czasu**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zapas czasu, w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w zapas czasu jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w zapas czasu musi toobe ustanowione.

W zapas czasu, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z zapas czasu, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Slack](#creating-a-slack-test-user)**  -toohave odpowiednikiem Simona Britta w zapas czasu, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne Slack aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z zapas czasu, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Slack** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. Na powitania **domeny zapas czasu i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.slack.com`

    b. W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://slack.com`

    > [!NOTE] 
    > wartość Hello nie jest prawdziwe. Masz tooupdate hello wartości z hello rzeczywiste na adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej Slack](https://slack.com/help/contact) tooget hello wartość
     
4. Slack aplikacji oczekuje potwierdzenia SAML hello w określonym formacie. Skonfiguruj powitania po oświadczeń dla tej aplikacji. Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji. powitania po zrzut ekranu przedstawia przykład tego.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **user.mail** jako **identyfikator użytkownika** i dla każdego wiersza wyświetlany w poniższej tabeli hello wykonaj następujące kroki hello:
    
    | Nazwa atrybutu | Wartość atrybutu |
    | --- | --- |
    | Imię | User.givenName |
    | nazwisko | User.surname |
    | User.Email | User.mail |  
    | User.Username | User.userPrincipalName |

    a. Polecenie **atrybutu** tooopen **atrybutu Edytuj** okna dialogowego pole i wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    a. W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.
    
    b. Z hello **wartość** lista, hello wybierz atrybut wyświetlany dla danego wiersza.
    
    c. Kliknij przycisk **OK**.

6. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. Na powitania **konfiguracji zapas czasu** kliknij **skonfigurować zapas czasu** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Slack tooyour jako administrator.

10.  Przejdź za**usługi Microsoft Azure AD** Przejdź zbyt**ustawień zespołu**.

     ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  W hello **ustawień zespołu** kliknij hello **uwierzytelniania** , a następnie kliknij pozycję **Zmień ustawienia**.

     ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. Na powitania **ustawienia uwierzytelniania SAML** okna dialogowego, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    a.  W hello **SAML 2.0 punktu końcowego (HTTP)** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.

    b.  W hello **wystawcy dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.

    c.  Otwórz plik certyfikatu pobrane w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu publicznego** pola tekstowego.

    d. Skonfiguruj hello powyżej trzy ustawienia odpowiednie dla swojego zespołu Slack. Aby uzyskać więcej informacji na temat ustawień hello Znajdź hello **Przewodnik po konfiguracji logowania jednokrotnego zapas czasu jego** tutaj. `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    e.  Kliknij przycisk **Zapisz konfigurację**.
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-slack-test-user"></a>Tworzenie użytkownika testowego Slack

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Slack. Zapas czasu obsługę w czasie, który jest domyślnie włączone.

Nie ma elementu akcji można w tej sekcji. Nowy użytkownik został utworzony podczas tooaccess próba zapas czasu, jeśli go jeszcze nie istnieje.

> [!NOTE]
> Jeśli potrzebujesz ręcznie toocreate użytkownika, należy tooContact [zespołem pomocy technicznej Slack](https://slack.com/help/contact).

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSlack.

![Przypisz użytkownika][200] 

**tooassign tooSlack Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Slack**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Slack hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Slack aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

