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
# <a name="dynamic-sql-in-sql-data-warehouse"></a>Dynamiczne SQL w usłudze SQL Data Warehouse
Podczas tworzenia kodu aplikacji dla usługi SQL Data Warehouse może muszą toohelp dynamiczne sql toouse dostarczanie rozwiązań elastyczny, ogólne i moduły. Usługi SQL Data Warehouse nie obsługuje typów danych obiektów blob w tym momencie. Może to limit rozmiaru hello z ciągów, jak typy obiektów blob obejmują typy zarówno varchar(max), jak i nvarchar(max). Jeśli użyto tych typów w kodzie aplikacji podczas kompilowania bardzo dużych ciągów, należy toobreak hello kodu do fragmentów i użycie instrukcji use EXEC hello zamiast tego.

Prosty przykład:

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

Jeśli hello ciąg jest krótkim służy [sp_executesql] [ sp_executesql] normalnego.

> [!NOTE]
> Instrukcje wykonywane jako dynamiczny SQL nadal będzie reguł sprawdzania poprawności TSQL tooall podmiotu.
> 
> 

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
