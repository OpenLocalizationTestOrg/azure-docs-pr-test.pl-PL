---
title: 'Samouczek: Integracji Azure Active Directory z IdeaScale | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: b9db921a88328c39cbf6bb4fcb6307cd77b748a5
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a>Samouczek: Integracji Azure Active Directory z IdeaScale

Z tego samouczka dowiesz się integrowanie IdeaScale z usługi Azure Active Directory (Azure AD).

Integracja z usługą Azure AD IdeaScale zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do IdeaScale
- Umożliwia użytkownikom automatycznie pobrać zalogowane do IdeaScale (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z IdeaScale, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- IdeaScale jednokrotnego włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie IdeaScale z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-ideascale-from-the-gallery"></a>Dodawanie IdeaScale z galerii
Aby skonfigurować integrację usługi Azure AD IdeaScale, należy dodać IdeaScale z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać IdeaScale z galerii, wykonaj następujące czynności:**

1. W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania wpisz **IdeaScale**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. W panelu wyników wybierz **IdeaScale**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z IdeaScale na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w IdeaScale jest dla użytkownika, w usłudze Azure AD. Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w IdeaScale musi się.

W IdeaScale, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z IdeaScale, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego IdeaScale](#creating-an-ideascale-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta IdeaScale połączonego z usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji IdeaScale.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z IdeaScale, wykonaj następujące czynności:**

1. W portalu Azure na **IdeaScale** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. Na **IdeaScale domeny i adres URL** sekcji, wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    a. W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.ideascale.com`

    b. W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości. Skontaktuj się z [zespołem pomocy technicznej klienta IdeaScale](http://support.ideascale.com/) uzyskać te wartości. 
 
4. Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. Na **konfiguracji IdeaScale** , kliknij przycisk **skonfigurować IdeaScale** otworzyć **Konfigurowanie logowania jednokrotnego** okna. Kopiuj **Sign-Out adresu URL i identyfikator jednostki SAML** z **sekcji krótkimi opisami**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy IdeaScale.

8. Przejdź do **ustawienia społeczności**.
   
    ![Ustawienia społeczności](./media/active-directory-saas-ideascale-tutorial/ic790847.png "ustawienia społeczności")

9. Przejdź do **zabezpieczeń \> pojedynczy ustawienia logować**.
   
    ![Pojedyncze ustawienia logować](./media/active-directory-saas-ideascale-tutorial/ic790848.png "pojedynczy logować ustawienia")

10. Jako **typu Pojedyncza**, wybierz pozycję **SAML 2.0**.
   
    ![Pojedynczy typ logować](./media/active-directory-saas-ideascale-tutorial/ic790849.png "pojedynczy typ logować")

11. Na **jednego ustawienia logować** okna dialogowego, wykonaj następujące czynności:
   
    ![Pojedyncze ustawienia logować](./media/active-directory-saas-ideascale-tutorial/ic790850.png "pojedynczy logować ustawienia")
   
    a. W **identyfikator jednostki IdP SAML** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.

    b. Skopiuj zawartość pliku metadanych pobranych z portalu Azure i wklej ją do **metadanych IdP SAML** pola tekstowego.

    c. W **URL Powodzenie wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL** którego została skopiowana z portalu Azure.

    d. Kliknij przycisk **zapisać zmiany**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu. Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    a. W **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-ideascale-test-user"></a>Tworzenie użytkownika testowego IdeaScale

Aby włączyć użytkowników usługi Azure AD zalogować się do IdeaScale, ich należy udostępnić w celu IdeaScale. W przypadku IdeaScale Inicjowanie obsługi to zadanie ręczne.

**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**

1. Zaloguj się do Twojego **IdeaScale** witryny firmy jako administrator.

2. Przejdź do **ustawienia społeczności**.
   
    ![Ustawienia społeczności](./media/active-directory-saas-ideascale-tutorial/ic790847.png "ustawienia społeczności")

3. Przejdź do **podstawowe ustawienia \> zarządzania elementu członkowskiego**.

4. Kliknij przycisk **dodać członka**.
   
    ![Element członkowski zarządzania](./media/active-directory-saas-ideascale-tutorial/ic790852.png "zarządzania elementu członkowskiego")

5. W sekcji Dodaj nowy element członkowski wykonaj następujące czynności:
   
    ![Dodaj nowy element członkowski](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Dodaj nowy element członkowski")
   
    a. W **adresy E-mail** tekstowym, wpisz adres e-mail prawidłowego konta usługi AAD chcesz udostępnić.
   
    b. Kliknij przycisk **zapisać zmiany**. 
   
    >[!NOTE]
    >Właściciel konta usługi Azure Active Directory pobiera wiadomość e-mail z łączem do potwierdzenia konta, zanim staje się aktywny.
      
>[!NOTE]
>Możesz użyć innych IdeaScale użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez IdeaScale do kont użytkowników usługi AAD.
 

### <a name="assigning-the-azure-ad-test-user"></a>Przypisanie użytkownika testowego usługi Azure AD

W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu IdeaScale.

![Przypisz użytkownika][200] 

**Aby przypisać Simona Britta IdeaScale, wykonaj następujące czynności:**

1. W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **IdeaScale**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej


Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Po kliknięciu kafelka IdeaScale w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji IdeaScale.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

