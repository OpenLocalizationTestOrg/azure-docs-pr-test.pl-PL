---
title: Uzyskiwanie Identyfikatora Azure maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: "Opisuje sposób pobrać i użyć Azure Linux VM unikatowego identyfikatora."
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
ms.openlocfilehash: 258ce425d5692730011cf2f4468dc0ba77f4cb79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a>Otwieranie i korzystanie z unikatowego Identyfikatora maszyna wirtualna platformy Azure
Azure VM Unikatowy identyfikator to identyfikator 128-bitowe zakodowane i przechowywane w SMBIOS wszystkich Azure IaaS maszyny Wirtualnej i obecnie mogą być odczytywane za pomocą poleceń systemu BIOS platformy.

Azure Unikatowy identyfikator maszyny Wirtualnej jest właściwością tylko do odczytu. Azure Unikatowy identyfikator maszyny Wirtualnej nie zmieni się podczas zamykania ponowne uruchomienie systemu (albo planowane nieplanowane), uruchamiania i zatrzymywania usunąć przydział, usługi, naprawianie lub Przywróć w miejscu. Jednak jeśli maszyna wirtualna jest migawką i skopiowane do utworzenia nowego wystąpienia, nowy identyfikator VM Azure jest skonfigurowany.

> [!NOTE]
> Jeśli masz starszą maszyny wirtualne utworzone i działania, ponieważ ta nowa funkcja otrzymano wprowadzanie (18 września 2014), proszę ponownego uruchomienia maszyny Wirtualnej na automatyczne uzyskiwanie Azure Unikatowy identyfikator.
> 
> 

Aby uzyskać dostęp do usługi Azure Unikatowy identyfikator maszyny Wirtualnej z poziomu maszyny Wirtualnej:

## <a name="create-a-vm"></a>Tworzenie maszyny wirtualnej
Aby uzyskać więcej informacji, zobacz [Utwórz maszynę wirtualną](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="connect-to-the-vm"></a>Łączenie z maszyną wirtualną
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

Z powodu Big Endian bit kolejności rzeczywista Unikatowy identyfikator maszyny Wirtualnej w tym przypadku będą:

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

Azure Unikatowy identyfikator maszyny Wirtualnej może służyć w różnych scenariuszy, czy maszyna wirtualna jest uruchomiona na platformie Azure lub lokalnego i może ułatwić wymagań śledzenia licencjonowania, raportowania lub ogólne, które masz na wdrożeń IaaS platformy Azure. Wiele niezależnych dostawców oprogramowania tworzenia aplikacji i poświadczania je na platformie Azure może wymagać, aby zidentyfikować maszyny Wirtualnej platformy Azure przez cały cykl życia i sprawdzić, czy maszyna wirtualna działa na platformie Azure, lokalnie lub w innych dostawców chmury. Ten identyfikator platformy pozwalają na przykład wykryć, czy oprogramowanie jest licencjonowane lub pomoc do skorelowania danych maszyny Wirtualnej do źródła, takich jak pomoc na temat ustawiania prawo metryki dla prawej platformy, a także śledzenia i skorelowania tych metryk wśród innych celów.

