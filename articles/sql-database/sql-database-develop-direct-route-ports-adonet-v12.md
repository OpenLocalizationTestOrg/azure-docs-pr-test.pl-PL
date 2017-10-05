---
title: "Porty inne niż 1433 dla bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Czasami połączeń klientów z ADO.NET z bazy danych SQL Azure pominąć serwer proxy i bezpośrednią interakcję z bazy danych. Porty inne niż 1433 nabierają znaczenia."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: d47ee8c794d1e231507dae6bb4aa88bf19ce6418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="ec1e9-104">Porty inne niż 1433 dla ADO.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="ec1e9-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="ec1e9-105">W tym temacie opisano zachowanie połączenia bazy danych SQL Azure dla klientów używających ADO.NET 4.5 lub nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-105">This topic describes the Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ec1e9-106">Informacje o architekturze łączności, zobacz [architektury połączenia bazy danych SQL Azure](sql-database-connectivity-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="ec1e9-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="ec1e9-107">Poza vs wewnątrz</span><span class="sxs-lookup"><span data-stu-id="ec1e9-107">Outside vs inside</span></span>
<span data-ttu-id="ec1e9-108">Dla połączeń z bazą danych SQL Azure, musi najpierw poprosimy czy uruchamia program kliencki *poza* lub *wewnątrz* granic chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-108">For connections to Azure SQL Database, we must first ask whether your client program runs *outside* or *inside* the Azure cloud boundary.</span></span> <span data-ttu-id="ec1e9-109">Podpunkty omówiono w nim dwóch typowych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-109">The subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="ec1e9-110">*Poza:* klient jest uruchamiany na komputerze stacjonarnym</span><span class="sxs-lookup"><span data-stu-id="ec1e9-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="ec1e9-111">Port 1433 jest tylko port, który musi być otwarty na komputerze stacjonarnym, hostującego aplikację kliencką bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-111">Port 1433 is the only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="ec1e9-112">*Wewnątrz:* klienta działa na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ec1e9-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="ec1e9-113">Po uruchomieniu klienta wewnątrz granic chmury Azure używa można zwany *trasy bezpośredniej* do interakcji z serwerem bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-113">When your client runs inside the Azure cloud boundary, it uses what we can call a *direct route* to interact with the SQL Database server.</span></span> <span data-ttu-id="ec1e9-114">Po nawiązaniu połączenia dalszej interakcji między klientem a bazy danych obejmują żadnego serwera proxy oprogramowania pośredniczącego.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-114">After a connection is established, further interactions between the client and database involve no middleware proxy.</span></span>

<span data-ttu-id="ec1e9-115">Sekwencja jest następujący:</span><span class="sxs-lookup"><span data-stu-id="ec1e9-115">The sequence is as follows:</span></span>

1. <span data-ttu-id="ec1e9-116">ADO.NET 4.5 (lub nowszej) inicjuje krótki interakcji z chmury Azure i odbiera numeru portu dynamicznie zidentyfikowane.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-116">ADO.NET 4.5 (or later) initiates a brief interaction with the Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="ec1e9-117">Numer portu dynamicznie zidentyfikowanych jest w zasięgu 11000 11999 lub 14000 14999.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-117">The dynamically identified port number is in the range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="ec1e9-118">ADO.NET następnie nawiązuje połączenie z serwerem bazy danych SQL bezpośrednio, z nie oprogramowania pośredniczącego między nimi.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-118">ADO.NET then connects to the SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="ec1e9-119">Zapytania są wysyłane bezpośrednio do bazy danych, a wyniki są zwracane bezpośrednio do klienta.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-119">Queries are sent directly to the database, and results are returned directly to the client.</span></span>

<span data-ttu-id="ec1e9-120">Upewnij się, że port, który 11000 11999 i 14000-14999 na komputerze klienta usługi Azure pozostają dostępne dla ADO.NET 4.5 interakcji klientów z bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-120">Ensure that the port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="ec1e9-121">W szczególności porty z zakresu nie może zawierać innych blokują ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-121">In particular, ports in the range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="ec1e9-122">Na maszynie Wirtualnej Azure **Zapora systemu Windows z zabezpieczeniami zaawansowanymi** kontroluje ustawienia portu.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-122">On your Azure VM, the **Windows Firewall with Advanced Security** controls the port settings.</span></span>
  
  * <span data-ttu-id="ec1e9-123">Można użyć [interfejsu użytkownika zapory](http://msdn.microsoft.com/library/cc646023.aspx) Aby dodać regułę, dla którego należy określić **TCP** , takich jak protokół wraz z zakresu portów przy użyciu składni **11000 11999**.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-123">You can use the [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) to add a rule for which you specify the **TCP** protocol along with a port range with the syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="ec1e9-124">Wyjaśnienia wersji</span><span class="sxs-lookup"><span data-stu-id="ec1e9-124">Version clarifications</span></span>
<span data-ttu-id="ec1e9-125">Ta sekcja zawiera wyjaśnienie informujące, krótkie, które odwołują się do wersji produktu.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-125">This section clarifies the monikers that refer to product versions.</span></span> <span data-ttu-id="ec1e9-126">Zawiera także listę par niektóre wersje produktów.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="ec1e9-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="ec1e9-127">ADO.NET</span></span>
* <span data-ttu-id="ec1e9-128">ADO.NET 4.0 obsługuje protokół TDS 7.3, ale nie 7.4.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-128">ADO.NET 4.0 supports the TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="ec1e9-129">ADO.NET 4.5 lub nowszej obsługuje protokół TDS 7.4.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-129">ADO.NET 4.5 and later supports the TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="ec1e9-130">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="ec1e9-130">Related links</span></span>
* <span data-ttu-id="ec1e9-131">ADO.NET 4.6 został wydany 20 lipca 2015 r.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="ec1e9-132">Zawiadomienie blog zespołu .NET jest dostępna [tutaj](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec1e9-132">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="ec1e9-133">ADO.NET 4.5 został wydany 15 sierpień 2012.</span><span class="sxs-lookup"><span data-stu-id="ec1e9-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="ec1e9-134">Zawiadomienie blog zespołu .NET jest dostępna [tutaj](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec1e9-134">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="ec1e9-135">Jest dostępna w blogu o ADO.NET 4.5.1 [tutaj](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec1e9-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="ec1e9-136">Lista wersji protokołu TDS</span><span class="sxs-lookup"><span data-stu-id="ec1e9-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="ec1e9-137">Omówienie tworzenia bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="ec1e9-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="ec1e9-138">Zapory bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ec1e9-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="ec1e9-139">Porady: Konfigurowanie ustawień zapory w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="ec1e9-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

