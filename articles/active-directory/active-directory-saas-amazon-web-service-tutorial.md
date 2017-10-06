---
title: "Samouczek: Integracji Azure Active Directory z usług sieci Web firmy Amazon (AWS) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usług sieci Web firmy Amazon (AWS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a>Samouczek: Integracji Azure Active Directory z usług sieci Web firmy Amazon (AWS)

Z tego samouczka, dowiesz się, jak toointegrate Amazon usług sieci Web (AWS) z usługą Azure Active Directory (Azure AD).

Integrowanie usługi Amazon Web Services (AWS) z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooAmazon usług sieci Web (AWS)
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAmazon usług sieci Web (AWS) (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z Amazon Web Services (AWS), należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Amazon Web Services (AWS) jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie Amazon Web Services (AWS) z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a>Dodawanie Amazon Web Services (AWS) z galerii hello
tooconfigure hello integracji z usługami sieci Web Amazon (AWS) do usługi Azure AD, należy tooadd Amazon Web Services (AWS) z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd Amazon usług sieci Web (AWS) z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[Azure Portal](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **Amazon Web Services (AWS)**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. W panelu wyników hello, wybierz **Amazon Web Services (AWS)**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Amazon Web usługi (AWS) w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Amazon Web Services (AWS) jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Amazon Web Services (AWS) musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Amazon Web Services (AWS).

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Amazon Web Services (AWS), należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego usług Amazon Web Services](#creating-an-amazon-web-services-test-user)**  -toohave odpowiednikiem Simona Britta w Amazon usług sieci Web (AWS), będącego jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji usługi sieci Web firmy Amazon (AWS).

**tooconfigure usługi Azure AD rejestracji jednokrotnej z Amazon usług sieci Web (AWS) wykonaj następujące kroki hello:**

1. W hello portalu Azure na powitania **Amazon Web Services (AWS)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. Na powitania **Amazon Web Services (AWS) domeny i adres URL** sekcji, hello użytkownik nie ma tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. Witaj Amazon Web Services (AWS) aplikacji oczekuje potwierdzenia SAML hello w określonym formacie. Skonfiguruj powitania po oświadczeń dla tej aplikacji. Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji. powitania po zrzut ekranu przedstawia przykład tego.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w powyższy obraz powitania i wykonywać hello następujące kroki:
    
    | Nazwa atrybutu  | Wartość atrybutu | przestrzeń nazw |
    | --------------- | --------------- | --------------- |
    | RoleSessionName | User.userPrincipalName | https://awS.amazon.com/SAML/Attributes |
    | Rola            | User.assignedroles |  https://awS.amazon.com/SAML/Attributes |
    
    >[!TIP]
    >Należy użytkownika hello tooconfigure inicjowania obsługi usługi Azure AD toofetch wszystkie role hello z konsoli usług AWS. Można znaleźć hello inicjowania obsługi administracyjnej poniższe kroki.

    a. Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    b. W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    c. Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza. Dodaj wartość Namespace hello podane powyżej.
    
    d. Kliknij przycisk **OK**.

7. Kliknij przycisk **zapisać** przycisk ustawień hello toosave na platformie Azure.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. W oknie innej przeglądarki, witryny firmy Amazon Web Services (AWS) tooyour logowania jako administrator.

9. Kliknij przycisk **konsoli głównej**.
   
    ![Konfigurowanie rejestracji jednokrotnej][11]

10. Kliknij przycisk **IAM** z **zabezpieczeń, tożsamości i zgodności** usługi.
   
    ![Konfigurowanie rejestracji jednokrotnej][12]

11. Kliknij przycisk **dostawców tożsamości**, a następnie kliknij przycisk **Tworzenie dostawcy**.
   
    ![Konfigurowanie rejestracji jednokrotnej][13]

12. Na powitania **Konfigurowanie dostawcy** okna dialogowego wykonaj hello następujące kroki:
   
    ![Konfigurowanie rejestracji jednokrotnej][14]
 
    a. Jako **typ dostawcy**, wybierz pozycję **SAML**.

    b. W hello **Nazwa dostawcy** tekstowym, wpisz nazwę dostawcy (np.: *drewna*).

    c. tooupload pliku metadanych pobranych, kliknij przycisk **wybierz plik**.

    d. Kliknij przycisk **następny krok**.

13. Na powitania **Sprawdź informacje o dostawcy** strony okna dialogowego, kliknij przycisk **Utwórz**. 
    
    ![Konfigurowanie rejestracji jednokrotnej][15]

14. Kliknij przycisk **ról**, a następnie kliknij przycisk **Utwórz nową rolę**. 
    
    ![Konfigurowanie rejestracji jednokrotnej][16]

15. Na powitania **Ustaw nazwę roli** okna dialogowego, wykonaj następujące kroki hello: 
    
    ![Konfigurowanie rejestracji jednokrotnej][17] 

    a. W hello **nazwy roli** tekstowym, wpisz nazwę roli (np.: *TestUser*). 

    b. Kliknij przycisk **następny krok**.

16. Na powitania **wybierz typ roli** okna dialogowego, wykonaj następujące kroki hello: 
    
    ![Konfigurowanie rejestracji jednokrotnej][18] 

    a. Wybierz **roli dostęp dostawcy tożsamości**. 

    b. W hello **Grant sieci Web rejestracji jednokrotnej (WebSSO) dostępu tooSAML dostawców** kliknij **wybierz**.

17. Na powitania **ustanowić zaufanie** okna dialogowego, wykonaj następujące kroki hello:  
    
    ![Konfigurowanie rejestracji jednokrotnej][19] 

    a. Jako dostawca SAML wybierz hello SAML dostawcy utworzonym wcześniej (np.: *drewna*)
  
    b. Kliknij przycisk **następny krok**.

18. Na powitania **Sprawdź zaufania roli** okna dialogowego, kliknij przycisk **następnego kroku**.
    
    ![Konfigurowanie rejestracji jednokrotnej][32]

19. Na powitania **Dołącz zasady** okna dialogowego, kliknij przycisk **następnego kroku**.
    
    ![Konfigurowanie rejestracji jednokrotnej][33]

20. Na powitania **przeglądu** okna dialogowego, wykonaj następujące kroki hello:
    
    ![Konfigurowanie rejestracji jednokrotnej][34]
 
    a. Kliknij przycisk **utworzyć rolę**.

    b. Tworzenie ról tyle zgodnie z potrzebami i zamapowania ich toohello dostawcy tożsamości.

21. Teraz skonfigurować użytkownika hello inicjowania obsługi administracyjnej toofetch wszystkie role hello z usług AWS

    a. Podczas logowania konsoli usług AWS hello przy użyciu konta głównego

    b. W hello prawym górnym rogu kliknij swoją nazwę, a następnie kliknij przycisk hello **moje poświadczenia zabezpieczeń** opcji. Spowoduje to otwarcie ekranu jako komunikat ostrzegawczy. Kliknij przycisk hello **poświadczenia zabezpieczeń** toopass przycisk hello ekranu.
        
       ![Konfigurowanie rejestracji jednokrotnej][36]

       ![Konfigurowanie rejestracji jednokrotnej][37]

    c. W hello kluczy dostępu do sekcji kliknij hello **Utwórz nowy klucz dostępu** przycisku. Spowoduje to wygenerowanie hello identyfikator klucza dostępu i wartość tokenu.
    
       ![Konfigurowanie rejestracji jednokrotnej][38]

    d. Skopiuj obie te wartości i go również pobrać, tak aby nie zostaną utracone.

    e. W hello portalu Azure na stronie integracji aplikacji hello, Amazon Web Services (AWS), kliknij przycisk **inicjowania obsługi administracyjnej**.
        
       ![Konfigurowanie rejestracji jednokrotnej][35]

    f. Ustaw tryb inicjowania obsługi administracyjnej hello zbyt**automatyczne**
        
       ![Konfigurowanie rejestracji jednokrotnej][39]

    g. Teraz w hello **clientsecret** i **klucz tajny tokenu** Wklej hello odpowiednie wartości, które zostały skopiowane z konsoli usług AWS.
    
    h. Możesz kliknąć hello **Testuj połączenie** przycisku łączności hello tootest. Gdy zostanie pomyślnie przesłany można uruchomić hello inicjowania obsługi administracyjnej łącznika.
       
       ![Konfigurowanie rejestracji jednokrotnej][40]

    i. Teraz Włącz hello stan inicjowania obsługi administracyjnej za**na**. Spowoduje to uruchomienie pobierania hello ról z aplikacji hello.

       ![Konfigurowanie rejestracji jednokrotnej][41]

    > [!NOTE]
    > Azure działa Usługa AD inicjowania obsługi administracyjnej co po niektóre role hello toosync czasu z usług AWS. Powinny zostać wyświetlone wszystkie hello dostawcy tożsamości dołączony ról usług AWS z usługą Azure AD i można było ich użyć podczas przypisywania toousers aplikacji hello lub grup.

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-amazon-web-services-test-user"></a>Tworzenie użytkownika testowego usług Amazon Web Services

W kolejności tooenable usługi Azure AD użytkownicy toolog w tooAmazon usług sieci Web (AWS) są udostępniane do usług sieci Web firmy Amazon (AWS). W przypadku hello z usług sieci Web firmy Amazon (AWS) Inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour **Amazon Web Services (AWS)** witryny firmy jako administrator.

2. Kliknij przycisk hello **konsoli głównej** ikony. 
   
    ![Konfigurowanie rejestracji jednokrotnej][11]

3. Tożsamość i zarządzanie dostępem. 
   
    ![Konfigurowanie rejestracji jednokrotnej][28]

4. W hello pulpitu nawigacyjnego, kliknij przycisk **użytkowników**, a następnie kliknij przycisk **Utwórz nowych użytkowników**. 
   
    ![Konfigurowanie rejestracji jednokrotnej][29]

5. W oknie dialogowym Tworzenie użytkownika hello wykonaj następujące kroki hello: 
   
    ![Konfigurowanie rejestracji jednokrotnej][30]   
    
    a. W hello **wprowadź nazwy użytkowników** pól tekstowych, wpisz nazwę użytkownika Simona Brita (userprincipalname) w usłudze Azure AD.

    b. Kliknij przycisk **utworzyć.**
        
### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooAmazon dostęp do usług sieci Web (AWS).

![Przypisz użytkownika][200] 

**tooassign tooAmazon Simona Britta usług sieci Web (AWS) wykonaj następujące kroki hello:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **Amazon Web Services (AWS)**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Na **wybierz rolę** kartę, hello wybierz odpowiednią rolę dla użytkownika hello. Te role są wyświetlane z nazwą roli hello i nazwa dostawcy tożsamości. Dzięki temu można łatwo zidentyfikować hello role z usług AWS.

8. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu powitalne Amazon Web Services (AWS) kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Amazon Web Services (AWS) aplikacji. 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
