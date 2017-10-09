---
title: "Samouczek: Integracji Azure Active Directory z Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a>Samouczek: Integracji Azure Active Directory z Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)

Z tego samouczka, dowiesz się, jak toointegrate Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) z usługą Azure Active Directory (Azure AD).

Integrowanie Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooFive9, a także karty (CTI, skontaktuj się z Centrum agentów)
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFive9 Plus karty (CTI, skontaktuj się z Centrum agentów) (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Integracja tooconfigure usługi Azure AD z Five9 Plus karty (CTI, skontaktuj się z Centrum agentów), należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a>Dodawanie Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) z galerii hello
tooconfigure hello integracji Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) do usługi Azure AD, należy tooadd Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. W panelu wyników hello, wybierz **Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) na podstawie użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) musi toobe ustanowione.

W Five9 Plus karty (CTI, skontaktuj się z Centrum agentów), należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Five9 Plus karty (CTI, skontaktuj się z Centrum agentów), należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave odpowiednikiem Simona Britta Five9 Plus karty (CTI, skontaktuj się z Centrum agentów), który jest odpowiednikiem połączonych toohello usługi Azure AD użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Five9 Plus karty (CTI, skontaktuj się z Centrum agentów).

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Five9 Plus karty (CTI, skontaktuj się z Centrum agentów), wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. Na powitania **domeny Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) i adresy URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    a. W hello **identyfikator** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:

    |    Środowisko      |       ADRES URL      |
    | :-- | :-- |
    | "Five9 plus karty dla programu Microsoft Dynamics CRM" | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | "Five9 plus karta Zendesk" | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | "Five9 plus karta Toolkit pulpitu agenta" | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:

    |      Środowisko     |      ADRES URL      |
    | :--                  | :--           |
    | "Five9 plus karty dla programu Microsoft Dynamics CRM" | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | "Five9 plus karta Zendesk" | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | "Five9 plus karta Toolkit pulpitu agenta" | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)** kliknij **skonfigurować Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. tooconfigure rejestracji jednokrotnej w **Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)** strony, należy pobrać hello toosend **Certificate(Base64), adres URL Sign-Out, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** za[zespołem pomocy technicznej Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)](https://www.five9.com/about/contact). Również Ponadto dla dalszego Konfigurowanie logowania jednokrotnego wykonaj hello następujące czynności, zgodnie z toohello karty:

    a. "Five9 Plus karta Toolkit pulpitu agenta" Przewodnik administratora: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)
    
    b. "Five9 Plus karty dla programu Microsoft Dynamics CRM" Przewodnik administratora: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)
    
    c. "Five9 Plus karta Zendesk" Przewodnik administratora: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)


> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a>Tworzenie użytkownika testowego Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Five9 Plus karty (CTI, skontaktuj się z Centrum agentów). Praca z [zespołem pomocy technicznej Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)](https://www.five9.com/about/contact) do dodawania użytkowników hello hello Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) platformy. Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooFive9 Plus karty (CTI, skontaktuj się z Centrum agentów).

![Przypisz użytkownika][200] 

**tooassign Simona Britta tooFive9 Plus karty (CTI, skontaktuj się z Centrum agentów), wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

