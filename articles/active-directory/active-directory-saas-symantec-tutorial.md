---
title: "Samouczek: Integracji Azure Active Directory z usługi zabezpieczeń firmy Symantec w sieci Web (WSS) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usług zabezpieczeń firmy Symantec w sieci Web (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a>Samouczek: Integracji Azure Active Directory z usługi zabezpieczeń firmy Symantec w sieci Web (WSS)

Z tego samouczka, dowiesz się, jak toointegrate Twojej firmy Symantec w sieci Web zabezpieczeń usługi (WSS) konta przy użyciu konta usługi Azure Active Directory (Azure AD), aby WSS można uwierzytelnić użytkownika końcowego udostępniane w hello Azure AD przy użyciu uwierzytelniania SAML i wymuszać użytkownika lub reguły poziomu zasad grupy.

Integrowanie usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z usługą Azure AD zapewnia hello następujące korzyści:

- Zarządzaj wszystkimi hello użytkowników końcowych i grupy używane przez Twoje konto programu WSS w portalu usługi Azure AD. 

- Pozwolić tooauthenticate użytkownicy końcowi hello programu WSS przy użyciu swoich poświadczeń usługi Azure AD.

- Włącz wymuszania hello użytkownika i grupy poziomu reguł zdefiniowanych w ramach konta programu WSS.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z usługi zabezpieczeń firmy Symantec w sieci Web (WSS), należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Konto usługi zabezpieczeń firmy Symantec w sieci Web (WSS)

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu konta programu WSS, który jest obecnie używana w celu produkcji.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać konta programu WSS, który jest obecnie używana w celu produkcji dla tego testu, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku skonfigurujesz programu Azure AD tooenable pojedynczego logowania jednokrotnego tooWSS przy użyciu poświadczeń użytkownika końcowego hello zdefiniowane w ramach konta usługi Azure AD.
Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie aplikacji usługi zabezpieczeń firmy Symantec w sieci Web (WSS) hello z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a>Dodawanie usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z galerii hello
tooconfigure hello integracji usługi zabezpieczeń firmy Symantec w sieci Web (WSS) do usługi Azure AD, należy tooadd usługi zabezpieczeń firmy Symantec w sieci Web (WSS) z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd firmy Symantec w sieci Web zabezpieczeń usługi (WSS) z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)**, wybierz pozycję **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)** z panelu wyników następnie kliknij przycisk **Dodaj** hello tooadd przycisku aplikacja.

    ![Symantec Web zabezpieczeń usługi (WSS) na liście wyników hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z firmy Symantec w sieci Web zabezpieczeń usługi (WSS) w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w sieci Web usług zabezpieczeń (WSS) firmy Symantec jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w sieci Web usług zabezpieczeń (WSS) firmy Symantec musi toobe ustanowione.

W firmy Symantec w sieci Web zabezpieczeń usługi (WSS), przypisz wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usługi zabezpieczeń firmy Symantec w sieci Web (WSS), należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego usługi zabezpieczeń firmy Symantec w sieci Web (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  -toohave odpowiednikiem Simona Britta w firmy Symantec sieci Web zabezpieczeń usługi (WSS), który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji usługi zabezpieczeń firmy Symantec w sieci Web (WSS).

**tooconfigure usługi Azure AD rejestracji jednokrotnej z firmy Symantec w sieci Web zabezpieczeń usługi (WSS), wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. Na powitania **domeny usługi (WSS) zabezpieczeń firmy Symantec w sieci Web i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Domena usługi zabezpieczeń firmy Symantec w sieci Web (WSS) i adresy URL pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    a. W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm`

    b. W hello **adres URL odpowiedzi** pole tekstowe, wprowadź adres URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`

    > [!NOTE]
    > Skontaktuj się z hello [zespołem pomocy technicznej klienta usługi zabezpieczeń firmy Symantec w sieci Web (WSS)](https://www.symantec.com/contact-us) Jeśli hello wartości hello **identyfikator** i **adres URL odpowiedzi** jakiegoś powodu nie działają.

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. tooconfigure rejestracji jednokrotnej na powitania po stronie usługi zabezpieczeń firmy Symantec w sieci Web (WSS), zapoznaj się z dokumentacją online programu WSS toohello. Witaj pobrane **XML metadanych** pliku będzie konieczne toobe importowane do portalu programu WSS hello. Skontaktuj się z pomocą hello [usługi zabezpieczeń firmy Symantec w sieci Web (WSS) obsługuje zespołu](https://www.symantec.com/contact-us) Jeśli potrzebujesz pomocy przy konfiguracji hello w portalu programu WSS hello.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.

    ![przycisk Dodaj Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a>Tworzenie użytkownika testowego usługi zabezpieczeń firmy Symantec w sieci Web (WSS)

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w sieci Web usług zabezpieczeń (WSS) firmy Symantec. Nazwa użytkownika końcowego odpowiedniego Hello można ręcznie utworzyć w portalu programu WSS hello lub poczekać hello użytkowników/grupy udostępniane w hello Azure AD synchronizowane toobe toohello WSS portalu po kilku minutach (~ 15 minut). Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej. publiczny adres IP Hello hello maszyny użytkownika końcowego, który będzie używany toobrowse witryn sieci Web może też być konieczne toobe udostępniane w portalu usługi zabezpieczeń firmy Symantec w sieci Web (WSS) hello.

> [!NOTE]
> Sprawdź [kliknij tutaj](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget komputera na publiczny adres IP.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSymantec usługi zabezpieczeń sieci Web (WSS).

![Przypisanie roli użytkownika hello][200] 

**tooassign tooSymantec Simona Britta usługi zabezpieczeń sieci Web (WSS) wykonaj następujące kroki hello:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **usługi zabezpieczeń firmy Symantec w sieci Web (WSS)**.

    ![łącze usługi zabezpieczeń firmy Symantec w sieci Web (WSS) Hello na liście aplikacji hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202]

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji przetestujesz hello pojedynczego logowania jednokrotnego funkcji teraz, gdy skonfigurowano programu WSS toouse konta usługi Azure AD do uwierzytelniania SAML.

Po skonfigurowaniu sieci web przeglądarce tooproxy ruchu tooWSS, po otwarciu przeglądarki sieci web i spróbuj toobrowse tooa lokacji, a następnie będzie strony przekierowanego toohello Azure logowania jednokrotnego. Wprowadź poświadczenia hello hello testu użytkownika, że obsługa została zainicjowana w hello Azure AD (czyli BrittaSimon) oraz skojarzone hasło. Po uwierzytelnieniu, będziesz w stanie toobrowse toohello witryny sieci Web, które wybrano. Należy można utworzyć reguły na powitania WSS po stronie tooblock BrittaSimon z przeglądania tooa określonej lokacji, a następnie powinna zostać wyświetlona strona bloku WSS hello przy próbie toobrowse toothat lokacji jako użytkownik BrittaSimon.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

