---
title: "Samouczek: Integracji Azure Active Directory z chmurą Creative Adobe | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Adobe Creative chmury."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>Samouczek: Integracji Azure Active Directory z chmurą Creative Adobe

Z tego samouczka dowiesz się integrowanie Adobe Creative chmurze z usługą Azure Active Directory (Azure AD).

Integrowanie Adobe Creative chmurze z usługą Azure AD zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do programu Adobe Creative chmury
- Umożliwia użytkownikom automatycznie pobrać zalogowane Adobe Creative chmurą (logowanie jednokrotne) z konta usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z chmurą Creative Adobe, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Adobe Creative chmury jednokrotnego włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Adobe Creative chmury z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a>Dodawanie Adobe Creative chmury z galerii
Aby skonfigurować integrację Adobe Creative chmury do usługi Azure AD, należy dodać Adobe Creative chmury z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać Adobe Creative chmury z galerii, wykonaj następujące czynności:**

1. W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania wpisz **chmury Creative Adobe**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. W panelu wyników wybierz **chmury Creative Adobe**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Adobe Creative w chmurze na koncie użytkownika testu o nazwie "Britta Simona".

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w chmurze Creative Adobe jest dla użytkownika, w usłudze Azure AD. Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w chmurze Creative Adobe musi się.

Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w chmurze Creative Adobe.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z chmurą Creative Adobe, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego chmury Creative Adobe](#creating-an-adobe-creative-cloud-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Adobe Creative chmurze, która jest połączona z jej reprezentacji usługi Azure AD.
4. **[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji możesz włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne do aplikacji w chmurze Creative Adobe.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z chmurą Creative Adobe, wykonaj następujące czynności:**

1. W portalu zarządzania Azure na **chmury Creative Adobe** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. Na **adresy URL i Adobe Creative domenę chmury** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    a. W **identyfikator** tekstowym, wpisz wartość, jak:`https://www.okta.com/saml2/service-provider/<token>`

    b. W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > Należy pamiętać, że nie są one rzeczywiste wartości. Należy zaktualizować te wartości z rzeczywistego identyfikatora i adres URL odpowiedzi. W tym miejscu zalecamy można używać unikatowej wartości ciągu w identyfikatorze. Należy ręcznie utworzyć użytkownika, należy skontaktować się z zespołem pomocy technicznej Adobe Creative chmury.

4. Na **adresy URL i Adobe Creative domenę chmury** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **SP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    a. Polecenie **Pokaż zaawansowane ustawienia adresu URL** opcji

    b. W **adres URL logowania** tekstowym, wpisz wartość, jak:`https://adobe.com`

5. Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. Na **Adobe Creative konfiguracji chmury** kliknij **Konfigurowanie chmury Creative Adobe** otworzyć **konfigurowania rejestracji** okna. Skopiuj **identyfikator jednostki SAML** i **adres URL usługi logowania jednokrotnego SAML** z krótkimi opisami sekcji.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. W oknie przeglądarki innej witryny sieci web logowania z dzierżawą chmury Creative Adobe jako administrator.

8.  Przejdź do **tożsamości** w okienku nawigacji po lewej stronie i kliknij domenę. Następnie wykonaj następujące czynności na **pojedynczy znak na wymagana konfiguracja** sekcji.

    ![Ustawienia](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "ustawienia")

9. Kliknij przycisk **Przeglądaj** można przekazać certyfikatu pobrane z usługi Azure AD do **certyfikatu IDP**.

10. W **wystawcy IDP** pole tekstowe, umieścić wartość elementu **identyfikator jednostki SAML** którego skopiowany z **Konfigurowanie logowania jednokrotnego** sekcji w portalu Azure.

11. W **adres URL logowania IDP** pole tekstowe, umieścić wartość elementu **adres URL usługi logowania jednokrotnego SAML** , które zostały skopiowane z **Konfigurowanie logowania jednokrotnego** sekcji w portalu Azure.

12. Wybierz **HTTP - przekierowania** jako **powiązania IDP**.

13. Wybierz **adres E-mail** jako **ustawienia logowania użytkownika**.
 
14. Kliknij przycisk **zapisać** przycisku.

15. Pulpit nawigacyjny teraz przedstawi XML **"Pobieranie metadanych"** pliku. Zawiera adres URL EntityDescriptor Adobe i AssertionConsumerService adresu URL. Otwórz plik i skonfigurować je w aplikacji usługi Azure AD.

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    a. Użyj wartości EntityDescriptor Adobe dostarczył dla **identyfikator** na **Konfigurowanie ustawień aplikacji** okna dialogowego.

    b. Użyj wartości AssertionConsumerService Adobe dostarczył dla **adres URL odpowiedzi** na **Konfigurowanie ustawień aplikacji** okna dialogowego.
 
### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    a. W **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.

    d. Kliknij przycisk **Utwórz**. 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>Tworzenie użytkownika testowego Adobe Creative chmury

Aby włączyć użytkowników usługi Azure AD zalogować się do chmury Creative Adobe, muszą mieć przydzielone do programu Adobe Creative chmury.  
W przypadku Adobe Creative chmury Inicjowanie obsługi to zadanie ręczne.

**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**

1. Zaloguj się do witryny firmy Adobe Creative chmurze jako administrator.

2. Kliknij przycisk **osób**.

    ![Osoby](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "osób")

3. Kliknij przycisk **zaprosić użytkowników**.

    ![Zaprosić użytkowników](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "zaprosić użytkowników")

4. Na **zaprosić użytkowników** okna dialogowego strony, należy wykonać następujące czynności:

    ![Zaproś inne osoby](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Zaproś inne osoby")

    a. W **E-mail** tekstowym, wpisz adres e-mail konta Simona Britta.
    
    b. Kliknij przycisk **zaprosić**.

    > [!NOTE]
    > Właścicielem konta usługi Azure Active Directory otrzymasz wiadomość e-mail, a następnie kliknij łącze, aby potwierdzić swoje konto, zanim staje się aktywny.

### <a name="assigning-the-azure-ad-test-user"></a>Przypisanie użytkownika testowego usługi Azure AD

W tej sekcji można włączyć Simona Britta na udostępnienie jej do chmury Creative Adobe za pomocą usługi Azure rejestracji jednokrotnej.

![Przypisz użytkownika][200] 

**Aby przypisać Simona Britta Adobe Creative chmury, wykonaj następujące czynności:**

1. Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **chmury Creative Adobe**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Po kliknięciu kafelka Adobe Creative chmury w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji w chmurze Creative Adobe.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png