---
title: "Za pomocą narzędzia importu/eksportu Azure - v1 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przygotować dyski twarde dla zadania importu, napraw zadania importu lub naprawy zadania eksportu za pomocą narzędzia importu/eksportu."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f77535bb-d577-438a-bdd3-e15a82e0c543
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/15/2017
ms.author: muralikk
ms.openlocfilehash: 4ce2273cc0dcc456c2edc8c5dd2fc22496f20380
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-importexport-tool-classic-deployment-model"></a><span data-ttu-id="566f9-103">Za pomocą narzędzia importu/eksportu Azure (klasycznego modelu wdrażania)</span><span class="sxs-lookup"><span data-stu-id="566f9-103">Using the Azure Import/Export Tool (classic deployment model)</span></span>

<span data-ttu-id="566f9-104">Narzędzie importu/eksportu Azure (WAImportExport.exe) służy do tworzenia zadania i zarządzać nimi w usłudze Import/Eksport Azure umożliwia transfer dużych ilości danych do i z magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="566f9-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="566f9-105">Niniejsza dokumentacja jest dla klasycznym modelu wdrażania narzędzia importu/eksportu Azure.</span><span class="sxs-lookup"><span data-stu-id="566f9-105">This documentation is for the classic deployment model of the Azure Import/Export Tool.</span></span> <span data-ttu-id="566f9-106">Aby uzyskać informacje dotyczące korzystania z najnowszej wersji narzędzia, zobacz [za pomocą narzędzia importu/eksportu Azure](../storage-import-export-tool-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="566f9-106">For information about using the most recent version of the tool, see [Using the Azure Import/Export Tool](../storage-import-export-tool-how-to.md).</span></span>

<span data-ttu-id="566f9-107">Następujące artykuły przedstawia sposób do:</span><span class="sxs-lookup"><span data-stu-id="566f9-107">The following articles show you how to:</span></span>

- <span data-ttu-id="566f9-108">Instalowanie i Konfigurowanie narzędzia importu/eksportu.</span><span class="sxs-lookup"><span data-stu-id="566f9-108">Install and set up the Import/Export Tool.</span></span>
- <span data-ttu-id="566f9-109">Przygotuj dyskach twardych dla zadania, w którym importowanie danych z dysków do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="566f9-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="566f9-110">Sprawdź stan zadania kopiowania plików dzienników.</span><span class="sxs-lookup"><span data-stu-id="566f9-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="566f9-111">Napraw zadania importu.</span><span class="sxs-lookup"><span data-stu-id="566f9-111">Repair an import job.</span></span> 
- <span data-ttu-id="566f9-112">Napraw zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="566f9-112">Repair an export job.</span></span> 
- <span data-ttu-id="566f9-113">Rozwiązywanie problemów z narzędzie importu/eksportu Azure, w przypadku, gdy wystąpił problem podczas procesu.</span><span class="sxs-lookup"><span data-stu-id="566f9-113">Troubleshoot the Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="566f9-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="566f9-114">Next steps</span></span>

* [<span data-ttu-id="566f9-115">Trwa konfigurowanie narzędzia WAImportExport</span><span class="sxs-lookup"><span data-stu-id="566f9-115">Setting up the WAImportExport tool</span></span>](../storage-import-export-tool-how-to.md)