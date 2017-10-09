---
title: 'Samouczek: Integracji Azure Active Directory z IdeaScale | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a>Samouczek: Integracji Azure Active Directory z IdeaScale

Z tego samouczka, dowiesz się, jak toointegrate IdeaScale w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD IdeaScale zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooIdeaScale
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooIdeaScale (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z IdeaScale należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- IdeaScale jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie IdeaScale z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-ideascale-from-hello-gallery"></a>Dodawanie IdeaScale z galerii hello
tooconfigure hello integracji IdeaScale do usługi Azure AD, należy tooadd IdeaScale z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd IdeaScale z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **IdeaScale**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. W panelu wyników hello zaznacz **IdeaScale**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z IdeaScale na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w IdeaScale jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w IdeaScale musi toobe ustanowione.

W IdeaScale, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z IdeaScale, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego IdeaScale](#creating-an-ideascale-test-user)**  -toohave odpowiednikiem Simona Britta w IdeaScale, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji IdeaScale.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z IdeaScale, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **IdeaScale** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. Na powitania **IdeaScale domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    a. W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.ideascale.com`

    b. W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator. Skontaktuj się z [zespołem pomocy technicznej klienta IdeaScale](http://support.ideascale.com/) tooget tych wartości. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji IdeaScale** kliknij **skonfigurować IdeaScale** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adresu URL i identyfikator jednostki SAML** z hello **sekcji krótki przewodnik**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy IdeaScale tooyour jako administrator.

8. Przejdź za**ustawienia społeczności**.
   
    ![Ustawienia społeczności](./media/active-directory-saas-ideascale-tutorial/ic790847.png "ustawienia społeczności")

9. Przejdź za**zabezpieczeń \> jednego ustawienia logować**.
   
    ![Pojedyncze ustawienia logować](./media/active-directory-saas-ideascale-tutorial/ic790848.png "pojedynczy logować ustawienia")

10. Jako **typu Pojedyncza**, wybierz pozycję **SAML 2.0**.
   
    ![Pojedynczy typ logować](./media/active-directory-saas-ideascale-tutorial/ic790849.png "pojedynczy typ logować")

11. Na powitania **jednego ustawienia logować** okna dialogowego, wykonaj następujące kroki hello:
   
    ![Pojedyncze ustawienia logować](./media/active-directory-saas-ideascale-tutorial/ic790850.png "pojedynczy logować ustawienia")
   
    a. W **identyfikator jednostki IdP SAML** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.

    b. Kopiowanie zawartości hello pliku metadanych pobranych z portalu Azure i wklej go do hello **metadanych IdP SAML** pola tekstowego.

    c. W **URL Powodzenie wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.

    d. Kliknij przycisk **zapisać zmiany**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-ideascale-test-user"></a>Tworzenie użytkownika testowego IdeaScale

tooenable usługi Azure AD użytkownicy toolog do IdeaScale, muszą mieć przydzielone w tooIdeaScale. W przypadku hello IdeaScale Inicjowanie obsługi to zadanie ręczne.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. Zaloguj się za tooyour **IdeaScale** witryny firmy jako administrator.

2. Przejdź za**ustawienia społeczności**.
   
    ![Ustawienia społeczności](./media/active-directory-saas-ideascale-tutorial/ic790847.png "ustawienia społeczności")

3. Przejdź za**podstawowe ustawienia \> zarządzania elementu członkowskiego**.

4. Kliknij przycisk **dodać członka**.
   
    ![Element członkowski zarządzania](./media/active-directory-saas-ideascale-tutorial/ic790852.png "zarządzania elementu członkowskiego")

5. W sekcji Dodaj nowy element członkowski hello wykonaj następujące kroki hello:
   
    ![Dodaj nowy element członkowski](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Dodaj nowy element członkowski")
   
    a. W hello **adresy E-mail** pole tekstowe, typ hello adres e-mail ma tooprovision prawidłowe konto usługi AAD.
   
    b. Kliknij przycisk **zapisać zmiany**. 
   
    >[!NOTE]
    >Właściciel konta usługi Azure Active Directory Hello pobiera wiadomości e-mail przy użyciu konta hello tooconfirm łącza, zanim staje się aktywny.
      
>[!NOTE]
>Możesz użyć innych IdeaScale użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez IdeaScale tooprovision kont użytkowników usługi AAD.
 

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooIdeaScale.

![Przypisz użytkownika][200] 

**tooassign tooIdeaScale Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **IdeaScale**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej


Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.

Po kliknięciu kafelka IdeaScale hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour IdeaScale aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
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

