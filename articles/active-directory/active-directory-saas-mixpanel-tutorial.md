---
title: 'Samouczek: Integracji Azure Active Directory z Mixpanel | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Mixpanel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 8da8aaefee3558c37babe3e10aeba4224ceffa16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a>Samouczek: Integracji Azure Active Directory z Mixpanel

Z tego samouczka, dowiesz się, jak toointegrate Mixpanel w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Mixpanel zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMixpanel
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMixpanel (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Mixpanel należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Mixpanel logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Mixpanel z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-mixpanel-from-hello-gallery"></a>Dodawanie Mixpanel z galerii hello
tooconfigure hello integracji Mixpanel do usługi Azure AD, należy tooadd Mixpanel z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Mixpanel z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Mixpanel**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. W panelu wyników hello zaznacz **Mixpanel**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Mixpanel w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Mixpanel jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Mixpanel musi toobe ustanowione.

W Mixpanel, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Mixpanel, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Mixpanel](#creating-a-mixpanel-test-user)**  -toohave odpowiednikiem Simona Britta w Mixpanel, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Mixpanel.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Mixpanel, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Mixpanel** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. Na powitania **Mixpanel domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     W hello **adres URL logowania** tekstowym, wpisz adres URL jako:`https://mixpanel.com/login/`

    > [!NOTE] 
    > Zarejestruj w [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset zapasową poświadczeń logowania i skontaktuj się z pomocą hello [zespołem pomocy technicznej Mixpanel](mailto:support@mixpanel.com) tooenable ustawienia logowania jednokrotnego dla dzierżawy. Możesz również uzyskać wartość na adres URL logowania w razie potrzeby z zespołem pomocy technicznej Mixpanel. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Mixpanel** kliknij **skonfigurować Mixpanel** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. W oknie innej przeglądarki, logowania jednokrotnego tooyour Mixpanel aplikacji jako administrator.

8. W dolnej części strony hello, kliknij polecenie hello nieco **narzędzi** ikonę w lewym rogu hello. 
   
    ![Mixpanel rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. Kliknij przycisk hello **dostęp zabezpieczeń** , a następnie kliknij pozycję **zmienić ustawienia**.
   
    ![Ustawienia Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. Na powitania **zmienić certyfikat** strony okna dialogowego, kliknij przycisk **wybierz plik** tooupload pobranego certyfikatu, a następnie kliknij przycisk **dalej**.
   
    ![Ustawienia Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  W polu tekstowym adres URL uwierzytelniania hello na powitania **zmienić adres URL uwierzytelniania** strony okna dialogowego, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** , które zostały skopiowane z portalu Azure, a następnie kliknij przycisk **Dalej**.
   
   ![Ustawienia Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. Kliknij przycisk **Gotowe**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-mixpanel-test-user"></a>Tworzenie użytkownika testowego Mixpanel

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Mixpanel. 

1. Rejestracja tooyour Mixpanel witryny firmy jako administrator.

2. Na powitania u dołu strony hello, kliknij przycisk hello małego koło zębate znajdującego się na powitania lewym rogu tooopen hello **ustawienia** okna.

3. Kliknij przycisk hello **zespołu** kartę.

4. W hello **członek zespołu** tekstowym, wpisz adres e-mail firmy Britta hello Azure.
   
    ![Ustawienia Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. Kliknij przycisk **zaprosić**. 

> [!Note]
> Witaj, użytkownik otrzyma tooset e-mail hello profilu.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMixpanel.

![Przypisz użytkownika][200] 

**tooassign tooMixpanel Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Mixpanel**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Mixpanel hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Mixpanel aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

