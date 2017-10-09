---
title: 'Samouczek: Integracji Azure Active Directory z Picturepark | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a>Samouczek: Integracji Azure Active Directory z Picturepark

Z tego samouczka, dowiesz się, jak toointegrate Picturepark w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Picturepark zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPicturepark
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPicturepark (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Picturepark należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Picturepark logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Picturepark z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-picturepark-from-hello-gallery"></a>Dodawanie Picturepark z galerii hello
tooconfigure hello integracji Picturepark do usługi Azure AD, należy tooadd Picturepark z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Picturepark z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Picturepark**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. W panelu wyników hello zaznacz **Picturepark**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Picturepark w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Picturepark jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Picturepark musi toobe ustanowione.

W Picturepark, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Picturepark, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Picturepark](#creating-a-picturepark-test-user)**  -toohave odpowiednikiem Simona Britta w Picturepark, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Picturepark.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Picturepark, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Picturepark** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. Na powitania **Picturepark domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.picturepark.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca: 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta Picturepark](https://picturepark.com/about/contact/) tooget tych wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartości certyfikatu.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Picturepark** kliknij **skonfigurować Picturepark** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Picturepark jako administrator.

8. Witaj pasku narzędzi u góry hello, kliknij przycisk **narzędzia administracyjne**, a następnie kliknij przycisk **konsoli zarządzania**.
   
    ![Konsola zarządzania](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Konsola zarządzania")

9. Kliknij przycisk **uwierzytelniania**, a następnie kliknij przycisk **dostawców tożsamości**.
   
    ![Uwierzytelnianie](./media/active-directory-saas-picturepark-tutorial/ic795063.png "uwierzytelniania")

10. W hello **konfiguracji dostawcy tożsamości** sekcji, wykonaj następujące kroki hello:
   
    ![Konfiguracja dostawcy tożsamości](./media/active-directory-saas-picturepark-tutorial/ic795064.png "konfiguracji dostawcy tożsamości")
   
    a. Kliknij pozycję **Dodaj**.
  
    b. Wpisz nazwę dla danej konfiguracji.
   
    c. Wybierz **Ustaw jako domyślny**.
   
    d. W **URI wystawcy** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.
   
    e. W **zaufanego wystawcy miniatury** pole tekstowe, Wklej wartość hello **odcisk palca** , które zostały skopiowane z **certyfikat podpisywania SAML** sekcji. 

11. Kliknij przycisk **JoinDefaultUsersGroup**.

12. tooset hello **Emailaddress** atrybutu w hello **oświadczeń** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` i kliknij przycisk **zapisać**.

      ![Konfiguracja](./media/active-directory-saas-picturepark-tutorial/ic795065.png "konfiguracji")

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-picturepark-test-user"></a>Tworzenie użytkownika testowego Picturepark

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Picturepark muszą mieć przydzielone do Picturepark. W przypadku hello Picturepark Inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour **Picturepark** dzierżawy.

2. Witaj pasku narzędzi u góry hello, kliknij przycisk **narzędzia administracyjne**, a następnie kliknij przycisk **użytkowników**.
   
    ![Użytkownicy](./media/active-directory-saas-picturepark-tutorial/ic795067.png "użytkowników")

3. W hello **Przegląd użytkowników** , kliknij pozycję **nowy**.
   
    ![Zarządzanie użytkownikami](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Zarządzanie użytkownikami")

4. Na powitania **Tworzenie użytkownika** okna dialogowego, hello wykonaj następujące kroki prawidłowego Azure Active Directory użytkownika ma tooprovision:
   
    ![Utwórz użytkownika](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Tworzenie użytkownika")
   
    a. W hello **adres E-mail** pole tekstowe, hello typu **adres e-mail** użytkownika hello  **BrittaSimon@contoso.com** .  
   
    b. W hello **hasło** i **Potwierdź hasło** pól tekstowych, hello typu **hasło** z BrittaSimon. 
   
    c. W hello **imię** pole tekstowe, hello typu **imię** użytkownika hello **Britta**. 
   
    d. W hello **nazwisko** pole tekstowe, hello typu **nazwisko** użytkownika hello **Simona**.
   
    e. W hello **firmy** pole tekstowe, hello typu **nazwa firmy** hello użytkownika. 
   
    f. W hello **kraju** pole tekstowe, wybierz hello **kraju** hello użytkownika.
  
    g. W hello **ZIP** pole tekstowe, hello typu **kod POCZTOWY** hello miasta.
   
    h. W hello **miasta** pole tekstowe, hello typu **nazwę miejscowości** hello użytkownika.

    i. Wybierz **języka**.
   
    j. Kliknij przycisk **Utwórz**.

>[!NOTE]
>Możesz użyć innych Picturepark użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Picturepark tooprovision kont użytkowników usługi Azure AD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPicturepark.

![Przypisz użytkownika][200] 

**tooassign tooPicturepark Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Picturepark**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Picturepark hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Picturepark aplikacji. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

