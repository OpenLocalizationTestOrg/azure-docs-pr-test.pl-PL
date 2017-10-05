---
title: "Przykładów dla magazynu platformy Azure przy użyciu języka Java | Dokumentacja firmy Microsoft"
description: "Wyświetlanie, Pobierz i uruchom przykładowy kod i aplikacji usługi Azure Storage. Wykryj, wprowadzenie przykłady dla obiektów blob, kolejek, tabel i plików, za pomocą biblioteki klienta magazynu Java."
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
ms.openlocfilehash: 98e6022062b4ef5b5c71b54a0e94775b925d216b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="5fbf8-104">Przykładów dla magazynu platformy Azure przy użyciu języka Java</span><span class="sxs-lookup"><span data-stu-id="5fbf8-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="5fbf8-105">Indeks przykładów Java</span><span class="sxs-lookup"><span data-stu-id="5fbf8-105">Java sample index</span></span>

<span data-ttu-id="5fbf8-106">Poniższa tabela zawiera omówienie naszym repozytorium przykłady i scenariusze w każdej próbce.</span><span class="sxs-lookup"><span data-stu-id="5fbf8-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="5fbf8-107">Kliknij łącza, aby wyświetlić odpowiednie przykładowy kod w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="5fbf8-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="5fbf8-108">Endpoint</span><span class="sxs-lookup"><span data-stu-id="5fbf8-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="5fbf8-109">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="5fbf8-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="5fbf8-110">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="5fbf8-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="5fbf8-111"><b>Obiekt blob</b></span><span class="sxs-lookup"><span data-stu-id="5fbf8-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="5fbf8-112">Dołącz obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="5fbf8-112">Append Blob</span></span></td> 
<td><span data-ttu-id="5fbf8-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-114">Blokowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="5fbf8-114">Block Blob</span></span></td>
<td><span data-ttu-id="5fbf8-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-116">Szyfrowania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="5fbf8-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="5fbf8-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Wprowadzenie do korzystania z szyfrowania po stronie klienta usługi Azure w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-118">Kopiowanie obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="5fbf8-118">Copy Blob</span></span></td>
<td><span data-ttu-id="5fbf8-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-120">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="5fbf8-120">Create Container</span></span></td>
<td><span data-ttu-id="5fbf8-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-122">Usuwanie obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="5fbf8-122">Delete Blob</span></span></td>
<td><span data-ttu-id="5fbf8-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-124">Usunąć kontenera</span><span class="sxs-lookup"><span data-stu-id="5fbf8-124">Delete Container</span></span></td>
<td><span data-ttu-id="5fbf8-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-126">Obiekt blob metadane/właściwości/Stats</span><span class="sxs-lookup"><span data-stu-id="5fbf8-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="5fbf8-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-128">Kontener właściwości listy ACL/metadanych</span><span class="sxs-lookup"><span data-stu-id="5fbf8-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="5fbf8-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-130">Get zakresów stron</span><span class="sxs-lookup"><span data-stu-id="5fbf8-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="5fbf8-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Przykładowe testów stronicowych obiektów Blob</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-132">Kontener obiektów Blob dzierżawy</span><span class="sxs-lookup"><span data-stu-id="5fbf8-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="5fbf8-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-134">Kontener obiektów Blob listy</span><span class="sxs-lookup"><span data-stu-id="5fbf8-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="5fbf8-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-136">Stronicowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="5fbf8-136">Page Blob</span></span></td>
<td><span data-ttu-id="5fbf8-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="5fbf8-138">SYGNATURY DOSTĘPU WSPÓŁDZIELONEGO</span><span class="sxs-lookup"><span data-stu-id="5fbf8-138">SAS</span></span></td>
<td><span data-ttu-id="5fbf8-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Przykładowe testy SAS</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="5fbf8-140">Właściwości usługi</span><span class="sxs-lookup"><span data-stu-id="5fbf8-140">Service Properties</span></span></td>
<td><span data-ttu-id="5fbf8-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="5fbf8-142">Migawki obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="5fbf8-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="5fbf8-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="5fbf8-144"><b>Plik</b></span><span class="sxs-lookup"><span data-stu-id="5fbf8-144"><b>File</b></span></span></td>
<td><span data-ttu-id="5fbf8-145">Tworzenie plików/katalogów/udziałów</span><span class="sxs-lookup"><span data-stu-id="5fbf8-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="5fbf8-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="5fbf8-147">Usuwanie plików/katalogów/udziałów</span><span class="sxs-lookup"><span data-stu-id="5fbf8-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="5fbf8-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-149">Metadanych właściwości katalogów</span><span class="sxs-lookup"><span data-stu-id="5fbf8-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="5fbf8-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-151">Pobierz pliki</span><span class="sxs-lookup"><span data-stu-id="5fbf8-151">Download Files</span></span></td> 
<td><span data-ttu-id="5fbf8-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-153">Plik właściwości/metadanych/metryk</span><span class="sxs-lookup"><span data-stu-id="5fbf8-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="5fbf8-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-155">Właściwości usługi plików</span><span class="sxs-lookup"><span data-stu-id="5fbf8-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="5fbf8-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-157">Lista katalogów i plików</span><span class="sxs-lookup"><span data-stu-id="5fbf8-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="5fbf8-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="5fbf8-159">Listy udziałów</span><span class="sxs-lookup"><span data-stu-id="5fbf8-159">List Shares</span></span></td> 
<td><span data-ttu-id="5fbf8-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="5fbf8-161">Udostępnianie właściwości/metadanych/Stats</span><span class="sxs-lookup"><span data-stu-id="5fbf8-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="5fbf8-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Wprowadzenie do korzystania z usługi Azure plików w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="5fbf8-163"><b>Kolejki</b></span><span class="sxs-lookup"><span data-stu-id="5fbf8-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="5fbf8-164">Dodaj komunikat</span><span class="sxs-lookup"><span data-stu-id="5fbf8-164">Add Message</span></span></td> 
<td><span data-ttu-id="5fbf8-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Przykłady biblioteki klienta Java magazynu</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-166">Szyfrowania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="5fbf8-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="5fbf8-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Przykłady biblioteki klienta Java magazynu</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-168">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="5fbf8-168">Create Queues</span></span></td> 
<td><span data-ttu-id="5fbf8-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-170">Usuwanie kolejki/komunikatów</span><span class="sxs-lookup"><span data-stu-id="5fbf8-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="5fbf8-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-172">Wgląd do wiadomości</span><span class="sxs-lookup"><span data-stu-id="5fbf8-172">Peek Message</span></span></td> 
<td><span data-ttu-id="5fbf8-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-174">Kolejki ACL/metadanych/Stats</span><span class="sxs-lookup"><span data-stu-id="5fbf8-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="5fbf8-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-176">Właściwości usługi kolejki</span><span class="sxs-lookup"><span data-stu-id="5fbf8-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="5fbf8-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-178">Komunikat dotyczący aktualizacji</span><span class="sxs-lookup"><span data-stu-id="5fbf8-178">Update Message</span></span></td> 
<td><span data-ttu-id="5fbf8-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="5fbf8-180"><b>Tabela</b></span><span class="sxs-lookup"><span data-stu-id="5fbf8-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="5fbf8-181">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="5fbf8-181">Create Table</span></span></td> 
<td><span data-ttu-id="5fbf8-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Wprowadzenie do korzystania z usługi Azure tabel w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-183">Usuń jednostki/tabeli.</span><span class="sxs-lookup"><span data-stu-id="5fbf8-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="5fbf8-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Wprowadzenie do korzystania z usługi Azure tabel w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-185">Wstaw/Merge/zastępowania jednostki</span><span class="sxs-lookup"><span data-stu-id="5fbf8-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="5fbf8-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Przykłady biblioteki klienta Java magazynu</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-187">Zapytanie jednostek</span><span class="sxs-lookup"><span data-stu-id="5fbf8-187">Query Entities</span></span></td> 
<td><span data-ttu-id="5fbf8-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Wprowadzenie do korzystania z usługi Azure tabel w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-189">Tabele kwerendy</span><span class="sxs-lookup"><span data-stu-id="5fbf8-189">Query Tables</span></span></td> 
<td><span data-ttu-id="5fbf8-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Wprowadzenie do korzystania z usługi Azure tabel w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-191">Właściwości listy ACL tabeli</span><span class="sxs-lookup"><span data-stu-id="5fbf8-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="5fbf8-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Wprowadzenie do korzystania z usługi Azure tabel w języku Java</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="5fbf8-193">Aktualizowanie jednostek</span><span class="sxs-lookup"><span data-stu-id="5fbf8-193">Update Entity</span></span></td> 
<td><span data-ttu-id="5fbf8-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Przykłady biblioteki klienta Java magazynu</a></span><span class="sxs-lookup"><span data-stu-id="5fbf8-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="5fbf8-195">Biblioteka przykłady kodu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5fbf8-195">Azure Code Samples library</span></span>

