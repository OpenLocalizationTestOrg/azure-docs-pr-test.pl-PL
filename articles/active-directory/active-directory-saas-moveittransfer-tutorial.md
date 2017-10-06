---
title: "Samouczek: Integracji Azure Active Directory z MOVEit Transfer — integracji z usługą Azure AD | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i MOVEit Transfer — integracji z usługą Azure AD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a>Samouczek: Integracji Azure Active Directory z MOVEit Transfer — integracji z usługą Azure AD

Z tego samouczka, dowiesz się, jak toointegrate MOVEit Transfer — integracji z usługą Azure AD z usługą Azure Active Directory (Azure AD).

Integrowanie MOVEit Transfer — integracji z usługą Azure AD z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMOVEit Transfer — integracji z usługą Azure AD.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMOVEit Transfer — Integracja usługi Azure AD (logowanie jednokrotne) z konta usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z MOVEit Transfer — integracji z usługą Azure AD, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- MOVEit Transfer — usługi Azure AD integracji jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie MOVEit Transfer — integracji z usługą Azure AD z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a>Dodawanie MOVEit Transfer — integracji z usługą Azure AD z galerii hello
Integracja hello tooconfigure transferu MOVEit - integracji usługi Azure AD do usługi Azure AD, należy tooadd MOVEit Transfer — integracji usługi Azure AD z listy tooyour galerii hello zarządzanych aplikacji SaaS.

**tooadd MOVEit Transfer — integracji z usługą Azure AD z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **MOVEit Transfer — integracji z usługą Azure AD**, wybierz pozycję **MOVEit Transfer — integracji z usługą Azure AD** z panelu wyników następnie kliknij przycisk **Dodaj** hello tooadd przycisk aplikacja.

    ![MOVEit Transfer — integracji usługi Azure AD hello listy wyników](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z MOVEit Transfer — integracji z usługą Azure AD w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD wymaga tooknow użytkownika odpowiednikiem hello transferu MOVEit — integracji z usługą Azure AD jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w MOVEit Transfer — integracji z usługą Azure AD musi toobe ustanowione.

W MOVEit Transfer — integracji z usługą Azure AD, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z MOVEit Transfer — integracji z usługą Azure AD, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie przeniesienia MOVEit - użytkownika testowego integracji usługi Azure AD](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - toohave odpowiednikiem Simona Britta transferu MOVEit - integracji usługi Azure AD z toohello połączonej usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w transferu MOVEit - aplikacji integracji usługi Azure AD.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z MOVEit Transfer — integracji z usługą Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **MOVEit Transfer — integracji z usługą Azure AD** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. Na powitania **MOVEit Transfer — adresy URL i integracji z usługą Azure AD domeny** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://contoso.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://contoso.com/<tenatid>`

    c. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`    
     
    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania. Może się odwoływać te wartości później w **adres URL metadanych dostawcy usługi** sekcji lub skontaktuj się z [MOVEit Transfer — zespołem pomocy technicznej klienta integracji usługi Azure AD](https://community.ipswitch.com/s/support) tooget tych wartości.

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. Zaloguj się na tooyour MOVEit Transfer dzierżawy z uprawnieniami administratora.

7. W okienku nawigacji po lewej stronie powitania kliknij **ustawienia**.

    ![Strona aplikacji w sekcji Ustawienia](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. Kliknij przycisk **pojedynczego logować** łącza, która znajduje się w **zasad zabezpieczeń -> uwierzytelniania użytkowników**.

    ![Strony aplikacji na zasady zabezpieczeń](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. Kliknij przycisk hello adres URL metadanych łącze toodownload hello metadanych dokumentu.

    ![Adres URL metadanych dostawcy usługi](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * Sprawdź **entityID** odpowiada **identyfikator** w hello **MOVEit Transfer — integracji z usługą Azure AD domeny i adres URL** sekcji.
    * Sprawdź **AssertionConsumerService** odpowiada adresu URL lokalizacji **adres URL odpowiedzi** w hello **MOVEit Transfer — adresy URL i integracji z usługą Azure AD domeny** sekcji.
    
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. Kliknij przycisk **Dodawanie dostawcy tożsamości** przycisk tooadd nowego dostawcę tożsamości federacyjnych.

    ![Dodaj dostawcę tożsamości](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. Kliknij przycisk **Przeglądaj...**  tooselect hello pliku metadanych, który został pobrany z portalu Azure, a następnie kliknij przycisk **Dodawanie dostawcy tożsamości** tooupload hello pobrany plik.

    ![Dostawca tożsamości SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. Wybierz opcję "**tak**" jako **włączone** w hello **Edycja ustawień tożsamości federacyjnych dostawca...**  i kliknij przycisk **zapisać**.

    ![Ustawienia dostawcy tożsamości federacyjnych](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. W hello **Edycja ustawień tożsamości federacyjnych dostawca użytkownika** wykonaj hello następujące akcje:
    
    ![Edytuj ustawienia dostawcy tożsamości federacyjnych](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    a. Wybierz **SAML NameID** jako **nazwa logowania**.
    
    b. Wybierz **innych** jako **imię i nazwisko** w hello **nazwa atrybutu** pole tekstowe umieścić wartość hello: `http://schemas.microsoft.com/identity/claims/displayname`.
    
    c. Wybierz **innych** jako **E-mail** w hello **nazwa atrybutu** pole tekstowe umieścić wartość hello: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    d. Wybierz **tak** jako **automatyczne tworzenie konta logowaniu**.
    
    e. Kliknij przycisk **zapisać** przycisku.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a>Tworzenie przeniesienia MOVEit - użytkownika testowego integracji usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w MOVEit Transfer — integracji z usługą Azure AD. MOVEit Transfer — integracji z usługą Azure AD obsługę just in time, które zostało włączone. Nie ma elementu akcji można w tej sekcji. Nowy użytkownik został utworzony podczas próby tooaccess MOVEit Transfer — integracji usługi Azure AD, jeśli go jeszcze nie istnieje.

>[!NOTE]
>Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [MOVEit Transfer — zespołem pomocy technicznej klienta integracji usługi Azure AD](https://community.ipswitch.com/s/support).

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMOVEit Transfer — integracji z usługą Azure AD.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooMOVEit Simona Britta Transfer — integracji z usługą Azure AD, należy wykonać hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **MOVEit Transfer — integracji z usługą Azure AD**.

    ![Witaj MOVEit Transfer — integracji z usługą Azure AD łącza na liście aplikacji hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.

Po kliknięciu hello MOVEit Transfer — kafelka integracji usługi Azure AD w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour MOVEit Transfer — aplikacji integracji usługi Azure AD. 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

