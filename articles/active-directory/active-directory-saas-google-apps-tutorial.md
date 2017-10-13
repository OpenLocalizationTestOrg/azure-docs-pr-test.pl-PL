---
title: "Samouczek: Integracji Azure Active Directory z usługi Google Apps w usłudze Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usługi Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 065841d6b4fe50e953f01bba4d3f23de82b82726
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a>Samouczek: Integracji Azure Active Directory z usługi Google Apps

Z tego samouczka dowiesz się Integrowanie usługi Google Apps w usłudze Azure Active Directory (Azure AD).

Integrowanie usługi Google Apps z usługą Azure AD zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do usługi Google Apps
- Umożliwia użytkownikom automatycznie pobrać zalogowane do aplikacji Google (logowanie jednokrotne) z konta usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure

Jeśli chcesz dowiedzieć się więcej informacji na temat integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z usługi Google Apps, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Usługi Google Apps logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="video-tutorial"></a>Samouczek wideo
Jak włączyć logowanie jednokrotne do aplikacji Google w ciągu 2 minut:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a>Często zadawane pytania
1. **Pytanie: czy Chromebooks i innych urządzeniach Chrome zgodne z usługą Azure AD rejestracji jednokrotnej?**
   
    Odpowiedź: tak, użytkownicy będą mogli zalogować się do swoich urządzeń Chromebook przy użyciu swoich poświadczeń usługi Azure AD. Zobacz to [usługi Google Apps obsługuje artykułu](https://support.google.com/chrome/a/answer/6060880) informacji o tym, dlaczego użytkownicy mogą się monit o poświadczenia dwa razy.

2. **Pytanie: czy włączyć logowanie jednokrotne, użytkownicy będą mogli używać swoich poświadczeń usługi Azure AD do logowania się do żadnego produktu Google, takich jak klasy Google, GMail, dysk Google, YouTube i tak dalej?**
   
    Odpowiedź: tak, w zależności od [aplikacje, które Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) chcesz włączyć lub wyłączyć w Twojej organizacji.

3. **Pytanie: czy można włączyć logowanie jednokrotne dla tylko podzestaw użytkowników usługi Google Apps?**
   
    A: wymaga włączenia logowania jednokrotnego natychmiast nie wszyscy użytkownicy usługi Google Apps do uwierzytelniania przy użyciu poświadczeń usługi Azure AD. Ponieważ usługi Google Apps nie obsługuje posiadanie wielu dostawców tożsamości, dostawca tożsamości w danym środowisku usługi Google Apps można usługi Azure AD lub Google —, ale nie oba jednocześnie.

4. **Pytanie: czy użytkownik jest zalogowany przy użyciu systemu Windows, są one automatycznie uwierzytelniania do aplikacji Google bez pobierania zostanie wyświetlony monit o podanie hasła?**
   
    Odpowiedź: istnieją dwie opcje dotyczące włączania tego scenariusza. Najpierw użytkownicy mogą zalogować się do urządzeń z systemem Windows 10 za pomocą [usługi Azure Active Directory Join](active-directory-azureadjoin-overview.md). Alternatywnie użytkownicy mogą zalogować się do urządzeń z systemem Windows, które są przyłączone do domeny do lokalnej usługi Active Directory, który został włączony dla pojedynczego logowania do usługi Azure AD za pomocą [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) wdrożenia. Obie te opcje wymagają należy wykonać czynności opisane w następujących samouczkiem, aby włączyć logowanie jednokrotne między usługą Azure AD i usługi Google Apps.

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie usługi Google Apps z galerii
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-google-apps-from-the-gallery"></a>Dodawanie usługi Google Apps z galerii
Aby skonfigurować integrację usługi Google Apps w usłudze Azure Active Directory, należy dodać usługi Google Apps z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać usługi Google Apps z galerii, wykonaj następujące czynności:**

1. W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania wpisz **usługi Google Apps**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. W panelu wyników wybierz **usługi Google Apps**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi Google Apps oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, odpowiednik użytkownika usługi Google Apps jest dla użytkownika, w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i powiązane użytkownika usługi Google Apps musi określone.

Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w usługi Google Apps.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi Google Apps, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego usługi Google Apps](#creating-a-google-apps-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta połączonego z usługi Azure AD reprezentację użytkownika usługi Google Apps.
4. **[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji Google Apps.

**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z usługi Google Apps, wykonaj następujące czynności:**

1. W portalu Azure na **usługi Google Apps** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. Na **domenę usługi Google Apps i adres URL** sekcji, wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://mail.google.com/a/<yourdomain>`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Zaktualizuj tę wartość z adresem URL logowania rzeczywistych. Skontaktuj się z [zespołem pomocy technicznej usługi Google](https://www.google.com/contact/).
 
4. Na **certyfikat podpisywania SAML** kliknij **certyfikatu** , a następnie Zapisz certyfikat na komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. Na **Google Apps konfiguracji** kliknij **Konfigurowanie usługi Google Apps** otworzyć **Konfigurowanie logowania jednokrotnego** okna. Kopiuj **Sign-Out adres URL, SAML pojedynczy znak na adres URL usługi i zmień adres URL hasła** z **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. Otwórz nową kartę w przeglądarce i zaloguj się do [konsoli administracyjnej usługi Google Apps](http://admin.google.com/) przy użyciu konta administratora.

8. Kliknij przycisk **zabezpieczeń**. Jeśli nie widzisz łącza może być ukryty w obszarze **więcej formantów** menu u dołu ekranu.
   
    ![Kliknij pozycję Zabezpieczenia.][10]

9. Na **zabezpieczeń** kliknij przycisk **Konfigurowanie rejestracji jednokrotnej (SSO).**
   
    ![Kliknij przycisk logowania jednokrotnego.][11]

10. Wykonaj następujące zmiany w konfiguracji:
   
    ![Konfigurowanie logowania jednokrotnego][12]
   
    a. Wybierz **Instalatora Usługa rejestracji Jednokrotnej z dostawcy tożsamości innych firm**.

    b. W **adres URL logowania strony** pola w usługi Google Apps, Wklej wartość **pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.

    c. W **adres URL strony wylogowania** pola w usługi Google Apps, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure. 

    d. W **zmienić adres URL hasła** pola w usługi Google Apps, Wklej wartość **zmienić adres URL hasła**, które zostały skopiowane z portalu Azure. 

    e. W usłudze Google Apps dla **certyfikatu weryfikacji**, Przekaż certyfikat, który został pobrany z portalu Azure.

    f. Kliknij przycisk **zapisać zmiany**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu. Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    a. W **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-google-apps-test-user"></a>Tworzenie użytkownika testowego usługi Google Apps

Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Google Apps oprogramowania. Usługi Google Apps obsługuje automatyczne Inicjowanie obsługi, który jest domyślnie włączone. Brak akcji można w tej sekcji. Jeśli użytkownik nie istnieje w oprogramowaniu do aplikacji Google, nowy jest tworzony podczas próby dostępu usługi Google Apps oprogramowania.

>[!NOTE] 
>Jeśli trzeba ręcznie utworzyć użytkownika, skontaktuj się z [zespołem pomocy technicznej usługi Google](https://www.google.com/contact/).

### <a name="assigning-the-azure-ad-test-user"></a>Przypisanie użytkownika testowego usługi Azure AD

W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do aplikacji Google.

![Przypisz użytkownika][200] 

**Aby przypisać Simona Britta usługi Google Apps, wykonaj następujące czynności:**

1. W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Na liście aplikacji zaznacz **usługi Google Apps**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji, aby przetestować jednego ustawienia logowania jednokrotnego, otwórz panelu dostępu pod adresem [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), następnie zaloguj się do konta testowego i kliknij przycisk **usługi Google Apps** kafelka w panelu dostępu.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Skonfiguruj Inicjowanie obsługi użytkowników](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png