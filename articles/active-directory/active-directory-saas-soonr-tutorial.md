---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy Soonr | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Soonr w miejscu pracy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a>Samouczek: Integracji Azure Active Directory z Soonr w miejscu pracy

Celem tego samouczka jest pokazanie sposobu integracji Soonr miejsca pracy z usługą Azure Active Directory (Azure AD).  
Integrowanie Soonr miejsca pracy z usługą Azure AD zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do miejsca pracy Soonr
- Umożliwia użytkownikom automatycznie pobrać zalogowane Soonr w miejscu pracy (logowanie jednokrotne) z konta usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - klasycznego portalu Azure

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z miejsca pracy Soonr, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Obszar roboczy Soonr jednokrotnego włączone subskrypcji


> [!NOTE] 
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.


Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Opis scenariusza
Celem tego samouczka jest umożliwienie umożliwia testowanie usługi Azure AD rejestracji jednokrotnej w środowisku testowym.  
Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie miejsca pracy Soonr z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne


## <a name="adding-soonr-workplace-from-the-gallery"></a>Dodawanie miejsca pracy Soonr z galerii
Aby skonfigurować integrację usługi Azure AD Soonr w miejscu pracy, należy dodać Soonr miejsca pracy z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać miejsce pracy Soonr z galerii, wykonaj następujące czynności:**

1. W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**. 

    ![Usługa Active Directory][1]

2. Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.

3. Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.

    ![Aplikacje][2]

4. Kliknij przycisk **Dodaj** w dolnej części strony.

    ![Aplikacje][3]

5. Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.
 
    ![Aplikacje][4]

6. W polu wyszukiwania wpisz **pracy Soonr**.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. W okienku wyników wybierz **pracy Soonr**, a następnie kliknij przycisk **Complete** można dodać aplikację.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
Celem tej sekcji jest, jak skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Soonr w miejscu pracy na podstawie użytkownika testowego o nazwie "Britta Simona".

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, co jest odpowiednikiem użytkownikowi w miejscu pracy Soonr użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w miejscu pracy Soonr musi określone.  

Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w miejscu pracy Soonr.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z miejsca pracy Soonr, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego pracy Soonr](#creating-a-soonr-workplace-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Soonr miejsca pracy, połączonej z jej reprezentacji usługi Azure AD.
4. **[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w klasycznym portalu i skonfigurować logowanie jednokrotne w miejscu pracy Soonr aplikacji.


**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z miejsca pracy Soonr, wykonaj następujące czynności:**

1. W klasycznym portalu Azure na **Soonr pracy** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować logowanie jednokrotne** okna dialogowego.

    ![Konfigurowanie rejestracji jednokrotnej][6] 

2. Na **jak chcesz użytkownikom zalogować do miejsca pracy Soonr** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. Na **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj następujące kroki:.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    a. W **na adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.

    b. Kliknij przycisk **Dalej**.

    > [!NOTE] 
    > Należy pamiętać, że nie jest rzeczywistą wartość. Należy zaktualizować tę wartość rzeczywista logowania na adres URL. Skontaktuj się z zespołem pomocy technicznej Soonr w miejscu pracy, aby zyskać tę wartość.

4. Na **skonfigurować logowanie jednokrotne w miejscu pracy Soonr** kliknij przycisk **pobierania metadanych** , a następnie zapisz plik na komputerze:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z zespołem pomocy technicznej Soonr w miejscu pracy i podaj następujące: 

    • Pobrany **metadanych** pliku

    • **Adres URL wystawcy**

    • **Adres URL logowania jednokrotnego SAML**

    • **Pojedynczy adres URL wylogowania usługi**

    >[!NOTE]
    >Ta aplikacja została zastąpiona nowszą <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">pracy Autotask</a> i może odnosić się <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">to</a> samouczka do konfigurowania aplikacji z usługą Azure AD.
   
6. W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **dalej**.

    ![Azure AD rejestracji jednokrotnej][10]

7. Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.  
  
    ![Azure AD rejestracji jednokrotnej][11]



### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem tej sekcji jest tworzenie użytkownika testowego w klasycznym portalu Azure o nazwie Simona Britta.  

![Tworzenie użytkowników usługi Azure AD][20]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.

3. Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. Na **Poinformuj nas o tym użytkowniku** okna dialogowego strony, należy wykonać następujące czynności:

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    a. Jako typ użytkownika wybierz nowego użytkownika w organizacji.

    b. W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.

    c. Kliknij przycisk **Dalej**.

6.  Na **profilu użytkownika** okna dialogowego strony, należy wykonać następujące czynności:

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    a. W **imię** pole tekstowe, typ **Britta**.  

    b. W **nazwisko** pole tekstowe, typ **Simona**.

    c. W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.

    d. W **roli** listy, wybierz **użytkownika**.

    e. Kliknij przycisk **Dalej**.

7. Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    a. Zanotuj wartość **nowe hasło**.

    b. Kliknij przycisk **Complete** (Zakończ).   



### <a name="creating-a-soonr-workplace-test-user"></a>Tworzenie użytkownika testowego Soonr w miejscu pracy

Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w miejscu pracy Soonr. Należy skontaktować się z zespołem pomocy technicznej Soonr w miejscu pracy, aby utworzyć użytkownika na platformie. Można zwiększyć biletu pomocy technicznej z Soonr z <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">tutaj</a>.


### <a name="assigning-the-azure-ad-test-user"></a>Przypisanie użytkownika testowego usługi Azure AD

Celem tej sekcji jest włączenie Simona Britta na udostępnienie jej do miejsca pracy Soonr za pomocą usługi Azure rejestracji jednokrotnej.

![Przypisz użytkownika][200] 

**Aby przypisać Simona Britta Soonr w miejscu pracy, wykonaj następujące czynności:**

1. W klasycznym portalu Azure, aby otworzyć widok aplikacji, w widoku katalogu, kliknij polecenie **aplikacji** w menu u góry.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **pracy Soonr**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. W menu u góry kliknij **użytkowników**.

    ![Przypisz użytkownika][203] 

1. Na liście użytkowników wybierz **Simona Britta**.

2. Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.

    ![Przypisz użytkownika][205]



### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.  
Po kliknięciu kafelka Soonr w miejscu pracy, w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do miejsca pracy Soonr aplikacji.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
