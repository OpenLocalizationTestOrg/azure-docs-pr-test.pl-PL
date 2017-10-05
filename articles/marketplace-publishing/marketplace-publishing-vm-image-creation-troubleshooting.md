---
title: "Jak rozwiązywać typowe problemy podczas tworzenia dysku VHD | Dokumentacja firmy Microsoft"
description: "Odpowiedzi na często zadawane pytania dotyczące rozwiązywania problemów i problemy podczas tworzenia dysku VHD."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c4e88a9fbb15dd90d619b159ae1065dfacc1907f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-common-issues-encountered-during-vhd-creation"></a><span data-ttu-id="1a0d3-103">Sposoby rozwiązywania typowych problemów napotykanych podczas tworzenia dysku VHD</span><span class="sxs-lookup"><span data-stu-id="1a0d3-103">How to troubleshoot common issues encountered during VHD creation</span></span>
<span data-ttu-id="1a0d3-104">W tym artykule zapewnia pomoc w portalu Azure Marketplace wydawcy i/lub administratora współpracującego, który może zgłaszać problemy lub ma często zadawane pytania podczas publikowania lub zarządzania ich solution(s) maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1a0d3-104">This article is provided to help an Azure Marketplace publisher and/or co-administrator that may experience an issue or have common questions while publishing or managing their virtual machine solution(s).</span></span>

1. <span data-ttu-id="1a0d3-105">Jak zmienić nazwę hosta?</span><span class="sxs-lookup"><span data-stu-id="1a0d3-105">How do I change the name of the host?</span></span>
   
    <span data-ttu-id="1a0d3-106">Po utworzeniu maszyny Wirtualnej, użytkownicy nie można zaktualizować nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="1a0d3-106">Once VM is created, users can’t update the name of the host.</span></span>
