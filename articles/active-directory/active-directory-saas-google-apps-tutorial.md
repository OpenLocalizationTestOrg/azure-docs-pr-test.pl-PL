---
title: "Samouczek: Integracji Azure Active Directory z usługi Google Apps w usłudze Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi Google Apps."
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
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a>Samouczek: Integracji Azure Active Directory z usługi Google Apps

Z tego samouczka, dowiesz się, jak toointegrate usługi Google Apps w usłudze Azure Active Directory (Azure AD).

Integrowanie usługi Google Apps z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooGoogle aplikacji
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooGoogle aplikacji (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z usługi Google Apps należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Usługi Google Apps logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="video-tutorial"></a>Samouczek wideo
Jak tooEnable rejestracji jednokrotnej tooGoogle aplikacji w ciągu 2 minut:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a>Często zadawane pytania
1. **Pytanie: czy Chromebooks i innych urządzeniach Chrome zgodne z usługą Azure AD rejestracji jednokrotnej?**
   
    A: tak, użytkownicy będą mogli toosign do swoich urządzeń Chromebook przy użyciu swoich poświadczeń usługi Azure AD. Zobacz to [usługi Google Apps obsługuje artykułu](https://support.google.com/chrome/a/answer/6060880) informacji o tym, dlaczego użytkownicy mogą się monit o poświadczenia dwa razy.

2. **Pytanie: czy włączyć logowanie jednokrotne, użytkownicy będą się mogli toouse ich toosign poświadczeń usługi Azure AD do żadnego produktu Google, takich jak klasy Google, GMail, dysk Google, YouTube itd.?**
   
    Odpowiedź: tak, w zależności od [aplikacje, które Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) wybierz tooenable lub wyłączenia dla Twojej organizacji.

3. **Pytanie: czy można włączyć logowanie jednokrotne dla tylko podzestaw użytkowników usługi Google Apps?**
   
    A: wymaga włączenia logowania jednokrotnego natychmiast nie wszystkie Twoje aplikacje Google użytkowników tooauthenticate przy użyciu poświadczeń usługi Azure AD. Ponieważ usługi Google Apps nie obsługuje posiadanie wielu dostawców tożsamości, hello dostawcy tożsamości w danym środowisku usługi Google Apps można usługi Azure AD lub Google —, ale nie oba na powitania tym samym czasie.

4. **Pytanie: czy użytkownik jest zalogowany przy użyciu systemu Windows, czy na pewno uwierzytelniają automatycznie tooGoogle aplikacji bez pobierania zostanie wyświetlony monit o podanie hasła?**
   
    Odpowiedź: istnieją dwie opcje dotyczące włączania tego scenariusza. Najpierw użytkownicy mogą zalogować się do urządzeń z systemem Windows 10 za pomocą [usługi Azure Active Directory Join](active-directory-azureadjoin-overview.md). Alternatywnie użytkownicy mogą zalogować się do urządzeń z systemem Windows, które są przyłączone do domeny tooan lokalnej usługi Active Directory została włączona dla pojedynczego logowania jednokrotnego tooAzure AD za pomocą [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) wdrożenia. Obie te opcje wymagają tooperform hello etapami powitania po tooenable samouczka rejestracji jednokrotnej między usługą Azure AD i usługi Google Apps.

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie usługi Google Apps z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-google-apps-from-hello-gallery"></a>Dodawanie usługi Google Apps z galerii hello
tooconfigure hello integracji usługi Google Apps w usłudze Azure Active Directory, należy tooadd usługi Google Apps z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd usługi Google Apps z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **usługi Google Apps**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. W panelu wyników hello, wybierz **usługi Google Apps**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi Google Apps oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w usługi Google Apps jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w usługi Google Apps musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w usługi Google Apps.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usługi Google Apps, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego usługi Google Apps](#creating-a-google-apps-test-user)**  -toohave odpowiednikiem Simona Britta w usługi Google Apps, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne do aplikacji Google Apps.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z usługi Google Apps, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **usługi Google Apps** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. Na powitania **domenę usługi Google Apps i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://mail.google.com/a/<yourdomain>`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Zaktualizuj wartość hello z hello rzeczywisty adres URL logowania. Skontaktuj się z hello [zespołem pomocy technicznej usługi Google](https://www.google.com/contact/).
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu** , a następnie Zapisz certyfikat hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. Na powitania **Google Apps konfiguracji** kliknij **Konfigurowanie usługi Google Apps** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, SAML pojedynczy znak na adres URL usługi i zmień adres URL hasła** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. Otwórz nową kartę w przeglądarce i zaloguj się do hello [konsoli administracyjnej usługi Google Apps](http://admin.google.com/) przy użyciu konta administratora.

8. Kliknij przycisk **zabezpieczeń**. Jeśli nie widzisz hello łącza może być ukryty w obszarze hello **więcej formantów** menu u dołu hello hello ekranu.
   
    ![Kliknij pozycję Zabezpieczenia.][10]

9. Na powitania **zabezpieczeń** kliknij przycisk **Konfigurowanie rejestracji jednokrotnej (SSO).**
   
    ![Kliknij przycisk logowania jednokrotnego.][11]

10. Wykonaj hello następujące zmiany w konfiguracji:
   
    ![Konfigurowanie logowania jednokrotnego][12]
   
    a. Wybierz **Instalatora Usługa rejestracji Jednokrotnej z dostawcy tożsamości innych firm**.

    b. W **adres URL logowania strony** pola w usługi Google Apps, Wklej wartość hello **pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.

    c. W hello **adres URL strony wylogowania** pola w usługi Google Apps, Wklej wartość hello **Sign-Out adres URL**, które zostały skopiowane z portalu Azure. 

    d. W hello **zmienić adres URL hasła** pola w usługi Google Apps, Wklej wartość hello **zmienić adres URL hasła**, które zostały skopiowane z portalu Azure. 

    e. W usłudze Google Apps dla hello **certyfikatu weryfikacji**, Przekaż hello certyfikatu, który został pobrany z portalu Azure.

    f. Kliknij przycisk **zapisać zmiany**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-google-apps-test-user"></a>Tworzenie użytkownika testowego usługi Google Apps

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Google Apps oprogramowania. Usługi Google Apps obsługuje automatyczne Inicjowanie obsługi, który jest domyślnie włączone. Brak akcji można w tej sekcji. Jeśli użytkownik nie istnieje w oprogramowaniu do aplikacji Google, nowy jest tworzony podczas próby tooaccess Google Apps oprogramowania.

>[!NOTE] 
>Toocreate użytkownik ręcznie, należy skontaktować się z hello [zespołem pomocy technicznej usługi Google](https://www.google.com/contact/).

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooGoogle aplikacji.

![Przypisz użytkownika][200] 

**tooassign Simona Britta tooGoogle aplikacji, należy wykonać hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **usługi Google Apps**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji tootest pojedynczego logowania jednokrotnego ustawienia, otwórz hello panelu dostępu pod adresem [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), następnie zaloguj się do konta testowego hello i kliknij przycisk **usługi Google Apps** kafelka w hello panelu dostępu.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
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