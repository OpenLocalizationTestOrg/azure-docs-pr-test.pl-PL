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
# <a name="ports-beyond-1433-for-adonet-45"></a>Porty inne niż 1433 dla ADO.NET 4.5
W tym temacie opisano zachowanie połączenia bazy danych SQL Azure powitania dla klientów używających ADO.NET 4.5 lub nowszej wersji. 

> [!IMPORTANT]
> Informacje o architekturze łączności, zobacz [architektury połączenia bazy danych SQL Azure](sql-database-connectivity-architecture.md).
>

## <a name="outside-vs-inside"></a>Poza vs wewnątrz
Dla połączeń tooAzure bazy danych SQL, należy najpierw poprosimy czy uruchamia program kliencki *poza* lub *wewnątrz* hello chmury Azure granic. Podpunkty Hello omówiono w nim dwóch typowych scenariuszy.

#### <a name="outside-client-runs-on-your-desktop-computer"></a>*Poza:* klient jest uruchamiany na komputerze stacjonarnym
Port 1433 jest hello wyłącznie port, który musi być otwarty na komputerze stacjonarnym, hostującego aplikację kliencką bazy danych SQL.

#### <a name="inside-client-runs-on-azure"></a>*Wewnątrz:* klienta działa na platformie Azure
Po uruchomieniu wewnątrz granic chmury Azure powitania klienta używa można zwany *trasy bezpośredniej* toointeract z hello bazy danych SQL server. Po nawiązaniu połączenia dalszych interakcji między powitania klienta i bazy danych obejmują żadnego serwera proxy oprogramowania pośredniczącego.

kolejność Hello jest następująca:

1. ADO.NET 4.5 (lub nowszej) inicjuje krótki interakcji z hello chmury Azure i odbiera numeru portu dynamicznie zidentyfikowane.
   
   * numer portu Hello dynamicznie identyfikowane jest w zasięgu hello 11000 11999 lub 14000 14999.
2. ADO.NET następnie łączy toohello bazy danych programu SQL server bezpośrednio z nie oprogramowania pośredniczącego między nimi.
3. Zapytania są wysyłane bezpośrednio toohello bazy danych, a wyniki są zwracane bezpośrednio toohello klienta.

Upewnij się, ten port hello 11000 11999 i 14000-14999 na komputerze klienta usługi Azure pozostają dostępne dla ADO.NET 4.5 interakcji klientów z bazy danych SQL.

* W szczególności porty hello zakresu nie może zawierać innych blokują ruchu wychodzącego.
* Na maszynie Wirtualnej Azure, hello **Zapora systemu Windows z zabezpieczeniami zaawansowanymi** formanty hello ustawienia portu.
  
  * Można użyć hello [interfejsu użytkownika zapory](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a regułę, dla którego określone hello **TCP** protokołu wraz ze składnią hello zakres portów, takich jak **11000 11999**.

## <a name="version-clarifications"></a>Wyjaśnienia wersji
Monikery hello, odwołujące się do wersji tooproduct wyjaśnia, w tej sekcji. Zawiera także listę par niektóre wersje produktów.

#### <a name="adonet"></a>ADO.NET
* ADO.NET 4.0 obsługuje protokół hello TDS 7.3, ale nie 7.4.
* ADO.NET 4.5 lub nowszej obsługuje protokół hello TDS 7.4.

## <a name="related-links"></a>Powiązane linki
* ADO.NET 4.6 został wydany 20 lipca 2015 r. Zawiadomienie blog zespołu .NET hello jest dostępna [tutaj](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).
* ADO.NET 4.5 został wydany 15 sierpień 2012. Zawiadomienie blog zespołu .NET hello jest dostępna [tutaj](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).
  
  * Jest dostępna w blogu o ADO.NET 4.5.1 [tutaj](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).
* [Lista wersji protokołu TDS](http://www.freetds.org/userguide/tdshistory.htm)
* [Omówienie tworzenia bazy danych SQL](sql-database-develop-overview.md)
* [Zapory bazy danych SQL Azure](sql-database-firewall-configure.md)
* [Porady: Konfigurowanie ustawień zapory w bazie danych SQL](sql-database-configure-firewall-settings.md)

