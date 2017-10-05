---
title: Przywracanie serwera w bazie danych systemu Azure dla programu MySQL | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób przywracania serwera w bazie danych Azure dla programu MySQL przy użyciu portalu Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a>Jak wykonywanie kopii zapasowych i przywracania serwera w bazie danych Azure dla programu MySQL przy użyciu portalu Azure

## <a name="backup-happens-automatically"></a>Kopia zapasowa jest wykonywana automatycznie
Korzystając z bazy danych platformy Azure dla programu MySQL, usługa bazy danych automatycznie sprawia, że usługa Kopia zapasowa co 5 minut. 

Kopie zapasowe są dostępne przez 7 dni, korzystając z warstwy podstawowej i 35 dni po użyciu warstwy standardowa. Aby uzyskać więcej informacji, zobacz [bazą danych Azure dla warstwy usługi MySQL](concepts-service-tiers.md)

Tej funkcji automatycznego tworzenia kopii zapasowej można przywrócić serwer i wszystkie jej baz danych do nowego serwera do wcześniejszego punktu w stanu.

## <a name="restore-in-the-azure-portal"></a>Przywracanie w portalu Azure
Bazy danych platformy Azure dla programu MySQL służy do przywrócenia serwera do punktu w czasie, a do z uprawnieniami do nowego serwera. Aby odzyskać dane, można użyć tego nowego serwera. 

Na przykład jeśli przypadkowo tabeli w południe dzisiaj, można przywrócenie na czas bezpośrednio przed południe i pobieranie Brak tabeli i danych z tej kopii nowego serwera.

Poniższe kroki przywrócenie serwera próbki do punktu w czasie:

1. Zaloguj się do [portalu Azure](https://portal.azure.com/)

2. Zlokalizuj bazy danych Azure, aby serwer MySQL. W okienku po lewej stronie wybierz **wszystkie zasoby**, następnie wybierz serwer z listy.

3.  W górnej części bloku Omówienie serwera, kliknij przycisk **przywrócić** na pasku narzędzi. Zostanie otwarty blok przywracania.
![Kliknij przycisk przywracania](./media/howto-restore-server-portal/click-restore-button.png)

4. Wypełnij formularz przywracania wymagane informacje:

- **(UTC) punkt przywracania**: za pomocą selektora daty i czasu selektora, wybierz w momencie przywrócić. Określona godzina jest w formacie UTC, więc prawdopodobnie trzeba przekonwertować czasu lokalnego w formacie UTC.
- **Przywracanie do nowego serwera**: Podaj nową nazwę serwera do istniejącego serwera do przywrócenia.
- **Lokalizacja**: wybór obszaru automatycznie wypełnia obszaru serwera źródłowego i nie można zmienić.
- **Warstwa cenowa**: wybór warstwy cenowej automatycznie wypełnia tej samej warstwie cenowej co serwer źródłowy i nie można ich tutaj zmienić. 
![Przywracanie PITR](./media/howto-restore-server-portal/pitr-restore.png)

5. Kliknij przycisk **OK** do przywrócenia serwera, aby wykonać przywracanie do punktu w czasie. 

6. Po zakończeniu przywracania, zlokalizuj nowy serwer, który został utworzony w celu sprawdzenia, czy zostały przywrócone baz danych, zgodnie z oczekiwaniami.

## <a name="next-steps"></a>Następne kroki
- [Biblioteki połączeń dla bazy danych Azure dla programu MySQL](concepts-connection-libraries.md)