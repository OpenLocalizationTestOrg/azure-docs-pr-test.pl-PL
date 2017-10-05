---
title: "Rozwiązywanie problemów z Microsoft Power BI Embedded Preview"
description: "Rozwiązywanie problemów z Microsoft Power BI Embedded Preview"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: c8aee652-ed8b-4c66-9c63-f798b7a655b4
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: f406d23e578acc825514aa5bd9eabcbf160bf9ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Rozwiązywanie problemów z Microsoft Power BI Embedded Preview
Ten artykuł zawiera odpowiedzi na jak rozwiązywać problemy z **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>Ustawianie parametrów połączenia SQL Server
Aby ustawić ciąg połączenia programu SQL Server, należy wykonywać określonego formatu. Poniżej znajduje się przykład parametry połączenia dla programu SQL Server.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

Aby dowiedzieć się więcej na temat parametrów połączenia SQL Server, zobacz następujące artykuły:

* [Parametry połączenia serwera SQL](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>Ustawianie poświadczeń
W przypadku, gdy użytkownik mający poświadczenia dla rozwoju lub środowiska przemieszczania, takie jak nazwa użytkownika i hasło może być konieczna aktualizacja poświadczenia, które odpowiadają rozwiązania produkcji.

## <a name="see-also"></a>Zobacz też
* [Rozpoczęcie pracy z przykładem](power-bi-embedded-get-started-sample.md)
* [Co to jest usługa Power BI Embedded](power-bi-embedded-what-is-power-bi-embedded.md)

