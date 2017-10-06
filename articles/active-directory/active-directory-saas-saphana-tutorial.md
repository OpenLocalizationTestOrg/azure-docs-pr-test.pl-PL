---
title: 'Samouczek: Integracji Azure Active Directory z SAP HANA | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a>Samouczek: Integracji Azure Active Directory z SAP HANA

Z tego samouczka, dowiesz się, jak toointegrate SAP HANA w usłudze Azure Active Directory (Azure AD).

Integrowanie SAP HANA z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSAP HANA
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSAP HANA (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z SAP HANA należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- SAP HANA logowanie jednokrotne włączone subskrypcji
- HANA uruchomione wystąpienie na publicznych IaaS, lokalnymi, maszynach wirtualnych platformy Azure lub SAP dużych wystąpień na platformie Azure
- Interfejs sieci Web administracji XSA Hello, jak również zainstalowana w wystąpieniu HANA hello Studio HANA.

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego programu SAP HANA. Testowanie integracji hello najpierw w rozwoju lub przemieszczania środowisko aplikacji hello, a następnie środowiska produkcyjnego hello użycia.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie SAP HANA z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-sap-hana-from-hello-gallery"></a>Dodawanie SAP HANA z galerii hello
tooconfigure hello integracji SAP HANA do usługi Azure AD, należy tooadd SAP HANA z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd SAP HANA z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **SAP HANA**, wybierz pozycję **SAP HANA** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd. 

    ![Witaj nowej aplikacji](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SAP HANA oparte na koncie użytkownika testu o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w SAP HANA jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w SAP HANA musi toobe ustanowione.

Przypisywanie wartości hello hello SAP HANA **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.

tooconfigure i test usługi Azure AD rejestracji jednokrotnej z SAP HANA należy hello toocomplete po bloków konstrukcyjnych:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego SAP HANA](#creating-a-sap-hana-test-user)**  -toohave odpowiednikiem Simona Britta w SAP HANA, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji SAP HANA.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z SAP HANA wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **SAP HANA** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. Na powitania **adresy URL i SAP HANA domeny** sekcji, wykonaj następujące kroki hello:

    ![Domena i adres URL z jednym informacje logowania jednokrotnego](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    a. W hello **identyfikator** pole tekstowe, typu co:`HA100` 

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`

    > [!NOTE] 
    > Wartości te nie są prawdziwe. Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości. Skontaktuj się z [zespołem pomocy technicznej SAP HANA klienta](https://cloudplatform.sap.com/contact.html) tooget tych wartości. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    >Jeśli certyfikat nie jest aktywne następnie uaktywnić go, klikając hello wyboru "Utwórz nowy certyfikat active" w hello Azure AD. 

5. Aplikacja SAP HANA oczekuje potwierdzenia SAML hello w określonym formacie. powitania po zrzut ekranu przedstawia przykład tego. W tym miejscu zostały zamapowane hello **identyfikator użytkownika** z **ExtractMailPrefix()** funkcji **user.mail**. Dzięki temu wartość prefiksu hello adres e-mail użytkownika hello, co jest hello Unikatowy identyfikator użytkownika. Każdy odpowiedź oznaczająca Powodzenie to wysyłane toohello aplikacji SAP HANA.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego:

    a. W hello **identyfikator użytkownika** listy rozwijanej wybierz **ExtractMailPrefix**.
    
    b. W hello **poczty** listy rozwijanej wybierz **user.mail**.

7. Kliknij przycisk **zapisać** przycisku.

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. tooconfigure rejestracji jednokrotnej w **SAP HANA** strona, logowania tooyour **konsoli sieci Web XSA HANA** przechodząc toohello odpowiednich punkt końcowy HTTPS.

    > [!Note]
    > W konfiguracji domyślnej hello hello adresu URL przekierowuje ekran logowania tooa żądania hello, co wymaga poświadczeń hello uwierzytelnionego SAP HANA bazy danych toocomplete hello proces logowania użytkownika. Witaj użytkownika, który loguje się musi mieć zadań administracyjnych hello uprawnienia wymagane tooperform SAML.

9. W hello XSA interfejs sieci Web, przejdź za**dostawca tożsamości SAML** i z tego miejsca, kliknij przycisk hello **"+"** -znajdujący się na dole hello hello ekranu toodisplay hello dodać informacje dostawcy tożsamości okienka i wykonania Witaj, następujące kroki:

    ![Dodaj dostawcę tożsamości](./media/active-directory-saas-saphana-tutorial/sap1.png)

    a. W hello **dodać informacje dostawcy tożsamości** okienka, Wklej zawartość hello hello XML metadanych, który został pobrany z portalu Azure, do hello **metadanych** pola tekstowego.

    ![Dodaj ustawienia dostawcy tożsamości](./media/active-directory-saas-saphana-tutorial/sap2.png)

    b. Jeśli zawartość hello hello dokumentu XML są prawidłowe, proces analizowania hello wyodrębnia hello tooinsert informacje wymagane do hello **podmiotu, identyfikator jednostki i wystawcy** pól w hello ogólne dane obszar ekranu i hello pól adres URL w hello Obszar ekranu docelowy, na przykład  **podstawowego adresu URL i adresu URL SingleSignOn (*)**.

    ![Dodaj ustawienia dostawcy tożsamości](./media/active-directory-saas-saphana-tutorial/sap3.png)

    c. W polu Nazwa hello hello danych ogólne obszar ekranu, wprowadź nazwę hello nowego logowania jednokrotnego SAML dostawcy tożsamości.

    > [!Note]
    > Nazwa Hello hello SAML IDP jest wymagana i musi być unikatowa. wygląda na to hello listę dostępnych IDPs SAML, który jest wyświetlany w przypadku wybrania SAML jako hello metodę uwierzytelniania dla programu SAP HANA XS toouse aplikacji, na przykład w obszarze ekranu uwierzytelniania hello narzędzia do administrowania artefaktu XS hello.

10. Zapisz szczegóły hello hello nowy dostawca tożsamości SAML. Wybierz **zapisać** toosave hello szczegóły dostawca tożsamości SAML hello i Dodaj hello nową SAML IDP toohello listę znanych IDPs SAML.

    ![Przyciskiem Zapisz](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. W Studio HANA w ramach właściwości systemu hello hello **konfiguracji** karcie, po prostu filtrowania ustawień przez **saml** i dostosować hello **assertion_timeout** z **10 s** za**120 s**.

    ![Ustawienie assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-a-sap-hana-test-user"></a>Tworzenie użytkownika testowego SAP HANA

toolog użytkowników tooenable usługi Azure AD w tooSAP HANA muszą mieć przydzielone do programu SAP HANA.
SAP HANA obsługę w czasie, który jest domyślnie włączone.

Jeśli potrzebujesz toocreate użytkownik ręcznie, wykonaj hello następujące kroki:

>[!Note]
>Uwierzytelnianie zewnętrzne hello używane przez użytkownika hello, można zmienić.
Użytkownicy zewnętrzni są uwierzytelniani, za pomocą zewnętrznego systemu, na przykład system protokołu Kerberos. Aby uzyskać szczegółowe informacje o tożsamości zewnętrznych, skontaktuj się z [administrator domeny](https://cloudplatform.sap.com/contact.html).

1. Otwórz hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) jako administrator i Włącz hello bazy danych użytkownika dla logowania jednokrotnego SAML.

    ![Utwórz użytkownika](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. Znaczników hello niewidoczne wyboru toohello rogu **SAML** i konfigurowanie hello łącza.

3. Kliknij przycisk **Dodaj** tooadd hello SAML IDP i kliknij przycisk **OK** wybranie hello odpowiednie IDP SAML.

4. Dodaj hello **tożsamości zewnętrznych** (np. W tym miejscu BrittaSimon) lub wybierz **"Wszystkie"** i kliknij przycisk **OK**.

    >[!Note]
    >Jeśli nie zaznaczono "Wszystkie" pole wyboru, a następnie hello nazwę użytkownika w HANA potrzebuje tooexactly dopasowania hello nazwy użytkownika hello w hello UPN przed sufiksem domeny hello (tj. BrittaSimon@contoso.com staje się BrittaSimon w HANA).

5. Do celów testowych, przypisać wszystkie **"XS"** użytkownika toohello ról.

    ![Przypisywanie ról](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > Należy podać te uprawnienia, które są odpowiednie dla Twojej przypadki użycia tylko.

6. Zapisz hello użytkownika.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSAP HANA.

![Przypisanie roli użytkownika hello][200] 

**tooassign tooSAP Simona Britta HANA, wykonaj następujące kroki hello:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **SAP HANA**.

    ![Przypisz użytkownika](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodaj przypisania Hello][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka SAP HANA hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji SAP HANA.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

