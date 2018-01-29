---
title: "Skonfiguruj parametry serwera w bazie danych Azure dla PostgreSQL za pośrednictwem portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób konfigurowania parametrów serwera w bazie danych Azure PostgreSQL za pośrednictwem portalu Azure."
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 11/08/2017
ms.openlocfilehash: 9e8262fbfcde2e69a656e356a7ab241f2d5043ad
ms.sourcegitcommit: 93902ffcb7c8550dcb65a2a5e711919bd1d09df9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/09/2017
---
# <a name="configure-server-parameters-in-azure-portal"></a>Skonfiguruj parametry serwera w portalu Azure
Można wyświetlić listę, wyświetlić i zaktualizować parametry konfiguracji bazy danych Azure PostgreSQL serwera za pośrednictwem portalu Azure.

## <a name="prerequisites"></a>Wymagania wstępne
Przez ten przewodnik krok po kroku, należy:
- [Azure bazy danych dla serwera PostgreSQL](quickstart-create-server-database-portal.md)

## <a name="viewing-and-editing-parameters"></a>Wyświetlanie i edytowanie parametrów
1. Otwórz [portal Azure](https://portal.azure.com).

2. Wybierz bazy danych Azure, PostgreSQL serwera.

3. W obszarze **ustawienia** zaznacz **parametry serwera**. Strona zawiera listę parametrów, ich wartości i opisy.
![Strona omówienia parametrów](./media/howto-configure-server-parameters-in-portal/3-overview-of-parameters.png)

4. Wybierz **listy rozwijanej** przycisk, aby wyświetlić możliwe wartości wyliczane typu parametry, takie jak client_min_messages.
![Wyliczanie listy w dół](./media/howto-configure-server-parameters-in-portal/4-enum-drop-down.png)

5. Wybierz lub umieść kursor nad **i** przycisk (informacje), aby wyświetlić zakres możliwe wartości liczbowe parametry, takie jak cpu_index_tuple_cost.
![przycisk informacje](./media/howto-configure-server-parameters-in-portal/4-information-button.png)

6. Jeśli to konieczne, użyj **pole wyszukiwania** do zawężania do określonego parametru. Wyszukiwanie znajduje się na nazwę i opis parametrów.
![Wyniki wyszukiwania](./media/howto-configure-server-parameters-in-portal/5-search.png)

7. Zmiany wartości parametrów, które chcesz dostosować. Wszystkie zmiany wprowadzone w sesji są wyróżnione na fioletowo. Po zmianie wartości, możesz wybrać **zapisać**. Można także **odrzucić** zmiany.
![Zapisz lub Odrzuć zmiany](./media/howto-configure-server-parameters-in-portal/6-save-and-discard-buttons.png)

8. Zapisanie nowej wartości parametrów można przywrócić wszystko, co do wartości domyślnych, wybierając **Resetuj wszystkie domyślne**.
![Resetuj wszystkie domyślne](./media/howto-configure-server-parameters-in-portal/7-reset-to-default-button.png)

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat:
- [Omówienie parametry serwera w bazie danych PostgreSQL Azure](concepts-servers.md)
- [Konfigurowanie parametrów przy użyciu wiersza polecenia platformy Azure](howto-configure-server-parameters-using-cli.md)
