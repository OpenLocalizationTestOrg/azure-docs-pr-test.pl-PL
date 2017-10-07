---
title: 'Samouczek: Integracji Azure Active Directory z Bonusly | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a>Samouczek: Integracji Azure Active Directory z Bonusly

Z tego samouczka, dowiesz się, jak toointegrate Bonusly w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Bonusly zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooBonusly
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBonusly (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Bonusly należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Bonusly logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Bonusly z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-bonusly-from-hello-gallery"></a>Dodawanie Bonusly z galerii hello
tooconfigure hello integracji Bonusly do usługi Azure AD, należy tooadd Bonusly z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Bonusly z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **Bonusly**, wybierz pozycję **Bonusly** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Bonusly hello listy wyników](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Bonusly w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Bonusly jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Bonusly musi toobe ustanowione.

W Bonusly, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Bonusly, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Bonusly](#create-a-bonusly-test-user)**  -toohave odpowiednikiem Simona Britta w Bonusly, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne Bonusly aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Bonusly, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Bonusly** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. Na powitania **Bonusly domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Adresy URL i domeny bonusly pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://Bonus.ly/saml/<tenant-name>`

    > [!NOTE] 
    > wartość Hello nie jest prawdziwe. Wartość hello aktualizacji z hello rzeczywisty adres URL odpowiedzi. Skontaktuj się z [zespołem pomocy technicznej Bonusly](https://Bonusly/contact) tooget hello wartość.
 
4. Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartość z zakresu od hello certyfikatu.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. Na powitania **Bonusly konfiguracji** kliknij **skonfigurować Bonusly** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Bonusly konfiguracji](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. W oknie innej przeglądarki, zaloguj się za tooyour **Bonusly** dzierżawy.

8. Witaj pasku narzędzi u góry hello, kliknij przycisk **ustawienia**, a następnie wybierz **integracji i aplikacje**.
   
    ![Sekcja społecznościowych bonusly](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")
9. W obszarze **rejestracji jednokrotnej**, wybierz pozycję **SAML**.

10. Na powitania **SAML** okna dialogowego wykonaj hello następujące kroki:
   
    ![Strony okna dialogowego Saml bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")
   
    a. W hello **logowania jednokrotnego IdP docelowy adres URL** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.
   
    b. W hello **wystawcy IdP** pole tekstowe, Wklej hello wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure. 

    c. W hello **adres URL logowania IdP** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.

    d. Wklej **odcisk palca** wartość skopiowany z portalu Azure do hello **odcisk palca certyfikatu** pola tekstowego.
   
11. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-bonusly-test-user"></a>Tworzenie użytkownika testowego Bonusly

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w tooBonusly muszą mieć przydzielone do Bonusly. W przypadku hello Bonusly Inicjowanie obsługi to zadanie ręczne.

>[!NOTE]
>Możesz użyć innych Bonusly użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Bonusly tooprovision AAD kont użytkowników.
>  

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. W oknie przeglądarki sieci web Zaloguj się za tooyour Bonusly dzierżawy.

2. Kliknij przycisk **ustawienia**.
 
    ![Ustawienia](./media/active-directory-saas-bonus-tutorial/ic781041.png "ustawienia")

3. Kliknij przycisk hello **użytkowników i dodatki** kartę.
   
    ![Użytkownicy i dodatki](./media/active-directory-saas-bonus-tutorial/ic781042.png "użytkowników i dodatki")

4. Kliknij przycisk **Zarządzanie użytkownikami**.
   
    ![Zarządzaj użytkownikami](./media/active-directory-saas-bonus-tutorial/ic781043.png "Zarządzanie użytkownikami")

5. Kliknij przycisk **dodać użytkownika**.
   
    ![Dodaj użytkownika](./media/active-directory-saas-bonus-tutorial/ic781044.png "Dodaj użytkownika")

6. Na powitania **Dodaj użytkownika** okna dialogowego, wykonaj następujące kroki hello:
   
    ![Dodaj użytkownika](./media/active-directory-saas-bonus-tutorial/ic781045.png "Dodaj użytkownika")  

    a. W hello **imię** pole tekstowe, wprowadź hello imię użytkownika, takich jak **Britta**.

    b. W hello **nazwisko** pole tekstowe, wprowadź hello nazwisko użytkownika, takich jak **Simona**.
 
    c. W hello **E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .

    d. Kliknij pozycję **Zapisz**.
   
     >[!NOTE]
     >Właściciel konta usługi Azure AD Hello otrzymuje wiadomość e-mail zawierającą łącze tooconfirm hello konta, zanim staje się aktywny.
     >  

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBonusly.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooBonusly Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Bonusly**.

    ![Witaj Bonusly łącza na liście aplikacji hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.

Po kliknięciu kafelka Bonusly hello w hello Panel dostępu, należy pobrać aplikację Bonusly tooyour zalogowane automatycznie.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

