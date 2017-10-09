---
title: "aaaMove tooand danych z magazynu obiektów Blob z Eksploratora usługi Storage platformy Azure | Dokumentacja firmy Microsoft"
description: "Przenieś tooand danych z magazynu obiektów Blob Azure za pomocą Eksploratora usługi Storage platformy Azure"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 10bd283f-0875-4c67-af63-6492270b7656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 38d3bc009950c97d8474b0acceaf74814638dac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azure-storage-explorer"></a>Przenieś tooand danych z magazynu obiektów Blob Azure za pomocą Eksploratora usługi Storage platformy Azure
Eksplorator usługi Storage platformy Azure to bezpłatne narzędzie firmy Microsoft, która pozwala toowork z danymi usługi Azure Storage w systemie Windows, macOS i Linux. W tym temacie opisano sposób toouse go magazynu obiektów blob tooupload i pobierania danych z platformy Azure. Narzędzie Hello można pobrać z [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Jeśli używasz maszyny Wirtualnej, który został skonfigurowany z dostarczonych przez skrypty hello [maszyn wirtualnych nauki danych na platformie Azure](machine-learning-data-science-virtual-machines.md), następnie Eksploratora usługi Storage platformy Azure jest już zainstalowana na powitania maszyny Wirtualnej.
> 
> [!NOTE]
> Magazyn obiektów blob tooAzure pełne wprowadzenie zbyt znaleźć[podstawy obiektów Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) i [usługi obiektów Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).   
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Tym dokumencie przyjęto założenie, że masz subskrypcję platformy Azure, konta magazynu i hello odpowiedniego klucza magazynu dla tego konta. Przed przekazaniem/pobieranie danych, musisz znać Azure klucz konta magazynu nazwy i konta. 

* tooset zapasową subskrypcji platformy Azure, zobacz [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).
* Aby uzyskać instrukcje dotyczące tworzenia konta magazynu oraz uzyskiwanie konta i informacje o kluczu, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md). Należy to konto toohello tooconnect klucza za pomocą narzędzia Eksplorator usługi Storage Azure hello należy wprowadzić klucz Uwaga hello dostępu dla konta magazynu.
* Narzędzie do Eksploratora usługi Storage Azure Hello można pobrać z [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/). Zaakceptuj ustawienia domyślne hello podczas instalacji.

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a>Użyj Eksploratora usługi Storage platformy Azure
Witaj, jak następujące kroki dokumentu tooupload/pobierania danych przy użyciu Eksploratora usługi Storage platformy Azure. 

1. Uruchom Eksploratora usługi Storage platformy Microsoft Azure.
2. toobring się hello **Zaloguj się na koncie tooyour...**  kreatora wybierz **ustawienia konta Azure** ikony, następnie **Dodaj konto** i podać swoje poświadczenia. ![Dodawanie konta magazynu platformy Azure](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)
3. toobring się hello **połączyć tooAzure magazynu** powitania w kreatorze, wybierz pozycję **łączą magazyn tooAzure** ikony. ![Połącz tooAzure magazynu](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)
4. Wprowadź klucz dostępu hello na koncie magazynu Azure na powitania **połączyć tooAzure magazynu** kreatora, a następnie **dalej**. ![Połącz tooAzure magazynu](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)
5. Wprowadź nazwę konta magazynu w hello **nazwa konta** polu, a następnie wybierz **dalej**. ![Dołącz magazynu zewnętrznego](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)
6. Konto magazynu Hello dodany teraz powinien być wyświetlany. toocreate kontenera obiektów blob na koncie magazynu, kliknij prawym przyciskiem myszy hello **kontenerów obiektów Blob** węzłów na tym koncie, wybierz opcję **Tworzenie kontenera obiektów Blob**i wprowadź nazwę.
7. kontener tooa danych tooupload, hello wybierz docelowy kontener i kliknij przycisk hello **przekazać** przycisku.![ Konta magazynu](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)
8. Polecenie hello **...**  toohello rogu hello **pliki** wybierz jednego lub wielu tooupload pliki z systemu plików hello a kliknij **przekazać** toobegin przekazywania plików hello.![ Przekazywanie plików](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)
9. toodownload danych, wybierając hello obiektu blob w hello odpowiedniego kontenera toodownload i kliknij przycisk **Pobierz**. ![Pobierz pliki](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)

