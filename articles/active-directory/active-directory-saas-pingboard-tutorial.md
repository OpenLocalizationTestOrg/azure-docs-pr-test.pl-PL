---
title: 'Samouczek: Integracji Azure Active Directory z Pingboard | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 008c670a8043da0c67ccefde48d5ef721c75d97c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a>Samouczek: Integracji Azure Active Directory z Pingboard

Z tego samouczka dowiesz się integrowanie Pingboard z usługi Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Pingboard zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do Pingboard
- Umożliwia użytkownikom automatycznie pobrać zalogowane do Pingboard (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z Pingboard, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Pingboard jednokrotnego włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Pingboard z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-pingboard-from-the-gallery"></a>Dodawanie Pingboard z galerii
Aby skonfigurować integrację usługi Azure AD Pingboard, należy dodać Pingboard z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać Pingboard z galerii, wykonaj następujące czynności:**

1. W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania wpisz **Pingboard**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. W panelu wyników wybierz **Pingboard**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pingboard w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Pingboard jest dla użytkownika, w usłudze Azure AD. Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Pingboard musi się.

Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Pingboard.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pingboard, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Pingboard](#creating-a-pingboard-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Pingboard połączonego z jej reprezentacji usługi Azure AD.
4. **[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji Pingboard.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Pingboard, wykonaj następujące czynności:**

1. W portalu zarządzania Azure na **Pingboard** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. Na **Pingboard domeny i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    a. W **identyfikator** tekstowym, wpisz wartość, jak:`http://<entity-id>.pingboard.com/sp`

    b. W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<entity-id>.pingboard.com/auth/saml/consume`

    > [!NOTE] 
    > Należy pamiętać, że nie są one rzeczywiste wartości. Należy zaktualizować te wartości z rzeczywistego identyfikatora i adres URL odpowiedzi. W tym miejscu zalecamy można używać unikatowej wartości ciągu w identyfikatorze. Skontaktuj się z [zespołem pomocy technicznej klienta Pingboard](https://support.pingboard.com/) uzyskać te wartości. 

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    a. W **adres URL logowania** tekstowym, wpisz wartość, jak:`http://<sub-domain>.pingboard.com/sign_in`
     
5. Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. Aby skonfigurować logowanie Jednokrotne po stronie Pingboard, Otwórz nowe okno przeglądarki i zaloguj się do swojego konta Pingboard. Musisz być administratorem Pingboard, aby skonfigurować funkcji logowania jednokrotnego.

8. Wybierz z górnego menu **aplikacji > integracji**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  Na **integracji** strony, Znajdź **"Azure Active Directory"** Kafelek, a następnie kliknij go.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. W modalne, kliknij poniżej **"Konfiguruj"**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. Na następnej stronie można zauważyć, że "Integracja z usługą Azure rejestracji Jednokrotnej jest włączona.". Otwórz pobrany plik XML metadanych w programie Notatnik i Wklej zawartość **metadanych IDP**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. Plik zostanie zweryfikowany, a jeśli wszystko jest poprawny, pojedynczy znak na zostanie ono włączone

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    a. W **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-pingboard-test-user"></a>Tworzenie użytkownika testowego Pingboard

Aby włączyć użytkowników usługi Azure AD zalogować się do Pingboard, musi być przygotowana do Pingboard.  
W przypadku Pingboard Inicjowanie obsługi to zadanie ręczne.

**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**

1. Zaloguj się do witryny firmy Pingboard jako administrator.

2. Kliknij przycisk **"Dodaj pracownika"** znajdującego się na **katalogu** strony.

    ![Dodawanie pracownika](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. Na **"Dodaj pracownika"** okna dialogowego wykonaj następujące kroki.

    ![Zaproś inne osoby](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    a. W **imię i nazwisko** tekstowym, wpisz pełną nazwę Simona Britta.

    b. W **E-mail** tekstowym, wpisz adres e-mail konta Simona Britta.

    c. W **stanowisko** tekstowym, wpisz nazwę zadania Simona Britta.

    d. W **lokalizacji** listy rozwijanej wybierz lokalizację Simona Britta.
    
    e. Kliknij pozycję **Dodaj**.   

4. Ekran potwierdzenia rozpocznie pracę, aby potwierdzić dodanie użytkownika.
    
    ![Upewnij się](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > Właścicielem konta usługi Azure Active Directory otrzymasz wiadomość e-mail, a następnie kliknij łącze, aby potwierdzić swoje konto, zanim staje się aktywny.

### <a name="assigning-the-azure-ad-test-user"></a>Przypisanie użytkownika testowego usługi Azure AD

W tej sekcji można włączyć Simona Britta do udostępnienia jej Pingboard za pomocą usługi Azure rejestracji jednokrotnej.

![Przypisz użytkownika][200] 

**Aby przypisać Simona Britta Pingboard, wykonaj następujące czynności:**

1. Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **Pingboard**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Po kliknięciu kafelka Pingboard w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Pingboard.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
