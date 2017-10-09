---
title: "aaaUsing hello Azure narzędzie importu/eksportu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello narzędzie importu/eksportu tooprepare dyski twarde dla zadania importu naprawy zadania importu lub naprawy zadania eksportu."
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
ms.openlocfilehash: fa2021e5a03281128e494e6e63f58bc6319aeb4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-tool"></a><span data-ttu-id="487d9-103">Przy użyciu hello Azure narzędzie importu/eksportu</span><span class="sxs-lookup"><span data-stu-id="487d9-103">Using hello Azure Import/Export Tool</span></span> 

<span data-ttu-id="487d9-104">Hello Azure narzędzie importu/eksportu (WAImportExport.exe) jest używane toocreate zadania i zarządzać nimi w przypadku usługi Import/Eksport Azure hello włączenie tootransfer dużych ilości danych do i z magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="487d9-104">hello Azure Import/Export Tool (WAImportExport.exe) is used toocreate and manage jobs for hello Azure Import/Export service, enabling you tootransfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="487d9-105">Niniejsza dokumentacja jest do najnowszej wersji hello hello Azure narzędzie importu/eksportu.</span><span class="sxs-lookup"><span data-stu-id="487d9-105">This documentation is for hello most recent version of hello Azure Import/Export Tool.</span></span> <span data-ttu-id="487d9-106">Aby dowiedzieć się, jak za pomocą narzędzia v1 hello, zobacz [hello Using Azure narzędzie importu/eksportu v1](storage-import-export-tool-how-to-v1.md).</span><span class="sxs-lookup"><span data-stu-id="487d9-106">For information about using hello v1 tool, please see [Using hello Azure Import/Export Tool v1](storage-import-export-tool-how-to-v1.md).</span></span>

<span data-ttu-id="487d9-107">W tych artykułach zobaczysz, jak toouse hello narzędzia toodo hello następujące:</span><span class="sxs-lookup"><span data-stu-id="487d9-107">In these articles, you will see how toouse hello tool toodo hello following:</span></span>  

- <span data-ttu-id="487d9-108">Instalowanie i konfigurowanie hello narzędzie importu/eksportu.</span><span class="sxs-lookup"><span data-stu-id="487d9-108">Install and set up hello Import/Export Tool.</span></span>
- <span data-ttu-id="487d9-109">Przygotuj dyskach twardych dla zadania, w którym Importuj dane z Twojego tooAzure dyski magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="487d9-109">Prepare your hard drives for a job where you import data from your drives tooAzure Blob Storage.</span></span>
- <span data-ttu-id="487d9-110">Sprawdź stan hello zadania kopiowania plików dzienników.</span><span class="sxs-lookup"><span data-stu-id="487d9-110">Review hello status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="487d9-111">Napraw zadania importu.</span><span class="sxs-lookup"><span data-stu-id="487d9-111">Repair an import job.</span></span> 
- <span data-ttu-id="487d9-112">Napraw zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="487d9-112">Repair an export job.</span></span> 
- <span data-ttu-id="487d9-113">Rozwiązywanie problemów z hello Azure narzędzie importu/eksportu, w przypadku, gdy wystąpił problem podczas procesu.</span><span class="sxs-lookup"><span data-stu-id="487d9-113">Troubleshoot hello Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="487d9-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="487d9-114">Next steps</span></span>

* [<span data-ttu-id="487d9-115">Trwa konfigurowanie narzędzia WAImportExport hello</span><span class="sxs-lookup"><span data-stu-id="487d9-115">Setting up hello WAImportExport tool</span></span>](storage-import-export-tool-setup.md)
