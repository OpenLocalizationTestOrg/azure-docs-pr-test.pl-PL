---
title: "Przykładów dla magazynu platformy Azure przy użyciu platformy .NET | Dokumentacja firmy Microsoft"
description: "Wyświetlanie, Pobierz i uruchom przykładowy kod i aplikacji usługi Azure Storage. Wykryj, wprowadzenie przykłady dla obiektów blob, kolejek, tabel i plików, za pomocą biblioteki klienta magazynu .NET."
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
ms.openlocfilehash: d2b6b3d9483f230ad25ae47255a4f28c1a67e064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="bbd7c-104">Przykładów dla magazynu platformy Azure przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="bbd7c-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="bbd7c-105">Indeks przykładów .NET</span><span class="sxs-lookup"><span data-stu-id="bbd7c-105">.NET sample index</span></span>

<span data-ttu-id="bbd7c-106">Poniższa tabela zawiera omówienie naszym repozytorium przykłady i scenariusze w każdej próbce.</span><span class="sxs-lookup"><span data-stu-id="bbd7c-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="bbd7c-107">Kliknij łącza, aby wyświetlić odpowiednie przykładowy kod w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="bbd7c-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="bbd7c-108">Endpoint</span><span class="sxs-lookup"><span data-stu-id="bbd7c-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="bbd7c-109">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="bbd7c-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="bbd7c-110">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="bbd7c-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="bbd7c-111"><b>Obiekt blob</b></span><span class="sxs-lookup"><span data-stu-id="bbd7c-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="bbd7c-112">Dołącz obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="bbd7c-112">Append Blob</span></span></td> 
<td><span data-ttu-id="bbd7c-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Przykład CloudBlobContainer.GetAppendBlobReference — metoda</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-114">Blokowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="bbd7c-114">Block Blob</span></span></td>
<td><span data-ttu-id="bbd7c-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Galeria fotografii magazynu obiektów Blob Azure aplikacji sieci Web</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-116">Szyfrowania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="bbd7c-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="bbd7c-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Przykłady szyfrowania obiektów blob</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-118">Kopiowanie obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="bbd7c-118">Copy Blob</span></span></td>
<td><span data-ttu-id="bbd7c-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-120">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="bbd7c-120">Create Container</span></span></td>
<td><span data-ttu-id="bbd7c-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Galeria fotografii magazynu obiektów Blob Azure aplikacji sieci Web</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-122">Usuwanie obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="bbd7c-122">Delete Blob</span></span></td>
<td><span data-ttu-id="bbd7c-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Galeria fotografii magazynu obiektów Blob Azure aplikacji sieci Web</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-124">Usunąć kontenera</span><span class="sxs-lookup"><span data-stu-id="bbd7c-124">Delete Container</span></span></td>
<td><span data-ttu-id="bbd7c-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-126">Obiekt blob metadane/właściwości/Stats</span><span class="sxs-lookup"><span data-stu-id="bbd7c-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="bbd7c-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-128">Kontener właściwości listy ACL/metadanych</span><span class="sxs-lookup"><span data-stu-id="bbd7c-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="bbd7c-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Galeria fotografii magazynu obiektów Blob Azure aplikacji sieci Web</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-130">Get zakresów stron</span><span class="sxs-lookup"><span data-stu-id="bbd7c-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="bbd7c-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-132">Kontener obiektów Blob dzierżawy</span><span class="sxs-lookup"><span data-stu-id="bbd7c-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="bbd7c-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-134">Kontener obiektów Blob listy</span><span class="sxs-lookup"><span data-stu-id="bbd7c-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="bbd7c-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-136">Stronicowych obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="bbd7c-136">Page Blob</span></span></td>
<td><span data-ttu-id="bbd7c-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="bbd7c-138">SYGNATURY DOSTĘPU WSPÓŁDZIELONEGO</span><span class="sxs-lookup"><span data-stu-id="bbd7c-138">SAS</span></span></td>
<td><span data-ttu-id="bbd7c-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="bbd7c-140">Właściwości usługi</span><span class="sxs-lookup"><span data-stu-id="bbd7c-140">Service Properties</span></span></td>
<td><span data-ttu-id="bbd7c-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Rozpoczynanie pracy z obiektami blob</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="bbd7c-142">Migawki obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="bbd7c-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="bbd7c-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Dysków kopii zapasowej maszyny wirtualnej platformy Azure przy użyciu przyrostowej migawki</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="bbd7c-144"><b>Plik</b></span><span class="sxs-lookup"><span data-stu-id="bbd7c-144"><b>File</b></span></span></td>
<td><span data-ttu-id="bbd7c-145">Tworzenie plików/katalogów/udziałów</span><span class="sxs-lookup"><span data-stu-id="bbd7c-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="bbd7c-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="bbd7c-147">Usuwanie plików/katalogów/udziałów</span><span class="sxs-lookup"><span data-stu-id="bbd7c-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="bbd7c-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Wprowadzenie do korzystania z usługi plików na platformę Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-149">Metadanych właściwości katalogów</span><span class="sxs-lookup"><span data-stu-id="bbd7c-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="bbd7c-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-151">Pobierz pliki</span><span class="sxs-lookup"><span data-stu-id="bbd7c-151">Download Files</span></span></td> 
<td><span data-ttu-id="bbd7c-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-153">Plik właściwości/metadanych/metryk</span><span class="sxs-lookup"><span data-stu-id="bbd7c-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="bbd7c-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-155">Właściwości usługi plików</span><span class="sxs-lookup"><span data-stu-id="bbd7c-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="bbd7c-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-157">Lista katalogów i plików</span><span class="sxs-lookup"><span data-stu-id="bbd7c-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="bbd7c-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="bbd7c-159">Listy udziałów</span><span class="sxs-lookup"><span data-stu-id="bbd7c-159">List Shares</span></span></td> 
<td><span data-ttu-id="bbd7c-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="bbd7c-161">Udostępnianie właściwości/metadanych/Stats</span><span class="sxs-lookup"><span data-stu-id="bbd7c-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="bbd7c-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Przykładowe magazynu plików .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="bbd7c-163"><b>Kolejki</b></span><span class="sxs-lookup"><span data-stu-id="bbd7c-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="bbd7c-164">Dodaj komunikat</span><span class="sxs-lookup"><span data-stu-id="bbd7c-164">Add Message</span></span></td> 
<td><span data-ttu-id="bbd7c-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-166">Szyfrowania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="bbd7c-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="bbd7c-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Szyfrowanie po stronie klienta kolejki .NET usługi Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-168">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="bbd7c-168">Create Queues</span></span></td> 
<td><span data-ttu-id="bbd7c-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-170">Usuwanie kolejki/komunikatów</span><span class="sxs-lookup"><span data-stu-id="bbd7c-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="bbd7c-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-172">Wgląd do wiadomości</span><span class="sxs-lookup"><span data-stu-id="bbd7c-172">Peek Message</span></span></td> 
<td><span data-ttu-id="bbd7c-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-174">Kolejki ACL/metadanych/Stats</span><span class="sxs-lookup"><span data-stu-id="bbd7c-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="bbd7c-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-176">Właściwości usługi kolejki</span><span class="sxs-lookup"><span data-stu-id="bbd7c-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="bbd7c-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-178">Komunikat dotyczący aktualizacji</span><span class="sxs-lookup"><span data-stu-id="bbd7c-178">Update Message</span></span></td> 
<td><span data-ttu-id="bbd7c-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="bbd7c-180"><b>Tabela</b></span><span class="sxs-lookup"><span data-stu-id="bbd7c-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="bbd7c-181">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="bbd7c-181">Create Table</span></span></td> 
<td><span data-ttu-id="bbd7c-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Zarządzanie za pomocą usługi Azure Storage — Przykładowa aplikacja współbieżności</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-183">Usuń jednostki/tabeli.</span><span class="sxs-lookup"><span data-stu-id="bbd7c-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="bbd7c-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Rozpoczynanie pracy z usługą Azure Table Storage na platformie .NET</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-185">Wstaw/Merge/zastępowania jednostki</span><span class="sxs-lookup"><span data-stu-id="bbd7c-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="bbd7c-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Zarządzanie za pomocą usługi Azure Storage — Przykładowa aplikacja współbieżności</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-187">Zapytanie jednostek</span><span class="sxs-lookup"><span data-stu-id="bbd7c-187">Query Entities</span></span></td> 
<td><span data-ttu-id="bbd7c-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Rozpoczynanie pracy z usługą Azure Table Storage na platformie .NET</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-189">Tabele kwerendy</span><span class="sxs-lookup"><span data-stu-id="bbd7c-189">Query Tables</span></span></td> 
<td><span data-ttu-id="bbd7c-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Rozpoczynanie pracy z usługą Azure Table Storage na platformie .NET</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-191">Właściwości listy ACL tabeli</span><span class="sxs-lookup"><span data-stu-id="bbd7c-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="bbd7c-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Rozpoczynanie pracy z usługą Azure Table Storage na platformie .NET</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="bbd7c-193">Aktualizowanie jednostek</span><span class="sxs-lookup"><span data-stu-id="bbd7c-193">Update Entity</span></span></td> 
<td><span data-ttu-id="bbd7c-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Zarządzanie za pomocą usługi Azure Storage — Przykładowa aplikacja współbieżności</a></span><span class="sxs-lookup"><span data-stu-id="bbd7c-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="bbd7c-195">Biblioteka przykłady kodu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bbd7c-195">Azure Code Samples library</span></span>

