---
title: 'Samouczek: Integracji Azure Active Directory z SkyDesk poczty E-mail | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SkyDesk wiadomości E-mail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a>Samouczek: Integracji Azure Active Directory z SkyDesk poczty E-mail

Z tego samouczka, dowiesz się, jak toointegrate SkyDesk poczty E-mail w usłudze Azure Active Directory (Azure AD).

Integrowanie SkyDesk wiadomości E-mail z usługi Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD mającego tooSkyDesk dostępu do poczty E-mail
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSkyDesk poczty E-mail (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z SkyDesk poczty E-mail, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- E-mail SkyDesk logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie SkyDesk wiadomości E-mail z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-skydesk-email-from-hello-gallery"></a>Dodawanie SkyDesk wiadomości E-mail z galerii hello
tooconfigure hello integracji SkyDesk poczty E-mail w usłudze Azure Active Directory, należy tooadd SkyDesk wiadomości E-mail z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd E-mail SkyDesk z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **E-mail SkyDesk**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. W panelu wyników hello, wybierz **E-mail SkyDesk**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z SkyDesk poczty E-mail w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w wiadomości E-mail SkyDesk jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w wiadomości E-mail SkyDesk musi toobe ustanowione.

W wiadomości E-mail SkyDesk, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SkyDesk poczty E-mail, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego E-mail SkyDesk](#creating-a-skydesk-email-test-user)**  -toohave odpowiednikiem Simona Britta w SkyDesk wiadomości E-mail, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji poczty E-mail SkyDesk.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z SkyDesk poczty E-mail, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **E-mail SkyDesk** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. Na powitania **SkyDesk domenę poczty E-mail i adresów URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://mail.skydesk.jp/portal/<companyname>`

    > [!NOTE] 
    > wartość Hello nie jest prawdziwe. Wartość hello aktualizacji z hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta poczty E-mail SkyDesk](https://www.skydesk.sg/support/) tooget hello wartość. 
 
4. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. Na powitania **konfiguracji poczty E-mail SkyDesk** , kliknij przycisk **konfigurowanie poczty E-mail SkyDesk** tooopen **Konfigurowanie logowania jednokrotnego** okna. Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. tooenable logowania jednokrotnego w **E-mail SkyDesk**, wykonaj następujące kroki hello:

    a. Zaloguj się na tooyour konta E-mail SkyDesk jako administrator.

    b. W menu hello na górze hello, kliknij przycisk **Instalator**i wybierz **organizacji**. 
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    c. Polecenie **domen** z hello lewego panelu.
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    d. Polecenie **Dodawanie domeny**.
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    e. Wpisz nazwę domeny, a następnie sprawdź hello domeny.
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    f. Polecenie **uwierzytelnianie SAML** z hello lewego panelu.
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. Na powitania **uwierzytelnianie SAML** okna dialogowego wykonaj hello następujące kroki:
   
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    >Uwierzytelnianie na podstawie toouse SAML, użytkownik powinien mieć **zweryfikowaną domeną** lub **portal adresu URL** Instalatora. Hello portal można ustawić adres URL z hello unikatową nazwę.
    > 
    > 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    a. W hello **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.
   
    b. W hello **wylogowania** pole tekstowe adresu URL, wartości hello Wklej **Sign-Out URL**, które zostały skopiowane z portalu Azure.

    c. **Zmień adres URL hasła** jest opcjonalny, dlatego pozostaw to pole puste.

    d. Polecenie **uzyskać klucz z pliku** tooselect certyfikat pobrany z portalu Azure, a następnie kliknij przycisk **Otwórz** tooupload hello certyfikatu.

    e. Jako **algorytm**, wybierz pozycję **RSA**.

    f. Kliknij przycisk **Ok** toosave hello zmiany.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-skydesk-email-test-user"></a>Tworzenie użytkownika testowego SkyDesk poczty E-mail

W tej sekcji utworzysz użytkownika o nazwie Simona Britta w SkyDesk wiadomości E-mail.

1. Polecenie **dostępu użytkownika** z pozostałych hello panelu w SkyDesk wiadomości E-mail, a następnie wprowadź nazwy użytkownika. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
>Jeśli potrzebujesz toocreate zbiorczego użytkowników, należy toocontact hello [zespołem pomocy technicznej klienta poczty E-mail SkyDesk](https://www.skydesk.sg/support/).


### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie tooSkyDesk dostępu do poczty E-mail.

![Przypisz użytkownika][200] 

**tooassign tooSkyDesk Simona Britta poczty E-mail, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **E-mail SkyDesk**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.

Po kliknięciu hello E-mail SkyDesk kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji SkyDesk poczty E-mail.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

