---
title: tooRestore aaaHow serwera w bazie danych Azure dla programu MySQL | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób toorestore serwera w bazie danych Azure poświęcone MySQL hello portalu Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a>Jak tooBackup i przywracania serwera w bazie danych Azure poświęcone MySQL hello portalu Azure

## <a name="backup-happens-automatically"></a>Kopia zapasowa jest wykonywana automatycznie
Korzystając z bazy danych platformy Azure dla programu MySQL, hello bazy danych usługi automatycznie tworzy kopię zapasową usługi hello co 5 minut. 

kopie zapasowe Hello są dostępne przez 7 dni, korzystając z warstwy podstawowej i 35 dni po użyciu warstwy standardowa. Aby uzyskać więcej informacji, zobacz [bazą danych Azure dla warstwy usługi MySQL](concepts-service-tiers.md)

Tej funkcji automatycznego tworzenia kopii zapasowej można przywrócić powitania serwera i wszystkich jego baz danych do nowego serwera tooan wcześniej punktu w czasie.

## <a name="restore-in-hello-azure-portal"></a>Przywracanie w hello portalu Azure
Bazy danych platformy Azure dla programu MySQL pozwala toorestore powitania serwera zapasowego tooa punktu w czasie, do nowej kopii tooa powitania serwera. Ten nowy toorecover serwera można użyć danych. 

Na przykład jeśli tabela została przypadkowo porzucony w południe dzisiaj, można przywrócenie czasu toohello tuż przed południe i pobrać hello Brak tabeli i danych z tej nowej kopii powitania serwera.

Witaj następujące kroki hello przykładowy serwer tooa punkt przywracania w czasie:

1. Zaloguj się na powitania [portalu Azure](https://portal.azure.com/)

2. Zlokalizuj bazy danych Azure, aby serwer MySQL. Wybierz w okienku po lewej stronie powitania **wszystkie zasoby**, następnie wybierz serwer z listy hello.

3.  U góry hello powitania serwera omówienie bloku, kliknij przycisk **przywrócić** na powitania narzędzi. zostanie otwarty blok przywracania Hello.
![Kliknij przycisk przywracania](./media/howto-restore-server-portal/click-restore-button.png)

4. Wypełnij formularz przywracania hello hello wymagane informacje:

- **(UTC) punkt przywracania**: za pomocą selektora czasu i hello wyboru daty, wybierz toorestore punktu w czasie, aby. określona godzina Hello jest w formacie UTC, warto prawdopodobnie tooconvert hello lokalnego czasu w formacie UTC.
- **Przywracanie serwera toonew**: Podaj nazwę toorestore hello istniejącego serwera do nowego serwera.
- **Lokalizacja**: wybór obszaru hello automatycznie wypełnia hello źródłowego serwera regionu i nie można zmienić.
- **Warstwa cenowa**: hello cennik wybór warstwy automatycznie wypełnia hello takie same ceny warstwy jako powitania serwera źródłowego i nie można ich tutaj zmienić. 
![Przywracanie PITR](./media/howto-restore-server-portal/pitr-restore.png)

5. Kliknij przycisk **OK** toorestore powitania serwera toorestore tooa punktu w czasie. 

6. Po zakończeniu przywracania hello zlokalizować hello nowy serwer, który został utworzony powitalne tooverify baz danych zostały przywrócone zgodnie z oczekiwaniami.

## <a name="next-steps"></a>Następne kroki
- [Biblioteki połączeń dla bazy danych Azure dla programu MySQL](concepts-connection-libraries.md)