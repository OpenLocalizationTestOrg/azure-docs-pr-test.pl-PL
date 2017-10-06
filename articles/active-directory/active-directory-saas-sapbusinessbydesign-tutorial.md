---
title: 'Samouczek: Integracji Azure Active Directory z SAP Business ByDesign | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a>Samouczek: integracja usługi Azure Active Directory z oprogramowaniem SAP Business ByDesign

Z tego samouczka, dowiesz się, jak SAP toointegrate ByDesign firm z usługą Azure Active Directory (Azure AD).

Integrowanie SAP Business ByDesign z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooSAP ByDesign biznesowych.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSAP ByDesign Business (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z SAP Business ByDesign należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- SAP Business ByDesign logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie SAP Business ByDesign z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a>Dodawanie SAP Business ByDesign z galerii hello
tooconfigure hello integracji SAP Business ByDesign do usługi Azure AD, należy tooadd SAP Business ByDesign z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd SAP Business ByDesign z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **SAP Business ByDesign**, wybierz pozycję **SAP Business ByDesign** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![SAP Business ByDesign hello listy wyników](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SAP Business ByDesign w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w SAP Business ByDesign jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w SAP Business ByDesign musi toobe ustanowione.

W SAP Business ByDesign, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SAP Business ByDesign, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**  -toohave odpowiednikiem Simona Britta w SAP Business ByDesign, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji SAP Business ByDesign.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z SAP Business ByDesign, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **SAP Business ByDesign** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. Na powitania **adresy URL i SAP Business ByDesign domeny** sekcji, wykonaj następujące kroki hello:

    ![Adresy URL i SAP Business ByDesign domeny pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<servername>.sapbydesign.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<servername>.sapbydesign.com`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej SAP Business ByDesign klienta](https://www.sap.com/products/cloud-analytics.support.html) tooget tych wartości.

4. Na powitania **atrybuty użytkownika** sekcji, wykonaj następujące kroki hello:

    ![SAP Business ByDesign atrybutów sekcji](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    a. W **identyfikator użytkownika** listy, wybierz opcję hello **ExtractMailPrefix()** funkcji.
    
    b. Z hello **poczty** listy, wybierz hello atrybut użytkownika ma toouse implementacji. Na przykład jeśli wartość atrybutu hello są przechowywane w hello ExtensionAttribute2 ma hello toouse identyfikator pracownika jako identyfikator unikatowy użytkownika, wybierz user.extensionattribute2.   

5. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. Na powitania **SAP Business ByDesign konfiguracji** kliknij **skonfigurować SAP Business ByDesign** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![SAP Business ByDesign konfiguracji](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. tooget logowania jednokrotnego skonfigurowane dla aplikacji, należy wykonać hello następujące kroki:
   
    a. Zaloguj się w portalu SAP Business ByDesign tooyour z uprawnieniami administratora.
   
    b. Przejdź za**aplikacji i typowych zadań zarządzania użytkownika** i kliknij przycisk hello **dostawcy tożsamości** kartę.
   
    c. Kliknij przycisk **nowego dostawcy tożsamości** i pliku XML metadanych wybierz hello pobranego z hello portalu Azure. Importując hello metadanych systemu hello automatyczne przekazywanie hello wymagany podpis certyfikatu i certyfikat szyfrowania.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    d. Witaj tooinclude **adres URL usługi klienta potwierdzenia** do żądania SAML hello, wybierz **zawierają potwierdzenie konsumenta adres URL usługi**.
   
    e. Kliknij przycisk **aktywacji rejestracji jednokrotnej**.
   
    f. Zapisz zmiany.
   
    g. Kliknij przycisk hello **systemie** kartę.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    h. Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z portalu Azure hello go do hello **Azure AD znaku w adresie URL** pola tekstowego.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    i. Określ, czy pracownika hello ręcznie wybrać między zalogowanie się przy użyciu Identyfikatora użytkownika i hasła lub logowania jednokrotnego, wybierając **wybór dostawcy tożsamości ręcznego**.
   
    j. W hello **adres URL logowania jednokrotnego** sekcji, podaj adres URL hello, które mają być używane przez system toohello toologon pracownika hello. 
    Witaj wysyłane na adres URL tooEmployee listy rozwijanej można wybrać hello następujące opcje:
   
    **Adres URL — Usługa rejestracji Jednokrotnej**
   
    Hello system wysyła tylko hello system normalny adres URL toohello pracownika. pracowników Hello nie może zalogować się przy użyciu logowania jednokrotnego i musi użyć hasła lub zamiast tego certyfikatu.
   
    **ADRES URL LOGOWANIA JEDNOKROTNEGO** 
   
    Hello system wysyła tylko hello pracownika toohello adres URL logowania jednokrotnego. Pracownik Hello można zalogować się przy użyciu logowania jednokrotnego. Za pomocą hello IdP kierowane jest żądanie uwierzytelniania.
   
    **Automatyczne wybieranie**
   
    Jeśli logowania jednokrotnego nie jest aktywne, hello system wysyła hello system normalny adres URL toohello pracownika. Jeśli rejestracji Jednokrotnej jest aktywny, hello system sprawdza, czy hello pracownik ma hasło. Jeśli hasło jest dostępny, zarówno adres URL logowania jednokrotnego i adres URL logowania jednokrotnego nie są wysyłane toohello pracownika. Jednak jeśli pracownik hello nie ma hasła, hello adres URL logowania jednokrotnego są wysyłane toohello pracownika.
   
    k. Zapisz zmiany.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-an-sap-business-bydesign-test-user"></a>Tworzenie użytkownika testowego SAP Business ByDesign

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w SAP Business ByDesign. We współpracy z [zespołem pomocy technicznej SAP Business ByDesign klienta](https://www.sap.com/products/cloud-analytics.support.html) użytkowników hello tooadd hello SAP Business ByDesign platformy. 

> [!NOTE]
> Upewnij się, że NameID wartość powinno być zgodne z pola Nazwa użytkownika hello hello SAP Business ByDesign platformy.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSAP ByDesign biznesowych.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooSAP Simona Britta ByDesign biznesowych, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **SAP Business ByDesign**.

    ![łącze SAP Business ByDesign Hello na liście aplikacji hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka SAP Business ByDesign hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SAP Business ByDesign aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

