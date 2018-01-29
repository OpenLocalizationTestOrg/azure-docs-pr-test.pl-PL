---
title: "Samouczek: Integracji Azure Active Directory z usługi ServiceNow | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usługi ServiceNow."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: a5a1a264-7497-47e7-b129-a1b5b1ebff5b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/16/2017
ms.author: jeedes
ms.openlocfilehash: 8b21c7b18c31f3111caa13d08efb5aa42ecc0e49
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>Samouczek: Integracji Azure Active Directory z usługi ServiceNow

Z tego samouczka dowiesz się Integrowanie usługi ServiceNow z usługą Azure Active Directory (Azure AD).

Integrowanie usługi ServiceNow z usługą Azure AD zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do usługi ServiceNow.
- Umożliwia użytkownikom automatycznie pobrać podpisany w przypadku usługi ServiceNow (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z usługi ServiceNow, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Dla usługi ServiceNow, wystąpienie lub dzierżawy usługi ServiceNow, wersja Calgary lub nowszej
- Usługi ServiceNow Express, wystąpienie usługi ServiceNow Express, wersja Helsinkach lub nowszej
- Dzierżawca usługi ServiceNow musi mieć [wielu pojedynczy znak na dodatek dostawcy](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) włączone. Można to zrobić [przesyłanie żądania obsługi](https://hi.service-now.com).

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie usługi ServiceNow z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-servicenow-from-the-gallery"></a>Dodawanie usługi ServiceNow z galerii
Aby skonfigurować integrację usługi ServiceNow z usługą Azure AD, należy dodać usługi ServiceNow z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać usługi ServiceNow z galerii, wykonaj następujące czynności:**

1. W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Przycisk usługi Azure Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.

    ![Nowy przycisk aplikacji][3]

4. W polu wyszukiwania wpisz **ServiceNow**, wybierz pozycję **ServiceNow** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.

    ![Usługi ServiceNow na liście wyników](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi ServiceNow w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w ServiceNow jest dla użytkownika, w usłudze Azure AD. Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w usługi ServiceNow musi się.

Usługi ServiceNow, przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi ServiceNow, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej dla usługi ServiceNow](#configure-azure-ad-single-sign-on-for-servicenow)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Konfigurowanie usługi Azure AD logowania jednokrotnego usługi ServiceNow Express](#configure-azure-ad-single-sign-on-for-servicenow-express)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
3. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
4. **[Tworzenie użytkownika testowego usługi ServiceNow](#create-a-servicenow-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta ServiceNow połączonego z usługi Azure AD reprezentację użytkownika.
5. **[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
6. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on-for-servicenow"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej dla usługi ServiceNow

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji usługi ServiceNow.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z usługi ServiceNow, wykonaj następujące czynności:**

1. W portalu Azure na **ServiceNow** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_samlbase.png)

3. Na **adresy URL i domeny usługi ServiceNow** sekcji, wykonaj następujące czynności:

    ![Adresy URL i domeny usługi ServiceNow z jednym informacje logowania jednokrotnego](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_url.png)

    a. W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instance-name>.service-now.com/navpage.do`

    b. W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instance-name>.service-now.com`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Musisz zaktualizować te wartości z rzeczywisty adres URL logowania i identyfikator, który znajduje się w dalszej części tego samouczka.

4. Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-servicenow-tutorial/tutorial_general_400.png)

6. Aby wygenerować **metadanych** adres url, wykonaj następujące czynności:

    a. Kliknij przycisk **rejestracji aplikacji**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/appregistrations.png)

    b. Kliknij przycisk **punkty końcowe** otworzyć **punkty końcowe** okno dialogowe.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/endpointicon.png)
    
    c. Kliknij przycisk Kopiuj, aby skopiować **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/endpoint.png)

    d. Teraz przejdź do **ServiceNow** właściwości i skopiuj **identyfikator aplikacji** przy użyciu **kopiowania** przycisk i wklej go do Notatnika.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/appid.png)

    e. Generowanie **adres URL metadanych** przy użyciu następującego wzorca: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`.  Skopiuj wartość wygenerowany w programie Notatnik jako adres URL, które będą używane w dalszej części samouczka metadanych.

7. Jedno kliknięcie skonfigurować usługę została podana dla usługi ServiceNow oznacza to, aby na platformie Azure AD automatycznie skonfigurować usługi ServiceNow dla uwierzytelniania opartego na SAML. Aby włączyć tę usługę, przejdź do **konfiguracji usługi ServiceNow** kliknij **skonfigurować usługi ServiceNow** można otworzyć Konfigurowanie logowania jednokrotnego okna.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_configure.png)

8. Wprowadź nazwę wystąpienia usługi ServiceNow, nazwa użytkownika i hasło administratora w **Konfigurowanie logowania jednokrotnego** tworzą, a następnie kliknij przycisk **Konfiguruj teraz**. Należy pamiętać, że podana nazwa użytkownika administratora musi mieć **security_admin** rola przypisana w usługi ServiceNow tej pracy. W przeciwnym razie, aby ręcznie skonfigurować usługi ServiceNow przy użyciu usługi Azure AD jako dostawca tożsamości SAML, kliknij przycisk **ręcznie skonfigurować logowanie jednokrotne** i skopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z sekcji krótkimi opisami.

    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/configure.png "skonfigurować adres URL aplikacji")

9. Zaloguj się do aplikacji usługi ServiceNow jako administrator.

10. Aktywuj **integracja — wiele pojedynczego logowania Instalatora dostawcy** wtyczki dalej wykonaj czynności:

    a. W okienku nawigacji po lewej stronie Wyszukaj **definicji systemu** sekcji na pasku wyszukiwania, a następnie kliknij przycisk **wtyczek**.

    ![Aktywowanie wtyczki](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "aktywowanie wtyczki")

     b. Wyszukaj **integracja — wiele pojedynczego logowania Instalatora dostawcy**.

     ![Aktywowanie wtyczki](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "aktywowanie wtyczki")

    c. Wybierz wtyczki. Kliknij prawym przyciskiem myszy i wybierz **Aktywuj/Upgrade**.

    d. Kliknij przycisk **Aktywuj** przycisku.

11. W okienku nawigacji po lewej stronie Wyszukaj **dostawcy usługi logowania jednokrotnego** sekcji na pasku wyszukiwania, a następnie kliknij przycisk **właściwości**.

    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "skonfigurować adres URL aplikacji")

12. Na **wiele właściwości logowania jednokrotnego dostawcy** okna dialogowego, wykonaj następujące czynności:

    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/ic7694981.png "skonfigurować adres URL aplikacji")

    a. Jako **włączyć wiele dostawcy logowania jednokrotnego**, wybierz pozycję **tak**.

    b. Jako **włączyć automatyczne importowanie użytkowników z wszystkich dostawców tożsamości do tabeli użytkownika**, wybierz pozycję **tak**.

    c. Jako **debugowania Włącz rejestrowanie dla wielu dostawcy logowania jednokrotnego integracji**, wybierz pozycję **tak**.

    d. W **tabeli pole użytkownika, który...**  pole tekstowe, typ **nazwa_użytkownika**.

    e. Kliknij pozycję **Zapisz**.

13. W okienku nawigacji po lewej stronie Wyszukaj **dostawcy usługi logowania jednokrotnego** sekcji na pasku wyszukiwania, a następnie kliknij przycisk **certyfikaty x509**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "skonfigurować logowanie jednokrotne")

14. Na **certyfikatów X.509** okna dialogowego, kliknij przycisk **nowy**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694974.png "skonfigurować logowanie jednokrotne")

15. Na **certyfikatów X.509** okna dialogowego, wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694975.png "skonfigurować logowanie jednokrotne")

    a. W **nazwa** tekstowym, wpisz nazwę konfiguracji (na przykład: **TestSAML2.0**).

    b. Wybierz **Active**.

    c. Jako **Format**, wybierz pozycję **PEM**.

    d. Jako **typu**, wybierz pozycję **zaufania certyfikatów magazynu**.

    e. Otwórz z certyfikatu szyfrowania Base64 pobrany z platformy Azure w programie Notatnik, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu PEM** pola tekstowego.

     f. Kliknij przycisk **przesłać**.

16. W okienku nawigacji po lewej stronie kliknij **dostawców tożsamości**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "skonfigurować logowanie jednokrotne")

17. Na **dostawców tożsamości** okna dialogowego, kliknij przycisk **nowy**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694977.png "skonfigurować logowanie jednokrotne")

18. Na **dostawców tożsamości** okna dialogowego, kliknij przycisk **aktualizację1 SAML2?**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694978.png "skonfigurować logowanie jednokrotne")

19. W oknie dialogowym właściwości aktualizację1 SAML2 wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/idp.png "skonfigurować logowanie jednokrotne")

    a. Wybierz **adres URL** opcji **Importuj metadane dostawcy tożsamości** okno dialogowe.

    b. Wprowadź **adres URL metadanych** wygenerowane z portalu Azure.

    c. Kliknij przycisk **Importuj**.

20. Adres URL metadanych IdP odczytuje i wypełnienie wszystkich pól informacji.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694982.png "skonfigurować logowanie jednokrotne")

    a. W **nazwa** tekstowym, wpisz nazwę konfiguracji (na przykład **SAML 2.0**).

    b. W **pole użytkownika** pole tekstowe, typ **e-mail** lub **nazwa_użytkownika**, w zależności od pole, które jest używane do unikatowego identyfikowania użytkowników w danym wdrożeniu usługi ServiceNow.

    > [!NOTE]
    > Można skonfigurować usługi Azure AD, aby emitować identyfikator użytkownika usługi Azure AD (główna nazwa użytkownika) lub adres e-mail jako unikatowy identyfikator w tokenie SAML, przechodząc do **ServiceNow > atrybuty > logowanie jednokrotne** części portalu Azure mapowania odpowiednie pola i **nameidentifier** atrybutu. Wartość przechowywana wybranego atrybutu w usłudze Azure AD (na przykład główna nazwa użytkownika) musi odpowiadać wartości przechowywane w usługi ServiceNow wprowadzone pola (na przykład nazwa_użytkownika)

    c. Kopiuj **strony głównej usługi ServiceNow** wartość, wklej go w **adres URL logowania** textbox w **ServiceNow domeny i adres URL** sekcji z portalu Azure.

    > [!NOTE]
    > Na stronie głównej wystąpienia usługi ServiceNow jest złączeniem Twojej **adres URL dzierżawy ServieNow** i **/navpage.do** (na przykład:`https://fabrikam.service-now.com/navpage.do`).

    d. Kopiuj **identyfikator jednostki / wystawcy** wartość, wklej go w **identyfikator** textbox w **ServiceNow domeny i adres URL** sekcji z portalu Azure.

     e. W obszarze **x509 certyfikatu**, zawiera listę certyfikat został utworzony w poprzednim kroku.

