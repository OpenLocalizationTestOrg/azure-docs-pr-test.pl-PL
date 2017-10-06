---
title: 'Samouczek: Integracji Azure Active Directory z TargetProcess | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i TargetProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a>Samouczek: Integracji Azure Active Directory z TargetProcess

Z tego samouczka, dowiesz się, jak toointegrate TargetProcess w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD TargetProcess zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTargetProcess
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTargetProcess (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z TargetProcess należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- TargetProcess logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodaj TargetProcess z galerii hello
2. Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

## <a name="add-targetprocess-from-hello-gallery"></a>Dodaj TargetProcess z galerii hello
tooconfigure hello integracji TargetProcess do usługi Azure AD, należy tooadd TargetProcess z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd TargetProcess z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **TargetProcess**, wybierz pozycję **TargetProcess** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Dodaj TargetProcess z galerii](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TargetProcess w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w TargetProcess jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w TargetProcess musi toobe ustanowione.

W TargetProcess, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z TargetProcess, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego TargetProcess](#create-a-targetprocess-test-user)**  -toohave odpowiednikiem Simona Britta w TargetProcess, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji TargetProcess.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z TargetProcess, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **TargetProcess** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Na podstawie SAML logowania jednokrotnego](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. Na powitania **TargetProcess domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Sekcja TargetProcess domeny i adresy URL](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.tpondemand.com/`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.tpondemand.com/`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta TargetProcess](mailto:support@targetprocess.com) tooget tych wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Przyciskiem Zapisz](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji TargetProcess** kliknij **skonfigurować TargetProcess** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Sekcja konfiguracji TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. Zaloguj się na tooyour TargetProcess aplikacji jako administrator.

8. W menu hello na górze hello, kliknij przycisk **Instalatora**.
   
    ![Konfiguracja](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. Kliknij przycisk **ustawienia**.
   
    ![Ustawienia](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. Kliknij przycisk **logowanie jednokrotne**.
   
    ![Kliknij przycisk rejestracji jednokrotnej](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. Na powitania rejestracji jednokrotnej okno dialogowe Ustawienia należy wykonać hello następujące kroki:
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    a. Kliknij przycisk **Włącz rejestrację jednokrotną**.
    
    b. W **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.

    c. Otwórz pobrany certyfikat w Notatniku, hello kopiowania zawartości, a następnie wklej go do hello **certyfikatu** pola tekstowego.
    
    d. Kliknij przycisk **włączyć udostępniania JIT**.

    e. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![toodisplay hello listę użytkowników](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Dodawanie przycisku](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Sekcja użytkownika](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-targetprocess-test-user"></a>Tworzenie użytkownika testowego TargetProcess

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w TargetProcess.

TargetProcess obsługę w czasie. Została już włączona w [Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on).

Nie ma elementu akcji można w tej sekcji.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTargetProcess.

![Przypisz użytkownika][200] 

**tooassign tooTargetProcess Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **TargetProcess**.

    ![TargetProcess listy aplikacji](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.

Po kliknięciu powitalne TargetProcess kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour TargetProcess aplikacji. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

