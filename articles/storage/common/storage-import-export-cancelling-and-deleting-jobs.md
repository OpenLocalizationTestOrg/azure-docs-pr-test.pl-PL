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
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="ae403-103">Anulowanie i usuwania zadań Import/Eksport Azure</span><span class="sxs-lookup"><span data-stu-id="ae403-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="ae403-104">Anulowane zadania przed jego toorequest jest hello `Packaging` stanu, wywołanie hello [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) operacji i zestawu hello `CancelRequested` element zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="ae403-104">toorequest that a job be canceled before it is in hello `Packaging` state, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="ae403-105">Witaj zadanie zostało anulowane w sposób optymalny.</span><span class="sxs-lookup"><span data-stu-id="ae403-105">hello job is canceled on a best-effort basis.</span></span> <span data-ttu-id="ae403-106">W przypadku dysków w hello proces transferowania danych, dane mogą nadal toobe przekazywane nawet po zażądano anulowania.</span><span class="sxs-lookup"><span data-stu-id="ae403-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="ae403-107">Anulowane zadanie jest przeniesionego toohello `Completed` stanu i są przechowywane przez 90 dni, w którym są usuwane.</span><span class="sxs-lookup"><span data-stu-id="ae403-107">A canceled job is moved toohello `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="ae403-108">toodelete zadania, wywołanie hello [Usuń zadanie](/rest/api/storageimportexport/jobs#Jobs_Delete) operacji przed wysłał hello zadania (to znaczy hello zadania w trakcie hello `Creating` stanu).</span><span class="sxs-lookup"><span data-stu-id="ae403-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (that is, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="ae403-109">Możesz także usunąć zadania, gdy jest on w hello `Completed` stanu.</span><span class="sxs-lookup"><span data-stu-id="ae403-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="ae403-110">Po usunięciu zadania, jego informacje i jego stan nie są już dostępne za pośrednictwem interfejsu API REST hello lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ae403-110">After a job is deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae403-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ae403-111">Next steps</span></span>

* [<span data-ttu-id="ae403-112">Przy użyciu interfejsu API REST usługi Import/Eksport hello</span><span class="sxs-lookup"><span data-stu-id="ae403-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
