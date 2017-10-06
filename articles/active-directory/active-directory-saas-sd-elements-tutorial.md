---
title: 'Samouczek: Integracji Azure Active Directory z elementami SD | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i elementy SD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a>Samouczek: Integracji Azure Active Directory z elementami SD.

Z tego samouczka, dowiesz się, jak toointegrate SD elementów w usłudze Azure Active Directory (Azure AD).

Integrowanie SD elementy z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSD elementów
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSD elementy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z elementami SD, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Elementy SD logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie elementów SD z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-sd-elements-from-hello-gallery"></a>Dodawanie elementów SD z galerii hello
tooconfigure hello integracji SD elementów do usługi Azure AD, należy tooadd SD elementy z listy tooyour galerii hello zarządzanych aplikacji SaaS.

**tooadd SD elementów z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **elementy SD**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. W panelu wyników hello, wybierz **elementy SD**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z elementami SD, w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w elementach SD jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w elementach SD musi toobe ustanowione.

W elementach SD, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z elementami SD, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego elementy SD](#creating-a-sd-elements-test-user)**  -toohave odpowiednikiem Simona Britta w elementach SD, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji SD elementów.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z elementami SD, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **elementy SD** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. Na powitania **SD elementy domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    a. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.sdelements.com/sso/saml2/metadata`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.sdelements.com/sso/saml2/acs/`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości. Skontaktuj się z [elementy SD obsługują zespołu](mailto:support@sdelements.com) tooget tych wartości.

4. Elementy SD aplikacji oczekuje potwierdzenia SAML hello w określonym formacie. Skonfiguruj powitania po oświadczeń dla tej aplikacji. Można zarządzać hello wartości tych atrybutów z hello **"Użytkownika atrybutu"** kartę aplikacji hello. powitania po zrzut ekranu przedstawia przykład tego.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki: 

    | Nazwa atrybutu | Wartość atrybutu |
    | --- | --- |
    | Adres e-mail |User.mail |
    | Imię |User.givenName |
    | nazwisko |User.surname |

    a. Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    b. W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.

    c. Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.

    d. Kliknij przycisk **OK**.
 
6. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. Na powitania **SD elementy konfiguracji** kliknij **skonfigurować elementy SD** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. tooget logowanie jednokrotne włączone, skontaktuj się z Twojego [elementy SD obsługują zespołu](mailto:support@sdelements.com) i dostarczać hello pliku pobranego certyfikatu. 

10. W oknie innej przeglądarki, tooyour logowania jednokrotnego elementy SD dzierżawy z uprawnieniami administratora.

11. W menu hello na górze hello, kliknij przycisk **systemu**, a następnie **rejestracji jednokrotnej**. 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. Na powitania **ustawień rejestracji jednokrotnej** okna dialogowego, wykonaj następujące kroki hello:
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    a. Jako **typ logowania jednokrotnego**, wybierz pozycję **SAML**.
   
    b. W hello **identyfikator jednostki dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure. 
   
    c. W hello **Dostawca pojedynczego logowania jednokrotnego usługi tożsamości** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure. 
   
    d. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-sd-elements-test-user"></a>Tworzenie użytkownika testowego elementy SD.

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta SD elementów. W przypadku hello elementy SD tworzenie elementów SD użytkowników jest zadanie ręczne.

**toocreate Simona Britta w elementach SD, wykonaj hello następujące kroki:**

1. W oknie przeglądarki sieci web, witryny firmy elementy SD tooyour logowania jako administrator.

2. W menu hello na górze hello, kliknij przycisk **Zarządzanie użytkownikami**, a następnie **użytkowników**.
   
    ![Tworzenie użytkownika testowego elementy SD.](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. Kliknij przycisk **Dodaj nowego użytkownika**.
   
    ![Tworzenie użytkownika testowego elementy SD.](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. Na powitania **Dodaj nowego użytkownika** okna dialogowego, wykonaj następujące kroki hello:
   
    ![Tworzenie użytkownika testowego elementy SD.](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    a. W hello **E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .
   
    b. W hello **imię** pole tekstowe, wprowadź hello imię użytkownika, takich jak **Britta**.
   
    c. W hello **nazwisko** pole tekstowe, wprowadź hello nazwisko użytkownika, takich jak **Simona**.
   
    d. Jako **roli**, wybierz pozycję **użytkownika**. 
   
    e. Kliknij przycisk **Utwórz użytkownika**.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSD elementów.

![Przypisz użytkownika][200] 

**tooassign Simona Britta tooSD elementów, należy wykonać hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **elementy SD**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.
  
Po kliknięciu powitalne elementy SD kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SD elementy aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

