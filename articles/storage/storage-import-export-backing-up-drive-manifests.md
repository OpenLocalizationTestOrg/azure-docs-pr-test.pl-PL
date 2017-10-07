---
title: "aaaBacking się manifestów dysku Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toohave dysku manifesty hello usługi Import/Eksport Microsoft Azure automatycznie kopii zapasowej."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a>Tworzenie kopii zapasowej dysku manifesty prac Import/Eksport Azure

Manifesty dysku może automatycznie kopii zapasowej tooblobs przez ustawienie hello `BackupDriveManifest` właściwości zbyt`true` w hello [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) lub [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) operacje interfejsu API REST. Domyślnie program hello dysku manifestów nie kopii zapasowej. Witaj dysku manifestu w kopie zapasowe są przechowywane jako blokowych obiektów blob w kontenerze w ramach konta magazynu hello skojarzone z zadaniem hello. Domyślnie nazwa kontenera hello jest `waimportexport`, można jednak określić inną nazwę w hello `DiagnosticsPath` właściwości podczas wywoływania metody hello `Put Job` lub `Update Job Properties` operacji. Witaj kopii zapasowej manifestu obiektów blob są o nazwie w hello następującego formatu: `waies/jobname_driveid_timestamp_manifest.xml`.

 Można pobrać identyfikatora URI dysku kopii zapasowej hello manifesty zadania przez wywołanie hello hello [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_Get) operacji. Identyfikator URI jest zwracany w hello blob Hello `ManifestUri` właściwości dla każdego dysku.

## <a name="next-steps"></a>Następne kroki

* [Przy użyciu interfejsu API REST usługi Import/Eksport hello](storage-import-export-using-the-rest-api.md)
