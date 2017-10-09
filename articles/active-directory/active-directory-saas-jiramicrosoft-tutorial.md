---
title: "Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML JIRA przez firmę Microsoft | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego SAML JIRA przez firmę Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a>Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML JIRA przez firmę Microsoft

Z tego samouczka, dowiesz się, jak toointegrate logowania jednokrotnego SAML JIRA przez firmę Microsoft w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD logowania jednokrotnego SAML JIRA przez firmę Microsoft udostępnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooJIRA logowania jednokrotnego SAML przez firmę Microsoft
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooJIRA logowania jednokrotnego SAML przez firmę Microsoft (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z logowania jednokrotnego SAML JIRA przez firmę Microsoft, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Aplikacja serwera JIRA zainstalowany na serwerze Windows 64-bitowych (lokalnie lub w chmurze hello infrastrukturą IaaS)
- Serwer JIRA jest obsługujące protokół HTTPS
- Uwaga hello obsługiwane wersje dla wtyczki JIRA są wymienione w poniższej sekcji.
- JIRA serwer jest dostępny w Internecie szczególnie tooAzure dla uwierzytelniania strony logowania usługi AD i powinien tooreceive stanie hello tokenu z usługi Azure AD
- Poświadczenia administratora są konfigurowane w JIRA
- WebSudo jest wyłączona w JIRA
- Testowanie użytkowników utworzone w hello JIRA serwera aplikacji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego programu JIRA. Testowanie integracji hello najpierw w rozwoju lub przemieszczania środowisko aplikacji hello, a następnie środowiska produkcyjnego hello użycia.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="supported-versions-of-jira"></a>Obsługiwane wersje JIRA 

Od tej chwili obsługiwane są następujące wersje JIRA:

- Podstawowe JIRA i oprogramowania: 6.0 too7.2.0
- JIRA działu: 3.0 too3.2

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie z galerii hello logowania jednokrotnego SAML JIRA przez firmę Microsoft
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a>Dodawanie z galerii hello logowania jednokrotnego SAML JIRA przez firmę Microsoft
tooconfigure hello włączenia logowania jednokrotnego SAML JIRA przez firmę Microsoft do usługi Azure AD, należy tooadd logowania jednokrotnego SAML JIRA przez firmę Microsoft z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd logowania jednokrotnego SAML JIRA przez firmę Microsoft z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **logowania jednokrotnego SAML JIRA przez firmę Microsoft**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. W panelu wyników hello, wybierz **logowania jednokrotnego SAML JIRA przez firmę Microsoft**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML JIRA przez firmę Microsoft na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w logowania jednokrotnego SAML JIRA przez firmę Microsoft jest tooa użytkownika w usłudze Azure AD. Innymi słowy łącze relację między użytkownika usługi Azure AD i powiązane użytkownika logowania jednokrotnego SAML JIRA przez firmę Microsoft hello musi toobe ustanowione.

W JIRA logowania jednokrotnego SAML przez firmę Microsoft, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML JIRA przez firmę Microsoft, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie logowania jednokrotnego SAML JIRA przez użytkownika testowego Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave odpowiednikiem Simona Britta w logowania jednokrotnego SAML JIRA przez firmę Microsoft, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci logowania jednokrotnego SAML JIRA przez aplikację Microsoft.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML JIRA przez firmę Microsoft, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **logowania jednokrotnego SAML JIRA przez firmę Microsoft** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. Na powitania **logowania jednokrotnego SAML JIRA Domain firmy Microsoft i adresy URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<domain:port>/plugins/servlet/saml/auth`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<domain:port>/`

    c. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania. Port jest opcjonalny w przypadku, gdy jest nazwane adres URL. Te wartości są odbierane podczas konfigurowania hello Jira wtyczki, który znajduje się w dalszej części samouczka hello.
 
4. Witaj toogenerate **metadanych** adres url, wykonaj następujące kroki hello:

    a. Kliknij przycisk **rejestracji aplikacji**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    b. Kliknij przycisk **punkty końcowe** tooopen **punkty końcowe** okno dialogowe.  
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    c. Kliknij przycisk toocopy przycisku Kopiuj hello **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    d. Teraz przejdź strony właściwości toohello **logowania jednokrotnego SAML JIRA przez firmę Microsoft** i hello kopiowania **identyfikator aplikacji** przy użyciu **kopiowania** przycisk i wklej go do Notatnika.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    e. Generowanie hello **adres URL metadanych** przy użyciu hello następującego wzorca: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` i skopiuj tę wartość w programie Notatnik, ponieważ jest później używany dla konfiguracji hello hello wtyczki.

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. Skontaktuj się z [Microsoft](mailto:waadpartners@microsoft.com) z następujących informacji dla wtyczki JIRA hello hello.
    
    *   Nazwa klienta:
    *   Nazwa domeny głównej:
    *   Azure AD Premium: Tak/nie (wtyczka będzie, dostępne tooall powitania klienta wolne, Basic i warstwy Premium)
    *   Liczba użytkowników, którzy będą używać tej integracji:
    *   Wersja JIRA:
    *   Uwagi:

7. W oknie przeglądarki innej witryny sieci web Zaloguj się w wystąpieniu JIRA tooyour jako administrator.

8. Umieść kursor na koło zębate, a następnie kliknij przycisk hello **dodatki**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. W sekcji Karta dodatki, kliknij przycisk **Zarządzanie dodatkami**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. Ręcznie przekazać wtyczki hello obsługiwane przez firmę Microsoft. Po zainstalowaniu dodatku hello pojawia się w **użytkownik zainstalował** sekcji dodatki **zarządzania dodatkami** sekcji.

11. Kliknij przycisk **Konfiguruj** tooconfigure hello nowej wtyczki.

12. Wykonaj następujące kroki na stronie konfiguracji:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    a. W **adres URL metadanych** Wklej hello **adres URL metadanych** generowane z usługi Azure AD i kliknij przycisk hello **rozwiązać** przycisku. Adres URL metadanych IdP hello odczytuje i wypełnienie wszystkich hello pól informacji.

    > [!Note]
    > Domyślna lokalizacja SAML użytkownika identyfikator to identyfikator nazwy. Można zmienić tej opcji atrybutu tooan i wprowadź nazwę atrybutu odpowiednie hello.

    > [!TIP]
    > Upewnij się, że istnieje tylko jeden certyfikat mapowany aplikacji hello tak, aby nie było błędu rozpoznawania hello metadanych. Jeśli dostępnych jest wiele certyfikatów na rozpoznawanie metadanych hello admin pobiera wystąpił błąd.
    
    b. Kopiuj hello **identyfikator, adres URL odpowiedzi i zaloguj się na adres URL** wartości i wklej je w **identyfikator, adres URL odpowiedzi i zaloguj się na adres URL** odpowiednio do pól tekstowych **logowania jednokrotnego SAML JIRA Domain firmy Microsoft i adresy URL** sekcji z portalu Azure.

    c. W **nazwa przycisku logowania** nazwa hello typu przycisku organizacja chce hello toosee użytkowników na ekranie logowania.

    d. W **lokalizacje identyfikator użytkownika SAML** wybierz opcję **identyfikator użytkownika jest w elemencie NameIdentifier hello hello instrukcji podmiotu** lub **identyfikator użytkownika jest w elemencie atrybutu**.  Ten identyfikator ma identyfikator użytkownika JIRA hello toobe. Jeśli hello identyfikator użytkownika nie jest zgodny, następnie systemu nie zezwala na toolog użytkowników w. 
    
    e. W przypadku wybrania **identyfikator użytkownika jest w elemencie atrybutu** opcji, a następnie w **nazwa atrybutu** pole tekstowe Nazwa hello typu atrybutu hello, gdzie jest oczekiwany identyfikator użytkownika. 

    f. Jeśli używasz hello domeny federacyjnej (na przykład usług AD FS itp.) z usługą Azure AD, należy kliknąć opcję hello **Włączanie odnajdowania obszaru macierzystego** opcji i skonfigurować hello **nazwy domeny**.
    
    g. W **nazwy domeny** hello domeny tym miejscu wpisz nazwę w przypadku logowania za pomocą usług AD FS hello.

    h. Sprawdź **włączyć pojedynczego Wyloguj** Jeśli chcesz toolog się z usługą Azure AD, gdy użytkownik zaloguje z JIRA. 

    i. Kliknij przycisk **zapisać** przycisk toosave hello ustawienia.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a>Tworzenie logowania jednokrotnego SAML JIRA przez użytkownika testowego firmy Microsoft

toolog użytkowników tooenable usługi Azure AD w tooJIRA na serwerze lokalnym, ich muszą mieć przydzielone do logowania jednokrotnego SAML JIRA przez firmę Microsoft. W przypadku logowania jednokrotnego SAML JIRA przez firmę Microsoft inicjowania obsługi administracyjnej jest zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour JIRA na lokalnym serwerze jako administrator.

2. Umieść kursor na koło zębate, a następnie kliknij przycisk hello **Zarządzanie użytkownikami**.

    ![Dodawanie pracownika](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. Jesteś tooenter stronę dostępu do przekierowanych tooAdministrator **hasła** i kliknij przycisk **Potwierdź** przycisku.

    ![Dodawanie pracownika](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. W obszarze **Zarządzanie użytkownikami** sekcji, kliknij pozycję **Utwórz użytkownika**.

    ![Dodawanie pracownika](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. Na powitania **"Tworzenie nowego użytkownika"** okna dialogowego wykonaj hello następujące kroki:

    ![Dodawanie pracownika](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    a. W hello **adres E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.

    b. W hello **imię i nazwisko** tekstowym, wpisz pełną nazwę użytkownika hello jak Simona Britta.

    c. W hello **Username** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak Brittasimon@contoso.com.

    d. W hello **hasło** tekstowym, wpisz hello hasło użytkownika.

    e. Kliknij przycisk **tworzenia użytkownika**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooJIRA logowania jednokrotnego SAML przez firmę Microsoft.

![Przypisz użytkownika][200] 

**tooassign tooJIRA Simona Britta logowania jednokrotnego SAML przez firmę Microsoft, należy wykonać hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **logowania jednokrotnego SAML JIRA przez firmę Microsoft**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello logowania jednokrotnego SAML JIRA przez Microsoft kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour logowania jednokrotnego SAML JIRA przez aplikację Microsoft.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

