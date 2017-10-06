---
title: 'Samouczek: Integracji Azure Active Directory z przodu | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między Azure Active Directory i do przodu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a>Samouczek: Integracji Azure Active Directory z przodu

Z tego samouczka, dowiesz się, jak toointegrate przodu z usługą Azure Active Directory (Azure AD).

Integrowanie przodu z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooFront.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFront (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Integracja tooconfigure usługi Azure AD z przodu, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Front logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie przodu z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-front-from-hello-gallery"></a>Dodawanie przodu z galerii hello
tooconfigure hello integracji przodu do usługi Azure AD, należy tooadd przodu z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd przodu z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **Front**, wybierz pozycję **Front** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Front hello listy wyników](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przodu w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow na wierzchu użytkownika odpowiednikiem hello jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi na wierzchu musi toobe ustanowione.

Na wierzchu przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z przodu, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego przodu](#create-a-front-test-user)**  -toohave Simona Britta w odpowiednikiem na wierzchu toohello połączonej usługi Azure AD reprezentacja użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne do przodu aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z przodu, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Front** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. Na powitania **Front domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.frontapp.com`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.frontapp.com/sso/saml/callback`

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.frontapp.com`
     
    > [!NOTE] 
    > Wartości te nie są prawdziwe. Aktualizacja tych wartości za pomocą hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, które opisano szczegółowo w dalszej części samouczka lub skontaktuj się z [zespołem pomocy technicznej klienta Front](mailto:support@frontapp.com) tooget tych wartości. 

5. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. Na powitania **konfiguracji frontonu** kliknij **skonfigurować Front** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. Dzierżawca przodu tooyour logowania jako administrator.

9. Przejdź za**ustawień (koło zębate ikonę u dołu po lewej stronie paska bocznego hello hello) > Preferencje**.
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. Kliknij przycisk **rejestracji jednokrotnej** łącza.
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. Wybierz **SAML** liście rozwijanej hello **rejestracji jednokrotnej**.
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. W hello **punktu wejścia** pole tekstowe umieścić wartość hello **pojedynczy znak na adres URL usługi** z Kreatora konfiguracji aplikacji usługi Azure AD.
    
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. Otwórz z pobranego **Certificate(Base64)** pliku w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu podpisywania** pola tekstowego.
    
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. Na powitania **ustawień dostawcy usług** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    a. Skopiuj wartość hello **identyfikator jednostki** i wklej go do hello **identyfikator** textbox w **Front domeny i adres URL** sekcji w portalu Azure.

    b. Skopiuj wartość hello **adres URL usługi ACS** i wklej go do hello **adres URL logowania** textbox w **Front domeny i adres URL** sekcji w portalu Azure.
    
15. Kliknij przycisk **zapisać** przycisku.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-front-test-user"></a>Tworzenie użytkownika testowego przodu

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta na wierzchu. Praca z [zespołem pomocy technicznej klienta Front](mailto:support@frontapp.com) do dodawania użytkowników hello hello przodu platformy. Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooFront.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooFront Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Front**.

    ![łącze przodu Hello na liście aplikacji hello](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest przy użyciu usługi Azure AD SSOconfiguration hello panelu dostępu.

Po kliknięciu kafelka przodu hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour przodu aplikacji. 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