<span data-ttu-id="bbd7c-196">Aby wyświetlić biblioteki kompletnego przykładu, przejdź do [przykłady kodu Azure](https://azure.microsoft.com/resources/samples/?service=storage) biblioteki, która zawiera przykłady dla usługi Azure Storage, który można pobrać i uruchom lokalnie.</span><span class="sxs-lookup"><span data-stu-id="bbd7c-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="bbd7c-197">Biblioteka przykładowy kod zawiera przykładowy kod w formacie zip.</span><span class="sxs-lookup"><span data-stu-id="bbd7c-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="bbd7c-198">Alternatywnie można wybrać i klonowania repozytorium GitHub dla każdej próbki.</span><span class="sxs-lookup"><span data-stu-id="bbd7c-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="bbd7c-199">Przewodniki z wprowadzeniem pobierania</span><span class="sxs-lookup"><span data-stu-id="bbd7c-199">Getting started guides</span></span>

<span data-ttu-id="bbd7c-200">Zapoznaj się z następujących przewodników, jeśli chcesz, aby uzyskać instrukcje dotyczące sposobu instalowania i rozpoczynanie pracy z biblioteki klienta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="bbd7c-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="bbd7c-201">Wprowadzenie do korzystania z usługi obiektów Blob platformy Azure w .NET</span><span class="sxs-lookup"><span data-stu-id="bbd7c-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="bbd7c-202">Wprowadzenie do korzystania z usługi kolejek platformy Azure w .NET</span><span class="sxs-lookup"><span data-stu-id="bbd7c-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="bbd7c-203">Wprowadzenie do korzystania z usługi tabeli platformy Azure w .NET</span><span class="sxs-lookup"><span data-stu-id="bbd7c-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="bbd7c-204">Wprowadzenie do korzystania z usługi plików na platformę Azure w .NET</span><span class="sxs-lookup"><span data-stu-id="bbd7c-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="bbd7c-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bbd7c-205">Next steps</span></span>

<span data-ttu-id="bbd7c-206">Aby uzyskać informacje na próbkach dla innych języków:</span><span class="sxs-lookup"><span data-stu-id="bbd7c-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="bbd7c-207">Java: [przykłady magazynu platformy Azure przy użyciu języka Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="bbd7c-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="bbd7c-208">Wszystkie inne języki: [przykłady usługi Azure Storage](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="bbd7c-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
