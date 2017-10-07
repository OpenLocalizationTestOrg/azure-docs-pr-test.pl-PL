---
title: "Samouczek: Integracji Azure Active Directory z podniesienia uprawnień LinkedIn | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i podnieść LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a>Samouczek: Integracji Azure Active Directory z LinkedIn podniesienia uprawnień

Z tego samouczka, dowiesz się, jak toointegrate LinkedIn podnoszenia uprawnień w usłudze Azure Active Directory (Azure AD).

Integrowanie LinkedIn podniesienia uprawnień w usłudze Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLinkedIn podniesienie uprawnień
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLinkedIn podniesienie uprawnień (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z LinkedIn podniesienia uprawnień, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Podniesienie poziomu LinkedIn jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie podniesienia uprawnień LinkedIn z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-linkedin-elevate-from-hello-gallery"></a>Dodawanie podniesienia uprawnień LinkedIn z galerii hello
tooconfigure hello integracji LinkedIn podniesienia uprawnień w usłudze Azure Active Directory, należy tooadd podniesienia uprawnień LinkedIn z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd LinkedIn podniesienia uprawnień z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **LinkedIn podniesienia uprawnień**. Z poziomu panelu wyników, kliknij przycisk **LinkedIn podniesienia uprawnień** tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LinkedIn podnoszenia uprawnień w oparciu o użytkownika testowego o nazwie "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w LinkedIn podniesienia uprawnień jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w LinkedIn podniesienia uprawnień musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w LinkedIn podniesienia uprawnień.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z LinkedIn podniesienia uprawnień, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego podniesienia uprawnień LinkedIn](#creating-a-linkedin-elevate-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji LinkedIn podniesienia uprawnień.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z LinkedIn podniesienia uprawnień, wykonaj następujące kroki hello:**

1. W portalu zarządzania Azure hello na powitania **podniesienia uprawnień LinkedIn** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour LinkedIn podniesienia uprawnień dzierżawy z uprawnieniami administratora.

4. W **Centrum konta**, kliknij przycisk **ustawienia globalne** w obszarze **ustawienia**. Zaznacz również **podniesienie uprawnień — podniesienie poziomu testu AAD** z listy rozwijanej hello.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. Polecenie **lub kliknij tutaj tooload i skopiuj poszczególnych pól formularza hello** i skopiuj **identyfikator jednostki** i **adresu Url potwierdzenia konsumenta dostępu (ACS)**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. W portalu Azure w obszarze **LinkedIn podniesienie poziomu domeny i adres URL**, wykonaj następujące kroki, jeśli chcesz, aby tooconfigure logowania jednokrotnego hello w **inicjowane IdP** tryb

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    a. W hello **identyfikator** pole tekstowe, wprowadź hello **identyfikator jednostki** skopiowany z portalu LinkedIn 

    b. W hello **adres URL odpowiedzi** pole tekstowe, wprowadź hello **potwierdzenia konsumenta dostępu (ACS) adres Url** skopiowany z portalu LinkedIn

7. Jeśli chcesz, aby tooconfigure logowania jednokrotnego w **inicjowane SP**, następnie kliknij opcję Ustawienia Pokaż zaawansowane adres URL w sekcji konfiguracji hello i konfigurowania rejestracji hello na adres URL hello następującego wzorca:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. Podniesienie poziomu LinkedIn aplikacji oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji. powitania po zrzut ekranu przedstawia przykład tego. Witaj wartość domyślną **identyfikator użytkownika** jest **user.userprincipalname** , ale LinkedIn podniesienia uprawnień oczekuje toobe, ten adres e-mail użytkownika hello zamapowana. W przypadku którego można użyć **user.mail** atrybutu z listy hello lub użyj wartości atrybutu odpowiednie hello zgodnie z konfiguracją organizacji. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustaw hello atrybuty. Należy tooadd innego oświadczeń o nazwie **działu** i wartość hello musi toobe mapowane za**user.department**.

    | Nazwa atrybutu | Wartość atrybutu |
    | --- | --- |    
    | Dział| User.Department |

      ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      a. Dodaj atrybut tooopen hello atrybutu szczegóły strony, kliknij polecenie Dodaj atrybut działu hello, jak pokazano poniżej-

      ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      b. Polecenie **Ok** toosave hello atrybutu.

      c. Zmień nazwę hello atrybutu hello **emailaddress** za**e-mail**.


10. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. Kliknij pozycję **Zapisz**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. Przejdź za**ustawienia administratora LinkedIn** sekcji. Przekaż plik XML hello pobrany z hello portalu Azure, klikając hello opcja pliku XML, Przekaż.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. Kliknij przycisk **na** tooenable logowania jednokrotnego. Stan rejestracji Jednokrotnej ulegnie zmianie z **niepołączone** zbyt**połączony**

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**. 

### <a name="creating-a-linkedin-elevate-test-user"></a>Tworzenie użytkownika testowego LinkedIn podniesienia uprawnień

Połączone podniesienia uprawnień aplikacji obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników zostaną utworzone w aplikacji hello automatycznie. Na stronie Ustawienia administratora hello na przełączniku portalu hello przerzucania podniesienia uprawnień LinkedIn hello **automatycznie przypisywać licencje** tooactive tooenable tylko w czasie inicjowania obsługi administracyjnej i to również przypisać licencję użytkownika toohello.

   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooLinkedIn dostępu podniesienie uprawnień.

![Przypisz użytkownika][200] 

**tooassign tooLinkedIn Simona Britta podniesienie uprawnień, wykonaj następujące kroki hello:**

1. W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **LinkedIn podniesienia uprawnień**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka hello LinkedIn podniesienia uprawnień w hello Panel dostępu, należy pobrać hello Azure logowania jednokrotnego strony i na po pomyślnym logowania, należy pobrać w aplikacji, LinkedIn podniesienia uprawnień.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Samouczek: Konfigurowanie LinkedIn podniesienia uprawnień dla użytkownika automatycznego inicjowania obsługi administracyjnej w usłudze Azure Active Directory](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
