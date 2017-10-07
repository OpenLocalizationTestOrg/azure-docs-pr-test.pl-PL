---
title: 'Samouczek: Integracji Azure Active Directory z Samanage | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Samanage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a>Samouczek: Integracji Azure Active Directory z Samanage

Z tego samouczka, dowiesz się, jak toointegrate Samanage w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Samanage zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSamanage
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSamanage (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Samanage należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Samanage logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Samanage z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-samanage-from-hello-gallery"></a>Dodawanie Samanage z galerii hello
tooconfigure hello integracji Samanage do usługi Azure AD, należy tooadd Samanage z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Samanage z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Samanage**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. W panelu wyników hello zaznacz **Samanage**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Samanage w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Samanage jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Samanage musi toobe ustanowione.

W Samanage, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Samanage, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Samanage](#creating-a-samanage-test-user)**  -toohave odpowiednikiem Simona Britta w Samanage, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Samanage.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Samanage, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Samanage** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. Na powitania **Samanage domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<Company Name>.samanage.com/saml_login/<Company Name>`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<Company Name>.samanage.com`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Witaj rzeczywisty adres URL logowania i identyfikator, który znajduje się w dalszej części samouczka hello, należy zaktualizować te wartości. Więcej informacji skontaktuj się z [zespołem pomocy technicznej klienta Samanage](https://www.samanage.com/support).    
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Samanage** kliknij **skonfigurować Samanage** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopia hello **Sign-Out adresu URL i identyfikator jednostki SAML** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Samanage jako administrator.

8. Kliknij przycisk **pulpitu nawigacyjnego** i wybierz **Instalator** w lewym okienku nawigacji.
   
    ![Pulpit nawigacyjny](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "pulpitu nawigacyjnego")

9. Kliknij przycisk **logowanie jednokrotne**.
   
    ![Logowanie jednokrotne](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "logowanie jednokrotne")

10. Przejdź za**logowania za pomocą protokołu SAML** sekcji, wykonaj następujące kroki hello:
   
    ![Zaloguj się przy użyciu SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "logowania za pomocą protokołu SAML")
 
    a. Kliknij przycisk **włączyć logowanie jednokrotne z SAML**.  
 
    b. W hello **adres URL dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.    
 
    c. Potwierdź hello **adres URL logowania** hello dopasowań **na adres URL logowania** z **Samanage domeny i adres URL** sekcji w portalu Azure.
 
    d. W hello **adresu URL wylogowania** pole tekstowe, wprowadź wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.
 
    e. W hello **wystawcy SAML** pole tekstowe, ustawiony typ hello aplikacji identyfikator URI w dostawcy tożsamości.
 
    f. Otwórz base-64 zakodowany certyfikat pobrany z portalu Azure w programie Notatnik hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **Wklej dostawcy tożsamości x.509 szyfrowany poniżej certyfikat** pola tekstowego.
 
    g. Kliknij przycisk **tworzenie użytkowników, jeśli nie istnieją w Samanage**.
 
    h. Kliknij przycisk **aktualizacji**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-samanage-test-user"></a>Tworzenie użytkownika testowego Samanage

toolog użytkowników tooenable usługi Azure AD w tooSamanage, muszą mieć przydzielone do Samanage.  
W przypadku hello Samanage Inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się do witryny firmy Samanage jako administrator.

2. Kliknij przycisk **pulpitu nawigacyjnego** i wybierz **Instalator** w przesuwanie nawigacji po lewej stronie.
   
    ![Instalator](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Instalatora")

3. Kliknij przycisk hello **użytkowników** kartę
   
    ![Użytkownicy](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "użytkowników")

4. Kliknij przycisk **nowego użytkownika**.
   
    ![Nowy użytkownik](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "nowego użytkownika")

5. Typ hello **nazwa** i hello **adres E-mail** konta usługi Azure Active Directory tooprovision i kliknij **tworzenia użytkownika**.
   
    ![Utwórz użytkownika](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Tworzenie użytkownika")
   
   >[!NOTE]
   >właścicielem konta usługi Azure Active Directory Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny. Możesz użyć innych Samanage użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Samanage usługi Azure Active Directory kont użytkowników.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSamanage.

![Przypisz użytkownika][200] 

**tooassign tooSamanage Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Samanage**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Samanage hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Samanage aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

