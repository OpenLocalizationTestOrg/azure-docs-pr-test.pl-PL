---
title: 'Samouczek: Integracji Azure Active Directory z wyszukiwania LinkedIn | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i LinkedIn wyszukiwania."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a>Samouczek: Integracji Azure Active Directory z LinkedIn wyszukiwania

Z tego samouczka, dowiesz się, jak toointegrate LinkedIn wyszukiwania w usłudze Azure Active Directory (Azure AD).

Integrowanie wyszukiwania LinkedIn z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLinkedIn wyszukiwania
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLinkedIn wyszukiwania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z LinkedIn wyszukiwania należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Wyszukiwanie LinkedIn jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie wyszukiwania LinkedIn z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-linkedin-lookup-from-hello-gallery"></a>Dodawanie wyszukiwania LinkedIn z galerii hello
tooconfigure hello integracji LinkedIn wyszukiwania w usłudze Azure Active Directory, należy tooadd LinkedIn wyszukiwania z listy tooyour galerii hello zarządzanych aplikacji SaaS.

**tooadd wyszukiwania LinkedIn z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **nowej aplikacji** przycisk na powitania górnej części okna dialogowego hello tooadd nowej aplikacji.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **wyszukiwania LinkedIn**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. W panelu wyników hello, wybierz **wyszukiwania LinkedIn**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z LinkedIn wyszukiwania w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello odnośnika LinkedIn jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w wyszukiwaniu LinkedIn musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** odnośnika LinkedIn.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z LinkedIn wyszukiwania, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego wyszukiwania LinkedIn](#creating-an-linkedin-lookup-test-user)**  -toohave odpowiednikiem Simona Britta odnośnika LinkedIn, który jest odpowiednikiem połączonych toohello usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji wyszukiwania LinkedIn.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z LinkedIn wyszukiwanie, należy wykonać hello następujące kroki:**

1. W portalu Azure na powitania hello **wyszukiwania LinkedIn** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, w **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour **wyszukiwania LinkedIn** witryny sieci Web jako administrator.

4. W **Centrum konta**, kliknij przycisk **ustawienia globalne** w obszarze **ustawienia**. Zaznacz również **wyszukiwania** z listy rozwijanej hello.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. Kliknij przycisk **lub kliknij tutaj tooload i skopiuj poszczególnych pól formularza hello** i skopiuj **identyfikator jednostki** i **adresu Url potwierdzenia konsumenta dostępu (ACS)**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. W portalu Azure w obszarze **domeny wyszukiwania LinkedIn i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    a. W hello **identyfikator** pole tekstowe, wprowadź hello **identyfikator jednostki** skopiowany z portalu LinkedIn 

    b. W hello **adres URL odpowiedzi** pole tekstowe, wprowadź hello **potwierdzenia konsumenta dostępu (ACS) adres Url** skopiowany z portalu LinkedIn

7. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`
     
    > [!NOTE] 
    > To nie jest rzeczywistą wartość. Użytkownik Hello ma tooupdate tych wartości za pomocą hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta wyszukiwania LinkedIn](https://business.LinkedIn.com/lookup) tooget tej wartości.

8. Twoje **wyszukiwania LinkedIn** aplikacji oczekuje potwierdzenia SAML hello w określonym formacie. Użytkownik Hello ma konfiguracja atrybutów tokenu SAML mapowania toohello tooadd atrybutu niestandardowego. powitania po zrzut ekranu przedstawia przykład. Witaj wartość domyślną **identyfikator użytkownika** jest **user.userprincipalname** , ale ta toobe zamapowana adres e-mail użytkownika hello oczekuje LinkedIn wyszukiwania. Można użyć **user.mail** atrybutu z listy hello lub użyj wartości atrybutu odpowiednie hello zgodnie z konfiguracją organizacji. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustaw hello atrybuty. Hello użytkownik powinien tooadd oświadczeń cztery o nazwie **e-mail**, **działu**, **imię**, i **nazwisko** i wartość hello jest zamapowana z toobe **user.mail**, **user.department**, **user.givenname**, i **user.surname** odpowiednio

    | Nazwa atrybutu | Wartość atrybutu |
    | --- | --- |
    | Adres e-mail| User.mail |    
    | Dział| User.Department |
    | Imię| User.givenName |
    | nazwisko| User.surname |

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    a. Kliknij przycisk **Dodawanie atrybutu** tooopen hello **Dodawanie atrybutu** okna dialogowego.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    b. W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.
    
    c. Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.
    
    d. Kliknij przycisk **Ok**

10. Wykonaj następujące kroki na powitania hello **nazwa** — atrybut

    a. Polecenie hello atrybutu tooopen hello **atrybutu Edytuj** okna.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    b. Usuń wartość adresu URL hello z hello **przestrzeni nazw**.
    
    c. Kliknij przycisk **Ok** toosave hello ustawienie.

10. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. Przejdź za**ustawienia administratora LinkedIn** sekcji. Plik XML hello przekazywania pobranego z hello portalu Azure, klikając hello **pliku XML, Przekaż** opcji.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. Kliknij przycisk **na** tooenable logowania jednokrotnego. Zmiany stanu rejestracji Jednokrotnej z **niepołączone** zbyt**połączony**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. Kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **Simona Britta**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z Simona Britta.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-linkedin-lookup-test-user"></a>Tworzenie użytkownika testowego LinkedIn wyszukiwania

Połączonej aplikacji wyszukiwania obsługuje tylko w czasie (JIT) Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji hello. Aktywuj **automatycznie przypisać licencje** tooassign toohello licencji użytkownika.
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLinkedIn wyszukiwania.

![Przypisz użytkownika][200] 

**tooassign tooLinkedIn Simona Britta wyszukiwanie, należy wykonać hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **wyszukiwania LinkedIn**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.

    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello wyszukiwania LinkedIn kafelka w hello panelu dostępu należy strony przekierowanego tooOrganizational gdzie masz tooprovide informacje osobowe konta LinkedIn. Łączy konto osobiste konta firmowego LinkedIn. 

Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

