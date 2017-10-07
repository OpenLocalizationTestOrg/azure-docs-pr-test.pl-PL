---
title: 'Samouczek: Integracji Azure Active Directory z FreshDesk | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a>Samouczek: Integracji Azure Active Directory z FreshDesk

Z tego samouczka, dowiesz się, jak toointegrate FreshDesk w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD FreshDesk zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooFreshDesk
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFreshDesk (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z FreshDesk należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- FreshDesk jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie FreshDesk z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-freshdesk-from-hello-gallery"></a>Dodawanie FreshDesk z galerii hello
tooconfigure hello integracji FreshDesk do usługi Azure AD, należy tooadd FreshDesk z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd FreshDesk z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **FreshDesk**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. W panelu wyników hello zaznacz **FreshDesk**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z FreshDesk w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w FreshDesk jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w FreshDesk musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w FreshDesk.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z FreshDesk, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego FreshDesk](#creating-a-freshdesk-test-user)**  -toohave odpowiednikiem Simona Britta w FreshDesk, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji FreshDesk.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z FreshDesk, wykonaj następujące kroki hello:**

1. W portalu zarządzania Azure hello na powitania **FreshDesk** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. Na powitania **FreshDesk domeny i adres URL** sekcji, wprowadź ciąg hello **adres URL logowania** jako: `https://<tenant-name>.freshdesk.com` lub wszelkie inne wartości Freshdesk ma sugerowane.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > Należy pamiętać, że nie jest rzeczywistą wartość. Należy zaktualizować wartości z adresem URL logowania rzeczywistych. Skontaktuj się z [zespołem pomocy technicznej klienta FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) aby zyskać tę wartość.  

4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu** , a następnie Zapisz certyfikat hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji FreshDesk** kliknij **skonfigurować FreshDesk** okna tooopen Konfigurowanie logowania jednokrotnego. Skopiuj hello SAML pojedynczy znak na adres URL usługi i adres URL Sign-Out z hello **krótkimi opisami** sekcji.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Freshdesk jako administrator.

8. W menu hello na górze hello, kliknij przycisk **Admin**.
   
   ![Administrator](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "administratora")

9. W hello **ustawienia ogólne** , kliknij pozycję **zabezpieczeń**.
   
   ![Zabezpieczenia](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "zabezpieczeń")

10. W hello **zabezpieczeń** sekcji, wykonaj następujące kroki hello:
   
    ![Jednokrotne](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "jednokrotne")
   
    a. Aby uzyskać **pojedynczy znak na rejestracji jednokrotnej (SSO)**, wybierz pozycję **na**.

    b. Wybierz **logowania jednokrotnego SAML**.

    c. Typ hello **SAML pojedynczy znak na adres URL usługi** skopiowany z portalu Azure do hello **adres URL logowania SAML** pola tekstowego.

    d. Typ hello **Sign-Out URL** skopiowany z portalu Azure do hello **adresu URL wylogowania** pole tekstowe.

    e. Kopiuj hello **odcisk palca** wartość z certyfikatu hello pobrany z portalu Azure i wklej go do hello **odcisk palca certyfikatu zabezpieczeń** pola tekstowego.  
 
    >[!TIP]
    >Aby uzyskać więcej informacji, zobacz [jak tooretrieve wartość odcisku palca certyfikatu](http://youtu.be/YKQF266SAxI). 
    
    f. Kliknij pozycję **Zapisz**.


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-freshdesk-test-user"></a>Tworzenie użytkownika testowego FreshDesk

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do FreshDesk muszą mieć przydzielone do FreshDesk.  
W przypadku hello FreshDesk Inicjowanie obsługi to zadanie ręczne.

**tooprovision kont użytkowników, wykonaj hello następujące kroki:**

1. Zaloguj się za tooyour **Freshdesk** dzierżawy.
2. W menu hello na górze hello, kliknij przycisk **Admin**.
   
   ![Administrator](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "administratora")

3. W hello **ustawienia ogólne** , kliknij pozycję **agentów**.
   
   ![Agenci](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "agentów")

4. Kliknij przycisk **nowego agenta**.
   
    ![Nowy Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "nowego agenta")

5. W oknie dialogowym informacji o agencie hello wykonaj następujące kroki hello:
   
   ![Informacji o agencie](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "informacji o agencie")
   
   a. W hello **imię i nazwisko** pole tekstowe, nazwa typu hello hello Azure AD konta tooprovision.

   b. W hello **E-mail** pole tekstowe, typ hello Azure AD adres e-mail konta usługi Azure AD hello tooprovision.

   c. W hello **tytuł** pole tekstowe, tytuł hello typu konta hello Azure AD, które ma być tooprovision.

   d. Wybierz **roli agentów**, a następnie kliknij przycisk **przypisać**.
       
   e. Kliknij pozycję **Zapisz**.     
   
    >[!NOTE]
    >Właściciel konta usługi Azure AD Hello otrzyma wiadomość e-mail zawierającą łącze tooconfirm hello konta, zanim zostanie aktywowany. 
    > 
    
    >[!NOTE]
    >Możesz użyć innych Freshdesk użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Freshdesk tooprovision kont użytkowników usługi AAD. tooFreshDesk.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooBox dostępu.

![Przypisz użytkownika][200] 

**tooassign tooFreshDesk Simona Britta wykonaj hello następujące kroki:**

1. W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **FreshDesk**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka FreshDesk hello w hello Panel dostępu, należy pobrać logowania strony tooget zalogowane tooyour FreshDesk aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

