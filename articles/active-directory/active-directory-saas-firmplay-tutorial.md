---
title: 'Samouczek: Integracji Azure Active Directory z FirmPlay - propagowanie pracownika dla Rekrutacja | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i FirmPlay - propagowanie pracownika dla Rekrutacja."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a>Samouczek: Integracji Azure Active Directory z FirmPlay - propagowanie pracownika dla Rekrutacja

Z tego samouczka, dowiesz się, jak toointegrate FirmPlay - propagowanie pracownika dla Rekrutacja w usłudze Azure Active Directory (Azure AD).

Integrowanie FirmPlay - propagowanie pracownika dla Rekrutacja z usługą Azure AD zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD mającego dostęp tooFirmPlay - propagowanie pracownika dla Rekrutacja
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFirmPlay - propagowanie pracownika dla Rekrutacja (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z FirmPlay - propagowanie pracownika dla Rekrutacja, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- FirmPlay - propagowanie pracownika dla rekrutacji jednokrotnego włączone subskrypcji


> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.


tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie FirmPlay - propagowanie pracownika dla Rekrutacja z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a>Dodawanie FirmPlay - propagowanie pracownika dla Rekrutacja z galerii hello
Integracja hello tooconfigure FirmPlay - propagowanie pracownika dla Rekrutacja do usługi Azure AD, należy tooadd FirmPlay - propagowanie pracownika dla Rekrutacja z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd FirmPlay - propagowanie pracownika dla Rekrutacja z galerii hello wykonaj hello następujące kroki:**

1. W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **FirmPlay - propagowanie pracownika dla Rekrutacja**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. W panelu wyników hello, wybierz **FirmPlay - propagowanie pracownika dla Rekrutacja**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z FirmPlay - propagowanie pracownika dla Rekrutacja w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w FirmPlay - propagowanie pracownika dla Rekrutacja jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w FirmPlay - propagowanie pracownika dla Rekrutacja musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w FirmPlay - propagowanie pracownika dla Rekrutacja.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z FirmPlay - propagowanie pracownika dla Rekrutacja, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie FirmPlay - propagowanie pracownika dla użytkownika testowego Rekrutacja](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave odpowiednikiem Simona Britta w FirmPlay: propagowanie pracownika dla rekrutacji, który jest połączony jej reprezentacji toohello usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w sieci FirmPlay - propagowanie pracownika Rekrutacja aplikacji.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z FirmPlay - propagowanie pracownika dla Rekrutacja, wykonaj następujące kroki hello:**

1. W portalu zarządzania Azure hello na powitania **FirmPlay - propagowanie pracownika dla Rekrutacja** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. Na powitania **FirmPlay - propagowanie pracownika rekrutacji domeny i adresów URL** części hello **na adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<your-subdomain>.firmplay.com/`

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > Należy pamiętać, że nie jest hello rzeczywistą wartość. Masz tooupdate tej wartości z rzeczywistego hello Zaloguj się na adres URL. Skontaktuj się z [FirmPlay - propagowanie pracowników zespołu pomocy technicznej Rekrutacja](mailto:engineering@firmplay.com) tooget tej wartości. 

4. Na powitania **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. Na powitania **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza hello i wybierz **Data wygaśnięcia**. Następnie kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. Na powitania **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. W oknie podręcznym hello **certyfikat przerzucania** okna, kliknij przycisk **OK**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. Na powitania **FirmPlay - propagowanie pracownika rekrutacji konfiguracji** kliknij **skonfigurować FirmPlay - propagowanie pracownika dla Rekrutacja** tooopen **Konfigurowanie logowania jednokrotnego**okna dialogowego.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. tooget logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [FirmPlay - propagowanie pracowników zespołu pomocy technicznej Rekrutacja](mailto:engineering@firmplay.com) i podaj następujący hello: 

    • hello pobrane **plik certyfikatu**

    • hello **SAML pojedynczy znak na adres URL usługi**

    • hello **identyfikator jednostki SAML**

    • hello **Sign-Out adresu URL**
  

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**. 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a>Tworzenie FirmPlay - propagowanie pracownika dla użytkownika testowego Rekrutacja

W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w FirmPlay - propagowanie pracownika dla Rekrutacja. We współpracy z [FirmPlay - propagowanie pracowników zespołu pomocy technicznej Rekrutacja](mailto:engineering@firmplay.com) tooadd hello użytkowników w hello FirmPlay - propagowanie pracownika Rekrutacja platformy.


### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooFirmPlay dostępu - propagowanie pracownika dla Rekrutacja.

![Przypisz użytkownika][200] 

**tooassign tooFirmPlay Simona Britta - propagowanie pracownika dla Rekrutacja, wykonaj hello następujące kroki:**

1. W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **FirmPlay - propagowanie pracownika dla Rekrutacja**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    


### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello FirmPlay - propagowanie pracownika Rekrutacja kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour FirmPlay - propagowanie pracownika Rekrutacja aplikacji.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png