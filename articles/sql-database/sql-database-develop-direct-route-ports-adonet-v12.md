---
title: aaaPorts poza 1433 dla bazy danych SQL | Dokumentacja firmy Microsoft
description: "Połączenia klientów z tooAzure ADO.NET bazy danych SQL czasami używaj serwera proxy hello i bezpośrednią interakcję z hello bazy danych. Porty inne niż 1433 nabierają znaczenia."
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
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="9938a-104">Porty inne niż 1433 dla ADO.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="9938a-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="9938a-105">W tym temacie opisano zachowanie połączenia bazy danych SQL Azure powitania dla klientów używających ADO.NET 4.5 lub nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="9938a-105">This topic describes hello Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9938a-106">Informacje o architekturze łączności, zobacz [architektury połączenia bazy danych SQL Azure](sql-database-connectivity-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="9938a-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="9938a-107">Poza vs wewnątrz</span><span class="sxs-lookup"><span data-stu-id="9938a-107">Outside vs inside</span></span>
<span data-ttu-id="9938a-108">Dla połączeń tooAzure bazy danych SQL, należy najpierw poprosimy czy uruchamia program kliencki *poza* lub *wewnątrz* hello chmury Azure granic.</span><span class="sxs-lookup"><span data-stu-id="9938a-108">For connections tooAzure SQL Database, we must first ask whether your client program runs *outside* or *inside* hello Azure cloud boundary.</span></span> <span data-ttu-id="9938a-109">Podpunkty Hello omówiono w nim dwóch typowych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="9938a-109">hello subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="9938a-110">*Poza:* klient jest uruchamiany na komputerze stacjonarnym</span><span class="sxs-lookup"><span data-stu-id="9938a-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="9938a-111">Port 1433 jest hello wyłącznie port, który musi być otwarty na komputerze stacjonarnym, hostującego aplikację kliencką bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="9938a-111">Port 1433 is hello only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="9938a-112">*Wewnątrz:* klienta działa na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="9938a-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="9938a-113">Po uruchomieniu wewnątrz granic chmury Azure powitania klienta używa można zwany *trasy bezpośredniej* toointeract z hello bazy danych SQL server.</span><span class="sxs-lookup"><span data-stu-id="9938a-113">When your client runs inside hello Azure cloud boundary, it uses what we can call a *direct route* toointeract with hello SQL Database server.</span></span> <span data-ttu-id="9938a-114">Po nawiązaniu połączenia dalszych interakcji między powitania klienta i bazy danych obejmują żadnego serwera proxy oprogramowania pośredniczącego.</span><span class="sxs-lookup"><span data-stu-id="9938a-114">After a connection is established, further interactions between hello client and database involve no middleware proxy.</span></span>

<span data-ttu-id="9938a-115">kolejność Hello jest następująca:</span><span class="sxs-lookup"><span data-stu-id="9938a-115">hello sequence is as follows:</span></span>

1. <span data-ttu-id="9938a-116">ADO.NET 4.5 (lub nowszej) inicjuje krótki interakcji z hello chmury Azure i odbiera numeru portu dynamicznie zidentyfikowane.</span><span class="sxs-lookup"><span data-stu-id="9938a-116">ADO.NET 4.5 (or later) initiates a brief interaction with hello Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="9938a-117">numer portu Hello dynamicznie identyfikowane jest w zasięgu hello 11000 11999 lub 14000 14999.</span><span class="sxs-lookup"><span data-stu-id="9938a-117">hello dynamically identified port number is in hello range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="9938a-118">ADO.NET następnie łączy toohello bazy danych programu SQL server bezpośrednio z nie oprogramowania pośredniczącego między nimi.</span><span class="sxs-lookup"><span data-stu-id="9938a-118">ADO.NET then connects toohello SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="9938a-119">Zapytania są wysyłane bezpośrednio toohello bazy danych, a wyniki są zwracane bezpośrednio toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="9938a-119">Queries are sent directly toohello database, and results are returned directly toohello client.</span></span>

<span data-ttu-id="9938a-120">Upewnij się, ten port hello 11000 11999 i 14000-14999 na komputerze klienta usługi Azure pozostają dostępne dla ADO.NET 4.5 interakcji klientów z bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="9938a-120">Ensure that hello port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="9938a-121">W szczególności porty hello zakresu nie może zawierać innych blokują ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="9938a-121">In particular, ports in hello range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="9938a-122">Na maszynie Wirtualnej Azure, hello **Zapora systemu Windows z zabezpieczeniami zaawansowanymi** formanty hello ustawienia portu.</span><span class="sxs-lookup"><span data-stu-id="9938a-122">On your Azure VM, hello **Windows Firewall with Advanced Security** controls hello port settings.</span></span>
  
  * <span data-ttu-id="9938a-123">Można użyć hello [interfejsu użytkownika zapory](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a regułę, dla którego określone hello **TCP** protokołu wraz ze składnią hello zakres portów, takich jak **11000 11999**.</span><span class="sxs-lookup"><span data-stu-id="9938a-123">You can use hello [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a rule for which you specify hello **TCP** protocol along with a port range with hello syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="9938a-124">Wyjaśnienia wersji</span><span class="sxs-lookup"><span data-stu-id="9938a-124">Version clarifications</span></span>
<span data-ttu-id="9938a-125">Monikery hello, odwołujące się do wersji tooproduct wyjaśnia, w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="9938a-125">This section clarifies hello monikers that refer tooproduct versions.</span></span> <span data-ttu-id="9938a-126">Zawiera także listę par niektóre wersje produktów.</span><span class="sxs-lookup"><span data-stu-id="9938a-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="9938a-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="9938a-127">ADO.NET</span></span>
* <span data-ttu-id="9938a-128">ADO.NET 4.0 obsługuje protokół hello TDS 7.3, ale nie 7.4.</span><span class="sxs-lookup"><span data-stu-id="9938a-128">ADO.NET 4.0 supports hello TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="9938a-129">ADO.NET 4.5 lub nowszej obsługuje protokół hello TDS 7.4.</span><span class="sxs-lookup"><span data-stu-id="9938a-129">ADO.NET 4.5 and later supports hello TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="9938a-130">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="9938a-130">Related links</span></span>
* <span data-ttu-id="9938a-131">ADO.NET 4.6 został wydany 20 lipca 2015 r.</span><span class="sxs-lookup"><span data-stu-id="9938a-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="9938a-132">Zawiadomienie blog zespołu .NET hello jest dostępna [tutaj](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="9938a-132">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="9938a-133">ADO.NET 4.5 został wydany 15 sierpień 2012.</span><span class="sxs-lookup"><span data-stu-id="9938a-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="9938a-134">Zawiadomienie blog zespołu .NET hello jest dostępna [tutaj](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="9938a-134">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="9938a-135">Jest dostępna w blogu o ADO.NET 4.5.1 [tutaj](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="9938a-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="9938a-136">Lista wersji protokołu TDS</span><span class="sxs-lookup"><span data-stu-id="9938a-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="9938a-137">Omówienie tworzenia bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="9938a-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="9938a-138">Zapory bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9938a-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="9938a-139">Porady: Konfigurowanie ustawień zapory w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="9938a-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

