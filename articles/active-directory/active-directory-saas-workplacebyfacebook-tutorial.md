---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy przez Facebook | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i miejsca pracy przez usługi Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Samouczek: Integracji Azure Active Directory z miejsca pracy przez usługi Facebook

Z tego samouczka, dowiesz się, jak toointegrate miejsca pracy w serwisie Facebook w usłudze Azure Active Directory (Azure AD).

Integrowanie miejsca pracy przez Facebook z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooWorkplace przez usługi Facebook
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWorkplace przez Facebook (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z miejsca pracy przez usługi Facebook, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Dołączanie w serwisie Facebook logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie miejsca pracy przez Facebook z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a>Dodawanie miejsca pracy przez Facebook z galerii hello
tooconfigure hello integracji miejsca pracy w serwisie Facebook w usłudze Azure Active Directory, należy tooadd miejsca pracy przez Facebook z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd miejsca pracy przez Facebook z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **miejsca pracy przez Facebook**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. W panelu wyników hello, wybierz **miejsca pracy przez Facebook**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z miejsca pracy przez usługi Facebook na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w miejscu pracy przez Facebook jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w miejscu pracy przez Facebook musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w miejscu pracy przez usługi Facebook.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z miejsca pracy przez usługi Facebook, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Konfigurowanie częstotliwości ponowne uwierzytelnianie](#configuring-reauthentication-frequency)**  -tooconfigure tooprompt dołączanie sprawdzania SAML.
3. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
4. **[Tworzenie pracy przez użytkownika testowego Facebook](#creating-a-workplace-by-facebook-test-user)**  -toohave odpowiednikiem Simona Britta w miejscu pracy przez usługi Facebook, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
5. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
6. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w miejscu pracy przez aplikację usługi Facebook.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z miejsca pracy przez Facebook, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **miejsca pracy przez Facebook** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. Na powitania **miejsca pracy przez domenę usługi Facebook i adresy URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instancename>.facebook.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.facebook.com/company/<instancename>`

    > [!NOTE] 
    > Wartości te nie są hello prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [miejsca pracy przez zespół obsługi klienta usługi Facebook](https://workplace.fb.com/faq/) tooget tych wartości. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. Na powitania **miejsca pracy przez konfigurację usługi Facebook** , kliknij przycisk **skonfigurować miejsca pracy przez Facebook** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. W oknie przeglądarki innej witryny sieci web, tooyour logowania miejsca pracy przez Facebook witryny firmy jako administrator.
  
   > [!NOTE] 
   > W ramach procesu uwierzytelniania SAML hello miejsce pracy mogą używać ciągów zapytań się too2.5 kilobajtów rozmiar w kolejności toopass parametry tooAzure AD.

8. W hello **pulpitu nawigacyjnego firmy**, przejdź toohello **uwierzytelniania** kartę.

9. W obszarze **uwierzytelnianie SAML**, wybierz pozycję **logowania jednokrotnego tylko** z listy rozwijanej hello.

10. Wartości wejściowe hello skopiowanych z **miejsca pracy przez konfigurację usługi Facebook** sekcji hello portalu Azure do odpowiednich pól hello:

    *   W **adres URL SAML** pole tekstowe, Wklej wartość hello **pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.
    *   W **pole tekstowe adres URL wystawcy SAML**, Wklej wartość hello **SAML identyfikator jednostki**, które zostały skopiowane z portalu Azure.
    *   W **przekierowania wylogowania SAML** (opcjonalnie), Wklej wartość hello **Sign-Out URL**, które zostały skopiowane z portalu Azure.
    *   Otwórz z **certyfikatu algorytmem base-64** w Notatniku pobrany z portalu Azure, skopiuj zawartość hello go do Schowka, a następnie wklej go toothe **certyfikatu SAML** pola tekstowego.

11. Może być konieczne tooenter hello odbiorców adres URL, adres URL odbiorcy, i adres URL ACS (usługa konsumenta potwierdzenia) w folderze hello **Konfiguracja SAML** sekcji.

12. Przewiń toohello dolnej części sekcji hello i kliknij przycisk hello **Test rejestracji Jednokrotnej** przycisku. Ten wyniki w oknie podręcznym znajdujących się ze strony logowania usługi Azure AD przedstawione. Wprowadź swoje poświadczenia w jako normalne tooauthenticate. 

    **Rozwiązywanie problemów:** adres e-mail hello upewnij się, że zostały zwrócone z usługi Azure AD jest hello tak samo jak hello są rejestrowane przy użyciu konta w miejscu pracy.

13. Po pomyślnym zakończeniu testu hello, przewiń toohello u dołu strony hello i kliknij przycisk hello **zapisać** przycisku.

14. Wszyscy użytkownicy korzystający z miejsca pracy zostanie teraz wyświetlone strony logowania usługi Azure AD do uwierzytelniania.

15. **SAML wylogowania przekierowania (opcjonalnie)** - 

    Możesz skonfigurować toooptionally adresu Url wylogowania SAML, które mogą być używane toopoint na strony wylogowania usługi Azure AD. Gdy to ustawienie jest włączone i skonfigurowane, hello użytkownika nie będzie strony wylogowania toohello bezpośrednie miejsca pracy. Zamiast tego użytkownik hello będzie toohello przekierowany adres url, który został dodany w ustawieniu przekierowania wylogowania SAML hello.


> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="configuring-reauthentication-frequency"></a>Konfigurowanie częstotliwości ponowne uwierzytelnianie

Można skonfigurować tooprompt pracy dotyczących sprawdzania SAML codziennie, trzy dni tygodnia, dwóch tygodni, miesięcy lub nigdy.

> [!NOTE] 
>Hello minimalną wartość sprawdzania SAML hello w aplikacjach mobilnych ustawiono tooone tygodnia.

Możesz też wymusić SAML zresetować dla wszystkich użytkowników za pomocą przycisku hello: Wymagaj SAML uwierzytelnianie dla wszystkich użytkowników.


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-workplace-by-facebook-test-user"></a>Tworzenie pracy przez użytkownika testowego usługi Facebook

W tej sekcji o nazwie Simona Britta tworzenia użytkownika w miejscu pracy przez usługi Facebook. Obszar roboczy w serwisie Facebook obsługę w czasie, który jest domyślnie włączona.

Brak akcji można w tej sekcji. Jeśli użytkownik nie istnieje w miejscu pracy przez usługi Facebook, nowy jest tworzona podczas próby tooaccess miejsca pracy przez Facebook.

>[!Note]
>Jeśli potrzebujesz toocreate użytkownik ręcznie, skontaktuj się z [miejsca pracy przez zespół obsługi klienta usługi Facebook](https://workplace.fb.com/faq/)

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWorkplace przez usługi Facebook.

![Przypisz użytkownika][200] 

**tooassign tooWorkplace Simona Britta przez Facebook, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **miejsca pracy przez Facebook**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Skonfiguruj Inicjowanie obsługi użytkowników](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

