---
title: "Samouczek: Azure Active Directory Integracja z platformą zarządzania kontraktu Icertis | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i platformy zarządzania Icertis kontraktu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6627e6dd-f559-4cd4-a509-f6d9a4961b49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 6eb99553ef9df732512a38fb0489e66b41ba94a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icertis-contract-management-platform"></a>Samouczek: Azure Active Directory Integracja z platformą zarządzania Icertis kontraktu

Z tego samouczka, dowiesz się, jak toointegrate Icertis kontraktu platformy do zarządzania z usługą Azure Active Directory (Azure AD).

Integracja platformy zarządzania kontraktu Icertis z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooIcertis platformy zarządzania kontraktu
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooIcertis kontraktu platformy zarządzania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z platformą zarządzania kontraktu Icertis należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Platforma zarządzania kontraktu Icertis logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie platformy zarządzania kontraktu Icertis z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-icertis-contract-management-platform-from-hello-gallery"></a>Dodawanie platformy zarządzania kontraktu Icertis z galerii hello
tooconfigure hello integracji platformy zarządzania Icertis kontraktu usługi Azure AD, należy tooadd platformy zarządzania kontraktu Icertis z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Icertis platformy zarządzania umowy z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **platformy zarządzania kontraktu Icertis**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_search.png)

5. W panelu wyników hello, wybierz **platformy zarządzania kontraktu Icertis**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z platformą zarządzania kontraktu Icertis w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello platformy zarządzania kontraktu Icertis jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi na platformie zarządzania kontraktu Icertis musi toobe ustanowione.

W Icertis kontraktu platformy zarządzania, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z platformą zarządzania Icertis kontraktu, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego platformy zarządzania kontraktu Icertis](#creating-an-icertis-contract-management-platform-test-user)**  -toohave odpowiednikiem Simona Britta w Icertis kontraktu platformy do zarządzania toohello połączonej usługi Azure AD reprezentacja użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji platformy zarządzania Icertis kontraktu.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z platformą zarządzania kontraktu Icertis, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **platformy zarządzania kontraktu Icertis** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_samlbase.png)

3. Na powitania **adresy URL i domeny platformy zarządzania kontraktu Icertis** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.icertis.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.icertis.com`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta platformy zarządzania kontraktu Icertis](https://www.icertis.com/company/contact/) tooget tych wartości. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-icertisicm-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji platformy zarządzania kontraktu Icertis** kliknij **skonfigurować platformę zarządzania kontraktu Icertis** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_configure.png) 

7. tooconfigure rejestracji jednokrotnej w **platformy zarządzania kontraktu Icertis** strony, należy pobrać hello toosend **XML metadanych** i **Sign-Out adres URL, identyfikator jednostki SAML i SAML logowania jednokrotnego Adres URL usługi** za[zespołem pomocy technicznej platformy zarządzania kontraktu Icertis](https://www.icertis.com/company/contact/).

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-icertis-contract-management-platform-test-user"></a>Tworzenie użytkownika testowego platformy zarządzania Icertis kontraktu

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Icertis kontraktu zarządzania platformy. We współpracy z [zespołem pomocy technicznej platformy zarządzania kontraktu Icertis](https://www.icertis.com/company/contact/) tooadd hello użytkowników w hello platformy zarządzania Icertis kontraktu.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooIcertis kontraktu platformy zarządzania.

![Przypisz użytkownika][200] 

**tooassign tooIcertis Simona Britta kontraktu platformy zarządzania, należy wykonać hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **platformy zarządzania kontraktu Icertis**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.

Po kliknięciu kafelka platformy zarządzania kontraktu Icertis hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour platformy zarządzania kontraktu Icertis aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_203.png

