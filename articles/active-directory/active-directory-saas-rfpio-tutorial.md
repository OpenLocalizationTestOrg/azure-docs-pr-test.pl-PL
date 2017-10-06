---
title: 'Samouczek: Integracji Azure Active Directory z RFPIO | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a>Samouczek: Integracji Azure Active Directory z RFPIO

Z tego samouczka, dowiesz się, jak toointegrate RFPIO w usłudze Azure Active Directory (Azure AD).

Integracja z usługą Azure AD RFPIO zapewnia hello następujące korzyści:

- Możesz kontrolować, kto w usłudze Azure AD, kto ma dostęp do tooRFPIO.
- Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooRFPIO (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji — Witaj portalu Azure.

Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z RFPIO należy hello następujące elementy:

- Subskrypcja usługi Azure AD.
- RFPIO pojedynczy znak z włączoną subskrypcji.

> [!NOTE]
> Nie zaleca się użyć procedura hello tootest środowiska produkcyjnego w tym samouczku.

kroki hello tootest w tym samouczku, wykonaj te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz Hello, opisaną w tym samouczku składa się z dwóch głównych elementów:

1. Dodawanie RFPIO z galerii hello.
2. Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne.

## <a name="add-rfpio-from-hello-gallery"></a>Dodaj RFPIO z galerii hello
tooconfigure hello integracji RFPIO do usługi Azure AD, należy tooadd RFPIO z hello galerii tooyour listę zarządzanych aplikacji SaaS.

### <a name="tooadd-rfpio-from-hello-gallery"></a>tooadd RFPIO z galerii hello

1. W hello  **[portalu Azure](https://portal.azure.com)**na temat hello w lewym okienku nawigacji, wybierz hello **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

2. Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.

    ![Aplikacje][2]
    
3. tooadd nowej aplikacji, wybierz opcję hello **nowej aplikacji** przycisk u góry hello okna dialogowego.

    ![Aplikacje][3]

4. W polu wyszukiwania hello wpisz **RFPIO**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. W panelu wyników hello, wybierz **RFPIO**, a następnie wybierz hello **Dodaj** przycisk aplikacji hello tooadd.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z RFPIO w oparciu o nazwie "Britta Simona" użytkownika testowego.

Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jakie relacje hello jest odpowiednikiem użytkownika w RFPIO i użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w RFPIO musi toobe ustanowione.

W RFPIO, należy przypisać wartość hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello **Username** tooestablish hello łącze relacji.

tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z RFPIO, należy po bloków konstrukcyjnych hello toocomplete:

1. **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**— tooenable Twojego toouse użytkowników tej funkcji.
2. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**— tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.
3. **[Tworzenie użytkownika testowego RFPIO](#creating-a-rfpio-test-user)**  — toohave odpowiednikiem Simona Britta w RFPIO, który jest połączony toohello usługi Azure AD reprezentację użytkownika.
4. **[Przypisz użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**tooenable — Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.
5. **[Test rejestracji jednokrotnej](#testing-single-sign-on)**  — tooverify, jeśli konfiguracja hello działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji RFPIO.

**tooconfigure usługi Azure AD rejestracji jednokrotnej z RFPIO, wykonaj następujące kroki hello:**

1. W portalu Azure na powitania hello **RFPIO** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. Na powitania **RFPIO domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    a. W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://www.rfpio.com`

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    b. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.

    c. W hello **stan przekazywania** pole tekstowe Wprowadź wartość ciągu. Skontaktuj się z [RFPIO obsługuje zespołu](https://www.rfpio.com/contact/) tooget tej wartości. 

4. Sprawdź **Pokaż zaawansowane ustawienia adresu URL**. Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:   

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    W hello **Zaloguj się na adres URL** pole tekstowe, wprowadź adres URL hello:`https://www.app.rfpio.com`

5. Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. Kliknij przycisk **zapisać** przycisku.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. W oknie przeglądarki innej witryny sieci web, logowania toohello **RFPIO** witryny sieci Web jako administrator.

8. Polecenie hello dolnej lewym rogu z listy rozwijanej.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. Polecenie hello **ustawienia organizacji**. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. Polecenie hello **funkcje & integracji**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. W hello **konfiguracji logowania jednokrotnego SAML** kliknij **Edytuj**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. W tej sekcji należy wykonać następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    a. Skopiuj zawartość hello hello **pobierane metadane XML** i wklej go do hello **konfiguracji tożsamości** pola.

    > [!NOTE]
    >pobrane hello toocopy zawartości **XML metadanych** użyj **Notatnik ++** lub właściwe **edytora XML**. 

    b. Kliknij przycisk **zweryfikować**.

    c. Po kliknięcie przycisku **weryfikacji**, przerzucania **SAML(Enabled)** tooon.

    d. Kliknij przycisk **przesłać**.

> [!TIP]
> Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!  Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello. Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.

![Tworzenie użytkowników usługi Azure AD][100]

**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**

1. W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** pole tekstowe, typ **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.

    d. Kliknij przycisk **Utwórz**.
 
### <a name="create-a-rfpio-test-user"></a>Tworzenie użytkownika testowego RFPIO

toolog użytkowników tooenable usługi Azure AD w tooRFPIO, muszą mieć przydzielone do RFPIO.  
W przypadku hello RFPIO Inicjowanie obsługi to zadanie ręczne.

**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**

1. Zaloguj się za tooyour RFPIO witryny firmy jako administrator.

2. Polecenie hello dolnej lewym rogu z listy rozwijanej.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. Polecenie hello **ustawienia organizacji**. 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. Kliknij przycisk **członków zespołu**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. Polecenie **Dodaj członków**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. W hello **Dodawanie nowych elementów członkowskich** sekcji. Wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app8.png)

    a. Wprowadź **adres E-mail** w hello **Podaj jeden adres e-mail w jednym wierszu** pola.

    b. Wybierz Plese **roli** zgodnie z wymaganiami.

    c. Kliknij przycisk **Dodaj członków**.
        
    > [!NOTE]
    > Właściciel konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail i następuje tooconfirm łącze swojego konta, zanim staje się aktywny.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooRFPIO.

![Przypisz użytkownika][200] 

**tooassign tooRFPIO Simona Britta wykonaj hello następujące kroki:**

1. W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. Z listy aplikacji hello wybierz **RFPIO**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

4. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

5. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.

6. Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.

7. Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.

Po kliknięciu hello RFPIO kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour RFPIO aplikacji.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

