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
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a><span data-ttu-id="beb0c-103">Przeniesienie magazynu długoterminowego z taśmy toohello chmury Azure</span><span class="sxs-lookup"><span data-stu-id="beb0c-103">Move your long-term storage from tape toohello Azure cloud</span></span>
<span data-ttu-id="beb0c-104">Azure Backup i System Center Data Protection Manager klienci mogą:</span><span class="sxs-lookup"><span data-stu-id="beb0c-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="beb0c-105">Utwórz kopię zapasową danych w harmonogramy, które najlepiej odpowiadają potrzebom organizacji hello.</span><span class="sxs-lookup"><span data-stu-id="beb0c-105">Back up data in schedules which best suit hello organizational needs.</span></span>
* <span data-ttu-id="beb0c-106">Zachowaj dane kopii zapasowej hello przez dłuższy czas</span><span class="sxs-lookup"><span data-stu-id="beb0c-106">Retain hello backup data for longer periods</span></span>
* <span data-ttu-id="beb0c-107">Wprowadź Azure ich przechowywania długoterminowego wymagających (zamiast taśma).</span><span class="sxs-lookup"><span data-stu-id="beb0c-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="beb0c-108">W tym artykule opisano, jak włączyć zasady tworzenia kopii zapasowej i przechowywania klientów.</span><span class="sxs-lookup"><span data-stu-id="beb0c-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="beb0c-109">Klienci korzystający z taśmy tooaddress ich długo-długoterminowego — przechowywania musi już wydajny i realną alternatywę hello dostępności tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="beb0c-109">Customers who use tapes tooaddress their long-term-retention needs now have a powerful and viable alternative with hello availability of this feature.</span></span> <span data-ttu-id="beb0c-110">Witaj włączeniu funkcji w najnowszym wydaniu hello hello kopia zapasowa Azure (który jest dostępny [tutaj](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="beb0c-110">hello feature is enabled in hello latest release of hello Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="beb0c-111">Zaktualizować do programu System Center DPM klientów, co najmniej programu DPM 2012 R2 pakiet zbiorczy aktualizacji 5 przed użyciem programu DPM z hello usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="beb0c-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with hello Azure Backup service.</span></span>

## <a name="what-is-hello-backup-schedule"></a><span data-ttu-id="beb0c-112">Co to jest harmonogram tworzenia kopii zapasowych hello?</span><span class="sxs-lookup"><span data-stu-id="beb0c-112">What is hello Backup Schedule?</span></span>
<span data-ttu-id="beb0c-113">harmonogram tworzenia kopii zapasowych Hello wskazuje częstotliwość hello hello operacji tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="beb0c-113">hello backup schedule indicates hello frequency of hello backup operation.</span></span> <span data-ttu-id="beb0c-114">Na przykład hello ustawienia w po ekranie powitania wskazują podjęcie kopii zapasowych codziennie o 18: 00 i o północy.</span><span class="sxs-lookup"><span data-stu-id="beb0c-114">For example, hello settings in hello following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Harmonogram dzienny](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="beb0c-116">Klientów można również zaplanować kopia zapasowa co tydzień.</span><span class="sxs-lookup"><span data-stu-id="beb0c-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="beb0c-117">Na przykład hello ustawienia w po ekranie powitania wskazują, czy kopie zapasowe są przyjmowane co alternatywny niedziela & środa na 9:30 a 1:00:00.</span><span class="sxs-lookup"><span data-stu-id="beb0c-117">For example, hello settings in hello following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Harmonogram tygodniowy](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a><span data-ttu-id="beb0c-119">Co to jest hello zasady przechowywania?</span><span class="sxs-lookup"><span data-stu-id="beb0c-119">What is hello Retention Policy?</span></span>
<span data-ttu-id="beb0c-120">zasady przechowywania Hello określa czas trwania hello, dla której muszą być przechowywane hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="beb0c-120">hello retention policy specifies hello duration for which hello backup must be stored.</span></span> <span data-ttu-id="beb0c-121">Zamiast określać "wspólne zasady" dla wszystkich punktów kopii zapasowej, klientów można określić, gdy wykonywana jest kopia zapasowa hello na podstawie różnych zasad przechowywania.</span><span class="sxs-lookup"><span data-stu-id="beb0c-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="beb0c-122">Na przykład hello punktu kopii zapasowej pobierane raz dziennie, która służy jako punkt odzyskiwania operacyjne, jest zachowywana przez 90 dni.</span><span class="sxs-lookup"><span data-stu-id="beb0c-122">For example, hello backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="beb0c-123">Witaj punktu kopii zapasowej wykonywaną na końcu hello co kwartał do celów inspekcji jest zachowywana przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="beb0c-123">hello backup point taken at hello end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Zasady przechowywania](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="beb0c-125">Witaj łączna liczba "punkty przechowywania" określone w tej zasadzie to 90 (codzienne punkty) + 40 (każdy kwartał 10 lat) = 130.</span><span class="sxs-lookup"><span data-stu-id="beb0c-125">hello total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="beb0c-126">Przykład — zarówno zestawienie</span><span class="sxs-lookup"><span data-stu-id="beb0c-126">Example – Putting both together</span></span>
![Przykład ekranu](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="beb0c-128">**Zasady przechowywania codziennych**: kopii zapasowych wykonanych codziennie są przechowywane na siedem dni.</span><span class="sxs-lookup"><span data-stu-id="beb0c-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="beb0c-129">**Co tydzień zasady przechowywania**: wykonaną codziennie o północy i 18: 00 Sobota kopie zapasowe są zachowywane przez 4 tygodnie</span><span class="sxs-lookup"><span data-stu-id="beb0c-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="beb0c-130">**Miesięczne zasady przechowywania**: kopii zapasowych wykonanych na północ i 18: 00 na powitania sobota ostatniego dnia każdego miesiąca są zachowywane przez 12 miesięcy</span><span class="sxs-lookup"><span data-stu-id="beb0c-130">**Monthly retention policy**: Backups taken at midnight and 6pm on hello last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="beb0c-131">**Zasady przechowywania corocznych**: kopii zapasowych wykonanych o północy w hello Ostatnia sobota co marca zostaną zachowane 10 lat</span><span class="sxs-lookup"><span data-stu-id="beb0c-131">**Yearly retention policy**: Backups taken at midnight on hello last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="beb0c-132">Całkowita liczba "punkty przechowywania" Hello (punkty, z których klient może przywrócić dane) w hello wcześniejszym diagramie jest obliczana w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="beb0c-132">hello total number of “retention points” (points from which a customer can restore data) in hello preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="beb0c-133">dwa punkty dziennie siedem dni = 14 punktów odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="beb0c-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="beb0c-134">dwa punkty tygodniowo dla cztery tygodnie = 8 punktów odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="beb0c-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="beb0c-135">dwa punkty USD miesięcznie przez 12 miesięcy = 24 punktów odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="beb0c-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="beb0c-136">wskazuje jeden punkt rocznie na 10 lat = 10 odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="beb0c-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="beb0c-137">Witaj łączną liczbę punktów odzyskiwania jest w 56.</span><span class="sxs-lookup"><span data-stu-id="beb0c-137">hello total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="beb0c-138">Kopia zapasowa Azure nie ma ograniczenie liczby punktów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="beb0c-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="beb0c-139">Konfiguracja zaawansowana</span><span class="sxs-lookup"><span data-stu-id="beb0c-139">Advanced configuration</span></span>
<span data-ttu-id="beb0c-140">Klikając **Modyfikuj** w hello ekranu poprzedzającym, klienci mają bardziej elastyczną określenie harmonogramu przechowywania.</span><span class="sxs-lookup"><span data-stu-id="beb0c-140">By clicking **Modify** in hello preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Modyfikuj](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="beb0c-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="beb0c-142">Next Steps</span></span>
<span data-ttu-id="beb0c-143">Aby uzyskać więcej informacji o usłudze Azure Backup zobacz:</span><span class="sxs-lookup"><span data-stu-id="beb0c-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="beb0c-144">Wprowadzenie tooAzure kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="beb0c-144">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="beb0c-145">Spróbuj kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="beb0c-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
