---
title: 'Samouczek: Integracji Azure Active Directory z Panorama9 | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a>Samouczek: Integracji Azure Active Directory z Panorama9

Z tego samouczka, dowiesz się, jak toointegrate Panorama9 w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Panorama9 zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPanorama9
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPanorama9 (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Panorama9 należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Panorama9 logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Panorama9 z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-panorama9-from-hello-gallery"></a>Dodawanie Panorama9 z galerii hello
tooconfigure hello integracji Panorama9 do usługi Azure AD, należy tooadd Panorama9 z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Panorama9 z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Panorama9**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. W panelu wyników hello zaznacz **Panorama9**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Panorama9 na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Panorama9 jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Panorama9 musi toobe ustanowione.

W Panorama9, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Panorama9, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Panorama9](#creating-a-panorama9-test-user)**  -toohave odpowiednikiem Simona Britta w Panorama9, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Panorama9.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Panorama9, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Panorama9** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. Na powitania **Panorama9 domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL jako:`https://dashboard.panorama9.com/saml/access/3262`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://www.panorama9.com/saml20/<tenant-name>`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta Panorama9](https://support.panorama9.com) tooget tych wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartości certyfikatu.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Panorama9** kliknij **skonfigurować Panorama9** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Panorama9 jako administrator.

6. Witaj pasku narzędzi u góry hello, kliknij przycisk **Zarządzaj**, a następnie kliknij przycisk **rozszerzenia**.
   
   ![Rozszerzenia](./media/active-directory-saas-panorama9-tutorial/ic790023.png "rozszerzeń")
7. Na powitania **rozszerzenia** okna dialogowego, kliknij przycisk **rejestracji jednokrotnej**.
   
   ![Logowanie jednokrotne](./media/active-directory-saas-panorama9-tutorial/ic790024.png "logowanie jednokrotne")
8. W hello **ustawienia** sekcji, wykonaj następujące kroki hello:
   
   ![Ustawienia](./media/active-directory-saas-panorama9-tutorial/ic790025.png "ustawienia")
   
    a. W **adres URL dostawcy tożsamości** pole tekstowe, Wklej wartość hello **pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.
   
    b. W **odcisk palca certyfikatu** pole tekstowe, Wklej hello **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.    
         
9. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-panorama9-test-user"></a>Tworzenie użytkownika testowego Panorama9

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Panorama9 muszą mieć przydzielone do Panorama9.  

W przypadku hello Panorama9 Inicjowanie obsługi to zadanie ręczne.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. Zaloguj się za tooyour **Panorama9** witryny firmy jako administrator.

2. W menu hello na górze hello, kliknij przycisk **Zarządzaj**, a następnie kliknij przycisk **użytkowników**.
   
  ![Użytkownicy](./media/active-directory-saas-panorama9-tutorial/ic790027.png "użytkowników")

3. W sekcji użytkownicy hello, kliknij przycisk  **+**  tooadd nowego użytkownika.

 ![Użytkownicy](./media/active-directory-saas-panorama9-tutorial/ic790028.png "użytkowników")

4. Przejdź toohello sekcji danych użytkownika, typu hello adres e-mail z prawidłowym użytkownikiem usługi Azure Active Directory ma tooprovision do hello **E-mail** pola tekstowego.

5. Pochodzić toohello sekcji Użytkownicy kliknij **zapisać**.
   
> [!NOTE]
    > Właściciel konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail i następuje tooconfirm łącze swojego konta, zanim staje się aktywny.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPanorama9.

![Przypisz użytkownika][200] 

**tooassign tooPanorama9 Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Panorama9**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka hello Panorama9 w hello Panel dostępu, należy pobrać automatycznie zalogowane tooPanorama9 aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

