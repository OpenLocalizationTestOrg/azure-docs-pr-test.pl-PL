---
title: "aaaAzure architektury połączenia bazy danych SQL | Dokumentacja firmy Microsoft"
description: "W tym dokumencie opisano hello Azure SQLDB łączności architektury od Azure lub z poza platformą Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a>Architektura połączenia bazy danych Azure SQL 

W tym artykule opisano architektury połączenia bazy danych SQL Azure hello oraz wyjaśniono, jak hello różnych składników funkcji toodirect ruchu tooyour wystąpienia bazy danych SQL Azure. Te składniki łączności bazy danych SQL Azure funkcji toohello ruchu sieciowego toodirect bazy danych platformy Azure z klientów łączących się w obrębie platformy Azure i klientów łączących się z poza platformą Azure. Ten artykuł zawiera także jak łączność występuje toochange przykłady skryptów i hello zagadnienia związane z toochanging hello domyślnych łączności. Jeśli istnieją jakieś pytania po przeczytaniu tego artykułu, skontaktuj się z Dhruv na dmalik@microsoft.com. 

## <a name="connectivity-architecture"></a>Architektura łączności

powitania po diagram zawiera omówienie hello architektury połączenia bazy danych SQL Azure. 

![Przegląd architektury](./media/sql-database-connectivity-architecture/architecture-overview.png)


Witaj poniższych krokach opisano sposób połączenie jest ustalonych tooan bazy danych Azure SQL za pośrednictwem hello bazy danych SQL Azure oprogramowania do równoważenia obciążenia (Programowego) i hello bramy bazy danych SQL Azure.

- Klienci w obrębie platformy Azure lub na zewnątrz Azure łączyć toohello Programowego, który ma publicznego adresu IP i nasłuchuje na porcie 1433.
- Witaj Programowego kieruje ruch toohello bazy danych SQL Azure bramy.
- Brama Hello przekierowuje hello ruchu toohello poprawne serwera proxy w oprogramowaniu pośredniczącym.
- oprogramowanie pośredniczące serwera proxy Hello przekierowuje hello ruchu toohello odpowiednie bazy danych Azure SQL.

> [!IMPORTANT]
> Każdy z tych składników został rozesłany odmowa wbudowanych w sieci hello i warstwy aplikacji hello protection service (DDoS).
>

## <a name="connectivity-from-within-azure"></a>Łączność między w obrębie platformy Azure

Jeśli nawiązujesz w obrębie platformy Azure połączenia mają zasady połączenia **przekierowania** domyślnie. Zasady **przekierowania** oznacza, że połączenia bazy danych Azure SQL ustalonych toohello po sesji TCP hello powitania klienta sesji, a następnie przekierowanie oprogramowania pośredniczącego serwera proxy toohello z zmiany toohello docelowego wirtualnego adresu IP z który hello bazy danych SQL Azure bramy toothat oprogramowania pośredniczącego serwera proxy hello. Następnie wszystkie kolejne pakiety przepływać bezpośrednio za pomocą oprogramowania pośredniczącego serwera proxy hello, pomijanie hello bramy bazy danych SQL Azure. powitania po diagram ilustruje tego przepływu ruchu.

