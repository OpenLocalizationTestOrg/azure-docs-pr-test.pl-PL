---
title: 'Samouczek: Integracji Azure Active Directory z Voyance | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a>Samouczek: Integracji Azure Active Directory z Voyance

Z tego samouczka, dowiesz się, jak toointegrate Voyance w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Voyance zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooVoyance
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooVoyance (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Voyance należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Voyance logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Voyance z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-voyance-from-hello-gallery"></a>Dodawanie Voyance z galerii hello
tooconfigure hello integracji Voyance do usługi Azure AD, należy tooadd Voyance z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Voyance z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **Voyance**, wybierz pozycję **Voyance** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Voyance hello listy wyników](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Voyance w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Voyance jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Voyance musi toobe ustanowione.

W Voyance, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Voyance, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Voyance](#create-a-voyance-test-user)**  -toohave odpowiednikiem Simona Britta w Voyance, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Voyance.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Voyance, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Voyance** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. Na powitania **Voyance domeny i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:

    ![Adresy URL i domeny Voyance pojedynczy informacje logowania dla dostawców tożsamości](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.nyansa.com`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.nyansa.com/saml/create/`

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonywać powitania po kroku, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:

    ![Adresy URL i domeny Voyance pojedynczy informacje logowania dla dostawcy](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.nyansa.com/`
     
    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta Voyance](mailto:support@nyansa.com) tooget tych wartości. 

5. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. Na powitania **konfiguracji Voyance** kliknij **skonfigurować Voyance** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfiguracja Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour Voyance dzierżawy z uprawnieniami administratora.

9. Przejdź toohello prawym górnym rogu paska nawigacyjnego hello i kliknij pozycję hello listy rozwijanej informacją "**University xyz**".
    
    ![Konfigurowanie rejestracji jednokrotnej w aplikacji po stronie xyz University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. Kliknij przycisk "**ustawienia administratora**".

    ![Konfigurowanie rejestracji jednokrotnej ustawieniami aplikacji po stronie administratora](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. Kliknij przycisk "**dostępu użytkownika**" kartę.

    ![Konfigurowanie rejestracji jednokrotnej na dostęp do aplikacji po stronie użytkownika](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. Kliknij przycisk hello "**wyłączeniu logowania jednokrotnego**" przycisk tooconfigure usługi Azure AD jako dostawca tożsamości przy użyciu SAML 2.0.

    ![Konfigurowanie jednego logowania w aplikacji po stronie rejestracji Jednokrotnej jest wyłączony przycisk](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. Przejdź za**SAML v2** sekcji i wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej w aplikacji po stronie SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    a. Wybierz **włączone**.
    
    b. Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z hello portalu Azure do hello **adres URL logowania IdP** pole tekstowe.

    c. Otwórz z pobranego certyfikatu szyfrowania Base64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **IdP Cert** pola tekstowego.
    
    d. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-voyance-test-user"></a>Tworzenie użytkownika testowego Voyance

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Voyance. Voyance obsługę w czasie, który jest domyślnie włączone. Nie ma elementu akcji można w tej sekcji. Nowy użytkownik jest tworzona podczas próby tooaccess Voyance, jeśli go jeszcze nie istnieje.

>[!NOTE]
>Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact [zespołem pomocy technicznej Voyance](maiLto:support@nyansa.com).

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooVoyance.

![Przypisanie roli użytkownika hello][200]

**tooassign tooVoyance Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Voyance**.

    ![łącze Voyance Hello na liście aplikacji hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Voyance hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Voyance aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

