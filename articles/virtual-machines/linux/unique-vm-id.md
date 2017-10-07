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
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="191ca-103">Otwieranie i korzystanie z unikatowego Identyfikatora maszyna wirtualna platformy Azure</span><span class="sxs-lookup"><span data-stu-id="191ca-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="191ca-104">Azure VM Unikatowy identyfikator to identyfikator 128-bitowe zakodowane i przechowywane w SMBIOS wszystkich Azure IaaS maszyny Wirtualnej i obecnie mogą być odczytywane za pomocą poleceń systemu BIOS platformy.</span><span class="sxs-lookup"><span data-stu-id="191ca-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="191ca-105">Azure Unikatowy identyfikator maszyny Wirtualnej jest właściwością tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="191ca-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="191ca-106">Azure Unikatowy identyfikator maszyny Wirtualnej nie zmieni się podczas zamykania ponowne uruchomienie systemu (albo planowane nieplanowane), uruchamiania i zatrzymywania usunąć przydział, usługi, naprawianie lub Przywróć w miejscu.</span><span class="sxs-lookup"><span data-stu-id="191ca-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="191ca-107">Jednak jeśli hello maszyny Wirtualnej jest migawki i skopiowanego toocreate nowe wystąpienie, nowy identyfikator VM Azure jest skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="191ca-107">However, if hello VM is a snapshot and copied toocreate a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="191ca-108">Jeśli masz starszą maszyny wirtualne utworzone i uruchomione, ponieważ ta nowa funkcja otrzymano wprowadzanie (18 września 2014), uruchom ponownie tooautomatically Twojego wirtualna uzyskać Azure unikatowego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="191ca-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM tooautomatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="191ca-109">Unikatowy identyfikator maszyny Wirtualnej platformy Azure z tooaccess w hello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="191ca-109">tooaccess Azure Unique VM ID from within hello VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="191ca-110">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="191ca-110">Create a VM</span></span>
<span data-ttu-id="191ca-111">Aby uzyskać więcej informacji, zobacz [Utwórz maszynę wirtualną](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="191ca-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-toohello-vm"></a><span data-ttu-id="191ca-112">Połącz toohello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="191ca-112">Connect toohello VM</span></span>
<span data-ttu-id="191ca-113">Aby uzyskać więcej informacji, zobacz [protokołu SSH w systemie Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="191ca-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="191ca-114">Unikatowy identyfikator VM zapytania</span><span class="sxs-lookup"><span data-stu-id="191ca-114">Query VM Unique ID</span></span>
<span data-ttu-id="191ca-115">Polecenie (przykładzie użyto **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="191ca-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="191ca-116">Przykład oczekiwane wyniki:</span><span class="sxs-lookup"><span data-stu-id="191ca-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="191ca-117">Powodu tooBig Endian bitów porządkowanie hello rzeczywiste Unikatowy identyfikator maszyny Wirtualnej w takim przypadku będą:</span><span class="sxs-lookup"><span data-stu-id="191ca-117">Due tooBig Endian bit ordering, hello actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="191ca-118">Unikatowy identyfikator Azure maszyny Wirtualnej może służyć w różnych scenariuszach czy hello maszyna wirtualna jest uruchomiona na platformie Azure lub lokalnie i może pomóc wymagań śledzenia licencjonowania, raportowania lub ogólne, które masz na wdrożeń IaaS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="191ca-118">Azure VM unique ID can be used in different scenarios whether hello VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="191ca-119">Wiele niezależnych dostawców oprogramowania tworzenia aplikacji i poświadczania je na platformie Azure mogą wymagać tooidentify maszyny Wirtualnej platformy Azure w całym jej cyklu życia i tootell, jeśli hello maszyna wirtualna jest uruchomiona na platformie Azure, lokalnie lub w innych dostawców chmury.</span><span class="sxs-lookup"><span data-stu-id="191ca-119">Many independent software vendors building applications and certifying them on Azure may require tooidentify an Azure VM throughout its lifecycle and tootell if hello VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="191ca-120">Ten identyfikator platformy na przykład może pomóc w wykryć, czy jest licencjonowane oprogramowanie hello lub pomoc toocorrelate dowolnego źródła tooits danych maszyny Wirtualnej, takie jak tooassist na temat ustawiania hello prawo metryki dla platformy prawo hello i tootrack i skorelowania tych metryk między innych celów.</span><span class="sxs-lookup"><span data-stu-id="191ca-120">This platform identifier can for example help detect if hello software is properly licensed or help toocorrelate any VM data tooits source such as tooassist on setting hello right metrics for hello right platform and tootrack and correlate these metrics amongst other uses.</span></span>

