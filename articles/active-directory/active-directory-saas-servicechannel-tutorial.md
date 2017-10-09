---
title: 'Samouczek: Integracji Azure Active Directory z obiektu ServiceChannel | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i obiektu ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a>Samouczek: Integracji Azure Active Directory z obiektu ServiceChannel

Z tego samouczka, dowiesz się, jak toointegrate kanale usługi z usługą Azure Active Directory (Azure AD).

Integrowanie kanale usługi z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooServiceChannel
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooServiceChannel (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z obiektu ServiceChannel należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Obiektu ServiceChannel jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie obiektu ServiceChannel z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-servicechannel-from-hello-gallery"></a>Dodawanie obiektu ServiceChannel z galerii hello
tooconfigure hello integracji kanale usługi z usługą Azure AD, należy tooadd obiektu ServiceChannel z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd obiektu ServiceChannel z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **obiektu ServiceChannel**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. W panelu wyników hello zaznacz **obiektu ServiceChannel**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z obiektu ServiceChannel w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w kanale usługi jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w kanale usługi musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w kanale usługi.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z obiektu ServiceChannel, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego obiektu ServiceChannel](#creating-a-servicechannel-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji obiektu ServiceChannel.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z obiektu ServiceChannel, wykonaj następujące kroki hello:**

1. W portalu zarządzania Azure hello na powitania **obiektu ServiceChannel** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. Na powitania **adresy URL i domeny obiektu ServiceChannel** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    a. W hello **identyfikator** pole tekstowe, wartość hello typu jako:`http://adfs.<domain>.com/adfs/service/trust`

    b. W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<customer domain>.servicechannel.com/saml/acs`

    > [!NOTE] 
    > Należy pamiętać, że nie są one hello wartości rzeczywistych. Masz tooupdate tych wartości za pomocą hello rzeczywisty identyfikator i odpowiedzi adresu URL. W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator. Skontaktuj się z [zespołem pomocy technicznej obiektu ServiceChannel](https://servicechannel.zendesk.com/hc/en-us) tooget tych wartości.

4. Aplikacja obiektu ServiceChannel oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji. powitania po zrzut ekranu przedstawia przykład tego. **NameIdentifier (identyfikator użytkownika)** hello tylko obowiązkowe oświadczeń i hello wartość domyślna to **user.userprincipalname** , ale ta toobe zamapowana oczekuje obiektu ServiceChannel **user.mail**. Jeśli planujesz Inicjowanie obsługi użytkowników tylko w czasie tooenable, należy dodać powitania po oświadczenia, jak pokazano poniżej. **Rola** oświadczeń musi toobe mapowane za**user.assignedroles** zawierającą hello roli użytkownika hello.  

    Może się odwoływać przewodnik obiektu ServiceChannel [tutaj](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) więcej wskazówki dotyczące oświadczeń.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > Kliknij [tutaj](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow jak tooconfigure **roli** w usłudze Azure AD

5. W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustaw hello atrybuty.

    | Nazwa atrybutu | Wartość atrybutu |
    | --- | --- |    
    | Rola| User.assignedroles |

    a. Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    b. W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.
    
    c. Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.
    
    d. Kliknij przycisk **Ok**
    
6. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. Kliknij pozycję **Zapisz**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. Na powitania **konfiguracji obiektu ServiceChannel** kliknij **skonfigurować obiektu ServiceChannel** tooopen **Konfigurowanie logowania jednokrotnego** okna. Należy pamiętać, hello **identyfikator jednostka SAML** z hello **krótkimi opisami** sekcji.

9. tooconfigure rejestracji jednokrotnej w **obiektu ServiceChannel** strony, należy pobrać hello toosend **certyfikatu (Base64)** i **identyfikator jednostki SAML** zbyt[ Zespołem pomocy technicznej obiektu ServiceChannel](https://servicechannel.zendesk.com/hc/en-us). One będzie skonfigurowanie tego numeru w kolejności toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML.

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**. 

### <a name="creating-a-servicechannel-test-user"></a>Tworzenie użytkownika testowego obiektu ServiceChannel

Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników zostaną utworzone w aplikacji hello automatycznie. Aby Inicjowanie obsługi użytkowników pełne, skontaktuj się z [obiektu ServiceChannel zespołem pomocy technicznej](https://servicechannel.zendesk.com/hc/en-us)

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooServiceChannel dostępu.

![Przypisz użytkownika][200] 

**tooassign tooServiceChannel Simona Britta wykonaj hello następujące kroki:**

1. W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **obiektu ServiceChannel**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka obiektu ServiceChannel hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour obiektu ServiceChannel aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png