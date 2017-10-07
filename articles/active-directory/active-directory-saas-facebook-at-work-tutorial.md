---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy przez Facebook | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i miejsca pracy przez usługi Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Samouczek: Integracji Azure Active Directory z miejsca pracy przez usługi Facebook

Z tego samouczka, dowiesz się, jak toointegrate miejsca pracy w serwisie Facebook w usłudze Azure Active Directory (Azure AD).

Integrowanie miejsca pracy przez Facebook z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooWorkplace przez usługi Facebook.
- Umożliwia użytkownikom tooautomatically uzyskać zalogowanego tooWorkplace przez Facebook (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji: hello portalu Azure.

Aby uzyskać więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z miejsca pracy przez usługi Facebook, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Dołączanie w serwisie Facebook rejestracji jednokrotnej (SSO) włączone subskrypcji

kroki hello tootest w tym samouczku, wykonaj te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować logowania jednokrotnego programu Azure AD w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodaj obszar roboczy w serwisie Facebook z galerii hello.
2. Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej.

## <a name="add-workplace-by-facebook-from-hello-gallery"></a>Dodawanie miejsca pracy przez Facebook z galerii hello
tooconfigure hello integrację z miejsca pracy przez usługi Facebook usługi Azure AD, Dodaj obszar roboczy w serwisie Facebook hello galerii tooyour listy zarządzanych aplikacji SaaS.

1. W hello [portalu Azure](https://portal.azure.com), w lewym okienku hello, wybierz **usługi Azure Active Directory**. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przeglądaj zbyt**aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd hello nowej aplikacji, wybierz pozycję **nowej aplikacji** u góry hello hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **miejsca pracy przez Facebook**i wybierz **miejsca pracy przez Facebook** z wyników. Następnie wybierz **Dodaj**, tooadd hello aplikacji.

    ![Obszar roboczy w serwisie Facebook hello listy wyników](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji Konfiguracja i testowanie usługi Azure AD SSO z miejsca pracy przez Facebook, na podstawie użytkownika testowego, nazywany "Britta Simona".

Aby toowork logowania jednokrotnego usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w miejscu pracy przez Facebook jest tooa użytkownika w usłudze Azure AD. Innymi słowy można ustanowić połączonego relacji między użytkownika usługi Azure AD i hello użytkownikowi w miejscu pracy przez usługi Facebook.

Ustanowić tę relację, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w miejscu pracy przez usługi Facebook.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji włączenia funkcji logowania jednokrotnego usługi Azure AD w portalu Azure hello i konfigurowanie logowania jednokrotnego w miejscu pracy aplikacji usługi Facebook.

1. W portalu Azure na powitania hello **miejsca pracy przez Facebook** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. W hello **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. W hello **miejsca pracy przez domenę usługi Facebook i adresy URL** sekcji, hello następujące:

    a. W hello **adres URL logowania** wpisz adres URL, który używa hello następującego wzorca:`https://<company subdomain>.facebook.com`

    b. W hello **identyfikator** wpisz adres URL, który używa hello następującego wzorca:`https://www.facebook.com/company/<scim company id>`

    > [!NOTE]
    > Te wartości są tylko przykładem. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z pomocą hello [miejsca pracy przez zespół obsługi klienta usługi Facebook](https://workplace.fb.com/faq/) tooget tych wartości. 

4. W hello **SAML certyfikat podpisywania** wybierz opcję **certyfikatu (Base64)**, a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Wybierz pozycję **Zapisz**.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. W hello **miejsca pracy przez konfigurację usługi Facebook** zaznacz **skonfigurować miejsca pracy przez Facebook** tooopen hello **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **krótkimi opisami** sekcji.

    ![Obszar roboczy w konfiguracji usługi Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się tooyour miejsca pracy przez Facebook witryny firmy jako administrator.
  
   > [!NOTE] 
   > W ramach procesu uwierzytelniania SAML hello miejsca pracy można użyć ciągów zapytania zapasowej kilobajtów too2.5 rozmiar w kolejności toopass parametry tooAzure AD.

8. W hello **pulpitu nawigacyjnego firmy**, przejdź toohello **uwierzytelniania** kartę.

9. W obszarze **uwierzytelnianie SAML**, wybierz pozycję **logowania jednokrotnego tylko** z listy rozwijanej hello.

10. Wprowadź wartości hello skopiowanych z hello **miejsca pracy przez konfigurację usługi Facebook** sekcji hello portalu Azure do odpowiednich pól hello:

    *   W **adres URL SAML** pole tekstowe, Wklej wartość hello **pojedynczy znak na adres URL usługi**, które zostały skopiowane z hello portalu Azure.
    *   W **adres URL wystawcy SAML** pole tekstowe, Wklej hello wartość **identyfikator jednostki SAML**, które zostały skopiowane z hello portalu Azure.
    *   W **SAML wylogowania przekierowania (opcjonalnie)**, Wklej wartość hello **Sign-Out URL**, które zostały skopiowane z hello portalu Azure.
    *   Otwórz z **certyfikatu algorytmem base-64** w Notatniku pobrane z hello portalu Azure. Skopiuj zawartość hello go do Schowka, a następnie wklej go toothe **certyfikatu SAML** pola tekstowego.

11. Może być konieczne odbiorców hello tooenter adres URL, adres URL odbiorcy i ACS (usługa konsumenta potwierdzenia) adres URL, na liście hello **Konfiguracja SAML** sekcji.

12. Przewiń toohello dołu hello sekcji, a następnie wybierz **Test rejestracji Jednokrotnej**. Zostanie wyświetlone okno podręczne ze strony logowania hello Azure AD. tooauthenticate, wprowadź swoje poświadczenia, jak zwykle. Upewnij się, adres e-mail hello zwrócony z usługi Azure AD jest taki sam, jak hello konto firmowe, w którym użytkownik jest zalogowany przy użyciu hello.

13. Jeśli hello test zakończyło się pomyślnie, przewiń toohello u dołu strony hello oraz wybierz **zapisać**.

14. Teraz przedstawiono wszystkich osób korzystających z miejsca pracy z usługą Azure AD strony logowania dla uwierzytelniania.

Możesz wybrać tooconfigure SAML wylogowaniu adresu URL, który może być używane toopoint na wyrejestrowywania hello Azure AD. Gdy to ustawienie jest włączone i skonfigurowane, hello użytkownik nie jest już wyrejestrowywania toohello bezpośrednie miejsca pracy. Zamiast tego użytkownik hello jest toohello przekierowany adres URL, który został dodany w ustawieniu przekierowania wylogowania SAML hello.


> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello. Po dodaniu tej aplikacji z hello **usługi Active Directory** > **aplikacje dla przedsiębiorstw** po prostu wybierz hello **rejestracji jednokrotnej** kartę i hello dostępu osadzone dokumentacji za pośrednictwem hello **konfiguracji** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w hello [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="configure-reauthentication-frequency"></a>Konfigurowanie częstotliwości ponowne uwierzytelnianie

Można skonfigurować tooprompt dołączanie sprawdzania SAML codziennie trzech dni, co tydzień, dwa tygodnie, co miesiąc lub nigdy.

> [!NOTE] 
>Hello minimalną wartość sprawdzania SAML hello w aplikacjach mobilnych ustawiono tooone tygodnia.

Możesz też wymusić SAML zresetować dla wszystkich użytkowników. toodo hello, użyj **SAML wymagają uwierzytelniania wszystkich użytkowników, którzy teraz** przycisku.


### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

1. W hello **portalu Azure**, w lewym okienku hello, wybierz **usługi Azure Active Directory**.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**i wybierz **wszyscy użytkownicy**.
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okno dialogowe, wybierz opcję **Dodaj**.
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. W hello **użytkownika** okna dialogowego pozycję hello następujące:
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** polu tekstowym **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło**i zapisz ją.

    d. Wybierz pozycję **Utwórz**.
 
### <a name="create-a-workplace-by-facebook-test-user"></a>Utwórz pracy przez użytkownika testowego usługi Facebook

W tej sekcji o nazwie Simona Britta tworzenia użytkownika w miejscu pracy przez usługi Facebook. Obszar roboczy w serwisie Facebook obsługę w czasie, który jest domyślnie włączona.

Brak akcji można w tej sekcji. Jeśli użytkownik nie istnieje w miejscu pracy przez usługi Facebook, nowy jest tworzona podczas próby tooaccess miejsca pracy przez Facebook.

>[!Note]
>Toocreate użytkownik ręcznie, należy skontaktować się z hello [miejsca pracy przez zespół obsługi klienta usługi Facebook](https://workplace.fb.com/faq/).

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWorkplace przez usługi Facebook.

![Przypisz użytkownika][200] 

1. W hello Azure umożliwia wyświetlanie aplikacji hello portalu, Otwórz. Przejdź do widoku katalogu toohello znajduje się zbyt**aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **miejsca pracy przez Facebook**.

    ![Witaj miejsca pracy przez łącze usługi Facebook na liście aplikacji hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. W menu hello powitania po lewej stronie wybierz **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. Wybierz pozycję **Dodaj**. Następnie w hello **Dodaj przydziału** okienku wybierz **użytkowników i grup**.

    ![Okienko Dodaj przypisania Hello][203]

5. W hello **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. W hello **użytkowników i grup** okno dialogowe, wybierz opcję **wybierz**.

7. W hello **Dodaj przydziału** okno dialogowe, wybierz opcję **przypisać**.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

Jeśli chcesz tootest ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.
Aby uzyskać więcej informacji, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).


## <a name="next-steps"></a>Następne kroki

* Zobacz hello [lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md).
* Odczyt [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).
* Dowiedz się więcej o tym, jak za[skonfigurować Inicjowanie obsługi użytkowników](active-directory-saas-facebook-at-work-provisioning-tutorial.md).



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

