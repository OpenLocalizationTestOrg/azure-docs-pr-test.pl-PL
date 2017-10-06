---
title: "Samouczek: Integracji Azure Active Directory przy użyciu usługi TINFOIL SECURITY | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługę TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a>Samouczek: Integracji Azure Active Directory przy użyciu usługi TINFOIL SECURITY

Z tego samouczka, dowiesz się, jak toointegrate usługę TINFOIL SECURITY w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD usługę TINFOIL SECURITY zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTINFOIL zabezpieczeń
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTINFOIL zabezpieczeń (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD przy użyciu usługi TINFOIL SECURITY należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Usługa TINFOIL SECURITY logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodaj usługę TINFOIL SECURITY z galerii hello
2. Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

## <a name="add-tinfoil-security-from-hello-gallery"></a>Dodaj usługę TINFOIL SECURITY z galerii hello
tooconfigure hello integracji usługa TINFOIL SECURITY do usługi Azure AD, należy tooadd usługę TINFOIL SECURITY z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd usługę TINFOIL SECURITY z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **usługę TINFOIL SECURITY**, wybierz pozycję **usługę TINFOIL SECURITY** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Usługa TINFOIL SECURITY z galerii](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługę TINFOIL SECURITY w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w usługę TINFOIL SECURITY jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w usługę TINFOIL SECURITY musi toobe ustanowione.

Usługa TINFOIL SECURITY przypisywanie wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD logowania jednokrotnego przy użyciu usługi TINFOIL SECURITY, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego usługę TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave odpowiednikiem Simona Britta w usługę TINFOIL SECURITY, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji usługę TINFOIL SECURITY.

**tooconfigure usługi Azure AD logowania jednokrotnego przy użyciu usługi TINFOIL SECURITY, wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **usługę TINFOIL SECURITY** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![SAML na podstawie logowania jednokrotnego](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. Na powitania **TINFOIL SECURITY domeny i adres URL** sekcji, hello użytkownik nie ma tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartość.

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. Mapowanie atrybutów hello wymagane tooadd, wykonaj hello następujące kroki:
    
    ![Atrybuty](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "atrybutów")
    
    | Nazwa atrybutu    |   Wartość atrybutu |
    | ------------------- | -------------------- |
    | AccountID | UXXXXXXXXXXXXX |
    
    a. Kliknij przycisk **Dodaj atrybut użytkownika**.
    
    ![Dodaj atrybut](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "atrybutów")
    
    ![Dodaj atrybut](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "atrybutów")
    
    b. W hello **nazwa atrybutu** pole tekstowe, typ **accountid**.
    
    c. W hello **wartość atrybutu** pole tekstowe, Wklej hello konta identyfikator wartość, która zostanie wyświetlony później w samouczku hello.
    
    d. Kliknij przycisk **OK**.    

6. Kliknij przycisk **zapisać** przycisku.

    ![Przyciskiem Zapisz](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. Na powitania **TINFOIL SECURITY Configuration** kliknij **skonfigurować usługę TINFOIL SECURITY** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfiguracja zabezpieczeń TINFOIL](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy usługę TINFOIL SECURITY jako administrator.

9. Witaj pasku narzędzi u góry hello, kliknij przycisk **Moje konto**.
   
    ![Pulpit nawigacyjny](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "pulpitu nawigacyjnego")

10. Kliknij przycisk **zabezpieczeń**.
   
    ![Zabezpieczenia](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "zabezpieczeń")

11. Na powitania **rejestracji jednokrotnej** konfiguracji wykonaj hello następujące kroki:
   
    ![Logowanie jednokrotne](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "logowanie jednokrotne")
   
    a. Wybierz **Włącz SAML**.
   
    b. Kliknij przycisk **ręcznej konfiguracji**.
   
    c. W **adresu URL przesyłania SAML** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure
   
    d. W **odcisk palca certyfikatu SAML** pole tekstowe, Wklej wartość hello **odcisk palca** , które zostały skopiowane z **certyfikat podpisywania SAML** sekcji.
  
    e. Kopiuj **swój identyfikator konta** i Wklej wartość hello w **wartość atrybutu** pole tekstowe, w obszarze **Dodawanie atrybutu** sekcji w portalu Azure.
   
    f. Kliknij pozycję **Zapisz**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Użytkownicy i grupy -> Wszyscy użytkownicy ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Użytkownik](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-tinfoil-security-test-user"></a>Tworzenie użytkownika testowego usługę TINFOIL SECURITY

W kolejności tooenable usługi Azure AD użytkownicy toolog do usługę TINFOIL SECURITY musi być przygotowana do usługę TINFOIL SECURITY. W przypadku hello usługę TINFOIL SECURITY Inicjowanie obsługi to zadanie ręczne.

**tooget użytkownika zainicjowano obsługę administracyjną, należy wykonać hello następujące kroki:**

1. Jeśli użytkownik hello jest część konta organizacji, należy za[skontaktuj się z zespołem pomocy technicznej usługę TINFOIL SECURITY hello](https://www.tinfoilsecurity.com/contact) tooget hello konta konto użytkownika.

2. Jeśli użytkownik hello jest zwykłych użytkowników TINFOIL SECURITY SaaS, hello użytkownik może dodać tooany współpracownika witryn hello użytkownika. Ta usługa wyzwalaczy toosend procesu, określony toohello zaproszenia poczty e-mail toocreate nowego konta użytkownika usługę TINFOIL SECURITY.

> [!NOTE]
> Możesz użyć innych usługę TINFOIL SECURITY użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez usługę TINFOIL SECURITY tooprovision konta użytkownika usługi Azure AD.
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTINFOIL zabezpieczeń.

![Przypisz użytkownika][200] 

**tooassign tooTINFOIL Simona Britta zabezpieczeń, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **usługę TINFOIL SECURITY**.

    ![Wybierz usługę TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka usługę TINFOIL SECURITY hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour usługę TINFOIL SECURITY aplikacji. Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

