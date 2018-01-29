---
title: "Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML zlewiska przez firmę Microsoft | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i logowania jednokrotnego SAML zlewiska przez firmę Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2018
ms.author: jeedes
ms.openlocfilehash: 22189c3d2d2164ba0fa3c2d790c36361fb0f5854
ms.sourcegitcommit: 28178ca0364e498318e2630f51ba6158e4a09a89
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a>Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML zlewiska przez firmę Microsoft

Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) logowania jednokrotnego SAML zlewiska przez firmę Microsoft.

Integracja z usługą Azure AD logowania jednokrotnego SAML zlewiska przez firmę Microsoft zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do logowania jednokrotnego SAML zlewiska przez firmę Microsoft
- Umożliwia użytkownikom automatycznie pobrać zalogowane do logowania jednokrotnego SAML zlewiska przez firmę Microsoft (logowanie jednokrotne) z konta usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="description"></a>Opis:

Korzystać z serwera zlewiska Atlassian konta Microsoft Azure Active Directory, aby włączyć logowanie jednokrotne. W ten sposób wszyscy użytkownicy organizacji można używać poświadczeń usługi Azure AD do logowania do aplikacji zlewiska. Ten dodatek plug-in używa SAML 2.0 dla Federacji.

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z logowania jednokrotnego SAML zlewiska przez firmę Microsoft, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Aplikacja serwera zlewiska zainstalowany na serwerze Windows 64-bitowych (lokalnie lub w chmurze infrastruktury IaaS)
- Serwer zlewiska jest obsługujące protokół HTTPS
- Należy pamiętać, że obsługiwane wersje dla wtyczki zlewiska są wymienione w poniższej sekcji.
- Zlewiska serwer jest dostępny w Internecie, szczególnie do strony logowania usługi AD platformy Azure do uwierzytelniania i powinien otrzymywać token z usługi Azure AD
- Poświadczenia administratora są konfigurowane w zlewiska
- WebSudo jest wyłączona w zlewiska
- Użytkownika testowego utworzone w zlewiska aplikacji serwera

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego programu zlewiska. Przetestowanie integracji w rozwoju lub środowisko przejściowe aplikacji, a następnie użyj środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="supported-versions-of-confluence"></a>Obsługiwane wersje zlewiska 

Od tej chwili obsługiwane są następujące wersje zlewiska:

- Zlewiska: 5.10 do 5.0

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie logowania jednokrotnego SAML zlewiska przez firmę Microsoft z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-confluence-saml-sso-by-microsoft-from-the-gallery"></a>Dodawanie logowania jednokrotnego SAML zlewiska przez firmę Microsoft z galerii
Aby skonfigurować integrację logowania jednokrotnego SAML zlewiska przez firmę Microsoft do usługi Azure AD, należy dodać logowania jednokrotnego SAML zlewiska przez firmę Microsoft z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać logowania jednokrotnego SAML zlewiska przez firmę Microsoft z galerii, wykonaj następujące czynności:**

