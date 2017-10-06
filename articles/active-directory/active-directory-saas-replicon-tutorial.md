---
title: 'Samouczek: Integracji Azure Active Directory z Replicon | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse Replicon z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>Samouczek: Integracji Azure Active Directory z Replicon
Celem Hello tego samouczka jest tooshow integracji hello Azure i Replicon. Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

* Ważnej subskrypcji platformy Azure
* Dzierżawy Replicon

Ten samouczek użytkownicy hello Azure AD przypisano tooReplicon będą mogli toosingle logowania do aplikacji hello w witrynie firmy Replicon (usługa zainicjował dostawcy logowania) lub przy użyciu hello [toohello wprowadzenie dostępu Panel](active-directory-saas-access-panel-introduction.md).

Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:

1. Włączanie integracji aplikacji hello dla Replicon
2. Konfigurowanie rejestracji jednokrotnej (SSO)
3. Konfigurowanie Inicjowanie obsługi użytkowników
4. Przypisywanie użytkowników

![Scenariusz](./media/active-directory-saas-replicon-tutorial/IC777798.png "scenariusza")

## <a name="enable-hello-application-integration-for-replicon"></a>Włącz integrację aplikacji hello dla Replicon
Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla Replicon.

**integracji aplikacji hello tooenable dla Replicon, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.
   
    ![Usługi Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "usługi Active Directory")
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Aplikacje](./media/active-directory-saas-replicon-tutorial/IC700994.png "aplikacji")
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Dodaj aplikację](./media/active-directory-saas-replicon-tutorial/IC749321.png "Dodaj aplikację")
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
    ![Dodawanie aplikacji z gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "dodać aplikację z gallerry")
6. W hello **pole wyszukiwania**, typ **Replicon**.
   
    ![Galerii aplikacji](./media/active-directory-saas-replicon-tutorial/IC777799.png "galerii aplikacji")
7. Wybierz w okienku wyników hello **Replicon**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
    ![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")
   
## <a name="configure-single-sign-on"></a>Konfigurowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooReplicon do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.

**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure na powitania **Replicon** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-replicon-tutorial/IC777801.png "skonfigurować logowanie jednokrotne")
2. Na powitania **jak ma toosign użytkowników na tooReplicon** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-replicon-tutorial/IC777802.png "skonfigurować logowanie jednokrotne")
3. Na powitania **Konfigurowanie adresu URL aplikacji** wykonaj hello następujące kroki:
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-replicon-tutorial/IC777803.png "skonfigurować adres URL aplikacji")
  1. W hello **Replicon na adres URL logowania** tekstowym, wpisz adres URL dzierżawy Replicon (np.: *https://na2.replicon.com/company/saml2/sp-sso/post*).
  2. W hello **adres URL odpowiedzi Replicon** tekstowym, wpisz Replicon Twojego **AssertionConsumerService** adres URL (np.: *https://global.replicon.com/! / saml2/firmy/logowania jednokrotnego/post*).  
      
     >[!NOTE]
     >Można uzyskać adres URL hello hello Replicon metadanych w: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.
     > 
     > 
 
  3. Kliknij przycisk **Dalej**.

4. Na powitania **skonfigurować logowanie jednokrotne w Replicon** strony, toodownload metadanych programu kliknij przycisk **pobierania metadanych**, a następnie zapisz metadanych hello na tym komputerze.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-replicon-tutorial/IC777804.png "skonfigurować logowanie jednokrotne")
5. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Replicon jako administrator.

6. tooconfigure SAML 2.0, wykonaj następujące kroki hello:
   
    ![Włącz uwierzytelnianie SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "uwierzytelnianie Włącz SAML")
  
  1. Witaj toodisplay **EnableSAML Authentication2** okna dialogowego, Dołącz hello następującego adresu URL tooyour, po klucz firmy: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**  
    * Oto Hello hello schemat hello pełny adres URL:  
   **https://Na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**
   2. Kliknij przycisk hello  **+**  tooexpand hello **v20Configuration** sekcji.
   3. Kliknij przycisk hello  **+**  tooexpand hello **metaDataConfiguration** sekcji.
   4. Kliknij przycisk **wybierz plik**, tooselect Twojego pliku XML metadanych dostawcy tożsamości, a następnie kliknij przycisk **przesyłania**.

7. Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-replicon-tutorial/IC778418.png "skonfigurować logowanie jednokrotne")
   
## <a name="configure-user-provisioning"></a>Skonfiguruj Inicjowanie obsługi użytkowników

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Replicon muszą mieć przydzielone do Replicon.  

W przypadku hello Replicon Inicjowanie obsługi to zadanie ręczne.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. W oknie przeglądarki sieci web Zaloguj się do witryny firmy Replicon jako administrator.
2. Przejdź za**administracji \> użytkowników**.
   
    ![Użytkownicy](./media/active-directory-saas-replicon-tutorial/IC777806.png "użytkowników")
3. Kliknij przycisk **+ Dodaj użytkownika**.
   
    ![Dodaj użytkownika](./media/active-directory-saas-replicon-tutorial/IC777807.png "Dodaj użytkownika")
4. W hello **profilu użytkownika** sekcji, wykonaj następujące kroki hello:
   
    ![Profil użytkownika](./media/active-directory-saas-replicon-tutorial/IC777808.png "profilu użytkownika")
   
  1. W hello **nazwa logowania** pole tekstowe, typ hello Azure AD adres e-mail użytkownika hello Azure AD ma tooprovision.
  2. Jako **typ uwierzytelniania**, wybierz pozycję **logowania jednokrotnego**.
  3. W hello **działu** tekstowym, wpisz dział hello użytkownika.
  4. Jako **typu pracownika**, wybierz pozycję **administratora**.
  5. Kliknij przycisk **Zapisz profil użytkownika**.

>[!NOTE]
>Możesz użyć innych Replicon użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Replicon tooprovision kont użytkowników usługi AAD.
> 
> 

## <a name="assign-users"></a>Przypisywanie użytkowników
tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.

**tooassign tooReplicon użytkowników, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure Utwórz konto testu.

2. Na powitania **Replicon** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.
   
    ![Przypisywanie użytkowników](./media/active-directory-saas-replicon-tutorial/IC777809.png "przypisywanie użytkowników")

3. Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.
   
    ![Tak](./media/active-directory-saas-replicon-tutorial/IC767830.png "tak")

Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

