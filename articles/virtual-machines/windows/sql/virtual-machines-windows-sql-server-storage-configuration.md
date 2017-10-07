---
title: Konfiguracja aaaStorage dla maszyn wirtualnych programu SQL Server | Dokumentacja firmy Microsoft
description: "W tym temacie opisano, jak Azure konfiguruje magazynu dla maszyn wirtualnych programu SQL Server podczas inicjowania obsługi administracyjnej (modelu wdrażania usługi Resource Manager). Wyjaśniono również, jak skonfigurować magazyn dla istniejących maszyn wirtualnych serwera SQL."
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 169fc765-3269-48fa-83f1-9fe3e4e40947
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: ninarn
ms.openlocfilehash: b50dbd698828780cfc044fa0966e8f4e2f3bb6c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storage-configuration-for-sql-server-vms"></a>Konfigurację magazynu dla maszyn wirtualnych programu SQL Server
Po skonfigurowaniu obraz maszyny wirtualnej programu SQL Server na platformie Azure hello portalu pomaga tooautomate konfigurację magazynu. Dotyczy to również dołączanie toohello magazynu maszyny Wirtualnej, udostępniania tego tooSQL dostępny magazyn serwera i jego konfigurowania toooptimize dla wymagania dotyczące wydajności.

W tym temacie wyjaśniono, jak Azure konfiguruje magazynu dla maszyn wirtualnych programu SQL Server podczas inicjowania obsługi administracyjnej oraz dla istniejących maszyn wirtualnych. Ta konfiguracja jest oparta na powitania [najlepsze rozwiązania w zakresie wydajności](virtual-machines-windows-sql-performance.md) dla maszyn wirtualnych platformy Azure, programem SQL Server.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Wymagania wstępne
toouse hello automatycznego ustawienia konfiguracji magazynu, Twoja maszyna wirtualna wymaga hello następujące cechy:

* Z udostępnionym [obraz w galerii programu SQL Server](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing).
* Używa hello [modelu wdrażania usługi Resource Manager](../../../azure-resource-manager/resource-manager-deployment-model.md).
* Używa [magazyn w warstwie Premium](../../../storage/common/storage-premium-storage.md).

## <a name="new-vms"></a>Nowe maszyny wirtualne
Witaj poniższych sekcjach opisano sposób tooconfigure magazynu dla maszyn wirtualnych programu SQL Server.

### <a name="azure-portal"></a>Azure Portal
Podczas inicjowania obsługi maszyny Wirtualnej platformy Azure przy użyciu obrazu galerii programu SQL Server, można wybrać tooautomatically Konfigurowanie hello magazynu dla nowej maszyny Wirtualnej. Należy określić rozmiar magazynu hello, ograniczeń wydajności i typ obciążenia pracą. Witaj Poniższy zrzut ekranu przedstawia blok konfiguracji magazynu hello używane podczas maszyny Wirtualnej SQL inicjowania obsługi administracyjnej.

![Konfiguracja magazynu maszyny Wirtualnej programu SQL Server podczas inicjowania obsługi](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-provisioning.png)

W oparciu o wybrane opcje, Azure wykonuje hello następujących zadań konfiguracji magazynu po utworzeniu hello maszyny Wirtualnej:

* Tworzy i dołącza maszynę wirtualną toohello dysków premium magazynu danych.
* Konfiguruje hello danych dysków toobe dostępny tooSQL serwera.
* Konfiguruje hello dyski danych do magazynu puli hello określone wymagania rozmiaru i wydajności (IOPS i przepływność).
* Kojarzy hello puli magazynu o nowy dysk na maszynie wirtualnej hello.
* Optymalizuje ten nowy dysk, na podstawie Twojej typu określonego obciążenia (magazynowanie danych, przetwarzanie transakcji, lub ogólne).

