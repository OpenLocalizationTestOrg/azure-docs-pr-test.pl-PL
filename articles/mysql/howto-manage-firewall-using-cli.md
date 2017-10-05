---
title: "Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tworzenia i zarządzania nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia z wiersza polecenia platformy Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 9a03722e9f71be307bdbf0b846a4cbf7b34cd7ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure
Reguły zapory poziomu serwera umożliwiają administratorom zarządzanie dostępem do bazy danych Azure MySQL serwera z określonego adresu IP lub zakresu adresów IP. Za pomocą wygodny poleceń interfejsu wiersza polecenia Azure, możesz utworzyć, zaktualizować, Usuń listę i Pokaż reguły zapory do zarządzania serwerem. Omówienie bazy danych Azure dla zapór MySQL, zobacz [bazą danych Azure dla reguł zapory serwera MySQL](./concepts-firewall-rules.md)

## <a name="prerequisites"></a>Wymagania wstępne
* [Zainstaluj interfejs wiersza polecenia platformy Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)
* Zainstaluj Azure Python SDK dla usługi MySQL i PostgreSQL
* Zainstaluj składnik wiersza polecenia platformy Azure dla usług PostgreSQL i MySQL
* Tworzenie serwera usługi Azure Database for MySQL

## <a name="firewall-rule-commands"></a>Polecenia reguły zapory:
**Az mysql reguły zapory serwera-** polecenie służy do tworzenia, usuwania, listy, Pokaż i zaktualizować reguł zapory z wiersza polecenia platformy Azure.

Polecenia:
- **Utwórz**: Tworzenie reguły zapory serwera Azure MySQL.
- **Usuń**: Usuń regułę zapory serwera Azure MySQL.
- **Lista** : lista reguł zapory serwera Azure MySQL.
- **Pokaż** : Pokaż szczegóły serwera Azure MySQL reguły zapory.
- **Zaktualizuj**: aktualizowanie reguły zapory serwera Azure MySQL.

## <a name="login-to-azure-and-list-your-azure-database-for-mysql-servers"></a>Logowanie do platformy Azure i listy Azure bazy danych dla serwerów MySQL
Bezpieczne łączenie wiersza polecenia platformy Azure z Twoim kontem platformy Azure. Użyj **logowania az** polecenie, aby to zrobić.

1. W wierszu polecenia uruchom następujące polecenie.
```azurecli
az login
```
To polecenie zwróci kod, którego należy użyć w następnym kroku.

2. W przeglądarce sieci Web otwórz stronę [https://aka.ms/devicelogin](https://aka.ms/devicelogin) i wprowadź kod.

3. Po wyświetleniu monitu zaloguj się przy użyciu swoich poświadczeń platformy Azure.

4. Autoryzowany logowanie listę subskrypcji będą wypisywane w konsoli. Skopiuj identyfikator żądanego subskrypcji można ustawić bieżącej subskrypcji do użycia przenoszenie do przodu.
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. Lista baz danych Azure, serwerów MySQL dla Twojej subskrypcji i grupie zasobów, jeśli nie wiesz o nazwach.

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   Należy pamiętać, atrybut nazwy na liście, która będzie używana do określenia, który serwer MySQL do pracy w. Jeśli to konieczne, Potwierdź szczegóły dla tego serwera, aby upewnić się, czy nazwa jest prawidłowa przy użyciu atrybutu name:

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>Lista reguł zapory na Azure bazy danych MySQL serwera 
Przy użyciu nazwy serwera i nazwa grupy zasobów, Wyświetl listę istniejących reguł zapory serwera na serwerze. Należy zauważyć, że nazwa serwera jest określony w **--server** przełącznika i nie **— nazwa** przełącznika.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
Dane wyjściowe wyświetli listę reguł, jeśli istnieje domyślnie w formacie JSON. Można użyć przełącznika **--tabeli wyników** dla bardziej czytelnym formacie tabeli jako dane wyjściowe.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>Tworzenie reguły zapory na Azure bazy danych MySQL serwera
Przy użyciu nazwy serwera Azure MySQL i nazwę grupy zasobów, Utwórz nową regułę zapory na serwerze. Podaj nazwę reguły, ustawiony początkowy adres IP i końcowemu adresowi IP reguły, aby pokryć zakres adresów IP zezwolić na dostęp.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
Dla pojedynczej adresu IP zezwolić na dostęp Podaj ten sam adres Start IP i End IP, jak w poniższym przykładzie.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
Na sukces dane wyjściowe polecenia Wyświetla szczegóły reguły zapory, które zostały utworzone, domyślnie w formacie JSON. W przypadku awarii, dane wyjściowe Pokaż wtedy tekst komunikatu o błędzie.

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>Aktualizuj reguły zapory w bazie danych Azure MySQL serwera 
Przy użyciu nazwy serwera Azure MySQL i nazwę grupy zasobów, zaktualizuj istniejącą regułę zapory na serwerze. Podaj nazwę istniejącej reguły zapory jako dane wejściowe i uruchom atrybutów IP adresów IP i końcowy do aktualizacji.
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
Na sukces dane wyjściowe polecenia Wyświetla szczegóły reguły zapory, które zostały zaktualizowane, domyślnie w formacie JSON. W przypadku awarii, dane wyjściowe Pokaż wtedy tekst komunikatu o błędzie.

> [!NOTE]
> Jeśli reguły zapory nie istnieje, zostanie utworzony za pomocą polecenia aktualizacji.

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>Pokaż szczegóły reguły zapory w bazie danych systemu Azure dla serwera MySQL
Przy użyciu nazwy serwera Azure MySQL i nazwę grupy zasobów, Pokaż szczegóły reguły z serwera istniejącą zapory. Podaj nazwę istniejącej reguły zapory jako dane wejściowe.
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Na sukces dane wyjściowe polecenia Wyświetla szczegóły reguły zapory, który został określony, domyślnie w formacie JSON. W przypadku awarii, dane wyjściowe Pokaż wtedy tekst komunikatu o błędzie.

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>Usuwanie reguły zapory w bazie danych Azure MySQL serwera
Przy użyciu nazwy serwera Azure MySQL i nazwę grupy zasobów, usuń istniejącą regułę zapory z serwera. Podaj nazwę istniejącej reguły zapory.
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Na sukces nie ma żadnych danych wyjściowych. W przypadku awarii zostanie zwrócony tekst komunikatu o błędzie.

## <a name="next-steps"></a>Następne kroki
- Dowiedzieć się więcej o [bazą danych Azure dla reguł zapory serwera MySQL](./concepts-firewall-rules.md)
- [Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu portalu Azure](./howto-manage-firewall-using-portal.md)
