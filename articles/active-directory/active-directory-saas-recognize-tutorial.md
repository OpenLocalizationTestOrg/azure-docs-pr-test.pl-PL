---
title: 'Samouczek: Integracji Azure Active Directory z rozpoznawanie | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i rozpoznawanie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a>Samouczek: Integracji Azure Active Directory z rozpoznawanie

Z tego samouczka, dowiesz się, jak rozpoznać toointegrate w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD rozpoznawanie zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooRecognize
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooRecognize (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Integracja tooconfigure usługi Azure AD z rozpoznawanie, potrzebujesz hello następujące elementy:

- Subskrypcję usługi Azure AD
- Rozpoznaj logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie rozpoznawaj z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-recognize-from-hello-gallery"></a>Dodawanie rozpoznawaj z galerii hello
tooconfigure hello integracji rozpoznawanie do usługi Azure AD, należy tooadd rozpoznawaj z galerii hello tooyour listę zarządzanych aplikacji SaaS.

**tooadd rozpoznawaj z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **rozpoznawanie**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. W panelu wyników hello, wybierz **rozpoznawanie**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z rozpoznawanie w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w rozpoznawanie jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w rozpoznawanie musi toobe ustanowione.

Rozpoznaj, przypisywanie wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD logowanie jednokrotne z rozpoznawanie, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego rozpoznawanie](#creating-a-recognize-test-user)**  -toohave odpowiednikiem Simona Britta w rozpoznawanie, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji rozpoznawanie.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z rozpoznawanie, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **rozpoznawanie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. Na powitania **adresy URL i rozpoznać domeny** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://recognizeapp.com/<your-domain>/saml/sso`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://recognizeapp.com/<your-domain>`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta rozpoznaje](mailto:support@recognizeapp.com) uzyskać adres URL logowania i można uzyskać wartość identyfikatora otwierając hello sekcja Ustawienia logowania jednokrotnego, która znajduje się w dalszej części samouczka hello hello adres URL metadanych dostawcy usługi. . 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. Na powitania **rozpoznaje konfiguracji** kliknij **skonfigurować rozpoznaje** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour rozpoznawanie dzierżawy z uprawnieniami administratora.

8. Na powitania prawym górnym rogu kliknij **Menu**. Przejdź za**administrator firmy**.
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. W okienku nawigacji po lewej stronie powitania kliknij **ustawienia**.
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. Wykonaj następujące kroki powitania **ustawienia logowania jednokrotnego** sekcji.
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    a. Jako **włączenia logowania jednokrotnego**, wybierz pozycję **ON**.

    b. W hello **identyfikator jednostki IDP** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.
    
    c. W hello **logowania jednokrotnego, docelowy adres url** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.
    
    d. W hello **Slo docelowy adres url** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure. 
    
    e. Otwórz z pobranego **certyfikatu (Base64)** pliku w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu** pola tekstowego.
    
    f. Kliknij przycisk hello **Zapisz ustawienia** przycisku. 

11. Obok hello **ustawienia logowania jednokrotnego** sekcji, skopiuj adres URL hello pod **adres url usługi dostawcy metadanych**.
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. Otwórz hello **łącze URL metadanych** w obszarze puste przeglądarki toodownload hello metadanych dokumentu. Następnie skopiuj hello EntityDescriptor value(entityID) z pliku hello i wklej go w **identyfikator** textbox w **sekcji rozpoznać domeny i adresy URL** w portalu Azure.
    
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-recognize-test-user"></a>Tworzenie użytkownika testowego rozpoznawanie

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do uznania muszą mieć przydzielone do uznania. W przypadku hello rozpoznawanie Inicjowanie obsługi to zadanie ręczne.

Ta aplikacja nie obsługuje udostępniania SCIM, ale ma synchronizacji alternatywny użytkownika, która udostępnia użytkownikom. 

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się do witryny firmy rozpoznawanie jako administrator.

2. Na powitania prawym górnym rogu kliknij **Menu**. Przejdź za**administrator firmy**.

3. W okienku nawigacji po lewej stronie powitania kliknij **ustawienia**.

4. Wykonaj następujące kroki powitania **synchronizacji użytkownika** sekcji.
   
   ![Nowy użytkownik](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "nowego użytkownika")
   
   a. Jako **włączona synchronizacja**, wybierz pozycję **ON**.
   
   b. Jako **dostawcy synchronizacji wybierz**, wybierz pozycję **Microsoft / usługi Office 365**.
   
   c. Kliknij przycisk **Przeprowadź synchronizację użytkownika**.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooRecognize.

![Przypisz użytkownika][200] 

**tooassign tooRecognize Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **rozpoznawanie**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.

Po kliknięciu kafelka rozpoznawanie hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour rozpoznawanie aplikacji. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

