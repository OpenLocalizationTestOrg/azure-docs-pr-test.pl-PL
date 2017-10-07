---
title: "aaaCreate i zarządzanie bazą danych Azure PostgreSQL reguł zapory przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocreate i zarządzanie bazą danych Azure dla PostgreSQL reguł zapory przy użyciu wiersza polecenia z wiersza polecenia platformy Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a>Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu wiersza polecenia platformy Azure
Reguły zapory poziomu serwera włączyć tooan dostępu toomanage administratorów bazy danych Azure PostgreSQL serwera z określonego adresu IP lub zakresu adresów IP. Za pomocą wygodny poleceń interfejsu wiersza polecenia Azure, można utworzyć, zaktualizować, Usuń, listy i Pokaż toomanage reguł zapory serwera. Omówienie bazy danych Azure dla zapór PostgreSQL, zobacz [bazą danych Azure dla reguł zapory serwera PostgreSQL](concepts-firewall-rules.md)

## <a name="prerequisites"></a>Wymagania wstępne
toostep za pośrednictwem tego jak tooguide, potrzebne są:
- [Bazy danych Azure PostgreSQL serwera i bazy danych](quickstart-create-server-database-azure-cli.md)
- Zainstaluj [Azure CLI 2.0](/cli/azure/install-azure-cli) wiersza polecenia narzędzia lub użyj hello powłoki chmury Azure w przeglądarce hello.

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a>Konfigurowanie reguł zapory dla bazy danych platformy Azure dla PostgreSQL
Witaj [az postgres reguły zapory serwera-](/cli/azure/postgres/server/firewall-rule) reguły zapory tooconfigure używane są polecenia.

## <a name="list-firewall-rules"></a>Lista reguł zapory 
toolist hello istniejących reguł zapory serwera na powitania serwera, uruchom hello [listy reguły zapory serwera postgres az](/cli/azure/postgres/server/firewall-rule#list) polecenia.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
dane wyjściowe Hello wymieniono hello reguły formatowania żadnego domyślnie w formacie JSON. Można użyć przełącznika hello `--output table` dla bardziej czytelnym formacie tabeli jako dane wyjściowe hello.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a>Tworzenie reguły zapory
toocreate nowej reguły zapory na powitania serwera Uruchom hello [az postgres reguły zapory serwera — Utwórz](/cli/azure/postgres/server/firewall-rule#create) polecenia. 

W tym przykładzie umożliwia zakres wszystkich serwera hello tooaccess adresy IP **mypgserver 20170401.postgres.database.azure.com**
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
Podaj tooallow pojedynczej tooaccess adres IP hello tego samego adresu, jak hello Start adresów IP i końcowemu adresowi IP, jak w poniższym przykładzie.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
Na sukces dane wyjściowe polecenia hello Wyświetla szczegóły hello hello reguły zapory, które zostały utworzone, domyślnie w formacie JSON. W przypadku awarii, hello zamiast output showserror tekst komunikatu.

## <a name="update-firewall-rule"></a>Aktualizuj reguły zapory 
Aktualizuj istniejącą regułę zapory na powitania serwera przy użyciu [aktualizacja reguły zapory serwera postgres az](/cli/azure/postgres/server/firewall-rule#update) polecenia. Podaj nazwę hello hello istniejącą regułę zapory jako dane wejściowe i hello start adresów IP i końcowy IP atrybutów tooupdate.
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
Na sukces dane wyjściowe polecenia hello Wyświetla szczegóły hello hello reguły zapory, które zostały zaktualizowane, domyślnie w formacie JSON. W przypadku awarii, hello zamiast output showserror tekst komunikatu.
> [!NOTE]
> Jeśli nie istnieje reguła zapory hello, pobiera on utworzony za pomocą polecenia aktualizacji hello.

## <a name="show-firewall-rule-details"></a>Pokaż szczegóły reguły zapory
Szczegóły reguły dla serwera hello istniejących Zapora może także wyświetlać uruchamiając [Pokaż reguły zapory serwera postgres az](/cli/azure/postgres/server/firewall-rule#show) polecenia.
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Na sukces dane wyjściowe polecenia hello Wyświetla szczegóły hello hello reguły zapory, który został określony, domyślnie w formacie JSON. W przypadku awarii, hello zamiast output showserror tekst komunikatu.

## <a name="delete-firewall-rule"></a>Usuwanie reguły zapory
toorevoke dostępu dla zakresu adresów IP z serwera hello, usuń istniejącą regułę zapory, wykonując hello [az postgres reguły zapory serwera-Usuń](/cli/azure/postgres/server/firewall-rule#delete) polecenia. Podaj nazwę hello hello istniejącej reguły zapory.
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Na sukces nie ma żadnych danych wyjściowych. W przypadku awarii tekst komunikatu o błędzie hello jest zwracana.

## <a name="next-steps"></a>Następne kroki
- Podobnie za można używać przeglądarki sieci web[tworzenie i zarządzanie bazą danych Azure dla PostgreSQL reguł zapory przy użyciu hello portalu Azure](howto-manage-firewall-using-portal.md)
- Dowiedzieć się więcej o [bazą danych Azure dla reguł zapory serwera PostgreSQL](concepts-firewall-rules.md)
- Aby uzyskać pomoc w łączenie tooan Azure bazy danych dla serwera PostgreSQL, [biblioteki połączeń dla bazy danych Azure dla PostgreSQL](concepts-connection-libraries.md)
