---
title: "Samouczek: Azure Active Directory integrację z cyklem życia SCC | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse SCC cyklu życia z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a>Samouczek: Azure Active Directory integrację z cyklem życia SCC
Celem Hello tego samouczka jest tooshow integracji hello Azure i SCC cyklu życia.  

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

* Ważnej subskrypcji platformy Azure
* Cykl życia SCC rejestracji jednokrotnej (SSO) włączone subskrypcji

Ten samouczek hello użytkowników usługi Azure AD przypisano tooSCC będzie cyklu życia stanie toosingle logowania do aplikacji hello w witrynie firmy SCC cyklu życia (usługa zainicjował dostawcy logowania) lub przy użyciu hello [wprowadzenie Panel dostępu toohello](active-directory-saas-access-panel-introduction.md).

Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:

1. Włączanie integracji aplikacji hello dla SCC cykl życia
2. Konfigurowanie rejestracji jednokrotnej (SSO)
3. Konfigurowanie Inicjowanie obsługi użytkowników
4. Przypisywanie użytkowników

![Scenariusz](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "scenariusza")

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a>Włącz integrację aplikacji hello dla SCC cykl życia
Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla SCC cyklu życia.

**Integracja aplikacji hello tooenable dla SCC cykl życia, wykonaj hello następujące kroki:**

1. W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.
   
    ![Usługi Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "usługi Active Directory")
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Aplikacje](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "aplikacji")
4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Dodaj aplikację](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Dodaj aplikację")
5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
    ![Dodawanie aplikacji z gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "dodać aplikację z gallerry")
6. W hello **pole wyszukiwania**, typ **cyklu życia SCC**.
   
    ![Galerii aplikacji](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "galerii aplikacji")
7. W okienku wyników hello, wybierz **cyklu życia SCC**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
    ![Cykl życia SCC](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC cykl życia")
   
## <a name="configure-single-sign-on"></a>Konfigurowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooSCC cyklu życia do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.

**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure na powitania **cyklu życia SCC** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello ** skonfigurować rejestrację jednokrotną ** okna dialogowego.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "skonfigurować logowanie jednokrotne")
2. Na powitania **jak ma toosign użytkowników na tooSCC cyklu życia** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "skonfigurować logowanie jednokrotne")
3. Na powitania **Konfigurowanie adresu URL aplikacji** strony w hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używany przez Twoje toosign użytkowników na tooyour SCC cyklem życia aplikacji przy użyciu następującego wzorca hello "*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*", a następnie kliknij przycisk **dalej**.
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "skonfigurować adres URL aplikacji")
4. Na powitania **skonfigurować logowanie jednokrotne w cyklu życia SCC** kliknij przycisk **pobierania metadanych**, a następnie zapisz plik metadanych lokalnie na komputerze.
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "skonfigurować logowanie jednokrotne")
5. Przesyła tego tooSCC pliku metadanych cyklu życia z pomocą techniczną.
   
   >[!NOTE]
   >Logowanie jednokrotne ma toobe włączane przez hello cyklu życia SCC zespołem pomocy technicznej.
   > 
   > 

6. Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "skonfigurować logowanie jednokrotne")
   
## <a name="configure-user-provisioning"></a>Skonfiguruj Inicjowanie obsługi użytkowników

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w cyklu życia SCC muszą mieć przydzielone do SCC cyklu życia. Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooSCC cyklu życia.

Gdy toolog prób przypisany użytkownik w cyklu życia SCC konta cyklu życia SCC jest tworzony automatycznie w razie potrzeby.

>[!NOTE]
>Możesz użyć innych cyklu życia SCC użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez SCC cyklu życia tooprovision kont użytkowników usługi AAD.
> 
> 

## <a name="assign-users"></a>Przypisywanie użytkowników
tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.

**tooassign użytkowników tooSCC cykl życia, wykonaj hello następujące kroki:**

1. W hello klasycznego portalu Azure Utwórz konto testu.
2. Na powitania ** cyklu życia SCC ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.
   
    ![Przypisywanie użytkowników](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "przypisywanie użytkowników")
3. Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.
   
    ![Tak](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "tak")

Jeśli chcesz tootest ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

