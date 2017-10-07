---
title: "aaaFrequently zadawane pytania dotyczące usługi Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące rozwiązywania problemów lub eliminowania błędów dotyczących usługi Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf7fd555-3e30-43ce-b28c-c3ad0a241fdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: eeabdeef18f3b72901bd1a14283f85dd9c0ead44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a>Często zadawane pytania dotyczące usługi Azure Data Lake Store
W tym artykule dowiesz się o powiązanych tooAzure często zadawane pytania dotyczące usługi Data Lake Store.

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a>Jak mogę jeszcze lepiej chronić dane przed awariami obejmującymi cały region lub przypadkowym usunięciem?
Hello danych na koncie usługi Azure Data Lake Store jest odporność tootransient awarie sprzętowe w obrębie regionu poprzez automatyczne replik. Dzięki temu trwałości i wysokiej dostępności, hello spotkania umowy SLA platformy Azure Data Lake magazynu. Oto niektóre wskazówki na jak toofurther ochronę danych przed rzadkich awarii całej region lub przypadkowym usunięciu.

### <a name="disaster-recovery-guidance"></a>Wskazówki dotyczące odzyskiwania po awarii
Jest bardzo istotne dla każdego klienta tooprepare własnych planu odzyskiwania po awarii. Można znaleźć w dokumentacji platformy Azure poniżej toobuild toohello planu odzyskiwania po awarii. Poniżej przedstawiono niektóre zasoby, które mogą pomóc w tworzeniu własnego planu.

* [Odzyskiwanie aplikacji platformy Azure po awarii i ich wysoka dostępność](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Odporność platformy Azure — wskazówki techniczne](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a>Najlepsze praktyki
Firma Microsoft zaleca, skopiuj tooanother Twojego kluczowych danych konta usługi Data Lake Store w innym regionie o potrzebach toohello częstotliwość wyrównane, planu odzyskiwania po awarii. Istnieją różne metody toocopy danych, w tym [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [programu Azure PowerShell](data-lake-store-get-started-powershell.md) lub [fabryki danych Azure](../data-factory/data-factory-azure-datalake-connector.md). Azure Data Factory to usługa przydatna w przypadku cyklicznego tworzenia i wdrażania potoków przepływu danych.

W przypadku regionalnej awarii można następnie uzyskać dostępu do danych w regionie hello, gdzie został skopiowany hello danych. Można monitorować hello [pulpit nawigacyjny kondycji usługi Azure](https://azure.microsoft.com/status/) hello toodetermine stan usługi Azure między Witaj świecie.

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a>Uszkodzenie lub przypadkowe usunięcie danych — wskazówki
Usługa Azure Data Lake Store zapewnia odporność danych za pośrednictwem automatycznych replik, ale nie zapobiega uszkodzeniu ani przypadkowemu usunięciu danych przez aplikację (lub deweloperów/użytkowników).

#### <a name="best-practices"></a>Najlepsze praktyki
tooprevent przypadkowego usunięcia zaleca się najpierw ustawić hello zasady dostępu dla konta usługi Data Lake Store.  Obejmuje to stosowanie [blokad zasobów platformy Azure](../azure-resource-manager/resource-group-lock-resources.md) toolock w dół do ważnych zasobów, a także stosowanie konta i pliku poziomu kontroli dostępu z wykorzystaniem hello dostępne [funkcje zabezpieczeń usługi Data Lake Store](data-lake-store-security-overview.md). Zalecamy również regularne tworzenie kopii kluczowych danych usług [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) lub [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) na innym koncie usługi Data Lake Store, w innym folderze lub w ramach innej subskrypcji platformy Azure.  Może to być używane toorecover ze zdarzenia uszkodzenie lub usunięciu danych. Azure Data Factory to usługa przydatna w przypadku cyklicznego tworzenia i wdrażania potoków przepływu danych.

Organizacje mogą również włączyć [rejestrowania diagnostycznego](data-lake-store-diagnostic-logs.md) dla ich Azure Data Lake Store konta toocollect zapisy inspekcji dostępu do danych, które zawiera informacje o mających może usunąć lub zaktualizować pliku.

## <a name="next-steps"></a>Następne kroki
* [Rozpoczynanie pracy z usługą Azure Data Lake Store](data-lake-store-get-started-portal.md)
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)

