---
title: "Samouczek: Integracji Azure Active Directory z usługi ServiceNow | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi ServiceNow i usługi ServiceNow Express."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>Samouczek: Integracji Azure Active Directory z usługi ServiceNow
Z tego samouczka, dowiesz się, jak toointegrate usługi ServiceNow i Express usługi ServiceNow z usługą Azure Active Directory (Azure AD).

Integrowanie usługi ServiceNow i Express usługi ServiceNow z usługą Azure AD zapewnia hello następujące korzyści:

* Można kontrolować w usłudze Azure AD, kto ma dostęp tooServiceNow oraz usługi ServiceNow Express
* Użytkownicy tooautomatically get zalogowane tooServiceNow, a usługi ServiceNow Express (logowanie jednokrotne) można włączyć przy użyciu ich kont usługi Azure AD
* Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne
tooconfigure integracji usługi Azure AD z usługi ServiceNow i usługi ServiceNow Express należy hello następujące elementy:

* Subskrypcję usługi Azure AD
* Dla usługi ServiceNow, wystąpienie lub dzierżawy usługi ServiceNow, wersja Calgary lub nowszej
* Usługi ServiceNow Express, wystąpienie usługi ServiceNow Express, wersja Helsinkach lub nowszej
* Dzierżawca usługi ServiceNow Hello musi mieć hello [wielu pojedynczy znak na dodatek dostawcy](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) włączone. Można to zrobić [przesyłanie żądania obsługi](https://hi.service-now.com). 

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.
> 
> 

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

* Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
* Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie usługi ServiceNow z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne dla usługi ServiceNow lub usługi ServiceNow Express

## <a name="adding-servicenow-from-hello-gallery"></a>Dodawanie usługi ServiceNow z galerii hello
tooconfigure hello integracji usługi ServiceNow lub Express usługi ServiceNow z usługą Azure AD, należy tooadd usługi ServiceNow z hello galerii tooyour listę zarządzanych aplikacji SaaS. 

**tooadd usługi ServiceNow z galerii hello wykonaj hello następujące kroki:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**. 
   
    ![Usługa Active Directory][1]
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Aplikacje][2]
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Aplikacje][3]
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
    ![Aplikacje][4]
6. W polu wyszukiwania hello wpisz **ServiceNow**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. Wybierz w okienku wyników hello **ServiceNow**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z usługi ServiceNow lub Express usługi ServiceNow w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w ServiceNow jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w usługi ServiceNow musi toobe ustanowione.
Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w usługi ServiceNow. tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usługi ServiceNow, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej dla usługi ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Konfigurowanie usługi Azure AD logowania jednokrotnego usługi ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable Twojego toouse użytkowników tej funkcji.
3. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
4. **[Tworzenie użytkownika testowego usługi ServiceNow](#creating-a-servicenow-test-user)**  -toohave odpowiednikiem Simona Britta w usługi ServiceNow, że jego reprezentacja toohello połączonej usługi Azure AD.
5. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
6. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

> [!NOTE]
> Jeśli chcesz, aby tooconfigure ServiceNow pominąć krok 2. Podobnie jeśli chcesz, aby tooconfigure Express usługi ServiceNow pominąć krok 1.
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej dla usługi ServiceNow
1. W klasycznym portalu usługi Azure AD hello na powitania **ServiceNow** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okna dialogowego .
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749323.png "skonfigurować logowanie jednokrotne")

2. Na powitania **jak ma toosign użytkowników na tooServiceNow** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749324.png "skonfigurować logowanie jednokrotne")

3. Na powitania **Konfigurowanie ustawień aplikacji** wykonaj hello następujące kroki:
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC769497.png "skonfigurować adres URL aplikacji")
   
    a. w hello **usługi ServiceNow na adres URL logowania** tekstowym, wpisz adres URL używany przez aplikację usługi ServiceNow na toosign tooyour użytkowników następującego wzorca hello: `https://<instance-name>.service-now.com`.
   
    b. W hello **identyfikator** tekstowym, wpisz adres URL używany przez aplikację usługi ServiceNow na toosign tooyour użytkowników następującego wzorca hello: `https://<instance-name>.service-now.com`.
   
    c. Kliknij przycisk **Dalej**

