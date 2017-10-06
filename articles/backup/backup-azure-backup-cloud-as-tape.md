---
title: "tooreplace kopia zapasowa Azure aaaUse infrastruktury taśmy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Kopia zapasowa Azure udostępnia semantyki przypominającej taśm, co pozwala toobackup i przywracania danych na platformie Azure"
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a>Przeniesienie magazynu długoterminowego z taśmy toohello chmury Azure
Azure Backup i System Center Data Protection Manager klienci mogą:

* Utwórz kopię zapasową danych w harmonogramy, które najlepiej odpowiadają potrzebom organizacji hello.
* Zachowaj dane kopii zapasowej hello przez dłuższy czas
* Wprowadź Azure ich przechowywania długoterminowego wymagających (zamiast taśma).

W tym artykule opisano, jak włączyć zasady tworzenia kopii zapasowej i przechowywania klientów. Klienci korzystający z taśmy tooaddress ich długo-długoterminowego — przechowywania musi już wydajny i realną alternatywę hello dostępności tej funkcji. Witaj włączeniu funkcji w najnowszym wydaniu hello hello kopia zapasowa Azure (który jest dostępny [tutaj](http://aka.ms/azurebackup_agent)). Zaktualizować do programu System Center DPM klientów, co najmniej programu DPM 2012 R2 pakiet zbiorczy aktualizacji 5 przed użyciem programu DPM z hello usługi Kopia zapasowa Azure.

## <a name="what-is-hello-backup-schedule"></a>Co to jest harmonogram tworzenia kopii zapasowych hello?
harmonogram tworzenia kopii zapasowych Hello wskazuje częstotliwość hello hello operacji tworzenia kopii zapasowej. Na przykład hello ustawienia w po ekranie powitania wskazują podjęcie kopii zapasowych codziennie o 18: 00 i o północy.

![Harmonogram dzienny](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

Klientów można również zaplanować kopia zapasowa co tydzień. Na przykład hello ustawienia w po ekranie powitania wskazują, czy kopie zapasowe są przyjmowane co alternatywny niedziela & środa na 9:30 a 1:00:00.

![Harmonogram tygodniowy](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a>Co to jest hello zasady przechowywania?
zasady przechowywania Hello określa czas trwania hello, dla której muszą być przechowywane hello kopii zapasowej. Zamiast określać "wspólne zasady" dla wszystkich punktów kopii zapasowej, klientów można określić, gdy wykonywana jest kopia zapasowa hello na podstawie różnych zasad przechowywania. Na przykład hello punktu kopii zapasowej pobierane raz dziennie, która służy jako punkt odzyskiwania operacyjne, jest zachowywana przez 90 dni. Witaj punktu kopii zapasowej wykonywaną na końcu hello co kwartał do celów inspekcji jest zachowywana przez dłuższy czas.

![Zasady przechowywania](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

Witaj łączna liczba "punkty przechowywania" określone w tej zasadzie to 90 (codzienne punkty) + 40 (każdy kwartał 10 lat) = 130.

## <a name="example--putting-both-together"></a>Przykład — zarówno zestawienie
![Przykład ekranu](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. **Zasady przechowywania codziennych**: kopii zapasowych wykonanych codziennie są przechowywane na siedem dni.
2. **Co tydzień zasady przechowywania**: wykonaną codziennie o północy i 18: 00 Sobota kopie zapasowe są zachowywane przez 4 tygodnie
3. **Miesięczne zasady przechowywania**: kopii zapasowych wykonanych na północ i 18: 00 na powitania sobota ostatniego dnia każdego miesiąca są zachowywane przez 12 miesięcy
4. **Zasady przechowywania corocznych**: kopii zapasowych wykonanych o północy w hello Ostatnia sobota co marca zostaną zachowane 10 lat

Całkowita liczba "punkty przechowywania" Hello (punkty, z których klient może przywrócić dane) w hello wcześniejszym diagramie jest obliczana w następujący sposób:

* dwa punkty dziennie siedem dni = 14 punktów odzyskiwania
* dwa punkty tygodniowo dla cztery tygodnie = 8 punktów odzyskiwania
* dwa punkty USD miesięcznie przez 12 miesięcy = 24 punktów odzyskiwania
* wskazuje jeden punkt rocznie na 10 lat = 10 odzyskiwania

Witaj łączną liczbę punktów odzyskiwania jest w 56.

> [!NOTE]
> Kopia zapasowa Azure nie ma ograniczenie liczby punktów odzyskiwania.
>
>

## <a name="advanced-configuration"></a>Konfiguracja zaawansowana
Klikając **Modyfikuj** w hello ekranu poprzedzającym, klienci mają bardziej elastyczną określenie harmonogramu przechowywania.

![Modyfikuj](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o usłudze Azure Backup zobacz:

* [Wprowadzenie tooAzure kopii zapasowej](backup-introduction-to-azure-backup.md)
* [Spróbuj kopia zapasowa Azure](backup-try-azure-backup-in-10-mins.md)
