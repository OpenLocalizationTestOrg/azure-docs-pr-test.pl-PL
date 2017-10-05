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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="8d286-103">Rozwiązywanie problemów z Microsoft Power BI Embedded Preview</span><span class="sxs-lookup"><span data-stu-id="8d286-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="8d286-104">Ten artykuł zawiera odpowiedzi na jak rozwiązywać problemy z **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="8d286-104">This article provides answers for how  to troubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="8d286-105">Ustawianie parametrów połączenia SQL Server</span><span class="sxs-lookup"><span data-stu-id="8d286-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="8d286-106">Aby ustawić ciąg połączenia programu SQL Server, należy wykonywać określonego formatu.</span><span class="sxs-lookup"><span data-stu-id="8d286-106">To set a SQL Server connecting string, you need to follow a specific format.</span></span> <span data-ttu-id="8d286-107">Poniżej znajduje się przykład parametry połączenia dla programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8d286-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="8d286-108">Aby dowiedzieć się więcej na temat parametrów połączenia SQL Server, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="8d286-108">To learn more about SQL Server connection strings, see the following articles:</span></span>

* [<span data-ttu-id="8d286-109">Parametry połączenia serwera SQL</span><span class="sxs-lookup"><span data-stu-id="8d286-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="8d286-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="8d286-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="8d286-111">Ustawianie poświadczeń</span><span class="sxs-lookup"><span data-stu-id="8d286-111">Setting credentials</span></span>
<span data-ttu-id="8d286-112">W przypadku, gdy użytkownik mający poświadczenia dla rozwoju lub środowiska przemieszczania, takie jak nazwa użytkownika i hasło może być konieczna aktualizacja poświadczenia, które odpowiadają rozwiązania produkcji.</span><span class="sxs-lookup"><span data-stu-id="8d286-112">In the case where you have credentials for a development or staging environment, such as user name and password, you might need to update credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="8d286-113">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="8d286-113">See Also</span></span>
* [<span data-ttu-id="8d286-114">Rozpoczęcie pracy z przykładem</span><span class="sxs-lookup"><span data-stu-id="8d286-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="8d286-115">Co to jest usługa Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="8d286-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

