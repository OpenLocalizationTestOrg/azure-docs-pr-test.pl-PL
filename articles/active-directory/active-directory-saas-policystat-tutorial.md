---
title: 'Samouczek: Integracji Azure Active Directory z PolicyStat | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a>Samouczek: Integracji Azure Active Directory z PolicyStat

Z tego samouczka, dowiesz się, jak toointegrate PolicyStat w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD PolicyStat zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPolicyStat
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPolicyStat (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z PolicyStat należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- PolicyStat logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie PolicyStat z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-policystat-from-hello-gallery"></a>Dodawanie PolicyStat z galerii hello
tooconfigure hello integracji PolicyStat do usługi Azure AD, należy tooadd PolicyStat z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd PolicyStat z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **PolicyStat**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. W panelu wyników hello zaznacz **PolicyStat**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PolicyStat w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w PolicyStat jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w PolicyStat musi toobe ustanowione.

W PolicyStat, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z PolicyStat, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego PolicyStat](#creating-a-policystat-test-user)**  -toohave odpowiednikiem Simona Britta w PolicyStat, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji PolicyStat.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z PolicyStat, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **PolicyStat** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. Na powitania **PolicyStat domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.policystat.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.policystat.com/saml2/metadata/`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta PolicyStat](http://www.policystat.com/support/) tooget tych wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooPolicyStat do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.

    PolicyStat aplikacji Hello oczekuje potwierdzenia SAML hello w określonym formacie wymaga tooyour mapowań atrybutów niestandardowych tooadd **atrybuty tokenu SAML** konfiguracji.  

     powitania po zrzut ekranu przedstawia przykład.

     ![Atrybuty](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "atrybutów")

6. Mapowanie atrybutów hello wymagane tooadd, wykonaj hello następujące kroki:

    | Nazwa atrybutu    |   Wartość atrybutu |
    |------------------- | -------------------- |
    | Identyfikator UID | ExtractMailPrefix([mail]) |
    
    a. Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    b. W hello **nazwa atrybutu** pole tekstowe, typ **uid**.

    c. W hello **wartość atrybutu** pole tekstowe, wybierz opcję **ExtractMailPrefix()**.    
   
    d. Z hello **poczty** listy, wybierz **User.mail**.
    
    e. Kliknij przycisk **Ok**

7. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy PolicyStat jako administrator.

9. Kliknij przycisk hello **Admin** , a następnie kliknij pozycję **konfiguracji rejestracji jednokrotnej** w lewym okienku nawigacji.
   
    ![Menu administratora](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu administratora")

10. W hello **Instalator** zaznacz **włączyć pojedynczego logowania jednokrotnego integracji**.
   
    ![Pojedynczy konfiguracji logowania jednokrotnego](./media/active-directory-saas-policystat-tutorial/ic808634.png "pojedynczy konfiguracji logowania jednokrotnego")

11. Kliknij przycisk **Konfigurowanie atrybutów**, a następnie na powitania **Konfigurowanie atrybutów** sekcji, wykonaj następujące kroki hello:
   
    ![Pojedynczy konfiguracji logowania jednokrotnego](./media/active-directory-saas-policystat-tutorial/ic808635.png "pojedynczy konfiguracji logowania jednokrotnego")
   
    a. W hello **atrybutu Username** pole tekstowe, typ **uid**.

    b. W hello **atrybutu imię** pole tekstowe, typ **imię** użytkownika **Britta**.

    c. W hello **ostatniego atrybutu Name** pole tekstowe, typ **nazwisko** użytkownika **Simona**.

    d. W hello **atrybut poczty E-mail** pole tekstowe, typ **emailaddress** użytkownika  **BrittaSimon@contoso.com** .

    e. Kliknij przycisk **zapisać zmiany**.

12. Kliknij przycisk **Your metadanych IDP**, a następnie na powitania **Your metadanych IDP** sekcji, wykonaj następujące kroki hello:
   
    ![Pojedynczy konfiguracji logowania jednokrotnego](./media/active-directory-saas-policystat-tutorial/ic808636.png "pojedynczy konfiguracji logowania jednokrotnego")
   
    a. Otwórz z pliku metadanych pobranych, hello kopiowania zawartości, a następnie wklej go do hello **Your metadanych dostawcy tożsamości** pola tekstowego.

    b. Kliknij przycisk **zapisać zmiany**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-policystat-test-user"></a>Tworzenie użytkownika testowego PolicyStat

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do PolicyStat muszą mieć przydzielone do PolicyStat.  

PolicyStat obsługuje tylko w czasie Inicjowanie obsługi użytkowników. Oznacza to, że nie ma potrzeby użytkowników hello tooadd ręcznie tooPolicyStat. Użytkownicy Hello będzie zostaną dodane automatycznie na ich pierwsze logowanie za pomocą logowania jednokrotnego.

>[!NOTE]
>Możesz użyć innych PolicyStat użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez PolicyStat tooprovision kont użytkowników usługi Azure AD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPolicyStat.

![Przypisz użytkownika][200] 

**tooassign tooPolicyStat Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **PolicyStat**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka PolicyStat hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour PolicyStat aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