4. toohave usługi Azure AD automatycznie skonfigurować usługi ServiceNow dla uwierzytelniania opartego na SAML, wprowadź nazwę wystąpienia usługi ServiceNow, nazwa użytkownika i hasło administratora w hello **automatycznie skonfigurować logowanie jednokrotne** tworzą, a następnie kliknij przycisk  *Skonfiguruj*. Należy pamiętać, że podana nazwa użytkownika administratora hello musi mieć hello **security_admin** rola przypisana w usługi ServiceNow dla tego toowork. W przeciwnym razie toomanually skonfigurować usługi ServiceNow toouse usługi Azure AD jako dostawca tożsamości SAML, kliknij przycisk **ręcznie skonfigurować aplikacji hello dla logowania jednokrotnego**, następnie kliknij przycisk **dalej** i hello ukończone Poniższe kroki.
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "skonfigurować adres URL aplikacji")

5. Na powitania **skonfigurować logowanie jednokrotne w ServiceNow** kliknij przycisk **pobierania certyfikatu**, Zapisz plik certyfikatu hello lokalnie na komputerze.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749325.png "skonfigurować logowanie jednokrotne")

6. Zaloguj się na tooyour ServiceNow aplikacji jako administrator.

7. Aktywuj hello *integracja — wiele pojedynczego logowania Instalatora dostawcy* wtyczki, wykonując hello następne kroki:
   
    a. W okienku nawigacji powitania po lewej stronie powitania Przejdź zbyt**definicji systemu** sekcji, a następnie kliknij przycisk **wtyczek**.
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "aktywowanie wtyczki")
   
    b. Wyszukaj *integracja — wiele pojedynczego logowania Instalatora dostawcy*.
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "aktywowanie wtyczki")
   
    c. Wybierz wtyczki hello. Rigth kliknij i zaznacz **Aktywuj/Upgrade**.
   
    d. Kliknij przycisk hello **Aktywuj** przycisku.

8. W okienku nawigacji hello po lewej stronie powitania kliknij **właściwości**.  
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "skonfigurować adres URL aplikacji")

9. Na powitania **wiele właściwości logowania jednokrotnego dostawcy** okna dialogowego, wykonaj następujące kroki hello:
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "skonfigurować adres URL aplikacji")
   
    a. Jako **włączyć wiele dostawcy logowania jednokrotnego**, wybierz pozycję **tak**.
   
    b. Jako **włączania rejestrowania debugowania otrzymano hello dostawca wielu mechanizmów integracji logowania jednokrotnego**, wybierz pozycję **tak**.
   
    c. W **tabeli pole hello na powitania użytkownika, który...**  pole tekstowe, typ **nazwa_użytkownika**.
   
    d. Kliknij pozycję **Zapisz**.

10. W okienku nawigacji hello po lewej stronie powitania kliknij **certyfikaty x509**.
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "skonfigurować logowanie jednokrotne")

11. Na powitania **certyfikatów X.509** okna dialogowego, kliknij przycisk **nowy**.
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "skonfigurować logowanie jednokrotne")

12. Na powitania **certyfikatów X.509** okna dialogowego, wykonaj następujące kroki hello:
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "skonfigurować logowanie jednokrotne")
    
     a. Kliknij przycisk **Nowy**.
    
     b. W hello **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: **TestSAML2.0**).
    
     c. Wybierz **Active**.
    
     d. Jako **Format**, wybierz pozycję **PEM**.
    
     e. Jako **typu**, wybierz pozycję **zaufania certyfikatów magazynu**.
    
     f. Otwórz z certyfikatu szyfrowania Base64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu PEM** pola tekstowego.
    
     g. Kliknij przycisk **aktualizacji**.

13. W okienku nawigacji hello po lewej stronie powitania kliknij **dostawców tożsamości**.
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "skonfigurować logowanie jednokrotne")

14. Na powitania **dostawców tożsamości** okna dialogowego, kliknij przycisk **nowy**:
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "skonfigurować logowanie jednokrotne")

15. Na powitania **dostawców tożsamości** okna dialogowego, kliknij przycisk **aktualizację1 SAML2?**:
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "skonfigurować logowanie jednokrotne")

