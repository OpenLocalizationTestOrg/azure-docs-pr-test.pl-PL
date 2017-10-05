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
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="e4f9f-103">Otwieranie i korzystanie z unikatowego Identyfikatora maszyna wirtualna platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e4f9f-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="e4f9f-104">Azure VM Unikatowy identyfikator to identyfikator 128-bitowe zakodowane i przechowywane w SMBIOS wszystkich Azure IaaS maszyny Wirtualnej i obecnie mogą być odczytywane za pomocą poleceń systemu BIOS platformy.</span><span class="sxs-lookup"><span data-stu-id="e4f9f-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="e4f9f-105">Azure Unikatowy identyfikator maszyny Wirtualnej jest właściwością tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="e4f9f-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="e4f9f-106">Azure Unikatowy identyfikator maszyny Wirtualnej nie zmieni się podczas zamykania ponowne uruchomienie systemu (albo planowane nieplanowane), uruchamiania i zatrzymywania usunąć przydział, usługi, naprawianie lub Przywróć w miejscu.</span><span class="sxs-lookup"><span data-stu-id="e4f9f-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="e4f9f-107">Jednak jeśli maszyna wirtualna jest migawką i skopiowane do utworzenia nowego wystąpienia, nowy identyfikator VM Azure jest skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="e4f9f-107">However, if the VM is a snapshot and copied to create a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="e4f9f-108">Jeśli masz starszą maszyny wirtualne utworzone i działania, ponieważ ta nowa funkcja otrzymano wprowadzanie (18 września 2014), proszę ponownego uruchomienia maszyny Wirtualnej na automatyczne uzyskiwanie Azure Unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="e4f9f-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM to automatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="e4f9f-109">Aby uzyskać dostęp do usługi Azure Unikatowy identyfikator maszyny Wirtualnej z poziomu maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e4f9f-109">To access Azure Unique VM ID from within the VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="e4f9f-110">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e4f9f-110">Create a VM</span></span>
<span data-ttu-id="e4f9f-111">Aby uzyskać więcej informacji, zobacz [Utwórz maszynę wirtualną](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e4f9f-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="e4f9f-112">Łączenie z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="e4f9f-112">Connect to the VM</span></span>
<span data-ttu-id="e4f9f-113">Aby uzyskać więcej informacji, zobacz [protokołu SSH w systemie Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e4f9f-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="e4f9f-114">Unikatowy identyfikator VM zapytania</span><span class="sxs-lookup"><span data-stu-id="e4f9f-114">Query VM Unique ID</span></span>
<span data-ttu-id="e4f9f-115">Polecenie (przykładzie użyto **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="e4f9f-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="e4f9f-116">Przykład oczekiwane wyniki:</span><span class="sxs-lookup"><span data-stu-id="e4f9f-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="e4f9f-117">Z powodu Big Endian bit kolejności rzeczywista Unikatowy identyfikator maszyny Wirtualnej w tym przypadku będą:</span><span class="sxs-lookup"><span data-stu-id="e4f9f-117">Due to Big Endian bit ordering, the actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="e4f9f-118">Azure Unikatowy identyfikator maszyny Wirtualnej może służyć w różnych scenariuszy, czy maszyna wirtualna jest uruchomiona na platformie Azure lub lokalnego i może ułatwić wymagań śledzenia licencjonowania, raportowania lub ogólne, które masz na wdrożeń IaaS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f9f-118">Azure VM unique ID can be used in different scenarios whether the VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="e4f9f-119">Wiele niezależnych dostawców oprogramowania tworzenia aplikacji i poświadczania je na platformie Azure może wymagać, aby zidentyfikować maszyny Wirtualnej platformy Azure przez cały cykl życia i sprawdzić, czy maszyna wirtualna działa na platformie Azure, lokalnie lub w innych dostawców chmury.</span><span class="sxs-lookup"><span data-stu-id="e4f9f-119">Many independent software vendors building applications and certifying them on Azure may require to identify an Azure VM throughout its lifecycle and to tell if the VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="e4f9f-120">Ten identyfikator platformy pozwalają na przykład wykryć, czy oprogramowanie jest licencjonowane lub pomoc do skorelowania danych maszyny Wirtualnej do źródła, takich jak pomoc na temat ustawiania prawo metryki dla prawej platformy, a także śledzenia i skorelowania tych metryk wśród innych celów.</span><span class="sxs-lookup"><span data-stu-id="e4f9f-120">This platform identifier can for example help detect if the software is properly licensed or help to correlate any VM data to its source such as to assist on setting the right metrics for the right platform and to track and correlate these metrics amongst other uses.</span></span>