<span data-ttu-id="5fbf8-196">Aby wyświetlić biblioteki kompletnego przykładu, przejdź do [przykłady kodu Azure](https://azure.microsoft.com/resources/samples/?service=storage) biblioteki, która zawiera przykłady dla usługi Azure Storage, który można pobrać i uruchom lokalnie.</span><span class="sxs-lookup"><span data-stu-id="5fbf8-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="5fbf8-197">Biblioteka przykładowy kod zawiera przykładowy kod w formacie zip.</span><span class="sxs-lookup"><span data-stu-id="5fbf8-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="5fbf8-198">Alternatywnie można wybrać i klonowania repozytorium GitHub dla każdej próbki.</span><span class="sxs-lookup"><span data-stu-id="5fbf8-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="5fbf8-199">Przewodniki z wprowadzeniem pobierania</span><span class="sxs-lookup"><span data-stu-id="5fbf8-199">Getting started guides</span></span>

<span data-ttu-id="5fbf8-200">Zapoznaj się z następujących przewodników, jeśli chcesz, aby uzyskać instrukcje dotyczące sposobu instalowania i rozpoczynanie pracy z biblioteki klienta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="5fbf8-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="5fbf8-201">Wprowadzenie do korzystania z usługi Azure Blob w języku Java</span><span class="sxs-lookup"><span data-stu-id="5fbf8-201">Getting Started with Azure Blob Service in Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="5fbf8-202">Wprowadzenie do korzystania z usługi Azure kolejek w języku Java</span><span class="sxs-lookup"><span data-stu-id="5fbf8-202">Getting Started with Azure Queue Service in Java</span></span>](storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="5fbf8-203">Wprowadzenie do korzystania z usługi Azure tabel w języku Java</span><span class="sxs-lookup"><span data-stu-id="5fbf8-203">Getting Started with Azure Table Service in Java</span></span>](storage-java-how-to-use-table-storage.md)
* [<span data-ttu-id="5fbf8-204">Wprowadzenie do korzystania z usługi Azure plików w języku Java</span><span class="sxs-lookup"><span data-stu-id="5fbf8-204">Getting Started with Azure File Service in Java</span></span>](storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="5fbf8-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5fbf8-205">Next steps</span></span>

<span data-ttu-id="5fbf8-206">Aby uzyskać informacje na próbkach dla innych języków:</span><span class="sxs-lookup"><span data-stu-id="5fbf8-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="5fbf8-207">.NET: [przykłady magazynu platformy azure przy użyciu platformy .NET](storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="5fbf8-207">.NET: [Azure Storage samples using .NET](storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="5fbf8-208">Wszystkie inne języki: [przykłady usługi Azure Storage](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="5fbf8-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
