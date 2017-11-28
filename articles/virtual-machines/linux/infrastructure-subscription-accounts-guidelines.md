---
title: aaaSubscription i konta dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat hello klucza projekt i implementację wytyczne dotyczące subskrypcji oraz konta na platformie Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9025a40783c008310ebd0f674deb4a9001ae974a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a><span data-ttu-id="8a75e-103">Azure subskrypcją i kontami wytyczne dotyczące maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="8a75e-103">Azure subscription and accounts guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="8a75e-104">Ten artykuł koncentruje się na sposób zwiększania rozmiaru tooapproach subskrypcji oraz konta zarządzania jako swojego środowiska i użytkownika podstawowej.</span><span class="sxs-lookup"><span data-stu-id="8a75e-104">This article focuses on understanding how tooapproach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="8a75e-105">Implementacja — wskazówki dla subskrypcji i konta</span><span class="sxs-lookup"><span data-stu-id="8a75e-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="8a75e-106">Decyzje:</span><span class="sxs-lookup"><span data-stu-id="8a75e-106">Decisions:</span></span>

* <span data-ttu-id="8a75e-107">Jaki zestaw subskrypcji i potrzebujesz toohost infrastruktury i obciążenia IT?</span><span class="sxs-lookup"><span data-stu-id="8a75e-107">What set of subscriptions and accounts do you need toohost your IT workload or infrastructure?</span></span>
* <span data-ttu-id="8a75e-108">Jak toobreak dół hello toofit hierarchii organizacji?</span><span class="sxs-lookup"><span data-stu-id="8a75e-108">How toobreak down hello hierarchy toofit your organization?</span></span>

<span data-ttu-id="8a75e-109">Zadania:</span><span class="sxs-lookup"><span data-stu-id="8a75e-109">Tasks:</span></span>

* <span data-ttu-id="8a75e-110">Zdefiniuj hierarchii logiczna organizacji ma się toomanage go z poziomu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8a75e-110">Define your logical organization hierarchy as you would like toomanage it from a subscription level.</span></span>
* <span data-ttu-id="8a75e-111">toomatch tej hierarchii logiczne, zdefiniuj hello konta wymagane i subskrypcje w ramach poszczególnych kont.</span><span class="sxs-lookup"><span data-stu-id="8a75e-111">toomatch this logical hierarchy, define hello accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="8a75e-112">Utwórz zestaw hello subskrypcje i kont za pomocą Konwencja nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="8a75e-112">Create hello set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="8a75e-113">Subskrypcje i konta</span><span class="sxs-lookup"><span data-stu-id="8a75e-113">Subscriptions and accounts</span></span>
<span data-ttu-id="8a75e-114">toowork z platformy Azure, należy co najmniej jedna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a75e-114">toowork with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="8a75e-115">Zasoby, na przykład maszynach wirtualnych (VM) lub sieci wirtualne istnieją w tych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8a75e-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="8a75e-116">Klienci korporacyjni zwykle mają rejestracji Enterprise, która jest hello najwyższy zasobów w hierarchii hello, a skojarzone tooone lub więcej kont.</span><span class="sxs-lookup"><span data-stu-id="8a75e-116">Enterprise customers typically have an Enterprise Enrollment, which is hello top-most resource in hello hierarchy, and is associated tooone or more accounts.</span></span>
* <span data-ttu-id="8a75e-117">Dla konsumentów i klientów bez rejestracji Enterprise zasób najwyższy hello jest hello konta.</span><span class="sxs-lookup"><span data-stu-id="8a75e-117">For consumers and customers without an Enterprise Enrollment, hello top-most resource is hello account.</span></span>
* <span data-ttu-id="8a75e-118">Subskrypcje są skojarzone tooaccounts i mogą istnieć co najmniej jedna subskrypcja dla danego konta.</span><span class="sxs-lookup"><span data-stu-id="8a75e-118">Subscriptions are associated tooaccounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="8a75e-119">Rozliczeń informacji na poziomie subskrypcji hello Azure rekordów.</span><span class="sxs-lookup"><span data-stu-id="8a75e-119">Azure records billing information at hello subscription level.</span></span>

<span data-ttu-id="8a75e-120">Powodu limit toohello poziomów hierarchii dwóch hello relacji konta/subskrypcji jest ważne tooalign hello konwencją nazewnictwa toohello konta i subskrypcji, rozliczeń potrzeb.</span><span class="sxs-lookup"><span data-stu-id="8a75e-120">Due toohello limit of two hierarchy levels on hello Account/Subscription relationship, it is important tooalign hello naming convention of accounts and subscriptions toohello billing needs.</span></span> <span data-ttu-id="8a75e-121">Na przykład jeśli globalne firma korzysta z platformy Azure, ich może wybrać konto toohave jeden na region, a ma zarządzać subskrypcjami w hello poziom regionu:</span><span class="sxs-lookup"><span data-stu-id="8a75e-121">For instance, if a global company uses Azure, they might choose toohave one account per region, and have subscriptions managed at hello region level:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="8a75e-122">Na przykład można użyć hello następujące struktury:</span><span class="sxs-lookup"><span data-stu-id="8a75e-122">For instance, you might use hello following structure:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="8a75e-123">Jeśli region decyduje toohave więcej niż jedną subskrypcję skojarzone tooa określonej grupy, hello konwencji nazewnictwa powinien dołączyć do nich tooencode sposób hello dodatkowe dane na konto hello lub hello nazwę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8a75e-123">If a region decides toohave more than one subscription associated tooa particular group, hello naming convention should incorporate a way tooencode hello extra data on either hello account or hello subscription name.</span></span> <span data-ttu-id="8a75e-124">Ta organizacja pozwala massaging rozliczeń danych toogenerate hello nowe poziomy hierarchii podczas rozliczeń raportów:</span><span class="sxs-lookup"><span data-stu-id="8a75e-124">This organization allows massaging billing data toogenerate hello new levels of hierarchy during billing reports:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="8a75e-125">Witaj organizacji może wyglądać hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="8a75e-125">hello organization could look like hello following example:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="8a75e-126">Firma Microsoft udostępnia szczegółowy rozliczeń za pośrednictwem plików do pobrania dla jednego konta lub dla wszystkich kont w umowy enterprise agreement.</span><span class="sxs-lookup"><span data-stu-id="8a75e-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a75e-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8a75e-127">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

