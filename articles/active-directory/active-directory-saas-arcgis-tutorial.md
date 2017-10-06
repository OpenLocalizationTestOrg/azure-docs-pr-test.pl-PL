---
title: "Samouczek: Integracja usługi Azure Active Directory z usługą ArcGIS Online | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ArcGIS Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a>Samouczek: Integracja usługi Azure Active Directory z usługą ArcGIS Online

Z tego samouczka, dowiesz się, jak toointegrate ArcGIS Online z usługą Azure Active Directory (Azure AD).

Integrowanie ArcGIS Online z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp tooArcGIS Online
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooArcGIS Online (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD ArcGIS online należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- ArcGIS Online jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie ArcGIS Online z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="adding-arcgis-online-from-hello-gallery"></a>Dodawanie ArcGIS Online z galerii hello
tooconfigure hello integracji ArcGIS Online z usługą Azure AD, należy tooadd ArcGIS Online z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd ArcGIS Online z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **nowej aplikacji** przycisk na powitania górnej części okna dialogowego hello tooadd nowej aplikacji.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **ArcGIS Online**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. W panelu wyników hello, wybierz **ArcGIS Online**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji można skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ArcGIS Online na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello ArcGIS online jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w trybie Online ArcGIS musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** ArcGIS online.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ArcGIS Online, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego ArcGIS Online](#creating-an-arcgis-online-test-user)**  -toohave odpowiednikiem Simona Britta w ArcGIS Online, które zostało połączone toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w trybie Online ArcGIS aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z ArcGIS Online wykonaj hello następujące kroki:**

1. W portalu Azure na powitania hello **ArcGIS Online** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. Na powitania **ArcGIS Online domeny i adres URL** sekcji, wykonaj powitania po kroku:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    W hello **adres URL logowania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://<company>.maps.arcgis.com`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe hello. Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej Online klienta ArcGIS](http://support.esri.com/) tooget tej wartości. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy ArcGIS jako administrator.

7. Kliknij przycisk **Edytuj ustawienia**.

    ![Edytuj ustawienia](./media/active-directory-saas-arcgis-tutorial/ic784742.png "edytować ustawienia")

8. Kliknij przycisk **zabezpieczeń**.

    ![Zabezpieczenia](./media/active-directory-saas-arcgis-tutorial/ic784743.png "zabezpieczeń")

9. W obszarze **logowania do organizacji**, kliknij przycisk **USTAWIĆ dostawcy tożsamości**.

    ![Logowania do organizacji](./media/active-directory-saas-arcgis-tutorial/ic784744.png "logowania do organizacji")

10. Na powitania **ustawić dostawcy tożsamości** konfiguracji wykonaj hello następujące kroki:
   
    ![Ustawienie dostawcy tożsamości](./media/active-directory-saas-arcgis-tutorial/ic784745.png "ustawienie dostawcy tożsamości")
   
    a. W hello **nazwa** tekstowym, wpisz nazwę organizacji.

    b. Dla **metadanych dla hello organizacji dostawcy tożsamości dostarczane za pomocą**, wybierz pozycję **plik**.

    c. tooupload pliku metadanych pobranych, kliknij przycisk **wybierz plik**.

    d. Kliknij przycisk **dostawcy tożsamości zestawu**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z Simona Britta.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="creating-an-arcgis-online-test-user"></a>Tworzenie użytkownika testowego ArcGIS Online

W kolejności tooenable usługi Azure AD użytkownicy toolog do ArcGIS Online musi być przygotowana do ArcGIS Online.  
W przypadku hello ArcGIS online Inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour **ArcGIS** dzierżawy.

2. Kliknij przycisk **członków zaproszenia**.
   
    ![Zaprosić](./media/active-directory-saas-arcgis-tutorial/ic784747.png "zaprosić")

3. Wybierz **automatycznie dodawać członków bez wysyłania wiadomości e-mail**, a następnie kliknij przycisk **dalej**.
   
    ![Automatyczne dodawanie członków](./media/active-directory-saas-arcgis-tutorial/ic784748.png "automatycznie dodawać członków")

4. Na powitania **członków** okna dialogowego wykonaj hello następujące kroki:
   
     ![Dodaj i przejrzyj](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Dodaj i przejrzyj")
    
     a. Wprowadź hello **E-mail**, **imię**, i **nazwisko** ma tooprovision poprawnego konta usługi AAD.
  
     b. Kliknij przycisk **Dodaj i przejrzyj**.
5. Przejrzyj hello dane zostały wprowadzone, a następnie kliknij przycisk **Dodaj członków**.
   
    ![Dodaj element członkowski](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Dodaj element członkowski")
        
    > [!NOTE]
    > właścicielem konta usługi Azure Active Directory Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny.

### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooArcGIS w trybie Online.

![Przypisz użytkownika][200] 

**tooassign tooArcGIS Simona Britta w trybie Online, wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **ArcGIS Online**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka ArcGIS Online hello w hello Panel dostępu, należy pobrać aplikacji ArcGIS Online tooyour zalogowane automatycznie.
Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

