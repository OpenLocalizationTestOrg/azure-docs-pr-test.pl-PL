---
title: "Wprowadzenie do magazynu obiektów Blob platformy Azure | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do magazynu obiektów Blob platformy Azure"
services: storage
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/28/2017
ms.author: tamram
ms.openlocfilehash: 0097f1c02b88343a135b6489130a6e0d35cf6fba
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="introduction-to-blob-storage"></a>Wprowadzenie do magazynu obiektów Blob

Azure Blob Storage to usługa do przechowywania dużych ilości danych obiektów niestrukturalnych, takich jak dane tekstowe lub binarne, do których można uzyskać dostęp z dowolnego miejsca na świecie za pośrednictwem protokołu HTTP lub HTTPS. Magazyn obiektów Blob może być użyty do udostępniania danych publicznie lub do przechowywania danych aplikacji prywatnie.

Najczęstsze zastosowania usługi Blob Storage obejmują:

* Obsługiwanie obrazów i dokumentów bezpośrednio w przeglądarce
* Przechowywanie plików do dostępu rozproszonego
* Przesyłanie strumieniowe audio i wideo
* Zapisywanie danych w celu tworzenia kopii zapasowych, przywracania, odzyskiwania po awarii i archiwizowania
* Przechowywanie danych w celu analizy w usłudze lokalnej lub hostowanej na platformie Azure

## <a name="blob-service-concepts"></a>Pojęcia dotyczące usługi Blob

Usługa Blob obejmuje następujące składniki:

![Architektura obiektów blob](./media/storage-blobs-introduction/blob1.png)

* **Konto magazynu:** cały dostęp do usługi Azure Storage odbywa się przez konto magazynu. Konto magazynu może być **konta magazynu ogólnego przeznaczenia (v1 lub v2)** lub **konta usługi Blob storage**. Aby uzyskać więcej informacji, zobacz [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Informacje o kontach usługi Azure Storage).

* **Kontener:** kontener zawiera grupowanie zestawu obiektów blob. Wszystkie obiekty blob muszą być w kontenerze. Konto może zawierać nieograniczoną liczbę kontenerów. Kontener może przechowywać nieograniczoną liczbę obiektów blob. Pamiętaj, że wszystkie litery w nazwie kontenera muszą być małymi literami.

* **Obiekt blob:** plik dowolnego typu o dowolnym rozmiarze. Usługa Azure Storage udostępnia trzy typy obiektów blob: blokowe obiekty BLOB, [stronicowe](storage-blob-pageblob-overview.md)i uzupełnialnych obiektów blob.
  
    *Blokowe obiekty blob* idealnie nadają się do przechowywania tekstu lub plików binarnych, takich dokumenty czy pliki multimedialne. *Uzupełnialne obiekty blob* są podobne do obiektów blokowych, ponieważ składają się z bloków, ale zoptymalizowane do operacji uzupełnialnych, więc przydatne w scenariuszach logowania. Pojedynczy blokowy obiekt blob może zawierać do 50 000 bloków do 100 MB każdy, których rozmiar całkowity może nieco przekraczać 4.75 TB (100 MB X 50 000). Pojedynczy uzupełniany obiekt blob może zawierać do 50 000 bloków do 4 MB każdy, których rozmiar całkowity może nieco przekraczać 195 GB (4 MB X 50 000).
  
    *Stronicowe obiekty BLOB* może mieć maksymalnie 8 TB i są bardziej efektywne w przypadku operacji częstego odczytu/zapisu. Usługa Azure Virtual Machines używa stronicowych obiektów blob jako systemu operacyjnego lub dysków z danymi.
  
    Aby uzyskać szczegółowe informacje o nazewnictwie kontenerów i obiektów blob, zobacz temat [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) (Nazewnictwo i odwoływanie się do kontenerów, obiektów blob i metadanych).

## <a name="next-steps"></a>Kolejne kroki

* [Tworzenie konta magazynu](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Wprowadzenie do magazynu obiektów Blob przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md)
* [Przykładów dla magazynu platformy Azure przy użyciu platformy .NET](../common/storage-samples-dotnet.md)
* [Przykładów dla magazynu platformy Azure przy użyciu języka Java](../common/storage-samples-java.md)
