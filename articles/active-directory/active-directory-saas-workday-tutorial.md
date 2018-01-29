---
title: 'Samouczek: Azure Active Directory integracji z produktem Workday | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i dzień roboczy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2018
ms.author: jeedes
ms.openlocfilehash: 1dfe319e708e6a4e815413da1a7bf635f4d0a53d
ms.sourcegitcommit: 28178ca0364e498318e2630f51ba6158e4a09a89
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a>Samouczek: Azure Active Directory integracji z produktem Workday

Z tego samouczka dowiesz się integrowanie pracy z usługą Azure Active Directory (Azure AD).

Integrowanie pracy z usługą Azure AD zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do produktu Workday.
- Umożliwia użytkownikom automatycznie pobrać zalogowane do produktu Workday (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z produktem Workday, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Produktu Workday jednokrotnego włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie produktu Workday z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-workday-from-the-gallery"></a>Dodawanie produktu Workday z galerii
Aby skonfigurować integrację z produktu Workday do usługi Azure AD, należy dodać produktu Workday z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać produktu Workday z galerii, wykonaj następujące czynności:**

1. W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Przycisk usługi Azure Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.

    ![Nowy przycisk aplikacji][3]

4. W polu wyszukiwania wpisz **produktu Workday**, wybierz pozycję **produktu Workday** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.

    ![Dzień roboczy na liście wyników](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z produktu Workday w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w produktu Workday jest dla użytkownika, w usłudze Azure AD. Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w pracy.

W pracy, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z produktem Workday, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego produktu Workday](#create-a-workday-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta produktu Workday połączonego z usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji produktu Workday.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z produktem Workday, wykonaj następujące czynności:**

1. W portalu Azure na **produktu Workday** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. Na **produktu Workday domeny i adres URL** sekcji, wykonaj następujące czynności:

    ![Adresy URL i domeny WORKDAY pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    a. W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://impl.workday.com/<tenant>/login-saml2.htmld`

    b. W **identyfikator** tekstowym, wpisz adres URL:`http://www.workday.com`

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonaj następujące kroki:

    ![Adresy URL i domeny WORKDAY pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-workday-tutorial/tutorial_workday_url1.png)

    W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://impl.workday.com/<tenant>/login-saml.htmld`
     
    > [!NOTE] 
    > Wartości te nie są rzeczywistych. Rzeczywisty adres URL logowania i adres URL odpowiedzi, należy zaktualizować te wartości. Adres URL odpowiedzi muszą mieć poddomeny na przykład: www, wd2, wd3, wd3 impl, wd5, wd5 impl). Przy użyciu przypominać "*http://www.myworkday.com*" działa, ale "*http://myworkday.com*" nie ma. Skontaktuj się z [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html) uzyskać te wartości.  

5. Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)
    
7. Na **konfiguracji produktu Workday** kliknij **Konfigurowanie produktu Workday** otworzyć **Konfigurowanie logowania jednokrotnego** okna. Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**

    ![WORKDAY konfiguracji](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 

8. W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy produktu Workday.

9. W **pole wyszukiwania** wyszukiwania o nazwie **Edytuj ustawienia dzierżawy — zabezpieczeń** u góry po lewej stronie strony głównej.
   
    ![Edytuj zabezpieczenia dzierżawy](./media/active-directory-saas-workday-tutorial/IC782925.png "Edytuj zabezpieczenia dzierżawy")

10. W **adresów URL przekierowań** sekcji, wykonaj następujące czynności:
   
    ![Adresy URL przekierowania](./media/active-directory-saas-workday-tutorial/IC7829581.png "adresów URL przekierowań")
   
    a. Kliknij przycisk **Dodaj wiersz**.
   
    b. W **Przekierowywanie adresu URL logowania do** pole tekstowe i **adresem URL przekierowania Mobile** pole tekstowe, typ **adres URL logowania** zostały wprowadzone na **produktu Workday domeny i adres URL** części portalu Azure.
   
    d. W portalu Azure na **konfigurowania rejestracji** okna, kopiowania **Sign-Out adres URL**, a następnie wklej go do **adresem URL przekierowania wylogowania** pola tekstowego.

    d. W **używane dla środowisk** pole tekstowe, wybierz nazwę środowiska.  

    >[!NOTE]
    > Wartość atrybutu środowisko jest powiązany z wartością adres URL dzierżawy:  
    >— Czy nazwy domeny adresu URL dzierżawy produktu Workday rozpoczyna się od impl na przykład: *https://impl.workday.com/\<dzierżawy\>/login-saml2.htmld*), **środowiska** atrybutu należy wybrać opcję implementacji.  
    >— Jeśli nazwa domeny rozpoczynają się od czegoś innego, należy skontaktować się [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html) uzyskanie odpowiedniego **środowiska** wartość.

11. W **Instalatora SAML** sekcji, wykonaj następujące czynności:
   
    ![Instalator SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Instalatora SAML")
   
    a.  Wybierz **włączyć uwierzytelnianie SAML**.
   
    b.  Kliknij przycisk **Dodaj wiersz**.

12. W **dostawców tożsamości SAML** sekcji, wykonaj następujące czynności:
   
    ![Dostawców tożsamości SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "dostawców tożsamości SAML")
   
    a. W **Nazwa dostawcy tożsamości** tekstowym, wpisz nazwę dostawcy (na przykład: *SPInitiatedSSO*).
   
    b. W portalu Azure na **Konfigurowanie logowania jednokrotnego** okna, kopiowania **identyfikator jednostki SAML** wartość, a następnie wklej ją do **wystawcy** pola tekstowego.

    ![Dostawców tożsamości SAML](./media/active-directory-saas-workday-tutorial/IC7829271(1).png "dostawców tożsamości SAML")
   
    d. Wybierz **włączyć Workday wylogowania inicjowane**.
   
    d. W portalu Azure na **Konfigurowanie logowania jednokrotnego** okna, kopiowania **Sign-Out URL** wartość, a następnie wklej ją do **adres URL wylogowania odpowiedzi** pola tekstowego.

    e. W portalu Azure na **Konfigurowanie logowania jednokrotnego** okna, kopiowania **SAML pojedynczy znak na adres URL usługi** wartość, a następnie wklej ją do **adres URL usługi logowania jednokrotnego IdP** pola tekstowego.

    f. W **używane dla środowisk** pole tekstowe, wybierz nazwę środowiska.

    g. Kliknij przycisk **certyfikatu klucza publicznego dostawcy tożsamości**, a następnie kliknij przycisk **Utwórz**. 

    ![Utwórz](./media/active-directory-saas-workday-tutorial/IC782928.png "tworzenie")

    h. Kliknij przycisk **x509 Utwórz klucz publiczny**. 

    ![Utwórz](./media/active-directory-saas-workday-tutorial/IC782929.png "tworzenie")

13. W **klucza publicznego widoku x509** sekcji, wykonaj następujące czynności: 
   
    ![Klucz publiczny widoku x509](./media/active-directory-saas-workday-tutorial/IC782930.png "widoku x509 klucza publicznego") 
   
    a. W **nazwa** tekstowym, wpisz nazwę dla certyfikatu (na przykład: *ŚOI\_SP*).
   
    b. W **ważny od** tekstowym, wpisz poprawna wartość atrybutu certyfikatu.
   
    d.  W **ważny do** tekstowym, wpisz prawidłową wartość atrybutu certyfikatu.
   
    > [!NOTE]
    > Możesz uzyskać prawidłową z datę i poprawna data z pobranego certyfikatu, kliknij go dwukrotnie.  Daty są wyświetlane w obszarze **szczegóły** kartę.
    > 
    >
   
    d.  Otwórz w Notatniku certyfikatu zakodowanego base-64, a następnie skopiuj zawartość tego.
   
    e.  W **certyfikatu** pole tekstowe, Wklej zawartość Schowka.
   
    f.  Kliknij przycisk **OK**.

14. Wykonaj następujące czynności: 
   
    ![Konfiguracja rejestracji Jednokrotnej](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "konfiguracji logowania jednokrotnego")
   
    a.  W **identyfikator dostawcy usługi** pole tekstowe, typ **http://www.workday.com**.
   
    b. Wybierz **nie Deflate żądania uwierzytelnienia zainicjowane SP**.
   
    d. Jako **podpisu żądania uwierzytelnienia**, wybierz pozycję **SHA256**. 
   
    ![Metoda podpisu żądania uwierzytelniania](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "metoda podpisu żądania uwierzytelniania") 
   
    d. Kliknij przycisk **OK**. 
   
    ![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu. Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png)

2. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png)

3. Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.

    ![Przycisk Dodaj](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png)

4. W **użytkownika** okna dialogowego wykonaj następujące czynności:

    ![Okno dialogowe użytkownika](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png)

    a. W **nazwa** wpisz **BrittaSimon**.

    b. W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.

    d. Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-workday-test-user"></a>Tworzenie użytkownika testowego produktu Workday

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w pracy. Praca z [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html) Aby dodać użytkowników do platformy produktu Workday. Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej. 

### <a name="assign-the-azure-ad-test-user"></a>Przypisz użytkownika testowego usługi Azure AD

W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do produktu Workday.

![Przypisanie roli użytkownika][200] 

**Aby przypisać Simona Britta do produktu Workday, wykonaj następujące czynności:**

1. W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **produktu Workday**.

    ![Łącze produktu Workday na liście aplikacji](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png)  

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Łącze "Użytkownicy i grupy"][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![W okienku Dodaj przydziału][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Po kliknięciu kafelka produktu Workday w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji produktu Workday.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Zasoby dodatkowe

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

