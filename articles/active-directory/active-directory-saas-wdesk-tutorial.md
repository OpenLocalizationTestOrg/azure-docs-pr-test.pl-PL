---
title: 'Samouczek: Integracji Azure Active Directory z Wdesk | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a>Samouczek: Integracji Azure Active Directory z Wdesk

Z tego samouczka, dowiesz się, jak toointegrate Wdesk w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Wdesk zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooWdesk
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWdesk (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz. [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Wdesk należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Wdesk jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Wdesk z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-wdesk-from-hello-gallery"></a>Dodawanie Wdesk z galerii hello
tooconfigure hello integracji Wdesk do usługi Azure AD, należy tooadd Wdesk z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Wdesk z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Wdesk**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. W panelu wyników hello zaznacz **Wdesk**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Wdesk na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Wdesk jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Wdesk musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Wdesk.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Wdesk, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Wdesk](#creating-a-wdesk-test-user)**  -toohave odpowiednikiem Simona Britta w Wdesk, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Wdesk.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Wdesk, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Wdesk** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. Na powitania **Wdesk domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb wykonywania hello następujące kroki:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**. Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane w trybie wykonywania powitania po kroku:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`
     
    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania. Te wartości można uzyskać od WDesk portalu, po skonfigurowaniu hello logowania jednokrotnego. 
  
5. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. W oknie przeglądarki innej witryny sieci web, tooWdesk logowania jako Administrator zabezpieczeń.

8. W lewej dolnej powitania kliknij **Admin** i wybierz polecenie **administrator konta**:
 
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. W Wdesk administratora, przejdź zbyt**zabezpieczeń**, następnie **SAML** > **ustawienia SAML**:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. W obszarze **ustawienia ogólne**, sprawdź hello **Włącz SAML rejestrację jednokrotną**:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. W obszarze **szczegóły dostawcy usług**, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      a. Kopiuj hello **adres URL logowania** i wklej go w **adres Url logowania** textbox w portalu Azure.
   
      b. Kopiuj hello **adres Url metadanych** i wklej go w **identyfikator** textbox w portalu Azure.
       
      c. Kopiuj hello **adres url klienta** i wklej go w **adres Url odpowiedzi** textbox w portalu Azure.
   
      d. Kliknij przycisk **zapisać** na zmiany hello toosave portalu Azure.      

12. Kliknij przycisk **Konfigurowanie ustawień IdP** tooopen **edytowanie ustawień dostawców tożsamości** okna dialogowego. Kliknij przycisk **wybierz plik** toolocate hello **Metadata.xml** następnie przekazać plik zapisany w portalu Azure.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. Kliknij przycisk **zapisać zmiany**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-wdesk-test-user"></a>Tworzenie użytkownika testowego Wdesk

toolog użytkowników tooenable usługi Azure AD w tooWdesk, muszą mieć przydzielone do Wdesk. W Wdesk Inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooWdesk jako Administrator zabezpieczeń.
2. Przejdź za**Admin** > **administrator konta**.

     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. Kliknij przycisk **członków** w obszarze **osób**.

4. Teraz kliknij **dodać element członkowski** tooopen **dodać element członkowski** okno dialogowe. 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. W **użytkownika** tekst Wprowadź hello nazwa użytkownika, takich jak  **brittasimon@contoso.com**  i kliknij przycisk **Kontynuuj** przycisku.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  Wprowadź szczegóły hello, jak pokazano poniżej:
  
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    a. W **E-mail** tekstowym wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .

    b. W **imię** tekst Wprowadź hello imię użytkownika, takich jak **Britta**.

    c. W **nazwisko** tekst Wprowadź hello nazwisko użytkownika, takich jak **Simona**.

7. Kliknij przycisk **zapisać element członkowski** przycisku.  

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWdesk.

![Przypisz użytkownika][200] 

**tooassign tooWdesk Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Wdesk**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Wdesk hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Wdesk aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

