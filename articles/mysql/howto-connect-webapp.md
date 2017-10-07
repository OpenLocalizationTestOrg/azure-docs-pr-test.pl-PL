---
title: "aaaConnect istniejącej usługi aplikacji Azure tooAzure bazy danych dla programu MySQL | Dokumentacja firmy Microsoft"
description: "Instrukcje dotyczące sposób łączenia tooproperly tooAzure usłudze Azure App Service istniejącej bazy danych dla programu MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a>Połącz istniejące usługi Azure App Service tooAzure bazy danych MySQL serwera
W tym dokumencie opisano sposób tooconnect istniejących tooyour usłudze Azure App Service MySQL serwera bazy danych Azure.

## <a name="before-you-begin"></a>Przed rozpoczęciem
Zaloguj się za toohello [portalu Azure](https://portal.azure.com). Utwórz bazę danych Azure dla serwera MySQL. Aby uzyskać więcej informacji, zobacz zbyt[jak toocreate Azure bazy danych MySQL serwera z portalu](quickstart-create-mysql-server-database-using-azure-portal.md) lub [jak toocreate Azure bazy danych MySQL serwera przy użyciu interfejsu wiersza polecenia](quickstart-create-mysql-server-database-using-azure-cli.md).

Obecnie istnieją dwa dostęp tooenable rozwiązań z usługi aplikacji Azure tooan bazy danych Azure dla programu MySQL. Oba rozwiązania wymagają konfigurowania reguł zapory na poziomie serwera.

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a>Rozwiązanie 1 — Tworzenie tooallow reguły zapory wszystkich adresów IP
Bazy danych platformy Azure dla programu MySQL zapewnia zabezpieczenia dostępu przy użyciu tooprotect zapory danych. Gdy łączących się z usługi aplikacji Azure tooAzure bazy danych MySQL serwera, należy pamiętać, że hello wychodzących adresów IP z usługi aplikacji są dynamiczne charakter. 

dostępność hello tooensure usłudze Azure App Service, firma Microsoft zaleca używanie tego rozwiązania tooallow wszystkich adresów IP.

> [!NOTE]
> Firma Microsoft współpracuje dla długoterminowego tooavoid rozwiązanie umożliwiający wszystkie adresy IP dla usług Azure tooconnect tooAzure bazy danych MySQL.

1. W bloku serwera MySQL hello, w obszarze Ustawienia kliknij pozycję **zabezpieczenia połączeń** tooopen hello zabezpieczenia połączeń bloku hello Azure bazy danych MySQL.

   ![Portal Azure — kliknij przycisk Zabezpieczenia połączeń](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Wprowadź **Nazwa reguły**, **ustawiony POCZĄTKOWY adres IP**, i **KOŃCOWEMU adresowi IP**. Następnie kliknij przycisk **Save** (Zapisz).
   - Nazwa reguły: Zezwalaj-All-adresów IP
   - Uruchom IP: 0.0.0.0
   - Zakończenie IP: 255.255.255.255

   ![Portal Azure — Dodaj wszystkie adresy IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a>Rozwiązanie 2 — Tworzenie Zapora tooexplicitly reguły Zezwalaj wychodzących adresów IP
Można jawnie dodać wszystkie hello wychodzących adresów IP z usługi aplikacji platformy Azure.

1. W bloku właściwości usługi aplikacji hello, wyświetlanie użytkownika **WYCHODZĄCY adres IP**.

   ![Portal Azure — widok wychodzących adresów IP](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. W bloku zabezpieczeń połączenia MySQL hello Dodaj wychodzących adresów IP pojedynczo.

   ![Portal Azure — Dodaj jawne adresów IP](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. Należy pamiętać, zbyt**zapisać** reguł zapory.

Chociaż hello Azure App service próbuje stała adresy IP tookeep wraz z upływem czasu, istnieją przypadki, w którym może zmienić hello adresów IP. Na przykład gdy hello odtwarza aplikacji występuje operacji skalowania lub dodania nowych maszyn w danych Azure regionalnych centrach tooincrease hello pojemności. Podczas zmiany adresów hello IP, aplikacja hello można przestój w przypadku hello nie można już połączyć toohello MySQL serwera. W przypadku wybrania jednej hello poprzedzających rozwiązania należy wziąć pod uwagę tej możliwości.

## <a name="ssl-configuration"></a>Konfiguracja protokołu SSL
Bazy danych platformy Azure dla programu MySQL jest domyślnie włączony protokół SSL. Jeśli aplikacja nie używa protokołu SSL tooconnect toohello w bazie danych, należy toodisable SSL na serwerze MySQL. Aby uzyskać więcej informacji na temat protokołu SSL, zobacz tooconfigure [przy użyciu protokołu SSL z bazą danych Azure dla programu MySQL](howto-configure-ssl.md).

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji dotyczących parametrów połączenia, można znaleźć zbyt[parametry połączenia](howto-connection-string.md).
