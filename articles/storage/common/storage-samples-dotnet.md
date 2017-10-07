---
title: "Przykłady magazynu aaaAzure przy użyciu platformy .NET | Dokumentacja firmy Microsoft"
description: "Wyświetlanie, Pobierz i uruchom przykładowy kod i aplikacji usługi Azure Storage. Wykryj, wprowadzenie przykłady dla obiektów blob, kolejek, tabel i plików, za pomocą biblioteki klienta magazynu .NET hello."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 6b02b596f77845fc5fa474fa235c2b5df6e94ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="c642a-104">Przykładów dla magazynu platformy Azure przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="c642a-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="c642a-105">Indeks przykładów .NET</span><span class="sxs-lookup"><span data-stu-id="c642a-105">.NET sample index</span></span>

<span data-ttu-id="c642a-106">Witaj Poniższa tabela zawiera omówienie nasze przykłady scenariuszy repozytorium i hello objęte każdej próbki.</span><span class="sxs-lookup"><span data-stu-id="c642a-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="c642a-107">Polecenie hello łącza tooview hello odpowiedniego przykładowy kod w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="c642a-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="c642a-108">Endpoint</span><span class="sxs-lookup"><span data-stu-id="c642a-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="c642a-109">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="c642a-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="c642a-110">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="c642a-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="c642a-111"><b>Obiekt blob</b></span><span class="sxs-lookup"><span data-stu-id="c642a-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="c642a-112">Dołącz obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="c642a-112">Append Blob</span></span></td> 
<td><span data-ttu-id="c642a-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Przykład CloudBlobContainer.GetAppendBlobReference — metoda</a></span><span class="sxs-lookup"><span data-stu-id="c642a-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-114">Blokowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="c642a-114">Block Blob</span></span></td>
<td><span data-ttu-id="c642a-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Galeria fotografii magazynu obiektów Blob Azure aplikacji sieci Web</a></span><span class="sxs-lookup"><span data-stu-id="c642a-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c642a-116">Szyfrowania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="c642a-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="c642a-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Przykłady szyfrowania obiektów blob</a></span><span class="sxs-lookup"><span data-stu-id="c642a-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c642a-118">Kopiowanie obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="c642a-118">Copy Blob</span></span></td>
<td><span data-ttu-id="c642a-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="c642a-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c642a-120">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="c642a-120">Create Container</span></span></td>
<td><span data-ttu-id="c642a-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Galeria fotografii magazynu obiektów Blob Azure aplikacji sieci Web</a></span><span class="sxs-lookup"><span data-stu-id="c642a-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c642a-122">Usuwanie obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="c642a-122">Delete Blob</span></span></td>
<td><span data-ttu-id="c642a-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Galeria fotografii magazynu obiektów Blob Azure aplikacji sieci Web</a></span><span class="sxs-lookup"><span data-stu-id="c642a-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c642a-124">Usunąć kontenera</span><span class="sxs-lookup"><span data-stu-id="c642a-124">Delete Container</span></span></td>
<td><span data-ttu-id="c642a-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="c642a-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c642a-126">Obiekt blob metadane/właściwości/Stats</span><span class="sxs-lookup"><span data-stu-id="c642a-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="c642a-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="c642a-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c642a-128">Kontener właściwości listy ACL/metadanych</span><span class="sxs-lookup"><span data-stu-id="c642a-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="c642a-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Galeria fotografii magazynu obiektów Blob Azure aplikacji sieci Web</a></span><span class="sxs-lookup"><span data-stu-id="c642a-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c642a-130">Get zakresów stron</span><span class="sxs-lookup"><span data-stu-id="c642a-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="c642a-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="c642a-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c642a-132">Kontener obiektów Blob dzierżawy</span><span class="sxs-lookup"><span data-stu-id="c642a-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="c642a-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="c642a-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c642a-134">Kontener obiektów Blob listy</span><span class="sxs-lookup"><span data-stu-id="c642a-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="c642a-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="c642a-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c642a-136">Stronicowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="c642a-136">Page Blob</span></span></td>
<td><span data-ttu-id="c642a-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="c642a-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="c642a-138">SYGNATURY DOSTĘPU WSPÓŁDZIELONEGO</span><span class="sxs-lookup"><span data-stu-id="c642a-138">SAS</span></span></td>
<td><span data-ttu-id="c642a-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="c642a-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="c642a-140">Właściwości usługi</span><span class="sxs-lookup"><span data-stu-id="c642a-140">Service Properties</span></span></td>
<td><span data-ttu-id="c642a-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="c642a-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="c642a-142">Migawki obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="c642a-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="c642a-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Dysków kopii zapasowej maszyny wirtualnej platformy Azure przy użyciu przyrostowej migawki</a></span><span class="sxs-lookup"><span data-stu-id="c642a-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="c642a-144"><b>Plik</b></span><span class="sxs-lookup"><span data-stu-id="c642a-144"><b>File</b></span></span></td>
<td><span data-ttu-id="c642a-145">Tworzenie plików/katalogów/udziałów</span><span class="sxs-lookup"><span data-stu-id="c642a-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="c642a-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="c642a-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="c642a-147">Usuwanie plików/katalogów/udziałów</span><span class="sxs-lookup"><span data-stu-id="c642a-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="c642a-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Wprowadzenie do korzystania z usługi plików na platformę Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="c642a-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-149">Metadanych właściwości katalogów</span><span class="sxs-lookup"><span data-stu-id="c642a-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="c642a-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="c642a-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-151">Pobierz pliki</span><span class="sxs-lookup"><span data-stu-id="c642a-151">Download Files</span></span></td> 
<td><span data-ttu-id="c642a-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="c642a-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-153">Plik właściwości/metadanych/metryk</span><span class="sxs-lookup"><span data-stu-id="c642a-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="c642a-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="c642a-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-155">Właściwości usługi plików</span><span class="sxs-lookup"><span data-stu-id="c642a-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="c642a-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="c642a-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-157">Lista katalogów i plików</span><span class="sxs-lookup"><span data-stu-id="c642a-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="c642a-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="c642a-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="c642a-159">Listy udziałów</span><span class="sxs-lookup"><span data-stu-id="c642a-159">List Shares</span></span></td> 
<td><span data-ttu-id="c642a-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="c642a-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="c642a-161">Udostępnianie właściwości/metadanych/Stats</span><span class="sxs-lookup"><span data-stu-id="c642a-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="c642a-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="c642a-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="c642a-163"><b>Kolejki</b></span><span class="sxs-lookup"><span data-stu-id="c642a-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="c642a-164">Dodaj komunikat</span><span class="sxs-lookup"><span data-stu-id="c642a-164">Add Message</span></span></td> 
<td><span data-ttu-id="c642a-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="c642a-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-166">Szyfrowania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="c642a-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="c642a-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Szyfrowanie po stronie klienta kolejki .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="c642a-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-168">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="c642a-168">Create Queues</span></span></td> 
<td><span data-ttu-id="c642a-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="c642a-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-170">Usuwanie kolejki/komunikatów</span><span class="sxs-lookup"><span data-stu-id="c642a-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="c642a-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="c642a-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-172">Wgląd do wiadomości</span><span class="sxs-lookup"><span data-stu-id="c642a-172">Peek Message</span></span></td> 
<td><span data-ttu-id="c642a-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="c642a-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-174">Kolejki ACL/metadanych/Stats</span><span class="sxs-lookup"><span data-stu-id="c642a-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="c642a-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="c642a-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-176">Właściwości usługi kolejki</span><span class="sxs-lookup"><span data-stu-id="c642a-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="c642a-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="c642a-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-178">Komunikat dotyczący aktualizacji</span><span class="sxs-lookup"><span data-stu-id="c642a-178">Update Message</span></span></td> 
<td><span data-ttu-id="c642a-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="c642a-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="c642a-180"><b>Tabela</b></span><span class="sxs-lookup"><span data-stu-id="c642a-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="c642a-181">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="c642a-181">Create Table</span></span></td> 
<td><span data-ttu-id="c642a-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Zarządzanie za pomocą usługi Azure Storage — Przykładowa aplikacja współbieżności</a></span><span class="sxs-lookup"><span data-stu-id="c642a-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-183">Usuń jednostki/tabeli.</span><span class="sxs-lookup"><span data-stu-id="c642a-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="c642a-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Rozpoczynanie pracy z usługą Azure Table Storage na platformie .NET</a></span><span class="sxs-lookup"><span data-stu-id="c642a-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-185">Wstaw/Merge/zastępowania jednostki</span><span class="sxs-lookup"><span data-stu-id="c642a-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="c642a-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Zarządzanie za pomocą usługi Azure Storage — Przykładowa aplikacja współbieżności</a></span><span class="sxs-lookup"><span data-stu-id="c642a-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-187">Zapytanie jednostek</span><span class="sxs-lookup"><span data-stu-id="c642a-187">Query Entities</span></span></td> 
<td><span data-ttu-id="c642a-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Rozpoczynanie pracy z usługą Azure Table Storage na platformie .NET</a></span><span class="sxs-lookup"><span data-stu-id="c642a-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-189">Tabele kwerendy</span><span class="sxs-lookup"><span data-stu-id="c642a-189">Query Tables</span></span></td> 
<td><span data-ttu-id="c642a-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Rozpoczynanie pracy z usługą Azure Table Storage na platformie .NET</a></span><span class="sxs-lookup"><span data-stu-id="c642a-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-191">Właściwości listy ACL tabeli</span><span class="sxs-lookup"><span data-stu-id="c642a-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="c642a-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Rozpoczynanie pracy z usługą Azure Table Storage na platformie .NET</a></span><span class="sxs-lookup"><span data-stu-id="c642a-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c642a-193">Aktualizowanie jednostek</span><span class="sxs-lookup"><span data-stu-id="c642a-193">Update Entity</span></span></td> 
<td><span data-ttu-id="c642a-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Zarządzanie za pomocą usługi Azure Storage — Przykładowa aplikacja współbieżności</a></span><span class="sxs-lookup"><span data-stu-id="c642a-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="c642a-195">Biblioteka przykłady kodu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c642a-195">Azure Code Samples library</span></span>

