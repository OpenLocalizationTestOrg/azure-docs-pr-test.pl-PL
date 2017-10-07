---
title: "Witaj aaaUsing interfejsu API REST usługi Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, gdzie toofind zasoby przy użyciu hello Import/Eksport Azure usługi interfejsu API REST, w tym zarówno tooand jak materiałów referencyjnych."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: a01c170b1bc9c2b2ce9086d39de78a39fafb2c8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a>Przy użyciu interfejsu API REST usługi Import/Eksport Azure hello

Hello usługi Import/Eksport Microsoft Azure udostępnia interfejs API REST tooenable programowe kontrolę nad zadania importu/eksportu. Można użyć tooperform interfejsu API REST hello wszystkie hello importu/eksportu operacje, które można wykonywać za pomocą hello [portalu Azure](https://portal.azure.com/). Ponadto można użyć tooperform interfejsu API REST hello niektóre szczegółowe operacji, takich jak badania hello procentu ukończenia zadania, które nie są obecnie dostępne w portalu klasycznym hello.

Zobacz [przy użyciu hello Import/Eksport Microsoft Azure service tooTransfer danych tooBlob magazynu](storage-import-export-service.md) Omówienie usługi Import/Eksport hello i samouczek, który demonstruje sposób toouse hello toocreate portalu klasycznego i zarządzanie nimi importu i wyeksportować zadań.

## <a name="service-endpoints"></a>Punkty końcowe usługi

Hello usługi Import/Eksport Azure jest dostawcą zasobów dla usługi Azure Resource Manager i zawiera zestaw interfejsów API REST na powitania po końcowy HTTPS w celu zarządzania zadaniami importu/eksportu:

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>Przechowywanie wersji

Żądania toohello usługi Import/Eksport musi określać hello `api-version` parametru i ustaw jej wartość zbyt`2016-11-01`.

## <a name="importexport-service-operations"></a>Import/Eksport operacji usługi

[Tworzenie zadania importu](storage-import-export-creating-an-import-job.md)

[Tworzenie zadania eksportu](storage-import-export-creating-an-export-job.md)

[Pobieranie informacji o stanie zadania](storage-import-export-retrieving-state-info-for-a-job.md)

[Wyliczanie zadań](storage-import-export-enumerating-jobs.md)

[Anulowanie i usuwanie zadań](storage-import-export-cancelling-and-deleting-jobs.md)

[Manifesty wykonywanie kopii zapasowych dysków](storage-import-export-backing-up-drive-manifests.md)

[Diagnostyka i odzyskiwanie po błędach zadań usługi Import/Export](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a>Następne kroki

* [Magazyn importu/eksportu REST](/rest/api/storageimportexport)
