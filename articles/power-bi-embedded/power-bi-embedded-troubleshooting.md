---
title: "Rozwiązywanie problemów z Power BI Embedded Preview aaaMicrosoft"
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
ms.openlocfilehash: a0a25cd73977c0ea0bd6b7c82e215412245771bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Rozwiązywanie problemów z Microsoft Power BI Embedded Preview
Ten artykuł zawiera odpowiedzi na temat tootroubleshoot **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>Ustawianie parametrów połączenia SQL Server
tooset parametry połączenia SQL Server, należy toofollow określonego formatu. Poniżej znajduje się przykład parametry połączenia dla programu SQL Server.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

toolearn więcej informacji na temat parametrów połączenia SQL Server, zobacz następujące artykuły hello:

* [Parametry połączenia serwera SQL](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>Ustawianie poświadczeń
W przypadku hello, gdy użytkownik mający poświadczenia dla rozwoju lub środowiska przemieszczania, takie jak nazwa użytkownika i hasło może być konieczne tooupdate poświadczenia, które odpowiadają rozwiązania produkcji.

## <a name="see-also"></a>Zobacz też
* [Rozpoczęcie pracy z przykładem](power-bi-embedded-get-started-sample.md)
* [Co to jest usługa Power BI Embedded](power-bi-embedded-what-is-power-bi-embedded.md)

