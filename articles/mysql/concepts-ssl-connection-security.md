---
title: "łączność aaaSSL bazy danych Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: "Informacje dotyczące konfiguracji bazy danych Azure MySQL i tooproperly skojarzonych aplikacji używać połączeń SSL"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a>Połączenie SSL w bazie danych Azure dla programu MySQL
Bazy danych platformy Azure dla programu MySQL obsługuje łączenie aplikacji tooclient serwera bazy danych przy użyciu protokołu Secure Sockets Layer (SSL). Wymuszanie połączenia SSL między serwerem bazy danych i aplikacji klienckich pomaga chronić przed atakami "man w środku powitania" hello strumienia danych między serwerem hello i aplikacji są szyfrowane.

## <a name="default-settings"></a>Ustawienia domyślne
Domyślnie hello bazy danych usługi powinien być skonfigurowany toorequire połączeń SSL podczas łączenia tooMySQL.  Zaleca się unikać wyłączenie opcji SSL hello, jeśli to możliwe. 

Podczas inicjowania obsługi administracyjnej nowej bazy danych Azure MySQL serwerem za pośrednictwem hello portalu Azure i interfejsu wiersza polecenia, wymuszanie połączeń SSL jest domyślnie włączona. 

Podobnie parametry połączenia, które są wstępnie zdefiniowanego w ustawieniach "Parametry połączenia" hello, w obszarze serwera w portalu Azure hello uwzględnia hello wymagane parametry dla typowych języków tooconnect tooyour serwera bazy danych przy użyciu protokołu SSL. Witaj parametru SSL w zależności od hello łącznika, na przykład "ssl = true" lub "sslmode = wymagają" lub "sslmode = wymagane" i innych zmian.

jak tooenable lub wyłącz połączenia SSL podczas opracowywania aplikacji, zobacz zbyt toolearn[jak tooconfigure SSL](howto-configure-ssl.md).

## <a name="next-steps"></a>Następne kroki
[Biblioteki połączeń dla bazy danych Azure dla programu MySQL](concepts-connection-libraries.md)
