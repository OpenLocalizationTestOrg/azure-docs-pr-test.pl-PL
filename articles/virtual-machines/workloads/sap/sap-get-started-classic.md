---
title: "W przypadku maszyn wirtualnych systemu Linux przy użyciu SAP | Dokumentacja firmy Microsoft"
description: "Informacje na temat używania rozwiązań SAP na maszynach wirtualnych z systemem Linux | Microsoft Azure"
services: virtual-machines-linux,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: f9cd93dc-71ad-48a4-8778-4e48aec484a6
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 66eb53f99ce4b30ec283243deb3649c9ca897a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="3e745-103">W przypadku maszyn wirtualnych systemu Linux na platformie Azure przy użyciu SAP</span><span class="sxs-lookup"><span data-stu-id="3e745-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="3e745-104">Chmura obliczeniowa jest szeroko używanych terminem, który zyskuje coraz większe znaczenie w branży IT, od małych firm po duże i międzynarodowe korporacje.</span><span class="sxs-lookup"><span data-stu-id="3e745-104">Cloud Computing is a widely used term which is gaining more and more importance within the IT industry, from small companies up to large and multinational corporations.</span></span> <span data-ttu-id="3e745-105">Microsoft Azure to platforma usług w chmurze firmy Microsoft oferująca szerokie spektrum nowych możliwości.</span><span class="sxs-lookup"><span data-stu-id="3e745-105">Microsoft Azure is the Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="3e745-106">Obecnie użytkownicy mogą szybko aprowizować zasoby jako usługi w chmurze i anulować ich aprowizację, dzięki czemu nie muszą przejmować się ograniczeniami technicznymi czy budżetowymi.</span><span class="sxs-lookup"><span data-stu-id="3e745-106">Now customers are able to rapidly provision and de-provision applications as Cloud-Services, so they are not limited to technical or budgeting restrictions.</span></span> <span data-ttu-id="3e745-107">Zamiast inwestować czas i budżet w infrastrukturę sprzętową firmy mogą skoncentrować się na aplikacjach, procesie biznesowym oraz korzyściach dla swoich klientów i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3e745-107">Instead of investing time and budget into hardware infrastructure, companies can focus on the application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="3e745-108">Maszynom wirtualnym Microsoft Azure firma Microsoft oferuje kompleksowe infrastruktura jako usługa (IaaS) platformy.</span><span class="sxs-lookup"><span data-stu-id="3e745-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="3e745-109">Aplikacje oparte na oprogramowaniu SAP NetWeaver są obsługiwane w usłudze Azure Virtual Machines (IaaS).</span><span class="sxs-lookup"><span data-stu-id="3e745-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="3e745-110">Oficjalne dokumenty poniżej opisano, jak zaplanować i wdrożyć aplikacje SAP NetWeaver oparte na maszynach wirtualnych systemu Windows na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3e745-110">The whitepapers below describe how to plan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="3e745-111">Można też wdrożyć aplikacje SAP NetWeaver oparte na [maszyn wirtualnych Windows](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3e745-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="3e745-112">SAP NetWeaver na maszynach wirtualnych Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="3e745-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="3e745-113">Nazwa: Testowanie SAP NetWeaver na maszynach wirtualnych systemu Linux SUSE platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3e745-113">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="3e745-114">Podsumowanie: Nie jest oficjalną SAP obsługiwane w tym momencie uruchamiania SAP NetWeaver na maszynach wirtualnych systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3e745-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="3e745-115">Niemniej jednak klientów może być przeprowadzenie niektórych testów lub rozważyć do uruchamiania pokaz SAP lub systemy na maszynach wirtualnych systemu Linux platformy Azure, pod warunkiem, nie istnieje potrzeba kontaktu z działem pomocy technicznej SAP.</span><span class="sxs-lookup"><span data-stu-id="3e745-115">Nevertheless customers might want to do some testing or might consider to run SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="3e745-116">W tym artykule należy pomocy przy konfigurowaniu maszynach wirtualnych platformy Azure SUSE Linux do uruchamiania programu SAP i daje niektóre podstawowe wskazówki w celu uniknięcia typowych potencjalne pułapki związane.</span><span class="sxs-lookup"><span data-stu-id="3e745-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order to avoid common potential pitfalls.</span></span>

<span data-ttu-id="3e745-117">Zaktualizowano: Grudnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="3e745-117">Updated: December 2015</span></span>

[<span data-ttu-id="3e745-118">W tym artykule można znaleźć tutaj</span><span class="sxs-lookup"><span data-stu-id="3e745-118">This article can be found here</span></span>](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

