---
title: 'Samouczek: Integracji Azure Active Directory z DocuSign | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a>Samouczek: Integracji Azure Active Directory z DocuSign

Z tego samouczka, dowiesz się, jak toointegrate DocuSign w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD DocuSign zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooDocuSign
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooDocuSign (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z DocuSign należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- DocuSign logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie DocuSign z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-docusign-from-hello-gallery"></a>Dodawanie DocuSign z galerii hello
tooconfigure hello integracji DocuSign do usługi Azure AD, należy tooadd DocuSign z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd DocuSign z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **DocuSign**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. W panelu wyników hello zaznacz **DocuSign**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z DocuSign na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w DocuSign jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w DocuSign musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w DocuSign.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z DocuSign, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego DocuSign](#creating-a-docusign-test-user)**  -toohave odpowiednikiem Simona Britta w DocuSign, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji DocuSign.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z DocuSign, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **DocuSign** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base 64)** , a następnie zapisz plik certyfikatu na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. Na powitania **konfiguracji DocuSign** części portalu Azure, kliknij przycisk **skonfigurować DocuSign** okna tooopen Konfigurowanie logowania jednokrotnego. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. W oknie przeglądarki innej witryny sieci web, logowania tooyour **portalu administracyjnego DocuSign** jako administrator.

6. W menu nawigacji powitania po lewej stronie powitania kliknij **domen**.
   
    ![Konfigurowanie rejestracji jednokrotnej][51]

7. W okienku po prawej stronie powitania, kliknij polecenie **oświadczenia domeny**.
   
    ![Konfigurowanie rejestracji jednokrotnej][52]

8. Na powitania **oświadczenia domeny** okna dialogowego, w hello **nazwy domeny** pole tekstowe, wpisz domenę firmy, a następnie kliknij przycisk **oświadczeń**. Upewnij się, że Sprawdź hello domeny i hello stan jest aktywny.
   
    ![Konfigurowanie rejestracji jednokrotnej][53]

9. W menu po lewej stronie powitania kliknij **dostawców tożsamości**  
   
    ![Konfigurowanie rejestracji jednokrotnej][54]
10. W okienku po prawej stronie powitania, kliknij przycisk **Dodawanie dostawcy tożsamości**. 
   
    ![Konfigurowanie rejestracji jednokrotnej][55]

11. Na powitania **ustawień dostawcy tożsamości** wykonaj hello następujące kroki:
   
    ![Konfigurowanie rejestracji jednokrotnej][56]

    a. W hello **nazwa** tekstowym, wpisz unikatową nazwę dla danej konfiguracji. Nie należy używać spacji.

    b. Wklej **identyfikator jednostki SAML** do hello **wystawcy dostawcy tożsamości** pola tekstowego.

    c. Wklej **SAML pojedynczy znak na adres URL usługi** do hello **adresu URL logowania do dostawcy tożsamości** pola tekstowego.

    d. Wklej **Sign-Out URL** do hello **adres URL wylogowania dostawcy tożsamości** pola tekstowego.

    e. Wybierz **podpisywania żądania uwierzytelniania**.

    f. Jako **AuthN wysyłanie żądania przez**, wybierz pozycję **POST**.

    g. Jako **Wyślij żądanie wylogowania**, wybierz pozycję **UZYSKAĆ**.

12. W hello **mapowanie atrybutu niestandardowego** sekcji, wybierz pole hello ma toomap oświadczenie, Azure AD. W tym przykładzie hello **emailaddress** oświadczenia jest zamapowana z wartością hello **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**. To nazwa oświadczenia domyślne hello z usługą Azure AD, oświadczenie adresu e-mail. 
   
    > [!NOTE]
    > Użyj hello odpowiednie **identyfikator użytkownika** toomap hello użytkownika z usługi Azure AD tooDocuSign użytkownika mapowania. Wybierz hello odpowiednie pola, a następnie wprowadź odpowiednie wartości hello na podstawie własnych ustawień organizacji.
          
    ![Konfigurowanie rejestracji jednokrotnej][57]

13. W hello **certyfikat dostawcy tożsamości** , kliknij przycisk **Dodaj certyfikat**, a następnie przekaż certyfikat hello został pobrany z portalu usługi Azure AD.   
   
    ![Konfigurowanie rejestracji jednokrotnej][58]

14. Kliknij pozycję **Zapisz**.

15. W hello **dostawców tożsamości** kliknij **akcje**, a następnie kliknij przycisk **punkty końcowe**.   
   
    ![Konfigurowanie rejestracji jednokrotnej][59]
 
16. W hello **Wyświetl SAML 2.0 punkty końcowe** sekcji na **portalu administracyjnego DocuSign**, wykonaj następujące kroki hello:
   
    ![Konfigurowanie rejestracji jednokrotnej][60]
   
    a. Hello kopiowania **adres URL wystawcy dostawcy usługi**i wkleić do hello **identyfikator** textbox w **DocuSign domeny i adres URL** sekcji hello Azure hello następujące portalu Wzorzec: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.
   
    b. Hello kopiowania **adresu URL logowania do usługi dostawcy**i wkleić do hello **na adres URL logowania** textbox w **DocuSign domeny i adres URL** sekcji hello Azure hello następujące portalu Wzorzec: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    c.  Kliknij przycisk **Zamknij**
    
17. Na powitania portalu Azure, kliknij przycisk **zapisać**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-docusign-test-user"></a>Tworzenie użytkownika testowego DocuSign

Aplikacja obsługuje **tylko w czasie Inicjowanie obsługi użytkowników** i po uwierzytelniania użytkowników są tworzone automatycznie w aplikacji hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooDocuSign dostępu.

![Przypisz użytkownika][200] 

**tooassign tooDocuSign Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **DocuSign**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka DocuSign hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour DocuSign aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Skonfiguruj Inicjowanie obsługi użytkowników](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

