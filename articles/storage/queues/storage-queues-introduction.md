---
title: tooAzure aaaIntroduction magazynu kolejek | Dokumentacja firmy Microsoft
description: Wprowadzenie tooAzure magazynu kolejek
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a>Wprowadzenie tooQueues

Magazyn kolejek Azure to usługa do przechowywania dużej liczby komunikatów, które można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS. Pojedynczy komunikat z kolejki można się too64 KB, rozmiar, a kolejka może zawierać miliony komunikatów w górę toohello całkowitego limitu pojemności konta magazynu.

## <a name="common-uses"></a>Najczęstsze zastosowania

Najczęstsze zastosowania usługi Queue Storage obejmują:

* Tworzenie zaległości pracy tooprocess asynchronicznie
* Przekazywanie komunikatów z roli procesu roboczego platformy Azure tooan roli sieci web platformy Azure

## <a name="queue-service-concepts"></a>Pojęcia dotyczące usługi kolejki

Hello usługa kolejki zawiera hello następujące składniki:

![Pojęcia dotyczące kolejki](./media/storage-queues-introduction/queue1.png)

* **Format adresu URL:** kolejek mają hello następującego formatu adresu URL:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    Witaj następującego adresu URL dotyczy kolejki w diagramie hello:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Konto magazynu:** wszystkie dostępu tooAzure magazynu odbywa się za pomocą konta magazynu. Aby uzyskać szczegółowe informacje na temat pojemności konta magazynu, zobacz temat [Cele dotyczące skalowalności i wydajności usługi Azure Storage](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).

* **Kolejka:** kolejka zawiera zestaw komunikatów. Wszystkie komunikaty muszą być w kolejce. Należy zauważyć, że nazwa kolejki hello musi być tylko małe litery. Informacje dotyczące nazewnictwa kolejek można znaleźć w temacie [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx) (Nazewnictwo kolejek i metadanych).

* **Komunikat o błędzie:** A komunikatu, w dowolnym formacie z zapasowej too64 KB. Witaj maksymalny czas, który komunikatu może pozostawać w kolejce hello wynosi siedem dni.

## <a name="next-steps"></a>Następne kroki

* [Tworzenie konta magazynu](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [Wprowadzenie do korzystania z kolejki przy użyciu platformy .NET](storage-dotnet-how-to-use-queues.md)
