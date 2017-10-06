---
title: 'Samouczek: Integracji Azure Active Directory z Halosys | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse Halosys z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a>Samouczek: Integracji Azure Active Directory z Halosys

Z tego samouczka, dowiesz się, jak toointegrate Halosys w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Halosys zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooHalosys
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooHalosys (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Halosys należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Halosys jednokrotnego włączone subskrypcji


> [!NOTE] 
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.


tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.

Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Halosys z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne


## <a name="adding-halosys-from-hello-gallery"></a>Dodawanie Halosys z galerii hello
tooconfigure hello integracji Halosys do usługi Azure AD, należy tooadd Halosys z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Halosys z galerii hello, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.

    ![Usługa Active Directory][1]
2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.

    ![Aplikacje][2]

4. Kliknij przycisk **Dodaj** u dołu hello hello strony.

    ![Aplikacje][3]

5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.

    ![Aplikacje][4]

6. W polu wyszukiwania hello wpisz **Halosys**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. Wybierz w okienku wyników hello **Halosys**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Halosys w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Halosys jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Halosys musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Halosys.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Halosys, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Halosys](#creating-a-halosys-test-user)**  -toohave odpowiednikiem Simona Britta w Halosys, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu klasycznym hello i skonfigurować logowanie jednokrotne w aplikacji Halosys.


**tooconfigure usługi Azure AD rejestracji jednokrotnej z Halosys, wykonaj następujące kroki hello:**

1. W klasycznym portalu hello na powitania **Halosys** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne** okna dialogowego.
     
    ![Konfigurowanie rejestracji jednokrotnej][6] 

2. Na powitania **jak ma toosign użytkowników na tooHalosys** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. Na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj hello następujące kroki:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    a. W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używanych przez aplikację Halosys toosign na tooyour użytkowników przy użyciu hello następującego wzorca: `https://<company-name>.Halosys.com/client-api/api`.

    Witaj b.In **adres URL identyfikatora** pole tekstowe, wprowadź adres URL hello w hello następującego wzorca: `https://<company-name>.Halosys.com`. 
         
4. Na powitania **skonfigurować logowanie jednokrotne w Halosys** kliknij przycisk **pobierania metadanych**, a następnie zapisz plik hello na tym komputerze:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, skontaktuj się z zespołem pomocy technicznej Halosys i podaj następujący hello:

    • hello pobrane **pliku metadanych**
    
    • hello **adres URL logowania jednokrotnego SAML**
    

6. W portalu klasycznym hello, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.
    
    ![Azure AD rejestracji jednokrotnej][10]

7. Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.  
 
    ![Azure AD rejestracji jednokrotnej][11]


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
W tej sekcji Tworzenie użytkownika testowego w portalu klasycznym hello o nazwie Simona Britta.


![Tworzenie użytkowników usługi Azure AD][20]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj następujące kroki hello: ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png) 

    a. Jako typ użytkownika wybierz nowego użytkownika w organizacji.

    b. W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.

    c. Kliknij przycisk **Dalej**.

6.  Na powitania **profilu użytkownika** okna dialogowego wykonaj następujące kroki hello: ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 

    a. W hello **imię** pole tekstowe, typ **Britta**.  

    b. W hello **nazwisko** pole tekstowe, typ **Simona**.

    c. W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.

    d. W hello **roli** listy, wybierz **użytkownika**.

    e. Kliknij przycisk **Dalej**.

7. Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    a. Zanotuj wartość hello hello **nowe hasło**.

    b. Kliknij przycisk **Complete** (Zakończ).   



### <a name="creating-a-halosys-test-user"></a>Tworzenie użytkownika testowego Halosys

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Halosys. Należy skontaktować się z Halosys pomocy technicznej zespół tooadd hello użytkowników hello Halosys platformy.


### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooHalosys dostępu.

![Przypisz użytkownika][200] 

**tooassign tooHalosys Simona Britta wykonaj hello następujące kroki:**

1. W portalu klasycznym hello, kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Halosys**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. W menu hello na górze hello, kliknij przycisk **użytkowników**.

    ![Przypisz użytkownika][203]

4. Na liście hello użytkowników, wybierz **Simona Britta**.

5. W narzędzi hello na dole powitania kliknij **przypisać**.

    ![Przypisz użytkownika][205]


### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu powitalne Halosys kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Halosys aplikacji.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
