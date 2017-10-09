---
title: "Przekierowanie aaaUsing w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure i używanie przekierowania w usłudze RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>Przy użyciu przekierowania w usłudze Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Przekierowywanie urządzeń pozwala użytkownikom interakcję z aplikacji zdalnych przy użyciu komputera lokalnego hello urządzeń dołączonych tootheir, telefon lub tablet. Na przykład jeśli podano Skype za pośrednictwem usługi Azure RemoteApp, użytkownika musi aparatu hello zainstalowane na ich toowork komputera za pomocą programu Skype. Dotyczy to również drukarki, głośniki monitorów i urządzenia peryferyjne podłączone zakresu USB.

Połączenia programów RemoteApp wykorzystuje hello protokołu RDP (Remote Desktop) i funkcja RemoteFX tooprovide przekierowania.

## <a name="what-redirection-is-enabled-by-default"></a>Jakie przekierowania jest domyślnie włączone?
Korzystając z programów RemoteApp, po przekierowań hello są domyślnie włączone. informacje Hello w nawiasach Pokaż hello ustawienie RDP.

* Odtwarzanie dźwięków na komputerze lokalnym hello (**Odtwarzaj na tym komputerze**). (audiomode:i:0)
* Przechwyć audio z komputera lokalnego hello i komputer zdalny toohello wysyłania (**Graj z tego komputera**). (audiocapturemode:i:1)
* Drukowanie toolocal drukarki (redirectprinters:i:1)
* Porty COM (redirectcomports:i:1)
* Karta inteligentna urządzenia (redirectsmartcards:i:1)
* Schowek (toocopy możliwości i Wklej) (redirectclipboard:i:1)
* Wyczyść typ czcionki Wygładzanie (Zezwalaj na wygładzanie czcionek: i:1)
* Przekieruj urządzeń wszystkich obsługiwanych Plug and Play. (devicestoredirect:s: *)

## <a name="what-other-redirection-is-available"></a>Jakie inne przekierowania jest dostępny?
Dwie opcje przekierowania są domyślnie wyłączone:

* Przekierowywanie dysków (mapowanie dysku): zamapowanych dysków w sesji zdalnej hello stają się dyski twarde komputera lokalnego. Dzięki temu możesz zapisać lub otwarte pliki z dysków lokalnych podczas pracy w sesji zdalnej hello.
* Przekierowywaniem USB: można użyć komputera lokalnego tooyour podłączonego urządzenia USB hello hello sesji zdalnej.

## <a name="change-your-redirection-settings-in-remoteapp"></a>Zmień ustawienia przekierowywania w programie RemoteApp
Ustawienia przekierowywania hello urządzeń dla kolekcji można zmienić za pomocą hello Microsoft Azure PowerShell przy użyciu zestawu SDK. Po zainstalowaniu hello nowego środowiska PowerShell i zestawu SDK, najpierw go skonfigurować toomanage subskrypcji, jak opisano w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

Następnie użyj polecenia toohello podobne, następujące właściwości niestandardowe RDP hello tooset:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(Należy pamiętać, że  *`n*  jest używany jako separator poszczególnych właściwości.)

Lista właściwości protokołu RDP, które niestandardowe są skonfigurowane, uruchom następujące polecenie cmdlet hello tooget. Warto zauważyć, że tylko niestandardowe właściwości są wyświetlane jako wyniki dane wyjściowe nie hello właściwości domyślnych:  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

Po ustawieniu właściwości niestandardowe należy określić wszystkie niestandardowe właściwości zawsze; w przeciwnym razie hello zostanie przywrócona ustawienia toodisabled.   

### <a name="common-examples"></a>Typowe przykłady
Użyj następującego polecenia cmdlet tooenable dysku przekierowania hello:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

Użyj tego polecenia cmdlet tooenable przekierowania USB i dysków:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

Użyj tego polecenia cmdlet toodisable Schowka udostępniania:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> Należy się toocompletely Wyloguj wszystkich użytkowników w kolekcji hello (i nie tylko odłączać) przed przetestowaniem hello zmiany. Wyłącz Przejdź toohello całkowicie są zalogowani użytkownicy tooensure **sesji** w kolekcji hello w hello portalu Azure i wylogowania wszyscy użytkownicy, którzy są odłączone lub zalogowany. Czasami może potrwać kilka sekund tooshow dyski lokalne powitania w Eksploratorze hello sesji.
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>Zmień ustawienia przekierowywania USB na kliencie systemu Windows
Jeśli chcesz toouse przekierowywaniem USB na komputerze, który łączy tooRemoteApp istnieją 2 akcje, które wymagają toohappen. 1 - administrator musi tooenable przekierowywaniem USB na poziomie zbioru hello przy użyciu programu Azure PowerShell. 2 — na każdym urządzeniu, gdzie chcesz toouse przekierowywaniem USB należy tooenable zasad grupy, która pozwala. Ten krok należy wykonać dla każdego użytkownika, który chce przekierowywaniem USB toouse toobe.

> [!NOTE]
> Przekierowywaniem USB z usługą Azure RemoteApp jest obsługiwana tylko dla komputerów z systemem Windows.
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a>Włącz przekierowanie USB w celu hello kolekcji usługi RemoteApp
Użyj następującego polecenia cmdlet przekierowywaniem USB tooenable na poziomie zbioru hello hello:

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a>Włącz przekierowywaniem USB do komputera klienckiego hello
ustawienia przekierowywania USB tooconfigure na komputerze:

1. Witaj Otwórz Edytor lokalnych zasad grupy (GPEDIT. MSC). (Uruchom gpedit.msc z wiersza polecenia).
2. Otwórz **komputera Konfiguracja komputera\Zasady\Szablony administracyjne\Składniki systemu Windows\Usługi usług pulpitu Podłączanie pulpitu Client\RemoteFX urządzenia przekierowywaniem USB**.
3. Kliknij dwukrotnie **Zezwalaj na RDP przekierowywanie inne obsługiwane urządzenia USB funkcji RemoteFX z tego komputera**.
4. Wybierz **włączone**, a następnie wybierz **administratorów i użytkowników w hello praw dostępu przekierowania USB RemoteFX**.
5. Otwórz wiersz polecenia z uprawnieniami administracyjnymi, a następnie uruchom następujące polecenie hello:
   
        gpupdate /force
6. Uruchom ponownie komputer hello.

Można również użyć toocreate narzędzia do zarządzania zasadami grupy hello i stosowanie zasad przekierowania USB powitania dla wszystkich komputerów w domenie:

1. Zaloguj się do kontrolera domeny hello jako administrator domeny hello.
2. Witaj Otwórz konsolę zarządzania zasadami grupy. (Kliknij **Start > Narzędzia administracyjne > Zarządzanie zasadami grupy**.)
3. Przejdź toohello domenę lub jednostkę organizacyjną, dla której ma zostać toocreate hello zasad.
4. Kliknij prawym przyciskiem myszy **domyślne zasady domeny**, a następnie kliknij przycisk **Edytuj**.
5. Otwórz **komputera Konfiguracja komputera\Zasady\Szablony administracyjne\Składniki systemu Windows\Usługi usług pulpitu Podłączanie pulpitu Client\RemoteFX urządzenia przekierowywaniem USB**.
6. Kliknij dwukrotnie **Zezwalaj na RDP przekierowywanie inne obsługiwane urządzenia USB funkcji RemoteFX z tego komputera**.
7. Wybierz **włączone**, a następnie wybierz **administratorów i użytkowników w hello praw dostępu przekierowania USB RemoteFX**.
8. Kliknij przycisk **OK**.  

