---
title: Jak tooback zapasowych i przywracania serwera w bazie danych Azure dla PostgreSQL | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooback zapasowej i przywracanie serwera w bazie danych Azure PostgreSQL przy użyciu hello wiersza polecenia platformy Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a>Jak tooback zapasowej i przywracanie serwera w bazie danych Azure PostgreSQL przy użyciu hello wiersza polecenia platformy Azure

Użyj bazy danych platformy Azure dla toorestore PostgreSQL tooan bazy danych serwera wcześniejszą datę, która jest liczony od 7 dni too35.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete to tooguide jak należy:
- [Bazy danych Azure PostgreSQL serwera i bazy danych](quickstart-create-server-database-azure-cli.md)

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> Jeśli został zainstalowany, użyj hello Azure CLI lokalnie to tooguide jak wymaga użycia interfejsu wiersza polecenia Azure w wersji 2.0 lub nowszej. Wprowadź tooconfirm hello wersji, w wierszu polecenia interfejsu wiersza polecenia Azure hello `az --version`. tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="back-up-happens-automatically"></a>Tworzenie kopii zapasowej odbywa się automatycznie
Gdy używasz bazy danych Azure PostgreSQL, hello bazy danych usługi automatycznie sprawia, że kopia zapasowa usługi hello co 5 minut. 

Dla warstwy Basic kopie zapasowe hello są dostępne przez 7 dni. Dla warstwy standardowa kopie zapasowe hello są dostępne dla 35 dni. Aby uzyskać więcej informacji, zobacz [bazą danych Azure dla PostgreSQL warstw cenowych](concepts-service-tiers.md).

Z automatycznej funkcji Kopia zapasowa można przywrócić wcześniejszą datę powitania serwera i jego tooan baz danych lub punktu w czasie.

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a>Przywracanie bazy danych tooa poprzedniego punktu w czasie przy użyciu interfejsu wiersza polecenia Azure hello
Na użytek bazy danych Azure PostgreSQL toorestore powitania serwera tooa wcześniejszego punktu w czasie. Hello przywrócić dane są kopiowane tooa nowy serwer, a hello istniejącego serwera pozostanie niezmieniona. Na przykład w tabeli jest przypadkowo usunięte w południe dzisiaj, można przywrócić czasu toohello tuż przed południe. Następnie można pobrać hello Brak tabeli i danych z hello przywrócić kopię powitania serwera. 

toorestore powitania serwera, użyj hello Azure CLI [przywracania serwera postgres az](/cli/azure/postgres/server#restore) polecenia.

### <a name="run-hello-restore-command"></a>Uruchom polecenie restore hello

toorestore powitania serwera, w wierszu polecenia interfejsu wiersza polecenia Azure hello, wprowadź następujące polecenie hello:

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Witaj `az postgres server restore` polecenie wymaga hello następujące parametry:
| Ustawienie | Sugerowana wartość | Opis  |
| --- | --- | --- |
| grupy zasobów |  myResourceGroup |  Grupy zasobów, gdy istnieje powitania serwera źródłowego.  |
| name | przywrócona mypgserver | Nazwa Hello hello nowy serwer, który jest tworzony przez polecenie restore hello. |
| Przywracanie punktu w czasie | 2017-04-13T13:59:00Z | Wybieranie punktu w czasie toorestore do. Ta data i godzina musi należeć powitania serwera źródłowego kopii zapasowych okresu przechowywania. Użyj hello ISO8601 format daty i godziny. Na przykład można własnej lokalnej strefie czasowej, takich jak `2017-04-13T05:59:00-08:00`. Można również użyć hello sformatować UTC Zulu, na przykład `2017-04-13T13:59:00Z`. |
| Serwer źródłowy | mypgserver 20170401 | Witaj, nazwa lub identyfikator toorestore serwera źródłowego hello z. |

Po przywróceniu tooan serwera wcześniejszego punktu w czasie, jest tworzony nowy serwer. Witaj oryginalnego określić serwer i jej baz danych z hello punktu w czasie są kopiowane toohello nowego serwera.

wartości warstwy Hello lokalizacji i cenach dla serwera hello przywrócić pozostają hello sam jako hello oryginalny serwer. 

Witaj `az postgres server restore` polecenie jest synchroniczne. Po przywróceniu serwera hello umożliwia ponownie toorepeat hello proces dla różnych punktu w czasie. 

Po hello zakończenie procesu przywracania, Znajdź hello nowego serwera i sprawdź, czy dane hello są przywracane zgodnie z oczekiwaniami.

## <a name="next-steps"></a>Następne kroki
[Biblioteki połączeń dla bazy danych Azure dla PostgreSQL](concepts-connection-libraries.md)
