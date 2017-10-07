---
title: "Samouczek: Integrację usługi Azure Active Directory ze ScaleX | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a>Samouczek: Integrację usługi Azure Active Directory ze ScaleX

Z tego samouczka, dowiesz się, jak toointegrate ScaleX przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).

Integrowanie ScaleX organizacji z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooScaleX przedsiębiorstwa
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooScaleX przedsiębiorstwa (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz. Co to jest dostęp do aplikacji i logowanie jednokrotne z [usługi Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z ScaleX Enterprise należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- ScaleX Enterprise jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie ScaleX przedsiębiorstwa z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-scalex-enterprise-from-hello-gallery"></a>Dodawanie ScaleX przedsiębiorstwa z galerii hello
tooconfigure hello integracji przedsiębiorstwa ScaleX w tooAzure AD, należy tooadd ScaleX przedsiębiorstwa z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd ScaleX przedsiębiorstwa z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **ScaleX Enterprise**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. W panelu wyników hello, wybierz **ScaleX Enterprise**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z ScaleX Enterprise oparte na użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w przedsiębiorstwie ScaleX jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w przedsiębiorstwie ScaleX musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w przedsiębiorstwie ScaleX.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ScaleX przedsiębiorstwa, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave odpowiednikiem Simona Britta w przedsiębiorstwie ScaleX, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji przedsiębiorstwa ScaleX.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z ScaleX przedsiębiorstwa, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **ScaleX Enterprise** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. Na powitania **ScaleX domeny przedsiębiorstwa i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    a. W hello **identyfikator** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://platform.rescale.com/saml2/<company id>/`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://platform.rescale.com/saml2/<company id>/acs/`

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    W hello **adres URL logowania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://platform.rescale.com/saml2/<company id>/sso/`
     
    > [!NOTE] 
    > Nie są hello wartości rzeczywistych. Z hello rzeczywisty identyfikator, adres URL odpowiedzi lub adres URL logowania, należy zaktualizować te wartości. Skontaktuj się z [zespołem pomocy technicznej klienta Enterprise ScaleX](http://info.rescale.com/contact_sales) tooget tych wartości. 

5. Aplikacja ScaleX oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz toomodify atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji. Kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** hello tooopen wyboru niestandardowych atrybutów ustawienia.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    a. Kliknij prawym przyciskiem myszy atrybut hello **nazwa** i kliknij przycisk Usuń.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    b. Kliknij przycisk **emailaddress** okno edycji atrybucie hello tooopen atrybutu. Zmień wartość z **user.mail** za**user.userprincipalname** i kliknij przycisk Ok.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. Na powitania **konfiguracja dla przedsiębiorstw ScaleX** , kliknij przycisk **skonfigurować ScaleX Enterprise** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML identyfikator jednostki** i **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. tooconfigure rejestracji jednokrotnej w **ScaleX Enterprise** strona, logowania toohello ScaleX Enterprise witryny sieci Web firmy jako administrator.

9. Kliknij menu hello w górnym hello prawo i wybierz **administracji Contoso**.

    > [!NOTE] 
    > Firma Contoso jest tylko przykładowe. Powinno to być rzeczywista nazwa firmy. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. Wybierz **integracji** z górnego menu hello i wybierz **rejestracji jednokrotnej**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. Wypełnij formularz hello w następujący sposób:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    a. Wybierz **"Utwórz każdy użytkownik, który może uwierzytelniać z logowania jednokrotnego."**

    b. **Saml dostawcy usług**: wkleić wartość hello ***urn: oasis: nazwy: tc: SAML:2.0:nameid-format: stałe***

    c. **Nazwa dostawcy tożsamości pola wiadomości e-mail w odpowiedzi ACS**: wkleić hello wartość`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

    d. **Identyfikator jednostki EntityDescriptor dostawcy tożsamości:** hello Wklej **identyfikator jednostki SAML** kopiuje wartość hello portalu Azure.

    e. **Adres URL SingleSignOnService dostawcy tożsamości:** hello Wklej **SAML pojedynczy znak na adres URL usługi** z hello portalu Azure.

    f. **Certyfikat publiczny X509 dostawcy tożsamości:** Otwórz hello X509 certyfikat pobrany z hello Azure w programie Notatnik i Wklej zawartość hello, w tym polu. Upewnij się, Brak Brak wiersza w podziałów hello środkowej hello treści certyfikatu.
    
    g. Sprawdź następujące pola wyboru hello: **włączone, NameID szyfrowania i AuthnRequests logowania.**

    h. Kliknij przycisk **ustawienia logowania jednokrotnego aktualizacji** toosave hello ustawienia.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-scalex-enterprise-test-user"></a>Tworzenie użytkownika testowego ScaleX Enterprise

toolog użytkowników tooenable usługi Azure AD w tooScaleX przedsiębiorstwa muszą mieć przydzielone w tooScaleX przedsiębiorstwa. W przypadku hello ScaleX przedsiębiorstwa Inicjowanie obsługi to zadanie automatycznej i nie są wymagane żadne czynności ręcznych. Każdy użytkownik, który może pomyślnie wykonać uwierzytelnienia przy użyciu poświadczeń logowania jednokrotnego będą automatycznie udostępniane na powitania po stronie ScaleX.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie Enterprise tooScaleX dostępu użytkownika.

![Przypisz użytkownika][200] 

**tooassign Simona Britta tooScaleX przedsiębiorstwa, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **ScaleX Enterprise**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.

### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Kliknij hello ScaleX Enterprise kafelka w hello Panel dostępu, otrzymasz automatycznie zalogowane tooyour aplikacja całościowa ScaleX. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](https://msdn.microsoft.com/library/dn308586).


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

