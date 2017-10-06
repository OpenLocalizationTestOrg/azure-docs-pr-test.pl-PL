---
title: 'Samouczek: Integracji Azure Active Directory z Citrix ShareFile | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a>Samouczek: Integracji Azure Active Directory z Citrix ShareFile

Z tego samouczka, dowiesz się, jak toointegrate Citrix ShareFile w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Citrix ShareFile zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooCitrix ShareFile.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCitrix ShareFile (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z Citrix ShareFile, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Citrix ShareFile logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodaj Citrix ShareFile z galerii hello
2. Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

## <a name="add-citrix-sharefile-from-hello-gallery"></a>Dodaj Citrix ShareFile z galerii hello
tooconfigure hello integracji Citrix ShareFile do usługi Azure AD, należy tooadd Citrix ShareFile z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Citrix ShareFile z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **Citrix ShareFile**, wybierz pozycję **Citrix ShareFile** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Citrix ShareFile w hello liście wyników](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Citrix ShareFile w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Citrix ShareFile jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Citrix ShareFile musi toobe ustanowione.

W Citrix ShareFile, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Citrix ShareFile, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave odpowiednikiem Simona Britta w Citrix ShareFile, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Citrix ShareFile.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Citrix ShareFile, należy wykonać hello następujące kroki:**

1. W portalu Azure na powitania hello **Citrix ShareFile** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. Na powitania **Citrix ShareFile domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Adresy URL i domeny ShareFile Citrix pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.sharefile.com/saml/login`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta ShareFile Citrix](https://www.citrix.co.in/products/sharefile/support.html) tooget tej wartości. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. Na powitania **konfigurację serwera Citrix ShareFile** , kliknij przycisk **skonfigurować Citrix ShareFile** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfiguracja Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **Citrix ShareFile** witryny firmy jako administrator.

8. Witaj pasku narzędzi u góry hello, kliknij przycisk **Admin**.

9. Wybierz w okienku nawigacji po lewej stronie powitania **skonfigurować logowanie jednokrotne**.
   
    ![Konto administracji](./media/active-directory-saas-sharefile-tutorial/ic773627.png "konta administracji")

10. Na powitania **rejestracji jednokrotnej / Konfiguracja SAML 2.0** strony okna dialogowego, w obszarze **podstawowe ustawienia**, wykonaj następujące kroki hello:
   
    ![Logowanie jednokrotne](./media/active-directory-saas-sharefile-tutorial/ic773628.png "logowanie jednokrotne")
   
    a. Kliknij przycisk **Włącz SAML**.
    
    b. W **Your wystawcy IDP / identyfikator jednostki** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.

    c. Kliknij przycisk **zmiany** dalej toohello **certyfikatu X.509** pola, a następnie przekazywania hello certyfikat pobrany z portalu Azure hello.
    
    d. W **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.
    
    e. W **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.

11. Kliknij przycisk **zapisać** na powitania Citrix ShareFile portalu zarządzania.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-citrix-sharefile-test-user"></a>Tworzenie użytkownika testowego Citrix ShareFile

W kolejności tooenable usługi Azure AD użytkownicy toolog do Citrix ShareFile musi być przygotowana do Citrix ShareFile. W przypadku hello Citrix ShareFile Inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour **Citrix ShareFile** dzierżawy.

2. Kliknij przycisk **Zarządzanie użytkownikami \> Zarządzanie główną użytkowników \> + Tworzenie pracownika**.
   
   ![Tworzenie pracownika](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Tworzenie pracownika")

3. Na powitania **podstawowe informacje** sekcji, wykonaj następujące czynności:
   
   ![Podstawowe informacje](./media/active-directory-saas-sharefile-tutorial/IC799951.png "podstawowe informacje")
   
   a. W hello **adres E-mail** tekstowym, wpisz adres e-mail hello Simona Britta jako  **brittasimon@contoso.com** .
   
   b. W hello **imię** pole tekstowe, typ **imię** użytkownika jako **Britta**.
   
   c. W hello **nazwisko** pole tekstowe, typ **nazwisko** użytkownika jako **Simona**.

4. Kliknij przycisk **dodać użytkownika**.
  
   >[!NOTE]
   >właścicielem konta usługi Azure AD Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny. Możesz użyć innych Citrix ShareFile użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Citrix ShareFile kont użytkowników usługi Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCitrix ShareFile.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooCitrix Simona Britta ShareFile, wykonaj następujące kroki hello:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Citrix ShareFile**.

    ![Witaj Citrix ShareFile łącza na liście aplikacji hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello Citrix ShareFile kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Citrix ShareFile aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

