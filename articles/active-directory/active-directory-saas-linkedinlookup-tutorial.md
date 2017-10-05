---
title: 'Samouczek: Integracji Azure Active Directory z wyszukiwania LinkedIn | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i LinkedIn wyszukiwania."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e296431866a8611b30e72f286884890adf0f7e50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a>Samouczek: Integracji Azure Active Directory z LinkedIn wyszukiwania

W tym samouczku Dowiedz się jak integracji LinkedIn wyszukiwania w usłudze Azure Active Directory (Azure AD).

Integrowanie wyszukiwania LinkedIn z usługą Azure AD zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do wyszukiwania LinkedIn
- Umożliwia użytkownikom automatycznie pobrać zalogowane do wyszukiwania LinkedIn (logowanie jednokrotne) z konta usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z LinkedIn wyszukiwania, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Wyszukiwanie LinkedIn jednokrotnego włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie wyszukiwania LinkedIn z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-linkedin-lookup-from-the-gallery"></a>Dodawanie wyszukiwania LinkedIn z galerii
Aby skonfigurować integrację LinkedIn wyszukiwania w usłudze Azure Active Directory, należy dodać wyszukiwania LinkedIn z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać wyszukiwania LinkedIn z galerii, wykonaj następujące czynności:**

1. W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego, aby dodać nową aplikację.

    ![Aplikacje][3]

4. W polu wyszukiwania wpisz **wyszukiwania LinkedIn**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. W panelu wyników wybierz **wyszukiwania LinkedIn**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z LinkedIn wyszukiwania w oparciu o nazwie "Britta Simona" użytkownika testowego.

Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednikiem LinkedIn odnośnika do użytkownika w usłudze Azure AD. Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w wyszukiwaniu LinkedIn.

Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** odnośnika LinkedIn.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LinkedIn wyszukiwania, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego wyszukiwania LinkedIn](#creating-an-linkedin-lookup-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta LinkedIn wyszukiwania, które jest połączone z reprezentacją usługi Azure AD.
4. **[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji wyszukiwania LinkedIn.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z LinkedIn wyszukiwania, wykonaj następujące czynności:**

1. W portalu Azure na **wyszukiwania LinkedIn** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okna dialogowego, w **tryb** wybierz **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. W oknie przeglądarki sieci web inną logowania jednokrotnego w sieci **wyszukiwania LinkedIn** witryny sieci Web jako administrator.

4. W **Centrum konta**, kliknij przycisk **ustawienia globalne** w obszarze **ustawienia**. Zaznacz również **wyszukiwania** z listy rozwijanej.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. Kliknij przycisk **lub kliknij tutaj, aby załadować i skopiuj poszczególnych pól w formularzu** i skopiuj **identyfikator jednostki** i **adresu Url potwierdzenia konsumenta dostępu (ACS)**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. W portalu Azure w obszarze **domeny wyszukiwania LinkedIn i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    a. W **identyfikator** pole tekstowe, wprowadź **identyfikator jednostki** skopiowany z portalu LinkedIn 

    b. W **adres URL odpowiedzi** pole tekstowe, wprowadź **potwierdzenia konsumenta dostępu (ACS) adres Url** skopiowany z portalu LinkedIn

7. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`
     
    > [!NOTE] 
    > To nie jest rzeczywistą wartość. Użytkownik musi zaktualizować te wartości z adresem URL logowania rzeczywistych. Skontaktuj się z [zespołem pomocy technicznej klienta wyszukiwania LinkedIn](https://business.LinkedIn.com/lookup) aby zyskać tę wartość.

8. Twoje **wyszukiwania LinkedIn** aplikacji oczekuje potwierdzenia języka SAML w określonym formacie. Użytkownik ma dodanie mapowań atrybutów niestandardowych do konfiguracji atrybuty tokenu SAML. Poniższy zrzut ekranu przedstawia przykład. Wartość domyślna **identyfikator użytkownika** jest **user.userprincipalname** , ale wyszukiwania LinkedIn oczekuje to być mapowane z adresu e-mail użytkownika. Można użyć **user.mail** atrybutu z listy lub użyj wartości atrybutu odpowiednie na podstawie konfiguracji organizacji. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustawić atrybutów. Użytkownik chce dodać cztery oświadczeń o nazwie **e-mail**, **działu**, **imię**, i **nazwisko** i wartość ma być zmapowana z **user.mail**, **user.department**, **user.givenname**, i **user.surname** odpowiednio

    | Nazwa atrybutu | Wartość atrybutu |
    | --- | --- |
    | Adres e-mail| User.mail |    
    | Dział| User.Department |
    | Imię| User.givenName |
    | nazwisko| User.surname |

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    a. Kliknij przycisk **Dodawanie atrybutu** otworzyć **Dodawanie atrybutu** okna dialogowego.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    b. W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.
    
    c. Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.
    
    d. Kliknij przycisk **Ok**

10. Wykonaj następujące czynności na **nazwa** — atrybut

    a. Kliknij ten atrybut można otworzyć **atrybutu Edytuj** okna.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    b. Usuń wartość adresu URL z **przestrzeni nazw**.
    
    c. Kliknij przycisk **Ok** Aby zapisać ustawienia.

10. Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. Przejdź do **ustawienia administratora LinkedIn** sekcji. Przekaż plik XML został pobrany z portalu Azure, klikając **pliku XML, Przekaż** opcji.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. Kliknij przycisk **na** do włączenia funkcji logowania jednokrotnego. Zmiany stanu rejestracji Jednokrotnej z **niepołączone** do **połączony**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu. Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. Kliknij przycisk **Dodaj** otworzyć **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    a. W **nazwa** pole tekstowe, typ **Simona Britta**.

    b. W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z Simona Britta.

    c. Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-linkedin-lookup-test-user"></a>Tworzenie użytkownika testowego LinkedIn wyszukiwania

Połączonej aplikacji wyszukiwania obsługuje tylko w czasie (JIT) Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji. Aktywuj **automatycznie przypisać licencje** przypisać licencję do użytkownika.
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-the-azure-ad-test-user"></a>Przypisanie użytkownika testowego usługi Azure AD

W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do wyszukiwania LinkedIn.

![Przypisz użytkownika][200] 

**Aby przypisać Simona Britta LinkedIn wyszukiwania, wykonaj następujące czynności:**

1. W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **wyszukiwania LinkedIn**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.

    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Po kliknięciu kafelka LinkedIn wyszukiwania w panelu dostępu, powinien być przekierowany do strony organizacji, gdzie należy podać informacje osobowe konta LinkedIn. Łączy konto osobiste konta firmowego LinkedIn. 

Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

