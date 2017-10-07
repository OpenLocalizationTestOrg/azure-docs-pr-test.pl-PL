---
title: "Samouczek: Integrowanie usługi Azure Active Directory z vxMaintain | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i vxMaintain."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a>Samouczek: Integrowanie usługi Azure Active Directory z vxMaintain

Z tego samouczka, dowiesz się, jak vxMaintain toointegrate w usłudze Azure Active Directory (Azure AD).

Integracja ta zapewnia kilka istotnych korzyści. Możesz:

- Formant w usłudze Azure AD, kto ma dostęp do toovxMaintain.
- Włącz użytkowników tooautomatically logowania toovxMaintain z logowaniem jednokrotnym (SSO) za pomocą ich kont usługi Azure AD.
- Zarządzanie kont w jednej centralnej lokalizacji: hello portalu Azure.

toolearn więcej informacji na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji z usługą Azure AD z vxMaintain należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- VxMaintain logowanie Jednokrotne włączone subskrypcji

> [!NOTE]
> Podczas testowania czynności hello w tym samouczku, firma Microsoft zaleca, nie używaj do środowiska produkcyjnego.

kroki hello tootest w tym samouczku, wykonaj te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. 

Scenariusz Hello, w tym samouczku przedstawiono składa się z dwóch głównych elementów:

* Dodawanie vxMaintain z galerii hello
* Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="add-vxmaintain-from-hello-gallery"></a>Dodaj vxMaintain z galerii hello
integracji hello tooconfigure vxMaintain z usługą Azure AD, należy vxMaintain tooadd z hello galerii tooyour listę zarządzanych aplikacji SaaS.

vxMaintain tooadd z galerii hello hello następujące:

