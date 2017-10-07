---
title: "pliki aaaPersist w powłoce chmury Azure (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące jak powłoki chmury Azure będzie się powtarzał plików."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a>Utrwalanie plików w powłoce chmury Azure
Powłoka chmury wykorzystuje pliki toopersist magazynu plików Azure między sesjami.

## <a name="set-up-a-clouddrive-file-share"></a>Konfigurowanie `clouddrive` udziału plików
Na początkowej start powłoki chmury monituje tooassociate nowy lub istniejący plik udostępniać pliki toopersist między sesjami.

### <a name="create-new-storage"></a>Tworzenie nowego magazynu

Gdy używasz podstawowych ustawień i wybierz tylko subskrypcję, powłoki chmury tworzy trzy zasoby w Twoim imieniu w regionie hello obsługiwane, która jest najbliższym tooyou:
* Grupa zasobów:`cloud-shell-storage-<region>`
* Konto magazynu:`cs<uniqueGuid>`
* Udziału plików:`cs-<user>-<domain>-com-<uniqueGuid>`

![Witaj ustawień subskrypcji](media/basic-storage.png)

Instaluje Hello udziału plików jako `clouddrive` w Twojej `$Home` katalogu. Witaj udział plików jest również używane toostore obrazu 5 GB, która jest tworzona automatycznie dla użytkownika i aktualizuje i będzie się powtarzał Twojej `$Home` katalogu. To działanie jednorazowe i udziału plików hello automatycznie instaluje się w kolejnych sesjach.

### <a name="use-existing-resources"></a>Korzystać z istniejących zasobów

Przy użyciu zaawansowanych opcji hello, można skojarzyć istniejących zasobów. Po wyświetleniu monitu Instalatora magazynu hello zaznacz **Pokaż zaawansowane ustawienia** tooview dodatkowe opcje. Istniejących udziałów plików odbierania toopersist obrazu użytkownika 5 GB z `$Home` katalogu. menu rozwijane Hello są filtrowane w Twoim regionie powłoki w chmurze i kont lokalnych nadmiarowe & geograficznie nadmiarowego magazynu.

