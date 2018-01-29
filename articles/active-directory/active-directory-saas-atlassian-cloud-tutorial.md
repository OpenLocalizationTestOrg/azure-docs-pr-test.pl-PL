---
title: "Samouczek: Integracji Azure Active Directory z chmurą Atlassian | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i w chmurze Atlassian."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/05/2017
ms.author: jeedes
ms.openlocfilehash: db9e9c7ae8380612bac9d0aeaaaf6df78cba523f
ms.sourcegitcommit: d247d29b70bdb3044bff6a78443f275c4a943b11
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/13/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a>Samouczek: Integracji Azure Active Directory z chmurą Atlassian

Z tego samouczka dowiesz się integrowanie Atlassian chmury w usłudze Azure Active Directory (Azure AD).

Integrowanie Atlassian chmurze z usługą Azure AD zapewnia następujące korzyści:

- Można kontrolować w usłudze Azure AD, który ma dostęp do chmury Atlassian.
- Można umożliwić użytkownikom zalogować się przy automatycznie (logowanie jednokrotne) do chmury Atlassian z konta usługi Azure AD.
- Możesz zarządzać kont w jednej centralnej lokalizacji, portalu Azure.

Aby uzyskać więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z chmurą Atlassian, potrzebne są następujące elementy:

- Subskrypcja usługi Azure AD.
- Aby włączyć Security (Assertion Markup Language SAML) rejestracji jednokrotnej dla produktów Atlassian chmury, musisz skonfigurować Identity Manager. Dowiedz się więcej o [Identity Manager]( https://www.atlassian.com/enterprise/cloud/identity-manager).

> [!NOTE]
> Podczas testowania czynności w tym samouczku, firma Microsoft zaleca, aby nie używać do środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, wykonaj te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisane w samouczku składa się z dwóch głównych elementów:

* Dodawanie Atlassian chmury z galerii
* Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne

## <a name="add-atlassian-cloud-from-the-gallery"></a>Dodaj Atlassian chmury z galerii
Aby skonfigurować integrację Atlassian chmurze z usługą Azure AD, Dodaj Atlassian chmury z galerii do listy zarządzane aplikacje SaaS w następujący sposób:

1. W [portalu Azure](https://portal.azure.com), w okienku po lewej stronie wybierz **usługi Azure Active Directory** przycisku. 

    ![Przycisk usługi Azure Active Directory][1]

2. Wybierz **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.

    ![W okienku aplikacji przedsiębiorstwa][2]
    
3. Aby dodać aplikację, wybierz **nowej aplikacji**.

    !["Nowa aplikacja" przycisku][3]

4. W polu wyszukiwania wpisz **chmury Atlassian**, na liście wyników wybierz **chmury Atlassian**, a następnie wybierz **Dodaj**.

    ![Chmura Atlassian na liście wyników](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z chmurą Atlassian, w oparciu o nazwie użytkownika testowego *Simona Britta*.

Dla rejestracji jednokrotnej do pracy usługi Azure AD musi zidentyfikować użytkowników chmury Atlassian i jego odpowiednik w usłudze Azure AD. Innymi słowy musisz ustanowić relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w chmurze Atlassian.

Do ustanawiania relacji łącza, przypisz jako chmury Atlassian *Username* taką samą wartość, który jest przypisany do usługi Azure AD *nazwy użytkownika*.

Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z chmurą Atlassian, należy wykonać bloków konstrukcyjnych w poniższych sekcjach.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD rejestracji jednokrotnej

W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji w chmurze Atlassian.

Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z chmurą Atlassian, wykonaj następujące czynności:

1. W portalu Azure w **chmury Atlassian** okienko integracji aplikacji, wybierz opcję **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. W **logowanie jednokrotne** okna w **tryb rejestracji jednokrotnej** wybierz opcję **na języku SAML logowania jednokrotnego**.
 
    ![Okno rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. Aby skonfigurować aplikację w trybie inicjowanych przez dostawców tożsamości, w obszarze **adresy URL i domenę chmury Atlassian**, wykonaj następujące czynności:

    ![Adresy URL i domenę chmury Atlassian pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)
    
    a. W **identyfikator** wpisz  **`https://auth.atlassian.com/saml/<unique ID>`** .
    
    b. W **adres URL odpowiedzi** wpisz  **`https://auth.atlassian.com/login/callback?connection=saml-<unique ID>`** .

    c. W **stan przekazywania** wpisz adres URL przy użyciu następującej składni:  **`https://<instancename>.atlassian.net`** .

4. Aby skonfigurować aplikację w trybie zainicjował SP, wybierz **Pokaż zaawansowane ustawienia adresu URL** , a następnie w **Zaloguj się na adres URL** wpisz adres URL przy użyciu następującej składni:  **`https://<instancename>.atlassian.net`**  .

    ![Adresy URL i domenę chmury Atlassian pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    > [!NOTE] 
    > Poprzednie wartości nie są prawdziwe. Zaktualizuj je z rzeczywisty identyfikator, adres URL odpowiedzi i logowania jednokrotnego wartości adresu URL. Na ekranie Konfiguracja SAML chmury Atlassian można uzyskać rzeczywiste wartości. Prezentujemy zasady wartości później w samouczku.

5. W obszarze **certyfikat podpisywania SAML**, wybierz pozycję **Certificate(Base64)**, a następnie zapisz plik certyfikatu na komputerze.

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. Aplikacja chmury Atlassian oczekuje można znaleźć potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do konfiguracji atrybuty tokenu SAML. 

    Domyślnie **identyfikator użytkownika** wartość jest mapowany na user.userprincipalname. Zmień tę wartość do mapowania na user.mail. Możesz również inne odpowiednie wartości zgodnie z ustawieniami w Twojej organizacji, ale w większości przypadków, wiadomości e-mail powinny działać.

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_attribute.png) 

7. Wybierz pozycję **Zapisz**.

    ![Konfigurowanie rejestracji jednokrotnej przycisk zapisywania](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

8. Aby otworzyć **Konfigurowanie logowania jednokrotnego** okna w **konfiguracji chmury Atlassian** wybierz opcję **Konfigurowanie chmury Atlassian**. 

9. W **krótkimi opisami** sekcji, skopiuj **identyfikator jednostki SAML** i **SAML pojedynczy znak na adres URL usługi**. 

    ![Konfiguracja chmury Atlassian](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

10. Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, zaloguj się do portalu Atlassian przy użyciu poświadczeń administratora.

11. Przejdź do **administrowania lokacją Atlassian** > **organizacji i zabezpieczenia**. Jeśli jeszcze tego nie zrobiono, Utwórz i nazwę organizacji, a następnie w okienku po lewej stronie wybierz **domen**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

12. Wybierz sposób, że chcesz zweryfikować domenę: **DNS** lub **HTTPS**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_17.png)

13. W celu weryfikacji DNS w **domen** wybierz **DNS** karcie, a następnie wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_18.png)

    a. Aby skopiować wartość z tekstu rekordu (TXT), zaznacz **kopiowania**.

    b. Aby dodać rekord, przejdź do strony ustawień w systemie DNS.

    c. Wybierz opcję dodawania nowego rekordu, a następnie wklej skopiowany w wartość **domen** okna **wartość** pola. Rekordu DNS może także odwołuje się do niego jako **odpowiedzi** lub **opis**.

    d. Rekordu DNS może także zawierać następujące pola:
    
    * W **typu rekordu** wprowadź **TXT**.
    * W **Alias-nazwy/hosta** pozostaw wartość domyślną (@ lub puste).
    * W **czas wygaśnięcia (TTL)** wprowadź **86400**.
    
    e.  Zapisz rekord.

14. Wróć do **domen** okna w organizacji administracji, a następnie wybierz **weryfikowanie domeny**. W **domeny** wpisz nazwę domeny, a następnie wybierz **weryfikowanie domeny**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_19.png)  

    > [!NOTE]
    > Ponieważ może potrwać do 72 godzin rekordu TXT zmiany zaczęły obowiązywać, nie wiadomo, od razu czy weryfikację domeny zakończyła się powodzeniem. Aby wyświetlić stan weryfikacji użytkownika, sprawdź **domen** okna zaraz po zakończeniu tej procedury. Zaktualizowany stan będzie wyświetlany jako *zweryfikowano*, jak pokazano na poniższej ilustracji:
    > 
    > ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_20.png)
    > 
    > 

15. W celu weryfikacji HTTPS w **domen** wybierz **HTTPS** karcie, a następnie wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_21.png)

    a. Aby pobrać plik HTML, wybierz **pobierania pliku**.

    b. Przekaż plik HTML do katalogu głównym domeny.

16. Wróć do **domen** strony w witrynie Administracja organizacji, a następnie wybierz **weryfikowanie domeny**. W **weryfikowanie domeny** okna w **domeny** wpisz Twojej **nazwy domeny**, a następnie wybierz **weryfikowanie domeny**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_22.png)

