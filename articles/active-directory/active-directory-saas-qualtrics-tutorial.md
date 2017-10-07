---
title: 'Samouczek: Integracji Azure Active Directory z Qualtrics | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse Qualtrics z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a>Samouczek: Integracji Azure Active Directory z Qualtrics
Celem Hello tego samouczka jest tooshow integracji hello Azure i Qualtrics.  

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

* Ważnej subskrypcji platformy Azure
* Qualtrics rejestracji jednokrotnej (SSO) włączone subskrypcji

Ten samouczek użytkownicy hello Azure AD przypisano tooQualtrics będą mogli toosingle logowania do aplikacji hello w witrynie firmy Qualtrics (usługa zainicjował dostawcy logowania) lub przy użyciu hello [toohello wprowadzenie Dostęp do panelu](active-directory-saas-access-panel-introduction.md).

Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:

1. Włączanie integracji aplikacji hello dla Qualtrics
2. Konfigurowanie rejestracji jednokrotnej (SSO)
3. Konfigurowanie Inicjowanie obsługi użytkowników
4. Przypisywanie użytkowników

![Scenariusz](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "scenariusza")

## <a name="enabling-hello-application-integration-for-qualtrics"></a>Włączanie integracji aplikacji hello dla Qualtrics
Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla Qualtrics.

**integracji aplikacji hello tooenable dla Qualtrics, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.
   
   ![Usługi Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "usługi Active Directory")
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
   ![Aplikacje](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "aplikacji")
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
   ![Dodaj aplikację](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Dodaj aplikację")
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
   ![Dodawanie aplikacji z gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "dodać aplikację z gallerry")
6. W hello **pole wyszukiwania**, typ **Qualtrics**.
   
   ![Galerii aplikacji](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "galerii aplikacji")
7. Wybierz w okienku wyników hello **Qualtrics**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
   ![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")
   
## <a name="configure-single-sign-on"></a>Konfigurowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooQualtrics do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.

**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure na powitania **Qualtrics** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "skonfigurować logowanie jednokrotne")
2. Na powitania **jak ma toosign użytkowników na tooQualtrics** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "skonfigurować logowanie jednokrotne")
3. Na powitania **Konfigurowanie adresu URL aplikacji** strony w hello **Qualtrics na adres URL logowania** pole tekstowe, wpisz adres URL (np.: "*https://ssotest2ut1.qualtrics.com*"), a następnie kliknij przycisk **Dalej**.
   
   ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "skonfigurować adres URL aplikacji")
4. Na powitania **skonfigurować logowanie jednokrotne w Qualtrics** kliknij przycisk **pobierania metadanych**, a następnie zapisz plik metadanych hello na tym komputerze.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "skonfigurować logowanie jednokrotne")
5. Wyślij hello metadanych pliku toohello Qualtrics zespołem pomocy technicznej.
   
   >[!NOTE]
   >Konfiguracja rejestracji Jednokrotnej Hello ma toobe wykonywane przez hello Qualtrics zespołem pomocy technicznej. Otrzymasz powiadomienie, jak hello konfiguracji została ukończona.
   > 
   > 
6. Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "skonfigurować logowanie jednokrotne")
   
## <a name="configure-user-provisioning"></a>Skonfiguruj Inicjowanie obsługi użytkowników

Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooQualtrics. Gdy przypisany użytkownik podejmie próbę toolog do Qualtrics za pomocą panelu dostępu hello, Qualtrics sprawdza, czy istnieje hello użytkownika.  

Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez Qualtrics.

## <a name="assign-users"></a>Przypisywanie użytkowników
tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.

**tooassign tooQualtrics użytkowników, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure Utwórz konto testu.
2. Na powitania **Qualtrics** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.
   
   ![Przypisywanie użytkowników](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "przypisywanie użytkowników")
3. Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.
   
   ![Tak](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "tak")

Jeśli chcesz tootest ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

