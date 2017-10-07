---
title: 'Samouczek: Integracji Azure Active Directory z ThousandEyes | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ThousandEyes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a>Samouczek: Integracji Azure Active Directory z ThousandEyes

Z tego samouczka, dowiesz się, jak toointegrate ThousandEyes w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD ThousandEyes zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooThousandEyes
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooThousandEyes (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z ThousandEyes należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- ThousandEyes logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie ThousandEyes z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-thousandeyes-from-hello-gallery"></a>Dodawanie ThousandEyes z galerii hello
tooconfigure hello integracji ThousandEyes do usługi Azure AD, należy tooadd ThousandEyes z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd ThousandEyes z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **ThousandEyes**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. W panelu wyników hello zaznacz **ThousandEyes**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ThousandEyes w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w ThousandEyes jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w ThousandEyes musi toobe ustanowione.

W ThousandEyes, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ThousandEyes, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego ThousandEyes](#creating-a-thousandeyes-test-user)**  -toohave odpowiednikiem Simona Britta w ThousandEyes, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji ThousandEyes.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z ThousandEyes, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **ThousandEyes** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. Na powitania **ThousandEyes domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL jako:`https://app.thousandeyes.com/login/sso`

4. Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji ThousandEyes** kliknij **skonfigurować ThousandEyes** tooopen **Konfigurowanie logowania jednokrotnego** okna. Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. W oknie przeglądarki innej witryny sieci web, zaloguj się na tooyour **ThousandEyes** witryny firmy jako administrator.

8. W menu hello na górze hello, kliknij przycisk **ustawienia**.
   
    ![Ustawienia](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "ustawienia")

9. Kliknij przycisk **konta**
   
    ![Konto](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "konta")

10. Kliknij przycisk hello **zabezpieczeń i uwierzytelniania** kartę.
   
    ![Bezpieczeństwo i uwierzytelniania](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "zabezpieczeń i uwierzytelniania")

11. W hello **ustawienia logowania jednokrotnego** sekcji, wykonaj następujące kroki hello:
   
    ![Konfiguracja rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "skonfigurować logowanie jednokrotne")
  
    a. Wybierz **Włącz rejestrację jednokrotną**.
  
    b. W **adres URL strony logowania** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.
  
    c. W **adres URL strony wylogowania** pole tekstowe, Wklej **Sign-Out URL** którego została skopiowana z portalu Azure.
  
    d. **Wystawca dostawcy tożsamości** pole tekstowe, Wklej **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.
  
    e. W **certyfikatu weryfikacji**, kliknij przycisk **wybierz plik**, a następnie przekaż certyfikat hello został pobrany z portalu Azure.
  
    f. Kliknij pozycję **Zapisz**.
 
> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-thousandeyes-test-user"></a>Tworzenie użytkownika testowego ThousandEyes

W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do ThousandEyes muszą mieć przydzielone do ThousandEyes.  
W przypadku hello ThousandEyes Inicjowanie obsługi to zadanie ręczne.

>[!NOTE]
>Możesz użyć innych ThousandEyes użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision ThousandEyes usługi Azure Active Directory kont użytkowników.

**tooprovision tooThousandEyes konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się do witryny firmy ThousandEyes jako administrator.

2. Kliknij przycisk **ustawienia**.
   
    ![Ustawienia](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "ustawienia")

3. Kliknij przycisk **konta**.
   
    ![Konto](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "konta")

4. Kliknij przycisk hello **konta & użytkowników** kartę.
   
    ![Konta & użytkowników](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "konta & użytkowników")

5. W hello **Dodawanie użytkowników i kont** sekcji, wykonaj następujące kroki hello:
   
    ![Dodaj konta użytkowników](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "dodawania kont użytkowników")   
  
    a. W **nazwa** pole tekstowe, nazwę użytkownika, takie jak hello typu **Simona Britta**.

    b. W **E-mail** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak  **brittasimon@contoso.com** .
   
    b. Kliknij przycisk **tooAccount Dodaj nowego użytkownika**.
      
     >[!NOTE]
     >Właściciel konta usługi Azure Active Directory Hello będzie otrzymasz wiadomość e-mail, w tym tooconfirm łącza i aktywować hello konta.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooThousandEyes.

![Przypisz użytkownika][200] 

**tooassign tooThousandEyes Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **ThousandEyes**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu powitalne ThousandEyes kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour ThousandEyes aplikacji.

Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

