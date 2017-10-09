---
title: aaaUsing SAP na maszynach wirtualnych systemu Linux | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: a805cdecb515239057e185a92bf5c4d4e707f72f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="c6d32-103">W przypadku maszyn wirtualnych systemu Linux na platformie Azure przy użyciu SAP</span><span class="sxs-lookup"><span data-stu-id="c6d32-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="c6d32-104">Chmura obliczeniowa terminem powszechnie używane, który jest uzyskanie coraz więcej znaczenia w ramach hello branży IT z małych firm się toolarge i wielonarodowych firmy.</span><span class="sxs-lookup"><span data-stu-id="c6d32-104">Cloud Computing is a widely used term which is gaining more and more importance within hello IT industry, from small companies up toolarge and multinational corporations.</span></span> <span data-ttu-id="c6d32-105">Microsoft Azure to hello platformy usług w chmurze firmy Microsoft, która oferuje szeroką gamę nowe możliwości.</span><span class="sxs-lookup"><span data-stu-id="c6d32-105">Microsoft Azure is hello Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="c6d32-106">Teraz klienci są toorapidly może udostępnić i usuwanie aplikacji jako usługi w chmurze, więc nie są ograniczone tootechnical lub ograniczeń budżetowych.</span><span class="sxs-lookup"><span data-stu-id="c6d32-106">Now customers are able toorapidly provision and de-provision applications as Cloud-Services, so they are not limited tootechnical or budgeting restrictions.</span></span> <span data-ttu-id="c6d32-107">Zamiast inwestowanie czas i pieniądze na infrastrukturę sprzętu, firmy mogą skupić się na aplikacji hello, procesy biznesowe i korzyści dla klientów i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c6d32-107">Instead of investing time and budget into hardware infrastructure, companies can focus on hello application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="c6d32-108">Maszynom wirtualnym Microsoft Azure firma Microsoft oferuje kompleksowe infrastruktura jako usługa (IaaS) platformy.</span><span class="sxs-lookup"><span data-stu-id="c6d32-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="c6d32-109">Aplikacje oparte na oprogramowaniu SAP NetWeaver są obsługiwane w usłudze Azure Virtual Machines (IaaS).</span><span class="sxs-lookup"><span data-stu-id="c6d32-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="c6d32-110">oficjalne dokumenty Hello poniżej opisano, jak tooplan i wdrożenia SAP NetWeaver aplikacji opartych na maszynach wirtualnych systemu Windows na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d32-110">hello whitepapers below describe how tooplan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="c6d32-111">Można też wdrożyć aplikacje SAP NetWeaver oparte na [maszyn wirtualnych Windows](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6d32-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="c6d32-112">SAP NetWeaver na maszynach wirtualnych Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="c6d32-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="c6d32-113">title: aaaTesting SAP NetWeaver na maszynach wirtualnych programu Microsoft Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="c6d32-113">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="c6d32-114">Podsumowanie: Nie jest oficjalną SAP obsługiwane w tym momencie uruchamiania SAP NetWeaver na maszynach wirtualnych systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d32-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="c6d32-115">Niemniej jednak klientów może być toodo niektórych testów lub rozważyć toorun pokaz lub szkolenia systemów SAP na maszynach wirtualnych systemu Linux Azure tak długo, jak nie istnieje potrzeba kontaktu z działem pomocy technicznej SAP.</span><span class="sxs-lookup"><span data-stu-id="c6d32-115">Nevertheless customers might want toodo some testing or might consider toorun SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="c6d32-116">W tym artykule należy pomocy przy konfigurowaniu maszynach wirtualnych platformy Azure SUSE Linux do uruchamiania programu SAP i daje niektóre podstawowe wskazówki w kolejności tooavoid wspólnej potencjalne pułapki związane z.</span><span class="sxs-lookup"><span data-stu-id="c6d32-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order tooavoid common potential pitfalls.</span></span>

<span data-ttu-id="c6d32-117">Zaktualizowano: Grudnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="c6d32-117">Updated: December 2015</span></span>

[<span data-ttu-id="c6d32-118">W tym artykule można znaleźć tutaj</span><span class="sxs-lookup"><span data-stu-id="c6d32-118">This article can be found here</span></span>](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

