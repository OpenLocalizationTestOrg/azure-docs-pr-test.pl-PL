---
title: "Samouczek: Integracji Azure Active Directory z chmurą SAP dla klienta | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i w chmurze SAP dla klienta."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a>Samouczek: Integracji Azure Active Directory z chmurą SAP dla klienta

Z tego samouczka, dowiesz się, jak SAP toointegrate chmury dla klienta w usłudze Azure Active Directory (Azure AD).

Integrowanie SAP chmury dla klienta z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD mającego dostęp tooSAP chmury dla klienta
- Twoje użytkowników tooautomatically get zalogowane tooSAP chmury można włączyć dla klienta (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z chmurą SAP dla klienta, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Chmurę SAP do klienta logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie SAP chmury dla klienta z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a>Dodawanie SAP chmury dla klienta z galerii hello
tooconfigure hello integracji SAP chmury dla klienta do usługi Azure AD, należy tooadd SAP chmury dla klienta z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd chmurę SAP do klienta z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **SAP chmury dla klienta**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. W panelu wyników hello, wybierz **SAP chmury dla klienta**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z chmurą SAP dla klienta w oparciu o użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w chmurze SAP dla klienta jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w chmurze SAP dla klienta musi toobe ustanowione.

W chmurze SAP dla klienta, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z chmurą SAP dla klienta, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie chmury SAP dla użytkownika testowego klienta](#creating-a-sap-cloud-for-customer-test-user)**  -toohave odpowiednikiem Simona Britta w chmurze SAP dla klienta, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w chmurze SAP dla aplikacji klienta.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z chmurą SAP dla klienta, należy wykonać hello następujące kroki:**

1. W portalu Azure na powitania hello **SAP chmury dla klienta** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. Na powitania **chmury SAP do domeny klienta i adresy URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server name>.crm.ondemand.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server name>.crm.ondemand.com`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [chmurę SAP do zespołu pomocy technicznej klienta klienta](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget tych wartości. 

4. Na powitania **atrybuty użytkownika** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    a. W **identyfikator użytkownika** listy, wybierz opcję hello **ExtractMailPrefix()** funkcji.

    b. Z hello **poczty** listy, wybierz hello atrybut użytkownika ma toouse implementacji.
    Na przykład jeśli wartość atrybutu hello są przechowywane w hello ExtensionAttribute2 ma hello toouse identyfikator pracownika jako identyfikator unikatowy użytkownika, wybierz user.extensionattribute2.  

5. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. Na powitania **SAP chmury dla konfiguracji klienta** kliknij **skonfigurować chmurę SAP do klienta** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. tooget logowania jednokrotnego skonfigurowane, wykonaj hello następujące kroki:
   
    a. Zaloguj się w chmurze SAP do portalu klienta z prawami administratora.
   
    b. Przejdź toohello **aplikacji i typowych zadań zarządzania użytkownika** i kliknij przycisk hello **dostawcy tożsamości** kartę.
   
    c. Kliknij przycisk **nowego dostawcy tożsamości** i pliku XML metadanych hello wybierz zostały pobrane z hello portalu Azure. Importując hello metadanych systemu hello automatyczne przekazywanie hello wymagany podpis certyfikatu i certyfikat szyfrowania.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    d. Element hello adres URL usługi klienta potwierdzenia w żądaniu SAML hello wymaga usługi Azure Active Directory, dlatego wybierz hello **zawierają potwierdzenie konsumenta adres URL usługi** wyboru.
   
    e. Kliknij przycisk **aktywacji rejestracji jednokrotnej**.
   
    f. Zapisz zmiany.
   
    g. Kliknij przycisk hello **systemie** kartę.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    h. W **Azure AD znaku w adresie URL** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    i. Określ, czy pracownika hello ręcznie wybrać między zalogowanie się przy użyciu Identyfikatora użytkownika i hasła lub logowania jednokrotnego, wybierając hello **wybór dostawcy tożsamości ręcznego**.
   
    j. W hello **adres URL logowania jednokrotnego** sekcji, podaj adres URL hello, które mają być używane przez użytkownika toosign pracowników w systemie toohello. 
    W hello **wysyłane na adres URL tooEmployee** listy, możesz wybrać hello następujące opcje:
   
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

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a>Tworzenie chmury SAP dla użytkownika testowego klienta

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w chmurze SAP dla klienta. We współpracy z [SAP chmury zespół obsługi klienta](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd hello użytkowników w hello SAP chmurze dla platformy klienta. 

> [!NOTE]
> Upewnij się, wartość NameID powinny być zgodne z pole username hello w hello SAP chmurze dla platformy klienta.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSAP chmury dla klienta.

![Przypisz użytkownika][200] 

**tooassign tooSAP Simona Britta chmury dla klienta, należy wykonać hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **SAP chmury dla klienta**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello SAP chmury dla klienta kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SAP chmury dla aplikacji klienta.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