1. W hello [portalu Azure](https://portal.azure.com), w lewym okienku hello, wybierz hello **usługi Azure Active Directory** przycisku. 

    ![przycisk usługi Azure Active Directory Hello][1]

2. Wybierz **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.

    ![okienko "Aplikacje przedsiębiorstwa" Hello][2]
    
3. tooadd aplikacji, w hello **wszystkie aplikacje** okno dialogowe, wybierz opcję **nowej aplikacji**.

    ![Witaj "Nowej aplikacji" przycisku][3]

4. W polu wyszukiwania hello wpisz **vxMaintain**.

    ![listy rozwijanej "Pojedynczy znak na tryb" Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. Na liście wyników hello, wybierz **vxMaintain**, a następnie wybierz **Dodaj**.

    ![Witaj vxMaintain łącza](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej
W tej sekcji można skonfigurować i przetestować logowania jednokrotnego programu Azure AD przy użyciu vxMaintain, na podstawie użytkownika testowego, nazywany "Britta Simona".

Dla toowork logowania jednokrotnego usługi Azure AD musi użytkownika tooknow hello vxMaintain odpowiednikiem toohello usługi Azure AD. Oznacza to należy ustanowić relację łącza między hello użytkownika usługi Azure AD i odpowiedniego użytkownika vxMaintain hello.

Relacja linku hello tooestablish, przypisz hello vxMaintain **nazwy użytkownika** wartość jako hello Azure AD **Username** wartość.

tooconfigure i testowania Azure AD logowania jednokrotnego przy użyciu vxMaintain, pełną powitania po bloków konstrukcyjnych.

### <a name="configure-azure-ad-sso"></a>Konfigurowanie usługi Azure AD logowania jednokrotnego.

W tej sekcji można zarówno włączenia funkcji logowania jednokrotnego usługi Azure AD w portalu Azure hello i konfigurowanie logowania jednokrotnego w aplikacji vxMaintain hello następujący:

1. W portalu Azure na powitania hello **vxMaintain** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.

    ![Witaj "Logowanie jednokrotne" polecenia][4]

2. tooenable logowanie Jednokrotne, w hello **tryb rejestracji jednokrotnej** listy rozwijanej wybierz **na języku SAML logowania jednokrotnego**.
 
    ![polecenie "na podstawie SAML logowania jednokrotnego" Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. W obszarze **vxMaintain domeny i adres URL**, hello następujące:

    ![Witaj vxMaintain sekcji domeny i adresy URL](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    a. W hello **identyfikator** wpisz adres URL, który ma hello następującej składni:`https://<company name>.verisae.com`

    b. W hello **adres URL odpowiedzi** wpisz adres URL, który ma hello następującej składni:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`

    > [!NOTE] 
    > Witaj poprzedniej wartości nie są prawdziwe. Można aktualizować hello rzeczywisty identyfikator i adres URL odpowiedzi. wartości hello tooobtain, skontaktuj się z pomocą hello [zespołem pomocy technicznej vxMaintain](http://www.verisae.com/contact-us).
 
4. W obszarze **SAML certyfikat podpisywania**, wybierz pozycję **XML metadanych**, a następnie zapisz hello metadanych pliku tooyour komputera.

    ![Witaj sekcji "Certyfikat podpisywania SAML"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. Wybierz pozycję **Zapisz**.

    ![przycisk Zapisz Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. tooconfigure **vxMaintain** logowania jednokrotnego, Wyślij hello pobrane **XML metadanych** pliku toohello [zespołem pomocy technicznej vxMaintain](http://www.verisae.com/contact-us).

> [!TIP]
> Po skonfigurowaniu aplikacji hello może odczytywać zwięzły wersji hello poprzedzających instrukcji w hello [portalu Azure](https://portal.azure.com). Po dodaniu aplikacji hello z hello **usługi Active Directory** > **aplikacje dla przedsiębiorstw** sekcji, wybierz hello **rejestracji jednokrotnej** kartę, a następnie hello dostępu osadzone dokumentacji z hello **konfiguracji** sekcji. 
>
>toolearn więcej informacji na temat hello osadzonych dokumentacji funkcji, zobacz [Zarządzanie logowanie jednokrotne dla aplikacji przedsiębiorstwa](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
W tej sekcji możesz tworzyć użytkownika testowego Simona Britta w hello portalu Azure, wykonując następujące hello:

![użytkownika testowego Hello Azure AD][100]

1. W hello **portalu Azure**, w lewym okienku hello, wybierz hello **usługi Azure Active Directory** przycisku.

    ![przycisk "Azure Active Directory" Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. toodisplay listę użytkowników, przejdź zbyt**użytkowników i grup** > **wszyscy użytkownicy**.
    
    ![Witaj link "Wszyscy użytkownicy"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)  
    Witaj **wszyscy użytkownicy** zostanie otwarte okno dialogowe. 

3. Witaj tooopen **użytkownika** okno dialogowe, wybierz opcję **Dodaj**.
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. W hello **użytkownika** okna dialogowego pozycję hello następujące:
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    a. W hello **nazwa** wpisz **BrittaSimon**.

    b. W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika testowego Simona Britta.

    c. Wybierz hello **Pokaż hasło** pole wyboru, a następnie wartość hello Uwaga, który został wygenerowany w hello **hasło** pole.

    d. Wybierz pozycję **Utwórz**.
 
### <a name="create-a-vxmaintain-test-user"></a>Tworzenie użytkownika testowego vxMaintain

W tej sekcji utworzysz użytkownika testowego Simona Britta w vxMaintain. Użytkownicy tooadd hello vxMaintain platformy, pracować z [zespołem pomocy technicznej vxMaintain](http://www.verisae.com/contact-us). Przed użyciem logowania jednokrotnego, Utwórz i Aktywuj hello użytkowników.

### <a name="assign-hello-azure-ad-test-user"></a>Przypisz użytkownika testowego hello Azure AD

W tej sekcji możesz włączyć użytkownika testowego toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu toovxMaintain. toodo tak, hello następujące:

![Użytkownik testowy hello liście Nazwa wyświetlana][200] 

1. W portalu Azure hello **aplikacji** wyświetlić, przejdź do zbyt**katalogu** Widok > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.

    ![Witaj link "Wszystkie aplikacje"][201] 

2. W hello **aplikacji** listy, wybierz **vxMaintain**.

    ![Witaj vxMaintain łącza](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. Wybierz w okienku po lewej stronie powitania **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. Wybierz **Dodaj** , a następnie w hello **Dodaj przydziału** okienku wybierz **użytkowników i grup**.

    ![łącze "Użytkownicy i grupy" Hello][203]

5. W hello **użytkowników i grup** okno dialogowe, w hello **użytkowników** listy, wybierz **Simona Britta**, a następnie wybierz hello **wybierz** przycisku.

7. W hello **Dodaj przydziału** okno dialogowe, wybierz opcję **przypisać**.
    
### <a name="test-your-azure-ad-single-sign-on"></a>Test z usługi Azure AD rejestracji jednokrotnej

W tej sekcji możesz przetestować konfigurację programu Azure AD z logowania jednokrotnego przy użyciu hello panelu dostępu.

Wybór hello **vxMaintain** kafelka w hello panelu dostępu należy automatycznej rejestracji w aplikacji vxMaintain tooyour.

Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

## <a name="next-steps"></a>Następne kroki

* [Lista samouczków dotyczących integracji aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

