---
title: "Samouczek: Azure Active Directory integrację ze IBM Kenexa ankiety | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i IBM Kenexa ankiety przedsiębiorstwa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a>Samouczek: Azure Active Directory integrację ze IBM Kenexa ankiety

Z tego samouczka, dowiesz się, jak toointegrate IBM Kenexa ankiety przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).

Integrowanie IBM Kenexa ankiety przedsiębiorstwa z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooIBM Kenexa ankiety przedsiębiorstwa.
- Tooautomatically użytkowników logowania tooIBM Kenexa ankiety przedsiębiorstwa można włączyć za pomocą rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji: hello portalu Azure.

Jeśli chcesz tooknow więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z IBM Kenexa ankiety Enterprise należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Włączone IBM Kenexa ankiety Enterprise SSO subskrypcji

> [!NOTE]
> Podczas testowania czynności hello w tym samouczku, firma Microsoft zaleca, nie używaj do środowiska produkcyjnego.

kroki hello tootest w tym samouczku, wykonaj te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować logowania jednokrotnego programu Azure AD w środowisku testowym. Scenariusz Hello opisane w samouczku hello składa się z dwóch głównych elementów:

* Dodawanie IBM Kenexa ankiety przedsiębiorstwa z galerii hello
* Konfigurowanie i testowania logowania jednokrotnego programu Azure AD

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a>Dodaj IBM Kenexa ankiety przedsiębiorstwa z galerii hello
tooconfigure hello integracji IBM Kenexa ankiety przedsiębiorstwa w usłudze Azure AD, Dodaj IBM Kenexa ankiety przedsiębiorstwa z hello galerii tooyour listę zarządzanych aplikacji SaaS.

tooadd IBM Kenexa ankiety przedsiębiorstwa z galerii hello hello następujące:

