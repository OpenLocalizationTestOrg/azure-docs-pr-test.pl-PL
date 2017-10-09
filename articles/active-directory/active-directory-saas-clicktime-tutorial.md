---
title: 'Samouczek: Integracji Azure Active Directory z ClickTime | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a>Samouczek: Integracji Azure Active Directory z ClickTime

Z tego samouczka, dowiesz się, jak toointegrate ClickTime w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD ClickTime zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooClickTime
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooClickTime (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z ClickTime należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- ClickTime logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie ClickTime z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-clicktime-from-hello-gallery"></a>Dodawanie ClickTime z galerii hello
tooconfigure hello integracji ClickTime do usługi Azure AD, należy tooadd ClickTime z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd ClickTime z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **ClickTime**, wybierz pozycję **ClickTime** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![ClickTime hello listy wyników](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ClickTime w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w ClickTime jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w ClickTime musi toobe ustanowione.

W ClickTime, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ClickTime, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego ClickTime](#create-a-clicktime-test-user)**  -toohave odpowiednikiem Simona Britta w ClickTime, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji ClickTime.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z ClickTime, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **ClickTime** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. Na powitania **ClickTime domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Adresy URL i domeny ClickTime pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL jako:`https://app.clicktime.com/sp/`
    
    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców: 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji ClickTime** kliknij **skonfigurować ClickTime** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfiguracja ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy ClickTime jako administrator.

8. Witaj pasku narzędzi u góry hello, kliknij przycisk **preferencje**, a następnie kliknij przycisk **ustawienia zabezpieczeń**.

9. W hello **preferencje rejestracji jednokrotnej** konfiguracji sekcji, wykonaj następujące kroki hello:
   
    ![Ustawienia zabezpieczeń](./media/active-directory-saas-clicktime-tutorial/tic777280.png "ustawienia zabezpieczeń")
   
    a.  Wybierz **Zezwalaj** Zaloguj się przy użyciu pojedynczego logowania jednokrotnego (SSO) z **usługi Azure AD**.
   
    b. W hello **punktu końcowego dostawcy tożsamości** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.
   
    c.  Otwórz hello **certyfikatu algorytmem base-64** pobrany z portalu Azure w **Notatnik**, skopiuj zawartość hello i wkleić go do hello **certyfikatu X.509** pola tekstowego.
   
    d.  Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-clicktime-test-user"></a>Tworzenie użytkownika testowego ClickTime

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do ClickTime muszą mieć przydzielone do ClickTime.  
W przypadku hello ClickTime Inicjowanie obsługi to zadanie ręczne.

> [!NOTE]
> Możesz użyć innych ClickTime użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez ClickTime tooprovision kont użytkowników usługi Azure AD.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**
1. Zaloguj się za tooyour **ClickTime** dzierżawy.
2. Witaj pasku narzędzi u góry hello, kliknij przycisk **firmy**, a następnie kliknij przycisk **osób**.
   
    ![Osoby](./media/active-directory-saas-clicktime-tutorial/tic777282.png "osób")
3. Kliknij przycisk **Dodaj osobę**.
   
    ![Dodaj osobę](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Dodaj osobę")
4. W sekcji nowej osoby hello wykonaj hello następujące kroki:
   
    ![Osoby](./media/active-directory-saas-clicktime-tutorial/tic777284.png "osób")
   
    a.  W hello **Pełna nazwa** pole tekstowe, typ Pełna nazwa użytkownika, takich jak **Simona Britta**. 
  
    b.  W hello **adres e-mail** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak  **brittasimon@contoso.com** .
       
    > [!NOTE]
    > Jeśli chcesz, można ustawić dodatkowe właściwości hello nowy obiekt osoby.
   
    c.  Kliknij pozycję **Zapisz**.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooClickTime.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooClickTime Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **ClickTime**.

    ![Łącze ClickTimne na liście aplikacji hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka ClickTime hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour ClickTime aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

