---
title: "aaaDynamic SQL w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Porady dotyczące używania dynamicznych SQL w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: a948c2c3-3cd1-4373-90a9-79e59414b778
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 4d66eecb37621510f657d1ec9a2a935daaa16052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a><span data-ttu-id="42460-103">Dynamiczne SQL w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="42460-103">Dynamic SQL in SQL Data Warehouse</span></span>
<span data-ttu-id="42460-104">Podczas tworzenia kodu aplikacji dla usługi SQL Data Warehouse może muszą toohelp dynamiczne sql toouse dostarczanie rozwiązań elastyczny, ogólne i moduły.</span><span class="sxs-lookup"><span data-stu-id="42460-104">When developing application code for SQL Data Warehouse you may need toouse dynamic sql toohelp deliver flexible, generic and modular solutions.</span></span> <span data-ttu-id="42460-105">Usługi SQL Data Warehouse nie obsługuje typów danych obiektów blob w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="42460-105">SQL Data Warehouse does not support blob data types at this time.</span></span> <span data-ttu-id="42460-106">Może to limit rozmiaru hello z ciągów, jak typy obiektów blob obejmują typy zarówno varchar(max), jak i nvarchar(max).</span><span class="sxs-lookup"><span data-stu-id="42460-106">This may limit hello size of your strings as blob types include both varchar(max) and nvarchar(max) types.</span></span> <span data-ttu-id="42460-107">Jeśli użyto tych typów w kodzie aplikacji podczas kompilowania bardzo dużych ciągów, należy toobreak hello kodu do fragmentów i użycie instrukcji use EXEC hello zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="42460-107">If you have used these types in your application code when building very large strings, you will need toobreak hello code into chunks and use hello EXEC statement instead.</span></span>

<span data-ttu-id="42460-108">Prosty przykład:</span><span class="sxs-lookup"><span data-stu-id="42460-108">A simple example:</span></span>

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

<span data-ttu-id="42460-109">Jeśli hello ciąg jest krótkim służy [sp_executesql] [ sp_executesql] normalnego.</span><span class="sxs-lookup"><span data-stu-id="42460-109">If hello string is short you can use [sp_executesql][sp_executesql] as normal.</span></span>

> [!NOTE]
> <span data-ttu-id="42460-110">Instrukcje wykonywane jako dynamiczny SQL nadal będzie reguł sprawdzania poprawności TSQL tooall podmiotu.</span><span class="sxs-lookup"><span data-stu-id="42460-110">Statements executed as dynamic SQL will still be subject tooall TSQL validation rules.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="42460-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="42460-111">Next steps</span></span>
<span data-ttu-id="42460-112">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="42460-112">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
