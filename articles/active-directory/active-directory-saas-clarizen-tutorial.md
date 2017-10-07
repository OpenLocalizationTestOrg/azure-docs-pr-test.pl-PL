---
title: 'Samouczek: Integracji Azure Active Directory z Clarizen | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Clarizen."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a>Samouczek: Integracji Azure Active Directory z Clarizen

Z tego samouczka, dowiesz się, jak Azure Active Directory (Azure AD) z Clarizen toointegrate. Umożliwia to integracji hello następujące korzyści:

- Można kontrolować, w usłudze Azure AD, kto ma dostęp do tooClarizen.
- Można włączyć użytkownika toobe użytkowników zostanie automatycznie zalogowany tooClarizen (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji, hello portalu Azure.

Scenariusz Hello w tym samouczku składa się z dwóch głównych zadań:

1. Dodaj Clarizen z galerii hello.
2. Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej.

Więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne
tooconfigure integracji z usługą Azure AD z Clarizen należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Clarizen subskrypcji, która jest włączone dla rejestracji jednokrotnej

kroki hello tootest w tym samouczku, wykonaj te zalecenia:

- Testowanie usługi Azure AD rejestracji jednokrotnej w środowisku testowym. Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz usługi Azure AD w środowisku testowym, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="add-clarizen-from-hello-gallery"></a>Dodaj Clarizen z galerii hello
Integracja hello tooconfigure Clarizen w usłudze Azure AD, Dodaj Clarizen hello galerii tooyour listy zarządzanych aplikacji SaaS.

1. W hello [portalu Azure](https://portal.azure.com), w lewym okienku hello, kliknij przycisk hello **usługi Azure Active Directory** ikony.

    ![Ikona usługi Azure Active Directory][1]

2. Kliknij przycisk **aplikacje dla przedsiębiorstw**. Następnie kliknij przycisk **wszystkie aplikacje**.

    ![Kliknięcie przycisku "aplikacje przedsiębiorstwa" i "Wszystkie aplikacje"][2]

3. Kliknij przycisk hello **Dodaj** u góry hello hello — okno dialogowe.

    ![przycisk "Dodaj" Hello][3]

4. W polu wyszukiwania hello wpisz **Clarizen**.

    ![Wpisz "Clarizen" w polu wyszukiwania hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. Wybierz w okienku wyników hello **Clarizen**, a następnie kliknij przycisk **Dodaj** tooadd hello aplikacji.

    ![Wybieranie Clarizen w okienku wyników hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W hello następujące sekcje zawierają informacje skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Clarizen na podstawie użytkownika testu hello Simona Britta.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Clarizen jest tooa użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Clarizen musi toobe ustanowione. Ustanowić tę relację łącza, przypisując wartość hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello **Username** w Clarizen.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Clarizen, pełną powitania po bloków konstrukcyjnych:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego Clarizen](#create-a-clarizen-test-user)**  toohave odpowiednikiem Simona Britta w Clarizen, że jego reprezentacja toohello połączonej usługi Azure AD.
4. **[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#test-single-sign-on)**  tooverify czy hello konfiguracji działania.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej
Włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Clarizen.

1. W portalu Azure na powitania hello **Clarizen** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Kliknięcie przycisku "Logowanie jednokrotne"][4]

2. W hello **logowanie jednokrotne** okno dialogowe dla **tryb**, wybierz pozycję **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.

    ![Wybieranie "na podstawie SAML logowania"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. W hello **Clarizen domeny i adres URL** sekcji, wykonaj następujące kroki hello:

    ![Pola Adres URL identyfikatora i odpowiedzi](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    a. W hello **identyfikator** polu wartość hello typu jako: **Clarizen**

    b. W hello **adres URL odpowiedzi** wpisz adres URL przy użyciu hello następującego wzorca: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**

    > [!NOTE]
    > Nie są hello wartości rzeczywistych. Masz toouse hello rzeczywisty identyfikator i adres URL odpowiedzi. W tym miejscu zalecamy Użyj hello unikatowej wartości ciągu, ponieważ hello identyfikator. tooget hello wartości rzeczywistych, skontaktuj się z pomocą hello [zespołem pomocy technicznej Clarizen](https://success.clarizen.com/hc/en-us/requests/new).

4. Na powitania **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.

    ![Klikając przycisk "Utwórz nowy certyfikat"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. W hello **Tworzenie nowego świadectwa** okno dialogowe pola, kliknij ikonę kalendarza hello i wybierz datę wygaśnięcia. Następnie kliknij przycisk **Save** (Zapisz).

    ![Wybranie i zapisanie Data wygaśnięcia](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. W hello **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowy certyfikat**, a następnie kliknij przycisk **zapisać**.

    ![Po zaznaczeniu pola wyboru hello na uaktywnienie hello nowego certyfikatu](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. W hello **certyfikat przerzucania** okno dialogowe, kliknij przycisk **OK**.

    ![Klikając przycisk OK, tooconfirm, które mają certyfikat hello toomake active](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. W hello **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.

    ![Klikając przycisk Pobierz hello toostart "Certyfikat (Base64)"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. W hello **konfiguracji Clarizen** , kliknij przycisk **skonfigurować Clarizen** tooopen hello **Konfigurowanie logowania jednokrotnego** okna.

    ![Klikając przycisk "Konfigurowanie Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Okno "Konfigurowanie logowania jednokrotnego", w tym adresy URL i pliki](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Clarizen tooyour jako administrator.

11. Kliknij nazwy użytkownika, a następnie kliknij przycisk **ustawienia**.

    ![Klikając pozycję "Ustawienia" w obszarze nazwy użytkownika](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "ustawienia")

12. Kliknij przycisk hello **ustawienia globalne** kartę. Następnie dalej zbyt**Federated Authentication**, kliknij przycisk **Edytuj**.

    ![Kartę "Ustawienia globalne"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "ustawienia globalne")

13. W hello **Federated Authentication** okna dialogowego wykonaj hello następujące kroki:

    ![Okno dialogowe "Uwierzytelnianie federacyjne"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")

    a. Wybierz **uwierzytelnianie federacyjne Włącz**.

    b. Kliknij przycisk **przekazać** tooupload pobranego certyfikatu.

    c. W hello **adres URL logowania** wprowadź wartość hello **SAML pojedynczy znak na adres URL usługi** z okna konfiguracji aplikacji hello Azure AD.

    d. W hello **Sign-out URL** wprowadź wartość hello **Sign-Out URL** z okna konfiguracji aplikacji hello Azure AD.

    e. Wybierz **Użyj POST**.

    f. Kliknij pozycję **Zapisz**.

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
W portalu Azure hello Tworzenie użytkownika testowego o nazwie Simona Britta.

![Nazwa i adres e-mail użytkownika testu hello Azure AD][100]

1. W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** ikony.

    ![Ikona usługi Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. Kliknij przycisk **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.

    ![Klikając pozycję "Użytkownicy i grupy" i "Wszyscy użytkownicy"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. U góry hello hello — okno dialogowe, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okno dialogowe.

    ![przycisk "Dodaj" Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:

    ![Okno dialogowe "Użytkownika" z nazwę, adres e-mail i hasło wypełnione](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole adresu e-mail hello typu hello Simona Britta konta.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello **hasło**.

    d. Kliknij przycisk **Utwórz**.

### <a name="create-a-clarizen-test-user"></a>Tworzenie użytkownika testowego Clarizen
tooenable toosign użytkowników usługi Azure AD w tooClarizen, należy udostępnić kont użytkowników. W przypadku hello Clarizen Inicjowanie obsługi to zadanie ręczne.

1. Zaloguj się tooyour Clarizen witryny firmy jako administrator.

2. Kliknij przycisk **osób**.

    ![Klikając przycisk "Osoby"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "osób")

3. Kliknij przycisk **zaprosić użytkowników**.

    ![Przycisk "Zaprosić użytkowników"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "zaprosić użytkowników")

4. W hello **zaprosić użytkowników** okna dialogowego wykonaj hello następujące kroki:

    ![Okno dialogowe "Zaproś inne osoby"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "zaprosić użytkowników")

    a. W hello **E-mail** pole adresu e-mail hello typu hello Simona Britta konta.

    b. Kliknij przycisk **zaprosić**.

    > [!NOTE]
    > właścicielem konta usługi Azure Active Directory Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD
Włącz toouse Simona Britta Azure rejestracji jednokrotnej, przyznając jej tooClarizen dostępu.

![Test przypisany użytkownik][200]

1. W portalu Azure hello, otwórz widok aplikacji hello, przejdź do widoku katalogu toohello, kliknij przycisk **aplikacje dla przedsiębiorstw**, a następnie kliknij przycisk **wszystkie aplikacje**.

    ![Kliknięcie przycisku "aplikacje przedsiębiorstwa" i "Wszystkie aplikacje"][201]

2. Z listy aplikacji hello wybierz **Clarizen**.

    ![Wybierając Clarizen hello listy](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. W okienku po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Klikając pozycję "Użytkownicy i grupy"][202]

4. Kliknij przycisk hello **Dodaj** przycisku. Następnie w hello **Dodaj przydziału** okno dialogowe, wybierz opcję **użytkowników i grup**.

    ![Hello przycisk "Dodaj" i "Dodaj przydziału" hello, okno dialogowe][203]

5. W hello **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. W hello **użytkowników i grup** okna dialogowego kliknij hello **wybierz** przycisku.

7. W hello **Dodaj przydziału** okna dialogowego kliknij hello **przypisać** przycisku.

### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej
Test konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu kafelka Clarizen hello w panelu dostępu hello powinny być automatycznie zalogowano tooyour Clarizen aplikacji.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
