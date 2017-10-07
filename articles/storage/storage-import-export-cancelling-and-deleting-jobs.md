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
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="90c28-103">Anulowanie i usuwania zadań Import/Eksport Azure</span><span class="sxs-lookup"><span data-stu-id="90c28-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="90c28-104">Możesz poprosić o anulowane zadania przed hello `Packaging` stanu przez wywołanie hello [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) operacji i ustawienie hello `CancelRequested` element zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="90c28-104">You can request that a job be cancelled before it is in hello `Packaging` state by calling hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="90c28-105">będzie można anulować zadania Hello w sposób optymalny.</span><span class="sxs-lookup"><span data-stu-id="90c28-105">hello job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="90c28-106">W przypadku dysków w hello proces transferowania danych, dane mogą nadal toobe przekazywane nawet po zażądano anulowania.</span><span class="sxs-lookup"><span data-stu-id="90c28-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="90c28-107">Anulowano zadanie zostanie przesunięty toohello `Completed` stanu i są przechowywane przez 90 dni, po czym zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="90c28-107">A cancelled job will move toohello `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="90c28-108">toodelete zadania, wywołanie hello [Usuń zadanie](/rest/api/storageimportexport/jobs#Jobs_Delete) operacji przed wysłał zadania hello (*tj.*, podczas gdy jest zadanie hello hello `Creating` stanu).</span><span class="sxs-lookup"><span data-stu-id="90c28-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (*i.e.*, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="90c28-109">Możesz także usunąć zadania, gdy jest on w hello `Completed` stanu.</span><span class="sxs-lookup"><span data-stu-id="90c28-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="90c28-110">Po usunięciu zadania, jego informacje i jego stan nie są już dostępne za pośrednictwem interfejsu API REST hello lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="90c28-110">After a job has been deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90c28-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90c28-111">Next steps</span></span>

* [<span data-ttu-id="90c28-112">Przy użyciu interfejsu API REST usługi Import/Eksport hello</span><span class="sxs-lookup"><span data-stu-id="90c28-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
