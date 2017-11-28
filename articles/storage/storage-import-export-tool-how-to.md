---
title: "Za pomocą narzędzia importu/eksportu Azure | Dokumentacja firmy Microsoft"
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
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 86073f5d15253d658fcb371e913dd3a543a2b075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-tool"></a><span data-ttu-id="7015d-103">Za pomocą narzędzia Azure Import/Eksport</span><span class="sxs-lookup"><span data-stu-id="7015d-103">Using the Azure Import/Export Tool</span></span> 

<span data-ttu-id="7015d-104">Narzędzie importu/eksportu Azure (WAImportExport.exe) służy do tworzenia zadania i zarządzać nimi w usłudze Import/Eksport Azure umożliwia transfer dużych ilości danych do i z magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7015d-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="7015d-105">Niniejsza dokumentacja jest do najnowszej wersji narzędzia importu/eksportu Azure.</span><span class="sxs-lookup"><span data-stu-id="7015d-105">This documentation is for the most recent version of the Azure Import/Export Tool.</span></span> <span data-ttu-id="7015d-106">Aby dowiedzieć się, jak za pomocą narzędzia v1, zobacz [za pomocą narzędzia importu/eksportu Azure w wersji 1](storage-import-export-tool-how-to-v1.md).</span><span class="sxs-lookup"><span data-stu-id="7015d-106">For information about using the v1 tool, please see [Using the Azure Import/Export Tool v1](storage-import-export-tool-how-to-v1.md).</span></span>

<span data-ttu-id="7015d-107">W tych artykułach zostanie wyświetlony jak za pomocą narzędzia wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7015d-107">In these articles, you will see how to use the tool to do the following:</span></span>  

- <span data-ttu-id="7015d-108">Instalowanie i Konfigurowanie narzędzia importu/eksportu.</span><span class="sxs-lookup"><span data-stu-id="7015d-108">Install and set up the Import/Export Tool.</span></span>
- <span data-ttu-id="7015d-109">Przygotuj dyskach twardych dla zadania, w którym importowanie danych z dysków do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7015d-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="7015d-110">Sprawdź stan zadania kopiowania plików dzienników.</span><span class="sxs-lookup"><span data-stu-id="7015d-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="7015d-111">Napraw zadania importu.</span><span class="sxs-lookup"><span data-stu-id="7015d-111">Repair an import job.</span></span> 
- <span data-ttu-id="7015d-112">Napraw zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="7015d-112">Repair an export job.</span></span> 
- <span data-ttu-id="7015d-113">Rozwiązywanie problemów z narzędzie importu/eksportu Azure, w przypadku, gdy wystąpił problem podczas procesu.</span><span class="sxs-lookup"><span data-stu-id="7015d-113">Troubleshoot the Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7015d-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7015d-114">Next steps</span></span>

* [<span data-ttu-id="7015d-115">Trwa konfigurowanie narzędzia WAImportExport</span><span class="sxs-lookup"><span data-stu-id="7015d-115">Setting up the WAImportExport tool</span></span>](storage-import-export-tool-setup.md)