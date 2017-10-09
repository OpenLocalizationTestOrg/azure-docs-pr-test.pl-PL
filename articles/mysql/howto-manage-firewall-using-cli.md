---
title: "aaaCreate i zarządzania nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocreate i zarządzania nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia z wiersza polecenia platformy Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure
Reguły zapory poziomu serwera włączyć tooan dostępu toomanage administratorów bazy danych Azure MySQL serwera z określonego adresu IP lub zakresu adresów IP. Za pomocą wygodny poleceń interfejsu wiersza polecenia Azure, można utworzyć, zaktualizować, Usuń, listy i Pokaż toomanage reguł zapory serwera. Omówienie bazy danych Azure dla zapór MySQL, zobacz [bazą danych Azure dla reguł zapory serwera MySQL](./concepts-firewall-rules.md)

## <a name="prerequisites"></a>Wymagania wstępne
* [Zainstaluj interfejs wiersza polecenia platformy Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)
* Zainstaluj Azure Python SDK dla usługi MySQL i PostgreSQL
* Zainstaluj składnik Azure CLI hello usług PostgreSQL i MySQL
* Tworzenie serwera usługi Azure Database for MySQL

## <a name="firewall-rule-commands"></a>Polecenia reguły zapory:
Witaj **az mysql reguły zapory serwera-** używane jest polecenie z wiersza polecenia platformy Azure toocreate, usunąć listy, wyświetlanie i aktualizowanie reguł zapory.

Polecenia:
- **Utwórz**: Tworzenie reguły zapory serwera Azure MySQL.
- **Usuń**: Usuń regułę zapory serwera Azure MySQL.
- **Lista** : lista reguł zapory serwera Azure MySQL hello.
- **Pokaż** : Pokaż szczegóły powitania serwera Azure MySQL reguły zapory.
- **Zaktualizuj**: aktualizowanie reguły zapory serwera Azure MySQL.

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a>TooAzure logowania i listy bazy danych Azure, serwerów MySQL
Bezpieczne łączenie wiersza polecenia platformy Azure z Twoim kontem platformy Azure. Użyj hello **logowania az** to polecenie toodo.

1. Uruchom następujące polecenie z wiersza polecenia hello hello.
```azurecli
az login
```
Toouse kodu, w następnym kroku hello będzie danych wyjściowych tego polecenia.

2. Użyj strony hello tooopen przeglądarki sieci web [https://aka.ms/devicelogin](https://aka.ms/devicelogin) i wprowadź kod hello.

3. W wierszu hello Zaloguj się przy użyciu poświadczeń konta platformy Azure.

4. Logowanie jest autoryzowany, w konsoli hello są drukowane listę subskrypcji. Skopiuj identyfikator hello hello potrzeby subskrypcji tooset hello bieżącej subskrypcji toobe używane przenoszenie do przodu.
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. Lista hello baz danych Azure, serwerów MySQL dla Twojej subskrypcji i grupie zasobów, w razie wątpliwości hello nazw.

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   Należy pamiętać, atrybut nazwy hello w hello wyświetlania, która będzie używana toospecify toowork serwera MySQL, które na. Jeśli to konieczne, potwierdź hello szczegóły dla tego serwera toousing hello nazwa atrybutu tooconfirm nazwa jest prawidłowa:

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>Lista reguł zapory na Azure bazy danych MySQL serwera 
Przy użyciu hello nazwę serwera i nazwa grupy zasobów hello, listy hello istniejących reguł zapory serwera na powitania serwera. Zwróć uwagę, ten atrybut nazwy serwera hello jest określona w hello **— serwer** przełącznika i nie hello **— nazwa** przełącznika.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
dane wyjściowe Hello znajduje się lista hello reguły formatowania żadnego domyślnie w formacie JSON. Można użyć przełącznika hello **--tabeli wyników** dla bardziej czytelnym formacie tabeli jako dane wyjściowe hello.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>Tworzenie reguły zapory na Azure bazy danych MySQL serwera
Przy użyciu hello Azure MySQL nazwę serwera i nazwa grupy zasobów hello, Utwórz nową regułę zapory na powitania serwera. Podaj nazwę reguły hello hello ustawiony początkowy adres IP i końcowemu adresowi IP dla hello toocover reguły dostępu tooallow adresów zakresu adresów IP.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
Dla pojedynczej adresów IP toobe zezwolenie na dostęp, podaj hello tego samego adresu, jak hello Start adresów IP i końcowemu adresowi IP, jak w poniższym przykładzie.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
Na sukces dane wyjściowe polecenia hello Wyświetla szczegóły hello hello reguły zapory, które zostały utworzone, domyślnie w formacie JSON. W przypadku awarii, dane wyjściowe hello Pokaż wtedy tekst komunikatu o błędzie.

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>Aktualizuj reguły zapory w bazie danych Azure MySQL serwera 
Przy użyciu hello Azure MySQL nazwę serwera i nazwa grupy zasobów hello, zaktualizuj istniejącą regułę zapory na powitania serwera. Podaj nazwę hello hello istniejącą regułę zapory jako dane wejściowe i hello start adresów IP i końcowy IP atrybutów tooupdate.
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
Na sukces dane wyjściowe polecenia hello Wyświetla szczegóły hello hello reguły zapory, które zostały zaktualizowane, domyślnie w formacie JSON. W przypadku awarii, dane wyjściowe hello Pokaż wtedy tekst komunikatu o błędzie.

> [!NOTE]
> Jeśli reguły zapory hello nie istnieje, zostanie utworzony przez polecenie aktualizacji hello.

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>Pokaż szczegóły reguły zapory w bazie danych systemu Azure dla serwera MySQL
Przy użyciu nazwy serwera Azure MySQL hello i nazwa grupy zasobów hello, zawierają hello istniejących zapory reguły szczegóły z serwera hello. Podaj nazwę hello hello istniejącą regułę zapory jako dane wejściowe.
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Na sukces dane wyjściowe polecenia hello znajduje się lista szczegółów hello hello reguły zapory, który został określony, domyślnie w formacie JSON. W przypadku awarii, dane wyjściowe hello Pokaż wtedy tekst komunikatu o błędzie.

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>Usuwanie reguły zapory w bazie danych Azure MySQL serwera
Przy użyciu hello Azure MySQL nazwę serwera i nazwa grupy zasobów hello, usuń istniejącą regułę zapory z powitania serwera. Podaj nazwę hello hello istniejącej reguły zapory.
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Na sukces nie ma żadnych danych wyjściowych. W przypadku awarii zostanie zwrócony tekst komunikatu o błędzie hello.

## <a name="next-steps"></a>Następne kroki
- Dowiedzieć się więcej o [bazą danych Azure dla reguł zapory serwera MySQL](./concepts-firewall-rules.md)
- [Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu hello portalu Azure](./howto-manage-firewall-using-portal.md)
