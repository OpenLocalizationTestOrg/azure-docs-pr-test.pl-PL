---
title: 'Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak skonfigurować logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a36d686ba39b5168860a20e8c4db357888df6a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a>Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH

Z tego samouczka dowiesz się integrowanie logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH w usłudze Azure Active Directory (Azure AD).

Integrowanie logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH z usługą Azure AD zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH
- Umożliwia użytkownikom automatycznie pobrać zalogowane do logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Logowania jednokrotnego SAML dla zlewiska przez rozpoznawanie jednokrotnego GmbH w subskrypcji włączone

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie logowania jednokrotnego SAML dla zlewiska przy rozdzielczości GmbH z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-the-gallery"></a>Dodawanie logowania jednokrotnego SAML dla zlewiska przy rozdzielczości GmbH z galerii

Aby skonfigurować integrację logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH do usługi Azure AD, należy dodać logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać logowania jednokrotnego SAML dla zlewiska za rozdzielczość GmbH z galerii, wykonaj następujące czynności:**

1. W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania wpisz **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. W panelu wyników wybierz **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla zlewiska przez rozdzielczość GmbH oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, jakiego odpowiednikiem użytkownika w logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH jest użytkownikiem w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH musi się.

W logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie logowania jednokrotnego SAML dla zlewiska przez użytkownika testowego GmbH rozpoznawania](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH połączonego z usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji możesz włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w sieci logowania jednokrotnego SAML dla zlewiska przy rozpoznawania GmbH aplikacji.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH, wykonaj następujące czynności:**

1. W portalu Azure na **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. Na **logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH domeny i adresów URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    a. W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`

    b. W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**. Jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Wartości te nie są prawdziwe. Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości. Skontaktuj się z [zespołu obsługi logowania jednokrotnego SAML dla zlewiska przez rozpoznawania klienta GmbH](https://www.resolution.de/go/support) uzyskać te wartości. 

5. Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **logowania jednokrotnego SAML dla zlewiska przez portal administracyjny GmbH rozpoznawania** jako administrator.

8. Umieść kursor na koło zębate, a następnie kliknij przycisk **dodatki**.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. Nastąpi przekierowanie do strony dostępu administratora. Wprowadź hasło i kliknij przycisk **Potwierdź** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. W obszarze **ATLASSIAN MARKETPLACE** , kliknij pozycję **znaleźć nowe dodatki**. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. Wyszukiwanie **SAML pojedynczy znak na rejestracji jednokrotnej (SSO) dla zlewiska** i kliknij przycisk **zainstalować** przycisk, aby zainstalować nowy wtyczki SAML.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. Uruchomi instalację dodatku. Kliknij przycisk **Zamknij**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. Kliknij pozycję **Zarządzaj**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. Kliknij przycisk **Konfiguruj** do skonfigurowania nowej wtyczki.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. Tej nowej wtyczki można także znaleźć w obszarze **użytkowników i zabezpieczenia** kartę.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. Na **konfiguracji wtyczki SingleSignOn SAML** kliknij przycisk **dodać dodatkowe dostawcy tożsamości** przycisk, aby skonfigurować ustawienia dostawcy tożsamości.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. Wykonaj następujące kroki na tej stronie:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    a. Dodaj **nazwa** dostawcy tożsamości (np. usługi Azure AD).
    
    b. Dodaj **opis** dostawcy tożsamości (np. usługi Azure AD).

    c. Kliknij przycisk **XML** i wybierz **metadanych** pliku, który został pobrany z portalu Azure.

    d. Kliknij przycisk **obciążenia** przycisku.

    e. Odczytuje metadanych IdP i wypełni pola jako wyróżnione na zrzucie ekranu. 
18. Kliknij przycisk **Zapisz ustawienia** przycisk, aby zapisać ustawienia.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu. Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    a. W **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a>Tworzenie logowania jednokrotnego SAML dla zlewiska przez użytkownika testowego GmbH rozwiązania

Aby umożliwić użytkownikom usługi Azure AD zalogowanie się do logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH, ich muszą mieć przydzielone do logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH.  
W logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH Inicjowanie obsługi to zadanie ręczne.

**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**

1. Zaloguj się do użytkownika logowania jednokrotnego SAML dla zlewiska przez witrynę firmy GmbH rozpoznawania jako administrator.

2. Umieść kursor na koło zębate, a następnie kliknij przycisk **Zarządzanie użytkownikami**.

    ![Dodawanie pracownika](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. W sekcji Użytkownicy kliknij **dodawania użytkowników** kartę. Na **"Dodaj użytkownika"** okna dialogowego strony, należy wykonać następujące czynności:

    ![Dodawanie pracownika](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    a. W **Username** tekstowym, wpisz adres e-mail użytkownika, takich jak Simona Britta.

    b. W **imię i nazwisko** tekstowym, wpisz pełną nazwę użytkownika, takich jak Simona Britta.

    c. W **E-mail** tekstowym, wpisz adres e-mail użytkownika, takich jak Brittasimon@contoso.com.

    d. W **hasło** tekstowym, wpisz hasło dla Simona Britta.

    e. Kliknij przycisk **Potwierdź hasło** wprowadź ponownie hasło.
    
    f. Kliknij przycisk **Dodaj** przycisku.    

### <a name="assigning-the-azure-ad-test-user"></a>Przypisanie użytkownika testowego usługi Azure AD

W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH.

![Przypisz użytkownika][200] 

**Aby przypisać Simona Britta logowania jednokrotnego SAML dla zlewiska rozpoznawania GmbH, wykonaj następujące czynności:**

1. W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Kliknięcie logowania jednokrotnego SAML dla zlewiska rozpoznawania GmbH kafelka w panelu dostępu, możesz powinien pobrać automatycznie zalogowane do użytkownika logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

