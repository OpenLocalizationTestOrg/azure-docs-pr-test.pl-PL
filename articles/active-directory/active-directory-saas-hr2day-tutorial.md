---
title: 'Samouczek: Integracji Azure Active Directory z HR2day przez Merces | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i HR2day przez Merces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a>Samouczek: Integracji Azure Active Directory z HR2day przez Merces

Z tego samouczka, dowiesz się, jak toointegrate HR2day przez Merces w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD HR2day przez Merces zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooHR2day przez Merces.
- Umożliwia użytkownikom tooautomatically uzyskać zalogowany tooHR2day przez Merces z konta usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji — Witaj portalu Azure.

Aby uzyskać więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z HR2day przez Merces należy hello następujące elementy:

- Subskrypcja usługi Azure AD.
- HR2day przez Merces logowanie jednokrotne włączone subskrypcji.

> [!NOTE]
> Nie zaleca się, że przy użyciu hello tootest środowiska produkcyjnego kroków w tym samouczku.

kroki hello tootest w tym samouczku, wykonaj te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Pobierz [miesięczna bezpłatna wersja próbna usługi Azure AD](https://azure.microsoft.com/pricing/free-trial/) Jeśli jeszcze nie masz.  

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello jest opisana w tym temacie składa się z dwóch głównych elementów:

1. Dodawanie HR2day przez Merces z galerii hello.
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne.

## <a name="add-hr2day-by-merces-from-hello-gallery"></a>Dodaj HR2day przez Merces z galerii hello
tooconfigure hello integracji HR2day przez Merces do usługi Azure AD, Dodaj HR2day przez Merces hello galerii tooyour listy zarządzanych aplikacji SaaS.

**tooadd HR2day przez Merces z galerii hello hello wykonaj następujące kroki:**

1. W hello [portalu Azure](https://portal.azure.com)na temat hello w lewym okienku nawigacji, wybierz hello **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nowej aplikacji, wybierz opcję hello **nowej aplikacji** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **HR2day przez Merces**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. W panelu wyników hello, wybierz **HR2day przez Merces**, a następnie wybierz hello **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HR2day przez Merces oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow, który użytkownik odpowiednikiem hello w HR2day przez Merces jest tooa użytkownika w usłudze Azure AD. Innymi słowy należy tooestablish łącza między użytkownika usługi Azure AD i hello użytkownikowi w HR2day przez Merces.

HR2day przez Merces, przypisywanie hello **nazwy użytkownika** w usłudze Azure AD za **Username** tooestablish hello relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z HR2day przez Merces, należy po bloków konstrukcyjnych hello toocomplete:

1. [Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on): Włącz toouse Twojego użytkowników tej funkcji.
2. [Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user): Test usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. [Utwórz HR2day przez użytkownika testowego Merces](#creating-an-hr2day-by-merces-test-user): tworzenie odpowiednikiem Simona Britta w HR2day przez Merces, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. [Przypisz użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user): Włącz Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. [Test rejestracji jednokrotnej](#testing-single-sign-on): Sprawdź, czy konfiguracja hello działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci HR2day przez aplikację Merces.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z HR2day przez Merces, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **HR2day przez Merces** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. tooenable logowanie jednokrotne, w hello **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego**.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. W hello **HR2day Merces domeny i adresy URL** sekcji, podjąć hello następujące kroki:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    a. W hello **adres URL logowania** wpisz adres URL przy użyciu hello następującego wzorca: `https://<tenantname>.force.com/<instancename>`.

    b. W hello **identyfikator** wpisz adres URL przy użyciu hello następującego wzorca: `https://hr2day.force.com/<companyname>`.

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z pomocą hello [HR2day przez zespół pomocy technicznej klienta Merces](mailto:servicedesk@merces.nl) tooget tych wartości. 
 


4. Na powitania **certyfikat podpisywania SAML** wybierz opcję **Certificate(Base64)**, a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. W tej sekcji opisano sposób tooenable użytkowników tooauthenticate tooHR2day przez Merces do swojego konta w usłudze Azure AD. One to robić przy użyciu Federacji opartego na powitania protokołu SAML.

    Twoje HR2day przez aplikację Merces oczekuje potwierdzenia SAML hello w określonym formacie, który wymaga tokenu SAML tooyour tooadd atrybutu niestandardowego mapowania. powitania po zrzut ekranu przedstawia przykład. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    Aby można było skonfigurować potwierdzenia języka SAML hello, musisz skontaktować się z hello [HR2day przez zespół pomocy technicznej klienta Merces](mailto:servicedesk@merces.nl) i zażądać hello wartość hello atrybut identyfikator unikatowy dla dzierżawy. Należy to wartość toocomplete hello kroki opisane w następnej sekcji hello. 

6. W hello **logowanie jednokrotne** okno dialogowe, w hello **atrybuty użytkownika** skonfiguruj atrybut tokenu SAML hello, jak pokazano w powitania po obrazu. Wykonaj następujące kroki hello.
    
      | Nazwa atrybutu    |   Wartość atrybutu |  
    | ------------------- | -------------------- |    
    | ATTR_LOGINCLAIM | sprzężenia ([poczty] "102938475Z", "@" |
    
      a. Witaj tooopen **Dodawanie atrybutu** okno dialogowe, wybierz opcję **Dodaj atrybut**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    b. W hello **nazwa** wpisz **ATTR_LOGINCLAIM**.

    c. Z hello **wartość** listy, wybierz **Join()**.

    d. Z hello **ciąg1** listy, wybierz **user.mail**.

    e. Aby uzyskać **ciąg2**, hello unikatowego identyfikatora dostarczonego przez zespół HR2day.

    f. W hello **separatora** wpisz  **@** .
    
    g. Wybierz **Ok**.

7. Wybierz hello **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. W hello **HR2day przez konfigurację Merces** zaznacz **skonfigurować HR2day przez Merces** tooopen hello **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL**, **SAML identyfikator jednostki**, i **SAML pojedynczy znak na adres URL usługi** z hello **krótki przewodnik** sekcji.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. tooconfigure logowania jednokrotnego dla twojej aplikacji, skontaktuj się z hello [HR2day przez zespół pomocy technicznej klienta Merces](mailTo:servicedesk@merces.nl). Dołącz hello pobrane **Certificate(Base64)** pliku tooyour wiadomości e-mail. Udostępniają hello **Sign-Out URL**, **identyfikator jednostki SAML**, i **SAML pojedynczy znak na adres URL usługi** tak, aby można je skonfigurować integracji logowania jednokrotnego.

    > [!NOTE]
    >Wspomina toohello Merces zespół, który wymaga tej integracji hello toobe identyfikator jednostki ustawiony za pomocą wzorca hello **https://hr2day.force.com/INSTANCENAME**.

    > [!TIP]
    >Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory** > **aplikacje dla przedsiębiorstw** sekcji, wybierz hello **rejestracji jednokrotnej** kartę. Witaj dostęp osadzone dokumentacji za pośrednictwem hello **konfiguracji** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w hello [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, hello wykonaj następujące kroki:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, wybierz hello **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie wybierz **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** wybierz pozycję **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. W hello **użytkownika** okno dialogowe, hello wykonaj następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** okno, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło**, a następnie Zapisz hasło hello.

    d. Wybierz pozycję **Utwórz**.
 
### <a name="create-an-hr2day-by-merces-test-user"></a>Utwórz HR2day przez Merces użytkownika testowego

Celem Hello w tej sekcji jest toocreate użytkownik wywołał Simona Britta w HR2day Merces. Użytkownicy hello tooadd na koncie hello HR2day pracować z hello [HR2day przez zespół pomocy technicznej klienta Merces](mailto:servicedesk@merces.nl). 

> [!NOTE]
> Toocreate użytkownik ręcznie, należy skontaktować się z hello [HR2day przez zespół pomocy technicznej klienta Merces](mailto:servicedesk@merces.nl).

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji zostanie włączone, przyznając jej tooHR2day dostępu przez Merces toouse Simona Britta Azure rejestracji jednokrotnej.

![Przypisz użytkownika][200] 

**tooassign tooHR2day Simona Britta przez Merces, hello wykonaj następujące kroki:**

1. W hello Azure aplikacji hello portalu, otwórz wyświetlić, przejdź do widoku katalogu toohello, a następnie przejdź zbyt**aplikacje dla przedsiębiorstw**. Następnie wybierz pozycję **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **HR2day przez Merces**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. W menu hello powitania po lewej stronie wybierz **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Wybierz hello **Dodaj** przycisku. Następnie w hello **Dodaj przydziału** okno dialogowe, wybierz opcję **użytkowników i grup**.

    ![Przypisz użytkownika][203]

5. W hello **użytkowników i grup** okno dialogowe, w hello **użytkowników** listy, wybierz **Simona Britta**.

6. Kliknij przycisk hello **wybierz** przycisku.

7. W hello **Dodaj przydziału** okno dialogowe, wybierz opcję **przypisać**.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

Witaj celem tej sekcji jest tootest konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.  

Po wybraniu hello HR2day przez Kafelek Merces w panelu dostępu hello automatycznie pobrać zalogowano tooyour HR2day przez aplikację Merces.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

