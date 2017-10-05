---
title: "Tworzenie i zarządzanie Azure bazy danych dla serwera MySQL przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak szybko utworzyć nową bazę danych Azure dla serwera MySQL i zarządzanie serwerem przy użyciu portalu Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4605518b6955d9943e76c25df2d4105a6a94433d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a>Tworzenie i zarządzanie Azure bazy danych dla serwera MySQL przy użyciu portalu Azure
W tym artykule opisano, jak szybko utworzyć nową bazę danych Azure dla serwera MySQL i zarządzanie serwerem przy użyciu portalu Azure. Zarządzanie serwerem obejmuje wyświetlanie szczegółów serwera & bazy danych, resetowanie hasła i usunięcie serwera.

## <a name="log-in-to-the-azure-portal"></a>Logowanie do witryny Azure Portal
Zaloguj się do witryny [Azure Portal](https://portal.azure.com).

## <a name="create-an-azure-database-for-mysql-server"></a>Tworzenie serwera usługi Azure Database for MySQL
Wykonaj następujące kroki, aby utworzyć bazę danych Azure MySQL serwera o nazwie "mysqlserver4demo"

Kliknij przycisk 1 **nowy** znaleziono przycisku w lewym górnym rogu portalu Azure.

Wybierz opcję 2 **baz danych** z nowej strony, a następnie wybierz **bazy danych Azure dla programu MySQL** ze strony baz danych.

> Baza danych Azure dla serwera MySQL jest tworzony z zdefiniowanego zestawu [obliczeniowej i pamięci masowej](./concepts-compute-unit-and-storage.md) zasobów. Baza danych została utworzona w ramach grupy zasobów platformy Azure i w bazie danych Azure dla serwera MySQL.

![Utwórz nowy serwera](./media/howto-create-manage-server-portal/create-new-server.png)

3 - Wypełnianie bazy danych Azure MySQL formularza z następującymi informacjami:

| **Pole formularza** | **Opis pola** |
|----------------|-----------------------|
| *Nazwa serwera* | Azure mysql (nazwa serwera jest globalnie unikatowa) |
| *Subskrypcja* | MySQLaaS (wybierz z listy rozwijanej) |
| *Grupa zasobów* | myresource (Utwórz nową grupę zasobów lub użyć istniejącego) |
| *Identyfikator logowania administratora serwera* | myadmin (skonfiguruj nazwę konta administratora) |
| *Hasło* | ustawienia hasła do konta administratora |
| *Potwierdź hasło* | potwierdź hasło konta administratora |
| *Lokalizacja* | Europa Północna (wybór między Europa Północna, Europa i zachodnie stany USA) |
| *Wersja* | 5.6 (Wybierz bazy danych Azure w wersji server MySQL) |

Kliknij przycisk 4 **warstwa cenowa** umożliwia określenie poziomu wydajności i warstwy usługi dla nowego serwera. Obliczenia bazy danych od 50 do 100 w warstwie podstawowa, 100 i 200 w warstwie standardowa, można skonfigurować jednostki i Magazyn można dodać zależności od uwzględniona ilość. Ten przewodnik Porada umożliwia wybierz 50 Jednostka obliczeniowa i 50GB. Kliknij przycisk **OK** Aby zapisać wybrane opcje.
![Utwórz server--warstwy cenowej](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

Kliknij przycisk 5 **Utwórz** do udostępnienia serwera. Aprowizacja zajmuje kilka minut.

> Zaznacz opcję **Przypnij do pulpitu nawigacyjnego**, aby łatwo śledzić wdrożenia.
> [!NOTE]
> Mimo że maksymalnie 1000GB w warstwie podstawowa i 10000 w warstwie standardowa będą obsługiwane dla magazynu, dla publicznej wersji zapoznawczej, pamięci masowej, jest ona nadal maksymalnie 1000GB tymczasowo. 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a>Aktualizacja bazy danych Azure dla serwera MySQL
Po udostępnieniu nowego serwera użytkownik ma 2 opcje do edycji istniejącego serwera: resetowanie hasła administratora lub skalowania w górę/dół serwera, zmieniając jednostki obliczeń.

### <a name="change-the-administrator-user-password"></a>Zmień hasło użytkownika administratora
1 — na serwerze **omówienie** bloku, kliknij przycisk **resetowania hasła** do wypełnienia okna wprowadzania i potwierdzenie hasła.

2 — wprowadź nowe hasło i Potwierdź hasło w oknie, jak pokazano poniżej: ![resetowania hasła](./media/howto-create-manage-server-portal/reset-password.png)

Kliknij 3 **OK** można zapisać nowego hasła.

### <a name="scale-updown-by-changing-compute-units"></a>Skalowanie w górę/dół zmieniając obliczeniowe jednostki

1 — w bloku serwera w obszarze **ustawienia**, kliknij przycisk **warstwa cenowa** aby otworzyć blok warstwa cenowa Azure bazy danych MySQL serwera.

2-wykonaj krok 4 w **utworzenia bazy danych MySQL serwera Azure** zmiany obliczeniowe jednostki w tej samej warstwie cenowej.

## <a name="delete-an-azure-database-for-mysql-server"></a>Usuwanie bazy danych Azure dla serwera MySQL

1 — na serwerze **omówienie** bloku, kliknij przycisk **usunąć** przycisku polecenia, aby otworzyć blok potwierdzający usunięcie.

2 — wpisz prawidłową nazwę serwera w polu wejściowym bloku o potwierdzenie dwa razy.

Kliknij 3 **usunąć** przycisk ponownie, aby potwierdzić usunięcie akcji i poczekaj, aż "Usuwanie sukces" popup na pasku powiadomień.

## <a name="list-the-azure-database-for-mysql-databases"></a>Lista Azure bazy danych dla baz danych MySQL
Na serwerze **omówienie** bloku, przewiń w dół, aż zostanie wyświetlony Kafelek na dole bazy danych. Wszystkie bazy danych będzie wyświetlane w tabeli. Kliknij przycisk **usunąć** przycisku polecenia, aby otworzyć blok potwierdzający usunięcie.

![Pokaż-baz danych](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a>Pokaż szczegóły bazy danych MySQL serwera Azure
Kliknij przycisk **właściwości** w obszarze **ustawienia** na serwerze zostanie otwarty blok **właściwości** bloku. Następnie można wyświetlić wszystkie szczegółowe informacje o serwerze.

## <a name="next-steps"></a>Następne kroki

[Szybki Start: Tworzenie bazy danych platformy Azure dla serwera MySQL przy użyciu portalu Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