### <a name="configure-azure-ad-single-sign-on-for-servicenow-express"></a>Konfigurowanie usługi Azure AD jednokrotnej usługi ServiceNow Express

1. W portalu Azure na **ServiceNow** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_samlbase.png)

3. Na **adresy URL i domeny usługi ServiceNow** sekcji, wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_url.png)

    a. W **adres URL logowania** tekstowym, wpisz wartość, przy użyciu następującego wzorca:`https://<instance-name>.service-now.com/navpage.do`

    b. W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instance-name>.service-now.com`

    > [!NOTE]
    > Wartości te nie są prawdziwe. Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości. Skontaktuj się z [zespołem pomocy technicznej klienta usługi ServiceNow](https://www.servicenow.com/support/contact-support.html) uzyskać te wartości.

4. Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_certificate.png)

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_general_400.png)

6. Jedno kliknięcie skonfigurować usługę została podana dla usługi ServiceNow oznacza to, aby na platformie Azure AD automatycznie skonfigurować usługi ServiceNow dla uwierzytelniania opartego na SAML. Aby włączyć tę usługę, przejdź do **konfiguracji usługi ServiceNow** kliknij **skonfigurować usługi ServiceNow** można otworzyć Konfigurowanie logowania jednokrotnego okna.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_configure.png)

7. Wprowadź nazwę wystąpienia usługi ServiceNow, nazwa użytkownika i hasło administratora w **Konfigurowanie logowania jednokrotnego** tworzą, a następnie kliknij przycisk **Konfiguruj teraz**. Należy pamiętać, że podana nazwa użytkownika administratora musi mieć **security_admin** rola przypisana w usługi ServiceNow tej pracy. W przeciwnym razie, aby ręcznie skonfigurować usługi ServiceNow przy użyciu usługi Azure AD jako dostawca tożsamości SAML, kliknij przycisk **ręcznie skonfigurować logowanie jednokrotne** i skopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z sekcji krótkimi opisami.

    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/configure.png "skonfigurować adres URL aplikacji")

8. Zaloguj się do aplikacji usługi ServiceNow Express jako administrator.

9. W okienku nawigacji po lewej stronie kliknij **rejestracji jednokrotnej**.

    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "skonfigurować adres URL aplikacji")

10. Na **rejestracji jednokrotnej** okna dialogowego, kliknij ikonę konfiguracji w prawym górnym rogu i ustaw następujące właściwości:

    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "skonfigurować adres URL aplikacji")

    a. Przełącz **włączyć wiele dostawcy logowania jednokrotnego** z prawej strony.
    
    b. Przełącz **debugowania Włącz rejestrowanie dla wielu dostawcy logowania jednokrotnego integracji** z prawej strony.
    
    c. W **tabeli pole użytkownika, który...**  pole tekstowe, typ **nazwa_użytkownika**.

11. Na **rejestracji jednokrotnej** okna dialogowego, kliknij przycisk **Dodaj nowy certyfikat**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "skonfigurować logowanie jednokrotne")

12. Na **certyfikatów X.509** okna dialogowego, wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694975.png "skonfigurować logowanie jednokrotne")

    a. W **nazwa** tekstowym, wpisz nazwę konfiguracji (na przykład: **TestSAML2.0**).

    b. Wybierz **Active**.

    c. Jako **Format**, wybierz pozycję **PEM**.

    d. Jako **typu**, wybierz pozycję **zaufania certyfikatów magazynu**.

    e. Otwórz z certyfikatu szyfrowania Base64 pobrany z portalu Azure w programie Notatnik, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu PEM** pola tekstowego.

    f. Kliknij przycisk **aktualizacji**

13. Na **rejestracji jednokrotnej** okna dialogowego, kliknij przycisk **Dodaj nowe IdP**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "skonfigurować logowanie jednokrotne")

14. Na **Dodaj nowego dostawcę tożsamości** okna dialogowego, w obszarze **Konfigurowanie dostawcy tożsamości**, wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "skonfigurować logowanie jednokrotne")

    a. W **nazwa** tekstowym, wpisz nazwę konfiguracji (na przykład: **SAML 2.0**).

    b. W **adres URL dostawcy tożsamości** pól, Wklej wartość **identyfikator dostawcy tożsamości** którego została skopiowana z portalu Azure.
    
    c. W **AuthnRequest dostawcy tożsamości** pól, Wklej wartość **adres URL żądania uwierzytelniania** , które zostały skopiowane z portalu Azure.

    d. W **SingleLogoutRequest dostawcy tożsamości** pól, Wklej wartość **pojedynczy adres URL usługi Sign-Out** którego została skopiowana z portalu Azure

    e. Jako **certyfikat dostawcy tożsamości**, wybierz certyfikat został utworzony w poprzednim kroku.

15. Kliknij przycisk **Zaawansowane ustawienia**, a następnie w obszarze **dodatkowe właściwości dostawcy tożsamości**, wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "skonfigurować logowanie jednokrotne")

    a. W **powiązanie protokołu IDP SingleLogoutRequest** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:bindings:HTTP-przekierowania**.

    b. W **zasad NameID** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: nieokreślony**.

    c. W **metody AuthnContextClassRef**, typ `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.

    d. Anuluj wybór **utworzyć AuthnContextClass**.

