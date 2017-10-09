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
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a>Tworzenie przestrzeni nazw usługi Service Bus przy użyciu hello portalu Azure

Przestrzeń nazw jest kontenerem określania zakresu dla wszystkich składników służących do obsługi komunikatów. W jednej przestrzeni nazw może znajdować się wiele kolejek i tematów, a przestrzenie nazw często pełnią rolę kontenerów aplikacji. Istnieją dwa sposoby toocreate przestrzeni nazw usługi Service Bus:

1. Azure Portal (w tym artykule)
2. [Szablony usługi Resource Manager][create-namespace-using-arm]

## <a name="create-a-namespace-in-hello-azure-portal"></a>Tworzenie przestrzeni nazw w hello portalu Azure

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

Gratulacje! Utworzono przestrzeń nazw obsługi komunikatów usługi Service Bus.

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z naszym [przykłady GitHub][github-samples], wykazujących niektóre hello bardziej zaawansowane funkcje obsługi komunikatów magistrali usług Azure.

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
