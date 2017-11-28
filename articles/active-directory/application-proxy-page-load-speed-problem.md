---
title: "Aplikacja serwera Proxy aplikacji trwa zbyt długo, aby załadować | Dokumentacja firmy Microsoft"
description: "Strona obciążenia Rozwiązywanie problemów z wydajnością z serwer Proxy aplikacji usługi Azure AD"
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
ms.openlocfilehash: ce462c90746e6af0dc201686557121665b82b93d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="an-application-proxy-application-takes-too-long-to-load"></a><span data-ttu-id="ca640-103">Aplikacja serwera Proxy aplikacji trwa zbyt długo, aby załadować</span><span class="sxs-lookup"><span data-stu-id="ca640-103">An Application Proxy application takes too long to load</span></span>

<span data-ttu-id="ca640-104">Ten artykuł ułatwia zrozumienie, dlaczego aplikacja serwera Proxy aplikacji usługi Azure AD może zająć dużo czasu ładowania i co można zrobić, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="ca640-104">This article help you to understand why an Azure AD Application Proxy application may take a long time to load, and what you can do to resolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="ca640-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ca640-105">Overview</span></span>
<span data-ttu-id="ca640-106">Jeśli pracy aplikacji, ale Zobacz długi czas oczekiwania, w topologii sieci, które warto uwzględnić w celu zwiększenia szybkości może istnieć kilka ulepszeń pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="ca640-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider to improve the speed.</span></span> <span data-ttu-id="ca640-107">W wersji ewaluacyjnej topologii, zobacz [dokumentu zagadnienia dotyczące sieci](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="ca640-107">For an evaluation of different topologies, see the [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="ca640-108">Jeśli te zagadnienia nie pomogły, Niestety nie ma obecnie mamy dodatkowe zalecenia dotyczące dostrajania wydajności.</span><span class="sxs-lookup"><span data-stu-id="ca640-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="ca640-109">Jak usługa serwera Proxy aplikacji zostanie rozszerzony więcej centrów danych, które mogą być zbliżonej do Ciebie, można rozpocząć bezpośrednio Zobacz ulepszone opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="ca640-109">As the Application Proxy service expands to more data centers that may be closer to you, you may start to see improved latency directly.</span></span> <span data-ttu-id="ca640-110">Aby zapoznać się z pełną listą centrach danych platformy Azure, zobacz [stronę testową opóźnienia](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="ca640-110">To see the full list of Azure data centers, you can see the [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="ca640-111">Centra danych z serwera Proxy aplikacji usługi można znaleźć z [narzędzia Test porty łącznika](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="ca640-111">The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="ca640-112">Opinię na lokalizacje centrum danych serwer Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="ca640-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="ca640-113">Może to być centrach danych platformy Azure, które jeszcze nie zawierają serwera Proxy aplikacji, ale może doprowadzić do poprawy opóźnienia doskonały dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="ca640-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead to a great latency improvement for you.</span></span> <span data-ttu-id="ca640-114">Centrum danych lokalizacji < aadapfeedback@microsoft.com > , możemy użyć swoją opinię do zaplanowania, jak firma Microsoft Rozwiń.</span><span class="sxs-lookup"><span data-stu-id="ca640-114">The data center location at <aadapfeedback@microsoft.com> so we can use your feedback to plan as we expand.</span></span>

<span data-ttu-id="ca640-115">Firma Microsoft pracuje nad pewne dodatkowe możliwości, które zwiększyć opóźnienie dzierżawcami, które są aktualnie długie opóźnienia i pamiętaj udostępnić dokumentacji, gdy są one dostępne.</span><span class="sxs-lookup"><span data-stu-id="ca640-115">We are working on some additional capabilities that help improve the latency for tenants that currently see long latencies, and be sure to share documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca640-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ca640-116">Next steps</span></span>
[<span data-ttu-id="ca640-117">Praca z istniejącym lokalnych serwerów proxy</span><span class="sxs-lookup"><span data-stu-id="ca640-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
