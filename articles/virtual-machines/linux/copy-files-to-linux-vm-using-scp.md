---
title: "aaaMove pliki tooand z maszyn wirtualnych systemu Linux platformy Azure z punktu połączenia usługi | Dokumentacja firmy Microsoft"
description: "Bezpiecznie przenieść tooand plików z maszyny Wirtualnej systemu Linux na platformie Azure przy użyciu połączenia usługi i parę kluczy SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a>Przenieś pliki tooand z maszyny Wirtualnej systemu Linux przy użyciu połączenia usługi

W tym artykule opisano, jak toomove pliki z stacji roboczej w górę tooan maszyny Wirtualnej systemu Linux platformy Azure lub Azure maszyny Wirtualnej systemu Linux w dół tooyour stacji roboczej, przy użyciu bezpiecznego kopiowania (SCP). Przenoszenie plików między tą stacją roboczą a Maszynę wirtualną systemu Linux, szybkie i bezpieczne, jest szczególnie ważne dla zarządzania infrastrukturą platformy Azure. 

W tym artykule należy Linux maszyn wirtualnych wdrożonych w Azure przy użyciu [SSH publiczne i prywatne pliki klucza](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Należy również połączenia klienta dla komputera lokalnego. Jest oparty na SSH i zawarte w powłoki Bash domyślne hello większość komputerów z systemami Linux i komputerów Mac i niektóre powłoki systemu Windows.

## <a name="quick-commands"></a>Szybkie polecenia

Skopiuj plik się toohello maszyny Wirtualnej systemu Linux

```bash
scp file azureuser@azurehost:directory/targetfile
```

Skopiuj plik w dół z hello maszyny Wirtualnej systemu Linux

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik

Jako przykład możemy przenieść pliku konfiguracji platformy Azure w górę tooa maszyny Wirtualnej systemu Linux i rozwiń katalog pliku dziennika używają kluczy punkt połączenia usługi oraz SSH.   

## <a name="ssh-key-pair-authentication"></a>Uwierzytelnianie pary kluczy SSH

Punkt połączenia usługi używa SSH hello warstwy transportowej. SSH uchwytów hello uwierzytelniania na hoście docelowym hello i przenosi plik hello w tunelu zaszyfrowanych domyślnie dostępne przy użyciu protokołu SSH. W przypadku uwierzytelniania SSH można użyć nazwy użytkowników i hasła. Jednak najlepszym rozwiązaniem bezpieczeństwa zaleca się SSH publicznego i prywatnego klucza uwierzytelniania. Po uwierzytelnieniu hello połączenia SSH SCP następnie rozpoczyna się kopiowanie pliku hello. Przy użyciu poprawnego skonfigurowania `~/.ssh/config` i publicznymi i prywatnymi kluczy SSH, połączenie hello punkt połączenia usługi można nawiązać za pomocą tylko nazwa serwera (lub adres IP). Jeśli masz tylko jeden klucz SSH, punkt połączenia usługi szuka go w hello `~/.ssh/` katalogu i używa go przez domyślny toolog w toohello maszyny Wirtualnej.

Aby uzyskać więcej informacji na temat konfigurowania sieci `~/.ssh/config` i kluczy publicznych i prywatnych SSH, zobacz [utworzyć SSH klucze](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="scp-a-file-tooa-linux-vm"></a>Punkt połączenia usługi tooa plików maszyny Wirtualnej systemu Linux

Na przykład pierwszy hello firma Microsoft skopiuj plik konfiguracji platformy Azure się tooa maszyny Wirtualnej systemu Linux, który jest używany toodeploy automatyzacji. Ponieważ ten plik zawiera interfejsu API Azure poświadczenia, których klucze tajne, ważne jest zabezpieczeń. szyfrowany tunel Hello udostępniane przez SSH chroni zawartość hello hello pliku.

Witaj następujące lokalne powitania kopie polecenia *.azure/config* pliku tooan maszyny Wirtualnej platformy Azure z nazwą FQDN *myserver.eastus.cloudapp.azure.com*. nazwa użytkownika administratora hello na powitania maszyny Wirtualnej platformy Azure jest *azureuser* . Hello plik jest docelowe toohello */home/azureuser/* katalogu. Zastąp wartości w tym poleceniu.

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a>Punkt połączenia usługi katalogu z maszyny Wirtualnej systemu Linux

Na przykład firma Microsoft Skopiuj katalog plików dziennika z hello maszyny Wirtualnej systemu Linux w dół tooyour stacji roboczej. Plik dziennika może lub nie mogą zawierać poufne dane. Jednak przy użyciu połączenia usługi gwarantuje, że zawartość hello hello pliki dziennika są szyfrowane. Przy użyciu plików hello tootransfer punkt połączenia usługi jest hello Najprostszym sposobem tooget hello katalogu dziennika i plików w dół stacji roboczej tooyour podczas również jest bezpieczne.

Witaj następujące polecenie skopiuje pliki hello */home/azureuser/dzienniki/* katalogu na powitania maszyny Wirtualnej Azure toohello lokalnego tmp:

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

Witaj `-r` flagi interfejsu wiersza polecenia powoduje, że punkt połączenia usługi toorecursively kopiowania hello pliki i katalogi z punktu hello katalogu hello polecenia hello na liście.  Należy zauważyć, że hello składni wiersza polecenia jest także podobne tooa `cp` skopiować polecenia.

## <a name="next-steps"></a>Następne kroki

* [Zarządzanie użytkownikami, SSH i wyboru lub naprawy dysków na maszynach wirtualnych systemu Linux platformy Azure przy użyciu hello rozszerzenia VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
