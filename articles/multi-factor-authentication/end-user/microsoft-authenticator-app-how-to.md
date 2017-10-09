---
title: "aaaMicrosoft Authenticator dla telefonów komórkowych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupgrade toohello najnowszej wersji Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a>Wprowadzenie do aplikacji Microsoft Authenticator hello
Witaj aplikacji Authenticator firmy Microsoft zapewnia dodatkowy poziom zabezpieczeń w ramach Twojego konta służbowego (na przykład bsimon@contoso.com) lub konta Microsoft (na przykład bsimon@outlook.com).

Aplikacja Hello działa w jednym z dwóch sposobów:

* **Powiadomienia**. Aplikacja Hello pomaga zapobiec tooaccounts nieautoryzowanym dostępem i Zatrzymaj fałszywe transakcje przez wypychanie powiadomień tooyour smartfonie lub tablecie. Wystarczy wyświetlić powiadomienie hello, a jeśli jest to uzasadnione, wybierz **Sprawdź**. W przeciwnym razie można wybrać **Odmów**. 
* **Kod weryfikacyjny**. Aplikacja Hello może służyć jako oprogramowania token toogenerate kod weryfikacyjny OAuth. Po wprowadzeniu nazwy użytkownika i hasła, należy wprowadzić kod hello podał aplikacji hello na powitania ekranu logowania. kod weryfikacyjny Hello zapewnia drugiej formy uwierzytelniania.

Aplikacja Microsoft Authenticator Hello zastępuje hello aplikacji Azure Authenticator. Aplikacja Azure Authenticator Hello wciąż działać, ale jeśli zdecydujesz się nową aplikację Microsoft Authenticator toomove toohello, w tym artykule mogą pomóc.  

## <a name="opt-in-for-two-step-verification"></a>Zgódź się na potrzeby weryfikacji dwuetapowej

Aplikacja Microsoft Authenticator Hello nie działa przez samego siebie. Skonfiguruj każdy z tooprompt kont dla drugiego metodę weryfikacji po zalogowaniu się nazwę użytkownika i hasło. 

Dla konta służbowego nie zwykle otrzymasz toochoose tej funkcji dla siebie. Zamiast tego administrator zabezpieczeń zdecyduje się w Twoim imieniu i następnie powiadamia tooregister metody weryfikacji dla Twojego konta. Jeśli ten scenariusz dotyczy tooyou, zapoznaj się z [co oznacza Azure Multi-Factor Authentication dla mnie](multi-factor-authentication-end-user.md).

Dla konta osobistego należy tooset się weryfikacji dwuetapowej dla siebie. Jeśli masz konto Microsoft, te kroki są dostępne w [o weryfikacji dwuetapowej](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification). 

Można również używać hello Authenticator firmy Microsoft z kont innych niż Microsoft. Funkcja hello one wywołać inną niż weryfikację dwuetapową, ale powinien być toofind mogli go w obszarze Ustawienia zabezpieczeń lub logowania. 

