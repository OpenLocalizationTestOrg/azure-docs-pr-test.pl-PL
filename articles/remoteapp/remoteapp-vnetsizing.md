---
title: "Ustawianie rozmiaru informacji dla sieci Wirtualnej w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat wymagania dotyczące adresów IP dla usługi Azure RemoteApp z sieci Wirtualnej"
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
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="6022c-103">Informacje dotyczące zmiany rozmiaru sieci wirtualnej w usłudze Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="6022c-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6022c-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="6022c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6022c-105">Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="6022c-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6022c-106">Gdy używasz usługi Azure RemoteApp z siecią wirtualną (VNET), programów RemoteApp używa adresów IP w podsieci.</span><span class="sxs-lookup"><span data-stu-id="6022c-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within the subnet.</span></span> <span data-ttu-id="6022c-107">Oparte na skali z usługą RemoteApp, należy się upewnić, że podsieć ma za mało adresów IP dostępnej dla maszyn wirtualnych usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="6022c-107">Based on the scale of your RemoteApp service, you need to ensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="6022c-108">Gdy w tych wskazówkach zmiany rozmiaru nie jest idealne jak RemoteApp dynamicznie się obraca i obraca dół maszyn wirtualnych w ramach kolekcji, pomoże Ci oszacować zakres podsieci.</span><span class="sxs-lookup"><span data-stu-id="6022c-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="6022c-109">Jest to szczególnie ważne, ponieważ po usługi RemoteApp znajduje się w sieci Wirtualnej, nie można zwiększyć rozmiar podsieci bez usuwania programów RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="6022c-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase the subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="6022c-110">Dla każdej kolekcji usługi RemoteApp, którą chcesz uruchomić maksymalnie wykorzystując swoje możliwości powinien mieć 100 dostępnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="6022c-110">For each RemoteApp collection that you want to run at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="6022c-111">Na przykład jeśli masz jednej kolekcji usługi RemoteApp w planie Standard i mają maksymalną 500 użytkowników, powinien mieć 100 adresów IP dla tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="6022c-111">For example, if you have one RemoteApp collection in the Standard plan and you want to have the maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="6022c-112">Podobnie należy 100 adresów IP dla kolekcji usługi RemoteApp w planie Basic mającą 800 użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="6022c-112">Similarly, you need 100 IP addresses for a RemoteApp collection in the Basic plan that has 800 users.</span></span> <span data-ttu-id="6022c-113">Jeśli planujesz mniejszą liczbę użytkowników (mniejszy niż maksymalny), można zmniejszyć adresy IP wymagane na kolekcję.</span><span class="sxs-lookup"><span data-stu-id="6022c-113">If you plan to have fewer users (less than the maximum), you can reduce the IP addresses needed per collection.</span></span> <span data-ttu-id="6022c-114">Wymagany rozmiar minimalny podsieci to 30 adresów IP (/ 27).</span><span class="sxs-lookup"><span data-stu-id="6022c-114">The minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="6022c-115">Sprawdź następujące informacje, aby upewnić się, że sieć wirtualna jest skonfigurowana i działa propertly:</span><span class="sxs-lookup"><span data-stu-id="6022c-115">Check out the following information to make sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="6022c-116">Migracja z osobistego sieci Wirtualnej do sieć Wirtualną platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6022c-116">Migrate from a personal VNET to an Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="6022c-117">Sprawdzanie poprawności sieci Wirtualnej platformy Azure do użycia z usługą Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="6022c-117">Validate the Azure VNET to use with Azure RemoteApp</span></span>](remoteapp-vnet.md)

