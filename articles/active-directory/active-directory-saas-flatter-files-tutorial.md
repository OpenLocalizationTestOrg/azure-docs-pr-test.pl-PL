---
title: "Samouczek: Integracji Azure Active Directory z plikami płaska | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i płaska plików."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 73ca2613b7bbaf9992ecf624ff5defabaa44f7a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a>Samouczek: Integracji Azure Active Directory z plikami płaska

Z tego samouczka, dowiesz się, jak toointegrate płaska plików w usłudze Azure Active Directory (Azure AD).

Integrowanie płaska pliki z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do plików tooFlatter
- Można włączyć tooautomatically Twojego użytkownikom pobieranie plików zalogowane tooFlatter (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z plikami płaska należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Pliki płaska logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie plików płaska z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-flatter-files-from-hello-gallery"></a>Dodawanie plików płaska z galerii hello
tooconfigure hello integracji płaska plików do usługi Azure AD, należy tooadd płaska plików z listy tooyour galerii hello zarządzanych aplikacji SaaS.

**tooadd płaska pliki z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **płaska pliki**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. W panelu wyników hello, wybierz **płaska pliki**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z plikami płaska w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w plikach płaska jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w plikach płaska musi toobe ustanowione.

W plikach płaska, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z plikami płaska, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego płaska pliki](#creating-a-flatter-files-test-user)**  -toohave odpowiednikiem Simona Britta płaska plików, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji płaska plików.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z plikami płaska wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **płaska pliki** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. Na powitania **płaska domeny plików i adresy URL** sekcji, hello użytkownik nie ma tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. Na powitania **płaska pliki konfiguracji** kliknij **skonfigurować płaska pliki** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. Zaloguj się na tooyour płaska pliki aplikacji jako administrator.

8. Kliknij przycisk **pulpitu NAWIGACYJNEGO**. 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. Kliknij przycisk **ustawienia**, a następnie wykonaj następujące kroki na powitania hello **firmy** karty: 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    a. Wybierz **SAML 2.0 jest używany do uwierzytelniania**.
    
    b. Kliknij przycisk **skonfigurować SAML**.

8. Na powitania **Konfiguracja SAML** okna dialogowego, wykonaj następujące kroki hello: 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    a. W hello **domeny** tekstowym, wpisz domenę zarejestrowany.
   
    >[!NOTE]
    >Jeśli użytkownik nie ma zarejestrowanej domeny jeszcze, skontaktuj się z bardziej płaski plików obsługuje zespołu za pomocą [ support@flatterfiles.com ](mailto:support@flatterfiles.com). 
    
    b. W **adres URL dostawcy tożsamości** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana tworzą portalu Azure.
   
    c.  Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat dostawcy tożsamości** pola tekstowego.

    d. Kliknij przycisk **aktualizacji**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-flatter-files-test-user"></a>Tworzenie użytkownika testowego płaska plików

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w płaska plików.

**toocreate użytkownika o nazwie Simona Britta w plikach płaska wykonaj hello następujące kroki:**

1. Zaloguj się na tooyour **płaska pliki** witryny firmy jako administrator.

2. W okienku nawigacji hello po lewej stronie powitania kliknij **ustawienia**, a następnie kliknij przycisk hello **użytkowników** kartę.
   
    ![Utwórz użytkownika płaska plików](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. Kliknij przycisk **dodać użytkownika**. 

4. Na powitania **Dodaj użytkownika** okna dialogowego, wykonaj następujące kroki hello:
   
    ![Utwórz użytkownika płaska plików](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    a. W hello **imię** pole tekstowe, typ **Britta**.
   
    b. W hello **nazwisko** pole tekstowe, typ **Simona**. 
   
    c. W hello **adres E-mail** tekstowym, wpisz adres e-mail firmy Britta hello portalu Azure.
   
    d. Kliknij przycisk **przesłać**.   


### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji, musisz włączyć Simona Britta toouse Azure logowania jednokrotnego za udzielanie dostępu do plików tooFlatter.

![Przypisz użytkownika][200] 

**tooassign Simona Britta tooFlatter pliki, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **płaska pliki**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu powitalne płaska pliki kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour płaska pliki aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

