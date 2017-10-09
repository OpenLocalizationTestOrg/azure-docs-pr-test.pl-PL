---
title: 'Samouczek: Integracji Azure Active Directory z SAP Business obiektu chmury | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SAP Business obiektu chmury."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a>Samouczek: Integracji Azure Active Directory z SAP Business obiektu chmury

Z tego samouczka, dowiesz się, jak toointegrate SAP Business obiektu chmury z usługą Azure Active Directory (Azure AD).

Możesz uzyskać hello następujące korzyści podczas integracji z usługą Azure AD SAP Business obiektu chmury:

- W usłudze Azure AD można kontrolować, kto ma dostęp tooSAP firm obiektu chmury.
- TooSAP Twojego użytkowników biznesowych obiektu chmury mogą automatycznie zaloguj przy użyciu rejestracji jednokrotnej i konta usługi Azure AD.
- Możesz zarządzać kont w jednej, centralnej lokalizacji, hello portalu Azure.

toolearn więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooset się integracji usługi Azure AD z SAP Business obiektu chmury, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Chmura obiektu SAP Business, z logowanie jednokrotne włączone

> [!NOTE]
> W przypadku testowania czynności hello w tym samouczku, zaleca się nie przetestować ich w środowisku produkcyjnym.

Zalecenia dotyczące testowania czynności hello w tym samouczku:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [Pobierz bezpłatną wersję próbną miesięcznego](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. 

Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodaj SAP Business obiektu chmury z galerii hello.
2. Instalowanie i testowanie usługi Azure AD rejestracji jednokrotnej.

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a>Dodaj SAP Business obiektu chmury z galerii hello
tooset się integracji hello SAP Business obiektu chmury z usługą Azure AD w galerii hello Dodaj SAP Business obiektu chmury tooyour listę zarządzanych aplikacji SaaS.

tooadd SAP Business obiektu chmury z galerii hello:

1. W hello [portalu Azure](https://portal.azure.com), w menu po lewej stronie Witaj, wybierz **usługi Azure Active Directory**. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.

    ![Strona aplikacji Hello Enterprise][2]
    
3. tooadd nowej aplikacji, wybierz **nowej aplikacji**.

    ![Nowy przycisk aplikacji Hello][3]

4. W polu wyszukiwania hello wpisz **SAP Business obiektu chmury**.

    ![pole wyszukiwania Hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. W panelu wyników hello zaznacz **SAP Business obiektu chmury**, a następnie wybierz **Dodaj**.

    ![SAP Business obiektu chmury hello listy wyników](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a>Instalowanie i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji możesz zdefiniować i test usługi Azure AD rejestracji jednokrotnej z SAP Business obiektu chmury w oparciu o nazwie użytkownika testowego *Simona Britta*.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi użytkownika odpowiednikiem tooknow hello Azure AD w chmurze programu SAP Business obiektu. Należy ustanowić relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w chmurze programu SAP Business obiektu.

tooestablish hello połączyć relacji w SAP Business obiektu chmury, **Username**, przypisz wartość hello hello **nazwy użytkownika** w usłudze Azure AD.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z chmurą obiektu SAP Business, pełną hello następujące zadania:

1. [Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#set-up-azure-ad-single-sign-on). Konfiguruje toouse użytkownika tej funkcji.
2. [Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user). Testy usługi Azure AD rejestracji jednokrotnej z użytkownikiem hello Simona Britta.
3. [Tworzenie użytkownika testowego SAP Business obiektu chmury](#create-an-sap-business-object-cloud-test-user). Tworzy odpowiednikiem Simona Britta SAP Business obiektu chmurze, który jest połączony toohello reprezentacja hello użytkownika usługi Azure AD.
4. [Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user). Konfiguruje toouse Simona Britta usługi Azure AD rejestracji jednokrotnej.
5. [Test rejestracji jednokrotnej](#test-single-sign-on). Sprawdza, czy konfiguracja tego hello działa.

### <a name="set-up-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji należy włączyć usługi Azure AD pojedynczego logowania jednokrotnego w hello portalu Azure. Następnie skonfigurowaniu rejestracji jednokrotnej w aplikacji SAP Business obiektu chmury.

tooset się usługi Azure AD rejestracji jednokrotnej z SAP Business obiektu chmury:

1. W portalu Azure na powitania hello **SAP Business obiektu chmury** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.

    ![Wybierz rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** strony, dla **tryb**, wybierz pozycję **na języku SAML logowania jednokrotnego**.
 
    ![Wybierz na języku SAML logowania jednokrotnego](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. W obszarze **adresy URL i SAP Business obiektu chmury domeny**pełnego hello następujące kroki:

    1. W hello **adres URL logowania** wprowadź adres URL, który ma hello następującego wzorca: 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. W hello **identyfikator** wprowadź adres URL, który ma hello następującego wzorca:
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![Adresy URL i SAP Business obiektu chmury domeny adresów URL stron](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > wartości Hello w tych adresów URL dotyczą tylko pokaz. Aktualizacja hello wartościami hello rzeczywiste logowania jednokrotnego adres URL adresu URL i identyfikator. tooget hello adres URL logowania, skontaktuj się z pomocą hello [zespołem pomocy technicznej SAP Business obiektu chmury klienta](https://www.sap.com/product/analytics/cloud-analytics.support.html). Adres URL identyfikatora hello można uzyskać, pobierając hello SAP Business obiektu chmury metadanych z konsoli administracyjnej hello. Wyjaśnienie jest zawarte w dalszej części samouczka hello. 

4. W obszarze **certyfikat podpisywania SAML**, wybierz pozycję **XML metadanych**. Następnie zapisz plik metadanych hello na tym komputerze.

    ![Wybierz XML metadanych](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. Wybierz pozycję **Zapisz**.

    ![Wybierz opcję Zapisz](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy SAP Business obiektu chmury tooyour jako administrator.

7. Wybierz **Menu** > **systemu** > **administracji**.
    
    ![Wybierz Menu, a następnie systemu, a następnie administracji](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. Na powitania **zabezpieczeń** kartę, zaznacz hello **Edytuj** ikona (pióra).
    
    ![Na karcie Zabezpieczenia hello wybierz ikonę edycji hello](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. Aby uzyskać **metodę uwierzytelniania**, wybierz pozycję **SAML pojedynczego logowania jednokrotnego (SSO)**.

    ![Wybierz SAML logowania jednokrotnego dla metod uwierzytelniania hello](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. toodownload hello dostawcy metadanych usługi (krok 1), wybierz opcję **Pobierz**. W pliku metadanych hello, należy znaleźć i skopiować hello **entityID** wartości. W hello Azure portalu, w obszarze **adresy URL i SAP Business obiektu chmury domeny**, Wklej wartość hello hello **identyfikator** pole.

    ![Skopiuj i Wklej hello entityID wartość](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. w obszarze hello tooupload hello dostawcy metadanych usługi (krok 2) w pliku hello, który został pobrany z portalu Azure, **metadanych Przekaż dostawcy tożsamości**, wybierz pozycję **przekazać**.  

    ![W obszarze metadanych Przekaż dostawcy tożsamości wybierz przekazywania](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. W hello **atrybut użytkownika** listy, wybierz hello atrybut użytkownika (krok 3) mają toouse implementacji. Ten atrybut użytkownika mapuje toohello dostawcy tożsamości. Atrybut niestandardowy na stronie powitania użytkownika, użyj hello tooenter **niestandardowe mapowanie SAML** opcji. Lub użytkownik może wybrać jedną **E-mail** lub **identyfikator użytkownika** jako atrybut użytkownika hello. W naszym przykładzie wybrano **E-mail** możemy mapowane hello oświadczenia identyfikatora użytkownika z hello **userprincipalname** atrybutu w hello **atrybuty użytkownika** części hello Portalu Azure. Zapewnia to adres e-mail użytkownika unikatowy, który jest wysyłany toohello aplikacji w chmurze programu SAP Business obiektu w każdym pomyślnym odpowiedzi SAML.

    ![Wybierz atrybut użytkownika](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. Konto hello tooverify z hello dostawcy tożsamości (krok 4) w hello **poświadczeń logowania (Poczta E-mail)** wprowadź adres e-mail użytkownika hello. Następnie wybierz opcję **Sprawdź konto**. Hello system dodaje konto użytkownika toohello poświadczenia logowania.

    ![Wprowadź adres e-mail, a następnie wybierz zweryfikować konta](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. Wybierz hello **zapisać** ikony.

    ![Zapisz](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> Możesz przeczytać zwięzły wersji tych instrukcji w hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji! Po dodaniu aplikacji hello wybierając **usługi Active Directory** > **aplikacje dla przedsiębiorstw**, wybierz pozycję hello **rejestracji jednokrotnej** kartę. Dostęp można uzyskać dokumentację hello osadzone w hello **konfiguracji** sekcji u dołu hello hello strony. Aby uzyskać więcej informacji, zobacz [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
W tej sekcji utworzysz użytkownika testu o nazwie Simona Britta w hello portalu Azure.

toocreate użytkownika testowego w usłudze Azure AD:

1. W portalu Azure, w menu po lewej stronie powitania hello wybierz **usługi Azure Active Directory**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, wybierz opcję **użytkowników i grup**, a następnie wybierz **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okno dialogowe, wybierz opcję **Dodaj**.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. W hello **użytkownika** okno dialogowe, pełną hello następujące kroki:
 
    1. W hello **nazwa** wprowadź **BrittaSimon**.

    2. W hello **nazwy użytkownika** wprowadź adres e-mail użytkownika hello Simona Britta hello.

    3. Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.

    4. Wybierz pozycję **Utwórz**.

        ![okno dialogowe Hello użytkownika](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Tworzenie użytkowników usługi Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a>Tworzenie użytkownika testowego SAP Business obiektu chmury

Użytkownicy usługi Azure AD należy udostępnić w chmurze programu SAP Business obiektu przed móc zalogować się tooSAP firm obiektu chmury. W chmurze obiektu biznesowych SAP Inicjowanie obsługi to zadanie ręczne.

tooprovision konto użytkownika:

1. Zaloguj się tooyour SAP Business obiektu chmury witryny firmy jako administrator.

2. Wybierz **Menu** > **zabezpieczeń** > **użytkowników**.

    ![Dodawanie pracownika](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. Na powitania **użytkowników** , tooadd nowe szczegóły użytkownika, wybierz  **+** . 

    ![Strona dodawania użytkowników](./media/active-directory-saas-sapboc-tutorial/user4.png)

    Następnie należy wykonać następujące kroki hello:

    1. W hello **identyfikator użytkownika** wprowadź identyfikator użytkownika hello hello użytkownika, takie jak **Britta**.

    2. W hello **imię** tak samo, jak wprowadź hello imię użytkownika hello **Britta**.

    3. W hello **nazwisko** tak samo, jak wprowadź hello nazwisko użytkownika hello **Simona**.

    4. W hello **nazwa WYŚWIETLANA** wpisz pełną nazwę użytkownika hello hello tak samo, jak **Simona Britta**.

    5. W hello **E-MAIL** tak samo, jak wprowadź adres e-mail użytkownika hello hello  **brittasimon@contoso.com** .

    6. Na powitania **Wybieranie ról** wybierz hello odpowiednią rolę dla użytkownika hello, a następnie wybierz **OK**.

      ![Wybór roli](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. Wybierz hello **zapisać** ikony.  


### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz Zezwalaj użytkownikowi hello Simona Britta toouse usługi Azure AD rejestracji jednokrotnej, przyznając hello użytkownika konta dostępu tooSAP firm obiektu chmury.

tooassign tooSAP Simona Britta firm obiektu chmury:

1. W portalu Azure hello Otwórz widok aplikacji hello, a następnie przejdź toohello widok katalogu. Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **SAP Business obiektu chmury**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. W menu po lewej stronie powitania wybierz **użytkowników i grup**.

    ![Wybierz użytkowników i grup][202] 

4. Wybierz pozycję **Dodaj**. Następnie na powitania **Dodaj przydziału** wybierz pozycję **użytkowników i grup**.

    ![Strona Dodawanie przypisanie Hello][203]

5. Na powitania **użytkowników i grup** strony w hello listę użytkowników, wybierz opcję **Simona Britta**.

6. Na powitania **użytkowników i grup** wybierz pozycję **wybierz**.

7. Na powitania **Dodaj przydziału** wybierz pozycję **przypisać**.

![Przypisanie roli użytkownika hello][200] 
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować przy użyciu panelu dostępu hello konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego.

Po wybraniu kafelka SAP Business obiektu chmury hello w panelu dostępu hello powinny być automatycznie zalogowano tooyour aplikacji SAP Business obiektu chmury.

Aby uzyskać więcej informacji na temat hello panel dostępu, zobacz [panelu dostępu toohello wprowadzenie](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

