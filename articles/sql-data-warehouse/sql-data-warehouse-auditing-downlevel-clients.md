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
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="2ffbe-103">Obsługa klientów niższych poziomów usługi SQL Data Warehouse — inspekcji i dynamicznego maskowania danych</span><span class="sxs-lookup"><span data-stu-id="2ffbe-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="2ffbe-104">[Inspekcja](sql-data-warehouse-auditing-overview.md) współpracuje z klientom SQL, które obsługują przekierowanie TDS.</span><span class="sxs-lookup"><span data-stu-id="2ffbe-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="2ffbe-105">Dowolnego klienta, który implementuje TDS 7.4 powinny również obsługiwać przekierowania.</span><span class="sxs-lookup"><span data-stu-id="2ffbe-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="2ffbe-106">Wyjątki toothis obejmują JDBC 4.0 w której hello funkcji przekierowania nie jest w pełni obsługiwane i Tedious dla środowiska Node.JS, w którym nie została zaimplementowana przekierowania.</span><span class="sxs-lookup"><span data-stu-id="2ffbe-106">Exceptions toothis include JDBC 4.0 in which hello redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="2ffbe-107">Dla "Klientów niższych poziomów" tj. co obsługuje TDS wersji 7.3 i poniżej — Witaj nazwa FQDN serwera w parametrach połączenia hello powinno zostać zmodyfikowane:</span><span class="sxs-lookup"><span data-stu-id="2ffbe-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - hello server FQDN in hello connection string should be modified:</span></span>

<span data-ttu-id="2ffbe-108">Oryginalna nazwa FQDN serwera w parametrach połączenia hello: <*nazwy serwera*>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="2ffbe-108">Original server FQDN in hello connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="2ffbe-109">Nazwa FQDN serwera zmodyfikowane w ciągu połączenia hello: <*nazwy serwera*> .database. **bezpieczne**. windows.net</span><span class="sxs-lookup"><span data-stu-id="2ffbe-109">Modified server FQDN in hello connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="2ffbe-110">Zawiera listę częściowej "Klienci z obniżonym poziomem":</span><span class="sxs-lookup"><span data-stu-id="2ffbe-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="2ffbe-111">.NET 4.0 i poniżej,</span><span class="sxs-lookup"><span data-stu-id="2ffbe-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="2ffbe-112">ODBC 10.0 i poniżej.</span><span class="sxs-lookup"><span data-stu-id="2ffbe-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="2ffbe-113">JDBC (gdy JDBC obsługuje 7.4 TDS, powitalne funkcji przekierowania TDS nie jest w pełni obsługiwana)</span><span class="sxs-lookup"><span data-stu-id="2ffbe-113">JDBC (while JDBC does support TDS 7.4, hello TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="2ffbe-114">Niewygodny (dla środowiska Node.JS)</span><span class="sxs-lookup"><span data-stu-id="2ffbe-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="2ffbe-115">**Uwaga:** hello powyżej modyfikacji przykładową nazwą FQDN serwera mogą być przydatne także stosowania zasad inspekcji programu SQL Server poziom bez potrzebę konfiguracji kroku w każdej bazie danych (ograniczenie tymczasowe).</span><span class="sxs-lookup"><span data-stu-id="2ffbe-115">**Remark:** hello above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

