---
title: "udział plików Azure aaaMount za pośrednictwem protokołu SMB macOS | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak udostępnić toomount plików Azure za pośrednictwem protokołu SMB z macOS."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 71aaec8a77b770fe147b783c0ab9f86830176bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a>Instalowanie udziału plików platformy Azure za pomocą protokołu SMB w systemie macOS
[Magazyn plików Azure](../storage-dotnet-how-to-use-files.md) usługi firmy Microsoft, która umożliwia toocreate i użyj udziałów plików sieciowych w hello Azure używa hello branżowymi. Udziały plików platformy Azure można instalować w systemach macOS Sierra (10.12) i El Capitan (10.11). W tym artykule przedstawiono dwa różne sposoby toomount udziału plików platformy Azure na macOS z hello interfejsu użytkownika wyszukiwania i przy użyciu hello terminalu.

> [!Note]  
> Przed instalowaniem udziału plików platformy Azure przy użyciu protokołu SMB zaleca się wyłączenie podpisywanie pakietów SMB. Nie w ten sposób może spowodować niską wydajnością, dostęp do udziału plików platformy Azure hello macOS. Połączenia SMB, będą szyfrowane, więc nie ma to wpływu na powitania zabezpieczeń połączenia. Z terminala hello, hello następujące polecenia spowoduje wyłączenie podpisywanie pakietów, jak opisano to [artykuł pomocy technicznej firmy Apple po wyłączeniu podpisywanie pakietów](https://support.apple.com/HT205926):  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a>Wymagania wstępne dotyczące instalowania udziału plików platformy Azure w systemie macOS
* **Nazwa konta magazynu**: udział plików Azure toomount, muszą hello nazwy konta magazynu hello.

* **Klucz konta magazynu**: udział plików Azure toomount, będzie konieczne hello klucz podstawowy (lub dodatkowej) magazynu. Klucze sygnatur dostępu współdzielonego nie są aktualnie obsługiwane na potrzeby instalowania.

* **Otwarty port 445**: Protokół SMB komunikuje się za pośrednictwem portu TCP 445. Na komputerze klienckim (hello Mac) sprawdź toomake się, że Zapora nie blokuje TCP port 445.

## <a name="mount-an-azure-file-share-via-finder"></a>Instalowanie udziału plików platformy Azure za pomocą programu Finder
1. **Otwórz wyszukiwanie**: wyszukiwanie jest otwarty na macOS domyślnie, ale można zapewnić jest hello aktualnie zaznaczonej aplikacji, klikając hello "macOS stają przed ikonę" hello dokowania:  
    ![System macOS Hello stają przed ikony](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)

2. **Wybierz pozycję "Connect tooServer" z Menu "Idź" hello**: przy użyciu ścieżki UNC hello z hello [wymagania wstępne](#preq), przekonwertować hello początku podwójny ukośnik odwrotny (`\\`) zbyt`smb://` i wszystkie inne ukośników odwrotnych (`\`) tooforwards ukośniki (`/`). Łącze powinien wyglądać jak poniżej hello: ![hello "Connect tooServer" w oknie dialogowym](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)

3. **Użyj hello udziału nazwy i przechowywanie klucza konta po wyświetleniu monitu o nazwę użytkownika i hasło**: gdy na powitania "Connect tooServer" w oknie dialogowym kliknij przycisk "Połącz", zostanie wyświetlony monit o hello nazwę użytkownika i hasło (są to autopopulated z Twojej macOS Nazwa użytkownika). Dostępna jest opcja hello umieszczenie klucz konta magazynowania nazwa udziału hello w Twojej macOS łańcucha kluczy.

4. **Użyj udziału plików platformy Azure hello zgodnie z potrzebami**: po podstawiając hello udziału nazwy i magazynu klucz konta w hello nazwy użytkownika i hasła, zostanie zainstalowany hello udziału. Mogą wykorzystać te informacje, jak w przypadku normalnie udział pliku/folderu lokalnego, w tym przeciąganie i upuszczanie plików w udziale plików hello:

    ![Migawka przedstawiająca zainstalowany udział plików platformy Azure](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a>Instalowanie udziału plików platformy Azure za pomocą Terminala
1. Zastąp `<storage-account-name>` hello nazwą konta magazynu. Jeśli zostanie wyświetlony monit, podaj klucz konta magazynu jako hasło. 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. **Użyj udziału plików platformy Azure hello zgodnie z potrzebami**: hello udziału plików platformy Azure zostanie zainstalowany w punkcie instalacji hello określony przez hello poprzednie polecenie.  

    ![Migawka hello zainstalować udział plików Azure](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a>Następne kroki
Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.

* [Artykuł pomocy technicznej firmy Apple - jak tooconnect z udostępnianie plików na komputerze Mac](https://support.apple.com/HT204445)
* [Często zadawane pytania](../storage-files-faq.md)
* [Rozwiązywanie problemów w systemie Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Rozwiązywanie problemów w systemie Linux](storage-troubleshoot-linux-file-connection-problems.md)    