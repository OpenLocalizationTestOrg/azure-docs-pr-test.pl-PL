---
title: 'Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: fe50636709857ec49023e24bdc8c6cd8c58e3c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a>Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH

Z tego samouczka, dowiesz się, jak toointegrate logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH w usłudze Azure Active Directory (Azure AD).

Integrowanie logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooSAML logowania jednokrotnego dla zlewiska przez rozpoznawania GmbH
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSAML logowania jednokrotnego dla zlewiska przez rozpoznawania GmbH (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Logowania jednokrotnego SAML dla zlewiska przez rozpoznawanie jednokrotnego GmbH w subskrypcji włączone

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie logowania jednokrotnego SAML dla zlewiska przy rozdzielczości GmbH z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-hello-gallery"></a>Dodawanie logowania jednokrotnego SAML dla zlewiska przy rozdzielczości GmbH z galerii hello

tooconfigure hello włączenia logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH do usługi Azure AD, należy tooadd logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. W panelu wyników hello, wybierz **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla zlewiska przez rozdzielczość GmbH oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika używanego w logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH musi toobe ustanowione.

W logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowanie usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie logowania jednokrotnego SAML dla zlewiska przez użytkownika testowego GmbH rozpoznawania](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  -toohave odpowiednikiem Simona Britta w logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci logowania jednokrotnego SAML dla zlewiska przy rozpoznawania GmbH aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. Na powitania **logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH domeny i adresów URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**. Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania. Skontaktuj się z [zespołu obsługi logowania jednokrotnego SAML dla zlewiska przez rozpoznawania klienta GmbH](https://www.resolution.de/go/support) tooget tych wartości. 

5. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. W oknie przeglądarki innej witryny sieci web, zaloguj się za tooyour **logowania jednokrotnego SAML dla zlewiska przez portal administracyjny GmbH rozpoznawania** jako administrator.

8. Umieść kursor na koło zębate, a następnie kliknij przycisk hello **dodatki**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. Jesteś przekierowanego tooAdministrator dostępu do strony. Wprowadź hasło hello, a następnie kliknij przycisk **Potwierdź** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. W obszarze **ATLASSIAN MARKETPLACE** , kliknij pozycję **znaleźć nowe dodatki**. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. Wyszukiwanie **SAML pojedynczy znak na rejestracji jednokrotnej (SSO) dla zlewiska** i kliknij przycisk **zainstalować** tooinstall przycisk hello nowej wtyczki SAML.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. Instalacja dodatku Hello rozpocznie. Kliknij przycisk **Zamknij**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. Kliknij pozycję **Zarządzaj**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. Kliknij przycisk **Konfiguruj** tooconfigure hello nowej wtyczki.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. Tej nowej wtyczki można także znaleźć w obszarze **użytkowników i zabezpieczenia** kartę.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. Na **konfiguracji wtyczki SingleSignOn SAML** kliknij przycisk **dodać dodatkowe dostawcy tożsamości** przycisk tooconfigure hello ustawienia dostawcy tożsamości.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. Wykonaj następujące kroki na tej stronie:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    a. Dodaj **nazwa** z hello dostawcy tożsamości (np. usługi Azure AD).
    
    b. Dodaj **opis** z hello dostawcy tożsamości (np. usługi Azure AD).

    c. Kliknij przycisk **XML** i wybierz hello **metadanych** pliku, który został pobrany z portalu Azure.

    d. Kliknij przycisk **obciążenia** przycisku.

    e. Odczytuje hello IdP metadanych i wypełni pola hello jak wyróżniono hello zrzucie ekranu.   
18. Kliknij przycisk **Zapisz ustawienia** przycisk toosave hello ustawienia.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a>Tworzenie logowania jednokrotnego SAML dla zlewiska przez użytkownika testowego GmbH rozwiązania

toolog użytkowników tooenable usługi Azure AD w tooSAML logowania jednokrotnego dla zlewiska przez rozpoznawania GmbH one muszą mieć przydzielone do logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH.  
W logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH Inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour logowania jednokrotnego SAML dla zlewiska przez witrynę firmy GmbH rozpoznawania jako administrator.

2. Umieść kursor na koło zębate, a następnie kliknij przycisk hello **Zarządzanie użytkownikami**.

    ![Dodawanie pracownika](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. W sekcji Użytkownicy kliknij **dodawania użytkowników** kartę. Na powitania **"Dodaj użytkownika"** okna dialogowego wykonaj hello następujące kroki:

    ![Dodawanie pracownika](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    a. W hello **Username** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Simona Britta.

    b. W hello **imię i nazwisko** pole tekstowe, typ hello pełną nazwę użytkownika, takich jak Simona Britta.

    c. W hello **E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.

    d. W hello **hasło** tekstowym, wpisz hasło powitania dla Simona Britta.

    e. Kliknij przycisk **Potwierdź hasło** ponownie hello hasła.
    
    f. Kliknij przycisk **Dodaj** przycisku.    

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSAML logowania jednokrotnego dla zlewiska przez rozpoznawania GmbH.

![Przypisz użytkownika][200] 

**tooassign Simona Britta tooSAML logowania jednokrotnego dla zlewiska przez rozpoznawania GmbH, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