![Witaj ustawienie grupy zasobów](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a>Ogranicz tworzenie zasobów przy użyciu zasad zasobów platformy Azure
Konta magazynu, utworzone w chmurze powłoki są oznaczane `ms-resource-usage:azure-cloud-shell`. Toodisallow użytkownikom tworzenie kont magazynu w chmurze powłoki, utworzyć [zasad zasobów platformy Azure dla tagów](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) wyzwolenia przy tym konkretnym elementem tag.

## <a name="how-cloud-shell-works"></a>Jak działa powłoki chmury
Powłoka w chmurze będzie się powtarzał plików za pomocą obu hello następujące metody:
* Tworzenie obrazu dysku z Twojej `$Home` toopersist katalogu wszystkich zawartości w katalogu hello. obraz dysku Hello jest zapisywany w udziale określony plik jako `acc_<User>.img` w `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, i automatycznie synchronizuje zmiany.

* Instalowanie udziału plików określony jako `clouddrive` w Twojej `$Home` katalogu do interakcji z udziału plików bezpośrednio. `/Home/<User>/clouddrive`jest mapowany za`fileshare.storage.windows.net/fileshare`.
 
> [!NOTE]
> Wszystkie pliki w Twojej `$Home` katalogu, takiego jak kluczy SSH są zachowywane w obrazie dysku użytkownika, który jest przechowywany w udziale zainstalowanego pliku. Zastosowanie najlepszych rozwiązań podczas utrwalania informacji w sieci `$Home` katalogu i udziału zainstalowanego pliku.

## <a name="use-hello-clouddrive-command"></a>Użyj hello `clouddrive` polecenia
Za pomocą powłoki w chmurze, można uruchomić polecenie o nazwie `clouddrive`, która umożliwia możesz toomanually aktualizacji hello udział pliku to jest tooCloud zainstalowanego powłoki.
![Uruchomienie polecenia "clouddrive" hello](media/clouddrive-h.png)

## <a name="mount-a-new-clouddrive"></a>Zainstaluj nowy`clouddrive`

### <a name="prerequisites-for-manual-mounting"></a>Wymagania wstępne dotyczące ręcznego instalowania
Można aktualizować hello udziału plików, który jest skojarzony z powłoki chmury przy użyciu hello `clouddrive mount` polecenia.

W przypadku instalowania istniejącego udziału pliku, muszą być hello kont magazynu:
* Magazyn lokalnie nadmiarowy lub udziałów plików magazynu geograficznie nadmiarowego toosupport.
* Znajduje się w danym regionie przypisane. Podczas pracy dołączania hello region przypisane do Ciebie toois na liście Nazwa grupy zasobów hello `cloud-shell-storage-<region>`.

### <a name="supported-storage-regions"></a>Regiony obsługiwanego magazynu
Hello Azure pliki muszą znajdować się w hello sam regionu co hello powłoki chmury maszyny, która jest instalowanie, ich. Klastry powłoki chmury istnieje obecnie w następujących regionach hello:
|Obszar|Region|
|---|---|
|Ameryki|Wschodnie stany USA, południowo środkowe stany USA, zachodnie stany USA|
|Europa|Europa Północna, Europa Zachodnia|
|Azja i Pacyfik|Indie centralnej, południowo-Azja.|

### <a name="hello-clouddrive-mount-command"></a>Witaj `clouddrive mount` polecenia

> [!NOTE]
> Jeśli w przypadku instalowania nowego udziału plików, nowy obraz użytkownika jest tworzona dla Twojego `$Home` katalogu, ponieważ poprzedniego `$Home` obrazu jest przechowywany w hello poprzedniej udziału plików.

Uruchom hello `clouddrive mount` z hello następujące parametry:

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

tooview więcej szczegółów, uruchom `clouddrive mount -h`, jak pokazano poniżej:

![Uruchomione hello "clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a>Odinstaluj`clouddrive`
Można odinstalować udziału plików, to jest zainstalowany tooCloud powłoki w dowolnym momencie. Po odinstalowane udziału plików będzie toomount zostanie wyświetlony monit o nowe tooyour wcześniejsze udziału pliku następnej sesji.

tooremove pliku udziału z chmury powłoki:
1. Uruchom polecenie `clouddrive unmount`.
2. Potwierdzić oraz potwierdzić monity hello.

Udziału plików będzie tooexist, o ile nie można usunąć ręcznie. Chmura powłoki wyszuka już ten udział plików w kolejnych sesjach.

tooview więcej szczegółów, uruchom `clouddrive unmount -h`, jak pokazano poniżej:

![Uruchomione hello "clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> Uruchomienie tego polecenia nie usunie żadnych zasobów. Ręczne usunięcie grupy zasobów, konta magazynu lub udziału plików, który jest mapowany tooCloud powłoki spowoduje trwałe usunięcie z `$Home` katalogu obrazu i innych plików w udziale plików. Nie można cofnąć tej akcji.

## <a name="list-clouddrive-file-shares"></a>Lista `clouddrive` udziałów plików
udziału plików, który jest zainstalowany jako toodiscover `clouddrive`, uruchom następujące hello `df` polecenia. 

tooclouddrive ścieżka pliku Hello pokazuje Twojej nazwy konta magazynu i udziału pliku w adresie URL hello. Na przykład: `//storageaccountname.file.core.windows.net/filesharename`

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a>Transfer plików lokalnych tooCloud powłoki
Witaj `clouddrive` katalogu synchronizacje z hello bloku magazynu z portalu Azure. Użyj tego bloku tootransfer lokalne pliki tooor z udziału plików. Aktualizowanie plików z poziomu powłoki chmury jest widoczny w hello magazyn plików graficznego interfejsu użytkownika podczas odświeżania bloku hello.

### <a name="download-files"></a>Pobieranie plików

![Lista plików lokalnych](media/download.png)
1. W hello portalu Azure Przejdź toohello udziału zainstalowanego pliku.
2. Wybierz plik docelowy hello.
3. Wybierz hello **Pobierz** przycisku.

### <a name="upload-files"></a>Przekazywanie plików

![Przekazane toobe plików lokalnych](media/upload.png)
1. Przejdź tooyour zainstalowanego udziału plików.
2. Wybierz hello **przekazać** przycisku.
3. Wybierz plik hello lub pliki, które mają tooupload.
4. Upewnij się, Przekaż hello.

Powinien zostać wyświetlony hello pliki, które są dostępne w Twojej `clouddrive` katalogu w chmurze powłoki.

## <a name="next-steps"></a>Następne kroki
[Szybki Start powłoki chmury](quickstart.md) <br>
[Więcej informacji na temat usługi Magazyn plików Azure](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[Więcej informacji na temat tagów magazynu](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>
