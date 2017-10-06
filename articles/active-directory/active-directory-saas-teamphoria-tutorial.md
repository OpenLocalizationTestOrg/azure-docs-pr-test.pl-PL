---
title: 'Samouczek: Integracji Azure Active Directory z Teamphoria | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a>Samouczek: Integracji Azure Active Directory z Teamphoria

Z tego samouczka, dowiesz się, jak toointegrate Teamphoria w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Teamphoria zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTeamphoria
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTeamphoria (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Teamphoria należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Teamphoria jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Teamphoria z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-teamphoria-from-hello-gallery"></a>Dodawanie Teamphoria z galerii hello
tooconfigure hello integracji Teamphoria do usługi Azure AD, należy tooadd Teamphoria z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Teamphoria z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Teamphoria**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. W panelu wyników hello zaznacz **Teamphoria**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Teamphoria w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Teamphoria jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Teamphoria musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Teamphoria.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Teamphoria, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Teamphoria](#creating-a-teamphoria-test-user)**  -toohave odpowiednikiem Simona Britta w Teamphoria, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji Teamphoria.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Teamphoria, wykonaj następujące kroki hello:**

1. W portalu zarządzania Azure hello na powitania **Teamphoria** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. Na powitania **Teamphoria domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    a. W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello przy użyciu hello następującego wzorca:`https://<sub-domain>.teamphoria.com/login`  

    > [!NOTE] 
    > Należy pamiętać, że nie są one hello wartości rzeczywistych. Masz tooupdate tych wartości za pomocą hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta Teamphoria](https://www.teamphoria.com/) tooget URL hello logowania jednokrotnego. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie Zapisz certyfikat hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Teamphoria** kliknij **skonfigurować Teamphoria** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. tooconfigure rejestracji jednokrotnej w **Teamphoria** strona, logowania tooyour Teamphoria aplikacji jako administrator.

8. Przejdź za**ustawienia administratora** opcji hello lewym pasku narzędzi i w obszarze hello powitania kliknij kartę skonfigurować **POJEDYNCZEGO logowania** tooopen hello logowania jednokrotnego konfiguracji okna.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. Polecenie **Dodaj nowego DOSTAWCĘ tożsamości** opcję hello prawym górnym rogu tooopen hello formularz służący do dodawania hello ustawienia logowania jednokrotnego.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. Wprowadź szczegóły hello w polach hello zgodnie z opisem poniżej-

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    a. **Nazwa WYŚWIETLANA** : Wprowadź nazwę wyświetlaną hello wtyczki hello na powitania strony administratora.

    b. **Nazwa przycisku** : Nazwa hello hello kartę, która będzie wyświetlana na powitania strony logowania dla logowania za pośrednictwem rejestracji Jednokrotnej.

    c. **CERTYFIKAT** : Otwórz hello certyfikatu pobrane wcześniej z portalu Azure w programie Notatnik kopiowania zawartości hello hello hello takie same i wklej go w tym miejscu w polu hello.

    d. **PUNKT wejścia** : hello Wklej **SAML pojedynczy znak na adres URL usługi** skopiowane wcześniej hello formularza portalu Azure.

    e. Przełącz opcję hello zbyt**ON** i wybierz polecenie **ZAPISAĆ**. 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-teamphoria-test-user"></a>Tworzenie użytkownika testowego Teamphoria

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Teamphoria muszą mieć przydzielone do Teamphoria. W przypadku hello Teamphoria Inicjowanie obsługi to zadanie ręczne.

**tooprovision kont użytkowników, wykonaj hello następujące kroki:**

1. Zaloguj się za tooyour Teamphoria witryny firmy jako administrator.

2. Polecenie **ADMIN** ustawień na powitania po lewej stronie narzędzi i w obszarze hello **ZARZĄDZAJ** karcie kliknij na **użytkowników** strony administratora hello tooopen dla użytkowników.

    ![Dodawanie pracownika](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. Polecenie hello **ZAPROSIĆ RĘCZNEGO** opcji.

    ![Zaproś inne osoby](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. Na tej stronie należy wykonać następujące działania. 
    
    ![Zaproś inne osoby](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    a. W hello **adres E-mail** pole tekstowe, hello **adres e-mail** z BrittaSimon.

    b. W hello **imię** pole tekstowe, typ **Britta**.

    c. W hello **nazwisko** pole tekstowe, typ **Simona**.

    d. Kliknij przycisk **użytkownika zaproszenia 1**. Użytkownik musi tooget zaproszenia hello tooaccept w systemie hello utworzona.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooTeamphoria dostępu.

![Przypisz użytkownika][200] 

**tooassign tooTeamphoria Simona Britta wykonaj hello następujące kroki:**

1. W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Teamphoria**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

