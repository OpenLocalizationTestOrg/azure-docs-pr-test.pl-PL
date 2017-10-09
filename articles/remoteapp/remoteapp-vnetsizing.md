---
title: "informacje o aaaSizing dla sieci Wirtualnej w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello wymagania dotyczące adresów IP dla usługi Azure RemoteApp z sieci Wirtualnej"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="e1d37-103">Informacje dotyczące zmiany rozmiaru sieci wirtualnej w usłudze Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e1d37-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e1d37-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="e1d37-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e1d37-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="e1d37-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e1d37-106">Gdy używasz usługi Azure RemoteApp z siecią wirtualną (VNET), programów RemoteApp używa adresów IP w podsieci hello.</span><span class="sxs-lookup"><span data-stu-id="e1d37-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within hello subnet.</span></span> <span data-ttu-id="e1d37-107">W oparciu o skali hello usługi RemoteApp, należy tooensure czy podsieć ma za mało adresów IP dostępnej dla maszyn wirtualnych usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e1d37-107">Based on hello scale of your RemoteApp service, you need tooensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="e1d37-108">Gdy w tych wskazówkach zmiany rozmiaru nie jest idealne jak RemoteApp dynamicznie się obraca i obraca dół maszyn wirtualnych w ramach kolekcji, pomoże Ci oszacować zakres podsieci.</span><span class="sxs-lookup"><span data-stu-id="e1d37-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="e1d37-109">Jest to szczególnie ważne, ponieważ po usługi RemoteApp znajduje się w sieci Wirtualnej, nie możesz zwiększyć rozmiar podsieci hello bez usuwania programów RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e1d37-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase hello subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="e1d37-110">Dla każdej kolekcji usługi RemoteApp, które mają toorun maksymalnie wykorzystując swoje możliwości powinien mieć 100 dostępnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="e1d37-110">For each RemoteApp collection that you want toorun at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="e1d37-111">Na przykład jeśli masz jednej kolekcji usługi RemoteApp w planie Standard hello i użytkownicy toohave hello maksymalną 500, powinien mieć 100 adresów IP dla tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="e1d37-111">For example, if you have one RemoteApp collection in hello Standard plan and you want toohave hello maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="e1d37-112">Podobnie należy 100 adresów IP dla kolekcji usługi RemoteApp w planie Basic hello mającą 800 użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="e1d37-112">Similarly, you need 100 IP addresses for a RemoteApp collection in hello Basic plan that has 800 users.</span></span> <span data-ttu-id="e1d37-113">Jeśli planujesz toohave mniejszą liczbę użytkowników (mniejsze niż maksymalna hello), można zmniejszyć adresów IP hello wymaganych na kolekcję.</span><span class="sxs-lookup"><span data-stu-id="e1d37-113">If you plan toohave fewer users (less than hello maximum), you can reduce hello IP addresses needed per collection.</span></span> <span data-ttu-id="e1d37-114">wymagany rozmiar minimalny podsieci Hello to 30 adresów IP (/ 27).</span><span class="sxs-lookup"><span data-stu-id="e1d37-114">hello minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="e1d37-115">Wyewidencjonuj hello następujące informacje toomake upewnić się, że sieć wirtualna jest skonfigurowana i działa propertly:</span><span class="sxs-lookup"><span data-stu-id="e1d37-115">Check out hello following information toomake sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="e1d37-116">Migracja z osobistego tooan sieci Wirtualnej sieci Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="e1d37-116">Migrate from a personal VNET tooan Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="e1d37-117">Sprawdź poprawność hello toouse sieci Wirtualnej platformy Azure z usługą Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e1d37-117">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>](remoteapp-vnet.md)

