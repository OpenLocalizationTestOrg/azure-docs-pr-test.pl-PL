---
title: 'Samouczek: Integracji Azure Active Directory z piaskownicy Salesforce | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usług Salesforce piaskownicy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Samouczek: Integracji Azure Active Directory z piaskownicy usług Salesforce

Z tego samouczka, dowiesz się, jak toointegrate piaskownicy usługi Salesforce z usługą Azure Active Directory (Azure AD).

Integrowanie piaskownicy usługi Salesforce z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSalesforce piaskownicy
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSalesforce piaskownicy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z piaskownicy Salesforce należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Piaskownica Salesforce jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie piaskownicy usługi Salesforce z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a>Dodawanie piaskownicy usługi Salesforce z galerii hello
tooconfigure hello integracji piaskownicy usługi Salesforce z usługą Azure AD, należy tooadd piaskownicy usługi Salesforce z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd piaskownicy usługi Salesforce z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **piaskownicy Salesforce**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. W panelu wyników hello, wybierz **piaskownicy Salesforce**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z piaskownicy Salesforce oparte na użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w piaskownicy Salesforce jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w piaskownicy Salesforce musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w piaskownicy Salesforce.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z piaskownicy Salesforce, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego piaskownicy Salesforce](#creating-a-salesforce-sandbox-test-user)**  -toohave odpowiednikiem Simona Britta w piaskownicy Salesforce, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Salesforce piaskownicy.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z piaskownicy Salesforce, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **piaskownicy Salesforce** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. Na powitania **Salesforce piaskownicy domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     W hello **adres URL logowania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://<subdomain>.my.salesforce.com`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe hello. Zaktualizuj tę wartość przy hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta piaskownicy Salesforce](https://help.salesforce.com/support) tooget tej wartości.


4. Jeśli skonfigurowano już program rejestracji jednokrotnej dla innego wystąpienia usług Salesforce piaskownicy w katalogu, a następnie należy także skonfigurować hello **identyfikator** toohave hello tę samą wartość jak hello **Zaloguj się na adres URL**. 
    
    >[!Note]
    >Witaj **identyfikator** pola można znaleźć, sprawdzając hello **Pokaż zaawansowane ustawienia** wyboru na powitania **Konfigurowanie adresu URL aplikacji** stronę hello okna dialogowego 


5. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. Na powitania **konfiguracji piaskownicy Salesforce** kliknij **skonfigurować piaskownicy Salesforce** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS>
8. Otwórz nową kartę w przeglądarce i zaloguj tooyour konto administratora usług Salesforce piaskownicy.

9. W menu hello na górze hello, kliknij przycisk **Instalatora**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. W okienku nawigacji hello po lewej stronie powitania kliknij **kontroli bezpieczeństwa**, a następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. Na hello w sekcji Ustawienia rejestracji jednokrotnej, wykonaj następujące kroki hello: ![skonfigurować logowanie jednokrotne](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)
     
     a.  Wybierz **SAML włączone**. 

     b.  Kliknij przycisk **Nowy**.

12. Witaj SAML pojedynczy znak w sekcji Ustawienia wykonywanie hello następujące kroki:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    pole tekstowe Nazwa hello a.In, hello nazwę typu konfiguracji hello (np.: *SPSSOWAAD\_testu*). 

    b. Wklej **identyfikator jednostki SMAL** wartości do hello **wystawcy** pola tekstowego.

    c. W hello **identyfikator jednostki** pole tekstowe, typ **https://test.salesforce.com** przypadku hello pierwszego wystąpienia usług Salesforce piaskownicy dodajesz tooyour katalogu. Jeśli masz już dodany wystąpienia usług Salesforce piaskownicy, a następnie dla hello **identyfikator jednostki** typu w hello **na adres URL logowania**, która powinna być w następującym formacie:`http://company.my.salesforce.com`  
 
    d. Kliknij przycisk **Przeglądaj** tooupload hello pobrać certyfikatu.  

    e. Jako **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera hello identyfikator federacyjnej z obiektu użytkownika hello**.
 
    f. Jako **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentifier hello hello instrukcji podmiotu**.

    g. Wklej **pojedynczy znak na adres URL usługi** do hello **adresu URL logowania do dostawcy tożsamości** pola tekstowego. 

    h. SFDC nie obsługuje SAML wylogowania.  Jako obejście, Wklej "https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0" go do hello **adres URL wylogowania dostawcy tożsamości** pola tekstowego.

    i. Jako **dostawcy zainicjował żądanie powiązania usługi**, wybierz pozycję **HTTP POST**. 

    j. Kliknij pozycję **Zapisz**.

### <a name="enable-your-domain"></a>Włącz domeny
W tej sekcji założono, że już utworzono domeny.  Aby uzyskać więcej informacji, zobacz [Definiowanie Twojej nazwy domeny](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable domeny, wykonaj następujące kroki hello:**

1. W okienku nawigacji po lewej stronie powitania kliknij **Zarządzanie domenami**, a następnie kliknij przycisk **Moje domeny.**
   
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   >Upewnij się, że poprawnie skonfigurowano domenę. 

2. W hello **ustawienia strony logowania** , kliknij przycisk **Edytuj**, następnie jako **usługi uwierzytelniania**, wybierz nazwę hello hello SAML pojedynczego logowania jednokrotnego ustawienia z poprzednich hello sekcja, a na koniec kliknij **zapisać**.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

Jak masz domenę skonfigurowane, użytkownicy należy używać hello domeny adres URL toologin toohello Salesforce piaskownicy.  

wartość hello tooget hello adresu URL, kliknij profil rejestracji Jednokrotnej hello, utworzony w poprzedniej sekcji hello.    

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-salesforce-sandbox-test-user"></a>Tworzenie użytkownika testowego piaskownicy usług Salesforce

W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w piaskownicy Salesforce. Piaskownica SalesForce obsługę w czasie, który jest domyślnie włączona.
Nie ma elementu akcji można w tej sekcji. Jeśli użytkownik nie istnieje w piaskownicy Salesforce, nowy jest tworzony podczas próby tooaccess piaskownicy Salesforce.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSalesforce piaskownicy.

![Przypisz użytkownika][200] 

**tooassign tooSalesforce Simona Britta piaskownicy, wykonaj następujące kroki hello:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **piaskownicy Salesforce**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Jeśli chcesz tootest ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Skonfiguruj Inicjowanie obsługi użytkowników](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

