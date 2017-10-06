---
title: 'Samouczek: Integracji Azure Active Directory z Veracode | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a>Samouczek: Integracji Azure Active Directory z Veracode

Z tego samouczka, dowiesz się, jak toointegrate Veracode w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Veracode zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooVeracode.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooVeracode (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Veracode należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Veracode logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodaj Veracode z galerii hello
2. Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

## <a name="add-veracode-from-hello-gallery"></a>Dodaj Veracode z galerii hello
tooconfigure hello integracji Veracode do usługi Azure AD, należy tooadd Veracode z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Veracode z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **Veracode**, wybierz pozycję **Veracode** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Veracode hello listy wyników](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Veracode w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Veracode jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Veracode musi toobe ustanowione.

W Veracode, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Veracode, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Veracode](#create-a-veracode-test-user)**  -toohave odpowiednikiem Simona Britta w Veracode, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Veracode.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Veracode, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Veracode** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. Na powitania **Veracode domeny i adres URL** sekcji, użytkownik nie ma tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooVeracode do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.

    Aplikacja Veracode oczekuje potwierdzenia SAML hello w określonym formacie wymaga tooyour mapowań atrybutów niestandardowych tooadd **atrybuty tokenu saml** konfiguracji. powitania po zrzut ekranu przedstawia przykład tego.
    
    ![Atrybuty](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "atrybutów")

6. Mapowanie atrybutów hello wymagane tooadd, wykonaj hello następujące kroki:

    | Nazwa atrybutu | Wartość atrybutu |
    |--- |--- |
    | Imię |User.givenName |
    | nazwisko |User.surname |
    | Adres e-mail |User.mail |
    
    a. Dla każdego wiersza danych w powyższej tabeli powitania kliknij **Dodaj atrybut użytkownika**.
    
    ![Atrybuty](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "atrybutów")
    
    ![Atrybuty](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "atrybutów")
    
    b. W hello **nazwa atrybutu** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.
    
    c. W hello **wartość atrybutu** pole tekstowe, wartość atrybutu hello wybierz wyświetlanego dla tego wiersza.
    
    d. Kliknij przycisk **OK**.

7. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. Na powitania **konfiguracji Veracode** kliknij **skonfigurować Veracode** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML identyfikator jednostki** z hello **sekcji krótkimi opisami.**

    ![Konfiguracja Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Veracode jako administrator.

10. W menu hello na górze hello, kliknij przycisk **ustawienia**, a następnie kliknij przycisk **administratora**.
   
    ![Administracja](./media/active-directory-saas-veracode-tutorial/ic802911.png "administracji")

11. Kliknij przycisk hello **SAML** kartę.

12. W hello **ustawienia SAML organizacji** sekcji, wykonaj następujące kroki hello:
   
    ![Administracja](./media/active-directory-saas-veracode-tutorial/ic802912.png "administracji")
   
    a.  W **wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.
    
    b. Kliknij certyfikat pobrany z portalu Azure, tooupload **wybierz plik**.
   
    c. Wybierz **umożliwić samodzielną rejestrację**.

13. W hello **ustawień rejestracji samoobsługowego** sekcji, wykonaj następujące kroki hello, a następnie kliknij przycisk **zapisać**:
   
    ![Administracja](./media/active-directory-saas-veracode-tutorial/ic802913.png "administracji")
   
    a. Jako **nowe Aktywacja użytkownika**, wybierz pozycję **wymagane uaktywnienie nr**.
   
    b. Jako **aktualizacje danych użytkownika**, wybierz pozycję **dane użytkownika Veracode preferencji**.
   
    c. Dla **szczegółów atrybutów SAML**, hello następujące czynności:
      * **Role użytkowników**
      * **Administrator zasad**
      * **Osoba dokonująca przeglądu**
      * **Realizacji zabezpieczeń**
      * **Główna programu SMS**
      * **Obiekt przesyłający**
      * **Twórcy**
      * **Wszystkie typy skanowania**
      * **Członkostwo zespołu**
      * **Domyślny zespół**

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-veracode-test-user"></a>Tworzenie użytkownika testowego Veracode
W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Veracode muszą mieć przydzielone do Veracode. W przypadku hello Veracode Inicjowanie obsługi to zadanie automatyczne. Nie ma elementu akcji dla Ciebie. Użytkownicy są tworzone automatycznie w razie potrzeby podczas hello pierwszej pojedynczego logowania jednokrotnego próby.

> [!NOTE]
> Możesz użyć innych Veracode użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Veracode tooprovision kont użytkowników usługi Azure AD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooVeracode.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooVeracode Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Veracode**.

    ![łącze Veracode Hello na liście aplikacji hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Veracode hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Veracode aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

