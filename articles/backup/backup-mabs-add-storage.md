---
title: "aaaUse nowoczesnych magazynu kopii zapasowej z serwera usługi Kopia zapasowa Azure w wersji 2 | Dokumentacja firmy Microsoft"
description: "Informacje o nowych funkcjach hello v2 serwer kopii zapasowej Azure. W tym artykule opisano sposób tooupgrade instalacją serwera kopii zapasowej."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a>Dodaj tooAzure magazynu kopii zapasowej serwera v2

Azure v2 Utwórz kopię zapasową serwera jest dostarczany z System Center 2016 ochrony Menedżera Modern kopii zapasowej pamięci masowej. Nowoczesne magazynu kopii zapasowej oferuje oszczędności pojemności magazynu 50 procent kopii zapasowych, które są trzy razy szybszych i bardziej wydajnych magazynu. Zapewnia także magazynu obsługującej obciążenie. 

> [!NOTE]
> toouse nowoczesnych magazynu kopii zapasowej, należy uruchomić v2 Utwórz kopię zapasową serwera w systemie Windows Server 2016. Po uruchomieniu v2 Utwórz kopię zapasową serwera we wcześniejszej wersji systemu Windows Server, serwer kopii zapasowej Azure nie może korzystać z nowoczesnych magazynu kopii zapasowej. Zamiast tego chroni ona obciążenia, jak w przypadku v1 Utwórz kopię zapasową serwera. Aby uzyskać więcej informacji, zobacz wersji kopii zapasowej serwera hello [macierzy ochrony](backup-mabs-protection-matrix.md).

## <a name="volumes-in-backup-server-v2"></a>Woluminy w kopii zapasowej serwera v2

Kopia zapasowa v2 Server akceptuje woluminów magazynu. Podczas dodawania woluminu, Utwórz kopię zapasową serwera formatuje hello tooResilient woluminu systemu plików ReFS, co wymaga nowoczesnej magazynu kopii zapasowej. tooadd woluminu, a tooexpand go później, jeśli zajdzie potrzeba, zaleca się używanie tego przepływu pracy:

1.  Skonfiguruj serwer zapasowy v2 na maszynie Wirtualnej.
2.  Utwórz wolumin na dysku wirtualnego w puli magazynów:
    1.  Dodaj pulę magazynu tooa dysk i Utwórz dysk wirtualny z układ prosty.
    2.  Dodaj dodatkowe dyski i rozszerzyć hello dysku wirtualnego.
    3.  Utworzyć woluminy na powitania dysku wirtualnego.
3.  Dodaj tooBackup woluminów powitania serwera.
4.  Konfigurowanie magazynu obsługującej obciążenie.

## <a name="create-a-volume-for-modern-backup-storage"></a>Tworzenie woluminu dla nowoczesnych magazynu kopii zapasowej

Użycie v2 Utwórz kopię zapasową serwera z woluminami jako magazynu danych na dysku może pomóc zachować kontrolę nad magazynu. Wolumin może być także jeden dysk. Jednak tooextend magazynu w hello przyszłych, utworzyć wolumin poza dysk utworzony przy użyciu funkcji miejsca do magazynowania. Może to ułatwić, jeśli chcesz tooexpand hello wolumin magazynu kopii zapasowej. Ta sekcja zawiera najlepsze rozwiązania dotyczące tworzenia woluminu z tej instalacji.

1. W Menedżerze serwera wybierz **usług plików i magazynowania** > **woluminów** > **pule magazynu**. W obszarze **dysków fizycznych**, wybierz pozycję **nowa pula magazynu**. 

    ![Tworzenie nowej puli magazynu](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. W hello **zadania** listy rozwijanej wybierz pozycję **nowego dysku wirtualnego**.

    ![Dodaj dysk wirtualny](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. Wybierz pulę magazynu hello, a następnie wybierz **Dodaj dysk fizyczny**.

    ![Dodaj dysk fizyczny](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. Wybierz dysk fizyczny hello, a następnie wybierz **Rozszerz dysk wirtualny**.

    ![Rozszerzanie dysku wirtualnego hello](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. Wybierz hello dysku wirtualnego, a następnie wybierz **nowy wolumin**.

    ![Utwórz nowy wolumin](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. W hello **wybierz powitania serwera i dysku** okno dialogowe, wybierz powitania serwera i hello nowego dysku. Następnie wybierz opcję **dalej**.

    ![Wybierz powitania serwera i dysku](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a>Dodawanie magazynu dyskowego serwera tooBackup woluminów

tooadd tooBackup woluminu serwera, w hello **zarządzania** okienku ponownego skanowania magazynu hello, a następnie wybierz **Dodaj**. Zostanie wyświetlona lista wszystkich hello woluminów dostępnych toobe dodane do magazynu kopii zapasowej serwera. Po dodaniu toohello Lista wybranych woluminów dostępnych woluminów, można przekazać toohelp przyjaznej nazwy, zarządzać nimi. tooformat tooReFS tych woluminów, Utwórz kopię zapasową serwera można użyć hello zalet nowoczesnych magazynu kopii zapasowej, wybierz **OK**.

![Dodaj dostępne woluminy](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a>Konfigurowanie magazynu obsługującej obciążenie

Z magazynu obsługujących obciążenie można wybrać hello woluminami preferencyjnie przechowywania określonych rodzajów obciążeń. Na przykład można ustawić kosztowne woluminów, które obsługują dużej liczby operacji wejścia/wyjścia na drugi (IOPS) toostore tylko hello obciążeń, które wymagają częstego, dużej liczby kopii zapasowych. Przykładem jest program SQL Server z dzienników transakcji. Inne obciążenia, których kopii zapasowej rzadziej, takich jak maszyny wirtualne, utworzeniem kopii zapasowej woluminów toolow kosztów.

### <a name="update-dpmdiskstorage"></a>DPMDiskStorage aktualizacji

Magazyn obsługujący obciążenia można skonfigurować za pomocą polecenia cmdlet programu PowerShell hello Update-DPMDiskStorage, która aktualizuje właściwości hello woluminu w puli magazynu hello na serwerze programu Data Protection Manager.

Składnia:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
Witaj Poniższy zrzut ekranu przedstawia polecenie cmdlet Update-DPMDiskStorage hello w oknie programu PowerShell hello.

![polecenie Update-DPMDiskStorage w oknie programu PowerShell hello Hello](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

zmiany Hello przy użyciu programu PowerShell są odzwierciedlane w hello konsoli administratora serwera kopii zapasowej.

![Dyski i woluminy w hello konsoli administratora](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a>Następne kroki
Po zainstalowaniu serwera kopii zapasowej, Dowiedz się jak tooprepare serwera, lub Włącz ochronę obciążeń.

- [Przygotowanie serwera kopii zapasowej obciążeń](backup-azure-microsoft-azure-backup.md)
- [Użyj tooback serwera kopii zapasowej serwera VMware](backup-azure-backup-server-vmware.md)
- [Użyj tooback serwera kopii zapasowej serwera SQL](backup-azure-sql-mabs.md)

