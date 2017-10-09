---
title: Interfejs sieciowy tooreset aaaHow dla maszyny Wirtualnej systemu Windows Azure | Dokumentacja firmy Microsoft
description: Pokazuje, jak tooreset interfejsu sieciowego dla maszyny Wirtualnej systemu Windows Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="64e25-103">Jak tooreset interfejsu sieciowego dla maszyny Wirtualnej systemu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="64e25-103">How tooreset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="64e25-104">Nie można połączyć z tooMicrosoft maszyny wirtualnej systemu Windows Azure (VM), po wyłączeniu hello domyślnego interfejsu sieciowego (NIC) lub ręcznie ustawia statyczny adres IP dla karty sieciowej hello.</span><span class="sxs-lookup"><span data-stu-id="64e25-104">You cannot connect tooMicrosoft Azure Windows Virtual Machine (VM) after you disable hello default Network Interface (NIC) or manually sets a static IP for hello NIC.</span></span> <span data-ttu-id="64e25-105">W tym artykule opisano, jak tooreset hello interfejsu sieciowego dla maszyny Wirtualnej systemu Windows Azure, która rozwiąże problem połączenia zdalnego hello.</span><span class="sxs-lookup"><span data-stu-id="64e25-105">This article shows how tooreset hello network interface for Azure Windows VM, which will resolve hello remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="64e25-106">Resetuj interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="64e25-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="64e25-107">Klasycznych maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="64e25-107">For Classic VMs</span></span>

<span data-ttu-id="64e25-108">sieci tooreset interfejsu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="64e25-108">tooreset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="64e25-109">Przejdź toohello [portalu Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64e25-109">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="64e25-110">Wybierz **maszyn wirtualnych (klasyczne)**.</span><span class="sxs-lookup"><span data-stu-id="64e25-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="64e25-111">Wybierz hello wpływ maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64e25-111">Select hello affected Virtual Machine.</span></span>
4.  <span data-ttu-id="64e25-112">Wybierz **adresów IP**.</span><span class="sxs-lookup"><span data-stu-id="64e25-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="64e25-113">Jeśli hello **przydziału prywatnego adresu IP** nie jest **statycznych**, zmień ją za**statycznych**.</span><span class="sxs-lookup"><span data-stu-id="64e25-113">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
6.  <span data-ttu-id="64e25-114">Zmień hello **adres IP** tooanother adresu IP, dostępnym w hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="64e25-114">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
7.  <span data-ttu-id="64e25-115">Wybierz opcję Zapisz.</span><span class="sxs-lookup"><span data-stu-id="64e25-115">Select Save.</span></span>
8.  <span data-ttu-id="64e25-116">Witaj maszyny wirtualnej zostanie uruchomiony ponownie tooinitialize hello nowy system toohello karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="64e25-116">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
9.  <span data-ttu-id="64e25-117">Spróbuj tooRDP tooyour maszyny.</span><span class="sxs-lookup"><span data-stu-id="64e25-117">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="64e25-118">W przypadku powodzenia można zmienić hello prywatnego adresu IP address wstecz toohello oryginalnej, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="64e25-118">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="64e25-119">W przeciwnym razie można zachować.</span><span class="sxs-lookup"><span data-stu-id="64e25-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="64e25-120">Dla maszyn wirtualnych wdrożonych w modelu grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="64e25-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="64e25-121">Przejdź toohello [portalu Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64e25-121">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="64e25-122">Wybierz hello wpływ maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64e25-122">Select hello affected Virtual Machine.</span></span>
3.  <span data-ttu-id="64e25-123">Wybierz **interfejsy sieciowe**.</span><span class="sxs-lookup"><span data-stu-id="64e25-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="64e25-124">Wybierz powitalne skojarzoną z interfejsem sieciowym z komputera</span><span class="sxs-lookup"><span data-stu-id="64e25-124">Select hello Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="64e25-125">Wybierz **konfiguracje adresów IP**.</span><span class="sxs-lookup"><span data-stu-id="64e25-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="64e25-126">Wybierz hello IP.</span><span class="sxs-lookup"><span data-stu-id="64e25-126">Select hello IP.</span></span> 
7.  <span data-ttu-id="64e25-127">Jeśli hello **przydziału prywatnego adresu IP** nie jest **statycznych**, zmień ją za**statycznych**.</span><span class="sxs-lookup"><span data-stu-id="64e25-127">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
8.  <span data-ttu-id="64e25-128">Zmień hello **adres IP** tooanother adresu IP, dostępnym w hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="64e25-128">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
9. <span data-ttu-id="64e25-129">Witaj maszyny wirtualnej zostanie uruchomiony ponownie tooinitialize hello nowy system toohello karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="64e25-129">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
10. <span data-ttu-id="64e25-130">Spróbuj tooRDP tooyour maszyny.</span><span class="sxs-lookup"><span data-stu-id="64e25-130">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="64e25-131">W przypadku powodzenia można zmienić hello prywatnego adresu IP address wstecz toohello oryginalnej, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="64e25-131">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="64e25-132">W przeciwnym razie można zachować.</span><span class="sxs-lookup"><span data-stu-id="64e25-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-hello-unavailable-nics"></a><span data-ttu-id="64e25-133">Usuń hello niedostępny kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="64e25-133">Delete hello unavailable NICs</span></span>
<span data-ttu-id="64e25-134">Po można maszyny toohello pulpitu zdalnego, należy usunąć hello starego kart sieciowych tooavoid hello potencjalny problem:</span><span class="sxs-lookup"><span data-stu-id="64e25-134">After you can remote desktop toohello machine, you must delete hello old NICs tooavoid hello potential problem:</span></span>

1.  <span data-ttu-id="64e25-135">Otwórz Menedżera urządzeń.</span><span class="sxs-lookup"><span data-stu-id="64e25-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="64e25-136">Wybierz **widoku** > **Pokaż ukryte urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="64e25-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="64e25-137">Wybierz **karty sieciowe**.</span><span class="sxs-lookup"><span data-stu-id="64e25-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="64e25-138">Sprawdź, czy karty hello jako "Karta sieciowa Microsoft Hyper-V".</span><span class="sxs-lookup"><span data-stu-id="64e25-138">Check for hello adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="64e25-139">Może pojawić się niedostępne karty, który jest niedostępny. Kliknij prawym przyciskiem myszy kartę hello, a następnie wybierz Odinstaluj.</span><span class="sxs-lookup"><span data-stu-id="64e25-139">You might see an unavailable adapter that is grayed out. Right-click hello adapter and then select Uninstall.</span></span>

    ![Obraz powitania hello karty Sieciowej](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="64e25-141">Tylko odinstalować hello kart niedostępny hello o nazwie "Karta sieciowa Microsoft Hyper-V".</span><span class="sxs-lookup"><span data-stu-id="64e25-141">Only uninstall hello unavailable adapters that have hello name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="64e25-142">Po odinstalowaniu żadnego hello innych kart ukryte, może to spowodować dodatkowe problemy.</span><span class="sxs-lookup"><span data-stu-id="64e25-142">If you uninstall any of hello other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="64e25-143">Teraz wszystkie karty niedostępny powinny zostać wyczyszczone z systemu.</span><span class="sxs-lookup"><span data-stu-id="64e25-143">Now all unavailable adapter should be cleared out from your system.</span></span>