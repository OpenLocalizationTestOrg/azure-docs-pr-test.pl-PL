---
title: 'Samouczek: Integracji Azure Active Directory z Thoughtworks Mingle | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a>Samouczek: Integracji Azure Active Directory z Thoughtworks Mingle

Z tego samouczka, dowiesz się, jak toointegrate Thoughtworks Mingle w usłudze Azure Active Directory (Azure AD).

Integrowanie Thoughtworks Mingle z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooThoughtworks Mingle
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooThoughtworks Mingle (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z Thoughtworks Mingle należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Thoughtworks Mingle logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Thoughtworks Mingle z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a>Dodawanie Thoughtworks Mingle z galerii hello
tooconfigure hello integracji Thoughtworks Mingle do usługi Azure AD, należy tooadd Thoughtworks Mingle z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Thoughtworks Mingle z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **Thoughtworks Mingle**, wybierz pozycję **Thoughtworks Mingle** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Thoughtworks Mingle hello listy wyników](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Thoughtworks Mingle w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Thoughtworks Mingle jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Thoughtworks Mingle musi toobe ustanowione.

W Thoughtworks Mingle, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Thoughtworks Mingle, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**  -toohave odpowiednikiem Simona Britta w Thoughtworks Mingle, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Thoughtworks Mingle.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Thoughtworks Mingle, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Thoughtworks Mingle** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. Na powitania **Thoughtworks Mingle domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Adresy URL i domeny Mingle Thoughtworks pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.mingle.thoughtworks.com`

    > [!NOTE] 
    > wartość Hello nie jest prawdziwe. Wartość hello aktualizacji z hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta Mingle Thoughtworks](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello wartość. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. Zaloguj się za tooyour **Thoughtworks Mingle** witryny firmy jako administrator.

7. Kliknij przycisk hello **Admin** , a następnie kliknij **konfiguracji logowania jednokrotnego**.
   
    ![Karta Admin](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "konfiguracji logowania jednokrotnego")

8. W hello **konfiguracji logowania jednokrotnego** sekcji, wykonaj następujące kroki hello:
   
    ![Konfiguracja rejestracji Jednokrotnej](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "konfiguracji logowania jednokrotnego")
    
    a. Plik metadanych hello tooupload, kliknij przycisk **wybierz plik**. 

    b. Kliknij przycisk **zapisać zmiany**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-thoughtworks-mingle-test-user"></a>Tworzenie użytkownika testowego Thoughtworks Mingle

Dla usługi Azure AD użytkownicy toobe stanie toosign w muszą być elastycznie toohello Thoughtworks Mingle aplikacji przy użyciu nazwy użytkowników usługi Azure Active Directory. W przypadku hello Thoughtworks Mingle Inicjowanie obsługi to zadanie ręczne.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. Zaloguj się za tooyour Thoughtworks Mingle witryny firmy jako administrator.

2. Kliknij przycisk **profilu**.
   
    ![Pierwszy projekt](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "pierwszego projektu")

3. Kliknij przycisk hello **Admin** , a następnie kliknij pozycję **użytkowników**.
   
    ![Użytkownicy](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "użytkowników")

4. Kliknij przycisk **nowego użytkownika**.
   
    ![Nowy użytkownik](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "nowego użytkownika")

5. Na powitania **nowego użytkownika** okna dialogowego wykonaj hello następujące kroki:
   
    ![Okno dialogowe nowego użytkownika](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "nowego użytkownika")  
 
    a. Hello typu **nazwy logowania**, **Nazwa wyświetlana**, **hasła wybierz**, **Potwierdź hasło** prawidłowy Azure AD konta tooprovision do hello związanych z pól tekstowych. 

    b. Jako **typ użytkownika**, wybierz pozycję **pełnej**.

    c. Kliknij przycisk **utworzyć ten profil**.

>[!NOTE]
>Możesz użyć innych Thoughtworks Mingle użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Thoughtworks Mingle tooprovision kont użytkowników usługi AAD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooThoughtworks Mingle.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooThoughtworks Simona Britta Mingle, wykonaj następujące kroki hello:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Thoughtworks Mingle**.

    ![Witaj Thoughtworks Mingle łącza na liście aplikacji hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.

Po kliknięciu kafelka Thoughtworks Mingle hello w hello Panel dostępu, należy pobrać zalogowane automatycznie tooyour Thoughtworks Mingle aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

