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
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="82309-103">Połączenie SSL w bazie danych Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="82309-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="82309-104">Bazy danych platformy Azure dla programu MySQL obsługuje łączenie aplikacji tooclient serwera bazy danych przy użyciu protokołu Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="82309-104">Azure Database for MySQL supports connecting your database server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="82309-105">Wymuszanie połączenia SSL między serwerem bazy danych i aplikacji klienckich pomaga chronić przed atakami "man w środku powitania" hello strumienia danych między serwerem hello i aplikacji są szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="82309-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="82309-106">Ustawienia domyślne</span><span class="sxs-lookup"><span data-stu-id="82309-106">Default settings</span></span>
<span data-ttu-id="82309-107">Domyślnie hello bazy danych usługi powinien być skonfigurowany toorequire połączeń SSL podczas łączenia tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="82309-107">By default, hello database service should be configured toorequire SSL connections when connecting tooMySQL.</span></span>  <span data-ttu-id="82309-108">Zaleca się unikać wyłączenie opcji SSL hello, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="82309-108">It is recommended avoid disabling hello SSL option whenever possible.</span></span> 

<span data-ttu-id="82309-109">Podczas inicjowania obsługi administracyjnej nowej bazy danych Azure MySQL serwerem za pośrednictwem hello portalu Azure i interfejsu wiersza polecenia, wymuszanie połączeń SSL jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="82309-109">When provisioning a new Azure Database for MySQL server through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="82309-110">Podobnie parametry połączenia, które są wstępnie zdefiniowanego w ustawieniach "Parametry połączenia" hello, w obszarze serwera w portalu Azure hello uwzględnia hello wymagane parametry dla typowych języków tooconnect tooyour serwera bazy danych przy użyciu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="82309-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="82309-111">Witaj parametru SSL w zależności od hello łącznika, na przykład "ssl = true" lub "sslmode = wymagają" lub "sslmode = wymagane" i innych zmian.</span><span class="sxs-lookup"><span data-stu-id="82309-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="82309-112">jak tooenable lub wyłącz połączenia SSL podczas opracowywania aplikacji, zobacz zbyt toolearn[jak tooconfigure SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="82309-112">toolearn how tooenable or disable SSL connection when developing application, please refer too[How tooconfigure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82309-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="82309-113">Next steps</span></span>
[<span data-ttu-id="82309-114">Biblioteki połączeń dla bazy danych Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="82309-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