16. W obszarze **dodatkowe właściwości dostawcy usług**, wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "skonfigurować logowanie jednokrotne")

    a. W **strony głównej usługi ServiceNow** tekstowym, wpisz adres URL strony głównej wystąpienia usługi ServiceNow.

    > [!NOTE]
    > Na stronie głównej wystąpienia usługi ServiceNow jest złączeniem Twojej **adres URL dzierżawy ServieNow** i **/navpage.do** (na przykład: `https://fabrikam.service-now.com/navpage.do`).

    b. W **identyfikator podmiot / wystawca** pole tekstowe, wpisz adres URL dzierżawy usługi ServiceNow.

    c. W **identyfikatora URI odbiorców** tekstowym, wpisz adres URL dzierżawy usługi ServiceNow.

    d. W **pochylanie zegara** pole tekstowe, typ **60**.

    e. W **pole użytkownika** pole tekstowe, typ **e-mail** lub **nazwa_użytkownika**, w zależności od pole, które jest używane do unikatowego identyfikowania użytkowników w danym wdrożeniu usługi ServiceNow.

    > [!NOTE]
    > Można skonfigurować usługi Azure AD, aby emitować identyfikator użytkownika usługi Azure AD (główna nazwa użytkownika) lub adres e-mail jako unikatowy identyfikator w tokenie SAML, przechodząc do **ServiceNow > atrybuty > logowanie jednokrotne** części portalu Azure mapowania odpowiednie pola i **nameidentifier** atrybutu. Wartość przechowywana wybranego atrybutu w usłudze Azure AD (na przykład główna nazwa użytkownika) musi odpowiadać wartości przechowywane w usługi ServiceNow wprowadzone pola (na przykład nazwa_użytkownika)

    f. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu. Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-servicenow-tutorial/create_aaduser_01.png)

2. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-servicenow-tutorial/create_aaduser_02.png)

3. Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.

    ![Przycisk Dodaj](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png)

4. W **użytkownika** okna dialogowego wykonaj następujące czynności:

    ![Okno dialogowe użytkownika](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png)

    a. W **nazwa** wpisz **BrittaSimon**.

    b. W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.

    c. Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-servicenow-test-user"></a>Tworzenie użytkownika testowego usługi ServiceNow

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w usługi ServiceNow. Jeśli nie wiadomo, jak dodać użytkownika w ramach konta usługi ServiceNow lub usługi ServiceNow Express, skontaktuj się z [zespołem pomocy technicznej usługi ServiceNow klienta](https://www.servicenow.com/support/contact-support.html)

### <a name="assign-the-azure-ad-test-user"></a>Przypisz użytkownika testowego usługi Azure AD

W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do usługi ServiceNow.

![Przypisanie roli użytkownika][200] 

**Aby przypisać Simona Britta usługi ServiceNow, wykonaj następujące czynności:**

1. W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **ServiceNow**.

    ![Łącze usługi ServiceNow na liście aplikacji](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_app.png)  

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Łącze "Użytkownicy i grupy"][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![W okienku Dodaj przydziału][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Po kliknięciu kafelka usługi ServiceNow w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji usługi ServiceNow.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png

