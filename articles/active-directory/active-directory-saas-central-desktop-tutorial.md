---
title: "Samouczek: Integracji Azure Active Directory przy użyciu centralnej pulpitu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse centralnej pulpitu z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a>Samouczek: Integracji Azure Active Directory przy użyciu centralnej pulpitu
Celem Hello tego samouczka jest tooshow integracji hello Azure i pulpitu centralnej. Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

* Ważnej subskrypcji platformy Azure
* Centralna pulpitu jednokrotne włączone subskrypcji / dzierżawy centralnej pulpitu

Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:

* Włączanie integracji aplikacji hello centralnej pulpitu
* Konfigurowanie rejestracji jednokrotnej (SSO)
* Konfigurowanie Inicjowanie obsługi użytkowników
* Przypisywanie użytkowników

![Scenariusz](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "scenariusza")

## <a name="enable-hello-application-integration-for-central-desktop"></a>Włącz integrację aplikacji hello centralnej pulpitu
Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable centralnej pulpitu.

**Integracja aplikacji hello tooenable centralnej pulpitu, wykonaj hello następujące kroki:**

1. W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.
   
   ![Usługi Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "usługi Active Directory")
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
   ![Aplikacje](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "aplikacji")
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
   ![Dodaj aplikację](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Dodaj aplikację")
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
   ![Dodawanie aplikacji z gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "dodać aplikację z gallerry")
6. W hello **pole wyszukiwania**, typ **centralnej pulpitu**.
   
   ![Galerii aplikacji](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "galerii aplikacji")
7. Wybierz w okienku wyników hello **centralnej pulpitu**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
   ![Centralna pulpitu](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "centralnej pulpitu")
   
## <a name="configure-single-sign-on"></a>Konfigurowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooCentral pulpitu do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.

W ramach tej procedury jest wymagana tooupload dzierżawcy centralnej pulpitu tooyour base-64 zakodowanego certyfikatu.  
Jeśli nie masz doświadczenia z tej procedury, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o).

**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure na powitania **centralnej pulpitu** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello ** skonfigurować rejestrację jednokrotną ** okna dialogowego.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "skonfigurować logowanie jednokrotne")
2. Na powitania **jak ma toosign użytkowników na pulpicie tooCentral** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "skonfigurować logowanie jednokrotne")
3. Na powitania **Konfigurowanie adresu URL aplikacji** , wykonaj następujące kroki hello, a następnie kliknij przycisk **dalej**: 
   
   1. W hello **centralnej pulpitu adres URL logowania** pole tekstowe, wprowadź adres URL hello dzierżawy centralnej pulpitu (np.: *http://contoso.centraldesktop.com*).
   2. W polu tekstowym adres URL odpowiedzi pulpitu Central hello, wpisz adres URL centralnej AssertionConsumerService pulpitu (np.: https://contoso.centraldesktop.com/saml2-assertion.php).
   
   >[!NOTE]
   >Można pobrać wartości hello z hello centralnej pulpitu metadanych (np.: *http://contoso.centraldesktop.com*).
   >  
   
   ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "skonfigurować adres URL aplikacji")
4. Na powitania **skonfigurować logowanie jednokrotne w centralnej pulpitu** strony, toodownload certyfikat, kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu hello na tym komputerze.
   
  ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "skonfigurować logowanie jednokrotne")
5. Zaloguj się za tooyour **centralnej pulpitu** dzierżawy.
6. Przejdź za**ustawienia**, kliknij przycisk **zaawansowane**, a następnie kliknij przycisk **rejestracji jednokrotnej**.
   
  ![Instalator — zaawansowane](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Instalator — zaawansowane")
7. Na powitania **pojedynczy znak na ustawienia** wykonaj hello następujące kroki:
   
  ![Rejestracja jednokrotna ustawień](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Rejestracja jednokrotna ustawień")
   
  1. Wybierz **Włącz SAML v2 logowania jednokrotnego**.
  2. W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w centralnej pulpitu** strony, hello kopiowania **adres URL wystawcy** wartość, a następnie wklej go do hello **adres URL logowania jednokrotnego** pola tekstowego.
  3. W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w centralnej pulpitu** strony, hello kopiowania **zdalnego adresu URL logowania** wartość, a następnie wklej go do hello **adres URL logowania jednokrotnego logowania**pola tekstowego.
  4. W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w centralnej pulpitu** strony, hello kopiowania **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej go do hello **adresu URL wylogowania logowania jednokrotnego** pola tekstowego.
8. W hello **metody weryfikacji podpisu wiadomości** sekcji, wykonaj następujące kroki hello:
   
   ![Metoda weryfikacji podpisu wiadomości](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "komunikatu metodę weryfikacji podpisu")
   
  1. Wybierz **certyfikatu**.
  2. Z hello **certyfikatu logowania jednokrotnego** listy, wybierz **RSH SHA256**.
  3. Utwórz plik tekstowy z certyfikatu hello pobrane, hello kopiowania zawartości z pliku tekstowego hello, a następnie wklej go do hello **certyfikatu logowania jednokrotnego** pola.  
     >[!TIP]
     >Aby uzyskać więcej informacji, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)
      >  
   4. Wybierz **wyświetlenia strony logowania łącze tooyour SAMLv2**.
9. Kliknij przycisk **aktualizacji**.
10. Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "skonfigurować logowanie jednokrotne")
    
## <a name="configure-user-provisioning"></a>Skonfiguruj Inicjowanie obsługi użytkowników

AAD użytkowników toobe stanie toosign w muszą być elastycznie toohello aplikacji centralnej pulpitu. W tej sekcji opisano, jak konta użytkowników usługi AAD toocreate w centralnej pulpitu.

**tooCentral kont użytkownika tooprovision pulpitu:**
1. Zaloguj się za tooyour dzierżawy centralnej pulpitu.
2. Przejdź za**osób \> wewnętrzne elementy członkowskie**.
3. Kliknij przycisk **Dodaj wewnętrzne elementy członkowskie**.
   
  ![Osoby](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "osób")
4. W hello **wiadomości E-mail adres z nowym elementom członkowskim** tekstowym, wpisz konto usługi AAD tooprovision, a następnie kliknij przycisk **dalej**.
   
  ![Adresy nowe elementy członkowskie e-mail](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "E-mail adresów nowych elementów członkowskich")
5. Kliknij przycisk **Dodaj wewnętrzne elementy członkowskie**.
   
  ![Dodawanie wewnętrznego elementu członkowskiego](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "dodać wewnętrznego elementu członkowskiego")
   
   >[!NOTE]
   >Użytkownicy Hello, dodane otrzymają wiadomość e-mail zawierającą link potwierdzenia muszą tooclick tooactivate hello konta.
   > 

>[!NOTE]
>Możesz użyć innych centralnej pulpitu użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez centralną pulpitu tooprovision kont użytkowników usługi AAD
>  

## <a name="assign-users"></a>Przypisywanie użytkowników
tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.

**tooassign tooCentral Użytkownicy pulpitu, wykonaj hello następujące kroki:**

1. W hello klasycznego portalu Azure Utwórz konto testu.
2. Na powitania **centralnej pulpitu** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.
   
   ![Przypisywanie użytkowników](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "przypisywanie użytkowników")
3. Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.
   
   ![Tak](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "tak")

Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

