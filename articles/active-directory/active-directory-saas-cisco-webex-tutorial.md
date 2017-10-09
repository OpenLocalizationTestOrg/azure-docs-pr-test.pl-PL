---
title: "Samouczek: Integracji usługi Azure Active Directory z Cisco Webex | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Cisco Webex z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a>Samouczek: Integracji usługi Azure Active Directory z Cisco Webex
Celem Hello tego samouczka jest tooshow integracji hello Azure i Cisco Webex.  
Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

* Ważnej subskrypcji platformy Azure
* Dzierżawy Cisco Webex

Ten samouczek hello użytkowników usługi Azure AD przypisano tooCisco Webex będą mogli toosingle logowania do aplikacji hello w witrynie firmy Cisco Webex (usługa zainicjował dostawcy logowania) lub przy użyciu hello [toohello wprowadzenie Dostęp do panelu](active-directory-saas-access-panel-introduction.md).

Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:

* Włączanie integracji aplikacji hello dla Cisco Webex
* Konfigurowanie rejestracji jednokrotnej (SSO)
* Konfigurowanie Inicjowanie obsługi użytkowników
* Przypisywanie użytkowników

![Scenariusz](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "scenariusza")

## <a name="enable-hello-application-integration-for-cisco-webex"></a>Włącz integrację aplikacji hello dla Cisco Webex
Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla Cisco Webex.

**Integracja aplikacji hello tooenable dla Cisco Webex wykonaj hello następujące kroki:**

1. W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.
   
   ![Usługi Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "usługi Active Directory")
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
   ![Aplikacje](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "aplikacji")
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
   ![Dodaj aplikację](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Dodaj aplikację")
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
   ![Dodawanie aplikacji z gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "dodać aplikację z gallerry")
6. W hello **pole wyszukiwania**, typ **Cisco Webex**.
   
   ![Galerii aplikacji](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "galerii aplikacji")
7. Wybierz w okienku wyników hello **Cisco Webex**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
   ![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")
   
## <a name="configure-single-sign-on"></a>Konfigurowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooCisco Webex do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.  

W ramach tej procedury jest wymagana toocreate zakodowanego certyfikatu base-64. Jeśli nie masz doświadczenia z tej procedury, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure na powitania **Cisco Webex** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "skonfigurować logowanie jednokrotne")
2. Na powitania **jak ma toosign użytkowników na tooCisco Webex** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "skonfigurować logowanie jednokrotne")
3. Na powitania **Konfigurowanie adresu URL aplikacji** , wykonaj następujące kroki hello, a następnie kliknij przycisk **dalej**.
   
   ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "skonfigurować adres URL aplikacji")   
   1. W hello **rejestrują na adres URL** tekstowym, wpisz adres URL dzierżawy Cisco Webex (np.: *http://contoso.webex.com*).
   2. W hello **adres URL odpowiedzi Webex Cisco** pole tekstowe, typ użytkownika **adres URL AssertionConsumerService Webex Cisco** (np.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).
4. Na powitania **skonfigurować logowanie jednokrotne w Cisco Webex** strony, toodownload certyfikat, kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu hello na tym komputerze.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "skonfigurować logowanie jednokrotne")
5. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Cisco Webex jako administrator.
6. W menu hello na górze hello, kliknij przycisk **administrowania lokacją**.
   
   ![Administrowanie lokacją](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "lokacji administracyjnej")
7. W hello **zarządzania witryną** kliknij **konfiguracji logowania jednokrotnego**.
   
   ![Konfiguracja rejestracji Jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "konfiguracji logowania jednokrotnego")
8. W hello sekcji federacyjnych konfiguracji Usługa rejestracji Jednokrotnej w sieci Web wykonaj hello następujące kroki:
   
   ![Federacyjna usługa rejestracji Jednokrotnej w konfiguracji](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federacyjna usługa rejestracji Jednokrotnej w konfiguracji")  
   1. Z hello **protokołu federacyjnego** listy, wybierz **SAML 2.0**.
   2. Utwórz **algorytmem Base-64** pliku z pobranego certyfikatu.  
    >[!TIP]
    >Aby uzyskać więcej informacji, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)
    >  
   3. Otwórz certyfikatu zakodowanego base-64 w Notatniku i hello kopiowania zawartości z niego.
   4. Kliknij przycisk **Importowanie metadanych SAML**, a następnie wklej certyfikatu zakodowanego base-64.
   5. W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w Cisco Webex** strony okna dialogowego, hello kopiowania **adres URL wystawcy** wartość, a następnie wklej go do hello **wystawca SAML (identyfikator IdP)** pola tekstowego.
   6. W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w Cisco Webex** strony okna dialogowego, hello kopiowania **zdalnego adresu URL logowania** wartość, a następnie wklej go do hello **klienta logowania jednokrotnego usługi logowania Adres URL** pola tekstowego.
   7. Z hello **NameID Format** listy, wybierz **adres E-mail**.
   8. W hello **AuthnContextClassRef** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:ac:classes:Password**.
   9. W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w Cisco Webex** strony okna dialogowego, hello kopiowania **zdalnego adresu URL wylogowania** wartość, a następnie wklej go do hello **wylogowania usługi logowania jednokrotnego klienta Adres URL** pola tekstowego.
   10. Kliknij przycisk **aktualizacji**.
9. W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w Cisco Webex** strony okna dialogowego, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete**.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "skonfigurować logowanie jednokrotne")
   
## <a name="configure-user-provisioning"></a>Skonfiguruj Inicjowanie obsługi użytkowników

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Cisco Webex muszą mieć przydzielone do Cisco Webex.  

* W przypadku hello Cisco Webex Inicjowanie obsługi to zadanie ręczne.

**tooprovision kont użytkowników, wykonaj hello następujące kroki:**

1. Zaloguj się za tooyour **Cisco Webex** dzierżawy.
2. Przejdź za**Zarządzanie użytkownikami \> Dodaj użytkownika**.
   
   ![Dodawanie użytkowników](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Dodawanie użytkowników")
3. W sekcji Dodaj użytkownika hello wykonaj hello następujące kroki:
   
   ![Dodaj użytkownika](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Dodaj użytkownika")   
   1. Jako **typ konta**, wybierz pozycję **hosta**.
   2. Wpisz informacje hello istniejącego użytkownika usługi Azure AD do hello następujące pola tekstowe: **imię, nazwisko**, **nazwy użytkownika**, **E-mail**, **hasło**, **Potwierdź hasło**.
   3. Kliknij pozycję **Dodaj**.

>[!NOTE]
>Możesz użyć innych Cisco Webex użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Cisco Webex kont użytkowników usługi AAD. 
> 

## <a name="assign-users"></a>Przypisywanie użytkowników
tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.

**tooassign użytkowników tooCisco Webex, wykonaj hello następujące kroki:**

1. W hello klasycznego portalu Azure Utwórz konto testu.
2. Na powitania **Cisco Webex** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.
   
   ![Przypisywanie użytkowników](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "przypisywanie użytkowników")
3. Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.
   
   ![Tak](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "tak")

Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

