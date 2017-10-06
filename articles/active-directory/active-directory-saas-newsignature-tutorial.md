---
title: "Samouczek: Integracji Azure Active Directory za pomocą portalu zarządzania w chmurze Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i chmury portalu zarządzania Microsoft Azure."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9596826e3dc1289b95009bf01ec8b86f823ef345
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a>Samouczek: Integracji Azure Active Directory za pomocą portalu zarządzania w chmurze Microsoft Azure

Z tego samouczka, dowiesz się, jak toointegrate chmury portalu zarządzania Microsoft Azure w usłudze Azure Active Directory (Azure AD).

Integrowanie portalu zarządzania w chmurze platformy Microsoft Azure z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD mającego tooCloud dostęp do portalu zarządzania Microsoft Azure
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCloud portalu zarządzania Microsoft Azure (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD za pomocą portalu zarządzania w chmurze Microsoft Azure, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Portal zarządzania chmury dla Microsoft Azure jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie z galerii hello chmury portalu zarządzania Microsoft Azure
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-hello-gallery"></a>Dodawanie z galerii hello chmury portalu zarządzania Microsoft Azure
tooconfigure hello integracji chmury portalu zarządzania Microsoft Azure w usłudze Azure Active Directory, należy tooadd chmury portalu zarządzania Microsoft Azure z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd chmury portalu zarządzania Microsoft Azure z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **chmury portalu zarządzania Microsoft Azure**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. W panelu wyników hello, wybierz **chmury portalu zarządzania Microsoft Azure**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD logowania jednokrotnego za pomocą portalu zarządzania w chmurze platformy Microsoft Azure w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w chmurze Portal zarządzania platformy Microsoft Azure jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w chmurze Portal zarządzania platformy Microsoft Azure musi toobe ustanowione.

W chmurze Portal zarządzania platformy Microsoft Azure, przypisz wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowanie usługi Azure AD logowania jednokrotnego za pomocą portalu zarządzania w chmurze Microsoft Azure, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie chmury Portal zarządzania dla użytkownika testowego Microsoft Azure](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)**  -toohave odpowiednikiem Simona Britta w chmurze Portal zarządzania platformy Microsoft Azure, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w portalu zarządzania usługi chmury dla aplikacji Microsoft Azure.

**tooconfigure usługi Azure AD logowania jednokrotnego za pomocą portalu zarządzania chmury Microsoft Azure, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **chmury portalu zarządzania Microsoft Azure** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. Na powitania **chmury portalu zarządzania Microsoft Azure domeny i adresów URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców: 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    b. W hello **identyfikator** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców: 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    c. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców: 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości hello rzeczywisty adres URL logowania, identyfikator i odpowiedzi adres URL. Skontaktuj się z [chmurze Portal zarządzania dla klienta platformy Microsoft Azure z pomocą techniczną](mailto:jczernuszka@newsignature.com) tooget tych wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. Na powitania **chmurze Portal zarządzania dla programu Microsoft Azure Configuration** kliknij **skonfigurować Portal zarządzania chmury Microsoft Azure** tooopen **Konfigurowanie logowania jednokrotnego**okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. tooconfigure rejestracji jednokrotnej w **chmury portalu zarządzania Microsoft Azure** strony, należy pobrać hello toosend **certyfikatu**, **Sign-Out URL**, **SAML pojedynczy znak na adres URL usługi** i **identyfikator jednostki SAML** za[chmurze Portal zarządzania dla zespołu pomocy technicznej Microsoft Azure](mailto:jczernuszka@newsignature.com). To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a>Tworzenie chmury Portal zarządzania dla użytkownika testowego Microsoft Azure

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w chmurze portalu zarządzania Microsoft Azure. We współpracy z [chmurze Portal zarządzania dla zespołu pomocy technicznej Microsoft Azure](mailto:jczernuszka@newsignature.com) tooadd hello użytkowników w hello chmurze Portal zarządzania dla konta Microsoft Azure.


### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCloud portalu zarządzania Microsoft Azure.

![Przypisz użytkownika][200] 

**tooassign tooCloud Simona Britta portalu zarządzania Microsoft Azure, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **chmury portalu zarządzania Microsoft Azure**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.
Po kliknięciu hello chmury portalu zarządzania Microsoft Azure kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour chmurze Portal zarządzania dla aplikacji Microsoft Azure.

Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

