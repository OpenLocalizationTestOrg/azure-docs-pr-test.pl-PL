---
title: Baza danych Analysis Services aaaAzure i przywracania kopii zapasowych | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak toobackup i przywracania usług Azure Analysis bazy danych."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a>Tworzenie kopii zapasowej i przywracanie

Tworzenie kopii zapasowej bazy danych modelu tabelarycznego w usług Azure Analysis Services jest znacznie Witaj takie same jak w przypadku lokalnego Analysis Services. Główną różnicą Hello służy do przechowywania plików kopii zapasowych. Pliki kopii zapasowej należy zapisać tooa kontenera w [konto magazynu Azure](../storage/common/storage-create-storage-account.md). Można było utworzyć, konfigurując ustawienia magazynu dla serwera lub służy konto magazynu i kontener, który już istnieje.

> [!NOTE]
> Tworzenie konta magazynu może skutkować nową usługą płatną. toolearn więcej, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/blobs/).
> 
> 

Kopie zapasowe są zapisywane z rozszerzeniem abf. Dla modeli tabelarycznych w pamięci zarówno w modelu danych, jak i metadane są przechowywane. Dla modeli tabelarycznych zapytania bezpośredniego są przechowywane tylko metadane modelu. Kopie zapasowe można skompresować i szyfrowane, w zależności od opcji hello. 



## <a name="configure-storage-settings"></a>Konfigurowanie ustawień magazynu
Przed utworzeniem kopii zapasowej, należy tooconfigure miejsca do magazynowania dla serwera.


### <a name="tooconfigure-storage-settings"></a>Ustawienia magazynu tooconfigure
1.  W portalu Azure > **ustawienia**, kliknij przycisk **kopii zapasowej**.

    ![Tworzenie kopii zapasowych w ustawieniach](./media/analysis-services-backup/aas-backup-backups.png)

2.  Kliknij przycisk **włączone**, następnie kliknij przycisk **ustawienia magazynu**.

    ![Włączanie](./media/analysis-services-backup/aas-backup-enable.png)

3. Wybierz konto magazynu lub Utwórz nową.

4. Wybierz kontener lub Utwórz nową.

    ![Wybierz kontener](./media/analysis-services-backup/aas-backup-container.png)

5. Zapisz ustawienia kopii zapasowej.

    ![Zapisanie ustawień kopii zapasowej](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a>Tworzenie kopii zapasowych

### <a name="toobackup-by-using-ssms"></a>toobackup przy użyciu narzędzia SSMS

1. W programie SSMS, kliknij prawym przyciskiem myszy bazę danych > **kopię zapasową**.

2. W **instrukcji Backup Database** > **plik kopii zapasowej**, kliknij przycisk **Przeglądaj**.

3. W hello **Zapisz plik jako** okna dialogowego, sprawdź, czy ścieżka folderu hello, a następnie wpisz nazwę pliku kopii zapasowej hello. 

4. W hello **instrukcji Backup Database** okno dialogowe, wybierz pozycję Opcje.

    **Plik zastąpić** — wybierz to opcja toooverwrite pliki kopii zapasowej hello tej samej nazwy. Jeśli ta opcja nie jest zaznaczona, zapisujesz plik hello nie może mieć hello takie same nazwy jako plik już istnieje w hello sam lokalizacji.

    **Zastosowanie kompresji** — wybierz tej opcję toocompress hello plik kopii zapasowej. Skompresowane pliki kopii zapasowej zaoszczędzić miejsce na dysku, ale wymaga nieco większe użycie procesora CPU. 

    **Szyfrowanie pliku kopii zapasowej** — wybierz tej opcję tooencrypt hello plik kopii zapasowej. Ta opcja wymaga hasła podanego przez użytkownika toosecure hello plik kopii zapasowej. Witaj hasło zapobiega odczytywanie danych kopii zapasowej hello inny sposób niż operacji przywracania. Jeśli wybierzesz tooencrypt kopii zapasowych, przechowywać hello hasła w bezpiecznym miejscu.

5. Kliknij przycisk **OK** toocreate i Zapisz plik kopii zapasowej hello.


### <a name="powershell"></a>PowerShell
Użyj [ASDatabase kopii zapasowej](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) polecenia cmdlet.

## <a name="restore"></a>Przywracanie
Podczas przywracania, pliku kopii zapasowej musi być na koncie magazynu hello skonfigurowanego dla serwera. Toomove plik kopii zapasowej z konta magazynu tooyour lokalizacji lokalnej, należy użyć [Eksploratora usługi Microsoft Azure Storage](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) lub hello [AzCopy](../storage/common/storage-use-azcopy.md) narzędzia wiersza polecenia. 



> [!NOTE]
> Jeśli jest przywracana z lokalnego serwera, należy usunąć wszystkich użytkowników domeny hello z modelu hello ról i dodać je kopii toohello ról jako użytkowników usługi Azure Active Directory.
> 
> 

### <a name="toorestore-by-using-ssms"></a>toorestore przy użyciu narzędzia SSMS

1. W programie SSMS, kliknij prawym przyciskiem myszy bazę danych > **przywrócić**.

2. W hello **instrukcji Backup Database** okna dialogowego, w **plik kopii zapasowej**, kliknij przycisk **Przeglądaj**.

3. W hello **zlokalizować pliki bazy danych** okno dialogowe, wybierz hello pliku, który chcesz toorestore.

4. W **Przywróć bazę danych**, wybierz pozycję hello bazy danych.

5. Określ opcje. Opcje zabezpieczeń muszą być zgodne hello opcje tworzenia kopii zapasowej, używane podczas wykonywania kopii zapasowej.


### <a name="powershell"></a>PowerShell

Użyj [ASDatabase przywracania](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) polecenia cmdlet.


## <a name="related-information"></a>Informacje pokrewne

[Konta magazynu platformy Azure](../storage/common/storage-create-storage-account.md)  
[Wysoka dostępność](analysis-services-bcdr.md)     
[Zarządzanie usług Azure Analysis Services](analysis-services-manage.md)
