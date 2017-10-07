---
title: "aaaCancel i Usuń zadanie usługi Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zadania toocancel i delete dla hello usługi Import/Eksport Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 13456a8e7652850baacb53730cc7bb1520b0a4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a>Anulowanie i usuwania zadań Import/Eksport Azure

 Anulowane zadania przed jego toorequest jest hello `Packaging` stanu, wywołanie hello [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) operacji i zestawu hello `CancelRequested` element zbyt`true`. Witaj zadanie zostało anulowane w sposób optymalny. W przypadku dysków w hello proces transferowania danych, dane mogą nadal toobe przekazywane nawet po zażądano anulowania.

 Anulowane zadanie jest przeniesionego toohello `Completed` stanu i są przechowywane przez 90 dni, w którym są usuwane.

 toodelete zadania, wywołanie hello [Usuń zadanie](/rest/api/storageimportexport/jobs#Jobs_Delete) operacji przed wysłał hello zadania (to znaczy hello zadania w trakcie hello `Creating` stanu). Możesz także usunąć zadania, gdy jest on w hello `Completed` stanu. Po usunięciu zadania, jego informacje i jego stan nie są już dostępne za pośrednictwem interfejsu API REST hello lub hello portalu Azure.

## <a name="next-steps"></a>Następne kroki

* [Przy użyciu interfejsu API REST usługi Import/Eksport hello](storage-import-export-using-the-rest-api.md)
