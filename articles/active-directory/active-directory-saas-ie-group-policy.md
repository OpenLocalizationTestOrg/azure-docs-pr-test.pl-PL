---
title: "Rozszerzenie panelu dostępu platformy Azure dla programu Internet Explorer przy użyciu obiektu zasad grupy aaaDeploy | Dokumentacja firmy Microsoft"
description: Jak toouse grupy zasad toodeploy hello programu Internet Explorer dodatek hello Moje aplikacje portalu.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a>Jak tooDeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy
Ten samouczek pokazuje, jak tooremotely zasad grupy toouse zainstalować hello rozszerzenia Panel dostępu dla programu Internet Explorer na komputerach użytkowników. To rozszerzenie jest wymagane dla programu Internet Explorer, użytkownicy muszą toosign do aplikacji, które są skonfigurowane przy użyciu [opartego na hasłach rejestracji jednokrotnej](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

Zaleca się, że administratorzy automatyzacji wdrażania hello tego rozszerzenia. W przeciwnym razie użytkownicy mają toodownload i sami zainstalują program hello rozszerzenia, który jest błąd toouser podatnych na błędy i musi mieć uprawnienia administratora. Ten samouczek obejmuje jedną metodę automatyzację wdrożenia oprogramowania za pomocą zasad grupy. [Dowiedz się więcej na temat zasad grupy.](https://technet.microsoft.com/windowsserver/bb310732.aspx)

Witaj rozszerzenia Panel dostępu jest również dostępny do [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) i [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), które wymagają tooinstall uprawnienia administratora.

## <a name="prerequisites"></a>Wymagania wstępne
* Po skonfigurowaniu [usług domenowych w usłudze Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), i mieć przyłączone do domeny tooyour maszyny użytkowników.
* Musi mieć hello "Edytuj ustawienia" uprawnień tooedit hello obiektu zasad grupy (GPO). Domyślnie to uprawnienie mają członkowie hello następujących grup zabezpieczeń: Administratorzy domeny, Administratorzy przedsiębiorstwa oraz Twórcy-właściciele zasad grupy. [Dowiedz się więcej.](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a>Krok 1: Tworzenie hello punktu dystrybucji
Najpierw należy umieścić pakiet Instalatora hello w lokalizacji sieciowej dostępnej dla maszyny hello który ma rozszerzenie hello instalacji tooremotely na. toodo, wykonaj następujące kroki:

1. Zaloguj się jako administrator na serwerze toohello
2. W hello **Menedżera serwera** okna, przejdź zbyt**pliki i usługi magazynu**.
   
    ![Otwieranie plików i usługi magazynu](./media/active-directory-saas-ie-group-policy/files-services.png)
3. Przejdź toohello **udziałów** kartę. Następnie kliknij przycisk **zadania** > **nowy udział...**
   
    ![Otwieranie plików i usługi magazynu](./media/active-directory-saas-ie-group-policy/shares.png)
4. Zakończenie hello **Kreator nowego udziału** oraz zestaw uprawnień tooensure, że jest dostępny z komputerów użytkowników. [Dowiedz się więcej na temat udziałów.](https://technet.microsoft.com/library/cc753175.aspx)
5. Pobierz powitania po pakiet Instalatora systemu Microsoft Windows (plik .msi): [Extension.msi panelu dostępu](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)
6. Kopiuj hello Instalatora pakietu tooa żądana lokalizacji w udziale hello.
   
    ![Skopiuj udziału toohello plików .msi hello.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. Sprawdź, czy z komputerów klienckich pakiet Instalatora hello stanie tooaccess z hello udziału. 

## <a name="step-2-create-hello-group-policy-object"></a>Krok 2: Tworzenie hello obiektu zasad grupy
1. Zaloguj się na serwerze toohello, który jest hostem instalacji usług domenowych w usłudze Active Directory (AD DS).
2. W hello Menedżera serwera, przejdź do pozycji zbyt**narzędzia** > **Zarządzanie zasadami grupy**.
   
    ![Przejdź tooTools > zarządzania zasadami grupy](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. W okienku po lewej stronie powitania hello **Zarządzanie zasadami grupy** okna, wyświetlić hierarchii jednostki organizacyjnej (OU) i określić, w których zakresie chcesz zasad grupy hello tooapply. Na przykład może się okazać toopick małych tooa toodeploy jednostki Organizacyjnej w przypadku kilku użytkowników do testowania lub mogą wybierać najwyższego poziomu jednostki Organizacyjnej toodeploy tooyour całej organizacji.
   
   > [!NOTE]
   > Czy toocreate, takich jak lub edytować jednostkach organizacyjnych (OU), Przełącz wstecz toohello Menedżera serwera i przejść za**narzędzia** > **użytkownicy usługi Active Directory i komputery**.
   > 
   > 
4. Po wybraniu jednostki Organizacyjnej, kliknij go prawym przyciskiem myszy i wybierz **Utwórz obiekt GPO w tej domenie i umieść tu łącze...**
   
    ![Utwórz nowy obiekt zasad grupy](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. W hello **nowy obiekt zasad grupy** monit, wpisz nazwę dla hello nowego obiektu zasad grupy.
   
    ![Nazwa hello nowy obiekt zasad grupy](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. Powitania kliknij prawym przyciskiem myszy obiekt zasad grupy, który został utworzony i wybierz **Edytuj**.
   
    ![Edytuj hello nowy obiekt zasad grupy](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a>Krok 3: Przypisz hello pakietu instalacyjnego
1. Określić, czy chcesz na podstawie rozszerzenia hello toodeploy **Konfiguracja komputera** lub **Konfiguracja użytkownika**. Korzystając z [Konfiguracja komputera](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), rozszerzenia hello jest zainstalowany na komputerze hello niezależnie od tego, które użytkownicy logują tooit. Z [Konfiguracja użytkownika](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), użytkownicy mają rozszerzenia hello zainstalowane dla nich niezależnie od tego, które komputery są zalogowani.
2. W okienku po lewej stronie powitania hello **Edytor zarządzania zasadami grupy** okna, przejdź tooeither o następującej ścieżki folderu, w zależności od tego, jakiego typu konfiguracji została wybrana opcja hello:
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. Kliknij prawym przyciskiem myszy **instalacji oprogramowania**, a następnie wybierz pozycję **nowy** > **pakietu...**
   
    ![Tworzenie nowego pakietu instalacyjnego oprogramowania](./media/active-directory-saas-ie-group-policy/new-package.png)
4. Przejdź toohello folderu udostępnionego, który zawiera pakiet Instalatora hello z [krok 1: Utwórz punkt dystrybucji hello](#step-1-create-the-distribution-point), wybierz plik msi hello i kliknij przycisk **Otwórz**.
   
   > [!IMPORTANT]
   > Udział hello znajduje się na tym samym serwerze, sprawdź, za pośrednictwem hello sieci ścieżkę, a nie ścieżkę do pliku lokalnego hello uzyskujesz hello msi.
   > 
   > 
   
    ![Wybierz pakiet instalacyjny hello z hello folderu udostępnionego.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. W hello **wdrażanie oprogramowania** monitu, wybierz pozycję **przypisane** dla metody wdrażania. Następnie kliknij przycisk **OK**.
   
    ![Wybierz przypisane, a następnie kliknij przycisk OK.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

rozszerzenie Hello jest teraz wdrożonej toohello jednostek organizacyjnych, wybrany. [Dowiedz się, jak Instalacja oprogramowania zasad grupy.](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a>Krok 4: Włącz automatyczne hello rozszerzenie programu Internet Explorer
Ponadto Instalator hello toorunning, każde rozszerzenie programu Internet Explorer musi być jawnie włączone zanim będzie można go używać. Wykonaj kroki hello poniżej tooenable hello rozszerzenia Panel dostępu za pomocą zasad grupy:

1. W hello **Edytor zarządzania zasadami grupy** Przejdź tooeither z hello następujące ścieżki, w zależności od tego, jakiego typu konfiguracji wybranego w oknie [krok 3: hello Przypisz pakietu instalacyjnego](#step-3-assign-the-installation-package):
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. Kliknij prawym przyciskiem myszy **lista dodatków**i wybierz **Edytuj**.
    ![Edytuj listę dodatek.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)
3. W hello **lista dodatków** wybierz **włączone**. Następnie w obszarze hello **opcje** kliknij **Pokaż...** .
   
    ![Kliknij pozycję Włącz, a następnie kliknij przycisk Pokaż...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. W hello **Pokaż zawartość** okna, wykonaj następujące kroki hello:
   
   1. Dla pierwszej kolumny hello (hello **Nazwa wartości** pola), kopiowanie i wklejanie powitania po identyfikator klasy:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`
   2. Dla drugiej kolumny hello (hello **wartość** pola), wpisz hello następujące wartości:`1`
   3. Kliknij przycisk **OK** tooclose hello **Pokaż zawartość** okna.
      
      ![Wypełnij hello wartości określonych powyżej.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. Kliknij przycisk **OK** tooapply Twoje zmiany i zamknij hello **lista dodatków** okna.

Witaj rozszerzenia powinno ono włączone dla hello maszyn w hello wybrane jednostki Organizacyjnej. [Dowiedz się więcej o korzystaniu z tooenable zasad grupy lub wyłącz dodatki programu Internet Explorer.](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a>Krok 5 (opcjonalny): wyłączanie "Zapamiętaj hasło" wiersza
Gdy użytkownicy logowania toowebsites przy użyciu hello rozszerzenia Panel dostępu, program Internet Explorer mogą następujące hello Pokaż Monituj pytaniem "ma toostore hasła?"

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

W razie potrzeby tooprevent użytkownikom dostępu do tego wiersza, wykonaj czynności hello tooprevent automatycznego zakończenia od zapamiętywanie haseł:

1. W hello **Edytor zarządzania zasadami grupy** okna, ścieżka Przejdź toohello wymienionych poniżej. Taka konfiguracja jest dostępna w obszarze tylko **Konfiguracja użytkownika**.
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. Znajdź ustawienie hello o nazwie **włączyć funkcję hello automatycznie uzupełniać nazwy użytkownika i hasła w formularzach**.
   
   > [!NOTE]
   > Poprzednie wersje usługi Active Directory może wyświetlić to ustawienie o nazwie hello **nie należy zezwalać haseł automatycznego zakończenia toosave**. Witaj konfiguracji tego ustawienia różni się od hello ustawienia opisane w tym samouczku.
   > 
   > 
   
    ![Należy pamiętać toolook w tym obszarze Ustawienia użytkownika.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. Kliknij prawym przyciskiem myszy hello powyżej ustawienia, a następnie wybierz **Edytuj**.
4. W oknie hello **włączyć funkcję hello automatycznie uzupełniać nazwy użytkownika i hasła w formularzach**, wybierz pozycję **wyłączone**.
   
    ![Wybierz opcję Wyłącz](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. Kliknij przycisk **OK** tooapply te zmiany i zamknij hello okna.

Użytkownicy będzie już można toostore stanie swoich poświadczeń lub użyj automatycznego zakończenia tooaccess wcześniej zapisanych poświadczeń. Jednak ta zasada umożliwia toouse toocontinue użytkowników automatycznego zakończenia dla innych typów pól formularza, np. pola wyszukiwania.

> [!WARNING]
> Jeśli zasada ta jest włączona po użytkownik zdecydował toostore niektórych poświadczeń, te zasady będą *nie* wyczyść hello poświadczenia, które zostały już zapisane.
> 
> 

## <a name="step-6-testing-hello-deployment"></a>Krok 6: Testowanie hello wdrożenia
Wykonaj kroki hello poniżej tooverify, jeśli wdrożenie rozszerzenie hello zakończyło się pomyślnie:

1. Jeśli została wdrożona przy użyciu **Konfiguracja komputera**, zaloguj się na komputerze klienckim, który należy toohello jednostek organizacyjnych, które wybrano w [krok 2: tworzenie hello obiektu zasad grupy](#step-2-create-the-group-policy-object). Jeśli została wdrożona przy użyciu **Konfiguracja użytkownika**, upewnij się, że toosign w jako użytkownik będący członkiem toothat jednostki Organizacyjnej.
2. Może upłynąć kilka znak dodatków dla zasad grupy hello zmiany toofully aktualizacji z tego komputera. Aktualizacja hello tooforce, otwórz **wiersza polecenia** okno i hello uruchom następujące polecenie:`gpupdate /force`
3. Należy ponownie uruchomić maszynę hello hello instalacji tootake miejsca. Rozruchowego może potrwać znacznie więcej czasu niż zwykle podczas rozszerzenia hello instaluje.
4. Po ponownym uruchomieniu, otwórz **programu Internet Explorer**. Na powitania prawym górnym rogu okna hello, kliknij przycisk **narzędzia** (hello koło zębate ikonę), a następnie wybierz **Zarządzanie dodatkami**.
   
    ![Przejdź tooTools > Zarządzanie dodatkami](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. W hello **Zarządzanie dodatkami** okna, sprawdź, że hello **rozszerzenia Panel dostępu** został zainstalowany, a jego **stan** została ustawiona zbyt**włączone**.
   
    ![Upewnij się, że hello rozszerzenia Panel dostępu jest zainstalowany i włączony.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a>Pokrewne artykuły
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Rozwiązywanie problemów z hello rozszerzenia Panel dostępu dla programu Internet Explorer](active-directory-saas-ie-troubleshooting.md)

