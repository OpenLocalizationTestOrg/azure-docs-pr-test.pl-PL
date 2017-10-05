---
title: "Anuluj i usunąć zadanie usługi Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak anulować i usuwać zadania usługi Import/Eksport Microsoft Azure."
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
ms.openlocfilehash: 1e989c72fc03697bf6d2e515ff53003703665d1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="75169-103">Anulowanie i usuwania zadań Import/Eksport Azure</span><span class="sxs-lookup"><span data-stu-id="75169-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="75169-104">Aby zażądać anulowane zadania przed znajduje się on w `Packaging` stanu, należy wywołać [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) operacji i zestawu `CancelRequested` elementu `true`.</span><span class="sxs-lookup"><span data-stu-id="75169-104">To request that a job be canceled before it is in the `Packaging` state, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="75169-105">Zadanie zostało anulowane w sposób optymalny.</span><span class="sxs-lookup"><span data-stu-id="75169-105">The job is canceled on a best-effort basis.</span></span> <span data-ttu-id="75169-106">Jeśli dyski są w trakcie przesyłania danych, dane mogą nadal ma zostać przesłany nawet po zażądano anulowania.</span><span class="sxs-lookup"><span data-stu-id="75169-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="75169-107">Anulowane zadanie zostanie przeniesiony do `Completed` stanu i są przechowywane przez 90 dni, w którym są usuwane.</span><span class="sxs-lookup"><span data-stu-id="75169-107">A canceled job is moved to the `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="75169-108">Aby usunąć zadania, wywołaj [Usuń zadanie](/rest/api/storageimportexport/jobs#Jobs_Delete) operacji przed wysłał zadania (oznacza to, gdy zadanie jest w `Creating` stanu).</span><span class="sxs-lookup"><span data-stu-id="75169-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (that is, while the job is in the `Creating` state).</span></span> <span data-ttu-id="75169-109">Możesz także usunąć zadania, gdy jest on w `Completed` stanu.</span><span class="sxs-lookup"><span data-stu-id="75169-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="75169-110">Po usunięciu zadania, jego informacje i jego stan nie są już dostępne za pośrednictwem interfejsu API REST lub w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="75169-110">After a job is deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75169-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="75169-111">Next steps</span></span>

* [<span data-ttu-id="75169-112">Przy użyciu interfejsu API REST usługi Import/Eksport</span><span class="sxs-lookup"><span data-stu-id="75169-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