1. W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania wpisz **logowania jednokrotnego SAML zlewiska przez firmę Microsoft**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. W panelu wyników wybierz **logowania jednokrotnego SAML zlewiska przez firmę Microsoft**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML zlewiska przez firmę Microsoft, w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w logowania jednokrotnego SAML zlewiska przez firmę Microsoft jest dla użytkownika, w usłudze Azure AD. Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w logowania jednokrotnego SAML zlewiska przez firmę Microsoft.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML zlewiska przez firmę Microsoft, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie logowania jednokrotnego SAML zlewiska przez użytkownika testowego Microsoft](#creating-a-confluence-saml-sso-by-microsoft-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta logowania jednokrotnego SAML zlewiska przez firmy Microsoft, który jest połączony z usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i konfigurowanie rejestracji jednokrotnej w sieci logowania jednokrotnego SAML zlewiska przez aplikację Microsoft.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML zlewiska przez firmę Microsoft, wykonaj następujące czynności:**

1. W portalu Azure na **logowania jednokrotnego SAML zlewiska przez firmę Microsoft** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. Na **logowania jednokrotnego SAML zlewiska Domain firmy Microsoft i adresy URL** sekcji, wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    a. W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<domain:port>/plugins/servlet/saml/auth`

    b. W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<domain:port>/`

    d. W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości. Port jest opcjonalny w przypadku, gdy jest nazwane adres URL. Te wartości są odbierane podczas konfigurowania zlewiska dodatek, który znajduje się w dalszej części tego samouczka.
 

4. Aby wygenerować **metadanych** adres url, wykonaj następujące czynności:

    a. Kliknij przycisk **rejestracji aplikacji**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    b. Kliknij przycisk **punkty końcowe** otworzyć **punkty końcowe** okno dialogowe.  
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    d. Kliknij przycisk Kopiuj, aby skopiować **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    d. Teraz przejdź do strony właściwości **logowania jednokrotnego SAML zlewiska przez firmę Microsoft** i skopiuj **identyfikator aplikacji** przy użyciu **kopiowania** przycisk i wklej go do Notatnika.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    e. Generowanie **adres URL metadanych** przy użyciu następującego wzorca: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` i skopiuj tę wartość w programie Notatnik, ponieważ jest później używany dla konfiguracji wtyczki.

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do Twojego wystąpienia zlewiska.

7. Umieść kursor na koło zębate, a następnie kliknij przycisk **dodatki**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

8. Pobierz dodatek z [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=56503). Ręcznie przekazać wtyczki, używając Microsoft **przekazać dodatek** menu
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon12.png)

9. Po zainstalowaniu dodatku plug-in pojawia się w **użytkownik zainstalował** sekcji dodatki **zarządzania dodatkami** sekcji. Kliknij przycisk **Konfiguruj** do skonfigurowania nowej wtyczki.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon13.png)

10. Wykonaj następujące kroki na stronie konfiguracji:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon52.png)
 
    > [!TIP]
    > Upewnij się, że istnieje tylko jeden certyfikat mapowany aplikacji tak, aby nie było błędu rozpoznawania metadanych. Jeśli dostępnych jest wiele certyfikatów, administrator pobiera wystąpił błąd podczas rozpoznawania metadanych.

    a. W **adres URL metadanych** Wklej **adres URL metadanych** z usługi Azure AD i kliknij przycisk **rozwiązać** przycisku. Adres URL metadanych IdP odczytuje i wypełnienie wszystkich pól informacji.

    b. Kopiuj **identyfikator, adres URL odpowiedzi i zaloguj się na adres URL** wartości i wklej je w **identyfikator, adres URL odpowiedzi i zaloguj się na adres URL** odpowiednio do pól tekstowych **logowania jednokrotnego SAML zlewiska Domain firmy Microsoft i adresy URL**  sekcji z portalu Azure.

    d. W **nazwa przycisku logowania** wpisz nazwę przycisku przez organizację nowych użytkowników na ekranie logowania.

    d. W **lokalizacje identyfikator użytkownika SAML**, wybierz opcję **identyfikator użytkownika jest w elemencie NameIdentifier instrukcji podmiotu** lub **identyfikator użytkownika jest w elemencie atrybutu**.  Ten identyfikator ma być zlewiska identyfikator użytkownika. Jeśli identyfikator użytkownika nie jest zgodny, następnie system uniemożliwi użytkownikom logować się. 

    > [!Note]
    > Domyślna lokalizacja SAML użytkownika identyfikator to identyfikator nazwy. Można to zmienić opcję atrybutu i wprowadź odpowiednią nazwę.
    
    e. W przypadku wybrania **identyfikator użytkownika jest w elemencie atrybutu** opcji, a następnie w **nazwa atrybutu** pole tekstowe wpisz nazwę atrybutu, gdy oczekiwano identyfikatora użytkownika. 

    f. Jeśli korzystasz z domeny federacyjnej (na przykład usług AD FS itp.) z usługą Azure AD, należy kliknąć opcję **Włączanie odnajdowania obszaru macierzystego** opcji i skonfigurować **nazwy domeny**.
    
    g. W **nazwy domeny** wpisz nazwę domeny, w tym miejscu w przypadku logowania za pomocą usług AD FS.

    h. Sprawdź **włączyć pojedynczego Wyloguj** chcesz wylogować się z usługi Azure AD, gdy użytkownik zaloguje z zlewiska. 

    i. Kliknij przycisk **zapisać** przycisk, aby zapisać ustawienia.


> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu. Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    a. W **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.

    d. Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a>Tworzenie logowania jednokrotnego SAML zlewiska przez użytkownika testowego firmy Microsoft

Aby umożliwić użytkownikom usługi Azure AD zalogować się do zlewiska na serwerze lokalnym, ich muszą mieć przydzielone do logowania jednokrotnego SAML zlewiska przez firmę Microsoft. W przypadku logowania jednokrotnego SAML zlewiska przez firmę Microsoft inicjowania obsługi administracyjnej jest zadanie ręczne.

**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**

1. Zaloguj się do Twojego zlewiska na lokalnym serwerze jako administrator.

2. Umieść kursor na koło zębate, a następnie kliknij przycisk **Zarządzanie użytkownikami**.

    ![Dodawanie pracownika](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. W sekcji Użytkownicy kliknij **dodawania użytkowników** kartę. Na **dodać użytkownika** okna dialogowego strony, należy wykonać następujące czynności:

    ![Dodawanie pracownika](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    a. W **Username** tekstowym, wpisz adres e-mail użytkownika, takich jak Simona Britta.

    b. W **imię i nazwisko** tekstowym, wpisz pełną nazwę użytkownika, takich jak Simona Britta.

    d. W **E-mail** tekstowym, wpisz adres e-mail użytkownika, takich jak Brittasimon@contoso.com.

    d. W **hasło** tekstowym, wpisz hasło dla Simona Britta.

    e. Kliknij przycisk **Potwierdź hasło** wprowadź ponownie hasło.
    
    f. Kliknij przycisk **Dodaj** przycisku.

### <a name="assigning-the-azure-ad-test-user"></a>Przypisanie użytkownika testowego usługi Azure AD

W tej sekcji musisz włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do logowania jednokrotnego SAML zlewiska przez firmę Microsoft.

![Przypisz użytkownika][200] 

**Aby przypisać Simona Britta do logowania jednokrotnego SAML zlewiska przez firmę Microsoft, wykonaj następujące czynności:**

1. W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **logowania jednokrotnego SAML zlewiska przez firmę Microsoft**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Po kliknięciu logowania jednokrotnego SAML zlewiska przez Kafelek firmy Microsoft w panelu dostępu należy powinien pobrać automatycznie zalogowane do użytkownika logowania jednokrotnego SAML zlewiska przez aplikację Microsoft.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Zasoby dodatkowe

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

