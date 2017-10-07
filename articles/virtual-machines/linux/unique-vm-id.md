---
title: aaaGet identyfikator maszyny Wirtualnej systemu Linux platformy Azure | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak tooget i użyj unikatowy maszyny Wirtualnej systemu Linux Azure identyfikatora."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a>Otwieranie i korzystanie z unikatowego Identyfikatora maszyna wirtualna platformy Azure
Azure VM Unikatowy identyfikator to identyfikator 128-bitowe zakodowane i przechowywane w SMBIOS wszystkich Azure IaaS maszyny Wirtualnej i obecnie mogą być odczytywane za pomocą poleceń systemu BIOS platformy.

Azure Unikatowy identyfikator maszyny Wirtualnej jest właściwością tylko do odczytu. Azure Unikatowy identyfikator maszyny Wirtualnej nie zmieni się podczas zamykania ponowne uruchomienie systemu (albo planowane nieplanowane), uruchamiania i zatrzymywania usunąć przydział, usługi, naprawianie lub Przywróć w miejscu. Jednak jeśli hello maszyny Wirtualnej jest migawki i skopiowanego toocreate nowe wystąpienie, nowy identyfikator VM Azure jest skonfigurowany.

> [!NOTE]
> Jeśli masz starszą maszyny wirtualne utworzone i uruchomione, ponieważ ta nowa funkcja otrzymano wprowadzanie (18 września 2014), uruchom ponownie tooautomatically Twojego wirtualna uzyskać Azure unikatowego identyfikatora.
> 
> 

Unikatowy identyfikator maszyny Wirtualnej platformy Azure z tooaccess w hello maszyny Wirtualnej:

## <a name="create-a-vm"></a>Tworzenie maszyny wirtualnej
Aby uzyskać więcej informacji, zobacz [Utwórz maszynę wirtualną](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="connect-toohello-vm"></a>Połącz toohello maszyny Wirtualnej
Aby uzyskać więcej informacji, zobacz [protokołu SSH w systemie Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="query-vm-unique-id"></a>Unikatowy identyfikator VM zapytania
Polecenie (przykładzie użyto **Ubuntu**):

```bash
sudo dmidecode | grep UUID
```

Przykład oczekiwane wyniki:

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

Powodu tooBig Endian bitów porządkowanie hello rzeczywiste Unikatowy identyfikator maszyny Wirtualnej w takim przypadku będą:

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

Unikatowy identyfikator Azure maszyny Wirtualnej może służyć w różnych scenariuszach czy hello maszyna wirtualna jest uruchomiona na platformie Azure lub lokalnie i może pomóc wymagań śledzenia licencjonowania, raportowania lub ogólne, które masz na wdrożeń IaaS platformy Azure. Wiele niezależnych dostawców oprogramowania tworzenia aplikacji i poświadczania je na platformie Azure mogą wymagać tooidentify maszyny Wirtualnej platformy Azure w całym jej cyklu życia i tootell, jeśli hello maszyna wirtualna jest uruchomiona na platformie Azure, lokalnie lub w innych dostawców chmury. Ten identyfikator platformy na przykład może pomóc w wykryć, czy jest licencjonowane oprogramowanie hello lub pomoc toocorrelate dowolnego źródła tooits danych maszyny Wirtualnej, takie jak tooassist na temat ustawiania hello prawo metryki dla platformy prawo hello i tootrack i skorelowania tych metryk między innych celów.

