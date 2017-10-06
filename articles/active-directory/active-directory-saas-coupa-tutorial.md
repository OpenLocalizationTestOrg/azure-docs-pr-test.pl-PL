---
title: 'Samouczek: Integracji Azure Active Directory z Coupa | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse Coupa z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>Samouczek: Integracji Azure Active Directory z Coupa
Celem Hello tego samouczka jest tooshow integracji hello Azure i Coupa.  
Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

* Ważnej subskrypcji platformy Azure
* Coupa rejestracji jednokrotnej (SSO) włączone subskrypcji

Ten samouczek użytkownicy hello Azure AD przypisano tooCoupa będą mogli toosingle logowanie do aplikacji hello przy użyciu hello [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:

* Włączanie integracji aplikacji hello dla Coupa
* Konfigurowanie rejestracji jednokrotnej
* Konfigurowanie Inicjowanie obsługi użytkowników
* Przypisywanie użytkowników

![Scenariusz](./media/active-directory-saas-coupa-tutorial/IC791897.png "scenariusza")

## <a name="enable-hello-application-integration-for-coupa"></a>Włącz integrację aplikacji hello dla Coupa
Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla Coupa.

**integracji aplikacji hello tooenable dla Coupa, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.
   
   ![Usługi Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "usługi Active Directory")
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
   ![Aplikacje](./media/active-directory-saas-coupa-tutorial/IC700994.png "aplikacji")
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
   ![Dodaj aplikację](./media/active-directory-saas-coupa-tutorial/IC749321.png "Dodaj aplikację")
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
   ![Dodawanie aplikacji z gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "dodać aplikację z gallerry")
6. W hello **pole wyszukiwania**, typ **Coupa**.
   
   ![Galerii aplikacji](./media/active-directory-saas-coupa-tutorial/IC791898.png "galerii aplikacji")
7. Wybierz w okienku wyników hello **Coupa**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
   ![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")
   
## <a name="configure-single-sign-on"></a>Konfigurowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooCoupa do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.  

Konfigurowanie rejestracji jednokrotnej dla Coupa wymaga tooretrieve wartość odcisku palca certyfikatu. Jeśli nie masz doświadczenia z tej procedury, zobacz [jak tooretrieve wartość odcisku palca certyfikatu](http://youtu.be/YKQF266SAxI).

**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**

1. Rejestracja tooyour Coupa witryny firmy jako administrator.
2. Przejdź za**Instalator \> zabezpieczeniem**.
   
   ![Opcje zabezpieczeń](./media/active-directory-saas-coupa-tutorial/IC791900.png "środki zabezpieczające.")
3. toodownload hello Coupa metadanych pliku tooyour komputera, kliknij przycisk **pobierać i importować metadane SP**.
   
   ![Metadane Coupa SP](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadanych")
4. W oknie innej przeglądarki Zaloguj się na toohello klasycznego portalu Azure.
5. Na powitania **Coupa** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-coupa-tutorial/IC791902.png "skonfigurować logowanie jednokrotne")
6. Na powitania **jak ma toosign użytkowników na tooCoupa** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-coupa-tutorial/IC791903.png "skonfigurować logowanie jednokrotne")
7. Na powitania **Konfigurowanie adresu URL aplikacji** wykonaj hello następujące kroki:
   
   ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-coupa-tutorial/IC791904.png "skonfigurować adres URL aplikacji")   
   1. W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL używany przez Twoje toosign użytkowników na tooyour Coupa aplikacji (np.: "*http://company.Coupa.com*").
   2. Otwórz pobrany plik metadanych Coupa, a następnie skopiuj hello **AssertionConsumerService indeksu lub adres URL**.
   3. W hello **adres URL odpowiedzi Coupa** pole tekstowe, Wklej hello **AssertionConsumerService indeksu lub adres URL** wartość.
   4. Kliknij przycisk **Dalej**.
8. Na powitania **skonfigurować logowanie jednokrotne w Coupa** strony, toodownload pliku metadanych, kliknij przycisk **pobierania metadanych**, a następnie zapisz plik hello lokalnie na komputerze.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-coupa-tutorial/IC791905.png "skonfigurować logowanie jednokrotne")
9. W witrynie firmy Coupa hello Przejdź zbyt**Instalator \> zabezpieczeniem**.
   
   ![Opcje zabezpieczeń](./media/active-directory-saas-coupa-tutorial/IC791900.png "środki zabezpieczające.")
10. W hello **Zaloguj się za pomocą poświadczeń Coupa** sekcji, wykonaj następujące kroki hello:  

   ![Zaloguj się za pomocą poświadczeń Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Zaloguj się za pomocą poświadczeń Coupa") 
   1. Wybierz **zalogowanie się przy użyciu SAML**.
   2. Kliknij przycisk **Przeglądaj** tooupload usługi Azure Active pobranego pliku metadanych.
   3. Kliknij pozycję **Zapisz**.
11. Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
    
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-coupa-tutorial/IC791907.png "skonfigurować logowanie jednokrotne")
    
## <a name="configure-user-provisioning"></a>Skonfiguruj Inicjowanie obsługi użytkowników

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Coupa muszą mieć przydzielone do Coupa.  

* W przypadku hello Coupa Inicjowanie obsługi to zadanie ręczne.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. Zaloguj się za tooyour **Coupa** witryny firmy jako administrator.
2. Hello menu u góry hello, kliknij przycisk **Instalator**, a następnie kliknij przycisk **użytkowników**.
   
   ![Użytkownicy](./media/active-directory-saas-coupa-tutorial/IC791908.png "użytkowników")
3. Kliknij przycisk **Utwórz**.
   
   ![Tworzenie użytkowników](./media/active-directory-saas-coupa-tutorial/IC791909.png "tworzenie użytkowników")
4. W hello **Utwórz użytkownika** sekcji, wykonaj następujące kroki hello:
   
   ![Szczegóły użytkownika](./media/active-directory-saas-coupa-tutorial/IC791910.png "szczegóły użytkownika")
   
   1. Typ hello **logowania**, **imię**, **nazwisko**, **identyfikator rejestracji jednokrotnej**, **E-mail** atrybutów prawidłowe konto usługi Azure Active Directory, które chcesz tooprovision do hello powiązanych pól tekstowych.
   2. Kliknij przycisk **Utwórz**.   
   >[!NOTE]
   >Właściciel konta usługi Azure Active Directory Hello otrzyma wiadomość e-mail z kontem hello tooconfirm łącze zanim staje się aktywny. 
   > 

>[!NOTE]
>Możesz użyć innych Coupa użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Coupa tooprovision kont użytkowników usługi AAD. 
> 

## <a name="assign-users"></a>Przypisywanie użytkowników
tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.

**tooassign tooCoupa użytkowników, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure Utwórz konto testu.
2. Na powitania ** Coupa ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.
   
   ![Przypisywanie użytkowników](./media/active-directory-saas-coupa-tutorial/IC791911.png "przypisywanie użytkowników")
3. Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.
   
   ![Tak](./media/active-directory-saas-coupa-tutorial/IC767830.png "tak")

Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