16. W oknie dialogowym właściwości aktualizację1 SAML2 hello wykonaj następujące kroki hello:
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "skonfigurować logowanie jednokrotne")

    a. w hello **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: **SAML 2.0**).

    b. W hello **pole użytkownika** pole tekstowe, typ **e-mail** lub **nazwa_użytkownika**, w zależności od tego, które pole służy toouniquely identyfikowania użytkowników w danym wdrożeniu usługi ServiceNow. 

    > [!NOTE] 
    > Możesz tooemit configue usługi Azure AD albo identyfikator użytkownika hello Azure AD (główna nazwa użytkownika) lub hello adres e-mail jako hello Unikatowy identyfikator w tokenie SAML hello przez przejście toohello **usługi ServiceNow > atrybuty > logowanie jednokrotne** sekcji Witaj klasycznego portalu Azure i mapowanie hello potrzeby pola toohello **nameidentifier** atrybutu. wartość Hello przechowywanych dla wybranego atrybutu hello w usłudze Azure AD (np. główna nazwa użytkownika) musi odpowiadać wartości hello przechowywane w usługi ServiceNow hello wprowadzony w polu (np. nazwa_użytkownika)

    c. W klasycznym portalu hello Azure AD, skopiuj hello **identyfikator dostawcy tożsamości** wartość, a następnie wklej go do hello **adres URL dostawcy tożsamości** pola tekstowego.

    d. W klasycznym portalu hello Azure AD, skopiuj hello **adres URL żądania uwierzytelniania** wartość, a następnie wklej go do hello **AuthnRequest dostawcy tożsamości** pola tekstowego.

    e. W klasycznym portalu hello Azure AD, skopiuj hello **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej go do hello **SingleLogoutRequest dostawcy tożsamości** pola tekstowego.

    f. W hello **strony głównej usługi ServiceNow** pole tekstowe, typ hello adres URL strony głównej wystąpienia usługi ServiceNow.

    > [!NOTE] 
    > Strona główna wystąpienia usługi ServiceNow Hello jest złączeniem Twojej **adres URL dzierżawy ServieNow** i **/navpage.do** (np.:`https://fabrikam.service-now.com/navpage.do`).

    g. W hello **identyfikator podmiot / wystawca** pole tekstowe, wprowadź adres URL hello dzierżawy usługi ServiceNow.

    h. W hello **URL odbiorców** pole tekstowe, wprowadź adres URL hello dzierżawy usługi ServiceNow. 

    i. W hello **powiązanie protokołu hello w rozszerzeniu IDP SingleLogoutRequest** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:bindings:HTTP-przekierowania**.

    j. W hello zasad NameID pole tekstowe, wpisz **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: nieokreślony**.

    k. Anuluj wybór **utworzyć AuthnContextClass**.

    l. W hello **metody AuthnContextClassRef**, typ `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`. Jest to potrzebne tylko w przypadku organizacji tylko w chmurze. Jeśli używasz lokalnych usług AD FS lub usługę MFA dla uwierzytelniania, a następnie ta wartość nie należy konfigurować. 

    m. W **pochylanie zegara** pole tekstowe, typ **60**.

    n. Jako **pojedynczy znak na skrypt**, wybierz pozycję **MultiSSO_SAML2_Update1**.

    o. Jako **x509 certyfikatu**, wybierz pozycję hello certyfikat został utworzony w poprzednim kroku hello.

    p. Kliknij przycisk **przesłać**. 

1. W portalu klasycznym hello Azure AD, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**. 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "skonfigurować logowanie jednokrotne")

2. Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "skonfigurować logowanie jednokrotne")

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a>Konfigurowanie usługi Azure AD jednokrotnej usługi ServiceNow Express
1. W klasycznym portalu usługi Azure AD hello na powitania **ServiceNow** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okna dialogowego .
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749323.png "skonfigurować logowanie jednokrotne")

2. Na powitania **jak ma toosign użytkowników na tooServiceNow** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749324.png "skonfigurować logowanie jednokrotne")

3. Na powitania **Konfigurowanie ustawień aplikacji** wykonaj hello następujące kroki:
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC769497.png "skonfigurować adres URL aplikacji")
   
    a. w hello **usługi ServiceNow na adres URL logowania** tekstowym, wpisz adres URL używany przez aplikację usługi ServiceNow na toosign tooyour użytkowników następującego wzorca hello: `https://<instance-name>.service-now.com`.
   
    b. W hello **adres URL wystawcy** tekstowym, wpisz adres URL używany przez aplikację usługi ServiceNow na toosign tooyour użytkowników następującego wzorca hello `https://<instance-name>.service-now.com`.
   
    c. Kliknij przycisk **Dalej**

4. Kliknij przycisk **ręcznie skonfigurować aplikacji hello dla logowania jednokrotnego**, następnie kliknij przycisk **dalej** i pełne hello wykonaj następujące kroki.
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "skonfigurować adres URL aplikacji")

5. Na powitania **skonfigurować logowanie jednokrotne w ServiceNow** kliknij przycisk **pobierania certyfikatu**, Zapisz plik certyfikatu hello lokalnie na komputerze, a następnie kliknij przycisk **dalej**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749325.png "skonfigurować logowanie jednokrotne")

6. Zaloguj się na tooyour aplikacji Express usługi ServiceNow jako administrator.

7. W okienku nawigacji hello po lewej stronie powitania kliknij **rejestracji jednokrotnej**.  
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "skonfigurować adres URL aplikacji")

