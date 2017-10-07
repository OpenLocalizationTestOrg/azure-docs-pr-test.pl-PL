---
title: "bibliotek aaaClient wymaganych przez połączenie usług analizy tooAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano bibliotek klienta wymaganych przez klienta aplikacji i narzędzi tooconnect usług Azure Analysis Services"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a>Połączenie usług analizy tooAzure biblioteki klienta

Biblioteki klienta są niezbędne dla aplikacji klienckich i serwerów usług tooAnalysis tooconnect narzędzia. 

Trzy bibliotek klienckich korzystać z usług Analysis Services. ADOMD.NET i Analysis Services Management Objects (AMO) są zarządzanego klienta biblioteki. dostawcy OLE DB usług Analysis Services Hello (MSOLAP DLL) jest biblioteka klienta natywnego. Zazwyczaj wszystkie trzy są instalowane na powitania tym samym czasie. Azure Analysis Services wymaga hello najnowszych wersji. 

Aplikacji klienta firmy Microsoft, takich jak Power BI Desktop i Excel zainstalować wszystkie trzech klientów biblioteki. Jednak w zależności od wersji hello lub częstotliwość aktualizacji bibliotek klienta nie może być najnowsze wersje hello wymagane przez usług Azure Analysis Services. Witaj dotyczy toocustom aplikacji lub innych interfejsów, takich jak AsCmd, TOMASZ, ADOMD.NET. Te aplikacje wymagają ręcznej instalacji hello bibliotek. powitania klienta biblioteki dla ręcznej instalacji znajdują się w pakiety funkcji programu SQL Server jako dystrybucyjnego pakietów. Te biblioteki klienta są jednak wiązanej toohello wersja programu SQL Server i nie może być hello najnowsza wersja.  

Biblioteki klienta dla połączeń klienckich różnią się od tooconnect wymagane dostawców danych ze źródła danych tooa serwera usług Azure Analysis Services. toolearn więcej informacji na temat połączenia źródła danych, zobacz [połączenia źródła danych](analysis-services-datasource.md).

## <a name="download-hello-latest-client-libraries"></a>Pobierz najnowsze bibliotek klienckich hello  
Użyj powitania po bibliotek klienta, jeśli w środowisku produkcyjnym i wymagają pełni zwolnione i obsługiwanych wersjach.

[MSOLAP (amd64)](https://go.microsoft.com/fwlink/?linkid=829576)</br>
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</br>
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</br>
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</br>

## <a name="next-steps"></a>Następne kroki
[Połącz przy użyciu programu Excel](analysis-services-connect-excel.md)    
[Łączenie z usługą Power BI](analysis-services-connect-pbi.md)
