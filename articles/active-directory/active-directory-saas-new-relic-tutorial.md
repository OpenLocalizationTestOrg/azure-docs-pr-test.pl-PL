---
title: "Samouczek: Integracji Azure Active Directory z usługi New Relic | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi New Relic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: dc8f0df3b18a32bde155e8911a581fc5f91af217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a>Samouczek: Integracji Azure Active Directory z usługi New Relic

Z tego samouczka, dowiesz się, jak toointegrate usługi New Relic w usłudze Azure Active Directory (Azure AD).

Integrowanie usługi New Relic z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooNew Relic
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooNew Relic (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z usługi New Relic należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Usługi New Relic logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie usługi New Relic w galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-new-relic-from-hello-gallery"></a>Dodawanie usługi New Relic w galerii hello
tooconfigure hello integracji usługi New Relic w usłudze Azure Active Directory, należy tooadd usługi New Relic z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd usługi New Relic w galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **usługi New Relic**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. W panelu wyników hello, wybierz **usługi New Relic**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi New Relic w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w usługi New Relic jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w usługi New Relic musi toobe ustanowione.

Usługi New Relic, przypisywanie wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usługi New Relic, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego usługi New Relic](#creating-a-new-relic-test-user)**  -toohave odpowiednikiem Simona Britta w usługi New Relic, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji usługi New Relic.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z usługi New Relic, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **usługi New Relic** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. Na powitania **adresy URL i nowej domeny Relic** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.newrelic.com`

    > [!NOTE] 
    > wartość Hello nie jest prawdziwe. Wartość hello aktualizacji z hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej nowego klienta Relic](https://support.newrelic.com/) tooget hello wartość. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. Na powitania **nowej konfiguracji Relic** kliknij **skonfigurować usługi New Relic** tooopen **Konfigurowanie logowania jednokrotnego** okna. Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. W oknie przeglądarki innej witryny sieci web, zaloguj się na tooyour **usługi New Relic** witryny firmy jako administrator.

8. W menu hello na górze hello, kliknij przycisk **ustawienia konta**.
   
    ![Ustawienia konta](./media/active-directory-saas-new-relic-tutorial/ic797036.png "ustawienia konta")

9. Kliknij przycisk hello **zabezpieczeń i uwierzytelniania** , a następnie kliknij pozycję hello **jednokrotne** kartę.
   
    ![Logowanie jednokrotne](./media/active-directory-saas-new-relic-tutorial/ic797037.png "logowanie jednokrotne")

10. Na stronie okna dialogowego SAML hello wykonaj następujące kroki hello:
   
    ![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")
   
   a. Kliknij przycisk **wybierz plik** tooupload pobrany certyfikat usługi Azure Active Directory.

   b. W hello **adres URL logowania zdalnego** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.
   
   c. W hello **lądowanie adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out adres URL**, które zostały skopiowane z portalu Azure.

   d. Kliknij przycisk **Zapisz moje zmiany**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-new-relic-test-user"></a>Tworzenie użytkownika testowego usługi New Relic

W przypadku użytkowników usługi Azure Active Directory toolog kolejności tooenable w tooNew Relic musi być przygotowana do usługi New Relic. W przypadku hello usługi New Relic Inicjowanie obsługi to zadanie ręczne.

**tooprovision tooNew konta użytkownika Relic, wykonaj następujące kroki hello:**

1. Zaloguj się za tooyour **usługi New Relic** witryny firmy jako administrator.

2. W menu hello na górze hello, kliknij przycisk **ustawienia konta**.
   
    ![Ustawienia konta](./media/active-directory-saas-new-relic-tutorial/ic797040.png "ustawienia konta")

3. W hello **konta** na powitania w okienku po lewej stronie, kliknij przycisk **Podsumowanie**, a następnie kliknij przycisk **Dodaj użytkownika**.
   
    ![Ustawienia konta](./media/active-directory-saas-new-relic-tutorial/ic797041.png "ustawienia konta")

4. Na powitania **aktywni użytkownicy** okna dialogowego, wykonaj następujące kroki hello:
   
    ![Aktywni użytkownicy](./media/active-directory-saas-new-relic-tutorial/ic797042.png "aktywni użytkownicy")
   
    a. W hello **E-mail** pole tekstowe, hello typu adres e-mail z prawidłowym użytkownikiem usługi Azure Active Directory ma tooprovision.

    b. Jako **roli** wybierz **użytkownika**.

    c. Kliknij przycisk **Dodaj tego użytkownika**.

>[!NOTE]
>Możesz użyć innych usługi New Relic użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez usługi New Relic tooprovision kont użytkowników usługi AAD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooNew Relic.

![Przypisz użytkownika][200] 

**tooassign tooNew Simona Britta Relic, wykonaj następujące kroki hello:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **usługi New Relic**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.

Po kliknięciu kafelka usługi New Relic hello w hello Panel dostępu, należy pobrać aplikację usługi New Relic tooyour zalogowane automatycznie.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

