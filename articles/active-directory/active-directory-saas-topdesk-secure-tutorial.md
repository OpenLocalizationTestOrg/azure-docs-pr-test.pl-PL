---
title: 'Samouczek: Integracji Azure Active Directory z TOPdesk - bezpiecznego | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse TOPdesk - zabezpieczyć za pomocą usługi Azure Active Directory tooenable logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a>Samouczek: Integracji Azure Active Directory z TOPdesk - bezpieczne
Celem Hello tego samouczka jest tooshow integracji hello Azure i TOPdesk — zabezpieczenia.  
Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

* Ważnej subskrypcji platformy Azure
* A TOPdesk - bezpieczne logowanie jednokrotne włączone subskrypcji

Po ukończeniu tego samouczka, użytkownicy hello Azure AD przypisano tooTOPdesk - bezpiecznego będzie można stanie toosingle logowania do aplikacji hello w Twojej TOPdesk - firmy bezpiecznej witryny (usługi zainicjował dostawcy logowania) lub przy użyciu hello [wprowadzenie Panel dostępu toohello](active-directory-saas-access-panel-introduction.md).

Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:

1. Włączanie integracji aplikacji hello dla TOPdesk - bezpieczne
2. Konfigurowanie rejestracji jednokrotnej
3. Konfigurowanie Inicjowanie obsługi użytkowników
4. Przypisywanie użytkowników

![Scenariusz](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "scenariusza")

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a>Włączanie integracji aplikacji hello dla TOPdesk - bezpieczne
Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla TOPdesk - bezpieczny.

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a>Integracja aplikacji hello tooenable dla TOPdesk - bezpieczny, wykonaj hello następujące kroki:
1. W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.
   
    ![Usługi Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "usługi Active Directory")

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Aplikacje](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "aplikacji")

4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Dodaj aplikację](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Dodaj aplikację")

5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
    ![Dodawanie aplikacji z gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "dodać aplikację z gallerry")

6. W hello **pole wyszukiwania**, typ **TOPdesk - bezpiecznego**.
   
    ![Galerii aplikacji](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "galerii aplikacji")

7. Wybierz w okienku wyników hello **TOPdesk - bezpiecznego**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
    ![TOPdesk - bezpiecznego](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - bezpieczne")

## <a name="configuring-single-sign-on"></a>Konfigurowanie rejestracji jednokrotnej
Celem Hello w tej sekcji jest toooutline jak tooTOPdesk tooauthenticate użytkowników tooenable - zabezpieczyć za pomocą swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.  
Konfigurowanie rejestracji jednokrotnej dla TOPdesk - bezpiecznego wymaga tooupload pliku ikony logo. Plik ikony hello tooget, skontaktuj się z pomocą hello TOPdesk z pomocą techniczną.

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a>tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:
1. Zaloguj się na tooyour **TOPdesk - bezpiecznego** witryny firmy jako administrator.
2. W hello **TOPdesk** menu, kliknij przycisk **ustawienia**.
   
    ![Ustawienia](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "ustawienia")

3. Kliknij przycisk **ustawienia logowania**.
   
    ![Ustawienia logowania](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "ustawienia logowania")

4. Rozwiń węzeł hello **ustawienia logowania** menu, a następnie kliknij przycisk **ogólne**.
   
    ![Ogólne](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "ogólne")

5. W hello **bezpiecznego** sekcji hello **logowania SAML** konfiguracji sekcji, wykonaj następujące kroki hello:
   
    ![Ustawienia techniczne](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "ustawienia techniczne")
   
    a. Kliknij przycisk **Pobierz** toodownload hello pliku metadanych publicznego, a następnie zapisz go lokalnie na komputerze.
   
    b. Otwórz plik metadanych hello, a następnie zlokalizuj hello **AssertionConsumerService** węzła.
    
    ![Usługa konsumenta potwierdzenia](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "potwierdzenia klienta usługi")
   
    c. Kopiuj hello **AssertionConsumerService** wartości.  
      
    > [!NOTE]
    > Będzie konieczne hello wartość hello **Konfigurowanie adresu URL aplikacji** dalszej części tego samouczka.
    > 
    > 

6. W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **klasycznego portalu Azure** jako administrator.

7. Na powitania **TOPdesk - bezpiecznego** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello ** skonfigurować rejestrację jednokrotną ** okna dialogowego.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "skonfigurować logowanie jednokrotne")

8. Na powitania **jak czy jak toosign użytkowników na tooTOPdesk - Secure** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "skonfigurować logowanie jednokrotne")