1. W hello [portalu Azure](https://portal.azure.com), w lewym okienku hello, kliknij przycisk hello **usługi Azure Active Directory** przycisku. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd aplikacji, kliknij przycisk hello **nowej aplikacji** przycisku.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **IBM Kenexa ankiety Enterprise**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. Hello listy wyników, wybierz **IBM Kenexa ankiety Enterprise**, a następnie kliknij przycisk hello **Dodaj** przycisk aplikacji hello tooadd.

    ![IBM Kenexa ankiety Enterprise hello listy wyników](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji Konfiguracja i testowanie logowania jednokrotnego AD Azure z przedsiębiorstwem ankiety Kenexa IBM oparte na koncie użytkownika testu o nazwie "Britta Simona".

Aby toowork logowania jednokrotnego usługi Azure AD musi tooidentify hello IBM Kenexa ankiety Enterprise użytkownika odpowiednikiem w usłudze Azure AD. Innymi słowy usługi Azure AD ustanowić relację łącza między użytkownika usługi Azure AD i powiązanych użytkowników w przedsiębiorstwie ankiety Kenexa IBM.

tooestablish hello łącze relację, przypisać wartość hello hello **nazwy użytkownika** w przedsiębiorstwie ankiety Kenexa IBM jako wartość hello hello **Username** w usłudze Azure AD.

tooconfigure i Azure AD SSO z IBM Kenexa ankiety przedsiębiorstwa, pełny test hello bloków konstrukcyjnych w hello w dwóch następnych sekcjach.

### <a name="configure-azure-ad-sso"></a>Konfigurowanie usługi Azure AD logowania jednokrotnego.

W tej sekcji włączenia funkcji logowania jednokrotnego usługi Azure AD w hello portalu Azure i skonfiguruj logowania jednokrotnego w aplikacji IBM Kenexa ankiety przedsiębiorstwa, wykonując następujące hello:

1. W portalu Azure na powitania hello **IBM Kenexa ankiety Enterprise** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![IBM Kenexa ankiety Enterprise Konfigurowanie logowania jednokrotnego łącza][4]

2. W hello **logowanie jednokrotne** okno dialogowe, w hello **tryb** wybierz opcję **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. W hello **IBM Kenexa ankiety Enterprise domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![IBM Kenexa ankiety Enterprise domeny i adres URL z jednym informacje logowania jednokrotnego](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL z hello następującego wzorca:`https://surveys.kenexa.com/<companycode>`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL z hello następującego wzorca:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    > [!NOTE] 
    > Witaj poprzedniej wartości nie są prawdziwe. Można aktualizować hello rzeczywisty identyfikator i adres URL odpowiedzi. tooobtain hello wartości rzeczywistych, skontaktuj się z pomocą hello [zespołem pomocy technicznej Enterprise ankiety Kenexa IBM](https://www.ibm.com/support/home/?lnk=fcw).

4. W obszarze **certyfikat podpisywania SAML**, kliknij przycisk **certyfikatu (Base64)**, a następnie zapisz hello certyfikatu pliku tooyour komputera.

    ![Witaj link do pobierania certyfikatu (Base64)](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    Hello aplikacja całościowa ankiety Kenexa IBM oczekuje potwierdzeń zabezpieczeń potwierdzenia Markup Language (SAML) hello tooreceive w określonym formacie, który wymaga możesz tooadd atrybutu niestandardowego mapowania toohello konfiguracji z atrybutów tokenu SAML. Witaj wartość hello oświadczenia identyfikatora użytkownika w odpowiedzi hello musi odpowiadać hello identyfikator logowania jednokrotnego, który jest skonfigurowany w systemie Kenexa hello. toomap hello identyfikator odpowiedniego użytkownika w organizacji jako SSO Internet Datagram Protocol (IDP), Praca z hello [zespołem pomocy technicznej Enterprise ankiety Kenexa IBM](https://www.ibm.com/support/home/?lnk=fcw). 

    Domyślnie usługi Azure AD Ustawia identyfikator użytkownika hello jako wartość głównej nazwy (UPN) użytkownika hello. Można zmienić tę wartość na powitania **atrybutu** karcie, jak pokazano w hello następującego zrzutu ekranu. Integracja Hello działa tylko po zakończeniu hello mapowania poprawnie.
    
    ![okno dialogowe Hello atrybutów użytkownika](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. Kliknij pozycję **Zapisz**.

    ![Witaj skonfigurować logowanie jednokrotne przycisk zapisywania](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. tooopen hello **Konfigurowanie logowania jednokrotnego** okna, w obszarze **konfiguracja dla przedsiębiorstw ankiety Kenexa IBM**, kliknij przycisk **skonfigurować IBM Kenexa ankiety Enterprise**. 
 
    ![łącze skonfigurować IBM Kenexa ankiety Enterprise Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. Kopiuj hello **Sign-Out adres URL**, **SAML identyfikator jednostki**, i **SAML pojedynczy znak na adres URL usługi** wartości z hello **krótki przewodnik** sekcji.

8. W hello **Konfigurowanie logowania jednokrotnego** okna, w obszarze **krótkimi opisami**, hello kopiowania **Sign-Out adres URL**, **identyfikator jednostki SAML**, i  **SAML pojedynczy znak na adres URL usługi** wartości.

9. tooconfigure logowania jednokrotnego na powitania **IBM Kenexa ankiety Enterprise** po stronie, Wyślij hello pobrane **certyfikatu (Base64)**, **Sign-Out URL**, **identyfikator jednostki SAML**, i **SAML pojedynczy znak na adres URL usługi** wartości toohello [zespołem pomocy technicznej Enterprise ankiety Kenexa IBM](https://www.ibm.com/support/home/?lnk=fcw).

> [!TIP]
> Może się odwoływać tooa zwięzły wersji tych instrukcji w hello [portalu Azure](https://portal.azure.com) podczas konfigurowania aplikacji hello. Po dodaniu aplikacji hello z hello **usługi Active Directory** > **aplikacje dla przedsiębiorstw** po prostu kliknij hello **logowanie jednokrotne** karcie, a następnie przejść Witaj osadzonych dokumentacji za pośrednictwem hello **konfiguracji** sekcji na końcu hello. toolearn więcej informacji na temat hello osadzonych dokumentacji funkcji, zobacz [usługi Azure AD osadzonych dokumentacji](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
W tej sekcji możesz tworzyć użytkownika testowego Simona Britta w hello portalu Azure, wykonując następujące hello:

![Tworzenie użytkownika testowego usługi Azure AD][100]

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a>Tworzenie użytkownika testowego IBM Kenexa ankiety Enterprise

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w przedsiębiorstwie ankiety Kenexa IBM. 

toocreate użytkowników w hello systemu IBM Kenexa ankiety przedsiębiorstwa i mapy hello identyfikator logowania jednokrotnego dla nich, możesz pracować z hello [zespołem pomocy technicznej Enterprise ankiety Kenexa IBM](https://www.ibm.com/support/home/?lnk=fcw). Ta wartość Identyfikatora logowania jednokrotnego również musi być zamapowany toohello wartość identyfikatora użytkownika z usługi Azure AD. Można zmienić to ustawienie domyślne na powitania **atrybutu** kartę.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć użytkownika toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooIBM Kenexa ankiety Enterprise.

![Przypisanie roli użytkownika hello][200] 

tooassign użytkownika tooIBM Simona Britta Kenexa Enterprise ankiety, hello następujące:

1. Hello portalu Azure, otwórz hello **aplikacji** wyświetlić, przejdź toohello **katalogu** widok, wybierz opcję **aplikacje dla przedsiębiorstw**, a następnie kliknij przycisk **wszystkie aplikacje**.

    ![Witaj, "Aplikacje przedsiębiorstwa" i "Wszystkie aplikacje" łącza][201] 

2. W hello **aplikacji** listy, wybierz **IBM Kenexa ankiety Enterprise**.

    ![łącze IBM Kenexa ankiety Enterprise Hello na liście aplikacji hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. W okienku po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. Kliknij przycisk hello **Dodaj** przycisk, a następnie w hello **Dodaj przydziału** okienku wybierz **użytkowników i grup**.

    ![Okienko Dodaj przypisania Hello][203]

5. W hello **użytkowników i grup** okno dialogowe, w hello **użytkowników** listy, wybierz **Simona Britta**.

6. W hello **użytkowników i grup** okna dialogowego kliknij hello **wybierz** przycisku.

7. W hello **Dodaj przydziału** okna dialogowego kliknij hello **przypisać** przycisku.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji możesz przetestować konfigurację programu Azure AD z logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello **IBM Kenexa ankiety Enterprise** kafelka w hello Panel dostępu, powinien być automatycznie zalogowano tooyour aplikacja całościowa ankiety Kenexa IBM.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