17. Jeśli proces weryfikacji można zlokalizować pliku, który został przekazany w katalogu głównym, stan domeny zostało zaktualizowane do *zweryfikowano*, jak pokazano poniżej:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_23.png)

    > [!NOTE]
    > Aby uzyskać więcej informacji, zobacz [weryfikację domeny Atlassian](https://confluence.atlassian.com/cloud/domain-verification-873871234.html).

18. W okienku po lewej stronie wybierz **SAML logowania jednokrotnego**. Jeśli jeszcze tego nie zrobiono, subskrypcja do Atlassian Identity Manager.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

19. W **Konfiguracja SAML dodać** okna, wykonaj następujące czynności:

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    a. W **dostawcy tożsamości identyfikator jednostki** Wklej identyfikator jednostki SAML skopiowany z portalu Azure.

    b. W **dostawcy tożsamości adresu URL logowania jednokrotnego** Wklej adres URL usługi rejestracji jednokrotnej SAML, który został skopiowany z portalu Azure.

    c. Otwórz certyfikat pobrany z portalu Azure w pliku txt, skopiuj wartość (bez *rozpocząć certyfikatu* i *End Certificate* wierszy), a następnie wklej go w **X509 publiczny certyfikat** pole.
    
    d. Wybierz **Zapisz konfigurację**.
     
20. Aby upewnić się, że skonfigurowano poprawne adresy URL, należy zaktualizować ustawienia usługi Azure AD w następujący sposób:
  
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)

    a. W oknie SAML kopiować **Identyfikatora tożsamości SP** , a następnie, w portalu Azure w chmurze Atlassian **domeny i adres URL**, wklej go w **identyfikator** pole.
    
    b. W oknie SAML kopiować **adres URL programu SP potwierdzenia klienta usługi** , a następnie, w portalu Azure w chmurze Atlassian **domeny i adres URL**, wklej go w **adres URL odpowiedzi** pole.  
        Adres URL logowania jest adres URL dzierżawy Atlassian chmury. 

    > [!NOTE]
    > Jeśli masz istniejący klient, po zaktualizowaniu **Identyfikatora tożsamości SP** i **adres URL programu SP potwierdzenia klienta usługi** wartości w portalu Azure wybierz **tak, zaktualizuj konfigurację**. W przypadku nowego klienta, możesz pominąć ten krok. 
    
