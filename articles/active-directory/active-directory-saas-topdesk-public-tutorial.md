---
title: 'Samouczek: Integracji Azure Active Directory z TOPdesk - publicznego | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i TOPdesk - publicznego."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a>Samouczek: Integracji Azure Active Directory z TOPdesk - publicznego

Z tego samouczka, dowiesz się, jak toointegrate TOPdesk - publicznego w usłudze Azure Active Directory (Azure AD).

Integrowanie TOPdesk - publicznego z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD mającego dostęp tooTOPdesk - publicznego.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTOPdesk — publiczny (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z TOPdesk - publiczny, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- TOPdesk — publiczny jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie TOPdesk - publicznego z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-topdesk---public-from-hello-gallery"></a>Dodawanie TOPdesk - publicznego z galerii hello
Integracja hello tooconfigure TOPdesk - publicznych do usługi Azure AD, należy tooadd TOPdesk - publicznego z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd TOPdesk - publicznego z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W hello wyszukiwania wpisz **TOPdesk - publicznego**, wybierz pozycję **TOPdesk - publicznego** z panelu wyników kliknięcie **Dodaj** przycisk aplikacji hello tooadd.

    ![TOPdesk - publicznego hello listy wyników](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TOPdesk — publiczny w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD wymaga tooknow użytkownika odpowiednikiem hello w TOPdesk — publiczny jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w TOPdesk - publicznego musi toobe ustanowione.

W TOPdesk - publiczny, przypisz wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowanie usługi Azure AD rejestracji jednokrotnej z TOPdesk — publiczny, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Utwórz TOPdesk - użytkownika testowego publicznego](#create-a-topdesk---public-test-user)**  - toohave odpowiednikiem Simona Britta w TOPdesk - publicznego, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci TOPdesk - publicznych aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z TOPdesk - publiczny, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **TOPdesk - publicznego** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. Na powitania **TOPdesk - domeny publicznej i adres URL** sekcji, wykonaj następujące kroki hello:

    ![TOPdesk - domeny publicznej i adresów URL jednym informacje logowania jednokrotnego](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.topdesk.net`
    
    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.topdesk.net/tas/public/login/verify`

    c. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.topdesk.net/tas/public/login/saml`
     
    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania. Adres URL odpowiedzi jest explaned później w samouczku. Skontaktuj się z [TOPdesk - zespołem pomocy technicznej klienta publicznego](https://help.topdesk.com/saas/enterprise/user/) tooget tych wartości.  

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. Na powitania **TOPdesk - publicznej konfiguracji** kliknij **skonfigurować TOPdesk - publicznego** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![TOPdesk - publicznej konfiguracji](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. Zaloguj się na tooyour **TOPdesk - publicznego** witryny firmy jako administrator.

8. W hello **TOPdesk** menu, kliknij przycisk **ustawienia**.
   
    ![Ustawienia](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "ustawienia")

9. Kliknij przycisk **ustawienia logowania**.
   
    ![Ustawienia logowania](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "ustawienia logowania")

10. Rozwiń węzeł hello **ustawienia logowania** menu, a następnie kliknij przycisk **ogólne**.
   
    ![Ogólne](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "ogólne")

11. W hello **publicznego** sekcji hello **logowania SAML** konfiguracji sekcji, wykonaj następujące kroki hello:
   
    ![Ustawienia techniczne](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "ustawienia techniczne")
   
    a. Kliknij przycisk **Pobierz** toodownload hello pliku metadanych publicznego, a następnie zapisz go lokalnie na komputerze.
   
    b. Otwórz plik metadanych hello pobrana, a następnie zlokalizuj hello **AssertionConsumerService** węzła.

    ![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")
   
    c. Hello kopiowania **AssertionConsumerService** wartość, wklej tę wartość w hello **adres URL odpowiedzi** textbox w **TOPdesk - domeny publicznej i adres URL** sekcji.      
   
12. toocreate plik certyfikatu, należy wykonać hello następujące kroki:
    
    ![Certyfikat](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "certyfikatu")
    
    a. Otwórz hello pobrany plik metadanych z portalu Azure.
    
    b. Rozwiń węzeł hello **RoleDescriptor** węzła, który ma **xsi: type** z **przekazywani: ApplicationServiceType**.
    
    c. Skopiuj wartość hello hello **X509Certificate** węzła.
    
    d. Zapisz hello skopiowane **X509Certificate** wartość lokalnie na komputerze w pliku.

13. W hello **publicznego** kliknij **Dodaj**.
    
    ![Logowania SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "logowania SAML")

14. Na powitania **Asystenta konfiguracji SAML** okna dialogowego wykonaj hello następujące kroki:
    
    ![Asystent konfiguracji SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Asystenta konfiguracji SAML")
    
    a. tooupload metadanych pobranych plików z portalu Azure, w obszarze **metadanych Federacji**, kliknij przycisk **Przeglądaj**.

    b. tooupload pliku certyfikatu, w obszarze **certyfikatu (RSA)**, kliknij przycisk **Przeglądaj**.

    c. plik z logo hello tooupload uzyskano z zespołem pomocy technicznej TOPdesk hello, w obszarze **ikona Logo**, kliknij przycisk **Przeglądaj**.

    d. W hello **atrybutu nazwy użytkownika** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    e. W hello **Nazwa wyświetlana** tekstowym, wpisz nazwę dla danej konfiguracji.

    f. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-topdesk---public-test-user"></a>Utwórz TOPdesk - użytkownika testowego publiczny

W kolejności tooenable usługi Azure AD użytkownicy toolog do TOPdesk - publiczny, muszą mieć przydzielone do TOPdesk - publicznego.  
W przypadku hello TOPdesk - publiczny, inicjowanie obsługi to zadanie ręczne.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:
1. Zaloguj się na tooyour **TOPdesk - publicznego** witryny firmy jako administrator.

2. W menu hello na górze hello, kliknij przycisk **TOPdesk \> nowy \> pliki obsługi \> osoby**.
   
    ![Osoba](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "osoby")

3. W oknie dialogowym nowej osoby hello wykonaj następujące kroki hello:
   
    ![Nowej osoby](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "nowej osoby")
   
    a. Kliknij kartę Ogólne hello.

    b. W hello **nazwisko** tekstowym, wpisz nazwisko użytkownika hello, takich jak Simona
 
    c. Wybierz **lokacji** hello konta.
 
    d. Kliknij pozycję **Zapisz**.

> [!NOTE]
> Można użyć innych TOPdesk — narzędzia do tworzenia konta użytkownika publiczny lub interfejsów API dostarczonych przez TOPdesk - kont użytkowników tooprovision publicznej usługi Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTOPdesk - publicznego.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooTOPdesk Simona Britta - publiczny, wykonaj następujące kroki hello:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **TOPdesk - publicznego**.

    ![Witaj TOPdesk - publicznego łącze w listę aplikacji hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello TOPdesk - publicznego kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour TOPdesk - publicznych aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

