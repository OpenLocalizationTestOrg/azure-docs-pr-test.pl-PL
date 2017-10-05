---
title: "Tworzenie kopii zapasowej manifestów dysku Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak ma Twojej manifestów dysku dla kopii zapasowej automatycznie usługi Import/Eksport Microsoft Azure."
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
ms.openlocfilehash: 33eb8e1eea8f8aa7b79ef3e54f2b1ed88dc794ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="98d50-103">Tworzenie kopii zapasowej dysku manifesty prac Import/Eksport Azure</span><span class="sxs-lookup"><span data-stu-id="98d50-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="98d50-104">Manifesty dysku mogą być automatycznie do kopii zapasowej do obiektów blob przez ustawienie `BackupDriveManifest` właściwości `true` w [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) lub [właściwości zadania aktualizacji](/rest/api/storageimportexport/jobs#Jobs_Update) operacje interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="98d50-104">Drive manifests can be automatically backed up to blobs by setting the `BackupDriveManifest` property to `true` in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="98d50-105">Domyślnie manifestów dysku nie kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="98d50-105">By default, the drive manifests are not backed up.</span></span> <span data-ttu-id="98d50-106">Tworzenie kopii zapasowych manifestu dysku są przechowywane jako blokowych obiektów blob w kontenerze w ramach konta magazynu skojarzone z zadaniem.</span><span class="sxs-lookup"><span data-stu-id="98d50-106">The drive manifest backups are stored as block blobs in a container within the storage account associated with the job.</span></span> <span data-ttu-id="98d50-107">Domyślnie nazwa kontenera jest `waimportexport`, ale można określić inną nazwę w `DiagnosticsPath` właściwości podczas wywoływania metody `Put Job` lub `Update Job Properties` operacji.</span><span class="sxs-lookup"><span data-stu-id="98d50-107">By default, the container name is `waimportexport`, but you can specify a different name in the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="98d50-108">Kopia zapasowa manifestu obiektów blob są nazywane w następującym formacie: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="98d50-108">The backup manifest blob are named in the following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="98d50-109">Identyfikator URI manifesty kopii zapasowej dysku dla zadania można pobrać przez wywołanie metody [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_Get) operacji.</span><span class="sxs-lookup"><span data-stu-id="98d50-109">You can retrieve the URI of the backup drive manifests for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="98d50-110">Identyfikator URI jest zwracany w obiekcie blob `ManifestUri` właściwości dla każdego dysku.</span><span class="sxs-lookup"><span data-stu-id="98d50-110">The blob URI is returned in the `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98d50-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="98d50-111">Next steps</span></span>

* [<span data-ttu-id="98d50-112">Przy użyciu interfejsu API REST usługi Import/Eksport</span><span class="sxs-lookup"><span data-stu-id="98d50-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
