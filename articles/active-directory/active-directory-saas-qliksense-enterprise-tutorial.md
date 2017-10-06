---
title: "Samouczek: Integracji Azure Active Directory z przedsiębiorstwa znaczeniu Qlik | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Qlik przedsiębiorstwa znaczeniu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a>Samouczek: Integracji Azure Active Directory z przedsiębiorstwa znaczeniu Qlik

Z tego samouczka, dowiesz się, jak toointegrate Qlik znaczeniu przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD przedsiębiorstwa znaczeniu Qlik zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooQlik przedsiębiorstwa znaczeniu.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooQlik przedsiębiorstwa znaczeniu (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z Qlik przedsiębiorstwa znaczeniu, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Przedsiębiorstwa znaczeniu Qlik logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie przedsiębiorstwa znaczeniu Qlik z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a>Dodawanie przedsiębiorstwa znaczeniu Qlik z galerii hello
tooconfigure hello integracji przedsiębiorstwa znaczeniu Qlik do usługi Azure AD, należy tooadd przedsiębiorstwa znaczeniu Qlik z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd przedsiębiorstwa znaczeniu Qlik z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **przedsiębiorstwa znaczeniu Qlik**, wybierz pozycję **przedsiębiorstwa znaczeniu Qlik** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Przedsiębiorstwa znaczeniu Qlik hello listy wyników](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Qlik przedsiębiorstwa znaczeniu, w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w przedsiębiorstwie znaczeniu Qlik jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w przedsiębiorstwie znaczeniu Qlik musi toobe ustanowione.

W Qlik przedsiębiorstwa znaczeniu, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Qlik przedsiębiorstwa znaczeniu, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego przedsiębiorstwa znaczeniu Qlik](#create-a-qlik-sense-enterprise-test-user)**  -toohave odpowiednikiem Simona Britta w przedsiębiorstwie znaczeniu Qlik, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji przedsiębiorstwa znaczeniu Qlik.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Qlik przedsiębiorstwa znaczeniu, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **przedsiębiorstwa znaczeniu Qlik** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. Na powitania **adresy URL i domeny przedsiębiorstwa znaczeniu Qlik** sekcji, wykonaj następujące kroki hello:

    ![Adresy URL i domeny przedsiębiorstwa znaczeniu Qlik pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`
    
    > [!NOTE]
    > Należy zwrócić uwagę hello kończyć się ukośnikiem na końcu hello tego identyfikatora URI. Jest wymagane.
    
    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Aktualizacja tych wartości za pomocą hello rzeczywisty adres URL logowania i identyfikator, które opisano szczegółowo w dalszej części tego samouczka lub skontaktuj się z [zespołem pomocy technicznej klienta przedsiębiorstwa znaczeniu Qlik](https://www.qlik.com/us/services/support) tooget tych wartości. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. Przygotuj plik XML metadanych Federacji hello, dzięki czemu możesz przekazać ten serwer znaczeniu tooQlik.
   
    > [!NOTE]
    > Przed przekazaniem hello IdP metadanych toohello serwera Qlik znaczeniu, plik hello musi toobe edytować tooremove informacji tooensure poprawne działanie między usługą Azure AD i serwer Qlik znaczeniu.
    
    ![QlikSense][qs24]
   
    a. Otwórz plik FederationMetaData.xml hello, który został pobrany z portalu Azure w edytorze tekstów.
   
    b. Wyszukaj wartości hello **RoleDescriptor**.  Istnieją cztery wpisy (dwie pary otwierające i zamykające znaczniki elementów).
   
    c. Usuwania hello RoleDescriptor tagów i wszystkie informacje między hello pliku.
   
    d. Zapisz plik hello i przechowywać w pobliżu do użytku w dalszej części tego dokumentu.

7. Przejdź toohello Qlik znaczeniu Qlik Management Console (QMC) jako użytkownik, który można utworzyć konfiguracji wirtualnego serwera proxy.

8. Witaj QMC polecenie hello **wirtualnych serwerów proxy** elementu menu.
   
    ![QlikSense][qs6] 

9. U dołu hello hello ekranu, kliknij przycisk hello **Utwórz nowy** przycisku.
   
    ![QlikSense][qs7]

10. zostanie wyświetlony ekran edycji proxy wirtualnej Hello.  Na powitania prawej krawędzi ekranu hello jest menu do wybierania opcji konfiguracji widoczne.
   
    ![QlikSense][qs9]

11. Z zaznaczoną opcją menu identyfikacji hello wprowadź informacje identyfikujące hello hello konfiguracji serwera proxy wirtualnych Azure.
    
    ![QlikSense][qs8]  
    
    a. Witaj **opis** pole jest przyjazną nazwę dla konfiguracji serwera proxy wirtualnego hello.  Wprowadź wartość opis.
    
    b. Witaj **prefiksu** pole identyfikuje punkt końcowy wirtualnego serwera proxy hello podłączania tooQlik znaczeniu z usługi Azure AD rejestracji jednokrotnej.  Wprowadź nazwę unikatowy prefiks dla tego wirtualnego serwera proxy.
    
    c. **Limit czasu bezczynności sesji (w minutach)** jest hello przekroczenia limitu czasu dla połączeń za pośrednictwem tego wirtualnego serwera proxy.
    
    d. Witaj **nazwy nagłówka pliku cookie sesji** jest przechowywanie nazwę pliku cookie hello hello identyfikator sesji hello znaczeniu Qlik sesji przez użytkownika otrzymuje po pomyślnym uwierzytelnieniu.  Ta nazwa musi być unikatowa.

12. Polecenie hello uwierzytelniania menu opcji toomake on widoczny.  zostanie wyświetlony ekran uwierzytelniania Hello.
    
    ![QlikSense][qs10]
    
    a. Hello **tryb dostępu anonimowego** listy rozwijanej określa użytkowników anonimowych może udostępniać znaczeniu Qlik za pośrednictwem hello wirtualnego serwera proxy.  Opcja domyślna Hello jest nie użytkownika anonimowego.
    
    b. Witaj **metodę uwierzytelniania** listy rozwijanej określa użyje hello uwierzytelniania schemat hello wirtualnego proxy.  Z listy rozwijanej hello wybierz SAML.  W związku z tym pojawi się więcej opcji.
    
    c. W hello **pola identyfikatora URI hosta SAML**, wejściowych hello hostname wprowadzania tooaccess znaczeniu Qlik za pośrednictwem tego serwera proxy do wirtualnego SAML.  Nazwa hosta Hello jest identyfikator uri hello powitania serwera Qlik znaczeniu.
    
    d. W hello **identyfikator jednostki SAML**, wprowadź hello tę samą wartość wprowadzona w polu identyfikatora URI hosta SAML hello.
    
    e. Hello **metadanych SAML IdP** jest plikiem hello edytować we wcześniejszej części hello **edytowanie metadanych federacji z konfiguracji usługi Azure AD** sekcji.  **Przed przekazaniem hello IdP metadanych pliku hello musi toobe edytować** poprawne działanie tooensure tooremove informacji między usługą Azure AD i serwer Qlik znaczeniu.  **Jeśli plik hello ma jeszcze edytować toobe należy zapoznać się z powyższych instrukcji toohello.**  Jeśli edytowano hello pliku kliknij hello przycisk Przeglądaj i wybierz hello metadanych edytowanego pliku tooupload go toohello konfiguracji wirtualnego serwera proxy.
    
    f. Wprowadź hello atrybut nazwy lub schematu odwołanie do atrybutu SAML hello reprezentujący hello **UserID** toohello znaczeniu Qlik serwer wysyła usługi Azure AD.  Informacje o odwołaniu schematu jest dostępna w konfiguracji wpisu ekrany Azure aplikacji hello.  Atrybut nazwy hello toouse, wprowadź `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    g. Wprowadź wartość hello hello **katalogu użytkownika** który będzie dołączony toousers podczas uwierzytelniania serwera znaczeniu tooQlik za pośrednictwem usługi Azure AD.  Wartości zapisane na stałe muszą być ujęte w **nawiasy kwadratowe []**.  toouse atrybut wysyłane w hello potwierdzenia języka SAML programu Azure AD, wprowadź nazwę hello atrybutu hello w tym polu tekstowym **bez** nawiasy kwadratowe.
    
    h. Witaj **algorytm podpisywania SAML** zestawy hello usługi dostawcy (w tym wielkość server znaczeniu Qlik) certyfikatu podpisywania hello konfiguracji wirtualnego serwera proxy.  Jeśli serwer znaczeniu Qlik używa zaufanego certyfikatu wygenerowanych przy użyciu Microsoft Enhanced RSA and AES Cryptographic Provider, zmień algorytm podpisywania SAML hello zbyt**algorytmu SHA-256**.
    
    i. Witaj SAML atrybutu mapowania sekcji umożliwia dodatkowych atrybutów, takich jak grupy toobe wysyłane tooQlik znaczeniu do użycia w zasadach zabezpieczeń.

13. Polecenie hello **RÓWNOWAŻENIA obciążenia** toomake opcji menu on widoczny.  zostanie wyświetlony ekran równoważenia obciążenia Hello.
    
    ![QlikSense][qs11]

14. Polecenie hello **Dodaj nowy węzeł serwera** przycisku wybierz aparat węzła lub węzłów znaczeniu Qlik wysyła celów równoważenia obciążenia toofor sesji i kliknij przycisk hello **Dodaj** przycisku.
    
    ![QlikSense][qs12]

15. Polecenie hello menu zaawansowanych opcji toomake on widoczny. zostanie wyświetlony ekran Zaawansowane Hello.
    
    ![QlikSense][qs13]
    
    Witaj hosta białą listę identyfikuje nazwy hostów, które są akceptowane, gdy połączenie toohello serwera Qlik znaczeniu.  **Wprowadź nazwę hosta hello, którą użytkownicy określą podczas łączenia serwera znaczeniu tooQlik.** Nazwa hosta Hello jest hello samą wartość jak hello SAML identyfikatora uri hosta bez hello https://.

16. Kliknij przycisk hello **Zastosuj** przycisku.
    
    ![QlikSense][qs14]

17. Kliknij przycisk OK tooaccept hello ostrzeżenie dotyczące serwerów proxy zostanie uruchomiona ponownie połączony toohello wirtualnego serwera proxy.
    
    ![QlikSense][qs15]

18. Po prawej stronie powitania ekranie powitania pojawi się hello skojarzone elementy menu.  Polecenie hello **proxy** opcji menu.
    
    ![QlikSense][qs16]

19. zostanie wyświetlony ekran proxy Hello.  Kliknij przycisk hello **łącze** znajdujący się u toolink dolnej hello proxy wirtualnego toohello serwera proxy.
    
    ![QlikSense][qs17]

20. Wybierz hello węzeł serwera proxy, który obsługi tego połączenia wirtualnego serwera proxy i kliknij przycisk hello **łącze** przycisku.  Po połączeniu, powitania serwera proxy, będą wyświetlane w skojarzone serwery proxy.
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. Po około pięciu sekundach tooten, Odśwież QMC wiadomość hello będą wyświetlane.  Kliknij przycisk hello **Odśwież QMC** przycisku.
    
    ![QlikSense][qs20]

22. Po odświeżeniu hello QMC na powitania kliknij przycisk **proxy wirtualnej** elementu menu. Nowy wpis wirtualnego serwera proxy SAML Hello to wymienione w tabeli hello na ekranie powitania.  Kliknij wpis wirtualnego serwera proxy hello.
    
    ![QlikSense][qs51]

23. U dołu hello hello ekranu hello SP pobrać metadanych przycisk zostanie aktywowany.  Kliknij przycisk hello **SP pobrać metadanych** pliku tooa przycisk toosave hello metadanych.
    
    ![QlikSense][qs52]

24. Otwórz hello sp pliku metadanych.  Obserwować hello **entityID** wpisu i hello **AssertionConsumerService** wpisu.  Te wartości są równoważne toohello **identyfikator** i hello **Zaloguj się na adres URL** w konfiguracji aplikacji hello Azure AD. Wklej te wartości w hello **adresy URL i domeny przedsiębiorstwa znaczeniu Qlik** sekcji w konfiguracji aplikacji hello Azure AD, jeśli ich są niezgodne, a następnie należy zastąpić je w Kreatorze konfiguracji usługi Azure AD aplikacji hello.
    
    ![QlikSense][qs53]

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

   ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

   ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

   ![przycisk Dodaj Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

   ![okno dialogowe Hello użytkownika](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   a. W hello **nazwa** wpisz **BrittaSimon**.

   b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

   c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

   d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a>Tworzenie użytkownika testowego przedsiębiorstwa znaczeniu Qlik

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Qlik przedsiębiorstwa znaczeniu. Praca z [zespołem pomocy technicznej klienta przedsiębiorstwa znaczeniu Qlik](https://www.qlik.com/us/services/support) do dodawania użytkowników hello hello przedsiębiorstwa znaczeniu Qlik platformy. Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej. 

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooQlik przedsiębiorstwa znaczeniu.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooQlik Simona Britta przedsiębiorstwa znaczeniu, należy wykonać hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **przedsiębiorstwa znaczeniu Qlik**.

    ![łącze przedsiębiorstwa znaczeniu Qlik Hello na liście aplikacji hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka przedsiębiorstwa znaczeniu Qlik hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour przedsiębiorstwa znaczeniu Qlik aplikacji. 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

