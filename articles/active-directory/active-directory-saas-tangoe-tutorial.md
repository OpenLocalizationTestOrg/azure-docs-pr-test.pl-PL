---
title: 'Samouczek: Integracji Azure Active Directory z Tangoe polecenia Premium Mobile | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Tangoe polecenie Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a>Samouczek: Integracji Azure Active Directory z Tangoe polecenia Premium Mobile

Z tego samouczka, dowiesz się, jak toointegrate Tangoe polecenia Premium Mobile w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Tangoe polecenia Premium Mobile zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooTangoe polecenia mobilnych — wersja Premium
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTangoe polecenia mobilnych — wersja Premium (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z Tangoe polecenia Premium Mobile należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Mobile Premium polecenia Tangoe logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodaj Mobile Premium polecenie Tangoe z galerii hello
2. Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a>Dodaj Mobile Premium polecenie Tangoe z galerii hello
tooconfigure hello integracji Tangoe polecenia Premium Mobile w usłudze Azure Active Directory, należy tooadd Mobile Premium polecenie Tangoe z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Tangoe polecenia Premium Mobile z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W hello wyszukiwania wpisz **Tangoe polecenia Premium Mobile**, wybierz pozycję **Tangoe polecenia Premium Mobile** z panelu wyników kliknięcie **Dodaj** przycisk aplikacji hello tooadd.

    ![Dodaj Mobile Premium polecenie Tangoe z galerii ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Mobile Premium polecenia Tangoe w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Tangoe polecenia Premium Mobile jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Tangoe polecenia Premium Mobile musi toobe ustanowione.

W Tangoe polecenia Premium urządzeń przenośnych, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Tangoe polecenia Premium Mobile, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Mobile Premium polecenia Tangoe](#create-a-tangoe-command-premium-mobile-test-user)**  -toohave odpowiednikiem Simona Britta w Tangoe polecenia Premium Mobile, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne do aplikacji mobilnych — wersja Premium polecenia Tangoe.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z urządzeń przenośnych Premium polecenia Tangoe, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Tangoe polecenia Premium Mobile** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Na podstawie SAML logowania jednokrotnego](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. Na powitania **Tangoe polecenia Premium Mobile domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Polecenie Tangoe Premium przenośnych domeny i adres URL](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://sso.tangoe.com/sp/ACS.saml2`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Adres URL odpowiedzi rzeczywiste hello i adres URL logowania, należy zaktualizować te wartości. Skontaktuj się z [zespołem pomocy technicznej klienta Mobile Premium polecenia Tangoe](https://www.tangoe.com/contact-2/) tooget tych wartości. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Przyciskiem Zapisz](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. Na powitania **konfigurację Mobile Premium polecenia Tangoe** , kliknij przycisk **skonfigurować Mobile Premium polecenia Tangoe** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Sekcja konfiguracji Mobile Premium polecenia Tangoe](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. tooget logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z Twojego [zespołem pomocy technicznej klienta Mobile Premium polecenia Tangoe](https://www.tangoe.com/contact-2/) i podaj następujące hello:

   - Plik metadanych pobranych Hello
   - Witaj **identyfikator jednostki SAML**
   - Witaj **SAML pojedynczy znak na adres URL usługi**
   - Witaj **Sign-Out adresu URL**

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Użytkownicy i grupy -> Wszyscy użytkownicy](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Dodawanie użytkownika](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Strony okna dialogowego użytkownika](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a>Tworzenie użytkownika testowego Tangoe polecenia Premium Mobile

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Tangoe polecenia Premium Mobile. 

Aplikacji mobilnych — wersja Premium polecenia Tangoe musi wszystkich toobe użytkowników hello udostępniane w aplikacji hello przed wykonaniem rejestracji jednokrotnej. Pracy, dlatego należy z hello [zespołem pomocy technicznej klienta Mobile Premium polecenia Tangoe](https://www.tangoe.com/contact-2/) tooprovision tych użytkowników do aplikacji hello. 

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTangoe Mobile Premium polecenia.

![Przypisz użytkownika][200] 

**tooassign tooTangoe Simona Britta polecenia Premium urządzeń przenośnych, należy wykonać hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Tangoe polecenia Premium Mobile**.

    ![Tangoe polecenia Premium Mobile listy aplikacji](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą hello panelu dostępu.

Po kliknięciu kafelka Tangoe polecenia Premium Mobile hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji mobilnych — wersja Premium polecenia Tangoe. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

