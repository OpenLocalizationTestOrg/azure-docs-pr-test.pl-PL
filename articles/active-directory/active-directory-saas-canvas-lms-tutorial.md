---
title: 'Samouczek: Integracji Azure Active Directory z kanwy Lms | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i LMS kanwy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a>Samouczek: Integracji Azure Active Directory z LMS kanwy

Z tego samouczka, dowiesz się, jak toointegrate obszaru roboczego z usługą Azure Active Directory (Azure AD).

Integracja z usługą Azure AD kanwy zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooCanvas
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCanvas (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD kanwy, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Kanwy jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodanie obszaru roboczego z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-canvas-from-hello-gallery"></a>Dodanie obszaru roboczego z galerii hello
tooconfigure hello integracja kanwy programu Azure AD, należy tooadd obszaru roboczego z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd obszaru roboczego z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **kanwy**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. W panelu wyników hello, wybierz **kanwy**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej kanwy oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello kanwie jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi kanwie musi toobe ustanowione.

W obszarze roboczym należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z kanwy, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego kanwy](#creating-a-canvas-test-user)**  -toohave odpowiednikiem Simona Britta w kanwy, która jest odpowiednikiem połączonych toohello usługi Azure AD użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji kanwy.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z kanwy, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **kanwy** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. Na powitania **kanwy domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.instructure.com`

    b. W hello **identyfikator** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://<tenant-name>.instructure.com/saml2`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta kanwy](https://community.canvaslms.com/community/help) tooget tych wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartości certyfikatu.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji kanwy** kliknij **skonfigurować kanwy** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Zmień adres URL hasła, adres URL Sign-Out identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy kanwy tooyour jako administrator.

8. Przejdź za**kursów \> kont zarządzanych \> Microsoft**.
   
    ![Kanwy](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "kanwy")

9. W okienku nawigacji hello powitania po lewej stronie wybierz **uwierzytelniania**, a następnie kliknij przycisk **dodać nowej konfiguracji SAML**.
   
    ![Uwierzytelnianie](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "uwierzytelniania")

10. Na stronie bieżącego integracji hello wykonaj hello następujące kroki:
   
    ![Integracja z bieżącym](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "bieżącego integracji")

    a. W **identyfikator jednostki IdP** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.

    b. W **dziennika na adres URL** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.

    c. W **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.

    d. W **łącze Zmień hasło** pole tekstowe, Wklej wartość hello **Zmień adres URL hasła** którego została skopiowana z portalu Azure. 

    e. W **odcisk palca certyfikatu** pole tekstowe, Wklej hello **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.      
        
    f. Z hello **atrybutu logowania** listy, wybierz **NameID**.

    g. Z hello **Format identyfikatora** listy, wybierz **emailAddress**.

    h. Kliknij przycisk **Zapisz ustawienia uwierzytelniania**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-canvas-test-user"></a>Tworzenie użytkownika testowego kanwy

toolog użytkowników tooenable usługi Azure AD w tooCanvas, muszą mieć przydzielone do kanwy.

W przypadku kanwy Inicjowanie obsługi użytkowników jest zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour **kanwy** dzierżawy.

2. Przejdź za**kursów \> kont zarządzanych \> Microsoft**.
   
   ![Kanwy](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "kanwy")

3. Kliknij przycisk **użytkowników**.
   
   ![Użytkownicy](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "użytkowników")

4. Kliknij przycisk **Dodaj nowego użytkownika**.
   
   ![Użytkownicy](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "użytkowników")

5. Dodaj nowego użytkownika strony okna dialogowego hello wykonywanie hello następujące kroki:
   
   ![Dodaj użytkownika](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Dodaj użytkownika")
   
   a. W hello **imię i nazwisko** pole tekstowe, wprowadź nazwę użytkownika, takie jak hello **BrittaSimon**.

   b. W hello **E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .

   c. W hello **logowania** pole tekstowe, wprowadź adres e-mail usługi Azure AD hello użytkownika, takich jak  **brittasimon@contoso.com** .

   d. Wybierz **E-mail hello użytkownika o tworzeniu tego konta**.

   e. Kliknij przycisk **dodać użytkownika**.

>[!NOTE]
>Możesz użyć innych kanwy użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision kanwy kont użytkowników usługi AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCanvas.

![Przypisz użytkownika][200] 

**tooassign tooCanvas Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **kanwy**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka kanwy hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour obszaru roboczego aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

