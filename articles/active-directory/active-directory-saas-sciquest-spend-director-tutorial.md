---
title: "Samouczek: Integracji Azure Active Directory z SciQuest spędzają na katalog | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SciQuest spędzają na katalog."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a>Samouczek: Integracji Azure Active Directory z SciQuest spędzają na katalog
Celem Hello tego samouczka jest tooshow należy jak toointegrate SciQuest spędzają na katalog z usługą Azure Active Directory (Azure AD).  
Integracja z usługą Azure AD SciQuest spędzają na katalog zawiera hello następujące korzyści: 

* Można kontrolować w usłudze Azure AD, kto ma dostęp tooSciQuest Dyrektor wydatków 
* Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSciQuest Dyrektor wydatków (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
* Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne
tooconfigure integracji usługi Azure AD z SciQuest spędzają na katalog, należy hello następujące elementy:

* Subskrypcję usługi Azure AD
* Dyrektor spędzają SciQuest jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.
> 
> 

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

* Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
* Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Opis scenariusza
Celem Hello tego samouczka jest tooenable możesz tootest usługi Azure AD rejestracji jednokrotnej w środowisku testowym.  
Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie SciQuest spędzają na katalog z galerii hello 
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a>Dodawanie SciQuest spędzają na katalog z galerii hello
tooconfigure hello integracji SciQuest spędzają na katalog usługi Azure AD, należy tooadd SciQuest spędzają na katalog z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd SciQuest spędzają na katalog z galerii hello, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**. 
   
    ![Usługa Active Directory][1]

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Aplikacje][2]

4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Aplikacje][3]

5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
    ![Aplikacje][4]

6. W polu wyszukiwania hello wpisz **sciQuest spędzają na katalog**.
   
    ![Aplikacje][5]

7. Wybierz w okienku wyników hello **SciQuest spędzają na katalog**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
    ![Aplikacje][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
Celem Hello w tej sekcji jest tooshow jak tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SciQuest Dyrektor spędzają na podstawie użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jest odpowiednikiem hello użytkownika w SciQuest spędzają na katalog tooan użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w SciQuest spędzają na katalog musi toobe ustanowione.  
Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w SciQuest spędzają na katalog.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SciQuest spędzają na katalog, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD pojedynczego rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego SciQuest spędzają na katalog](#creating-a-halogen-software-test-user)**  -toohave odpowiednikiem Simona Britta w spędzają na katalog SciQuest, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-single-sign-on"></a>Konfigurowanie usługi Azure AD pojedynczej rejestracji jednokrotnej
Celem Hello w tej sekcji jest tooenable usługi Azure AD rejestracji jednokrotnej w hello klasycznego portalu Azure i tooconfigure rejestracji jednokrotnej w SciQuest spędzają na katalog aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z SciQuest spędzają na katalog, wykonaj następujące kroki hello:**

1. W hello klasycznego portalu Azure na powitania **SciQuest spędzają na katalog** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne**okna dialogowego.
   
    ![Konfigurowanie rejestracji jednokrotnej][8]

2. Na powitania **jak ma toosign użytkowników na tooSciQuest Dyrektor wydatków** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Azure AD rejestracji jednokrotnej][9]

3. Na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj hello następujące kroki: 
   
    ![Konfiguruj ustawienia aplikacji][10]
   
     a. W hello **na adres URL logowania** tekstowym, wpisz adres URL używany przez Twoje toosign użytkowników na tooyour SciQuest spędzają na katalog aplikacji przy użyciu następującego wzorca hello: *https://.* SciQuest.com/.**
   
     b. W hello **adres URL odpowiedzi** pole tekstowe, typ hello takie same wartości zostały wpisane w hello **na adres URL logowania** pola tekstowego. 
   
     c. Kliknij przycisk **Dalej**.

4. Na powitania **skonfigurować logowanie jednokrotne w SciQuest spędzają na katalog** kliknij przycisk **pobierania metadanych**, a następnie zapisz plik metadanych hello lokalnie na komputerze.
   
    ![Co to jest program Azure AD Connect][11]

5. Skontaktuj się z SciQuest tooenable obsługi tej metody uwierzytelniania przy użyciu metadanych hello powyżej pobrane.

6. Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego. 
   
    ![Co to jest program Azure AD Connect][15]

7. Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.  

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego w hello klasycznego portalu Azure o nazwie Simona Britta.

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Co to jest program Azure AD Connect][100] 

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.
   
    ![Co to jest program Azure AD Connect][101] 

4. Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**. 
   
    ![Co to jest program Azure AD Connect][102] 

5. Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:
   
    ![Co to jest program Azure AD Connect][103] 
   
    a. Jako **typ użytkownika**, wybierz pozycję **nowy użytkownik w organizacji**.
   
    b. W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.
   
    c. Kliknij przycisk **Dalej**.

6. Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki: 
   
    ![Co to jest program Azure AD Connect][104] 
   
    a. W hello **imię** pole tekstowe, typ **Britta**.  
   
    b. W hello **nazwisko** txtbox, typ **Simona**.
   
    c. W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.
   
    d. W hello **roli** listy, wybierz **użytkownika**.
   
    e. Kliknij przycisk **Dalej**.

7. Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.
   
    ![Co to jest program Azure AD Connect][105]  

8. Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:
   
    ![Co to jest program Azure AD Connect][106]   
   
    a. Zanotuj wartość hello hello **nowe hasło**.
   
    b. Kliknij przycisk **Complete** (Zakończ).   

### <a name="creating-a-sciquest-spend-director-test-user"></a>Tworzenie użytkownika testowego SciQuest spędzają na katalog
Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w SciQuest spędzają na katalog.

Należy toocontact z zespołem pomocy technicznej SciQuest spędzają na katalog i podaj szczegóły hello o tooget konta użytkownika testu, on utworzony.

Alternatywnie można też skorzystać w czasie inicjowania obsługi administracyjnej, pojedynczego logowania jednokrotnego funkcja, która jest obsługiwana przez SciQuest spędzają na katalog.  
Po włączeniu w czasie inicjowania obsługi użytkowników są tworzone automatycznie przez SciQuest spędzają na katalog podczas jednego próba logowania jednokrotnego, jeśli nie istnieją. Ta funkcja eliminuje konieczność hello toomanually tworzenie odpowiednikiem rejestracji jednokrotnej użytkowników.

tooget w czasie inicjowania obsługi administracyjnej włączone, ale trzeba toocontact jest zespołem pomocy technicznej SciQuest spędzają na katalog.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD
Celem Hello w tej sekcji jest tooenabling toouse Simona Britta Azure rejestracji jednokrotnej, przyznając jej tooSciQuest dostępu Dyrektor wydatków.

![Co to jest program Azure AD Connect][200]

**tooassign tooSciQuest Simona Britta dyrektora wydatków, wykonaj hello następujące kroki:**

1. Na hello Azure kliknij klasycznego portalu, widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Co to jest program Azure AD Connect][201]

2. Z listy aplikacji hello wybierz **SciQuest spędzają na katalog**.
   
    ![Co to jest program Azure AD Connect][202]

3. W menu hello na górze hello, kliknij przycisk **użytkowników**.
   
    ![Co to jest program Azure AD Connect][203]

4. Na liście hello użytkowników, wybierz **Simona Britta**.
   
    ![Co to jest program Azure AD Connect][204]

5. W narzędzi hello na dole powitania kliknij **przypisać**.
   
    ![Co to jest program Azure AD Connect][205]

### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej
Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.  
Po kliknięciu kafelka SciQuest spędzają na katalog hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SciQuest spędzają na katalog aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

