---
title: "aaaTroubleshooting hello Azure narzędzie importu/eksportu | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat niektórych typowych problemów hello widoczne, używając hello narzędzie importu/eksportu Azure oraz w jaki sposób toohandle je."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 254439c15797862dded5d80028b8780ad163b2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a><span data-ttu-id="84777-103">Rozwiązywanie problemów z hello Azure narzędzie importu/eksportu</span><span class="sxs-lookup"><span data-stu-id="84777-103">Troubleshooting hello Azure Import/Export Tool</span></span>
<span data-ttu-id="84777-104">Hello narzędzia importu/eksportu pakietu Microsoft Azure zwraca komunikaty o błędach, gdy jest ono uruchomione na problemy.</span><span class="sxs-lookup"><span data-stu-id="84777-104">hello Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="84777-105">W tym temacie wymieniono niektóre typowe problemy, które użytkownicy mogą napotkać.</span><span class="sxs-lookup"><span data-stu-id="84777-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="84777-106">Kopiuj sesja nie powiedzie się, co należy zrobić?</span><span class="sxs-lookup"><span data-stu-id="84777-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="84777-107">W przypadku awarii sesji kopiowania dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="84777-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="84777-108">Jeśli hello Błąd powtarzający operację, na przykład jeśli udział sieciowy hello była w trybie offline, krótki okres, a teraz jest znowu w trybie online, możesz wznowić hello kopiowania sesji.</span><span class="sxs-lookup"><span data-stu-id="84777-108">If hello error is retryable, for example if hello network share was offline for a short period and now is back online, you can resume hello copy session.</span></span> <span data-ttu-id="84777-109">Błąd hello nie jest powtarzający operację, na przykład, jeśli określony katalog pliku nieprawidłowe źródło hello w hello parametry wiersza polecenia, należy najpierw tooabort hello kopiowania sesji.</span><span class="sxs-lookup"><span data-stu-id="84777-109">If hello error is not retryable, for example if you specified hello wrong source file directory in hello command line parameters, you need tooabort hello copy session.</span></span> <span data-ttu-id="84777-110">Zobacz [przygotowywanie dyski twarde dla zadania importu](../storage-import-export-tool-preparing-hard-drives-import-v1.md) uzyskać więcej informacji o wznawianie i przerywanie sesji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="84777-110">See [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="84777-111">I nie można wznowić lub przerwania sesji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="84777-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="84777-112">Jeśli sesja kopiowania hello jest hello pierwszej sesji kopii dysku, a następnie komunikat o błędzie hello powinny prezentować: "hello pierwszej sesji kopii nie można wznowić ani przerwane".</span><span class="sxs-lookup"><span data-stu-id="84777-112">If hello copy session is hello first copy session for a drive, then hello error message should state: "hello first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="84777-113">W takim przypadku można usunąć starego pliku dziennika hello i ponownie uruchom polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="84777-113">In this case, you can delete hello old journal file and rerun hello command.</span></span>  
  
 <span data-ttu-id="84777-114">Jeśli sesja kopiowania nie jest hello pierwszego dysku, można go zawsze wznowione lub zostało przerwane.</span><span class="sxs-lookup"><span data-stu-id="84777-114">If a copy session is not hello first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a><span data-ttu-id="84777-115">Utratą hello pliku dziennika, może nadal utworzyć zadanie hello?</span><span class="sxs-lookup"><span data-stu-id="84777-115">I lost hello journal file, can I still create hello job?</span></span>  
 <span data-ttu-id="84777-116">Hello plik dziennika dla dysku zawiera hello pełne informacje kopiowania danych toothis dysku i jest wymagane tooadd dysku toohello więcej plików i będą używane toocreate zadania importu.</span><span class="sxs-lookup"><span data-stu-id="84777-116">hello journal file for a drive contains hello complete information of copying data toothis drive, and it is needed tooadd more files toohello drive and will be used toocreate an import job.</span></span> <span data-ttu-id="84777-117">Jeśli plik dziennika hello zostaną utracone, konieczne będzie tooredo wszystkie sesje kopiowania hello hello dysku.</span><span class="sxs-lookup"><span data-stu-id="84777-117">If hello journal file is lost, you will have tooredo all hello copy sessions for hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="84777-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="84777-118">Next steps</span></span>
 
* [<span data-ttu-id="84777-119">Trwa konfigurowanie narzędzia importu/eksportu azure hello</span><span class="sxs-lookup"><span data-stu-id="84777-119">Setting up hello azure import/export tool</span></span>](../storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="84777-120">Przygotowywanie dysków twardych do zadania importu</span><span class="sxs-lookup"><span data-stu-id="84777-120">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="84777-121">Sprawdzanie stanu zadania za pomocą plików dziennika kopiowania</span><span class="sxs-lookup"><span data-stu-id="84777-121">Reviewing job status with copy log files</span></span>](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="84777-122">Naprawianie zadania importu</span><span class="sxs-lookup"><span data-stu-id="84777-122">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="84777-123">Naprawianie zadania eksportu</span><span class="sxs-lookup"><span data-stu-id="84777-123">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)
