---
title: "Samouczek: Integracji Azure Active Directory z chmurą Creative Adobe | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Adobe Creative chmury."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>Samouczek: Integracji Azure Active Directory z chmurą Creative Adobe

Z tego samouczka, dowiesz się, jak toointegrate Adobe Creative chmury w usłudze Azure Active Directory (Azure AD).

Integrowanie Adobe Creative chmurze z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooAdobe Creative chmury
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAdobe Creative chmury (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z chmurą Creative Adobe należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Adobe Creative chmury jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Adobe Creative chmury z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a>Dodawanie Adobe Creative chmury z galerii hello
tooconfigure hello integracji Adobe Creative chmury do usługi Azure AD, należy tooadd Adobe Creative chmury z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Adobe Creative chmury z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **chmury Creative Adobe**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. W panelu wyników hello, wybierz **chmury Creative Adobe**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Adobe Creative w chmurze na koncie użytkownika testu o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w chmurze Creative Adobe jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w chmurze Creative Adobe musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w chmurze Creative Adobe.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z chmurą Creative Adobe, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego chmury Creative Adobe](#creating-an-adobe-creative-cloud-test-user)**  -toohave odpowiednikiem Simona Britta w chmurze Creative Adobe, która jest jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne do aplikacji w chmurze Creative Adobe.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Adobe Creative chmury, wykonaj hello następujące kroki:**

1. W portalu zarządzania Azure hello na powitania **chmury Creative Adobe** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. Na powitania **adresy URL i Adobe Creative domenę chmury** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    a. W hello **identyfikator** pole tekstowe, wartość hello typu jako:`https://www.okta.com/saml2/service-provider/<token>`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > Należy pamiętać, że nie są one hello wartości rzeczywistych. Masz tooupdate tych wartości za pomocą hello rzeczywisty identyfikator i odpowiedzi adresu URL. W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator. Należy ręcznie toocreate użytkownika, należy najpierw toocontact hello Adobe Creative chmury z pomocą techniczną.

4. Na powitania **adresy URL i Adobe Creative domenę chmury** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    a. Polecenie hello **Pokaż zaawansowane ustawienia adresu URL** opcji

    b. W hello **adres URL logowania** pole tekstowe, wartość hello typu jako:`https://adobe.com`

5. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. Na powitania **Adobe Creative konfiguracji chmury** kliknij **Konfigurowanie chmury Creative Adobe** tooopen **Konfigurowanie logowania jednokrotnego** okna. Skopiuj hello **identyfikator jednostki SAML** i **adres URL usługi logowania jednokrotnego SAML** z krótkimi opisami sekcji.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. W oknie przeglądarki innej witryny sieci web, tooyour logowania w chmurze Creative Adobe dzierżawy jako administrator.

8.  Przejdź za**tożsamości** hello okienka nawigacji po lewej stronie i kliknij domenę. Następnie wykonaj następujące kroki powitania **pojedynczy znak na wymagana konfiguracja** sekcji.

    ![Ustawienia](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "ustawienia")

9. Kliknij przycisk **Przeglądaj** tooupload hello pobrać certyfikatu z usługi Azure AD za**certyfikatu IDP**.

10. W hello **wystawcy IDP** pole tekstowe, umieść wartość hello **identyfikator jednostki SAML** którego skopiowany z **Konfigurowanie logowania jednokrotnego** sekcji w portalu Azure.

11. W hello **adres URL logowania IDP** pole tekstowe, umieść wartość hello **adres URL usługi logowania jednokrotnego SAML** , które zostały skopiowane z **Konfigurowanie logowania jednokrotnego** sekcji w portalu Azure.

12. Wybierz **HTTP - przekierowania** jako **powiązania IDP**.

13. Wybierz **adres E-mail** jako **ustawienia logowania użytkownika**.
 
14. Kliknij przycisk **zapisać** przycisku.

15. pulpit nawigacyjny Hello teraz przedstawi hello XML **"Pobieranie metadanych"** pliku. Zawiera adres URL EntityDescriptor Adobe i AssertionConsumerService adresu URL. Otwórz plik hello i skonfigurować je w hello aplikacji usługi Azure AD.

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    a. Użyj hello wartość EntityDescriptor Adobe dostarczył dla **identyfikator** na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego.

    b. Użyj hello wartość AssertionConsumerService Adobe dostarczył dla **adres URL odpowiedzi** na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego.
 
### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**. 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>Tworzenie użytkownika testowego Adobe Creative chmury

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w chmurze Creative Adobe muszą mieć przydzielone do Adobe Creative chmury.  
W przypadku hello Adobe Creative chmury Inicjowanie obsługi to zadanie ręczne.

**tooprovision kont użytkowników, wykonaj hello następujące kroki:**

1. Zaloguj się za tooyour witryny firmy Adobe Creative chmurze jako administrator.

2. Kliknij przycisk **osób**.

    ![Osoby](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "osób")

3. Kliknij przycisk **zaprosić użytkowników**.

    ![Zaprosić użytkowników](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "zaprosić użytkowników")

4. Na powitania **zaprosić użytkowników** okna dialogowego wykonaj hello następujące kroki:

    ![Zaproś inne osoby](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Zaproś inne osoby")

    a. W hello **E-mail** pole tekstowe, adres e-mail hello typu Simona Britta konta.
    
    b. Kliknij przycisk **zaprosić**.

    > [!NOTE]
    > właścicielem konta usługi Azure Active Directory Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooAdobe dostępu Creative chmury.

![Przypisz użytkownika][200] 

**tooassign tooAdobe Simona Britta Creative chmury, wykonaj hello następujące kroki:**

1. W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **chmury Creative Adobe**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Adobe Creative chmury hello w hello Panel dostępu, należy pobrać aplikacji w chmurze Creative Adobe tooyour zalogowane automatycznie.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png