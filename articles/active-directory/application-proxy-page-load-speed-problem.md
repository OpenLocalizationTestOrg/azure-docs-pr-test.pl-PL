---
title: "aaaAn aplikacji serwera Proxy aplikacji trwa zbyt długo tooload | Dokumentacja firmy Microsoft"
description: "Strona obciążenia Rozwiązywanie problemów z wydajnością z powitania serwera Proxy aplikacji usługi Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a><span data-ttu-id="94bb8-103">Aplikacja serwera Proxy aplikacji trwa zbyt długo tooload</span><span class="sxs-lookup"><span data-stu-id="94bb8-103">An Application Proxy application takes too long tooload</span></span>

<span data-ttu-id="94bb8-104">W tym artykule pomocy toounderstand, dlaczego aplikacja serwera Proxy aplikacji usługi Azure AD może potrwać tooload dużo czasu i co można zrobić tooresolve ten problem.</span><span class="sxs-lookup"><span data-stu-id="94bb8-104">This article help you toounderstand why an Azure AD Application Proxy application may take a long time tooload, and what you can do tooresolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="94bb8-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="94bb8-105">Overview</span></span>
<span data-ttu-id="94bb8-106">Pracy aplikacji, ale Zobacz długi czas oczekiwania, może mieć kilka ulepszeń pomocniczych w topologii sieci, rozważ tooimprove hello szybkości.</span><span class="sxs-lookup"><span data-stu-id="94bb8-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider tooimprove hello speed.</span></span> <span data-ttu-id="94bb8-107">W wersji ewaluacyjnej topologii, zobacz hello [dokumentu zagadnienia dotyczące sieci](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="94bb8-107">For an evaluation of different topologies, see hello [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="94bb8-108">Jeśli te zagadnienia nie pomogły, Niestety nie ma obecnie mamy dodatkowe zalecenia dotyczące dostrajania wydajności.</span><span class="sxs-lookup"><span data-stu-id="94bb8-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="94bb8-109">Jako powitania serwera Proxy aplikacji usługi rozszerza toomore centrów danych, które mogą być bliżej tooyou, toosee poprawia czas oczekiwania może uruchomić bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="94bb8-109">As hello Application Proxy service expands toomore data centers that may be closer tooyou, you may start toosee improved latency directly.</span></span> <span data-ttu-id="94bb8-110">w centrach toosee hello pełny wykaz danych Azure, zostanie wyświetlony hello [stronę testową opóźnienia](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="94bb8-110">toosee hello full list of Azure data centers, you can see hello [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="94bb8-111">Witaj centrach danych o powitania serwera Proxy aplikacji usługi można znaleźć z hello [narzędzia Test porty łącznika](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="94bb8-111">hello data centers with hello Application Proxy service can be found with hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="94bb8-112">Opinię na lokalizacje centrum danych serwer Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="94bb8-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="94bb8-113">Może to być centra danych platformy Azure, które jeszcze nie zawierają serwera Proxy aplikacji, ale może spowodować tooa poprawy opóźnienia doskonały dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="94bb8-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead tooa great latency improvement for you.</span></span> <span data-ttu-id="94bb8-114">Lokalizacja w centrum danych Hello < aadapfeedback@microsoft.com > , możemy użyć tooplan Twojej opinii, jak firma Microsoft Rozwiń.</span><span class="sxs-lookup"><span data-stu-id="94bb8-114">hello data center location at <aadapfeedback@microsoft.com> so we can use your feedback tooplan as we expand.</span></span>

<span data-ttu-id="94bb8-115">Firma Microsoft pracuje nad pewne dodatkowe możliwości, które zwiększyć czas oczekiwania hello dzierżawcami, które są aktualnie długie opóźnienia i można się dokumentacji tooshare po dostępne.</span><span class="sxs-lookup"><span data-stu-id="94bb8-115">We are working on some additional capabilities that help improve hello latency for tenants that currently see long latencies, and be sure tooshare documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94bb8-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94bb8-116">Next steps</span></span>
[<span data-ttu-id="94bb8-117">Praca z istniejącym lokalnych serwerów proxy</span><span class="sxs-lookup"><span data-stu-id="94bb8-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
