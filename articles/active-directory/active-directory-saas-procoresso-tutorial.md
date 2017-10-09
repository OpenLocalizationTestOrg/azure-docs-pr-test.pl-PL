---
title: "Samouczek: Integracji usługi Azure Active Directory z logowania jednokrotnego Procore | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Procore logowania jednokrotnego."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a>Samouczek: Integracji Azure Active Directory z Procore logowania jednokrotnego

Z tego samouczka, dowiesz się, jak toointegrate Procore logowania jednokrotnego w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Procore logowania jednokrotnego zawiera hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooProcore logowania jednokrotnego
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooProcore SSO (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z Procore logowania jednokrotnego należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Procore logowania jednokrotnego jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Procore rejestracji Jednokrotnej z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-procore-sso-from-hello-gallery"></a>Dodawanie Procore rejestracji Jednokrotnej z galerii hello
tooconfigure hello integracji Procore logowania jednokrotnego do usługi Azure AD, należy tooadd Procore rejestracji Jednokrotnej z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Procore rejestracji Jednokrotnej z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Procore logowania jednokrotnego**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. W panelu wyników hello, wybierz **Procore logowania jednokrotnego**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej Procore logowaniem jednokrotnym w oparciu o użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Procore rejestracji Jednokrotnej jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Procore logowania jednokrotnego musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Procore logowania jednokrotnego.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Procore logowania jednokrotnego, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Procore logowania jednokrotnego](#creating-a-procore-sso-test-user)**  -toohave odpowiednikiem Simona Britta w Procore logowania jednokrotnego, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji Procore logowania jednokrotnego.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Procore logowanie Jednokrotne, należy wykonać hello następujące kroki:**

1. W portalu zarządzania Azure hello na powitania **Procore logowania jednokrotnego** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. Na powitania **Procore domena logowania jednokrotnego i adresy URL** sekcji, hello użytkownik nie ma tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. Na powitania **Procore konfiguracji logowania jednokrotnego** kliknij **Konfigurowanie logowania jednokrotnego Procore** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. tooconfigure rejestracji jednokrotnej w **Procore logowania jednokrotnego** strona, witryny firmy procore tooyour logowania jako administrator.

8. Z listy przybornika hello w dół, kliknij pozycję **Admin** tooopen hello logowania jednokrotnego ustawienia strony.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. Wklej hello wartości w polach hello opisane poniżej-

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    a. W hello **pojedynczy znak na adres URL wystawcy** Wklej hello identyfikator jednostki SAML skopiowanych z hello portalu Azure.

    b. W hello **SAML logowania na docelowy adres URL** Wklej hello SAML pojedynczy znak na adres URL usługi skopiowanych z hello portalu Azure.

    c. Teraz Otwórz hello **XML metadanych** pobranego wcześniej z hello portalu Azure i certyfikat hello kopiowania w tagu hello o nazwie **X509Certificate**. Witaj Wklej skopiowane wartości do hello **certyfikatu rejestracji jednokrotnej x509** pole.

10. Polecenie **zapisać zmiany**.

11. Po tych ustawień wymaga toosend hello **nazwy domeny** (np. **contoso.com**) za pomocą którego logujesz się do Procore toohello [zespołem pomocy technicznej Procore](https://support.procore.com/) i zostaną one Aktywacja z federacyjną rejestracją Jednokrotną dla tej domeny.

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-procore-sso-test-user"></a>Tworzenie użytkownika testowego Procore logowania jednokrotnego

Wykonaj hello poniżej toocreate czynności użytkownika testowego Procore w bok.

1. Logowania z witryny firmy procore tooyour jako administrator.  

2. Z listy przybornika hello w dół, kliknij pozycję **katalogu** tooopen hello firmy katalogu strony.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. Polecenie **dodać osobę** opcję tooopen hello formularz i wprowadzić wykonaj następujące opcje —

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    a. W hello **imię** pole tekstowe, imię użytkownika typu, takich jak **Britta**.

    b. W hello **nazwisko** pole tekstowe, nazwisko użytkownika typu, takich jak **Simona**.

    c. W hello **adres E-mail** , adres e-mail użytkownika typu pole tekstowe, takich jak  **BrittaSimon@contoso.com** .

    d. Wybierz **szablon uprawnień** jako **później Zastosuj szablon uprawnień**.

    e. Kliknij przycisk **Utwórz**.

4. Sprawdź i zaktualizuj szczegóły hello, dla hello nowo dodany kontakt.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. Polecenie **zapisywanie i wysyłanie Invitiation** (Jeśli wymagane jest zaproszenia pocztą) lub **zapisać** (Zapisz bezpośrednio) toocomplete hello użytkownika rejestracji.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooProcore dostępu logowania jednokrotnego.

![Przypisz użytkownika][200] 

**tooassign tooProcore Simona Britta logowanie Jednokrotne, należy wykonać hello następujące kroki:**

1. W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Procore logowania jednokrotnego**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586). Po kliknięciu kafelka Procore logowania jednokrotnego hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Procore logowania jednokrotnego aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

