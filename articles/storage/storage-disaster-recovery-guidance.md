---
title: "toodo aaaWhat w zdarzeniu hello awarii usługi Azure Storage | Dokumentacja firmy Microsoft"
description: "Jakie toodo w zdarzeniu hello awarii usługi Azure Storage"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: ee7eb71311c6e453dc078ec3566267ee0c2f444a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-if-an-azure-storage-outage-occurs"></a>Jakie toodo w przypadku wystąpienia awarii usługi Azure Storage
Firma Microsoft pracujemy twardych toomake się, że naszych usług są zawsze dostępne. Czasami wymusza poza naszych wpływ kontroli nam w sposób, aby spowodować usługi nieplanowanych przestojów w jednym lub więcej regionów. toohelp obsługi tych zdarzeń w rzadkich, udostępniamy hello następujące ogólne wskazówki dotyczące usługi Azure Storage.

## <a name="how-tooprepare"></a>Jak tooprepare
Jest bardzo istotne dla każdego klienta tooprepare własnych planu odzyskiwania po awarii. Hello toorecover wysiłku z awarii magazynu zwykle obejmuje zarówno personel i zautomatyzowanych procedur w kolejności tooreactivate aplikacji w działającym stanie. Przeczytaj dokumentację platformy Azure poniżej toobuild toohello własnego planu odzyskiwania po awarii:

