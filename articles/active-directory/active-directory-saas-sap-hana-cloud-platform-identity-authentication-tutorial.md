---
title: "Samouczek: Integracji Azure Active Directory z uwierzytelnianie tożsamości SAP HANA chmury platformy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SAP HANA Cloud Platform tożsamość uwierzytelniania."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a>Samouczek: Integracji Azure Active Directory z uwierzytelnianie tożsamości SAP HANA Cloud Platform

Z tego samouczka, dowiesz się, jak toointegrate SAP HANA chmury platformy tożsamość uwierzytelniania za pomocą usługi Azure Active Directory (Azure AD). Uwierzytelnianie tożsamości SAP HANA Cloud Platform jest używana jako serwera proxy IdP tooaccess SAP aplikacji przy użyciu usługi Azure AD jako hello IdP głównego.

Integrowanie SAP HANA Cloud Platform tożsamości uwierzytelniania z usługi Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do aplikacji tooSAP
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSAP aplikacji rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).


## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z uwierzytelnianie tożsamości SAP HANA Cloud Platform, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- A **uwierzytelnianie tożsamości SAP HANA Cloud Platform** logowanie Jednokrotne włączone subskrypcji


>[!NOTE] 
>tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.
>

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.

Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie uwierzytelniania tożsamości SAP HANA chmury platformy z galerii hello
2. Konfigurowanie i testowania logowania jednokrotnego programu Azure AD

Przed rozpoczęciem pracy hello szczegółowe informacje techniczne, jest istotne toounderstand hello pojęcia, które chcesz zacząć toolook w. Witaj uwierzytelnianie tożsamości SAP HANA Cloud Platform i Azure Active Directory federation umożliwia tooimplement logowania jednokrotnego w aplikacji lub usług chronione przez usługi AAD (jako IdP) przy użyciu aplikacje SAP i chronione przez SAP HANA Cloud Platform tożsamości usługi Uwierzytelnianie.

Obecnie uwierzytelnianie tożsamości SAP HANA Cloud Platform działa jako dostawca tożsamości serwera Proxy tooSAP — aplikacje. Usługa Azure Active Directory z kolei działa jako hello wiodące dostawcy tożsamości w tej instalacji. 

powitania po diagram ilustruje to:    

