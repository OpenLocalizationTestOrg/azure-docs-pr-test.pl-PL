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
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="65fdc-103">Tworzenie kopii zapasowej dysku manifesty prac Import/Eksport Azure</span><span class="sxs-lookup"><span data-stu-id="65fdc-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="65fdc-104">Manifesty dysku może automatycznie kopii zapasowej tooblobs przez ustawienie hello `BackupDriveManifest` właściwości zbyt`true` w hello [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) lub [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) operacje interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="65fdc-104">Drive manifests can be automatically backed up tooblobs by setting hello `BackupDriveManifest` property too`true` in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="65fdc-105">Domyślnie program hello dysku manifestów nie kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="65fdc-105">By default, hello drive manifests are not backed up.</span></span> <span data-ttu-id="65fdc-106">Witaj dysku manifestu w kopie zapasowe są przechowywane jako blokowych obiektów blob w kontenerze w ramach konta magazynu hello skojarzone z zadaniem hello.</span><span class="sxs-lookup"><span data-stu-id="65fdc-106">hello drive manifest backups are stored as block blobs in a container within hello storage account associated with hello job.</span></span> <span data-ttu-id="65fdc-107">Domyślnie nazwa kontenera hello jest `waimportexport`, można jednak określić inną nazwę w hello `DiagnosticsPath` właściwości podczas wywoływania metody hello `Put Job` lub `Update Job Properties` operacji.</span><span class="sxs-lookup"><span data-stu-id="65fdc-107">By default, hello container name is `waimportexport`, but you can specify a different name in hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="65fdc-108">Witaj kopii zapasowej manifestu obiektów blob są o nazwie w hello następującego formatu: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="65fdc-108">hello backup manifest blob are named in hello following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="65fdc-109">Można pobrać identyfikatora URI dysku kopii zapasowej hello manifesty zadania przez wywołanie hello hello [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_Get) operacji.</span><span class="sxs-lookup"><span data-stu-id="65fdc-109">You can retrieve hello URI of hello backup drive manifests for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="65fdc-110">Identyfikator URI jest zwracany w hello blob Hello `ManifestUri` właściwości dla każdego dysku.</span><span class="sxs-lookup"><span data-stu-id="65fdc-110">hello blob URI is returned in hello `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65fdc-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="65fdc-111">Next steps</span></span>

* [<span data-ttu-id="65fdc-112">Przy użyciu interfejsu API REST usługi Import/Eksport hello</span><span class="sxs-lookup"><span data-stu-id="65fdc-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
