---
title: "Samouczek: Integracji Azure Active Directory z chmurą Atlassian | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i w chmurze Atlassian."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a>Samouczek: Integracji Azure Active Directory z chmurą Atlassian

Z tego samouczka, dowiesz się, jak toointegrate Atlassian chmury w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Atlassian chmury udostępnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooAtlassian chmury
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAtlassian chmury (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z chmurą Atlassian należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Chmura Atlassian logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Atlassian chmury z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-atlassian-cloud-from-hello-gallery"></a>Dodawanie Atlassian chmury z galerii hello
tooconfigure hello integracji Atlassian chmury do usługi Azure AD, należy tooadd Atlassian chmury z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Atlassian chmury z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **chmury Atlassian**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. W panelu wyników hello, wybierz **chmury Atlassian**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z chmurą Atlassian oparte na użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w chmurze Atlassian jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w chmurze Atlassian musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w chmurze Atlassian.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z chmurą Atlassian, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego chmury Atlassian](#creating-an-atlassian-cloud-test-user)**  -toohave odpowiednikiem Simona Britta w chmurze Atlassian, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w chmurze Atlassian aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z chmurą Atlassian wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **chmury Atlassian** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. Na powitania **adresy URL i domenę chmury Atlassian** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instancename>.atlassian.net/admin/saml/edit`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL jako:`https://id.atlassian.com/login/saml/acs`

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonywać powitania po kroku, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instancename>.atlassian.net`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty identyfikator i adres URL logowania. Możesz uzyskać dokładne wartości hello z ekranu konfiguracji SAML chmury Atlassian.
 
5. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. Na powitania **konfiguracji chmury Atlassian** , kliknij przycisk **Konfigurowanie chmury Atlassian** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. tooget logowania jednokrotnego skonfigurowane dla aplikacji, toohello logowania portalu Atlassian za pomocą hello uprawnienia administratora.

8. W sekcji uwierzytelnianie hello hello lewy pasek nawigacyjny kliknij **domen**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    a. W polu tekstowym hello, wpisz nazwę domeny, a następnie kliknij przycisk **Dodaj domenę**.
        
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    b. tooverify hello domeny, kliknij przycisk **Sprawdź**. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    c. Pobierz plik html weryfikacji domeny hello, Prześlij go toohello folder główny witryny sieci Web w danej domenie, a następnie kliknij **weryfikowanie domeny**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    d. Po zweryfikowaniu domeny hello hello wartość hello **stan** pole jest **zweryfikowano**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. Na pasku nawigacyjnym po lewej stronie powitania kliknij **SAML**.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. Utwórz Konfiguracja SAML i Dodaj hello tożsamości dostawcy konfiguracji.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    a. W hello **dostawcy tożsamości identyfikator jednostki** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.

    b. W hello **dostawcy tożsamości adresu URL logowania jednokrotnego** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.

    c. Otwórz certyfikat hello pobrane z Azure portal i skopiuj wartości hello bez hello Begin i na końcu wiersza i wklej go w hello **X509 publicznego certyfikatu** pole.
    
    d. Kliknij przycisk **Zapisz konfigurację** tooSave hello ustawienia.
     
11. Zaktualizuj toomake ustawienia usługi Azure AD hello upewnić się, że Instalator hello, popraw adres URL identyfikatora.
  
    a. Kopiuj hello **Identyfikatora tożsamości SP** z hello SAML ekranu i wklej go w usłudze Azure AD jako hello **identyfikator** wartość.

    b. Zaloguj się na adres URL jest adres URL dzierżawy hello Atlassian chmury.     

     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. W portalu Azure hello, kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-atlassian-cloud-test-user"></a>Tworzenie użytkownika testowego Atlassian chmury

toolog użytkowników tooenable usługi Azure AD w tooAtlassian chmurze muszą mieć przydzielone do Atlassian chmury.  
W przypadku Atlassian chmury Inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. W sekcji Administracja witryny hello, kliknij przycisk hello **użytkowników** przycisku

    ![Utwórz użytkownika Atlassian chmury](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. Kliknij przycisk hello **Tworzenie użytkownika** toocreate przycisk użytkownika w chmurze Atlassian hello

    ![Utwórz użytkownika Atlassian chmury](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. Wprowadź nazwę użytkownika hello **adres E-mail**, **Username**, i **Pełna nazwa** i przypisz hello dostęp do aplikacji. 

    ![Utwórz użytkownika Atlassian chmury](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. Kliknij przycisk **tworzenia użytkownika** przycisku, wysyła hello e-mail zaproszenia toohello użytkownika i po zaakceptowaniu hello zaproszenia hello użytkownika będzie aktywny w systemie hello. 

>[!NOTE] 
>Można również utworzyć hello zbiorczego użytkowników, klikając hello **Tworzenie zbiorczego** przycisk w sekcji użytkownicy hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAtlassian chmury.

![Przypisz użytkownika][200] 

**tooassign tooAtlassian Simona Britta chmury, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **chmury Atlassian**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą hello panelu dostępu.

Po kliknięciu hello chmury Atlassian kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji w chmurze Atlassian. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

