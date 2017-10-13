---
title: "Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tworzenia i zarządzania bazą danych Azure PostgreSQL reguł zapory przy użyciu wiersza polecenia z wiersza polecenia platformy Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 6f081416dd7d78f0153b3fda21a340a8c1a70c5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a>Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu wiersza polecenia platformy Azure
Reguły zapory poziomu serwera umożliwiają administratorom zarządzanie dostępem do bazy danych Azure PostgreSQL serwera z określonego adresu IP lub zakresu adresów IP. Za pomocą wygodny poleceń interfejsu wiersza polecenia Azure, możesz utworzyć, zaktualizować, Usuń listę i Pokaż reguły zapory do zarządzania serwerem. Omówienie bazy danych Azure dla zapór PostgreSQL, zobacz [bazą danych Azure dla reguł zapory serwera PostgreSQL](concepts-firewall-rules.md)

## <a name="prerequisites"></a>Wymagania wstępne
Do wykonania kroków opisanych ten przewodnik, potrzebne są:
- [Bazy danych Azure PostgreSQL serwera i bazy danych](quickstart-create-server-database-azure-cli.md)
- Zainstaluj [Azure CLI 2.0](/cli/azure/install-azure-cli) narzędzia wiersza polecenia lub użyć powłoki chmury Azure w przeglądarce.

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a>Konfigurowanie reguł zapory dla bazy danych platformy Azure dla PostgreSQL
[Az postgres reguły zapory serwera-](/cli/azure/postgres/server/firewall-rule) polecenia są używane do konfigurowania reguł zapory.

## <a name="list-firewall-rules"></a>Lista reguł zapory 
Aby wyświetlić listę istniejących reguł zapory serwera na serwerze, uruchom [listy reguły zapory serwera postgres az](/cli/azure/postgres/server/firewall-rule#list) polecenia.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
Dane wyjściowe wymieniono reguły, jeśli istnieje domyślnie w formacie JSON. Można użyć przełącznika `--output table` dla bardziej czytelnym formacie tabeli jako dane wyjściowe.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a>Tworzenie reguły zapory
Aby utworzyć nową regułę zapory na serwerze, uruchom [az postgres reguły zapory serwera — Utwórz](/cli/azure/postgres/server/firewall-rule#create) polecenia. 

W tym przykładzie umożliwia zakres wszystkie adresy IP na dostęp do serwera **mypgserver 20170401.postgres.database.azure.com**
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
Aby umożliwić pojedynczej adresu IP uzyskać dostęp, podaj ten sam adres Start IP i End IP, jak w poniższym przykładzie.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
Na sukces dane wyjściowe polecenia Wyświetla szczegóły reguły zapory, które zostały utworzone, domyślnie w formacie JSON. Jeśli występuje awaria, tekst komunikatu showserror danych wyjściowych.

## <a name="update-firewall-rule"></a>Aktualizuj reguły zapory 
Aktualizuj istniejącą regułę zapory na serwerze przy użyciu [aktualizacja reguły zapory serwera postgres az](/cli/azure/postgres/server/firewall-rule#update) polecenia. Podaj nazwę istniejącej reguły zapory jako dane wejściowe i uruchom atrybutów IP adresów IP i końcowy do aktualizacji.
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
Na sukces dane wyjściowe polecenia Wyświetla szczegóły reguły zapory, które zostały zaktualizowane, domyślnie w formacie JSON. Jeśli występuje awaria, tekst komunikatu showserror danych wyjściowych.
> [!NOTE]
> Jeśli reguły zapory nie istnieje, pobiera on utworzony za pomocą polecenia aktualizacji.

## <a name="show-firewall-rule-details"></a>Pokaż szczegóły reguły zapory
Szczegóły reguły dla serwera istniejących Zapora może także wyświetlać uruchamiając [Pokaż reguły zapory serwera postgres az](/cli/azure/postgres/server/firewall-rule#show) polecenia.
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Na sukces dane wyjściowe polecenia Wyświetla szczegóły reguły zapory, który został określony, domyślnie w formacie JSON. Jeśli występuje awaria, tekst komunikatu showserror danych wyjściowych.

## <a name="delete-firewall-rule"></a>Usuwanie reguły zapory
Aby odwołać dostępu dla zakresu adresów IP z serwera, usuń istniejącą regułę zapory, wykonując [az postgres reguły zapory serwera-Usuń](/cli/azure/postgres/server/firewall-rule#delete) polecenia. Podaj nazwę istniejącej reguły zapory.
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Na sukces nie ma żadnych danych wyjściowych. W przypadku awarii zwracana jest tekst komunikatu o błędzie.

## <a name="next-steps"></a>Następne kroki
- Analogicznie, można użyć przeglądarki sieci web [tworzenie i zarządzanie bazą danych Azure PostgreSQL reguł zapory przy użyciu portalu Azure](howto-manage-firewall-using-portal.md)
- Dowiedzieć się więcej o [bazą danych Azure dla reguł zapory serwera PostgreSQL](concepts-firewall-rules.md)
- Aby uzyskać pomoc w połączeniu z bazą danych PostgreSQL serwera Azure, zobacz [biblioteki połączeń dla bazy danych Azure dla PostgreSQL](concepts-connection-libraries.md)
