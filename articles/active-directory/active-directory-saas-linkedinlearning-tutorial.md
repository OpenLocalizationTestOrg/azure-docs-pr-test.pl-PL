---
title: 'Samouczek: Integracji Azure Active Directory z LinkedIn Learning | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i uczenie się LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a>Samouczek: Integracji Azure Active Directory z LinkedIn Learning

Z tego samouczka, dowiesz się, jak toointegrate LinkedIn Learning z usługą Azure Active Directory (Azure AD).

Integrowanie LinkedIn Learning z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLinkedIn nauki
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLinkedIn Learning (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD przy użyciu LinkedIn Learning należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- LinkedIn Learning jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie LinkedIn Learning z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-linkedin-learning-from-hello-gallery"></a>Dodawanie LinkedIn Learning z galerii hello
tooconfigure hello integracji LinkedIn Learning z usługą Azure AD, należy tooadd LinkedIn Learning z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Learning LinkedIn z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **LinkedIn Learning**. Z poziomu panelu wyników, kliknij przycisk **LinkedIn Learning** tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD logowania jednokrotnego przy użyciu Learning LinkedIn w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w uczeniu LinkedIn jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w uczeniu LinkedIn musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w uczeniu LinkedIn.

tooconfigure i testowych usługi Azure AD logowania jednokrotnego przy użyciu LinkedIn Learning, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego LinkedIn Learning](#creating-a-linkedin-learning-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji LinkedIn Learning.

**tooconfigure usługi Azure AD logowania jednokrotnego przy użyciu LinkedIn Learning wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **LinkedIn Learning** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour LinkedIn Learning dzierżawy z uprawnieniami administratora.

4. W **Centrum konta**, kliknij przycisk **ustawienia globalne** w obszarze **ustawienia**. Zaznacz również **Learning - domyślne** z listy rozwijanej hello.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. Kliknij przycisk **lub kliknij tutaj tooload i skopiuj poszczególnych pól formularza hello** i skopiuj **identyfikator jednostki** i **adresu Url potwierdzenia konsumenta dostępu (ACS)**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. W portalu Azure w obszarze **domeny Learning LinkedIn i adres URL**, wykonaj następujące kroki, jeśli chcesz, aby tooconfigure logowania jednokrotnego hello w **inicjowane IdP** tryb

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    a. W hello **identyfikator** pole tekstowe, wprowadź hello **identyfikator jednostki** skopiowany z portalu LinkedIn 

    b. W hello **adres URL odpowiedzi** pole tekstowe, wprowadź hello **potwierdzenia konsumenta dostępu (ACS) adres Url** skopiowany z portalu LinkedIn

7. Jeśli chcesz, aby tooconfigure logowania jednokrotnego w **inicjowane SP**, następnie kliknij opcję Ustawienia Pokaż zaawansowane adres URL w sekcji konfiguracji hello i skonfigurować hello adres URL logowania z hello następującego wzorca:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. Aplikacja LinkedIn Learning oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji. powitania po zrzut ekranu przedstawia przykład tego. Witaj wartość domyślną **identyfikator użytkownika** jest **user.userprincipalname** , ale ten toobe zamapowana adres e-mail użytkownika hello oczekuje LinkedIn Learning. W przypadku którego można użyć **user.mail** atrybutu z listy hello lub użyj wartości atrybutu odpowiednie hello zgodnie z konfiguracją organizacji. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustaw hello atrybuty. Hello użytkownik powinien tooadd oświadczeń cztery o nazwie **e-mail**, **działu**, **imię**, i **nazwisko** i wartość hello jest zamapowana z toobe **user.mail**, **user.department**, **user.givenname**, i **user.surname** odpowiednio

    | Nazwa atrybutu | Wartość atrybutu |
    | --- | --- |
    | Adres e-mail| User.mail |    
    | Dział| User.Department |
    | Imię| User.givenName |
    | nazwisko| User.surname |
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    a. Kliknij przycisk **Dodawanie atrybutu** tooopen hello atrybutu w oknie dialogowym.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    b. W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.
    
    c. Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.
    
    d. Kliknij przycisk **Ok**

10. Wykonaj następujące kroki na powitania hello **nazwa** — atrybut

    a. Polecenie hello atrybutu tooopen hello **atrybutu Edytuj** okna.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    b. Usuń wartość adresu URL hello z hello **przestrzeni nazw**.
    
    c. Kliknij przycisk **Ok** toosave hello ustawienie.

11. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. Kliknij pozycję **Zapisz**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. Przejdź za**ustawienia administratora LinkedIn** sekcji. Przekaż hello pliku XML, który został pobrany z hello portalu Azure, klikając opcję pliku XML, Przekaż hello.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. Kliknij przycisk **na** tooenable logowania jednokrotnego. Zmiany stanu rejestracji Jednokrotnej z **niepołączone** zbyt**połączony**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**. 

### <a name="creating-a-linkedin-learning-test-user"></a>Tworzenie użytkownika testowego LinkedIn Learning

Obsługuje połączonych aplikacji Learning. Tylko na czas Inicjowanie obsługi użytkowników, a następnie uwierzytelniania użytkowników są tworzone automatycznie w aplikacji hello. Na stronie Ustawienia administratora hello na przełączniku portalu hello przerzucania LinkedIn Learning hello **automatycznie przypisywać licencje** tooactive tooenable tylko w czasie inicjowania obsługi administracyjnej i to również przypisać licencję użytkownika toohello.
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji, Włącz toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLinkedIn Learning.

![Przypisz użytkownika][200] 

**tooassign tooLinkedIn Simona Britta uczenia, wykonaj następujące kroki hello:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **LinkedIn Learning**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka LinkedIn Learning hello w hello Panel dostępu, należy pobrać hello Azure logowania jednokrotnego strony i na po pomyślnym logowania, należy pobrać do aplikacji LinkedIn Learning.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png