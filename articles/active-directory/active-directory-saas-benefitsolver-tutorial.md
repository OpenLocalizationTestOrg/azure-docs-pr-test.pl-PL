---
title: 'Samouczek: Integracji Azure Active Directory z Benefitsolver | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse Benefitsolver z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>Samouczek: Integracji Azure Active Directory z Benefitsolver
Celem Hello tego samouczka jest tooshow integracji hello Azure i Benefitsolver.  

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

* Ważnej subskrypcji platformy Azure
* Benefitsolver rejestracji jednokrotnej (SSO) włączone subskrypcji

Ten samouczek użytkownicy hello Azure AD przypisano tooBenefitsolver będą mogli toosingle logowanie do aplikacji hello przy użyciu hello [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:

1. Włączanie integracji aplikacji hello dla Benefitsolver
2. Konfigurowanie rejestracji jednokrotnej (SSO)
3. Konfigurowanie Inicjowanie obsługi użytkowników
4. Przypisywanie użytkowników

![Scenariusz](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "scenariusza")

## <a name="enabling-hello-application-integration-for-benefitsolver"></a>Włączanie integracji aplikacji hello dla Benefitsolver
Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla Benefitsolver.

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a>integracji aplikacji hello tooenable dla Benefitsolver, wykonaj następujące kroki hello:
1. W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.
   
   ![Usługi Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "usługi Active Directory")
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
   ![Aplikacje](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "aplikacji")
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
   ![Dodaj aplikację](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Dodaj aplikację")
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
   ![Dodawanie aplikacji z gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "dodać aplikację z gallerry")
6. W hello **pole wyszukiwania**, typ **Benefitsolver**.
   
   ![Galerii aplikacji](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "galerii aplikacji")
7. Wybierz w okienku wyników hello **Benefitsolver**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>Konfigurowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooBenefitsolver do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.  

Aplikacja Benefitsolver oczekuje potwierdzenia SAML hello w określonym formacie wymaga tooyour mapowań atrybutów niestandardowych tooadd **atrybuty tokenu saml** konfiguracji. 

powitania po zrzut ekranu przedstawia przykład tego.

![Atrybuty](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "atrybutów")

**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure na powitania **Benefitsolver** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okno dialogowe.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "skonfigurować logowanie jednokrotne")
2. Na powitania **jak ma toosign użytkowników na tooBenefitsolver** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "skonfigurować logowanie jednokrotne")
3. Na powitania **Konfigurowanie ustawień aplikacji** wykonaj hello następujące kroki:
   
   ![Konfiguruj ustawienia aplikacji](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Konfiguruj ustawienia aplikacji")
   
   1. W hello **na adres URL logowania** pole tekstowe, typ **http://azure.benefitsolver.com**.
   2. W hello **adres URL odpowiedzi** pole tekstowe, typ **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.  
   3. Kliknij przycisk **Dalej**.
4. Na powitania **skonfigurować logowanie jednokrotne w Benefitsolver** strony, toodownload metadanych programu kliknij **pobierania metadanych**, a następnie zapisz plik metadanych hello lokalnie na komputerze.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "skonfigurować logowanie jednokrotne")
5. Wyślij hello pobrać metadanych pliku tooyour Benefitsolver z pomocą techniczną.
   
   >[!NOTE]
   >Z zespołem pomocy technicznej Benefitsolver ma toodo hello rzeczywista konfiguracja logowania jednokrotnego. Otrzymasz powiadomienie podczas logowania jednokrotnego została włączona dla Twojej subskrypcji.
   >

6. Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "skonfigurować logowanie jednokrotne")
7. W menu hello na górze hello, kliknij przycisk **atrybuty** tooopen hello **atrybuty tokenu SAML** okna dialogowego.
   
   ![Atrybuty](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "atrybutów")
8. Mapowanie atrybutów hello wymagane tooadd, wykonaj hello następujące kroki:
   
   ![Atrybuty](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "atrybutów")
   
   | Nazwa atrybutu | Wartość atrybutu |
   | --- | --- |
   | ClientID |Należy tooget tej wartości z zespołem pomocy technicznej Benefitsolver. |
   | ClientKey |Należy tooget tej wartości z zespołem pomocy technicznej Benefitsolver. |
   | LogoutURL |Należy tooget tej wartości z zespołem pomocy technicznej Benefitsolver. |
   | Identyfikator pracownika |Należy tooget tej wartości z zespołem pomocy technicznej Benefitsolver. |
   
   1. Dla każdego wiersza danych w powyższej tabeli powitania kliknij **Dodaj atrybut użytkownika**.
   2. W hello **nazwa atrybutu** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.
   3. W hello **wartość atrybutu** pole tekstowe, wartość atrybutu hello wybierz wyświetlanego dla tego wiersza.
   4. Kliknij przycisk **Complete** (Zakończ).
9. Kliknij przycisk **Zastosuj zmiany**.

## <a name="configure-user-provisioning"></a>Skonfiguruj Inicjowanie obsługi użytkowników
W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Benefitsolver muszą mieć przydzielone do Benefitsolver.  

W przypadku hello Benefitsolver pracownika danych jest w aplikacji wypełniać za pomocą pliku spisu z systemu HRIS (zazwyczaj co noc).  

>[!NOTE]
>Możesz użyć innych Benefitsolver użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Benefitsolver tooprovision kont użytkowników usługi AAD. 
> 

## <a name="assigning-users"></a>Przypisywanie użytkowników
tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a>tooassign tooBenefitsolver użytkowników, wykonaj następujące kroki hello:
1. W hello klasycznego portalu Azure Utwórz konto testu.
2. Na powitania ** Benefitsolver ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.
   
   ![Przypisywanie użytkowników](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "przypisywanie użytkowników")
3. Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.
   
   ![Tak](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "tak")

Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