21. W portalu Azure wybierz **zapisać**.

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> Jak podczas konfigurowania aplikacji, możesz przeczytać zwięzły wersji poprzednich instrukcji w [portalu Azure](https://portal.azure.com). Po dodaniu tej aplikacji z **usługi Active Directory** > **aplikacje dla przedsiębiorstw** zaznacz **rejestracji jednokrotnej** karcie i uzyskuje dostęp do osadzonego Dokumentacja w **konfiguracji** sekcji w dolnej części okna. Aby uzyskać więcej informacji, zobacz [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

W tej sekcji możesz tworzyć użytkownika testowego Simona Britta w portalu Azure w następujący sposób:

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

1. W portalu Azure, w lewym okienku wybierz **usługi Azure Active Directory** przycisku.

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png)

2. Aby wyświetlić listę użytkowników, wybierz **użytkowników i grup** > **wszyscy użytkownicy**.

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png)

3. W **wszyscy użytkownicy** wybierz **Dodaj**.

    ![Przycisk Dodaj](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png)

4. W **użytkownika** okna, wykonaj następujące czynności:

    ![Okno użytkownika](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png)

    a. W **nazwa** wpisz **BrittaSimon**.

    b. W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.

    c. Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.

    d. Wybierz pozycję **Utwórz**.
  
### <a name="create-an-atlassian-cloud-test-user"></a>Tworzenie użytkownika testowego Atlassian chmury

Aby umożliwić użytkownikom usługi Azure AD do logowania się w chmurze Atlassian, Zapewnij kont użytkowników ręcznie w chmurze Atlassian w następujący sposób:

1. W **administracji** okienku wybierz **użytkowników**.

    ![Łącze Atlassian użytkownicy w chmurze](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. Aby utworzyć użytkownika w chmurze Atlassian, wybierz **użytkownika zaproszenia**.

    ![Utwórz użytkownika Atlassian chmury](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. W **adres E-mail** wprowadź adres e-mail użytkownika, a następnie przypisz dostęp do aplikacji. 

    ![Utwórz użytkownika Atlassian chmury](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. Aby wysłać zaproszenie wiadomości e-mail do użytkownika, zaznacz **zaprosić użytkowników**.  
    Wiadomość e-mail z zaproszeniem są wysyłane do użytkownika, i po zaakceptowaniu zaproszenia, użytkownik jest aktywny w systemie. 

>[!NOTE] 
>Można również zbiorcze — tworzenie użytkowników, wybierając **Tworzenie zbiorczego** przycisk **użytkowników** sekcji.

### <a name="assign-the-azure-ad-test-user"></a>Przypisz użytkownika testowego usługi Azure AD

W tej sekcji możesz umożliwić użytkownikowi Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do chmury Atlassian. Aby to zrobić, wykonaj następujące czynności:

![Przypisanie roli użytkownika][200] 

1. W portalu Azure Otwórz **aplikacji** wyświetlić, przejdź do widoku katalogu, a następnie wybierz **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

2. W **aplikacji** listy, wybierz **chmury Atlassian**.

    ![Łącze Atlassian chmury na liście aplikacji](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png)  

3. W okienku po lewej stronie wybierz **użytkowników i grup**.

    ![Łącze "Użytkownicy i grupy"][202]

4. Wybierz **Dodaj** , a następnie w **Dodaj przydziału** okienku wybierz **użytkowników i grup**.

    ![W okienku Dodaj przydziału][203]

5. W **użytkowników i grup** okna w **użytkowników** listy, wybierz **Simona Britta**.

6. W **użytkowników i grup** wybierz **wybierz**.

7. W **Dodaj przydziału** wybierz **przypisać**.
    
### <a name="test-single-sign-on"></a>Test rejestracji jednokrotnej

W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.

Po wybraniu **chmury Atlassian** kafelka w panelu dostępu użytkownik powinien zalogować się przy automatycznie do aplikacji Atlassian chmury.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

