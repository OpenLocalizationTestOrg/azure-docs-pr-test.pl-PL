---
title: "aaaTroubleshoot powolne kopii zapasowej plików i folderów w usłudze Kopia zapasowa Azure | Dokumentacja firmy Microsoft"
description: "Udostępnia rozwiązywanie problemów z toohelp wskazówki diagnozowanie hello przyczyną problemów z wydajnością kopia zapasowa Azure"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.assetid: e379180a-db13-4e0c-90e4-28e5dd6f5b14
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 21d79bbd03c2706bc43fcc7c14020cffd6b919c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-backup-of-files-and-folders-in-azure-backup"></a>Rozwiązywanie problemów związanych z powolnym tworzeniem kopii zapasowych plików i folderów w usłudze Azure Backup
Ten artykuł zawiera wskazówki dotyczące rozwiązywania problemów toohelp zdiagnozowaniu przyczyny hello niską wydajność tworzenia kopii zapasowej plików i folderów podczas korzystania z usługi Kopia zapasowa Azure. Gdy używasz hello Azure Backup agent tooback zapasowych plików, hello procesu tworzenia kopii zapasowej może trwać dłużej, niż oczekiwano. To opóźnienie może być spowodowany przez jedną lub więcej z następujących hello:

* [Brak wąskich gardeł wydajności na komputerze hello, która jest tworzona kopia zapasowa.](#cause1)
* [Inny proces lub oprogramowanie antywirusowe jest zakłócać hello procesu tworzenia kopii zapasowej Azure.](#cause2)
* [agent usługi Kopia zapasowa Hello jest uruchomiona na maszynie wirtualnej platformy Azure (VM).](#cause3)  
* [W przypadku tworzenia kopii zapasowej dużą liczbą plików (w milionach).](#cause4)

Przed rozpoczęciem rozwiązywania problemów zaleca się pobrać i zainstalować hello [najnowsza wersja agenta usługi Kopia zapasowa Azure](http://aka.ms/azurebackup_agent). Firma Microsoft dokonać toofix agenta kopii zapasowej toohello częste aktualizacje różne problemy, Dodaj funkcje i zwiększyć wydajność.

Ponadto zdecydowanie zalecamy zapoznanie się hello [usługi Kopia zapasowa Azure — często zadawane pytania](backup-azure-backup-faq.md) toomake się, że nie występują dowolne hello typowych problemów z konfiguracją.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

<a id="cause1"></a>

## <a name="cause-performance-bottlenecks-on-hello-computer"></a>Przyczyna: Wąskich gardeł wydajności na komputerze hello
Wąskie gardła na komputerze hello, która jest tworzona kopia zapasowa może powodować opóźnienia. Na przykład Witaj toodisk tooread lub zapisu możliwości komputera lub danych toosend dostępną przepustowość sieci hello może spowodować wąskich gardeł.

System Windows oferuje wbudowane narzędzie, które jest nazywany [monitora wydajności](https://technet.microsoft.com/magazine/2008.08.pulse.aspx) toodetect (Perfmon) tych wąskich gardeł.

Poniżej przedstawiono niektóre liczniki wydajności i zakresy, które mogą pomóc w zdiagnozowaniu wąskich gardeł optymalne kopii zapasowych.

| Licznik | Stan |
| --- | --- |
| Dysk logiczny (dysk fizyczny)--% bezczynności |• too50 bezczynności 100% % bezczynności = w dobrej kondycji</br>• too20 bezczynności 49% % bezczynności = ostrzeżenia lub monitora</br>• too0 bezczynności 19% % bezczynności = krytyczne lub specyfikacji z |
| Dysk logiczny (dysk fizyczny)--% średni S odczytu lub zapisu na dysku |• 0,001 ms too0.015 ms = w dobrej kondycji</br>• 0,015 ms too0.025 ms = ostrzeżenia lub monitora</br>• 0.026 ms lub już = krytyczne lub specyfikacji z |
| Dysk logiczny (dysk fizyczny) — bieżąca długość kolejki dysku (dla wszystkich wystąpień) |80 żądań przez więcej niż 6 minut |
| Pamięć — Bajty z systemem innym niż puli stronicowanej |• Mniej niż 60% puli używane = w dobrej kondycji<br>• 61% too80% puli używane = ostrzeżenia lub monitora</br>• Większa niż 80% puli używane = krytyczne lub specyfikacji z |
| Pamięć — Bajty w puli stronicowanej |• Mniej niż 60% puli używane = w dobrej kondycji</br>• 61% too80% puli używane = ostrzeżenia lub monitora</br>• Większa niż 80% puli używane = krytyczne lub specyfikacji z |
| Pamięć — dostępnego w megabajtach |• 50% pamięci lub więcej = w dobrej kondycji</br>• 25% pamięci = monitora</br>• 10% pamięci = ostrzeżenie</br>• Mniej niż 100 MB lub 5% wolnej pamięci = krytyczne lub specyfikacji z |
| Procesor —\%czas procesora (wszystkie wystąpienia) |• Mniej niż 60% używane = w dobrej kondycji</br>• 61% too90% używane = Monitor lub Uwaga</br>• 91% too100% używane = krytyczne |

> [!NOTE]
> Jeśli okaże się, że infrastruktura hello jest hello culprit, zaleca się defragmentowania dysków hello regularnie w celu zapewnienia lepszej wydajności.
>
>

<a id="cause2"></a>

## <a name="cause-another-process-or-antivirus-software-interfering-with-azure-backup"></a>Przyczyna: Inny proces lub zakłócać kopia zapasowa Azure oprogramowanie antywirusowe
Firma Microsoft przedstawiono kilka wystąpień, gdy inne procesy w systemie Windows hello mieć negatywny wpływ na wydajność hello procesu agenta usługi Kopia zapasowa Azure. Na przykład hello agenta usługi Kopia zapasowa Azure i inny program tooback zapasową danych, lub gdy oprogramowanie antywirusowe jest uruchomiony i ma blokadę toobe pliki kopii zapasowej, hello blokad wielu plików może spowodować rywalizacji. W takiej sytuacji hello kopii zapasowej może zakończyć się niepowodzeniem lub hello zadania może trwać dłużej, niż oczekiwano.

Witaj najlepsze zalecenie, w tym scenariuszu jest tooturn poza hello innych toosee kopii zapasowej program, czy zmiany czasu tworzenia kopii zapasowych hello hello Azure Backup agent. Zwykle, upewniając się, że wiele zadań tworzenia kopii zapasowej nie są uruchomione na powitania jednocześnie jest wystarczające tooprevent je z wpływających na siebie.

Programy antywirusowe, zaleca się wykluczenie hello następujące pliki i lokalizacje:

* C:\Program Files\Microsoft Azure Recovery Services Agent\bin\cbengine.exe jako proces
* C:\Program Files\Microsoft Azure Recovery Services Agent\ folderów
* Pliki tymczasowe lokalizacji (Jeśli nie używasz hello standardowej lokalizacji)

<a id="cause3"></a>

## <a name="cause-backup-agent-running-on-an-azure-virtual-machine"></a>Przyczyna: Kopia zapasowa agenta uruchomionego na maszynie wirtualnej platformy Azure
Jeśli używasz hello agenta kopii zapasowej na maszynie Wirtualnej, wydajność będzie mniejsza niż po uruchomieniu go na komputerze fizycznym. Jest to zachowanie normalne powodu tooIOPS ograniczenia.  Jednak można zoptymalizować wydajność hello przełączając hello dysków z danymi tworzona jest kopia zapasowa tooAzure magazyn w warstwie Premium. Pracujemy nad rozwiązywania tego problemu, a hello poprawki będą dostępne w przyszłej wersji.

<a id="cause4"></a>

## <a name="cause-backing-up-a-large-number-millions-of-files"></a>Przyczyna: Tworzenie kopii zapasowej dużą liczbą plików (w milionach)
Przenoszenie dużej ilości danych będzie trwało dłużej niż przenoszenie mniejsza ilość danych. W niektórych przypadkach czas tworzenia kopii zapasowej jest powiązana toonot tylko hello rozmiar danych hello, ale także hello liczbę plików lub folderów. Jest to szczególnie istotne, kiedy miliony małych plików (kilka tooa bajtów kilku kilobajtów) tworzona jest kopia zapasowa.

Dzieje się tak, ponieważ w przypadku tworzenia kopii zapasowej danych hello i przeniesienie ich tooAzure, Azure jest jednocześnie skatalogowania plików. W niektórych scenariuszach rzadkich hello katalogu operacji może potrwać dłużej niż oczekiwano.

powitania po wskaźniki może pomóc w zrozumieć "wąskie gardło" hello i odpowiednio działają na powitania następne kroki:

* **Interfejs użytkownika jest wyświetlany postęp do transferu danych hello**. dane Hello są wciąż przesyłane. przepustowość sieci Hello lub hello rozmiar danych mogą być przyczyną opóźnień.
* **Interfejs użytkownika nie jest wyświetlany postęp do transferu danych hello**. Hello otwórz dzienniki znajdujący się w Agent\Temp usług odzyskiwania Azure C:\Microsoft, a następnie wyszukaj hello FileProvider::EndData wpis w dziennikach hello. Ten wpis oznacza, że zakończono transferu danych hello dzieje hello katalogu operacji. Nie Anuluj hello zadania tworzenia kopii zapasowej. Zamiast tego należy zaczekać nieco dłużej na powitania katalogu operacji toofinish. Jeśli hello problem będzie się powtarzać, skontaktuj się z [pomocy technicznej platformy Azure](https://portal.azure.com/#create/Microsoft.Support).