2. <span data-ttu-id="1a0d3-107">Jak można zresetować usług pulpitu zdalnego lub jego hasło logowania?</span><span class="sxs-lookup"><span data-stu-id="1a0d3-107">How to reset the Remote Desktop service or its login password?</span></span>
   
   * [<span data-ttu-id="1a0d3-108">Informacje dotyczące systemu Windows maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1a0d3-108">Reference for Windows VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [<span data-ttu-id="1a0d3-109">Informacje dotyczące maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="1a0d3-109">Reference for Linux VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. <span data-ttu-id="1a0d3-110">Sposób generowania nowych ssh certyfikatów?</span><span class="sxs-lookup"><span data-stu-id="1a0d3-110">How to generate new ssh certificates?</span></span>
   
   <span data-ttu-id="1a0d3-111">Skorzystaj z łącza: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span><span class="sxs-lookup"><span data-stu-id="1a0d3-111">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span></span>
4. <span data-ttu-id="1a0d3-112">Jak skonfigurować Otwórz certyfikatu sieci VPN?</span><span class="sxs-lookup"><span data-stu-id="1a0d3-112">How to configure an open VPN certificate?</span></span>
   
   <span data-ttu-id="1a0d3-113">Skorzystaj z łącza: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span><span class="sxs-lookup"><span data-stu-id="1a0d3-113">Please refer to the link: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span></span>
5. <span data-ttu-id="1a0d3-114">Co to jest zasady udzielania pomocy technicznej do uruchamiania w środowisku maszyny wirtualnej Microsoft Azure (infrastruktury jako — usługa) oprogramowanie serwera firmy Microsoft?</span><span class="sxs-lookup"><span data-stu-id="1a0d3-114">What is the support policy for running Microsoft server software in the Microsoft Azure virtual machine environment (infrastructure-as-a-service)?</span></span>
   
   <span data-ttu-id="1a0d3-115">Skorzystaj z łącza: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="1a0d3-115">Please refer to the link: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
6. <span data-ttu-id="1a0d3-116">Czy maszyny wirtualne mają żadnych Unikatowy identyfikator?</span><span class="sxs-lookup"><span data-stu-id="1a0d3-116">Do Virtual Machines have any unique identifier?</span></span>
   
   <span data-ttu-id="1a0d3-117">Azure koduje Azure VM Unikatowy identyfikator w każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1a0d3-117">Azure encodes Azure VM Unique ID in every VM.</span></span> <span data-ttu-id="1a0d3-118">Zobacz szczegółowe informacje w tym blogu i dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="1a0d3-118">See details in this blog and documentation.</span></span>
7. <span data-ttu-id="1a0d3-119">Na maszynie wirtualnej w jaki sposób zarządzać rozszerzenie skryptu niestandardowego w zadanie uruchamiania?</span><span class="sxs-lookup"><span data-stu-id="1a0d3-119">In a VM how can I manage the custom script extension in the startup task?</span></span>
   
   <span data-ttu-id="1a0d3-120">Skorzystaj z łącza: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span><span class="sxs-lookup"><span data-stu-id="1a0d3-120">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span></span>
8. <span data-ttu-id="1a0d3-121">Jak utworzyć Maszynę wirtualną z portalu Azure za pomocą wirtualny dysk twardy zostanie przekazany do magazynu premium?</span><span class="sxs-lookup"><span data-stu-id="1a0d3-121">How to create a VM from the Azure portal using the VHD that is uploaded to premium storage?</span></span>
   
   <span data-ttu-id="1a0d3-122">Firma Microsoft nie obsługują tej funkcji jeszcze.</span><span class="sxs-lookup"><span data-stu-id="1a0d3-122">We do not support this feature yet.</span></span>
9. <span data-ttu-id="1a0d3-123">Aplikacja 32-bitowych jest obsługiwane w portalu Azure Marketplace?</span><span class="sxs-lookup"><span data-stu-id="1a0d3-123">Is a 32-bit app supported in the Azure Marketplace?</span></span>
   
   <span data-ttu-id="1a0d3-124">Zapoznaj się z łącze, aby uzyskać więcej informacji na temat zasad pomocy technicznej: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="1a0d3-124">Please refer to the link for details on the support policy: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
10. <span data-ttu-id="1a0d3-125">Za każdym razem próbuję Tworzenie obrazu na podstawie moich wirtualne dyski twarde, zgłaszany jest błąd ". Dysk VHD jest już zarejestrowany z repozytorium obrazów jako zasób"w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a0d3-125">Every time I am trying to create an image from my VHDs, I get the error “.VHD is already registered with image repository as the resource” in PowerShell.</span></span> <span data-ttu-id="1a0d3-126">Nie utworzono żadnego obrazu, przed nie może znaleźć żadnego obrazu o tej nazwie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1a0d3-126">I did not create any image before nor did I find any image with this name in Azure.</span></span> <span data-ttu-id="1a0d3-127">Jak rozwiązać ten problem?</span><span class="sxs-lookup"><span data-stu-id="1a0d3-127">How do I resolve this?</span></span>
    
    <span data-ttu-id="1a0d3-128">Zazwyczaj dzieje się tak, jeśli użytkownik zainicjowaniu obsługi maszyny Wirtualnej z tym dyskiem VHD i istnieje blokada na tym dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="1a0d3-128">This usually happen if the user provisioned a VM from this VHD and there is a lock on that VHD.</span></span> <span data-ttu-id="1a0d3-129">Sprawdź, czy przydzielony z tym dyskiem VHD maszyna wirtualna nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="1a0d3-129">Please check that there is no VM allocated from this VHD.</span></span> <span data-ttu-id="1a0d3-130">Jeśli błąd nadal będzie nadal występować, następnie należy podnieść biletu pomocy technicznej za pomocą tego łącza lub z publikowania portalu dotyczącej to (szczegółowe informacje są podane w odpowiedzi na pytania 11).</span><span class="sxs-lookup"><span data-stu-id="1a0d3-130">If the error still persist , then please raise a support ticket using this link or from the Publishing portal regarding this (details are given in the answer of question 11).</span></span>