9. Na powitania **Konfigurowanie adresu URL aplikacji** wykonaj hello następujące kroki:
   
    ![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "skonfigurować adres URL aplikacji")
   
    a. W hello **TOPdesk - bezpiecznego logowania na adres URL** pole tekstowe, wprowadź adres URL hello używany przez Twoje toosign użytkowników do Twojej TOPdesk - zabezpieczonej aplikacji (np.: "*https://qssolutions.topdesk.net*").
   
    b. W hello **TOPdesk — publiczny adres URL odpowiedzi** pole tekstowe, Wklej hello **TOPdesk - bezpiecznego adresu URL AssertionConsumerService** (np.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")
   
    c. Kliknij przycisk **Dalej**.

10. Na powitania **skonfigurować logowanie jednokrotne w TOPdesk - bezpiecznego** strony, toodownload pliku metadanych, kliknij przycisk **pobierania metadanych**, a następnie zapisz plik hello lokalnie na komputerze.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "skonfigurować logowanie jednokrotne")

11. toocreate plik certyfikatu, należy wykonać hello następujące kroki:
    
    ![Certyfikat](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "certyfikatu")
    
    a. Plik metadanych pobranych hello otwarte.
    b. Rozwiń węzeł hello **RoleDescriptor** węzła, który ma **xsi: type** z **przekazywani: ApplicationServiceType**.
    c. Skopiuj wartość hello hello **X509Certificate** węzła.
    d. Zapisz hello skopiowane **X509Certificate** wartość lokalnie na komputerze w pliku.

12. W Twojej TOPdesk - zabezpieczenie witryny firmy, w hello **TOPdesk** menu, kliknij przycisk **ustawienia**.
    
    ![Ustawienia](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "ustawienia")

13. Kliknij przycisk **ustawienia logowania**.
    
    ![Ustawienia logowania](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "ustawienia logowania")

14. Rozwiń węzeł hello **ustawienia logowania** menu, a następnie kliknij przycisk **ogólne**.
    
    ![Ogólne](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "ogólne")

15. W hello **publicznego** kliknij **Dodaj**.
    
    ![Dodaj](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Dodaj")

16. Na powitania **Asystenta konfiguracji SAML** okna dialogowego wykonaj hello następujące kroki:
    
    ![Asystent konfiguracji SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Asystenta konfiguracji SAML")
    
    a. tooupload metadanych pobranych plików, w obszarze **metadanych Federacji**, kliknij przycisk **Przeglądaj**.

    b. tooupload pliku certyfikatu, w obszarze **certyfikatu (RSA)**, kliknij przycisk **Przeglądaj**.

    c. plik z logo hello tooupload uzyskano z zespołem pomocy technicznej TOPdesk hello, w obszarze **ikona Logo**, kliknij przycisk **Przeglądaj**.

    d. W hello **atrybutu nazwy użytkownika** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    e. W hello **Nazwa wyświetlana** tekstowym, wpisz nazwę dla danej konfiguracji.

    f. Kliknij pozycję **Zapisz**.

17. Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "skonfigurować logowanie jednokrotne")

## <a name="configuring-user-provisioning"></a>Konfigurowanie Inicjowanie obsługi użytkowników
W kolejności tooenable usługi Azure AD użytkownicy toolog do TOPdesk - bezpieczny, ich muszą mieć przydzielone do TOPdesk - bezpieczny.  
W przypadku hello TOPdesk - bezpieczny, inicjowanie obsługi to zadanie ręczne.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:
1. Zaloguj się na tooyour **TOPdesk - bezpiecznego** witryny firmy jako administrator.
2. W menu hello na górze hello, kliknij przycisk **TOPdesk \> nowy \> pliki obsługi \> Operator**.
   
    ![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "— Operator")

3. Na powitania **operatora New** okna dialogowego, wykonaj następujące kroki hello:
   
    ![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New — Operator")
   
    a. Kliknij kartę Ogólne hello.
   
    b. W hello **nazwisko** textbox hello **ogólne** typu hello nazwisko prawidłowe konto usługi Azure Active Directory ma tooprovision, sekcji.
   
    c. Wybierz **lokacji** konta hello w hello **lokalizacji** sekcji.
   
    d. W hello **nazwa logowania** textbox hello **logowania TOPdesk** wpisz nazwę logowania dla użytkownika.
   
    e. Kliknij pozycję **Zapisz**.

> [!NOTE]
> Można użyć dowolnego innych TOPdesk - bezpieczne konta narzędzia do tworzenia lub interfejsów API dostarczonych przez TOPdesk - Secure tooprovision kont użytkowników usługi AAD.
> 
> 

## <a name="assigning-users"></a>Przypisywanie użytkowników
tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a>tooTOPdesk użytkowników tooassign - bezpieczny, wykonaj następujące kroki hello:
1. W hello klasycznego portalu Azure Utwórz konto testu.
2. Na powitania ** TOPdesk - bezpiecznego ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.
   
    ![Przypisywanie użytkowników](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "przypisywanie użytkowników")

3. Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.
   
    ![Tak](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "tak")

Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

