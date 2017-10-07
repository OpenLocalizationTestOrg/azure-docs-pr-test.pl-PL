---
title: "Klienci z obniżonym poziomem hurtowni danych aaaSQL Obsługa inspekcji danych | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat obsługi klientów niższych poziomów usługi SQL Data Warehouse danych inspekcji"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a>Obsługa klientów niższych poziomów usługi SQL Data Warehouse — inspekcji i dynamicznego maskowania danych
[Inspekcja](sql-data-warehouse-auditing-overview.md) współpracuje z klientom SQL, które obsługują przekierowanie TDS.

Dowolnego klienta, który implementuje TDS 7.4 powinny również obsługiwać przekierowania. Wyjątki toothis obejmują JDBC 4.0 w której hello funkcji przekierowania nie jest w pełni obsługiwane i Tedious dla środowiska Node.JS, w którym nie została zaimplementowana przekierowania.

Dla "Klientów niższych poziomów" tj. co obsługuje TDS wersji 7.3 i poniżej — Witaj nazwa FQDN serwera w parametrach połączenia hello powinno zostać zmodyfikowane:

Oryginalna nazwa FQDN serwera w parametrach połączenia hello: <*nazwy serwera*>. database.windows.net

Nazwa FQDN serwera zmodyfikowane w ciągu połączenia hello: <*nazwy serwera*> .database. **bezpieczne**. windows.net

Zawiera listę częściowej "Klienci z obniżonym poziomem":

* .NET 4.0 i poniżej,
* ODBC 10.0 i poniżej.
* JDBC (gdy JDBC obsługuje 7.4 TDS, powitalne funkcji przekierowania TDS nie jest w pełni obsługiwana)
* Niewygodny (dla środowiska Node.JS)

**Uwaga:** hello powyżej modyfikacji przykładową nazwą FQDN serwera mogą być przydatne także stosowania zasad inspekcji programu SQL Server poziom bez potrzebę konfiguracji kroku w każdej bazie danych (ograniczenie tymczasowe).     

