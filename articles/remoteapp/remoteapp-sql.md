---
title: "aaaSQL Azure z usługą Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse SQL Azure z usługą Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
editor: 
ms.assetid: 35f81d75-bfd7-4980-807e-00339f2cb2a4
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fec4cb1f1ab3cde03b6ff613650e01bae3552824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-azure-with-azure-remoteapp"></a>Usługi SQL Azure z usługą Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Często w przypadku, gdy klienci planujący toohost swoich aplikacji systemu Windows w chmurze hello z usługą Azure RemoteApp chcą także toomigrate swoje dane, takie jak serwery SQL do hello chmury dla pełnego wdrożenia w chmurze. Pozwala to uzyskać całościowe rozwiązanie hostowane w chmurze, dostępne w dowolnym momencie z każdego miejsca przy użyciu dowolnego urządzenia za pośrednictwem usługi Azure RemoteApp. Poniżej podano linki i odwołuje się wraz z toohelp wskazówki można z tego procesu.  

## <a name="migrate-your-sql-data"></a>Migrowanie danych SQL
Rozpoczynać [Migrowanie tooAzure bazy danych programu SQL Server, bazy danych SQL](../sql-database/sql-database-cloud-migrate.md). 

## <a name="configure-azure-remoteapp"></a>Konfigurowanie usługi Azure RemoteApp
Możesz hostować aplikacje systemu Windows w usłudze Azure RemoteApp Poniżej znajduje się ogólny opis kroków, które należy wykonać:

1. Utwórz hello [maszynę Wirtualną z szablonem usługi Azure RemoteApp](remoteapp-imageoptions.md). 
2. Zainstaluj aplikacji hello wymagane na powitania maszyny Wirtualnej.
3. Konfigurowanie aplikacji hello łączy toohello bazy danych SQL i potwierdź poprawność jej działania.
4. Narzędzia Sysprep i zamknij hello maszyny Wirtualnej. Przechwyć to jako obraz przeznaczony do użycia z usługą Azure. **Uwaga:** należy tooensure, że aplikacja hello jest tooretain stanie hello DB łączności informacji za pośrednictwem procesu sysprep hello. Jeśli aplikacja hello jest tooretain hello bazy danych — informacje o połączeniu, może być dostawcą hello tooengage toocheck aplikacji hello jak można określić parametry połączenia hello.
5. Zaimportuj niestandardowy obraz powitania do biblioteki usługi Azure RemoteApp, wybierając hello właściwą lokalizację geograficzną wdrożenia usług SQL Azure znajduje się. 
6. Wdrażanie w hello tych samych danych Centrum jako wdrożenie usług SQL Azure przy użyciu hello powyżej szablonu i publikowanie aplikacji hello kolekcji usługi RemoteApp. Wdrożenie usługi Azure RemoteApp w hello tego samego centrum danych, co wdrożenie usług SQL Azure pomaga zapewnić hello największą szybkość połączeń i zmniejszenia opóźnień. 

## <a name="app-and-sql-configuration-considerations"></a>Zagadnienia do rozważenia związane z konfiguracją aplikacji i bazy danych SQL:
Istnieje kilka punktów tooconsider przy użyciu Azure SQL RemoteApp:

Dowiedz się [jak tooconfigure Azure SQL bazy danych zapory](../sql-database/sql-database-firewall-configure.md). Zgodnie z artykułem hello "początkowo wszystkie serwera Azure SQL Database tooyour dostępu jest zablokowany przez zaporę Windows hello. W kolejności toobegin korzysta z serwera bazy danych SQL Azure musi przejść toohello klasycznego portalu i określ co najmniej jedną regułę zapory poziomu serwera, które tooyour dostępu na serwerze bazy danych SQL Azure. Użyj toospecify reguły zapory hello który adres IP od hello są dozwolone przez Internet, i czy aplikacjami platformy Azure można spróbować serwera bazy danych SQL Azure tooyour tooconnect."

Gdy komputer próbuje tooconnect tooyour bazy danych serwera z hello Internet, zapory hello sprawdza również hello pochodzące z adresu IP hello żądania dotyczącego hello pełny zestaw z poziomu serwera i (jeśli jest to wymagane) reguły zapory poziomu bazy danych. "Jeśli adres IP hello żądania hello jest w jednej z określonych w regułach zapory poziomu serwera hello zakresach hello, hello zostanie ustanowione połączenie serwera bazy danych SQL Azure tooyour." Dzięki temu można używać zakresów adresów IP, a nie tylko pojedynczych źródłowych adresów IP.

Postępuj zgodnie z instrukcjami krok po kroku hello [porady: Konfigurowanie ustawień zapory w bazie danych SQL przy użyciu portalu Azure hello](../sql-database/sql-database-configure-firewall-settings.md) zakres adresów IP hello toospecify. Podczas konfigurowania reguł zapory SQL hello, podaj zakres adresów IP hello hello podsieci, która została określona hello kolekcji usługi Azure RemoteApp. Powinno to umożliwić serwerom ARA hello toohello tooconnect bazy danych SQL nawet, jeśli będzie dynamicznie przypisaniu adresów IP.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli hello z aplikacji klienckiej hostowanej w usłudze Azure RemoteApp, który łączy tooa SQL bazy danych w przypadku, gdy hostowanej na platformie Azure lub lokalnie jest powolne może istnieć kilka przyczyn dlaczego.  

* Opóźnienie sieci pomiędzy tooAzure Twojego urządzenia jest wysoka. Przenieś toohello najlepsze i najszybsze połączenie, które można uzyskać najlepszą wydajność. Użyj [azurespeed.com](http://azurespeed.com/) jako tootest ogólnego Narzędzia centrum danych tooAzure opóźnienia urządzeń.  
* Aplikacja kliencka hostowana w usłudze Azure RemoteApp jest mocno obciążona. Wybór innego planu rozliczeniowego, na przykład Premium, umożliwi zwiększenie wydajności. Innym sposobem jest toomonitor hello zasobów jest korzystanie z aplikacji: podczas aktywnej sesji wykonać sekwencję klawiszy ctrl-alt-end, który uruchomi hello ekranu SAS, wybierz Menedżera zadań i sprawdź wykorzystanie zasobów dla aplikacji.
* Serwer SQL jest mocno obciążony lub nie jest zoptymalizowany. Postępuj zgodnie ze wskazówkami dotyczącymi rozwiązywania problemów z bazą danych SQL. 

