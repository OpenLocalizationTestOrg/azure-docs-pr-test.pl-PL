---
title: 'Samouczek: Integracji Azure Active Directory z Marketo | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a>Samouczek: Integracji Azure Active Directory z usługi Marketo

Z tego samouczka, dowiesz się, jak toointegrate Marketo w usłudze Azure Active Directory (Azure AD).

Integrowanie usługi Marketo w usłudze Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMarketo
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMarketo (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z Marketo należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Usługi Marketo jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie usługi Marketo z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-marketo-from-hello-gallery"></a>Dodawanie usługi Marketo z galerii hello
tooconfigure hello integracji usługi Marketo w usłudze Azure Active Directory, należy tooadd Marketo od hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Marketo z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Marketo**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. W panelu wyników hello, wybierz **Marketo**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi Marketo oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Marketo jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Marketo musi toobe ustanowione.

W Marketo, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Marketo, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Marketo](#creating-a-marketo-test-user)**  -toohave odpowiednikiem Simona Britta w Marketo, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji usługi Marketo.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Marketo, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Marketo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. Na powitania **Marketo domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://saml.marketo.com/sp`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://login.marketo.com/saml/assertion/\<munchkinid\>`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości. Skontaktuj się z [zespołem pomocy technicznej usługi Marketo](http://investors.marketo.com/contactus.cfm) tooget tych wartości.
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji usługi Marketo** kliknij **Konfiguruj usługi Marketo** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. tooget Munchkin identyfikator aplikacji, zaloguj się przy użyciu poświadczeń administratora tooMarketo i wykonania następujących czynności:
   
    a. Zaloguj się w aplikacji tooMarketo przy użyciu poświadczeń administratora.
   
    b. Kliknij przycisk hello **Admin** przycisk w okienku nawigacji w górnym hello.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Przejdź do menu integracji toohello, a następnie kliknij przycisk hello **łącze Munchkin**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    d. Skopiuj identyfikator Munchkin wyświetlany na ekranie powitania hello i wykonaj adres URL odpowiedzi, w Kreatorze konfiguracji hello Azure AD.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. Witaj tooconfigure logowania jednokrotnego w aplikacji hello wykonaj hello następujące czynności:
   
    a. Zaloguj się w aplikacji tooMarketo przy użyciu poświadczeń administratora.
   
    b. Kliknij przycisk hello **Admin** przycisk w okienku nawigacji w górnym hello.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Przejdź do menu integracji toohello i kliknij przycisk **rejestracji jednokrotnej**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    d. tooenable hello SAML ustawienia, kliknij przycisk **Edytuj** przycisku.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    e. **Włączone** ustawienia logowania jednokrotnego.
   
    f. Wklej hello **identyfikator jednostki SAML**, w hello **identyfikator wystawcy** pola tekstowego.
   
    g. W hello **identyfikator jednostki** pole tekstowe, wprowadź adres URL hello jako `http://saml.marketo.com/sp`.
   
    h. Wybierz hello lokalizacji identyfikator użytkownika jako **element nazwa identyfikatora**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > Jeśli Twojego identyfikatora użytkownika nie ma wartości głównej nazwy użytkownika, a następnie zmień wartość hello hello atrybutu karcie.
   
    i. Przekaż certyfikat hello, który został pobrany z Kreatora konfiguracji usługi Azure AD. **Zapisz** hello ustawienia.
   
    j. Edytowanie ustawień stron przekierowania hello.
   
    k. Wklej hello **SAML pojedynczy znak na adres URL usługi** w hello **adres URL logowania** pola tekstowego.
   
    l. Wklej hello **Sign-Out URL** w hello **adresu URL wylogowania** pola tekstowego.
   
    m. W hello **adres URL błędu**, kopia programu **adresu URL wystąpienia usługi Marketo** i kliknij przycisk **zapisać** przycisk toosave ustawienia.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. tooenable hello logowania jednokrotnego dla użytkowników, pełną hello następujące akcje:
   
    a. Zaloguj się w aplikacji tooMarketo przy użyciu poświadczeń administratora.
   
    b. Kliknij przycisk hello **Admin** przycisk w okienku nawigacji w górnym hello.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Przejdź toohello **zabezpieczeń** menu i kliknij przycisk **ustawienia logowania**.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    d. Sprawdź hello **wymagają rejestracji Jednokrotnej** opcji i **zapisać** hello ustawienia.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-marketo-test-user"></a>Tworzenie użytkownika testowego usługi Marketo

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Marketo. Wykonaj te kroki toocreate użytkownika na platformie Marketo.

1. Zaloguj się w aplikacji tooMarketo przy użyciu poświadczeń administratora.

2. Kliknij przycisk hello **Admin** przycisk w okienku nawigacji w górnym hello.
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. Przejdź toohello **zabezpieczeń** menu i kliknij przycisk **użytkownicy i role**
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. Kliknij przycisk hello **zaprosić nowego użytkownika** link na karcie Użytkownicy hello
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. W hello zaprosić nowego użytkownika Kreatora wypełnienia hello następujących informacji
   
    a. Wprowadź nazwę użytkownika hello **E-mail** adres w polu tekstowym hello
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    b. Wprowadź hello **imię** w polu tekstowym hello
   
    c. Wprowadź hello **nazwisko** w polu tekstowym hello
   
    d. Kliknij przycisk **Dalej**

6. W hello **uprawnienia** kartę, zaznacz hello **roli użytkownika** i kliknij przycisk **dalej**
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. Kliknij przycisk hello **wysyłania** przycisk toosend hello użytkownika zaproszenia
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. Użytkownik otrzymuje powiadomienie e-mail hello i hello tooclick łącze i zmień hello hasło tooactivate hello konta. 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMarketo.

![Przypisz użytkownika][200] 

**tooassign tooMarketo Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Marketo**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Marketo hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Marketo aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

