---
title: "Samouczek: Azure Active Directory integracji z pakietem życia SilkRoad | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SilkRoad życia pakietu."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a>Samouczek: Azure Active Directory integracji z pakietem życia SilkRoad
Celem Hello tego samouczka jest tooshow należy jak toointegrate SilkRoad Suite użytkowania z usługą Azure Active Directory (Azure AD). 

Integrowanie SilkRoad Suite użytkowania z usługą Azure AD zapewnia hello następujące korzyści: 

* Można kontrolować w usłudze Azure AD, kto ma dostęp tooSilkRoad Suite życia 
* Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSilkRoad życia pakiet rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne
tooconfigure integracji usługi Azure AD z pakietem życia SilkRoad należy hello następujące elementy:

* Subskrypcję usługi Azure AD
* Subskrypcja SilkRoad życia Suite logowanie Jednokrotne włączone

>[!NOTE]
>tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego. 
> 

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

* Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
* Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Opis scenariusza
Celem Hello tego samouczka jest tooenable możesz tootest logowania jednokrotnego programu Azure AD w środowisku testowym.

Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie pakietu życia SilkRoad z galerii hello 
2. Konfigurowanie i testowania logowania jednokrotnego programu Azure AD

## <a name="add-silkroad-life-suite-from-hello-gallery"></a>Dodawanie zestawu życia SilkRoad z galerii hello
tooconfigure hello integracji pakietu życia SilkRoad do usługi Azure AD, należy tooadd SilkRoad życia pakietu z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd SilkRoad życia pakietu z galerii hello wykonaj hello następujące kroki:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**. 
   
    ![Usługa Active Directory][1]

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Aplikacje][2]

4. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Aplikacje][3]

5. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.
   
    ![Aplikacje][4]

6. W polu wyszukiwania hello wpisz **Suite życia SilkRoad**.
   
    ![Aplikacje][5]

7. W okienku wyników hello, wybierz **Suite życia SilkRoad**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.
   
    ![Aplikacje][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
Celem Hello w tej sekcji jest tooshow użytkownika jak tooconfigure i Azure AD SSO z pakietem życia SilkRoad testu na podstawie użytkownika testowego o nazwie "Britta Simona".

Dla toowork logowania jednokrotnego usługi Azure AD musi tooknow jest użytkownika odpowiednikiem hello w SilkRoad życia Suite tooan użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi pakietu życia SilkRoad musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** SilkRoad życia pakietu.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z pakietem życia SilkRoad, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego zestawu życia SilkRoad](#creating-a-silkroad-life-suite-test-user)**  -toohave odpowiednikiem Simona Britta życia pakietu SilkRoad, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej
Celem Hello w tej sekcji jest tooenable logowania jednokrotnego programu Azure AD w hello klasycznego portalu Azure i tooconfigure logowania jednokrotnego w SilkRoad życia pakietu aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z pakietem życia SilkRoad, wykonaj hello następujące kroki:**

1. Logowania jednokrotnego tooyour SilkRoad witryna firmy jako administrator. 

  >[!NOTE] 
  > tooobtain dostępu toohello SilkRoad życia Suite uwierzytelniania aplikacji dla Konfigurowanie Federacji przy użyciu usługi Microsoft Azure AD, skontaktuj się z SilkRoad pomocy technicznej lub Twoim przedstawicielem SilkRoad usług.
  > 

2. Przejdź za**dostawcy usług**, a następnie kliknij przycisk **szczegóły federacyjnego**. 
   
    ![Azure AD rejestracji jednokrotnej][10] 

3. Kliknij przycisk **pobierania metadanych Federacji**, a następnie zapisz plik metadanych hello na tym komputerze.
   
    ![Azure AD rejestracji jednokrotnej][11] 

4. W hello klasycznego portalu Azure na powitania **Suite życia SilkRoad** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne**  okno dialogowe.
   
    ![Konfigurowanie rejestracji jednokrotnej][6] 

5. Na powitania **jak ma toosign użytkowników na tooSilkRoad Suite życia** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.
   
    ![Azure AD rejestracji jednokrotnej][7] 

6. Na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj hello następujące kroki:
   
    ![Azure AD rejestracji jednokrotnej][8]   
 1. W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używanej przez Twoją witrynę Suite życia SilkRoad toosign na tooyour użytkowników (np.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).  
 2. Otwórz hello pobrane **Silkroad** pliku metadanych. 
 3. Zlokalizuj hello **AssertionConsumerService** tag, a następnie hello kopiowania **lokalizacji** atrybutu.         
   
    ![Azure AD rejestracji jednokrotnej][21] 
 4. Wklej wartość hello do hello **adres URL odpowiedzi** pola tekstowego.  
 5. Kliknij przycisk **Dalej**.

6. Na powitania **skonfigurować logowanie jednokrotne w SilkRoad życia Suite** wykonaj hello następujące kroki:
   
    ![Azure AD rejestracji jednokrotnej][9]  
 1. Kliknij przycisk Pobierz certyfikat, a następnie zapisz plik hello na tym komputerze.  
 2. Kliknij przycisk **Dalej**.

7. W Twojej **SilkRoad** aplikacji, kliknij przycisk **źródeł uwierzytelniania**.
   
    ![Azure AD rejestracji jednokrotnej][12] 

8. Kliknij przycisk **Dodawanie uwierzytelniania źródła**. 
   
    ![Azure AD rejestracji jednokrotnej][13] 

9. W hello **Dodaj źródło uwierzytelniania** sekcji, wykonaj następujące kroki hello: 
   
    ![Azure AD rejestracji jednokrotnej][14]  
 1. W obszarze **opcja 2 — plik metadanych**, kliknij przycisk **Przeglądaj** tooupload hello pobrany plik metadanych.  
 2. Kliknij przycisk **dostawcy tożsamości utworzyć przy użyciu danych pliku**.

10. W hello **źródeł uwierzytelniania** kliknij **Edytuj**. 
    
     ![Azure AD rejestracji jednokrotnej][15] 

11. Na powitania **Edytuj źródło uwierzytelniania** okna dialogowego, wykonaj następujące kroki hello: 
    
     ![Azure AD rejestracji jednokrotnej][16] 
 1. Jako **włączone**, wybierz pozycję **tak**.   
 2. W hello **opis IdP** tekstowym, wpisz opis dla danej konfiguracji (np.: *logowania jednokrotnego programu Azure AD*).  
 3. W hello **nazwa IdP** tekstowym, wpisz nazwę, która jest tooyour określonej konfiguracji (np.: *Azure SP*).  
 4. Kliknij pozycję **Zapisz**.

12. Wyłącz wszystkie źródła uwierzytelniania. 
    
     ![Azure AD rejestracji jednokrotnej][17]

13. W hello klasycznego portalu Azure na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **dalej**.  
    
     ![Azure AD rejestracji jednokrotnej][18]

14. Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.
    
     ![Azure AD rejestracji jednokrotnej][19]

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego w hello klasycznego portalu Azure o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][20]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.

3. Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**. 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki: 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. Jako typ użytkownika wybierz nowego użytkownika w organizacji.  
 2. W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**. 
 3. Kliknij przycisk **Dalej**.

6. Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki: 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. W hello **imię** pole tekstowe, typ **Britta**.    
 2. W hello **nazwisko** pole tekstowe, typ **Simona**. 
 3. W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**. 
 4. W hello **roli** listy, wybierz **użytkownika**.
 5. Kliknij przycisk **Dalej**.

7. Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. Zanotuj wartość hello hello **nowe hasło**. 
 2. Kliknij przycisk **Complete** (Zakończ).   

### <a name="create-a-silkroad-life-suite-test-user"></a>Tworzenie użytkownika testowego SilkRoad życia pakietu
Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta SilkRoad życia pakietu. Britta firmy musi mieć identyfikator logowania jednokrotnego (czasem określana tooas *AuthParam*), które odpowiadają na Britta **emailaddress** w usłudze Azure AD.

**toocreate użytkownika o nazwie Simona Britta SilkRoad życia pakietu, należy wykonać hello następujące kroki:**

- Pytaj użytkownika toocreate zespołu pomocy technicznej SilkRoad życia pakietu użytkownika, takiej jak **identyfikator logowania jednokrotnego** hello atrybutu samą wartość jak hello **emailaddress** z Simona Britta w usłudze Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD
Celem Hello w tej sekcji jest tooenable toouse Simona Britta Azure logowania jednokrotnego, przyznając jej tooSilkRoad dostępu Suite życia.

![Przypisz użytkownika][200] 

**tooassign tooSilkRoad Simona Britta Suite życia wykonaj hello następujące kroki:**

1. Na hello Azure kliknij klasycznego portalu, widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.
   
    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Suite życia SilkRoad**.
   
    ![Przypisz użytkownika][202] 

3. W menu hello na górze hello, kliknij przycisk **użytkowników**.
   
    ![Przypisz użytkownika][203] 

4. Na liście hello użytkowników, wybierz **Simona Britta**.

5. W narzędzi hello na dole powitania kliknij **przypisać**.
   
    ![Przypisz użytkownika][205]

### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej
Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.  

Po kliknięciu kafelka Suite życia SilkRoad hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SilkRoad życia pakietu aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