8. Na powitania **rejestracji jednokrotnej** okna dialogowego, kliknij ikonę konfiguracji hello na wielką hello prawo i ustaw hello następujących właściwości:
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "skonfigurować adres URL aplikacji")
   
    a. Przełącz **włączyć wiele dostawcy logowania jednokrotnego** toohello prawo.
   
    b. Przełącz **debugowania Włącz rejestrowanie dla hello dostawca wielu mechanizmów integracji logowania jednokrotnego** toohello prawo.
   
    c. W **tabeli pole hello na powitania użytkownika, który...**  pole tekstowe, typ **nazwa_użytkownika**.
9. Na powitania **rejestracji jednokrotnej** okna dialogowego, kliknij przycisk **Dodaj nowy certyfikat**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "skonfigurować logowanie jednokrotne")
10. Na powitania **certyfikatów X.509** okna dialogowego, wykonaj następujące kroki hello:
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "skonfigurować logowanie jednokrotne")
    
    a. W hello **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: **TestSAML2.0**).
    
    b. Wybierz **Active**.
    
    c. Jako **Format**, wybierz pozycję **PEM**.
    
    d. Jako **typu**, wybierz pozycję **zaufania certyfikatów magazynu**.
    
    e. Utwórz plik kodowany w standardzie Base64 z pobranego certyfikatu.
    
    > [!NOTE]
    > Aby uzyskać więcej informacji, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o).
    > 
    > 
    
    f. Otwórz z certyfikatu szyfrowania Base64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu PEM** pola tekstowego.
    
    g. Kliknij przycisk **aktualizacji**.
11. Na powitania **rejestracji jednokrotnej** okna dialogowego, kliknij przycisk **Dodaj nowe IdP**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "skonfigurować logowanie jednokrotne")
12. Na powitania **Dodaj nowego dostawcę tożsamości** okna dialogowego, w obszarze **Konfigurowanie dostawcy tożsamości**, wykonaj następujące kroki hello:
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "skonfigurować logowanie jednokrotne")

    a. w hello **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: **SAML 2.0**).

    b. W klasycznym portalu hello Azure AD, skopiuj hello **identyfikator dostawcy tożsamości** wartość, a następnie wklej go do hello **adres URL dostawcy tożsamości** pola tekstowego.

    c. W klasycznym portalu hello Azure AD, skopiuj hello **adres URL żądania uwierzytelniania** wartość, a następnie wklej go do hello **AuthnRequest dostawcy tożsamości** pola tekstowego.

    d. W klasycznym portalu hello Azure AD, skopiuj hello **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej go do hello **SingleLogoutRequest dostawcy tożsamości** pola tekstowego.

    e. Jako **certyfikat dostawcy tożsamości**, wybierz pozycję hello certyfikat został utworzony w poprzednim kroku hello.


1. Kliknij przycisk **Zaawansowane ustawienia**, a następnie w obszarze **dodatkowe właściwości dostawcy tożsamości**, wykonaj następujące kroki hello:
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "skonfigurować logowanie jednokrotne")
   
    a. W hello **powiązanie protokołu hello w rozszerzeniu IDP SingleLogoutRequest** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:bindings:HTTP-przekierowania**.
   
    b. W hello **zasad NameID** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: nieokreślony**.    
   
    c. W hello **metody AuthnContextClassRef**, typ **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.
   
    d. Anuluj wybór **utworzyć AuthnContextClass**.

2. W obszarze **dodatkowe właściwości dostawcy usług**, wykonaj następujące kroki hello:
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "skonfigurować logowanie jednokrotne")
   
    a. W hello **strony głównej usługi ServiceNow** pole tekstowe, typ hello adres URL strony głównej wystąpienia usługi ServiceNow.
   
    > [!NOTE]
    > Strona główna wystąpienia usługi ServiceNow Hello jest złączeniem Twojej **adres URL dzierżawy ServieNow** i **/navpage.do** (np.: `https://fabrikam.service-now.com/navpage.do`).
    > 
    > 
   
    b. W hello **identyfikator podmiot / wystawca** pole tekstowe, wprowadź adres URL hello dzierżawy usługi ServiceNow.
   
    c. W hello **identyfikatora URI odbiorców** pole tekstowe, wprowadź adres URL hello dzierżawy usługi ServiceNow. 
   
    d. W **pochylanie zegara** pole tekstowe, typ **60**.
   
    e. W hello **pole użytkownika** pole tekstowe, typ **e-mail** lub **nazwa_użytkownika**, w zależności od tego, które pole służy toouniquely identyfikowania użytkowników w danym wdrożeniu usługi ServiceNow.
   
    > [!NOTE]
    > Możesz tooemit configue usługi Azure AD albo identyfikator użytkownika hello Azure AD (główna nazwa użytkownika) lub hello adres e-mail jako hello Unikatowy identyfikator w tokenie SAML hello przez przejście toohello **usługi ServiceNow > atrybuty > logowanie jednokrotne** sekcji Witaj klasycznego portalu Azure i mapowanie hello potrzeby pola toohello **nameidentifier** atrybutu. wartość Hello przechowywanych dla wybranego atrybutu hello w usłudze Azure AD (np. główna nazwa użytkownika) musi odpowiadać wartości hello przechowywane w usługi ServiceNow hello wprowadzony w polu (np. nazwa_użytkownika)
    > 
    > 
   
    f. Kliknij pozycję **Zapisz**. 

