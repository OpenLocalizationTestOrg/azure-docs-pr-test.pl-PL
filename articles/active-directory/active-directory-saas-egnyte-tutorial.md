---
title: 'Samouczek: Integracji Azure Active Directory z Egnyte | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Egnyte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a>Samouczek: Integracji Azure Active Directory z Egnyte

Z tego samouczka, dowiesz się, jak toointegrate Egnyte w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Egnyte zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooEgnyte
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooEgnyte (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Egnyte należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Egnyte logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Egnyte z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-egnyte-from-hello-gallery"></a>Dodawanie Egnyte z galerii hello
tooconfigure hello integracji Egnyte do usługi Azure AD, należy tooadd Egnyte z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Egnyte z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Egnyte**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. W panelu wyników hello zaznacz **Egnyte**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Egnyte na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Egnyte jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Egnyte musi toobe ustanowione.

W Egnyte, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Egnyte, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Egnyte](#creating-an-egnyte-test-user)**  -toohave odpowiednikiem Simona Britta w Egnyte, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Egnyte.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Egnyte, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Egnyte** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. Na powitania **Egnyte domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.egnyte.com`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) tooget tej wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Egnyte** kliknij **skonfigurować Egnyte** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Egnyte tooyour jako administrator.

8. Kliknij przycisk **ustawienia**.
   
   ![Ustawienia](./media/active-directory-saas-egnyte-tutorial/ic787819.png "ustawienia")

9. W menu powitania kliknij **ustawienia**.

   ![Ustawienia](./media/active-directory-saas-egnyte-tutorial/ic787820.png "ustawienia")

10. Kliknij przycisk hello **konfiguracji** , a następnie kliknij pozycję **zabezpieczeń**.

    ![Zabezpieczenia](./media/active-directory-saas-egnyte-tutorial/ic787821.png "zabezpieczeń")

11. W hello **uwierzytelniania rejestracji jednokrotnej** sekcji, wykonaj następujące kroki hello:

    ![Rejestracja jednokrotna na uwierzytelnianie](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Rejestracja jednokrotna dotyczących uwierzytelniania")   
    
    a. Jako **uwierzytelniania rejestracji jednokrotnej**, wybierz pozycję **SAML 2.0**.
   
    b. Jako **dostawcy tożsamości**, wybierz pozycję **AzureAD**.
   
    c. Wklej **SAML pojedynczy znak na adres URL usługi** skopiowany z portalu Azure do hello **adresu URL logowania do dostawcy tożsamości** pola tekstowego.
   
    d. Wklej **identyfikator jednostki SAML** którego została skopiowana z portalu Azure do hello **identyfikator jednostki dostawcy tożsamości** pola tekstowego.
      
    e. Otwieranie certyfikatu zakodowanego base-64 w Notatniku pobrany z portalu Azure, hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat dostawcy tożsamości** pola tekstowego.
   
    f. Jako **domyślne mapowanie użytkownika**, wybierz pozycję **adres E-mail**.
   
    g. Jako **Użyj wartości wystawcy specyficznego dla domeny**, wybierz pozycję **wyłączone**.
   
    h. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-egnyte-test-user"></a>Tworzenie użytkownika testowego Egnyte

toolog użytkowników tooenable usługi Azure AD w tooEgnyte, muszą mieć przydzielone do Egnyte. W przypadku hello Egnyte Inicjowanie obsługi to zadanie ręczne.

**tooprovision kont użytkowników, wykonaj hello następujące kroki:**

1. Zaloguj się za tooyour **Egnyte** witryny firmy jako administrator.

2. Przejdź za**ustawienia \> użytkownicy i grupy**.

3. Kliknij przycisk **Dodaj nowego użytkownika**, a następnie wybierz typ hello użytkownika ma tooadd.
   
   ![Użytkownicy](./media/active-directory-saas-egnyte-tutorial/ic787824.png "użytkowników")

4. W hello **nowego użytkownika standardowego** sekcji, wykonaj następujące kroki hello:
   
   ![Nowy użytkownik standardowy](./media/active-directory-saas-egnyte-tutorial/ic787825.png "nowego użytkownika standardowego")   

   a. Typ hello **poczty E-mail**, **Username**i inne szczegóły ma tooprovision prawidłowe konto usługi Azure Active Directory.
   
   b. Kliknij pozycję **Zapisz**.
    
    >[!NOTE]
    >Właściciel konta usługi Azure Active Directory Hello otrzymają wiadomość e-mail z powiadomieniem.
    >

>[!NOTE]
>Możesz użyć innych Egnyte użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Egnyte tooprovision kont użytkowników usługi AAD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooEgnyte.

![Przypisz użytkownika][200] 

**tooassign tooEgnyte Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Egnyte**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Egnyte hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Egnyte aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