* [Odzyskiwanie aplikacji platformy Azure po awarii i ich wysoka dostępność](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Odporność platformy Azure — wskazówki techniczne](../resiliency/resiliency-technical-guidance.md)
* [Usługa Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)
* [Replikacja usługi Azure Storage](storage-redundancy.md)
* [Usługa Kopia zapasowa Azure](https://azure.microsoft.com/services/backup/)

## <a name="how-toodetect"></a>Jak toodetect
Hello zalecany sposób toodetermine hello stan usługi systemu Azure jest toosubscribe toohello [pulpit nawigacyjny kondycji usługi Azure](https://azure.microsoft.com/status/).

## <a name="what-toodo-if-a-storage-outage-occurs"></a>Jakie toodo, jeśli wystąpi awaria magazynu
Jeśli co najmniej jednej usługi magazynu są tymczasowo niedostępne na jeden lub więcej regionów, dostępne są dwie opcje dla tooconsider użytkownik. Jeśli chcesz natychmiastowy dostęp tooyour danych, rozważ opcja 2.

### <a name="option-1-wait-for-recovery"></a>Opcja 1: Poczekaj, aż odzyskiwanie
W takim przypadku jest wymagana żadna akcja ze strony użytkownika. Pracujemy nad dokładnie toorestore hello usługi Azure dostępności. Można monitorować stan usługi hello na powitania [pulpit nawigacyjny kondycji usługi Azure](https://azure.microsoft.com/status/).

### <a name="option-2-copy-data-from-secondary"></a>Opcja 2: Kopiowanie danych z pomocniczego
Jeśli została wybrana opcja [dostęp do odczytu magazynu geograficznie nadmiarowego (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (zalecane) dla konta magazynu, będzie mieć dostęp do odczytu tooyour danych z regionu pomocniczego hello. Można użyć narzędzia, takie jak [AzCopy](storage-use-azcopy.md), [programu Azure PowerShell](storage-powershell-guide-full.md)i hello [Biblioteka przenoszenia danych Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/) toocopy dane z regionu pomocniczego hello na innym koncie magazynu w unimpacted region, a następnie punkt konto magazynu toothat aplikacje do odczytu i zapisu dostępności.

## <a name="what-tooexpect-if-a-storage-failover-occurs"></a>Jakie tooexpect, jeśli do pracy awaryjnej magazynu
Jeśli została wybrana opcja [magazyn geograficznie nadmiarowy (GRS)](storage-redundancy.md#geo-redundant-storage) lub [dostęp do odczytu magazynu geograficznie nadmiarowego (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (zalecane), usługi Azure Storage będzie przechowywać swoje dane trwałe w dwóch regionach (podstawowych i pomocniczych). W obu regionów usługi Magazyn Azure przechowuje stale wiele replik danych.

W przypadku regionalnej awarii wpływa regionu podstawowego, najpierw spróbujemy toorestore hello usługę w tym regionie. Zależne od charakteru hello powitania po awarii i jej wpływ na środowisko, w niektórych rzadkich firma Microsoft nie może być regionu podstawowego hello toorestore stanie. W tym momencie zostaną wykonane geograficznie trybu failover. Replikacja danych między region Hello jest proces asynchroniczny, które obejmują opóźnienia, więc jest to możliwe, że zmiany, które nie zostały jeszcze zreplikowane region pomocniczy toohello mogą zostać utracone. Można zbadać hello ["Czas ostatniej synchronizacji" konta magazynu](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/) tooget szczegóły dotyczące stanu replikacji hello.

Kilka punktów dotyczących środowiska pracy awaryjnej geo magazynu hello:

* Magazyn geograficznie pracy w trybie failover tylko zostanie wywołane przez zespół usługi Azure Storage hello — nie jest wymagane żadne akcje klienta.
* Istniejącą usługę magazynu pozostaną punktów końcowych dla obiektów blob, tabel, kolejek i plików hello sam po pracy awaryjnej hello; Hello wpisu DNS należy tooswitch toobe zaktualizowane z regionu pomocniczego toohello hello regionu podstawowego.
* Przed i podczas hello geograficznie pracy w trybie failover nie będziesz mieć dostęp do zapisu konta magazynu tooyour ze względu na wpływ toohello powitania po awarii, ale można nadal odczytać z hello dodatkowej Jeśli Twoje konto magazynu został skonfigurowany jako RA-GRS.
* Gdy hello geograficznie pracy w trybie failover została ukończona i hello propagowane zmian DNS, Odczyt i zapis konta magazynu tooyour zostanie wznowione; Wskazuje to toobe toowhat używane dodatkowej punktu końcowego. 
* Należy pamiętać, że będzie miał dostęp zapisu, jeśli masz GRS lub RA-GRS skonfigurowanych dla konta magazynu hello. 
* Można zbadać ["Geograficznie trybu Failover ostatniego" konta magazynu](https://msdn.microsoft.com/library/azure/ee460802.aspx) tooget więcej szczegółowych informacji.
* Po przełączeniu hello konta magazynu będzie można w pełni funkcjonalne, ale w stanie "obniżeniem", ponieważ faktycznie znajduje się w regionie autonomiczny z nie możliwości replikacja geograficzna. toomitigate to ryzyko, zostanie przywrócona hello oryginalnego regionu podstawowego, a następnie oryginalny stan hello toorestore czy geograficznie-powrotu po awarii. W przypadku oryginalnego regionu podstawowego hello jest nieodwracalny, firma Microsoft będzie przydzielić inny region pomocniczy.
  Więcej szczegółów na powitania infrastruktury replikacja geograficzna usługi Azure Storage, można znaleźć w artykule toohello na powitania blog zespołu usługi Magazyn o [Opcje nadmiarowości i RA-GRS](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

## <a name="best-practices-for-protecting-your-data"></a>Najlepsze rozwiązania w zakresie ochrony danych
Brak niektórych tooback zalecane podejście zapasowe magazynu danych na bieżąco.

* Dyski maszyny Wirtualnej — Użyj hello [usługi Kopia zapasowa Azure](https://azure.microsoft.com/services/backup/) tooback się hello wirtualna dysków używanych przez maszyny wirtualne platformy Azure.
* Blokowych obiektów blob — Utwórz [migawki](https://msdn.microsoft.com/library/azure/hh488361.aspx) każdego blokowy, lub skopiuj konta magazynu tooanother obiekty BLOB hello w innym regionie przy użyciu [AzCopy](storage-use-azcopy.md), [programu Azure PowerShell](storage-powershell-guide-full.md), lub hello [ Biblioteka przenoszenia danych platformy Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/).
* Użyj tabel — [AzCopy](storage-use-azcopy.md) tooexport hello tabeli danych do innego konta magazynu w innym regionie.
* Pliki — [AzCopy](storage-use-azcopy.md) lub [programu Azure PowerShell](storage-powershell-guide-full.md) toocopy konta magazynu tooanother pliki w innym regionie.

Aby uzyskać informacje o tworzeniu aplikacji, które korzystają z funkcji hello RA-GRS, zapoznaj się [Projektowanie wysoce dostępnych aplikacji przy użyciu magazynu RA-GRS](storage-designing-ha-apps-with-ragrs.md)

