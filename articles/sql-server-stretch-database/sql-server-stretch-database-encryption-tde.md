---
title: aaaEnable przezroczystego szyfrowania danych dla bazy danych Stretch - Azure | Dokumentacja firmy Microsoft
description: "Włącz przezroczystego szyfrowania danych (funkcji TDE) dla danych programu SQL Server Stretch na platformie Azure"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>Włącz przezroczystego szyfrowania danych (funkcji TDE) dla baza danych Stretch na platformie Azure
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Funkcji przezroczystego szyfrowania danych (TDE) ułatwia ochronę przed zagrożeniem hello złośliwych działań, wykonując w czasie rzeczywistym szyfrowania i odszyfrowywania hello bazy danych, skojarzonych kopii zapasowych i plików dziennika transakcji w stanie spoczynku bez konieczności zmiany toohello aplikacja.

Funkcji TDE szyfruje magazyn hello całej bazy danych przy użyciu klucza szyfrowania symetrycznego klucza o nazwie hello bazy danych. klucz szyfrowania bazy danych Hello jest chroniony za pomocą certyfikatu wbudowanego serwera. certyfikat serwera wbudowanych Hello jest unikatowy dla każdego serwera Azure. Microsoft automatycznie przełącza tych certyfikatów, co najmniej co 90 dni. Ogólny opis funkcji TDE, zobacz [funkcji przezroczystego szyfrowania danych (TDE)].

## <a name="enabling-encryption"></a>Włączenie szyfrowania
tooenable funkcji TDE Azure bazy danych, która jest przechowywana hello migracji danych z bazy danych programu SQL Server z obsługą odcinek, hello następujące czynności:

1. Bazy danych otwórz hello w hello [portalu Azure](https://portal.azure.com)
2. W bloku bazy danych powitania kliknij hello **ustawienia** przycisku
3. Wybierz hello **przezroczystego szyfrowania danych** opcji![][1]
4. Wybierz hello **na** ustawienia, a następnie wybierz **Zapisz**
   ![][2]

## <a name="disabling-encryption"></a>Wyłączenie szyfrowania
toodisable funkcji TDE Azure bazy danych, która jest przechowywana hello migracji danych z bazy danych programu SQL Server z obsługą odcinek, hello następujące czynności:

1. Bazy danych otwórz hello w hello [portalu Azure](https://portal.azure.com)
2. W bloku bazy danych powitania kliknij hello **ustawienia** przycisku
3. Wybierz hello **przezroczystego szyfrowania danych** opcji
4. Wybierz hello **poza** ustawienia, a następnie wybierz **Zapisz**

<!--Anchors-->
[funkcji przezroczystego szyfrowania danych (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
