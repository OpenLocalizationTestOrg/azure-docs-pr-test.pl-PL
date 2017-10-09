---
title: "aaaMigrate danych użytkownika z usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomigrate danych użytkownika i usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a>Jak toomigrate danych do i z usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Można używać wielu różnych narzędzi i metod tootransfer [dane użytkownika](remoteapp-upd.md) do i z usługi Azure RemoteApp. Oto kilka metod:

* Skopiuj i Wklej korzystania z funkcji udostępniania schowka
* Skopiuj pliki i dane serwera plików tooa
* Skopiuj pliki tooOneDrive dla firm przy użyciu przeglądarki
* Skopiować pliki przy użyciu przekierowania

> [!NOTE]
> Nie można włączyć hello usługi OneDrive dla firm i konsumentów agentów synchronizacji — one [nie są obsługiwane](remoteapp-onedrive.md) w usłudze Azure RemoteApp.
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a>Użyj kopiowania i wklejania w Eksploratorze plików
Kopiowanie i wklejanie przy użyciu Schowka hello jest włączone w przypadku wdrożeń usługi RemoteApp [domyślnie](remoteapp-redirection.md). Umożliwia to użytkownikom kopiowania plików między ich lokalnego komputera i programów RemoteApp aplikacji. Często za pośrednictwem hello trakcie normalnego przebiegu za pomocą aplikacji w usłudze RemoteApp, użytkownicy mają zapisane pliki UPD tootheir — przenoszenie, że dane z usługi RemoteApp jest prosty:

1. [Publikowanie Eksploratora plików jako aplikacja](remoteapp-publish.md) w kolekcji usługi RemoteApp. (Należy pamiętać, że jest to zadanie administracyjne).
2. Bezpośrednie użytkowników toolaunch hello Eksploratora plików aplikacji, która została opublikowana i toouse tego toocopy i Wklej pliki zarówno do ich UPD i od niego.

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a>Przekazywanie plików i serwer plików tooa danych za pomocą kopiowania plików na standardowe sieci
Organizacje często używają danych toostore ogólnych serwerów plików. Jeśli znasz nazwę serwera hello lub lokalizacji, użytkowników można Przeglądaj hello sieci lokalne powitania serwera, a następnie skopiuj pliki, znacznie, tak jak powyżej. Będzie ponownie mają toopublish tooRemoteApp Eksplorator plików i udostępnij go użytkownikom.

> [!NOTE]
> powitania serwera plików musi być hello routingu sieci, która programów RemoteApp został wdrożony do.
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a>Skopiuj pliki tooOneDrive dla firm
Mimo że nie można włączyć hello usługi OneDrive dla firm agenta synchronizacji w usłudze RemoteApp, możesz nadal skopiować pliki z tooOneDrive Twojego UPD dla firm za pośrednictwem przeglądarki. 

1. Publikowanie tooRemoteApp Eksploratora plików, a następnie się, że użytkownicy tooaccess hello plików za pomocą tej aplikacji. 
2. Jest najprostszym pliki tootransfer ich kompresji, użytkowników, należy utworzyć plik zip, który zawiera wszystkie tooOneDrive toomove pliki hello dla firm.
3. Poproś użytkowników portalu usługi Office 365 toohello toogo i przejdź tooOneDrive i przekaż plik zip hello.

## <a name="copy-files-by-using-drive-redirection"></a>Skopiuj pliki za pomocą przekierowania dysku
Jeśli włączono [przekierowanie dysku](remoteapp-redirection.md), mapowany dysk zostały już utworzone dla użytkowników. W takim przypadku można skompresować swoich plików na dysku hello przekierowanie i zapisywać je po tootheir komputera lokalnego.

## <a name="how-administrators-can-export-data"></a>Jak Administratorzy mogą eksportować dane

Zarządza dla usługi Azure RemoteApp można wyeksportować wszystkie dyski profilu użytkownika (UPD) dla wszystkich kolekcji w subskrypcji tooAzure magazynu przy użyciu programu Azure PowerShell polecenia cmdlet Export-AzureRemoteAppUserDisk.  Nie możliwości tooselect poszczególnych UPD firmy nie istnieje.  Po wykonaniu polecenia programu PowerShell hello każdego dysku użytkownika zostanie 50gb dysku o stałym rozmiarze rozmiar i być wyeksportowane tooAzure magazynu.  Koszty magazynu Azure będą naliczane natychmiast dla tego magazynu.  Jeżeli upewnij się, wykonanie tego polecenia nie ma żadnych sesji, które w przeciwnym razie eksportu hello zakończy się niepowodzeniem.

UPD dla wdrożenia usługi Azure RemoteApp przyłączony do domeny mogą być używane tylko ponownie we wdrożeniu usług pulpitu zdalnego, nie można użyć wdrożenia przyłączone do domeny z systemem innym niż.  W przypadku użycia tych dysków we wdrożeniu usług pulpitu zdalnego, firma Microsoft zaleca toouse naszych [automatycznego skrypty](https://github.com/arcadiahlyy/aramigration) który będzie wyeksportować, konwertowanie oraz importowanie hello w UPD do wdrożenia usług pulpitu zdalnego.