3. W portalu klasycznym hello Azure AD, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**. 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "skonfigurować logowanie jednokrotne")

4. Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "skonfigurować logowanie jednokrotne")

## <a name="configuring-user-provisioning"></a>Konfigurowanie Inicjowanie obsługi użytkowników
Celem Hello w tej sekcji jest toooutline jak tooServiceNow kont tooenable użytkownika usługi Active Directory Inicjowanie obsługi użytkowników.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:
1. Hello Azure classic Portal zarządzania, na powitania **ServiceNow** strona integracji aplikacji, kliknij przycisk **skonfigurować Inicjowanie obsługi użytkowników**. 
   
    ![Inicjowanie obsługi użytkowników](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Inicjowanie obsługi użytkowników")

2. Na powitania **Wprowadź użytkownika usługi ServiceNow poświadczenia tooenable automatyczne Inicjowanie obsługi użytkowników** Podaj hello następujące ustawienia konfiguracji:
   
     a. W hello **nazwy wystąpienia usługi ServiceNow** pole tekstowe, nazwę wystąpienia usługi ServiceNow hello typu.
   
     b. W hello **nazwa użytkownika administratora usługi ServiceNow** pole tekstowe, nazwa typu hello hello konta administratora usługi ServiceNow.
   
     c. W hello **hasło administratora usługi ServiceNow** tekstowym, wpisz hello hasło dla tego konta.
   
     d. Kliknij przycisk **zweryfikować** tooverify konfiguracji.
   
     e. Kliknij przycisk hello **dalej** hello tooopen przycisk **następne kroki** strony.
   
     f. Tooprovision wszystkich użytkowników toothis aplikacji, wybierz opcję "**automatycznie obsługiwać wszystkich kont użytkowników w aplikacji toothis katalogu hello**". 
   
    ![Następne kroki](./media/active-directory-saas-servicenow-tutorial/IC698804.png "następne kroki")
   
     g. Na powitania **następne kroki** kliknij przycisk **Complete** toosave konfiguracji.

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
W tej sekcji Tworzenie użytkownika testowego w portalu klasycznym hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][20]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    a. Jako typ użytkownika wybierz nowego użytkownika w organizacji.
   
    b. W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.
   
    c. Kliknij przycisk **Dalej**.

6. Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   a. W hello **imię** pole tekstowe, typ **Britta**.  
   
   b. W hello **nazwisko** pole tekstowe, typ **Simona**.
   
   c. W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.
   
   d. W hello **roli** listy, wybierz **użytkownika**.
   
   e. Kliknij przycisk **Dalej**.

7. Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    a. Zanotuj wartość hello hello **nowe hasło**.
   
    b. Kliknij przycisk **Complete** (Zakończ).   

### <a name="creating-a-servicenow-test-user"></a>Tworzenie użytkownika testowego usługi ServiceNow
W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w usługi ServiceNow. W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w usługi ServiceNow. Jeśli nie wiesz, jak tooadd w ServiceNow lub Express usługi ServiceNow konta użytkownika, skontaktuj się z zespołem pomocy technicznej usługi ServiceNow.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD
W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooServiceNow dostępu.

![Przypisz użytkownika][200] 

**tooassign tooServiceNow Simona Britta wykonaj hello następujące kroki:**

1. W portalu klasycznym hello, kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **ServiceNow**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. W menu hello na górze hello, kliknij przycisk **użytkowników**.
   
    ![Przypisz użytkownika][203] 

4. Na liście hello wszystkich użytkowników, wybierz **Simona Britta**.

5. W narzędzi hello na dole powitania kliknij **przypisać**.
   
    ![Przypisz użytkownika][205]

### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej
Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.

Po kliknięciu kafelka usługi ServiceNow hello w hello panelu dostępu należy pobrać aplikację usługi ServiceNow tooyour zalogowane automatycznie.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