Aby uzyskać więcej szczegółowych informacji dotyczących sposobu Azure umożliwia skonfigurowanie ustawień magazynu, zobacz hello [sekcji konfiguracji magazynu](#storage-configuration). Pełny przewodnik toocreate maszyna wirtualna serwera SQL w hello portalu Azure, zobacz temat [hello inicjowania obsługi administracyjnej samouczek](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="resource-manage-templates"></a>Szablony Zarządzaj zasobów
Jeśli używasz hello następujące szablony Menedżera zasobów dwóch dysków danych w warstwie premium są dołączone domyślnie z nie konfiguracji puli magazynu. Można jednak dostosować te szablony toochange hello liczba dysków danych — warstwa premium, które są dołączone toohello maszyny wirtualnej.

* [Tworzenie maszyny Wirtualnej z automatycznego tworzenia kopii zapasowej](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autobackup)
* [Tworzenie maszyny Wirtualnej z automatyczne stosowanie poprawek](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autopatching)
* [Tworzenie maszyny Wirtualnej z Integracja](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-keyvault)

## <a name="existing-vms"></a>Istniejące maszyny wirtualne
Dla istniejących maszyn wirtualnych serwera SQL można zmodyfikować niektórych ustawień magazynu hello portalu Azure. Wybierz maszyny Wirtualnej, przejdź do obszaru Ustawienia toohello, a następnie wybierz konfiguracji serwera SQL. Blok konfiguracji serwera SQL Hello pokazuje hello bieżące użycie magazynu maszyny wirtualnej. Wszystkie dyski, które istnieją na maszynie Wirtualnej są wyświetlane na tym wykresie. Dla każdego dysku miejsca do magazynowania hello jest wyświetlany w cztery sekcje:

* Danych SQL
* Dziennika SQL
* Inne (z systemem innym niż SQL magazynu)
* Dostępna

![Konfigurowanie magazynu dla istniejącego programu SQL Server maszyny Wirtualnej](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-existing.png)

tooconfigure hello tooadd magazynu nowego dysku lub Rozszerz istniejący dysk, kliknij przycisk łącza edycji hello powyżej hello wykresu.

Opcje konfiguracji Hello widoczne jest różny w zależności od tego, czy używasz tej funkcji przed. Korzystając z powitania po raz pierwszy, można określić wymagania dotyczące magazynowania dla nowego dysku. Jeśli poprzednio korzystano tej funkcji toocreate dysku, można wybrać tooextend magazynu tego dysku.

### <a name="use-for-hello-first-time"></a>Na użytek powitania po raz pierwszy
Jeśli jest używany po raz pierwszy za pomocą tej funkcji, można określić hello limity rozmiaru i wydajności magazynu dla nowego dysku. To środowisko jest podobne toowhat, dostępne w inicjowania obsługi administracyjnej czasu. Witaj podstawowa różnica polega na tym, nie są dozwolone toospecify hello obciążenia typu. Tego ograniczenia zapobiega zakłócania wszystkie istniejące konfiguracje programu SQL Server na maszynie wirtualnej hello.

![Konfigurowanie programu SQL Server magazynu suwaki](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-usage-sliders.png)

Platforma Azure tworzy nowy dysk, na podstawie specyfikacji użytkownika. W tym scenariuszu Azure wykonuje hello następujących zadań konfiguracji magazynu:

* Tworzy i dołącza maszynę wirtualną toohello dysków premium magazynu danych.
* Konfiguruje hello danych dysków toobe dostępny tooSQL serwera.
* Konfiguruje hello dyski danych do magazynu puli hello określone wymagania rozmiaru i wydajności (IOPS i przepływność).
* Kojarzy hello puli magazynu o nowy dysk na maszynie wirtualnej hello.

Aby uzyskać więcej szczegółowych informacji dotyczących sposobu Azure umożliwia skonfigurowanie ustawień magazynu, zobacz hello [sekcji konfiguracji magazynu](#storage-configuration).

### <a name="add-a-new-drive"></a>Dodaj nowy dysk
Jeśli został już skonfigurowany magazyn na maszyną Wirtualną programu SQL Server, rozszerzanie magazynu powoduje wyświetlenie dwóch nowych opcji. Pierwsza opcja Hello jest tooadd nowego dysku, co może zwiększyć poziom wydajności hello maszyny wirtualnej.

![Dodaj nowy tooa dysku maszyny Wirtualnej SQL](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-add-new-drive.png)

Jednak po dodaniu dysku hello, należy wykonać niektóre wzrost wydajności hello tooachieve bardzo ręcznej konfiguracji.

### <a name="extend-hello-drive"></a>Rozszerz dysk hello
Witaj innych możliwości rozszerzania magazynu jest tooextend hello istniejącego dysku. Ta opcja zwiększa hello dostępny magazyn na dysku, ale nie zwiększa wydajność. Używając puli magazynu nie można zmienić hello liczba kolumn, po utworzeniu puli magazynu hello. Witaj liczbę kolumn określa hello liczbę równoległych zapisy, które mogą być rozkładane na dyskach danych hello. W związku z tym wszystkie dyski dodane danych nie może zwiększyć wydajność. Użytkownik tylko podać więcej pamięci masowej dla danych hello zapisywana. To ograniczenie również oznacza, że, podczas rozszerzania dysku hello, hello liczbę kolumn określa hello minimalna liczba dysków z danymi, które można dodać. Dlatego po utworzeniu puli magazynów z dysków z danymi cztery hello liczba kolumn jest również cztery. Zawsze, gdy rozszerzenie hello magazynu, należy dodać dysków z danymi co najmniej cztery.

![Rozszerz dysk maszyny wirtualnej SQL](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-extend-a-drive.png)

## <a name="storage-configuration"></a>Konfiguracja usługi Storage
Ta sekcja zawiera odwołanie do zmian konfiguracji magazynu hello Azure automatycznie wykonuje podczas obsługi maszyny Wirtualnej SQL i konfiguracji w hello portalu Azure.

* Jeśli wybrano mniej niż dwóch tabel magazynu dla maszyny Wirtualnej, Azure nie powoduje utworzenia puli magazynu.
* Jeśli wybrano co najmniej dwóch tabel magazynu dla maszyny Wirtualnej, Azure konfiguruje pulę magazynu. Witaj w następnej sekcji tego tematu zawiera szczegóły hello hello w konfiguracji puli magazynu.
* Automatyczne magazynu konfiguracji zawsze używa [magazyn w warstwie premium](../../../storage/common/storage-premium-storage.md) P30 dysków z danymi. W rezultacie 1:1 mapowania między wybranej liczby terabajty i hello liczba dysków danych dołączone tooyour maszyny Wirtualnej.

Aby uzyskać informacje o cenach, zobacz hello [cennik Storage](https://azure.microsoft.com/pricing/details/storage) strony na powitania **Magazyn dyskowy** kartę.

### <a name="creation-of-hello-storage-pool"></a>Tworzenie puli magazynu hello
Platforma Azure korzysta powitania po puli magazynów hello toocreate ustawień na maszynach wirtualnych serwera SQL.

| Ustawienie | Wartość |
| --- | --- |
| Rozmiar usługi STRIPE |256 KB (magazynowanie danych); 64 KB (transakcyjnej) |
| Rozmiary dysków |1 TB |
| Pamięć podręczna |Odczyt |
| Rozmiar alokacji |Rozmiar jednostki alokacji systemu plików NTFS 64 KB |
| Inicjowanie błyskawicznych plików |Enabled (Włączony) |
| Blokowanie stron w pamięci |Enabled (Włączony) |
| Odzyskiwanie |Odzyskiwania prostego (Brak odporności) |
| Liczba kolumn |Liczba dysków danych<sup>1</sup> |
| Lokalizacja bazy danych TempDB |Przechowywane na dyskach danych<sup>2</sup> |

<sup>1</sup> po utworzeniu puli magazynu hello, nie można zmienić hello liczba kolumn w puli magazynu hello.

<sup>2</sup> to ustawienie dotyczy tylko pierwszego dysku toohello utworzonych za pomocą funkcji konfiguracji hello magazynu.

## <a name="workload-optimization-settings"></a>Ustawienia optymalizacji obciążenia
Witaj poniższej tabeli opisano hello trzy obciążenia typu dostępne opcje oraz ich odpowiednich optymalizacje:

| Typ obciążenia | Opis | Optymalizacje |
| --- | --- | --- |
| **Ogólne** |Ustawienie domyślne obsługujące większość obciążeń |Brak |
| **Przetwarzania transakcyjnego** |Optymalizuje hello magazynowania dla obciążeń OLTP tradycyjne bazy danych |Flaga śledzenia 1117<br/>Flaga śledzenia 1118 |
| **Magazynowania danych** |Optymalizuje magazyn hello analizą i raportami obciążeń |Flaga śledzenia 610<br/>Flaga śledzenia 1117 |

> [!NOTE]
> Typ obciążenia hello można określić tylko podczas obsługi administracyjnej maszyny wirtualnej SQL, wybierz je w kroku konfiguracji magazynu hello.
>
>

## <a name="next-steps"></a>Następne kroki
Dla innych tematach dotyczących toorunning programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych Azure](virtual-machines-windows-sql-server-iaas-overview.md).
