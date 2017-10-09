---
title: 'Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a>Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH

Z tego samouczka, dowiesz się, jak toointegrate logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH w usłudze Azure Active Directory (Azure AD).

Integrowanie logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD mającego tooSAML dostępu logowania jednokrotnego dla Jira przez rozpoznawania GmbH
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSAML logowania jednokrotnego dla Jira rozpoznawania GmbH (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Logowania jednokrotnego SAML dla Jira przez rozpoznawanie jednokrotnego GmbH w subskrypcji włączone

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie logowania jednokrotnego SAML dla Jira przy rozdzielczości GmbH z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a>Dodawanie logowania jednokrotnego SAML dla Jira przy rozdzielczości GmbH z galerii hello
tooconfigure hello włączenia logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH do usługi Azure AD, należy tooadd logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. W panelu wyników hello, wybierz **logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla Jira przez rozdzielczość GmbH oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika używanego w logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH musi toobe ustanowione.

W logowania jednokrotnego SAML Jira przez rozpoznawania GmbH, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowanie usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML Jira przez rozpoznawania GmbH, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie logowania jednokrotnego SAML dla Jira przez użytkownika testowego GmbH rozpoznawania](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave odpowiednikiem Simona Britta w logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci logowania jednokrotnego SAML dla Jira przy rozpoznawania GmbH aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. Na powitania **logowania jednokrotnego SAML Jira przez rozpoznawania GmbH domeny i adresów URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**. Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania. Skontaktuj się z [zespołu obsługi logowania jednokrotnego SAML dla Jira przez rozpoznawania klienta GmbH](https://www.resolution.de/go/support) tooget tych wartości. 

5. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. W oknie przeglądarki innej witryny sieci web, zaloguj się za tooyour **logowania jednokrotnego SAML dla Jira przez portal administracyjny GmbH rozpoznawania** jako administrator.

8. Umieść kursor na koło zębate, a następnie kliknij przycisk hello **dodatki**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. Jesteś przekierowanego tooAdministrator dostępu do strony. Wprowadź hello **hasło** i kliknij przycisk **Potwierdź** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. W sekcji Karta dodatki, kliknij przycisk **znaleźć nowe dodatki**. Wyszukiwanie **SAML pojedynczy znak na rejestracji jednokrotnej (SSO) dla JIRA** i kliknij przycisk **zainstalować** tooinstall przycisk hello nowej wtyczki SAML.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. Instalacja dodatku Hello rozpocznie. Kliknij przycisk **Zamknij**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. Kliknij pozycję **Zarządzaj**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. Kliknij przycisk **Konfiguruj** tooconfigure hello nowej wtyczki.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. Na **konfiguracji wtyczki SingleSignOn SAML** kliknij przycisk **dodać dodatkowe dostawcy tożsamości** przycisk tooconfigure hello ustawienia dostawcy tożsamości.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. Wykonaj następujące kroki na tej stronie:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    a. Dodaj **nazwa** z hello dostawcy tożsamości (np. usługi Azure AD).
    
    b. Dodaj **opis** z hello dostawcy tożsamości (np. usługi Azure AD).

    c. Kliknij przycisk **XML** i wybierz hello **metadanych** pliku, który został pobrany z portalu Azure.

    d. Kliknij przycisk **obciążenia** przycisku.

    e. Odczytuje hello IdP metadanych i wypełni pola hello jak wyróżniono hello zrzucie ekranu.   

16. Kliknij przycisk **Zapisz ustawienia** przycisk toosave hello ustawienia.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a>Tworzenie logowania jednokrotnego SAML dla Jira przez użytkownika testowego GmbH rozwiązania

toolog użytkowników tooenable usługi Azure AD w tooSAML logowania jednokrotnego dla Jira przez rozpoznawania GmbH one muszą mieć przydzielone do logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH.  
W logowania jednokrotnego SAML Jira przez rozpoznawania GmbH Inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour logowania jednokrotnego SAML dla Jira przez witrynę firmy GmbH rozpoznawania jako administrator.

2. Umieść kursor na koło zębate, a następnie kliknij przycisk hello **Zarządzanie użytkownikami**.

    ![Dodawanie pracownika](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. Jesteś tooenter stronę dostępu do przekierowanych tooAdministrator **hasła** i kliknij przycisk **Potwierdź** przycisku.

    ![Dodawanie pracownika](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. W obszarze **Zarządzanie użytkownikami** sekcji, kliknij pozycję **Utwórz użytkownika**.

    ![Dodawanie pracownika](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. Na powitania **"Tworzenie nowego użytkownika"** okna dialogowego wykonaj hello następujące kroki:

    ![Dodawanie pracownika](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    a. W hello **adres E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.

    b. W hello **imię i nazwisko** tekstowym, wpisz pełną nazwę użytkownika hello jak Simona Britta.

    c. W hello **Username** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak Brittasimon@contoso.com.

    d. W hello **hasło** tekstowym, wpisz hello hasło użytkownika.

    e. Kliknij przycisk **tworzenia użytkownika**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSAML logowania jednokrotnego dla Jira przez rozpoznawania GmbH.

![Przypisz użytkownika][200] 

**tooassign Simona Britta tooSAML logowania jednokrotnego dla Jira przez rozpoznawania GmbH, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

