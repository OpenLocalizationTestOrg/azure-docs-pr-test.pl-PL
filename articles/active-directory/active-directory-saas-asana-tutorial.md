---
title: 'Samouczek: Integracji Azure Active Directory z Asana | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Asana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a>Samouczek: Integracji Azure Active Directory z Asana

Z tego samouczka, dowiesz się, jak toointegrate Asana w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Asana zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAsana
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAsana (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Asana należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Asana jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Asana z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-asana-from-hello-gallery"></a>Dodawanie Asana z galerii hello
tooconfigure hello integracji Asana do usługi Azure AD, należy tooadd Asana z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Asana z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **Asana**, wybierz pozycję **Asana** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Asana na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Asana jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Asana musi toobe ustanowione.

W Asana, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Asana, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Asana](#create-an-asana-test-user)**  -toohave odpowiednikiem Simona Britta w Asana, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Asana.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Asana, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Asana** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. Na powitania **Asana domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Adresy URL i domeny Asana pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    a. W hello **adres URL logowania** pole tekstowe, wprowadź adres URL:`https://app.asana.com/`

    b. W hello **identyfikator** pole tekstowe, wartość typu:`https://app.asana.com/`
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Asana** kliknij **skonfigurować Asana** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfiguracja Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. W oknie innej przeglądarki, logowania jednokrotnego tooyour Asana aplikacji. Logowanie Jednokrotne w Asana, ustawień dostępu hello obszaru roboczego, klikając nazwę obszaru roboczego hello na powitania prawym górnym rogu ekranu hello tooconfigure. Następnie kliknij  **\<nazwa obszaru roboczego\> ustawienia**. 
   
    ![Ustawienia logowania jednokrotnego Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. Na powitania **ustawienia organizacji** okna, kliknij przycisk **administracji**. Następnie kliknij przycisk **elementów członkowskich należy zalogować się za pośrednictwem SAML** tooenable hello logowania jednokrotnego konfiguracji. Witaj wykonaj hello następujące kroki:
   
    ![Skonfiguruj ustawienia organizacji rejestracji jednokrotnej](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     a. W hello **adres URL logowania strony** pole tekstowe, Wklej hello **SAML pojedynczy znak na adres URL usługi**.

     b. Kliknij prawym przyciskiem myszy certyfikat hello pobrany z portalu Azure, a następnie otwórz plik certyfikatu hello Notatniku lub w edytorze tekstów preferowany. Kopiowanie zawartości hello między hello begin i hello zakończenia certyfikatów tytułu i wklej go w hello **certyfikatu X.509** pola tekstowego.

9. Kliknij pozycję **Zapisz**. Przejdź za[Asana przewodnik konfigurowania rejestracji Jednokrotnej](https://asana.com/guide/help/premium/authentication#gl-saml) Jeœli potrzebujesz dodatkowej pomocy.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-an-asana-test-user"></a>Tworzenie użytkownika testowego Asana

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Asana.

1. Na **Asana**, przejdź toohello **zespołów** sekcji na powitania lewego panelu. Kliknij przycisk hello oraz przycisk Zaloguj. 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. Wpisz wiadomość hello e-mail britta.simon@contoso.com w hello pola tekstowego, a następnie wybierz **zaprosić**.

3. Kliknij przycisk **wysłać zaproszenie**. Witaj nowy użytkownik otrzyma wiadomość e-mail na swoje konto e-mail. Użytkownik należy toocreate a sprawdzania hello konta.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAsana.

![Przypisanie roli użytkownika hello][200]

**tooassign tooAsana Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Asana**.

    ![łącze Asana Hello na liście aplikacji hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest programu Azure AD rejestracji jednokrotnej.

Przejdź na stronę logowania tooAsana. W polu tekstowym Adres E-mail hello, Wstaw adres e-mail hello britta.simon@contoso.com. Pozostaw pole tekstowe hasła hello w puste, a następnie kliknij przycisk **dziennika w**. Będzie przekierowany tooAzure AD strony logowania. Ukończ poświadczeń usługi Azure AD. Teraz użytkownik jest zalogowany na Asana.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
