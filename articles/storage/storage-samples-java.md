---
title: "Przykłady magazynu aaaAzure przy użyciu języka Java | Dokumentacja firmy Microsoft"
description: "Wyświetlanie, Pobierz i uruchom przykładowy kod i aplikacji usługi Azure Storage. Wykryj, wprowadzenie przykłady dla obiektów blob, kolejek, tabel i plików, za pomocą biblioteki klienta magazynu Java hello."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: e3b8fbe86e82dd58c2a13a3c68760cbf6e9a6e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="e0637-104">Przykładów dla magazynu platformy Azure przy użyciu języka Java</span><span class="sxs-lookup"><span data-stu-id="e0637-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="e0637-105">Indeks przykładów Java</span><span class="sxs-lookup"><span data-stu-id="e0637-105">Java sample index</span></span>

<span data-ttu-id="e0637-106">Witaj Poniższa tabela zawiera omówienie nasze przykłady scenariuszy repozytorium i hello objęte każdej próbki.</span><span class="sxs-lookup"><span data-stu-id="e0637-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="e0637-107">Polecenie hello łącza tooview hello odpowiedniego przykładowy kod w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="e0637-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="e0637-108">Endpoint</span><span class="sxs-lookup"><span data-stu-id="e0637-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="e0637-109">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="e0637-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="e0637-110">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="e0637-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="e0637-111"><b>Obiekt blob</b></span><span class="sxs-lookup"><span data-stu-id="e0637-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="e0637-112">Dołącz obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="e0637-112">Append Blob</span></span></td> 
<td><span data-ttu-id="e0637-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-114">Blokowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="e0637-114">Block Blob</span></span></td>
<td><span data-ttu-id="e0637-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e0637-116">Szyfrowania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="e0637-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="e0637-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Wprowadzenie do korzystania z szyfrowania po stronie klienta usługi Azure w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e0637-118">Kopiowanie obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="e0637-118">Copy Blob</span></span></td>
<td><span data-ttu-id="e0637-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e0637-120">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="e0637-120">Create Container</span></span></td>
<td><span data-ttu-id="e0637-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e0637-122">Usuwanie obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="e0637-122">Delete Blob</span></span></td>
<td><span data-ttu-id="e0637-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e0637-124">Usunąć kontenera</span><span class="sxs-lookup"><span data-stu-id="e0637-124">Delete Container</span></span></td>
<td><span data-ttu-id="e0637-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e0637-126">Obiekt blob metadane/właściwości/Stats</span><span class="sxs-lookup"><span data-stu-id="e0637-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="e0637-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e0637-128">Kontener właściwości listy ACL/metadanych</span><span class="sxs-lookup"><span data-stu-id="e0637-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="e0637-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e0637-130">Get zakresów stron</span><span class="sxs-lookup"><span data-stu-id="e0637-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="e0637-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Przykładowe testów stronicowych obiektów Blob</a></span><span class="sxs-lookup"><span data-stu-id="e0637-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e0637-132">Kontener obiektów Blob dzierżawy</span><span class="sxs-lookup"><span data-stu-id="e0637-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="e0637-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e0637-134">Kontener obiektów Blob listy</span><span class="sxs-lookup"><span data-stu-id="e0637-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="e0637-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="e0637-136">Stronicowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="e0637-136">Page Blob</span></span></td>
<td><span data-ttu-id="e0637-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="e0637-138">SYGNATURY DOSTĘPU WSPÓŁDZIELONEGO</span><span class="sxs-lookup"><span data-stu-id="e0637-138">SAS</span></span></td>
<td><span data-ttu-id="e0637-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Przykładowe testy SAS</a></span><span class="sxs-lookup"><span data-stu-id="e0637-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="e0637-140">Właściwości usługi</span><span class="sxs-lookup"><span data-stu-id="e0637-140">Service Properties</span></span></td>
<td><span data-ttu-id="e0637-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="e0637-142">Migawki obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="e0637-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="e0637-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="e0637-144"><b>Plik</b></span><span class="sxs-lookup"><span data-stu-id="e0637-144"><b>File</b></span></span></td>
<td><span data-ttu-id="e0637-145">Tworzenie plików/katalogów/udziałów</span><span class="sxs-lookup"><span data-stu-id="e0637-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="e0637-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="e0637-147">Usuwanie plików/katalogów/udziałów</span><span class="sxs-lookup"><span data-stu-id="e0637-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="e0637-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-149">Metadanych właściwości katalogów</span><span class="sxs-lookup"><span data-stu-id="e0637-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="e0637-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-151">Pobierz pliki</span><span class="sxs-lookup"><span data-stu-id="e0637-151">Download Files</span></span></td> 
<td><span data-ttu-id="e0637-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-153">Plik właściwości/metadanych/metryk</span><span class="sxs-lookup"><span data-stu-id="e0637-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="e0637-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-155">Właściwości usługi plików</span><span class="sxs-lookup"><span data-stu-id="e0637-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="e0637-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-157">Lista katalogów i plików</span><span class="sxs-lookup"><span data-stu-id="e0637-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="e0637-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="e0637-159">Listy udziałów</span><span class="sxs-lookup"><span data-stu-id="e0637-159">List Shares</span></span></td> 
<td><span data-ttu-id="e0637-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="e0637-161">Udostępnianie właściwości/metadanych/Stats</span><span class="sxs-lookup"><span data-stu-id="e0637-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="e0637-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="e0637-163"><b>Kolejki</b></span><span class="sxs-lookup"><span data-stu-id="e0637-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="e0637-164">Dodaj komunikat</span><span class="sxs-lookup"><span data-stu-id="e0637-164">Add Message</span></span></td> 
<td><span data-ttu-id="e0637-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Przykłady biblioteki klienta Java magazynu</a></span><span class="sxs-lookup"><span data-stu-id="e0637-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-166">Szyfrowania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="e0637-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="e0637-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Przykłady biblioteki klienta Java magazynu</a></span><span class="sxs-lookup"><span data-stu-id="e0637-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-168">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="e0637-168">Create Queues</span></span></td> 
<td><span data-ttu-id="e0637-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-170">Usuwanie kolejki/komunikatów</span><span class="sxs-lookup"><span data-stu-id="e0637-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="e0637-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-172">Wgląd do wiadomości</span><span class="sxs-lookup"><span data-stu-id="e0637-172">Peek Message</span></span></td> 
<td><span data-ttu-id="e0637-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-174">Kolejki ACL/metadanych/Stats</span><span class="sxs-lookup"><span data-stu-id="e0637-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="e0637-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-176">Właściwości usługi kolejki</span><span class="sxs-lookup"><span data-stu-id="e0637-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="e0637-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-178">Komunikat dotyczący aktualizacji</span><span class="sxs-lookup"><span data-stu-id="e0637-178">Update Message</span></span></td> 
<td><span data-ttu-id="e0637-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="e0637-180"><b>Tabela</b></span><span class="sxs-lookup"><span data-stu-id="e0637-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="e0637-181">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="e0637-181">Create Table</span></span></td> 
<td><span data-ttu-id="e0637-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Wprowadzenie do korzystania z usługi Azure tabel w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-183">Usuń jednostki/tabeli.</span><span class="sxs-lookup"><span data-stu-id="e0637-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="e0637-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Wprowadzenie do korzystania z usługi Azure tabel w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-185">Wstaw/Merge/zastępowania jednostki</span><span class="sxs-lookup"><span data-stu-id="e0637-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="e0637-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Przykłady biblioteki klienta Java magazynu</a></span><span class="sxs-lookup"><span data-stu-id="e0637-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-187">Zapytanie jednostek</span><span class="sxs-lookup"><span data-stu-id="e0637-187">Query Entities</span></span></td> 
<td><span data-ttu-id="e0637-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Wprowadzenie do korzystania z usługi Azure tabel w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-189">Tabele kwerendy</span><span class="sxs-lookup"><span data-stu-id="e0637-189">Query Tables</span></span></td> 
<td><span data-ttu-id="e0637-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Wprowadzenie do korzystania z usługi Azure tabel w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-191">Właściwości listy ACL tabeli</span><span class="sxs-lookup"><span data-stu-id="e0637-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="e0637-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Wprowadzenie do korzystania z usługi Azure tabel w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="e0637-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="e0637-193">Aktualizowanie jednostek</span><span class="sxs-lookup"><span data-stu-id="e0637-193">Update Entity</span></span></td> 
<td><span data-ttu-id="e0637-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Przykłady biblioteki klienta Java magazynu</a></span><span class="sxs-lookup"><span data-stu-id="e0637-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="e0637-195">Biblioteka przykłady kodu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e0637-195">Azure Code Samples library</span></span>

