---
title: "aaaMoving dużych ilości danych do/z magazynu w chmurze na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przegląd hello różne metody przenoszenia tooand danych z usługi Magazyn Azure."
services: storage
documentationcenter: 
author: JarrettRenshaw
manager: msmets
editor: tysonn
ms.assetid: 5e3947a9-d99b-4108-9d57-3eb67c03e7ba
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jarrettr
ms.openlocfilehash: 8f7105fea7c2d28ba9954898743070d338f46a37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-tooand-from-azure-storage"></a>Przenoszenie tooand danych z usługi Azure Storage
Jeśli chcesz, aby toomove lokalnych danych tooAzure magazynu (lub odwrotnie), istnieją różne sposoby toodo to. podejście Hello, która najlepiej pasuje do można będzie zależeć od danego scenariusza. W tym artykule zapewnia szybki przegląd różnych scenariuszy i odpowiednich ofert dla każdej z nich.

## <a name="building-applications"></a>Tworzenie aplikacji
Jeśli tworzysz aplikację, tworzenie oprogramowania dla hello interfejsu API REST lub jednego z naszych wiele bibliotek klienta jest tooand doskonały sposób toomove danych z usługi Magazyn Azure.

Usługa Azure Storage udostępnia rozbudowane biblioteki dla platformy .NET, iOS, Java, Android, Windows platformy Uniwersalnej, Xamarin, C++, Node.JS, PHP, Ruby i Python. Witaj biblioteki klienta oferują zaawansowane możliwości, takie jak logika ponowień, rejestrowanie i przekazywanie równoległe. Możesz również utworzyć bezpośrednio przed hello interfejsu API REST, które można wywołać za pomocą dowolnego języka, który sprawia, że żądania HTTP i HTTPS.

Zobacz [Rozpoczynanie pracy z magazynem obiektów Blob Azure](storage-dotnet-how-to-use-blobs.md) toolearn więcej.

Ponadto firma Microsoft oferuje również hello [Biblioteka przenoszenia danych magazynu Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) czyli biblioteki przeznaczone dla wysokowydajnej kopiowanie tooand danych z platformy Azure. Zobacz tooour Biblioteka przenoszenia danych [dokumentacji](https://github.com/Azure/azure-storage-net-data-movement) toolearn więcej. 

## <a name="quickly-viewinginteracting-with-your-data"></a>Szybkie wyświetlanie danych i interakcje z danymi
Jeśli tooview łatwy sposób danych usługi Azure Storage przy jednoczesnym zachowaniu również hello możliwości tooupload i Pobierz dane, należy rozważyć przy użyciu Eksploratora usługi Storage platformy Azure.

Zapoznaj się z naszej listy [eksploratory usługi Storage Azure](storage-explorers.md) toolearn więcej.

## <a name="system-administration"></a>Administracja systemu
Jeśli wymagają lub potrafisz więcej narzędzia wiersza polecenia (np. administratorów), poniżej przedstawiono kilka opcji tooconsider możesz:

### <a name="azcopy"></a>Narzędzie AzCopy
Narzędzie AzCopy to narzędzie wiersza polecenia systemu Windows przeznaczony dla wysokowydajnej kopiowanie tooand danych z usługi Magazyn Azure. Można także skopiować dane w ramach konta magazynu lub od różnych kont magazynu.

Zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md) toolearn więcej.

### <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell to moduł udostępniający polecenia cmdlet służące do zarządzania usługami na platformie Azure. Jest to język skryptów i powłoka wiersza polecenia oparta na zadaniach zaprojektowane pod kątem administrowania systemem.

Zobacz [przy użyciu programu Azure PowerShell z usługą Azure Storage](storage-powershell-guide-full.md) toolearn więcej.

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
Interfejsu wiersza polecenia platformy Azure oferuje zestaw typu open source, obsługujący wiele platform polecenia do pracy z usługami Azure. Interfejs wiersza polecenia platformy Azure jest dostępna w systemach Windows, OS x i Linux.

Zobacz [hello używanie interfejsu wiersza polecenia Azure z usługą Azure Storage](storage-azure-cli.md) toolearn więcej.

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a>Przenoszenie dużych ilości danych przy użyciu wolnej sieci
Jedną z największych wyzwań hello skojarzone z przenoszenia dużych ilości danych jest hello czas transferu. Aby bez obaw o koszty sieci i pisanie kodu tooget danych z usługi Magazyn Azure, Import/Eksport Azure to odpowiednie rozwiązanie.

Zobacz [Import/Eksport Azure](storage-import-export-service.md) toolearn więcej.

## <a name="backing-up-your-data"></a>Tworzenie kopii zapasowej danych
Jeśli po prostu potrzebujesz toobackup Twojego tooAzure danych magazynu, kopia zapasowa Azure jest toogo sposób hello. To wydajne rozwiązanie tworzenia kopii zapasowych danych lokalnych i maszyn wirtualnych platformy Azure.

Zobacz [kopia zapasowa Azure](../backup/backup-introduction-to-azure-backup.md) toolearn więcej.

## <a name="accessing-your-data-on-premises-and-from-hello-cloud"></a>Uzyskiwanie dostępu do danych lokalnej i w chmurze hello
Jeśli potrzebujesz rozwiązania do uzyskiwania dostępu do danych lokalnej i w chmurze hello, następnie należy rozważyć przy użyciu platformy Azure cloud magazynu hybrydowego, StorSimple. To rozwiązanie składa się z urządzenia fizycznego StorSimple, że inteligentnie magazynów często używane dane na dyskach SSD, czasami używane dane na dyski twarde i nieaktywne/tworzenia kopii zapasowej/archiwizowanie danych w magazynie Azure.

Zobacz [StorSimple](../storsimple/storsimple-overview.md) toolearn więcej.

## <a name="recovering-your-data"></a>Odzyskiwanie danych
Gdy masz lokalne obciążeń i aplikacji, konieczne będzie rozwiązanie umożliwiający Twojej toocontinue firm uruchomione w razie awarii hello. Usługa Azure Site Recovery obsługuje replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych. Replikowane dane są przechowywane w magazynie Azure, dzięki czemu tooeliminate hello potrzebę dodatkowego centrum danych na miejscu.

Zobacz [usługi Azure Site Recovery](../site-recovery/site-recovery-overview.md) toolearn więcej.
### <a name="moving-data-faq"></a>Przenoszenie danych często zadawane pytania:
## <a name="can-i-migrate-vhds-from-one-region-tooanother-without-copying"></a>Czy można migrować wirtualne dyski twarde z jednego regionu tooanother bez kopiowania
Witaj tylko sposób toocopy wirtualne dyski twarde między region jest toocopy hello danych między kontami magazynu w każdym regionie. Narzędzia AZCopy można użyć w tym. Zobacz transferu danych za pomocą wiersza polecenia Azcopy toolearn hello więcej. W przypadku bardzo dużych ilości danych można także Import/Eksport Azure. Zobacz [Import/Eksport Azure](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) toolearn więcej.
