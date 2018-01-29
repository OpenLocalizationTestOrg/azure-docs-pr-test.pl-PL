---
title: "Konfigurowanie i uzyskiwać dostęp do dzienników serwera dla PostgreSQL w portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób konfigurowania i uzyskiwać dostęp do dzienników serwera w bazie danych Azure dla PostgreSQL z portalu Azure."
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 10/19/2017
ms.openlocfilehash: a2f67b21293a1a0456b27cad9043be01fdd5274a
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2018
---
# <a name="configure-and-access-server-logs-in-the-azure-portal"></a>Konfigurowanie i dzienników serwera dostępu w portalu Azure

Można skonfigurować, listy i pobrać [bazy danych Azure do dzienników serwera PostgreSQL](concepts-server-logs.md) z portalu Azure.

## <a name="prerequisites"></a>Wymagania wstępne
Do wykonania kroków opisanych ten przewodnik, potrzebne są:
- [Azure bazy danych dla serwera PostgreSQL](quickstart-create-server-database-portal.md)

## <a name="configure-logging"></a>Konfigurowanie rejestrowania
Konfigurowanie dostępu do dzienników zapytania i dzienników błędów. 

1. Zaloguj się w [Portalu Azure](http://portal.azure.com/).

2. Wybierz bazy danych Azure, PostgreSQL serwera.

3. W obszarze **monitorowanie** sekcji na pasku bocznym wybierz **dzienniki serwera**. 

   ![Wybierz dzienniki serwera, a następnie wybierz pozycję "Kliknij tutaj, aby włączyć..."](./media/howto-configure-server-logs-in-portal/1-select-server-logs-configure.png)

4. Wybierz nagłówek **kliknij tutaj, aby włączyć dzienniki i skonfigurować parametry dziennika** można znaleźć w temacie parametry serwera.

5. Wybierz **Pokaż więcej** expander, aby zobaczyć rozszerzoną listę dostępnych parametrów. 

   Aby uzyskać więcej informacji na definicje parametrów, zobacz dokumentację PostgreSQL na [raportowanie błędów i rejestrowanie](https://www.postgresql.org/docs/current/static/runtime-config-logging.html).

   ![Krótką listę parametrów dziennika. Kliknij przycisk Pokaż więcej dla long](./media/howto-configure-server-logs-in-portal/2-show-more.png)

6. Zmień parametry, które należy skorygować. Wszystkie zmiany wprowadzone w tej sesji są wyróżnione na fioletowo.

   Po zmianie parametrów, możesz kliknąć **zapisać**. Można także **odrzucić** zmiany. 

   ![Długą listę parametrów z Zapisz lub Odrzuć zmiany](./media/howto-configure-server-logs-in-portal/3-save-discard.png)

7. Wróć do listy dzienników, klikając **przycisk Zamknij** (X ikona) na **parametry serwera** strony.

## <a name="view-list-and-download-logs"></a>Wyświetl listę i Pobierz dzienniki
Po rozpoczęciu rejestrowania, można wyświetlić listę dostępnych dzienników i pobrać osobnych plikach dziennika w okienku dzienniki serwera. 

1. Otwórz witrynę Azure Portal.

2. Wybierz bazy danych Azure, PostgreSQL serwera.

3. W obszarze **monitorowanie** sekcji na pasku bocznym wybierz **dzienniki serwera**. Strona zawiera listę plików dziennika, jak pokazano:

   ![Lista dzienników serwera](./media/howto-configure-server-logs-in-portal/4-server-logs-list.png)

   > [!TIP]
   > Konwencja nazewnictwa dziennika jest **postgresql rrrr mm-dd_hh0000.log**. Data i godzina w polu Nazwa pliku jest czas, gdy dziennik został wystawiony. Obróć plik dziennika co godzinę lub 100 MB rozmiar, zależnie od zostanie osiągnięty jako pierwszy.

4. Jeśli to konieczne, użyj **pole wyszukiwania** do szybkiego zawężania określonego dziennika według daty/godziny. Wyszukiwanie znajduje się na nazwę dziennika.

   ![Przykład wyszukiwania na nazwy dziennika](./media/howto-configure-server-logs-in-portal/5-search.png)

5. Pobierz pojedyncze pliki dziennika przy użyciu **Pobierz** przycisk (ikona strzałki w dół) obok każdego pliku dziennika, w wierszu tabeli, jak pokazano:

   ![Kliknij ikonę pobierania](./media/howto-configure-server-logs-in-portal/6-download.png)

## <a name="next-steps"></a>Kolejne kroki
- Zobacz [Access Server Logs WE CLI](howto-configure-server-logs-using-cli.md) Aby dowiedzieć się, jak pobrać dzienniki programowo.
- Dowiedz się więcej o [dzienniki serwera](concepts-server-logs.md) w usłudze Azure DB dla PostgreSQL. 
- Aby uzyskać więcej informacji o definicji parametrów i PostgreSQL rejestrowania, zobacz dokumentację PostgreSQL na [rejestrowania i raportowania błędów](https://www.postgresql.org/docs/current/static/runtime-config-logging.html).