![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

W przypadku tej konfiguracji dzierżawy uwierzytelnianie tożsamości SAP HANA Cloud Platform zostanie skonfigurowany jako zaufanych aplikacji w usłudze Azure Active Directory. 

Wszystkie aplikacje SAP i usługi mają tooprotect za pośrednictwem w ten sposób następnie są konfigurowane w konsoli zarządzania uwierzytelnianie tożsamości SAP HANA Cloud Platform hello!

To oznacza, że autoryzacji za udzielanie dostępu tooSAP aplikacji i usług potrzeb tootake miejscu uwierzytelnianie tożsamości SAP HANA Cloud Platform dla instalacji (w przeciwieństwie tooconfiguring autoryzacji w usłudze Azure Active Directory).

Konfigurując uwierzytelnianie tożsamości SAP HANA chmury platformy jako aplikację za pomocą hello Azure Active Directory Marketplace, nie potrzebujesz tootake nad Konfigurowanie wymagane oddzielne oświadczenia / tooproduce potrzebne potwierdzenia języka SAML i przekształcenia token uwierzytelniania prawidłowy dla aplikacji SAP.

>[!NOTE] 
>Obecnie obie strony tylko przetestowano Jednokrotną w sieci Web. Przepływy potrzebne w przypadku aplikacji do interfejsu API lub interfejsu API do interfejsu API komunikacji powinny działać, ale nie zostały one przetestowane, jeszcze. Zostaną one przetestowane w ramach kolejnych działań.
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a>Dodaj uwierzytelnianie tożsamości SAP HANA Cloud Platform z galerii hello
tooconfigure hello integracji SAP HANA Cloud Platform tożsamości uwierzytelniania w usłudze Azure Active Directory, należy tooadd uwierzytelnianie tożsamości SAP HANA Cloud Platform z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd SAP HANA platformy tożsamość uwierzytelniania w chmurze z galerii hello, wykonaj następujące kroki hello:**

1. W hello [ **portalu zarządzania Azure**](https://portal.azure.com)na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **uwierzytelnianie tożsamości SAP HANA Cloud Platform**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. W panelu wyników hello, wybierz **uwierzytelnianie tożsamości SAP HANA Cloud Platform**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji możesz Konfiguracja i testowanie usługi Azure AD SSO z SAP HANA Cloud Platform tożsamości uwierzytelnianie oparte na użytkownika testowego o nazwie "Britta Simona".

Aby toowork logowania jednokrotnego usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w SAP HANA Cloud Platform tożsamości uwierzytelniania jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w uwierzytelnianie tożsamości SAP HANA chmury platformy musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w uwierzytelnianie tożsamości SAP HANA chmury platformy.

tooconfigure i testowania Azure AD z logowania jednokrotnego SAP HANA Cloud Platform tożsamości uwierzytelniania, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego uwierzytelnianie tożsamości SAP HANA Cloud Platform](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave odpowiednikiem Simona Britta w SAP HANA chmury platformy tożsamości uwierzytelniania, który jest jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-sso"></a>Konfigurowanie usługi Azure AD logowania jednokrotnego.

W tej sekcji włączenia funkcji logowania jednokrotnego usługi Azure AD w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne do aplikacji uwierzytelnianie tożsamości SAP HANA Cloud Platform.

Uwierzytelnianie tożsamości SAP HANA chmury platformy aplikacji oczekuje potwierdzenia SAML hello w określonym formacie. Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji. powitania po zrzut ekranu przedstawia przykład tego.

![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

**tooconfigure Azure AD SSO z SAP HANA platformy tożsamość uwierzytelniania w chmurze, wykonaj następujące kroki hello:**

1. W portalu zarządzania Azure hello na powitania **uwierzytelnianie tożsamości SAP HANA Cloud Platform** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej][5]

3. W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, jeśli aplikacja SAP oczekuje na przykład "imię" atrybutu. W oknie dialogowym atrybuty tokenu SAML hello Dodaj atrybut "imię" hello.
 1. Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.
 
    ![Konfigurowanie rejestracji jednokrotnej][6]

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. W hello **nazwa atrybutu** pole tekstowe, nazwa atrybutu hello typu "imię".
 3. Z hello **wartość atrybutu** listy, wybierz opcję hello wartość atrybutu "user.givenname".
 4. Kliknij przycisk **OK**.

4. Na powitania **adresy URL i domeny uwierzytelniania tożsamości chmury platformy SAP HANA** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. W hello **na adres URL logowania** tekstowym, wpisz znak hello na adres URL dla aplikacji SAP hello.
 2. W hello **identyfikator** pole tekstowe, wartość hello typu następującego wzorca:`<entity-id>.accounts.ondemand.com` 
    * Jeśli nie znasz tej wartości, wykonaj hello uwierzytelnianie tożsamości SAP HANA Cloud Platform dokumentacji [dzierżawy SAML 2.0 konfiguracji](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).

5. Na powitania **konfiguracji uwierzytelniania tożsamości chmury platformy SAP HANA** kliknij **skonfigurować SAP HANA platformy tożsamość uwierzytelniania w chmurze** tooopen **Konfigurowanie logowania jednokrotnego** okna dialogowego. Następnie kliknij **SAML XML metadanych** i Zapisz plik hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, przejdź tooSAP konsoli administracyjnej uwierzytelniania tożsamości HANA Cloud Platform. adres URL Hello ma hello następującego wzorca:`https://<tenant-id>.accounts.ondemand.com/admin`
 * Następnie wykonaj dokumentacji hello na uwierzytelnianie tożsamości SAP HANA Cloud Platform zbyt[Konfigurowanie usługi Microsoft Azure AD jako firmowe dostawcy tożsamości na uwierzytelnianie tożsamości SAP HANA Cloud Platform](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html). 

7. W portalu zarządzania Azure powitania kliknij **zapisać** przycisku.
8. Nadal hello następujące kroki tylko wtedy, gdy mają tooadd i włączenia funkcji logowania jednokrotnego dla innej aplikacji SAP. Powtórz kroki w obszarze hello sekcję "Dodawanie SAP HANA platformy tożsamość uwierzytelniania w chmurze z galerii hello" tooadd inne wystąpienie programu SAP HANA Cloud Platform tożsamości uwierzytelniania.
9. W portalu zarządzania Azure hello na powitania **uwierzytelnianie tożsamości SAP HANA Cloud Platform** strona integracji aplikacji, kliknij przycisk **połączonej logowania jednokrotnego**.

    ![Skonfiguruj połączonego logowania jednokrotnego](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. Następnie Zapisz konfigurację hello.

>[!NOTE] 
>Nowa aplikacja Hello będzie korzystać z konfiguracji logowania jednokrotnego hello hello poprzedniej SAP aplikacji. Upewnij się, możesz Użyj hello tej samej firmowej dostawców tożsamości w hello konsoli administracyjnej uwierzytelniania tożsamości platformy SAP HANA chmury.
>

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego w hello nowego portalu o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.
  2. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.
  3. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.
  4. Kliknij przycisk **Utwórz**. 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a>Tworzenie użytkownika testowego uwierzytelnianie tożsamości SAP HANA Cloud Platform

Nie trzeba toocreate użytkownika na uwierzytelnianie tożsamości SAP HANA Cloud Platform. Użytkownicy, którzy są w magazynie użytkownika hello Azure AD można użyć funkcji logowania jednokrotnego hello.

Uwierzytelnianie tożsamości SAP HANA chmurze platforma obsługuje hello opcję federacji tożsamości. Ta opcja umożliwia toocheck aplikacji hello, jeśli użytkownik hello uwierzytelniony przez dostawcę tożsamości firmy hello w hello użytkownika magazynu programu SAP HANA platformy tożsamość uwierzytelniania w chmurze. 

W ustawieniu domyślny hello, hello opcja federacji tożsamości jest wyłączona. Włączenie federacji tożsamości tylko użytkownicy hello zaimportowane w SAP HANA Cloud Platform tożsamości uwierzytelniania są aplikacji hello tooaccess stanie. 

Aby uzyskać więcej informacji na temat tooenable lub wyłącz federacji tożsamości z SAP HANA platformy tożsamość uwierzytelniania w chmurze, zobacz temat włączyć Federację tożsamości z SAP HANA platformy tożsamość uwierzytelniania w chmurze w [Konfigurowanie federacji tożsamości z hello użytkownika magazynu programu SAP HANA platformy tożsamość uwierzytelniania w chmurze. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooSAP dostęp do uwierzytelniania tożsamości platformy HANA w chmurze.

![Przypisz użytkownika][200] 

**tooassign tooSAP Simona Britta HANA uwierzytelnianie tożsamości platformy chmury, wykonaj hello następujące kroki:**

1. W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **uwierzytelnianie tożsamości SAP HANA Cloud Platform**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    

### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą hello panelu dostępu.

Po kliknięciu kafelka uwierzytelnianie tożsamości SAP HANA Cloud Platform hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour uwierzytelnianie tożsamości SAP HANA Cloud Platform aplikacji.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png