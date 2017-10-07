---
title: "aaaInternet ukierunkowane Omówienie usługi równoważenia obciążenia | Dokumentacja firmy Microsoft"
description: "Omówienie internetowy modułu równoważenia obciążenia i ich funkcje. Jak usługi równoważenia obciążenia działa na platformie Azure przy użyciu maszyn wirtualnych i usług w chmurze."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="c570d-104">Omówienie usługi równoważenia obciążenia połączonej Internet</span><span class="sxs-lookup"><span data-stu-id="c570d-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="c570d-105">Moduł równoważenia obciążenia Azure mapuje hello publicznego adresu IP adres i numer portu przychodzącego ruchu toohello prywatnego adresu IP adres i numer portu hello maszyny wirtualnej i na odwrót hello ruchu odpowiedzi z maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="c570d-105">Azure load balancer maps hello public IP address and port number of incoming traffic toohello private IP address and port number of hello virtual machine and vice versa for hello response traffic from hello virtual machine.</span></span> <span data-ttu-id="c570d-106">Reguły równoważenia obciążenia pozwalają toodistribute określonych rodzajów ruchu sieciowego między wiele maszyn wirtualnych lub usług.</span><span class="sxs-lookup"><span data-stu-id="c570d-106">Load balancing rules allow you toodistribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="c570d-107">Na przykład wielu serwerów sieci web lub role sieci web można rozmieścić hello obciążenia ruchu żądania sieci web.</span><span class="sxs-lookup"><span data-stu-id="c570d-107">For example, you can spread hello load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="c570d-108">Dla usługi w chmurze, zawierającej wystąpienia ról sieci web lub roli proces roboczy można określić publiczny punkt końcowy w pliku definicji (csdef) hello usługi.</span><span class="sxs-lookup"><span data-stu-id="c570d-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in hello service definition (.csdef) file.</span></span>

<span data-ttu-id="c570d-109">Witaj *servicedefinition.csdef* plik zawiera hello konfiguracji punktu końcowego i jeśli istnieje wiele wystąpień roli we wdrożeniu roli sieci web lub procesu roboczego hello modułu równoważenia obciążenia będzie skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="c570d-109">hello *servicedefinition.csdef* file contains hello endpoint configuration and when you have multiple role instances for a web or worker role deployment, hello load balancer will be setup for it.</span></span> <span data-ttu-id="c570d-110">wdrożenie chmury tooyour wystąpień Hello sposób tooadd zmienia hello liczbę wystąpień w pliku konfiguracji usługi hello (.csfg).</span><span class="sxs-lookup"><span data-stu-id="c570d-110">hello way tooadd instances tooyour cloud deployment is changing hello instance count on hello service configuration file (.csfg).</span></span>

<span data-ttu-id="c570d-111">Witaj poniższej ilustracji przedstawiono punktu końcowego równoważeniem obciążenia dla ruchu w sieci web współużytkowany trzech maszyn wirtualnych do hello publiczne i prywatne port TCP 80.</span><span class="sxs-lookup"><span data-stu-id="c570d-111">hello following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for hello public and private TCP port of 80.</span></span> <span data-ttu-id="c570d-112">Te trzy maszyny wirtualne są w zestawie o zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="c570d-112">These three virtual machines are in a load-balanced set.</span></span>

![przykład modułu równoważenia obciążenia publiczny](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="c570d-114">Rysunek 1 — równoważeniem obciążenia punktu końcowego dla ruchu w sieci web</span><span class="sxs-lookup"><span data-stu-id="c570d-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="c570d-115">Gdy klienci internetowi wysyłać żądania strony sieci web toohello publicznego adresu IP usługi w chmurze hello na porcie TCP 80, hello Azure Load Balancer rozdziela żądania hello między hello trzech maszyn wirtualnych w zestawie o zrównoważonym obciążeniu hello.</span><span class="sxs-lookup"><span data-stu-id="c570d-115">When Internet clients send web page requests toohello public IP address of hello cloud service on TCP port 80, hello Azure Load Balancer distributes hello requests between hello three virtual machines in hello load-balanced set.</span></span> <span data-ttu-id="c570d-116">Aby uzyskać więcej informacji na temat algorytmów równoważenia obciążenia, zobacz hello [strony Przegląd usługi równoważenia obciążenia](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="c570d-116">For more information about load balancer algorithms, see hello [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="c570d-117">Domyślnie usługa równoważenia obciążenia Azure dystrybuuje ruch sieciowy równomiernie wielu wystąpień maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c570d-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="c570d-118">Można również skonfigurować koligację sesji, aby uzyskać więcej informacji, zobacz [tryb dystrybucji modułu równoważenia obciążenia](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="c570d-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c570d-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c570d-119">Next steps</span></span>

<span data-ttu-id="c570d-120">Dowiedz się więcej o [wewnętrznego modułu równoważenia obciążenia](load-balancer-internal-overview.md) toobetter zrozumienie, które usługa równoważenia obciążenia jest lepszym rozwiązaniem dla danego wdrożenia w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c570d-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) toobetter understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="c570d-121">Możesz również [rozpocząć tworzenie internetowy modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md) i skonfigurować typ [trybu rozkładu](load-balancer-distribution-mode.md) dla zachowania ruchu sieci usługi równoważenia obciążenia określonego.</span><span class="sxs-lookup"><span data-stu-id="c570d-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="c570d-122">Jeśli aplikacja wymaga połączenia tookeep aktywności dla serwerów za modułem równoważenia obciążenia, użytkownik może dowiedzieć się więcej o [ustawienia limitu czasu protokołu TCP dla usługi równoważenia obciążenia w stanie bezczynności](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="c570d-122">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="c570d-123">Aby ułatwić toolearn dotyczących zachowania bezczynności połączenia podczas korzystania z usługi równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="c570d-123">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
