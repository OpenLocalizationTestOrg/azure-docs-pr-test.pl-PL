---
title: 'Samouczek: Integracji Azure Active Directory z Boomi | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a>Samouczek: Integracji Azure Active Directory z Boomi

Z tego samouczka, dowiesz się, jak toointegrate Boomi w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Boomi zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooBoomi
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBoomi (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Boomi należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Boomi logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Boomi z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-boomi-from-hello-gallery"></a>Dodawanie Boomi z galerii hello
tooconfigure hello integracji Boomi do usługi Azure AD, należy tooadd Boomi z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Boomi z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Boomi**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. W panelu wyników hello zaznacz **Boomi**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Boomi w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Boomi jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Boomi musi toobe ustanowione.

W Boomi, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Boomi, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Boomi](#creating-a-boomi-test-user)**  -toohave odpowiednikiem Simona Britta w Boomi, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Boomi.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Boomi, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Boomi** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. Na powitania **Boomi domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://platform.boomi.com/sso/<accountname>/saml`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://platform.boomi.com/sso/<accountname>/saml`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości. Skontaktuj się z [zespołem pomocy technicznej Boomi](https://boomi.com/company/contact/) tooget tych wartości.

4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. Aplikacja Boomi oczekuje potwierdzenia SAML hello w określonym formacie. Skonfiguruj powitania po oświadczeń dla tej aplikacji. Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji. powitania po zrzut ekranu przedstawia przykład tego.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, dla każdego wiersza przedstawione w poniższej tabeli hello wykonaj hello następujące kroki:

    | Nazwa atrybutu | Wartość atrybutu |
    | -------------- | --------------- |
    | FEDERATION_ID | User.mail |
    
    a. Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    b. W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.
    
    c. Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.
    
    d. Kliknij przycisk **OK**.

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. Na powitania **konfiguracji Boomi** kliknij **skonfigurować Boomi** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Boomi jako administrator. 

9. Przejdź za**nazwa firmy** i przejść za**Konfigurowanie**.

10. Kliknij przycisk hello **opcje logowania jednokrotnego** karcie i wykonaj następujące czynności.

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    a. Sprawdź **Włącz SAML logowania jednokrotnego** wyboru.

    b. Kliknij przycisk **importu** tooupload hello pobrać certyfikatu z usługi Azure AD za**certyfikat dostawcy tożsamości**.
    
    c. W hello **adresu URL logowania do dostawcy tożsamości** pole tekstowe, umieść wartość hello **SAML pojedynczy znak na adres URL usługi** z okna konfiguracji aplikacji usługi Azure AD.

    d. Jako **federacyjnego identyfikator lokalizacji**, wybierz pozycję **identyfikator federacyjnej jest w elemencie atrybutu FEDERATION_ID** przycisk radiowy. 

    e. Kliknij przycisk **zapisać** przycisku.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-boomi-test-user"></a>Tworzenie użytkownika testowego Boomi

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w tooBoomi muszą mieć przydzielone do Boomi. W przypadku hello Boomi Inicjowanie obsługi to zadanie ręczne.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision konta użytkownika, należy wykonać hello następujące kroki:

1. Zaloguj się za tooyour Boomi witryny firmy jako administrator.

2. Po zalogowaniu Przejdź zbyt**Zarządzanie użytkownikami** i przejść za**użytkowników**.

    ![Użytkownicy](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "użytkowników")

3. Kliknij przycisk  **+**  ikony, jak i hello **ról użytkownika Add/Zachowaj** zostanie otwarte okno dialogowe.

    ![Użytkownicy](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "użytkowników")

    ![Użytkownicy](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "użytkowników")

    a. W hello **adres e-mail użytkownika** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak BrittaSimon@contoso.com.
    
    b. W hello **imię** pole tekstowe, typ hello imię użytkownika, takich jak Britta.

    c. W hello **nazwisko** pole tekstowe, typ hello nazwisko użytkownika, takich jak Simona.
    
    d. Wprowadź nazwę użytkownika hello **identyfikator federacyjnej**. Każdy użytkownik musi mieć identyfikator federacyjnego, który unikatowo identyfikuje użytkownika hello w ramach konta hello.
    
    e. Przypisz hello **użytkownika standardowego** użytkownika toohello roli. Nie należy przypisywać hello rolę administratora, ponieważ który spowodowałoby to nadanie mu dostęp do atmosfery, a także dostępu rejestracji jednokrotnej.
    
    f. Kliknij przycisk **OK**.
    
    > [!NOTE]
    > Hello użytkownik nie otrzyma wiadomość e-mail z powiadomieniem powitalnej zawierająca hasło, które mogą być toolog używanych w toohello AtomSphere konta, ponieważ jego hasło jest zarządzane przez dostawcę tożsamości hello. Możesz użyć innych Boomi użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Boomi tooprovision kont użytkowników usługi AAD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBoomi.

![Przypisz użytkownika][200] 

**tooassign tooBoomi Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Boomi**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Boomi hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Boomi aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

