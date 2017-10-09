---
title: 'Samouczek: Integracji Azure Active Directory z UserVoice | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a>Samouczek: Integracji Azure Active Directory z UserVoice

Z tego samouczka, dowiesz się, jak toointegrate UserVoice w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD UserVoice zawiera hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooUserVoice.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooUserVoice (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z UserVoice należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- UserVoice logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie UserVoice z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-uservoice-from-hello-gallery"></a>Dodawanie UserVoice z galerii hello
tooconfigure hello integracji usługi UserVoice w usłudze Azure Active Directory, należy tooadd UserVoice z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd UserVoice z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **UserVoice**, wybierz pozycję **UserVoice** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![UserVoice hello listy wyników](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z UserVoice w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w UserVoice jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w UserVoice musi toobe ustanowione.

W UserVoice, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z UserVoice, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego UserVoice](#create-a-uservoice-test-user)**  -toohave odpowiednikiem Simona Britta w UserVoice, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji UserVoice.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z UserVoice, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **UserVoice** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. Na powitania **UserVoice domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Adresy URL i domeny UserVoice pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.UserVoice.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.UserVoice.com`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta UserVoice](https://www.uservoice.com/) tooget tych wartości.

4. Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartości certyfikatu.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji UserVoice** kliknij **skonfigurować UserVoice** tooopen **Konfigurowanie logowania jednokrotnego** okna. Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfiguracja usługi UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy UserVoice tooyour jako administrator.

8. Hello pasku narzędzi u góry hello, kliknij przycisk **ustawienia**, a następnie wybierz **portalu sieci Web** hello menu.
   
    ![W sekcji Ustawienia na stronie aplikacji](./media/active-directory-saas-uservoice-tutorial/ic777519.png "ustawienia")

9. Na powitania **portalu sieci Web** na karcie hello **uwierzytelnianie użytkownika** kliknij **Edytuj** tooopen hello **Edytuj uwierzytelnianie użytkownika** okna dialogowego Strona.
   
    ![Portal sieci Web kartę](./media/active-directory-saas-uservoice-tutorial/ic777520.png "portalu sieci Web")

10. Na powitania **Edytuj uwierzytelnianie użytkownika** okna dialogowego wykonaj hello następujące kroki:
   
    ![Edytuj uwierzytelnianie użytkownika](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edytuj uwierzytelnianie użytkownika")
   
    a. Kliknij przycisk **logowanie jednokrotne (SSO)**.
 
    b. Wklej hello **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z hello portalu Azure do hello **logowania jednokrotnego zdalnego logowania** pola tekstowego.

    c. Wklej hello **Sign-Out adres URL** wartość, która została skopiowana z hello portalu Azure do hello **Sign-Out zdalnego logowania jednokrotnego textbox**.
 
    d. Wklej hello **odcisk palca** wartość, która została skopiowana z portalu Azure do **bieżącego odcisk palca certyfikatu SHA1** pola tekstowego.
    
    e. Kliknij przycisk **Zapisz ustawienia uwierzytelniania**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-uservoice-test-user"></a>Tworzenie użytkownika testowego UserVoice

toolog użytkowników tooenable usługi Azure AD w tooUserVoice, muszą mieć przydzielone do UserVoice. W przypadku hello UserVoice Inicjowanie obsługi to zadanie ręczne.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision konta użytkownika, należy wykonać hello następujące kroki:
1. Zaloguj się za tooyour **UserVoice** dzierżawy.

2. Przejdź za**ustawienia**.
   
    ![Ustawienia](./media/active-directory-saas-uservoice-tutorial/ic777811.png "ustawienia")

3. Kliknij przycisk **ogólne**.

4. Kliknij przycisk **agentów i uprawnienia**.
   
    ![Agenci i uprawnienia](./media/active-directory-saas-uservoice-tutorial/ic777812.png "agentów i uprawnień")

5. Kliknij przycisk **dodać Administratorzy**.
   
    ![Dodaj administratorów](./media/active-directory-saas-uservoice-tutorial/ic777813.png "dodać administratorów")

6. Na powitania **zaprosić Administratorzy** okna dialogowego, wykonaj następujące kroki hello:
   
    ![Zaproś Administratorzy](./media/active-directory-saas-uservoice-tutorial/ic777814.png "zaprosić Administratorzy")
   
    a. W polu tekstowym wiadomości powitania, wpisz adres e-mail hello konta hello tooprovision, a następnie kliknij przycisk **Dodaj**.
   
    b. Kliknij przycisk **zaprosić**.

> [!NOTE]
> Możesz użyć innych UserVoice użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez UserVoice tooprovision kont użytkowników usługi AAD.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooUserVoice.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooUserVoice Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **UserVoice**.

    ![łącze UserVoice Hello na liście aplikacji hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka UserVoice hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour UserVoice aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