<span data-ttu-id="c642a-196">tooview hello kompletnego przykładu biblioteki, przejdź toohello [przykłady kodu Azure](https://azure.microsoft.com/resources/samples/?service=storage) biblioteki, która zawiera przykłady dla usługi Azure Storage, który można pobrać i uruchom lokalnie.</span><span class="sxs-lookup"><span data-stu-id="c642a-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="c642a-197">Witaj biblioteki przykładowy kod zawiera przykładowy kod w formacie zip.</span><span class="sxs-lookup"><span data-stu-id="c642a-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="c642a-198">Alternatywnie można wybrać i klonowania repozytorium GitHub powitania dla każdej próbki.</span><span class="sxs-lookup"><span data-stu-id="c642a-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="c642a-199">Przewodniki z wprowadzeniem pobierania</span><span class="sxs-lookup"><span data-stu-id="c642a-199">Getting started guides</span></span>

<span data-ttu-id="c642a-200">Zapoznaj się z powitania po przewodnikach, jeśli chcesz, aby uzyskać instrukcje dotyczące tooinstall i rozpoczynanie pracy z hello biblioteki klienta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="c642a-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="c642a-201">Wprowadzenie do korzystania z usługi obiektów Blob platformy Azure w .NET</span><span class="sxs-lookup"><span data-stu-id="c642a-201">Getting Started with Azure Blob Service in .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="c642a-202">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</span><span class="sxs-lookup"><span data-stu-id="c642a-202">Getting Started with Azure Queue Service in .NET</span></span>](../storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="c642a-203">Wprowadzenie do korzystania z usługi tabeli platformy Azure w .NET</span><span class="sxs-lookup"><span data-stu-id="c642a-203">Getting Started with Azure Table Service in .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="c642a-204">Wprowadzenie do korzystania z usługi plików na platformę Azure w .NET</span><span class="sxs-lookup"><span data-stu-id="c642a-204">Getting Started with Azure File Service in .NET</span></span>](../storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="c642a-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c642a-205">Next steps</span></span>

<span data-ttu-id="c642a-206">Aby uzyskać informacje na próbkach dla innych języków:</span><span class="sxs-lookup"><span data-stu-id="c642a-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="c642a-207">Java: [przykłady magazynu platformy Azure przy użyciu języka Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="c642a-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="c642a-208">Wszystkie inne języki: [przykłady usługi Azure Storage](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="c642a-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