![Przegląd architektury](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a>Łączność z poza platformą Azure

Jeśli łączysz się z zewnętrznej platformy Azure, połączenia mają zasady połączenia **Proxy** domyślnie. Zasady **Proxy** oznacza, że ustanowieniu sesji TCP hello za pośrednictwem bramy bazy danych SQL Azure hello i wszystkie kolejne pakiety przepływu za pośrednictwem hello bramy. powitania po diagram ilustruje tego przepływu ruchu.

![Przegląd architektury](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a>Adresy IP bramy bazy danych SQL Azure

tooconnect tooan bazy danych Azure SQL z lokalnych zasobów, należy tooallow wychodzącego ruchu toohello bazy danych SQL Azure bramy w Twoim regionie Azure. Połączenia postępować tylko za pośrednictwem bramy hello podczas nawiązywania połączenia w trybie serwera Proxy, który jest domyślnym hello, podczas nawiązywania połączenia z zasobami lokalnymi.

Witaj w następującej tabeli przedstawiono hello głównych i dodatkowych adresów IP hello bramy bazy danych SQL Azure dla wszystkich obszarów danych. W pewnych regionach istnieją dwa adresy IP. W tych regionów hello podstawowy adres IP jest hello bieżącego adresu IP bramy hello i hello drugiego adresu IP jest adresem IP trybu failover. adres trybu failover Hello jest toowhich adres hello firma Microsoft może przenieść Twojej tookeep hello usługi dostępność serwera wysokiej. Dla tych regionów firma Microsoft zaleca Zezwalaj wychodzących tooboth hello adresy IP. Witaj drugiego adresu IP jest własnością firmy Microsoft i nie będzie nasłuchiwać na wszystkich usług, dopóki nie zostanie aktywowany przez połączenia tooaccept bazy danych SQL Azure.

| Nazwa regionu | Podstawowy adres IP | Pomocniczy adres IP |
| --- | --- |--- |
| Australia Wschodnia | 191.238.66.109 | 13.75.149.87 |
| Australia Południowo-Wschodnia | 191.239.192.109 | 13.73.109.251 |
| Brazylia Południowa | 104.41.11.5 | |    
| Kanada Środkowa | 40.85.224.249 | |    
| Kanada Wschodnia | 40.86.226.166 | |
| Środkowe stany USA | 23.99.160.139 | 13.67.215.62 |
| Azja Wschodnia | 191.234.2.139 | 52.175.33.150 |
| Wschodnie stany USA 1 | 191.238.6.43 | 40.121.158.30 |
| Wschodnie stany USA 2 | 191.239.224.107 | 40.79.84.180 |
| Indie Środkowe | 104.211.96.159  | |   
| Indie Południowe | 104.211.224.146  | |
| Indie Zachodnie | 104.211.160.80 | |
| Japonia Wschodnia | 191.237.240.43 | 13.78.61.196 |
| Japonia Zachodnia | 191.238.68.11 | 104.214.148.156 |
| Korea Środkowa | 52.231.32.42 | |
| Korea Południowa | 52.231.200.86 |  |
| Środkowo-północne stany USA | 23.98.55.75 | 23.96.178.199 |
| Europa Północna | 191.235.193.75 | 40.113.93.91 |
| Środkowo-południowe stany USA | 23.98.162.75 | 13.66.62.124 |
| Azja Południowo-Wschodnia | 23.100.117.95 | 104.43.15.0 |
| Północne Zjednoczone Królestwo | 13.87.97.210 | |
| Wielka Brytania Południowa 1 | 51.140.184.11 | |    
| Południowe Zjednoczone Królestwo 2 | 13.87.34.7 | |
| Zachodnie Zjednoczone Królestwo | 51.141.8.11  | |
| Środkowo-zachodnie stany USA | 13.78.145.25 | |
| Europa Zachodnia | 191.237.232.75 | 40.68.37.158 |
| Zachodnie stany USA 1 | 23.99.34.75 | 104.42.238.205 |
| Zachodnie stany USA 2 | 13.66.226.202  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a>Zmień zasady połączenia bazy danych SQL Azure

Witaj toochange zasady połączenia bazy danych SQL Azure dla serwera bazy danych SQL Azure, użyj hello [interfejsu API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx). 

- Jeśli zasady połączenia ustawiono zbyt**Proxy**, wszystkich sieci przepływu pakietów za pośrednictwem hello bramy bazy danych SQL Azure. Dla tego ustawienia należy IP bramy tooallow wychodzących tooonly hello bazy danych SQL Azure. Przy użyciu ustawienie **Proxy** ma opóźnienia więcej niż ustawienie **przekierowania**. 
- Jeśli to ustawienie zasad połączenia **przekierowania**, wszystkich pakietów sieciowych bezpośrednio przepływ toohello proxy oprogramowania pośredniczącego. Dla tego ustawienia należy tooallow toomultiple wychodzących adresów IP. 

## <a name="script-toochange-connection-settings"></a>Ustawienia połączenia toochange skryptu

> [!IMPORTANT]
> Ten skrypt wymaga hello [modułu Azure PowerShell](/powershell/azure/install-azurerm-ps).
>

Witaj następującego skryptu programu PowerShell pokazuje, jak toochange hello zasad połączenia.

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a>Następne kroki

- Informacje dotyczące sposobu toochange hello zasady połączenia bazy danych SQL Azure dla serwera bazy danych SQL Azure znajdują się w temacie [Create lub zasada połączenia serwera aktualizacji przy użyciu hello interfejsu API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).
- Uzyskać informacji dotyczących zachowania połączenia bazy danych SQL Azure dla klientów używających ADO.NET 4.5 lub nowszej wersji, zobacz [porty inne niż 1433 dla ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).
- Informacje ogólne programowanie ogólne aplikacji, zobacz [Omówienie projektowania aplikacji bazy danych SQL](sql-database-develop-overview.md).
