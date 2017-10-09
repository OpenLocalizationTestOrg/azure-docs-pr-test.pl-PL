---
title: "toocreate aaaHow przestrzeni nazw usługi Service Bus w hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie przestrzeni nazw usługi Service Bus przy użyciu hello portalu Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: d8907e7e4a804056f6d66d5a177d9ace967ed2ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a><span data-ttu-id="9a55c-103">Tworzenie przestrzeni nazw usługi Service Bus przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9a55c-103">Create a Service Bus namespace using hello Azure portal</span></span>

<span data-ttu-id="9a55c-104">Przestrzeń nazw jest kontenerem określania zakresu dla wszystkich składników służących do obsługi komunikatów.</span><span class="sxs-lookup"><span data-stu-id="9a55c-104">A namespace is a scoping container for all messaging components.</span></span> <span data-ttu-id="9a55c-105">W jednej przestrzeni nazw może znajdować się wiele kolejek i tematów, a przestrzenie nazw często pełnią rolę kontenerów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9a55c-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span> <span data-ttu-id="9a55c-106">Istnieją dwa sposoby toocreate przestrzeni nazw usługi Service Bus:</span><span class="sxs-lookup"><span data-stu-id="9a55c-106">There are two different ways toocreate a Service Bus namespace:</span></span>

1. <span data-ttu-id="9a55c-107">Azure Portal (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="9a55c-107">Azure portal (this article)</span></span>
2. <span data-ttu-id="9a55c-108">[Szablony usługi Resource Manager][create-namespace-using-arm]</span><span class="sxs-lookup"><span data-stu-id="9a55c-108">[Resource Manager templates][create-namespace-using-arm]</span></span>

## <a name="create-a-namespace-in-hello-azure-portal"></a><span data-ttu-id="9a55c-109">Tworzenie przestrzeni nazw w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9a55c-109">Create a namespace in hello Azure portal</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

<span data-ttu-id="9a55c-110">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="9a55c-110">Congratulations!</span></span> <span data-ttu-id="9a55c-111">Utworzono przestrzeń nazw obsługi komunikatów usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="9a55c-111">You have now created a Service Bus Messaging namespace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a55c-112">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9a55c-112">Next steps</span></span>

<span data-ttu-id="9a55c-113">Zapoznaj się z naszym [przykłady GitHub][github-samples], wykazujących niektóre hello bardziej zaawansowane funkcje obsługi komunikatów magistrali usług Azure.</span><span class="sxs-lookup"><span data-stu-id="9a55c-113">Check out our [GitHub samples][github-samples], which show some of hello more advanced features of Azure Service Bus Messaging.</span></span>

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
