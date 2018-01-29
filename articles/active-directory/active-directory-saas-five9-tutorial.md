---
title: "Samouczek: Integracji Azure Active Directory z Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 7eae27ba61cf61e616bb7060ce99b3802793993f
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a>Samouczek: Integracji Azure Active Directory z Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)

W tym samouczku Dowiedz się jak zintegrować Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) z usługą Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)
- Umożliwia użytkownikom automatycznie pobrać zalogowane Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure

Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z Five9 Plus karty (CTI, skontaktuj się z Centrum agentów), potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-the-gallery"></a>Dodawanie Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) z galerii
Aby skonfigurować integrację Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) do usługi Azure AD, należy dodać Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) z galerii, wykonaj następujące czynności:**

1. W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania wpisz **Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. W panelu wyników wybierz **Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) na podstawie użytkownika testowego o nazwie "Britta Simona".

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednikiem Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) jest dla użytkownika, w usłudze Azure AD. Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi Five9 Plus karty (CTI, skontaktuj się z Centrum agentów).

W Five9 Plus karty (CTI, skontaktuj się z Centrum agentów), należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Five9 Plus karty (CTI, skontaktuj się z Centrum agentów), należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) połączonej z usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Five9 Plus karty (CTI, skontaktuj się z Centrum agentów).

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Five9 Plus karty (CTI, skontaktuj się z Centrum agentów), wykonaj następujące czynności:**

1. W portalu Azure na **Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. Na **domeny Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) i adresy URL** sekcji, wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    a. W **identyfikator** tekstowym, wpisz adres URL za pomocą następujących wzorców:

    |    Środowisko      |       Adres URL      |
    | :-- | :-- |
    | "Five9 plus karty dla programu Microsoft Dynamics CRM" | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | "Five9 plus karta Zendesk" | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | "Five9 plus karta Toolkit pulpitu agenta" | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    b. W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:

    |      Środowisko     |      Adres URL      |
    | :--                  | :--           |
    | "Five9 plus karty dla programu Microsoft Dynamics CRM" | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | "Five9 plus karta Zendesk" | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | "Five9 plus karta Toolkit pulpitu agenta" | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. Na **konfiguracji Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)** , kliknij przycisk **skonfigurować Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)** otworzyć **Konfigurowanie logowania jednokrotnego** okna. Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. Skonfigurować logowanie jednokrotne w **Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)** stronie, musisz wysłać pobrany **Certificate(Base64), adres URL Sign-Out, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [zespołem pomocy technicznej Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)](https://www.five9.com/about/contact). Również Ponadto dla dalszego Konfigurowanie logowania jednokrotnego wykonaj następujące czynności, zgodnie z karty:

    a. "Five9 Plus karta Toolkit pulpitu agenta" Przewodnik administratora: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)
    
    b. "Five9 Plus karty dla programu Microsoft Dynamics CRM" Przewodnik administratora: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)
    
    c. "Five9 Plus karta Zendesk" Przewodnik administratora: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)


> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu. Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    a. W **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a>Tworzenie użytkownika testowego Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Five9 Plus karty (CTI, skontaktuj się z Centrum agentów). Praca z [zespołem pomocy technicznej Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)](https://www.five9.com/about/contact) Aby dodać użytkowników do platformy Five9 Plus karty (CTI, skontaktuj się z Centrum agentów). Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.

### <a name="assigning-the-azure-ad-test-user"></a>Przypisanie użytkownika testowego usługi Azure AD

W tej sekcji musisz włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do Five9 Plus karty (CTI, skontaktuj się z Centrum agentów).

![Przypisz użytkownika][200] 

**Aby przypisać Simona Britta Five9 Plus karty (CTI, skontaktuj się z Centrum agentów), wykonaj następujące czynności:**

1. W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **Five9 Plus karty (CTI, skontaktuj się z Centrum agentów)**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Po kliknięciu kafelka Five9 Plus karty (CTI, skontaktuj się z Centrum agentów) w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Five9 Plus karty (CTI, skontaktuj się z Centrum agentów).
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

