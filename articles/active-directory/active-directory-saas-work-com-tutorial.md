---
title: 'Samouczek: Integracji Azure Active Directory z Work.com | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a>Samouczek: Integracji Azure Active Directory z Work.com

Z tego samouczka, dowiesz się, jak toointegrate Work.com w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD Work.com zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooWork.com
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWork.com (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Work.com należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Work.com logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodaj Work.com z galerii hello
2. Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

## <a name="add-workcom-from-hello-gallery"></a>Dodaj Work.com z galerii hello
tooconfigure hello integracji Work.com do usługi Azure AD, należy tooadd Work.com z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Work.com z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Work.com**, wybierz pozycję **Work.com** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Dodaj z galerii](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Work.com w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Work.com jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Work.com musi toobe ustanowione.

W Work.com, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Work.com, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Work.com](#create-a-workcom-test-user)**  -toohave odpowiednikiem Simona Britta w Work.com, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Work.com.

>[!NOTE]
>tooconfigure logowanie jednokrotne, należy toosetup niestandardową nazwę domeny Work.com jeszcze. Należy toodefine co najmniej domeny nazwy, przetestować nazwę domeny i wdrożyć ją tooyour całej organizacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Work.com, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **Work.com** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Na podstawie SAML logowania jednokrotnego](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. Na powitania **Work.com domeny i adres URL** sekcji, wykonaj następujące hello:

    ![Sekcja Work.com domeny i adresy URL](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://<companyname>.my.salesforce.com`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) tooget tej wartości. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Przycisk Zapisz](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji Work.com** kliknij **skonfigurować Work.com** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Sekcja konfiguracji Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. Zaloguj się za tooyour Work.com dzierżawy jako administrator.

8. Przejdź za**Instalatora**.
   
    ![Instalator](./media/active-directory-saas-work-com-tutorial/ic794108.png "Instalatora")

9. W okienku nawigacji po lewej stronie powitania w hello **Administruj** , kliknij przycisk **Zarządzanie domenami** tooexpand hello powiązanych sekcji, a następnie kliknij przycisk **Moje domeny** tooopen hello  **Mojej domeny** strony. 
   
    ![Mojej domeny](./media/active-directory-saas-work-com-tutorial/ic767825.png "mojej domeny")

10. tooverify, który domeny nie został skonfigurowany prawidłowo, upewnij się, że jest on "**krok 4 wdrożone tooUsers**" i zapoznaj się z "**Moje ustawienia domeny**".
   
    ![Domeny wdrożono tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser wdrożone domeny")

11. Zaloguj się za tooyour Work.com dzierżawy.

12. Przejdź za**Instalatora**.
    
    ![Instalator](./media/active-directory-saas-work-com-tutorial/ic794108.png "Instalatora")

13. Rozwiń węzeł hello **kontroli bezpieczeństwa** menu, a następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.
    
    ![Single Sign-On ustawienia](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On ustawienia")

14. Na powitania **ustawień rejestracji jednokrotnej** okna dialogowego wykonaj hello następujące kroki:
    
    ![Włączone SAML](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML włączone")
    
    a. Wybierz **SAML włączone**.
    
    b. Kliknij przycisk **Nowy**.

15. W hello **SAML pojedynczego logowania jednokrotnego ustawienia** sekcji, wykonaj następujące kroki hello:
    
    ![SAML pojedynczy znak na ustawienie](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML pojedynczy znak na ustawienie")
    
    a. W hello **nazwa** tekstowym, wpisz nazwę dla danej konfiguracji.  
       
    > [!NOTE]
    > Wartość dla **nazwa** automatycznie wypełnić hello **Nazwa interfejsu API** pola tekstowego.
    
    b. W **wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.
    
    c. tooupload certyfikatu hello pobrany z portalu Azure, kliknij przycisk **Przeglądaj**.
    
    d. W hello **identyfikator jednostki** pole tekstowe, typ `https://salesforce-work.com`.
    
    e. Jako **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera hello identyfikator federacyjnej z obiektu użytkownika hello**.
    
    f. Jako **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentfier hello hello instrukcji podmiotu**.
    
    g. W **adresu URL logowania do dostawcy tożsamości** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.

    h. W **adres URL wylogowania dostawcy tożsamości** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.
    
    i. Jako **dostawcy zainicjował żądanie powiązania usługi**, wybierz pozycję **HTTP Post**.
    
    j. Kliknij pozycję **Zapisz**.

16. W portalu klasycznym Work.com, w okienku nawigacji po lewej stronie powitania kliknij **Zarządzanie domenami** tooexpand hello powiązanych sekcji, a następnie kliknij przycisk **Moje domeny** tooopen hello **Moje domeny**strony. 
    
    ![Mojej domeny](./media/active-directory-saas-work-com-tutorial/ic794115.png "mojej domeny")

17. Na powitania **Moje domeny** strony w hello **znakowanie strony logowania** kliknij **Edytuj**.
    
    ![Znakowanie strony logowania](./media/active-directory-saas-work-com-tutorial/ic767826.png "znakowanie strony logowania")

14. Na powitania **znakowanie strony logowania** strony w hello **usługi uwierzytelniania** sekcji, hello nazwę Twojej **ustawienia logowania jednokrotnego SAML** jest wyświetlany. Wybierz go, a następnie kliknij przycisk **zapisać**.
    
    ![Znakowanie strony logowania](./media/active-directory-saas-work-com-tutorial/ic784366.png "znakowanie strony logowania")

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Użytkownicy i grupy -> Wszyscy użytkownicy](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Add](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Strony okna dialogowego użytkownika](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-workcom-test-user"></a>Tworzenie użytkownika testowego Work.com
Dla usługi Azure Active Directory użytkowników toobe stanie toosign w muszą być tooWork.com elastycznie. W przypadku hello Work.com Inicjowanie obsługi to zadanie ręczne.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:
1. Rejestracja tooyour Work.com witryny firmy jako administrator.

2. Przejdź za**Instalatora**.
   
    ![Instalator](./media/active-directory-saas-work-com-tutorial/IC794108.png "Instalatora")
3. Przejdź za**Zarządzanie użytkownikami \> użytkowników**.
   
    ![Zarządzaj użytkownikami](./media/active-directory-saas-work-com-tutorial/IC784369.png "Zarządzanie użytkownikami")

4. Kliknij przycisk **nowego użytkownika**.
   
    ![Wszyscy użytkownicy](./media/active-directory-saas-work-com-tutorial/IC794117.png "wszyscy użytkownicy")

5. W hello sekcji Edytuj użytkowników, wykonaj następujące kroki w przypadku atrybutów elementów prawidłową Azure hello konta AD mają tooprovision w hello związane z pól tekstowych:
   
    ![Edycja użytkownika](./media/active-directory-saas-work-com-tutorial/ic794118.png "Edycja użytkownika")
   
    a. W hello **imię** pole tekstowe, hello typu **imię** użytkownika hello **Britta**.
    
    b. W hello **nazwisko** pole tekstowe, hello typu **nazwisko** użytkownika hello **Simona**.
    
    c. W hello **Alias** pole tekstowe, hello typu **nazwa** użytkownika hello **BrittaS**.
    
    d. W hello **E-mail** pole tekstowe, hello typu **adres e-mail** użytkownika  **Brittasimon@contoso.com** .
    
    e. W hello **nazwy użytkownika** tekstowym, wpisz nazwę użytkownika użytkownika, takich jak  **Brittasimon@contoso.com** .
    
    f. W hello **pseudonim** pola tekstowego, a typ **pseudonim** użytkownika **Simona**.
    
    g. Wybierz **roli**, **licencji użytkownika**, i **profilu**.
    
    h. Kliknij pozycję **Zapisz**.  
      
    > [!NOTE]
    > Właściciel konta usługi Azure AD Hello otrzymają wiadomość e-mail z tym kontem hello tooconfirm łącze zanim staje się aktywny.
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWork.com.

![Przypisz użytkownika][200] 

**tooassign tooWork.com Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Work.com**.

    ![Work.com na liście aplikacji](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Work.com hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Work.com aplikacji.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

