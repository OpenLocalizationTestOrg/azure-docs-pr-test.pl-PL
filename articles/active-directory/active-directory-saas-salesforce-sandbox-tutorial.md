---
title: 'Samouczek: Integracji Azure Active Directory z piaskownicy Salesforce | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse piaskownicy usługi Salesforce z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Samouczek: Integracji Azure Active Directory z piaskownicy usług Salesforce

Celem Hello tego samouczka jest tooshow integracji hello Azure i usługi Salesforce piaskownicy.  

>[!TIP]
>Opinii, zobacz hello [stronę pomocy technicznej platformy Azure](http://go.microsoft.com/fwlink/?LinkId=521878). 
> 

Nadaj piaskownic możesz tekst hello toocreate możliwości wielu kopii organizacji w oddzielnych środowisk do różnych celów, takich jak projektowanie, testowanie i uczenie bez naruszenia hello danych i aplikacji w produkcji usług Salesforce organizacja.  

Aby uzyskać więcej informacji, zobacz [piaskownicy — omówienie](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

* Ważnej subskrypcji platformy Azure
* Piaskownica w witrynie Salesforce.com

Jeśli nie masz jeszcze prawidłowy piaskownicy w witrynie Salesforce.com, należy toocontact Salesforce.

Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:

1. Włączanie integracji aplikacji hello piaskownica usług Salesforce
2. Konfigurowanie rejestracji jednokrotnej (SSO)
3. Włączanie domeny
4. Konfigurowanie Inicjowanie obsługi użytkowników
5. Przypisywanie użytkowników

![Scenariusz](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "scenariusza")

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a>Włącz integrację aplikacji hello piaskownica usług Salesforce
Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable piaskownica Salesforce.

**Integracja aplikacji hello tooenable piaskownica Salesforce, wykonaj hello następujące kroki:**

1. W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.
   
   ![Usługi Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "usługi Active Directory")
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
   ![Aplikacje](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "aplikacji")
4. Witaj tooopen **galerii aplikacji**, kliknij przycisk **Dodaj aplikację**, a następnie kliknij przycisk **Dodawanie aplikacji dla mojej organizacji toouse**.
   
   ![Co chcesz toodo? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Co chcesz toodo?")
5. W hello **pole wyszukiwania**, typ **piaskownicy Salesforce**.
   
   ![Galerii aplikacji](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "galerii aplikacji")
6. Wybierz w okienku wyników hello **piaskownicy Salesforce**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
   ![Piaskownica SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce piaskownicy")
   
## <a name="configur-single-sign-on-sso"></a>Configur rejestracji jednokrotnej (SSO)

Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooSalesforce do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.

**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure na powitania **piaskownicy Salesforce** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okno dialogowe.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "skonfigurować logowanie jednokrotne")
2. Na powitania **jak ma toosign użytkowników na tooSalesforce piaskownicy** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
   ![Piaskownica SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce piaskownicy")
3. Na powitania **Konfigurowanie adresu URL aplikacji** strony w hello **na adres URL logowania** pole tekstowe, wpisz adres URL przy użyciu następującego wzorca hello `http://company.my.salesforce.com`, a następnie kliknij przycisk **dalej**.
   
   ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "skonfigurować adres URL aplikacji")
4. Jeśli skonfigurowano już program rejestracji jednokrotnej dla innego wystąpienia usług Salesforce piaskownicy w katalogu, a następnie należy także skonfigurować hello **identyfikator** toohave hello tę samą wartość jak hello **Zaloguj się na adres URL**. 
 * Witaj **identyfikator** pola można znaleźć, sprawdzając hello **Pokaż zaawansowane ustawienia** wyboru na powitania **Konfigurowanie adresu URL aplikacji** stronę hello okna dialogowego.
5. Na powitania **skonfigurować logowanie jednokrotne w piaskownicy Salesforce** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu hello na tym komputerze.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "skonfigurować logowanie jednokrotne")
6. W oknie przeglądarki innej witryny sieci web Zaloguj się do Twojego piaskownicy Salesforce jako administrator.
7. W menu hello na górze hello, kliknij przycisk **Instalatora**.
   
   ![Instalator](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Instalatora")
8. W okienku nawigacji hello po lewej stronie powitania kliknij **kontroli bezpieczeństwa**, a następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.
   
   ![Single Sign-On ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On ustawienia")
9. Witaj w sekcji Ustawienia rejestracji jednokrotnej wykonywanie hello następujące kroki:
   
   ![Single Sign-On ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On ustawienia")  
 1.  Wybierz **SAML włączone**. 
 2.  Kliknij przycisk **Nowy**.
10. Witaj SAML pojedynczy znak w sekcji Ustawienia wykonywanie hello następujące kroki:
    
    ![SAML pojedynczego logowania jednokrotnego ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML jednego ustawienia rejestracji")  
 1. W polu tekstowym Nazwa hello, wpisz nazwę hello hello konfiguracji (np.: *SPSSOWAAD\_testu*). 
 2. W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w piaskownicy Salesforce** dialogu strony, hello kopiowania **adres URL wystawcy** wartość, a następnie wklej go do hello **wystawcy**pola tekstowego.
 3. W hello **identyfikator jednostki** pole tekstowe, typ **https://test.salesforce.com** Jeśli jest to hello pierwszego wystąpienia usług Salesforce piaskownicy dodajesz tooyour katalogu. Jeśli masz już dodany wystąpienia usług Salesforce piaskownicy, a następnie dla hello **identyfikator jednostki** typu w hello **na adres URL logowania**, która powinna być w następującym formacie:`http://company.my.salesforce.com`   
 4. Kliknij przycisk **Przeglądaj** tooupload hello pobrać certyfikatu.  
 5. Jako **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera hello identyfikator federacyjnej z obiektu użytkownika hello**. 
 6. Jako **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentifier hello hello instrukcji podmiotu**.
 7. W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w piaskownicy Salesforce** dialogu strony, hello kopiowania **zdalnego adresu URL logowania** wartość, a następnie wklej go do hello **dostawcy tożsamości Adres URL logowania** pola tekstowego. 
 8. SFDC nie obsługuje SAML wylogowania.  Jako obejście, Wklej "https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0" go do hello **adres URL wylogowania dostawcy tożsamości** pola tekstowego.
 9. Jako **dostawcy zainicjował żądanie powiązania usługi**, wybierz pozycję **HTTP POST**. 
 10. Kliknij pozycję **Zapisz**.
11. Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "skonfigurować logowanie jednokrotne")

## <a name="enable-your-domain"></a>Włącz domeny
W tej sekcji założono, że już utworzono domeny.  Aby uzyskać więcej informacji, zobacz [Definiowanie Twojej nazwy domeny](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable domeny, wykonaj następujące kroki hello:**

1. W okienku nawigacji po lewej stronie powitania kliknij **Zarządzanie domenami**, a następnie kliknij przycisk **Moje domeny.**
   
   ![Mojej domeny](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "mojej domeny")
   
   >[!NOTE]
   >Upewnij się, że poprawnie skonfigurowano domenę. 
   > 
2. W hello **ustawienia strony logowania** , kliknij przycisk **Edytuj**, następnie jako **usługi uwierzytelniania**, wybierz nazwę hello hello SAML pojedynczego logowania jednokrotnego ustawienia z poprzednich hello sekcja, a na koniec kliknij **zapisać**.
   
   ![Mojej domeny](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "mojej domeny")

Jak masz domenę skonfigurowane, użytkownicy należy używać hello domeny adres URL toologin toohello Salesforce piaskownicy.  

wartość hello tooget hello adresu URL, kliknij profil rejestracji Jednokrotnej hello, utworzony w poprzedniej sekcji hello.

## <a name="configure-user-provisioning"></a>Skonfiguruj Inicjowanie obsługi użytkowników
Celem Hello w tej sekcji jest toooutline jak tooenable użytkownika usługi Active Directory Inicjowanie obsługi użytkowników kont tooSalesforce piaskownicy.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. W portalu usługi Salesforce hello hello górnym pasku nawigacyjnym wybierz tooexpand Twojej nazwy użytkownika menu użytkownika:
   
   ![Ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Moje ustawienia")
2. Wybierz z menu programu użytkownika **Moje ustawienia** tooopen Twojego **Moje ustawienia** strony.
3. W okienku po lewej stronie powitania kliknij **osobistych** tooexpand hello sekcji osobistych, a następnie kliknij przycisk **zresetować moje tokenu zabezpieczeń**:
   
   ![Ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Moje ustawienia")
4. Na powitania **zresetować moje tokenu zabezpieczeń** kliknij przycisk **zresetować tokenu zabezpieczeń** toorequest wiadomości e-mail, który zawiera token zabezpieczeń witryny Salesforce.com.
   
   ![Nowy Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "nowy Token")
5. Sprawdź skrzynki odbiorczej poczty e-mail, wiadomości e-mail z witryny Salesforce.com z "**potwierdzenia zabezpieczeń salesforce.com.com**" jako podmiotu.
6. Przejrzyj tej wiadomości e-mail i skopiuj hello zabezpieczeń wartość tokenu.
7. W hello klasycznego portalu Azure na powitania **salesforce piaskownicy** strona integracji aplikacji, kliknij przycisk **skonfigurować Inicjowanie obsługi użytkowników** tooopen hello **skonfigurować Inicjowanie obsługi użytkowników**okna dialogowego.
   
   ![Skonfiguruj Inicjowanie obsługi użytkowników](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "skonfigurować Inicjowanie obsługi użytkowników")
8. Na powitania **Wprowadź użytkownika piaskownicy Salesforce poświadczenia tooenable automatyczne Inicjowanie obsługi użytkowników** Podaj hello następujące ustawienia konfiguracji:
   
   ![Piaskownica SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce piaskownicy")   
 1. W hello **nazwa użytkownika administratora piaskownicy Salesforce** tekstowym, wpisz nazwę, która ma hello konta piaskownicy Salesforce **administratorem** profilu w witrynie Salesforce.com przypisane.
 2. W hello **hasło administratora piaskownicy Salesforce** tekstowym, wpisz hello hasło dla tego konta.
 3. W hello **tokenu zabezpieczeń użytkownika** pole tekstowe, wartość tokenu zabezpieczeń hello wklejania.
 4. Kliknij przycisk **weryfikacji** tooverify konfiguracji.
 5. Kliknij przycisk hello **dalej** hello tooopen przycisk **potwierdzenie** strony.
9. Na powitania **potwierdzenie** kliknij przycisk **Complete** toosave konfiguracji.
   
## <a name="assigning-users"></a>Przypisywanie użytkowników

tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.

**tooassign użytkowników tooSalesforce piaskownicy, wykonaj hello następujące kroki:**

1. W hello klasycznego portalu Azure Utwórz konto testu.
2. Na powitania ** piaskownicy Salesforce ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.
   
   ![Przypisywanie użytkowników](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "przypisywanie użytkowników")
3. Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.
   
   ![Tak](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "tak")

Należy teraz Odczekaj 10 minut i sprawdź, czy konto hello zostało zsynchronizowane tooSalesforce piaskownicy.

Jeśli chcesz tootest ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](https://msdn.microsoft.com/library/dn308586).

