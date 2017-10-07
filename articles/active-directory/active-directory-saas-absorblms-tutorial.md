---
title: "Samouczek: Integracji Azure Active Directory z przyjęcia LMS | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i przyjęcia LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a>Samouczek: Integracji Azure Active Directory z przyjęcia LMS

Z tego samouczka, dowiesz się, jak toointegrate Absorb LMS w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD przyjęcia LMS zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAbsorb LMS
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAbsorb LMS (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz. [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z przyjęcia LMS należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Przyjęcia LMS jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie przyjęcia LMS z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-absorb-lms-from-hello-gallery"></a>Dodawanie przyjęcia LMS z galerii hello
tooconfigure hello integracji LMS przyjęcia w tooAzure AD, należy tooadd Absorb LMS z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Absorb LMS z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **przyjęcia LMS**, wybierz pozycję **przyjęcia LMS** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Przyjęcia LMS hello listy wyników](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przyjęcia LMS oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w przyjęcia LMS jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w przyjęcia LMS musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w LMS przyjęcia.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z przyjęcia LMS, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego przyjęcia LMS](#create-an-absorb-lms-test-user)**  -toohave odpowiednikiem Simona Britta w przyjęcia LMS, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji przyjęcia LMS.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z przyjęcia LMS, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **przyjęcia LMS** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. Na powitania **adresy URL i przyjęcia domeny LMS** sekcji, wykonaj następujące kroki hello:

    ![Przyjęcia LMS domeny i adres URL pojedynczego logowania jednokrotnego informacji](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.myabsorb.com/Account/SAML`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.myabsorb.com/Account/SAML`
     
    > [!NOTE] 
    > Wartości te nie są hello prawdziwe. Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości. Skontaktuj się z [zespołem pomocy technicznej klienta LMS przyjęcia](https://www.absorblms.com/support) tooget tych wartości. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. Na powitania **przyjęcia konfiguracji LMS** kliknij **skonfigurować LMS przyjęcia** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Przyjęcia LMS konfiguracji](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy przyjęcia LMS tooyour jako administrator.

9. Kliknij przycisk hello **ikonę konta** na powitania interfejsu administracyjnego. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/1.png)

10. Kliknij przycisk **ustawienia portalu**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. Kliknij przycisk hello **użytkowników** kartę.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/3.png)

12. Wykonaj następujące kroki tooaccess hello rejestracji jednokrotnej pola konfiguracji hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/4.png)

    a. Wybierz odpowiednie hello **tryb**.

    b. Otwórz hello certyfikatu, który został pobrany z portalu Azure w programie Notatnik hello Usuń hello **---BEGIN CERTIFICATE---** i **---END CERTIFICATE---** tag, a następnie wklej hello pozostała zawartość Witaj **klucza** pola tekstowego.
    
    c. W hello **właściwość identyfikatora**, wybierz hello odpowiedni atrybut, który został skonfigurowany jako hello identyfikatora użytkownika w hello Azure AD (na przykład, jeśli wybrano hello userprinciplename w usłudze Azure AD, a następnie zaznaczony tutaj nazwę użytkownika.)

    d. W hello **adres URL logowania**, Wklej hello **"SAML pojedynczy znak na adres URL usługi"** wartość została skopiowana z hello **Konfigurowanie logowania jednokrotnego** okna hello portalu Azure.

    e. W hello **adresu URL wylogowania**, Wklej hello **"Adres URL Sign-Out"** wartość została skopiowana z hello **Konfigurowanie logowania jednokrotnego** okna hello portalu Azure.

13. Włącz **"Zezwalaj tylko na logowanie SSO"**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/5.png)

14. Kliknij przycisk **"Zapisz".**

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.

### <a name="create-an-absorb-lms-test-user"></a>Tworzenie użytkownika testowego przyjęcia LMS

toolog użytkowników tooenable usługi Azure AD w tooAbsorb LMS, muszą mieć przydzielone w tooAbsorb LMS.  
W przypadku przyjęcia LMS inicjowania obsługi administracyjnej jest zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour przyjęcia LMS witryny firmy jako administrator.

2. Kliknij przycisk **użytkowników** kartę.

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. Kliknij przycisk **użytkowników** w obszarze hello **użytkowników** kartę.

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  Wybierz **użytkownika** z **Dodaj nowy** listy rozwijanej.

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. Na powitania **Dodaj użytkownika** wykonaj hello następujące kroki:

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/user.png)

    a. W hello **imię** pole tekstowe, typ hello imię jak Britta.

    b. W hello **nazwisko** pole tekstowe, typ hello nazwisko jak Simona.
    
    c. W hello **Username** tekstowym, wpisz nazwę użytkownika hello jak Simona Britta.

    d. W hello **hasło** tekstowym, wpisz hasło hello Simona Britta.

    e. W hello **Potwierdź hasło** pole tekstowe, hello typu tego samego hasła.
    
    f. Należy go jako **ACTIVE**.   

6. Kliknij przycisk **"Zapisz".**
 
### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAbsorb LMS.

![Przypisanie roli użytkownika hello][200]

**tooassign tooAbsorb Simona Britta LMS, wykonaj następujące kroki hello:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **przyjęcia LMS**.

    ![łącze przyjęcia LMS Hello na liście aplikacji hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Kliknij przycisk hello przyjęcia LMS kafelka w hello panelu dostępu otrzymasz automatycznie zalogowane tooyour przyjęcia LMS aplikacji. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

