---
title: "aaaCreate i zarządzanie bazą danych Azure dla serwera MySQL przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak szybko utworzyć nową bazę danych Azure MySQL serwera i zarządzanie serwerem hello za pomocą hello portalu Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a>Tworzenie i zarządzanie Azure bazy danych dla serwera MySQL przy użyciu portalu Azure
W tym artykule opisano, jak szybko utworzyć nową bazę danych Azure MySQL serwera i zarządzanie serwerem hello za pomocą hello portalu Azure. Zarządzanie serwerem obejmuje wyświetlanie szczegółów serwera & bazy danych, resetowanie hasła i usuwanie powitania serwera.

## <a name="log-in-toohello-azure-portal"></a>Zaloguj się za toohello portalu Azure
Zaloguj się za toohello [portalu Azure](https://portal.azure.com).

## <a name="create-an-azure-database-for-mysql-server"></a>Tworzenie serwera usługi Azure Database for MySQL
Wykonaj te kroki toocreate bazy danych Azure programu MySQL serwer o nazwie "mysqlserver4demo"

Kliknij przycisk 1 **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.

Wybierz opcję 2 **baz danych** z hello nowej strony, a następnie wybierz **bazy danych Azure dla programu MySQL** ze strony baz danych hello.

> Baza danych Azure dla serwera MySQL jest tworzony z zdefiniowanego zestawu [obliczeniowej i pamięci masowej](./concepts-compute-unit-and-storage.md) zasobów. Witaj baza danych została utworzona, w ramach grupy zasobów platformy Azure i w bazie danych Azure dla serwera MySQL.

![Utwórz nowy serwera](./media/howto-create-manage-server-portal/create-new-server.png)

3 - wypełnić hello Azure bazy danych MySQL formularza z hello następujących informacji:

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

Kliknij przycisk 4 **warstwa cenowa** toospecify hello warstwę i poziom wydajności usługi dla nowego serwera. Obliczenia bazy danych od 50 do 100 w warstwie podstawowa, 100 i 200 w warstwie standardowa, można skonfigurować jednostki i Magazyn można dodać zależności od uwzględniona ilość. Ten przewodnik Porada umożliwia wybierz 50 Jednostka obliczeniowa i 50GB. Kliknij przycisk **OK** toosave wybór.
![Utwórz server--warstwy cenowej](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

Kliknij przycisk 5 **Utwórz** tooprovision powitania serwera. Aprowizacja zajmuje kilka minut.

> Sprawdź hello **toodashboard numeru Pin** opcji tooallow łatwe monitorowanie wdrożeń.
> [!NOTE]
> Mimo że too1000GB w warstwie podstawowa i 10000GB w standardzie warstwy będą obsługiwane dla magazynu, dla publicznej wersji zapoznawczej, pamięci masowej hello jest tymczasowo too1000GB nadal ograniczone. 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a>Aktualizacja bazy danych Azure dla serwera MySQL
Po udostępnieniu nowego serwera użytkownik ma 2 tooedit opcje istniejącego serwera: resetowanie hasła administratora lub skalowania w górę/dół powitania serwera, zmieniając hello obliczeń jednostki.

### <a name="change-hello-administrator-user-password"></a>Zmienianie hasła użytkownika administratora hello
1 — na serwerze hello **omówienie** bloku, kliknij przycisk **resetowania hasła** toopopulate okna wprowadzania i potwierdzenie hasła.

2 — wprowadź nowe hasło i potwierdzenie hasła hello w oknie hello zgodnie z poniższymi instrukcjami: ![resetowania hasła](./media/howto-create-manage-server-portal/reset-password.png)

Kliknij 3 **OK** toosave hello nowe hasło.

### <a name="scale-updown-by-changing-compute-units"></a>Skalowanie w górę/dół zmieniając obliczeniowe jednostki

1 - na powitania serwera bloku w obszarze **ustawienia**, kliknij przycisk **warstwa cenowa** bloku warstwa cenowa tooopen hello, hello Azure bazy danych dla serwera MySQL.

2-wykonaj krok 4 w **utworzenia bazy danych MySQL serwera Azure** toochange obliczeniowe jednostki w hello samą warstwę cenową.

## <a name="delete-an-azure-database-for-mysql-server"></a>Usuwanie bazy danych Azure dla serwera MySQL

1 - na powitania serwera **omówienie** bloku, kliknij przycisk **usunąć** polecenia przycisk tooopen hello usunięcie potwierdzenie bloku.

Typ 2 hello poprawną nazwę serwera w polu wejściowym hello bloku o potwierdzenie dwa razy.

Kliknij 3 **usunąć** ponownie przycisk usuwania akcji tooconfirm i poczekaj "Usuwanie sukces" popup na powitania pasek powiadomień.

## <a name="list-hello-azure-database-for-mysql-databases"></a>Lista hello Azure bazy danych dla baz danych MySQL
Na serwerze hello **omówienie** bloku, przewiń w dół, aż zostanie wyświetlony hello bazy danych kafelka na dole hello. Wszystkie hello bazy danych będzie wyświetlane w tabeli hello. Kliknij przycisk **usunąć** polecenia przycisk tooopen hello usunięcie potwierdzenie bloku.

![Pokaż-baz danych](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a>Pokaż szczegóły bazy danych MySQL serwera Azure
Kliknij przycisk **właściwości** w obszarze **ustawienia** na powitania serwera zostanie otwarty hello blok **właściwości** bloku. Następnie można wyświetlić wszystkie szczegółowe informacje o serwerze hello.

## <a name="next-steps"></a>Następne kroki

[Szybki Start: Tworzenie bazy danych platformy Azure dla serwera MySQL przy użyciu portalu Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
