---
title: 'Samouczek: Integracji Azure Active Directory z Druva | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a>Samouczek: Integracji Azure Active Directory z Druva

Z tego samouczka, dowiesz się, jak toointegrate Druva w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Druva zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooDruva.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooDruva (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Druva należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Druva logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Druva z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-druva-from-hello-gallery"></a>Dodawanie Druva z galerii hello
tooconfigure hello integracji Druva do usługi Azure AD, należy tooadd Druva z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Druva z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **Druva**, wybierz pozycję **Druva** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Druva hello listy wyników](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Druva w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Druva jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Druva musi toobe ustanowione.

W Druva, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Druva, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Druva](#create-a-druva-test-user)**  -toohave odpowiednikiem Simona Britta w Druva, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Druva.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Druva, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Druva** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. Na powitania **Druva domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello:`https://cloud.druva.com/home`

4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. Aplikacja Druva oczekuje potwierdzenia SAML hello w określonym formacie wymaga tooyour mapowań atrybutów niestandardowych tooadd **atrybuty tokenu SAML** konfiguracji. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, Konfigurowanie atrybutu tokenu SAML, jak pokazano w hello poprzedzających obrazu i wykonywanie hello następujące kroki:

    | Nazwa atrybutu      | Wartość atrybutu      |
    | ------------------- | -------------------- |
    | zsynchronizowana\_uwierzytelniania\_tokenu |Wprowadź wartość tokenu wygenerowanego hello |
    
    a. Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    b. W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.

    c. Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza. tłumaczy wartość tokenu wygenerowanego Hello później w samouczku.
    
    d. Kliknij przycisk **OK**.    

7. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. Na powitania **konfiguracji Druva** kliknij **skonfigurować Druva** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Druva tooyour jako administrator.

10. Przejdź za**Zarządzaj \> ustawienia**.

    ![Ustawienia](./media/active-directory-saas-druva-tutorial/ic795091.png "ustawienia")

11. W oknie dialogowym Ustawienia rejestracji jednokrotnej hello wykonaj następujące kroki hello:

    ![Single Sign-On ustawienia](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On ustawienia")
    
    a. Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z hello portalu Azure do hello **adres URL logowania dostawcy identyfikator** pola tekstowego.
    
    b. Wklej **Sign-Out URL** wartość, która została skopiowana z hello portalu Azure do hello **adres URL wylogowania dostawcy identyfikator** pola tekstowego.
    
     c. Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat dostawcy identyfikator** pole tekstowe
     
     d. Witaj tooopen **ustawienia** kliknij przycisk **zapisać**.

12. Na powitania **ustawienia** kliknij przycisk **generowania tokenu rejestracji Jednokrotnej**.

    ![Ustawienia](./media/active-directory-saas-druva-tutorial/ic795093.png "ustawienia")

13. Na powitania **pojedynczego logowania jednokrotnego tokenu uwierzytelniania** okna dialogowego, wykonaj następujące kroki hello:

    ![Token rejestracji Jednokrotnej](./media/active-directory-saas-druva-tutorial/ic795094.png "tokenu rejestracji Jednokrotnej")
    
    a. Kliknij przycisk **kopiowania**, wklej skopiowane wartość hello **wartość** textbox w hello **Dodawanie atrybutu** sekcji.
    
    b. Kliknij przycisk **Zamknij**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-druva-test-user"></a>Tworzenie użytkownika testowego Druva

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w tooDruva muszą mieć przydzielone do Druva. W przypadku hello Druva Inicjowanie obsługi to zadanie ręczne.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. Zaloguj się za tooyour **Druva** witryny firmy jako administrator.

2. Przejdź za**Zarządzaj \> użytkowników**.
   
   ![Zarządzaj użytkownikami](./media/active-directory-saas-druva-tutorial/ic795097.png "Zarządzanie użytkownikami")

3. Kliknij przycisk **tworzenia nowych**.
   
   ![Zarządzaj użytkownikami](./media/active-directory-saas-druva-tutorial/ic795098.png "Zarządzanie użytkownikami")

4. W oknie dialogowym Tworzenie nowego użytkownika hello wykonaj następujące kroki hello:
   
   ![Utwórz NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "utworzyć NewUser")
   
   a. W hello **adres E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .
   
   b. W hello **nazwa** pole tekstowe, wprowadź nazwę użytkownika, takie jak hello **BrittaSimon**.
   
   c. Kliknij przycisk **Utwórz użytkownika**.

>[!NOTE]
>Możesz użyć innych Druva użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Druva tooprovision kont użytkowników usługi Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooDruva.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooDruva Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Druva**.

    ![łącze Druva Hello na liście aplikacji hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Druva hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Druva aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