## <a name="install-hello-app"></a>Instalowanie aplikacji hello
Aplikacja Microsoft Authenticator Hello jest dostępna dla [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), i [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="add-accounts-toohello-app"></a>Dodaj aplikację toohello kont
Dla każdego konta, które mają aplikacji Microsoft Authenticator toohello tooadd użyj jednej z hello następujące procedury:

### <a name="add-a-personal-microsoft-account-toohello-app"></a>Dodaj aplikację toohello osobistego konta Microsoft

Do osobistego konta Microsoft (jeden użycie toosign w tooOutlook.com, Xbox, Skype, itp.), wszystkie mają toodo jest, zaloguj się na koncie tooyour w aplikacji Microsoft Authenticator hello.

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a>Dodaj służbowego lub szkolnego konta toohello aplikacji przy użyciu skaner kodów QR hello
1. Przejdź na ekran ustawień weryfikacji zabezpieczeń toohello.  Aby uzyskać informacje na temat tooget toothis ekranu, zobacz [zmiana ustawień zabezpieczeń](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).
2. Witaj pole wyboru obok zbyt**aplikacji uwierzytelniania** następnie wybierz **Konfiguruj**.

    ![przycisk Konfiguruj Hello na ekranie Ustawienia weryfikacji zabezpieczeń hello](./media/authenticator-app-how-to/azureauthe.png)

    Spowoduje to wyświetlenie ekranu kod QR.

    ![Ekran, który zawiera kod QR hello](./media/authenticator-app-how-to/barcode2.png)
3. Otwórz hello aplikacji Authenticator firmy Microsoft. Na powitania **kont** ekranu wybierz  **+** , a następnie określ, które mają tooadd konta firmowego lub szkolnego.
4. Użyj hello aparatu tooscan hello QR kodu, a następnie wybierz **gotowe** tooclose hello QR kodu ekranu.

    Jeśli aparatu nie działa prawidłowo, możesz [ręcznie wprowadzić kod hello QR i adres URL](#add-an-account-to-the-app-manually).

5. Gdy aplikacja hello zawiera nazwę konta z sześciocyfrowy kod podrzędne, wszystko będzie gotowe. 

    ![Ekran kont](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a>Ręcznie dodaj aplikację toohello konta
1. Przejdź na ekran ustawień weryfikacji zabezpieczeń toohello.  Aby uzyskać informacje na temat tooget toothis ekranu, zobacz [zmiana ustawień zabezpieczeń](multi-factor-authentication-end-user-manage-settings.md).
2. Wybierz **skonfigurować**.

    ![przycisk Konfiguruj Hello na ekranie Ustawienia weryfikacji zabezpieczeń hello](./media/authenticator-app-how-to/azureauthe.png)

    Spowoduje to wyświetlenie ekranu kod QR.  Uwaga hello kod i adres URL.

    ![Ekran, który zawiera kod hello QR i adres URL](./media/authenticator-app-how-to/barcode2.png)
3. Otwórz hello aplikacji Authenticator firmy Microsoft. Na powitania **kont** ekranu wybierz  **+** , a następnie określ, które mają tooadd konta firmowego lub szkolnego.

4. Skaner hello wybierz **ręcznie wprowadzić kod**.

    ![Ekran skanowania kod QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. Wprowadź w odpowiednich polach hello w aplikacji hello hello kod i adres URL hello, a następnie wybierz **Zakończ**.

    ![Ekran wprowadzić kod i adres URL](./media/authenticator-app-how-to/manual.png)

6. Gdy aplikacja hello zawiera nazwę konta z sześciocyfrowy kod podrzędne, wszystko będzie gotowe.

    ![Ekran kont](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a>Dodaj aplikację toohello konta przy użyciu funkcji Touch ID
Aplikacja Microsoft Authenticator Hello w systemie iOS obsługuje użycia funkcji Touch ID.  Usługa Azure Multi-Factor Authentication umożliwia organizacjom toorequire numeru PIN dla urządzeń. Touch ID użytkownicy systemu iOS nie wymagają tooenter numeru PIN. Zamiast tego można skanować ich odcisk palca i wybierz **Zatwierdź**.

Konfigurowanie funkcji Touch ID z Authenticator firmy Microsoft jest proste. Można wykonać żądanie normalne weryfikacji przy użyciu numeru PIN. Jeśli urządzenie obsługuje funkcję Touch ID, Microsoft Authenticator konfiguruje ją automatycznie dla tego konta.

![Weryfikacja instalacji funkcji Touch ID](./media/authenticator-app-how-to/touchid1.png)

Od tego punktu do przodu, gdy użytkownik jest wymagane tooverify logowanie, wybierz hello otrzymał powiadomienie wypychane i skanowania odcisku palca zamiast wprowadzania numeru PIN.

![Powiadomienia wypychane](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a>Po zalogowaniu się przy użyciu aplikacji hello

Po dodaniu konta toohello aplikacji może być zostanie wyświetlony monit o toodo testu toomake weryfikacji, czy wszystko zostało poprawnie skonfigurowane. Po wykonaniu tej gotowe! Nie trzeba toodo inaczej dopóki hello następnym logowaniu.

Jeśli została wybrana opcja toouse kodów weryfikacji w aplikacji hello, uruchom toosee ich na powitania strony głównej. Ich zmiana co 30 sekund, aby zawsze mieć nowy kod gdy będziesz potrzebować. Ale nie ma potrzeby toodo niczego z nimi dopóki Zaloguj się i są tooenter zostanie wyświetlony monit o kod weryfikacyjny.  