<span data-ttu-id="e0637-196">tooview hello kompletnego przykładu biblioteki, przejdź toohello [przykłady kodu Azure](https://azure.microsoft.com/resources/samples/?service=storage) biblioteki, która zawiera przykłady dla usługi Azure Storage, który można pobrać i uruchom lokalnie.</span><span class="sxs-lookup"><span data-stu-id="e0637-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="e0637-197">Witaj biblioteki przykładowy kod zawiera przykładowy kod w formacie zip.</span><span class="sxs-lookup"><span data-stu-id="e0637-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="e0637-198">Alternatywnie można wybrać i klonowania repozytorium GitHub powitania dla każdej próbki.</span><span class="sxs-lookup"><span data-stu-id="e0637-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="e0637-199">Przewodniki z wprowadzeniem pobierania</span><span class="sxs-lookup"><span data-stu-id="e0637-199">Getting started guides</span></span>

<span data-ttu-id="e0637-200">Zapoznaj się z powitania po przewodnikach, jeśli chcesz, aby uzyskać instrukcje dotyczące tooinstall i rozpoczynanie pracy z hello biblioteki klienta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e0637-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="e0637-201">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</span><span class="sxs-lookup"><span data-stu-id="e0637-201">Getting Started with Azure Blob Service in Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="e0637-202">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</span><span class="sxs-lookup"><span data-stu-id="e0637-202">Getting Started with Azure Queue Service in Java</span></span>](storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="e0637-203">Wprowadzenie do korzystania z usługi Azure tabel w języku Java</span><span class="sxs-lookup"><span data-stu-id="e0637-203">Getting Started with Azure Table Service in Java</span></span>](storage-java-how-to-use-table-storage.md)
* [<span data-ttu-id="e0637-204">Wprowadzenie do korzystania z usługi Azure plików w języku Java</span><span class="sxs-lookup"><span data-stu-id="e0637-204">Getting Started with Azure File Service in Java</span></span>](storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="e0637-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0637-205">Next steps</span></span>

<span data-ttu-id="e0637-206">Aby uzyskać informacje na próbkach dla innych języków:</span><span class="sxs-lookup"><span data-stu-id="e0637-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="e0637-207">.NET: [przykłady magazynu platformy azure przy użyciu platformy .NET](storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="e0637-207">.NET: [Azure Storage samples using .NET](storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="e0637-208">Wszystkie inne języki: [przykłady usługi Azure Storage](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="e0637-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
