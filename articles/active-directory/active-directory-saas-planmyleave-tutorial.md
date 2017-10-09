---
title: 'Samouczek: Integracji Azure Active Directory z PlanMyLeave | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a>Samouczek: Integracji Azure Active Directory z PlanMyLeave

Z tego samouczka, dowiesz się, jak toointegrate PlanMyLeave w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD PlanMyLeave zapewnia hello następujące korzyści:

- Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPlanMyLeave
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPlanMyLeave (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD
- Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z PlanMyLeave należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- PlanMyLeave jednokrotnego włączone subskrypcji


> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.


tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie PlanMyLeave z galerii hello
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne


## <a name="adding-planmyleave-from-hello-gallery"></a>Dodawanie PlanMyLeave z galerii hello
tooconfigure hello integracji PlanMyLeave do usługi Azure AD, należy tooadd PlanMyLeave z hello galerii tooyour listę zarządzanych aplikacji SaaS.

**tooadd PlanMyLeave z galerii hello, wykonaj następujące kroki hello:**

1. W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Przejdź za**aplikacje dla przedsiębiorstw**. Następnie przejdź zbyt**wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **PlanMyLeave**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. W panelu wyników hello zaznacz **PlanMyLeave**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PlanMyLeave w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w PlanMyLeave jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w PlanMyLeave musi toobe ustanowione.

Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w PlanMyLeave.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z PlanMyLeave, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave odpowiednikiem Simona Britta w PlanMyLeave, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji PlanMyLeave.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z PlanMyLeave, wykonaj następujące kroki hello:**

1. W portalu zarządzania Azure hello na powitania **PlanMyLeave** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** strony okna dialogowego jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. Na powitania **PlanMyLeave domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    a. W hello **na adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company-name>.planmyleave.com/Login.aspx`
    
    b. W hello **identyfikatorem** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company-name>.planmyleave.com`

    > [!NOTE] 
    > Należy pamiętać, że nie są one hello wartości rzeczywistych. Masz tooupdate tych wartości za pomocą hello rzeczywiste Zaloguj się na adres URL i identyfikator. Skontaktuj się z [zespołem pomocy technicznej PlanMyLeave](mailto:support@planmyleave.com) tooget tych wartości.

4. Na powitania **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. Na powitania **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza hello i wybierz **Data wygaśnięcia**. Następnie kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. Na powitania **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. W oknie podręcznym hello **certyfikat przerzucania** okna, kliknij przycisk **OK**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. Na powitania **konfiguracji PlanMyLeave** kliknij **skonfigurować PlanMyLeave** tooopen **Konfigurowanie logowania jednokrotnego** okna.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. W oknie przeglądarki innej witryny sieci web Zaloguj się do dzierżawy PlanMyLeave jako administrator.

11. Przejdź za**konfiguracji systemu**. Następnie na powitania **zarządzania zabezpieczeniami** kliknij sekcję **ustawienia SAML firmy** .

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. Na powitania **ustawienia SAML** sekcji, kliknij ikonę edytora.

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. Na powitania **ustawienia SAML aktualizacji** sekcji, wykonaj następujące kroki hello:

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    a.  W hello **adres URL logowania** pole tekstowe, umieść wartość hello **SAML pojedynczy znak na adres URL usługi** z okna konfiguracji aplikacji usługi Azure AD.

    b.  Otwórz w Notatniku plik certyfikatu pobrane, tylko hello zawartości między hello---rozpocząć certyfikatu---i---koniec certyfikatu---go do Schowka, skopiuj i wklej go po toohello **certyfikatu** pola tekstowego.

    c. Ustawianie"**jest włączona**"za"**tak**".

    d. Kliknij pozycję **Zapisz**.



### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**. 



### <a name="creating-a-planmyleave-test-user"></a>Tworzenie użytkownika testowego PlanMyLeave

Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w PlanMyLeave. PlanMyLeave obsługę w czasie, który jest domyślnie włączone.

Nie ma elementu akcji można w tej sekcji. Nowy użytkownik zostanie utworzony podczas próby tooaccess PlanMyLeave, jeśli go jeszcze nie istnieje.

> [!NOTE]
> Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact [zespołem pomocy technicznej PlanMyLeave](mailto:support@planmyleave.com).



### <a name="assigning-hello-azure-ad-test-user"></a>Przypisanie użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooPlanMyLeave dostępu.

![Przypisz użytkownika][200] 

**tooassign tooPlanMyLeave Simona Britta wykonaj hello następujące kroki:**

1. W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **PlanMyLeave**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    


### <a name="testing-single-sign-on"></a>Testowanie rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka PlanMyLeave hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour PlanMyLeave aplikacji.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png