---
title: "Omówienie usługi Azure Table Storage | Microsoft Docs"
description: "Przechowywanie danych strukturalnych w chmurze za pomocą Magazynu tabel Azure, magazyn danych NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/23/2017
ms.author: mimig
ms.openlocfilehash: 9099e90c402185b371495379db943d64fb82cdb8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-table-storage-overview"></a><span data-ttu-id="95c99-103">Omówienie usługi Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="95c99-103">Azure Table storage overview</span></span>

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="95c99-104">Azure Table Storage to usługa, która przechowuje dane NoSQL ze strukturą w chmurze, udostępniając magazyn par klucz-atrybut z projektem bez schematu.</span><span class="sxs-lookup"><span data-stu-id="95c99-104">Azure Table storage is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="95c99-105">Ponieważ Magazyn tabel nie ma schematu, łatwo zaadaptować dane do rozwijających się potrzeb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="95c99-105">Because Table storage is schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="95c99-106">Dla większości aplikacji dostęp do danych w usłudze Table Storage jest szybki i ekonomiczny, jest też zazwyczaj tańszy od tradycyjnego rozwiązania SQL dla podobnych ilości danych.</span><span class="sxs-lookup"><span data-stu-id="95c99-106">Access to Table storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="95c99-107">Usługa Table Storage umożliwia przechowywanie elastycznych zestawów danych, takich jak dane użytkowników dla aplikacji sieci Web, książki adresowe, informacje o urządzeniach i inne typy metadanych, których wymaga Twoja usługa.</span><span class="sxs-lookup"><span data-stu-id="95c99-107">You can use Table storage to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="95c99-108">W tabeli można przechowywać dowolną liczbę jednostek, a konto magazynu może zawierać dowolną liczbę tabel w granicach pojemności konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="95c99-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

## <a name="next-steps"></a><span data-ttu-id="95c99-109">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95c99-109">Next steps</span></span>

* <span data-ttu-id="95c99-110">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatną aplikacją autonomiczną oferowaną przez firmę Microsoft, która umożliwia wizualną pracę z danymi w usłudze Azure Storage w systemach Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="95c99-110">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* [<span data-ttu-id="95c99-111">Rozpoczynanie pracy z usługą Azure Table Storage na platformie .NET</span><span class="sxs-lookup"><span data-stu-id="95c99-111">Getting Started with Azure Table Storage in .NET</span></span>](table-storage-how-to-use-dotnet.md)

* <span data-ttu-id="95c99-112">Przejrzyj dokumentację referencyjną usługi Table service, aby uzyskać szczegółowe informacje o dostępnych interfejsach API:</span><span class="sxs-lookup"><span data-stu-id="95c99-112">View the Table service reference documentation for complete details about available APIs:</span></span>

    * [<span data-ttu-id="95c99-113">Dokumentacja biblioteki klienta usługi Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="95c99-113">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

    * [<span data-ttu-id="95c99-114">Dokumentacja interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="95c99-114">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
