---
title: aaaHD magazynu opartego na ekonomicznych standardowych i dyski maszyny Wirtualnej Azure | Dokumentacja firmy Microsoft
description: "Omówiono w nim ekonomicznego magazynowania standardowe i niezarządzane i zarządzane dyski maszyny Wirtualnej."
services: storage
documentationcenter: 
author: yuemlu
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: yuemlu
ms.openlocfilehash: c9162eaea50cdd43862378e62dcff9a3d762e092
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cost-effective-standard-storage-and-unmanaged-and-managed-azure-vm-disks"></a>Ekonomiczne Standard Storage i dysków maszyny Wirtualnej Azure niezarządzane i zarządzane

Azure Standard Storage zapewnia obsługę niezawodnych, tanich dysków dla maszyn wirtualnych obciążeniami niezależnych od opóźnienia. Obsługuje ona również obiekty BLOB, tabel, kolejek i plików. Z magazynu w warstwie standardowa hello dane są przechowywane na dyskach twardych (HDD). Podczas pracy z maszyn wirtualnych, można użyć dysków magazynu w warstwie standardowa scenariusze tworzenia/testowania i mniej istotny obciążeń i dyski magazynu premium przez aplikacje produkcyjne o znaczeniu krytycznym. Standardowy magazyn jest dostępny we wszystkich regionach platformy Azure. 

Ten artykuł koncentruje się na użycie hello standard Storage dla dysków maszyny Wirtualnej. Aby uzyskać więcej informacji na temat używania hello magazynu z obiektów blob, tabel, kolejek i plików można znaleźć toohello [tooStorage wprowadzenie](../storage-introduction.md).

## <a name="disk-types"></a>Typy dysków

Istnieją dwa sposoby toocreate dyski standardowe dla maszyn wirtualnych platformy Azure:

**Niezarządzane dysków**: jest hello oryginalnej metody, w których zarządzasz hello magazynu kont używanych toostore hello plików VHD, które odpowiadają toohello dysków maszyny Wirtualnej. Pliki VHD są przechowywane jako stronicowe obiekty BLOB na kontach magazynu. Niezarządzane dyski mogą być dołączone tooany rozmiar maszyny Wirtualnej Azure, w tym hello maszyn wirtualnych, przede wszystkim używających magazyn w warstwie Premium, takich jak hello DSv2 i GS serii. Maszyny wirtualne platformy Azure obsługuje podłączania kilka dyski standardowe, umożliwiając się too256 TB pamięci masowej dla maszyny Wirtualnej.

[**Azure dysków zarządzanych**](../../virtual-machines/windows/managed-disks-overview.md): Ta funkcja zarządzania kontami magazynu hello użył hello dysków maszyny Wirtualnej dla Ciebie. Określ typ hello (Premium lub Standard) oraz rozmiar dysku należy i Azure tworzy i zarządza hello dysku. Nie masz tooworry o umieszczenie dysków hello za wiele kont magazynu w kolejności tooensure się, że pozostać w hello limity skalowalności w przypadku kont magazynu hello — Azure obsługuje, który automatycznie.

Mimo że oba typy dysków są dostępne, zalecamy używanie dysków zarządzanych zalety tootake ich wielu funkcji.

tooget wprowadzenie do usługi Azure Standard Storage, odwiedź stronę [zacznij pracę bezpłatnie](https://azure.microsoft.com/pricing/free-trial/). 

Aby uzyskać informacje dotyczące sposobu toocreate maszynę Wirtualną za pomocą zarządzania dyskami Zobacz jedną z następujących hello artykułów.

* [Tworzenie maszyny wirtualnej przy użyciu usługi Resource Manager i programu PowerShell](/azure/virtual-machines/windows/quick-create-powershell.md)
* [Utwórz Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 2.0](../../virtual-machines/windows/quick-create-cli.md)

## <a name="standard-storage-features"></a>Funkcje magazynu w warstwie standardowa 

Spójrzmy na niektóre funkcje hello Standard Storage. Aby uzyskać więcej informacji, zobacz [tooAzure wprowadzenie magazynu](../storage-introduction.md).

**Standard Storage**: usługi Azure Standard Storage obsługuje dysków Azure, obiektów blob Azure, Magazyn plików Azure, tabel Azure i kolejek Azure. usługi magazynu w warstwie standardowa toouse, uruchomione z [Tworzenie konta usługi Azure Storage](storage-create-storage-account.md#create-a-storage-account).

**Dyski standardowe magazynu:** magazynu w warstwie standardowa dyski mogą być dołączony maszynach wirtualnych platformy Azure tooall tym rozmiar serii maszyn wirtualnych używane z magazyn w warstwie Premium, takich jak hello DSv2 i GS serii. Dysk magazynu w warstwie standardowa może być tylko dołączone tooone maszyny Wirtualnej. Jednak możesz dołączyć co najmniej jednego z tych dysków tooa maszyny Wirtualnej, się liczba maksymalna liczba dyskowych operacji toohello zdefiniowane dla tego rozmiaru maszyny Wirtualnej. W następujących sekcji w cele dotyczące wydajności i skalowalności magazynu standardowego hello możemy opisano specyfikacje hello bardziej szczegółowo. 

**Standardowa stronicowych obiektów blob**: standardowy stronicowe obiekty BLOB są używane toohold stałe dyski dla maszyn wirtualnych i mogą również uzyskiwać bezpośrednio za pomocą REST, podobnie jak inne typy obiektów blob Azure. [Stronicowe obiekty BLOB](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) to zbiór stron 512-bajtowych zoptymalizowane pod kątem losowego odczytu i zapisu. 

**Replikacja magazynu:** w większości regionów, dane na koncie magazynu w warstwie standardowa mogą być replikowane lokalnie replikacją geograficzną w wielu centrach danych. Witaj cztery typy replikacji dostępne są magazyn lokalnie nadmiarowy (LRS), Magazyn Strefowo nadmiarowy (ZRS) i magazynu geograficznie nadmiarowego (GRS) oraz dostęp do odczytu magazynu geograficznie nadmiarowego (RA-GRS). Dysków zarządzanych w Standard Storage obsługuje obecnie magazyn lokalnie nadmiarowy (LRS) tylko. Aby uzyskać więcej informacji, zobacz [replikacji magazynu](../storage-redundancy.md).

## <a name="scalability-and-performance-targets"></a>Cele dotyczące skalowalności i wydajności

W tej sekcji zostaną przedstawione cele wydajności i skalowalności hello potrzebne tooconsider za pomocą magazynu w warstwie standardowa.

### <a name="account-limits--does-not-apply-toomanaged-disks"></a>Limity konta — nie ma zastosowania toomanaged dysków

| **Zasób** | **Limit domyślny** |
|--------------|-------------------|
| TB na konto magazynu  | 500 TB. |
| Maksymalna liczba wejściowych<sup>1</sup> na konto magazynu (nam regiony) | 10 GB/s włączenie GRS/ZRS, 20 GB/s dla LRS |
| Maksymalna liczba wyjście<sup>1</sup> na konto magazynu (nam regiony) | 20 GB/s włączenie RA-GRS/GRS/ZRS 30 GB/s dla LRS |
| Maksymalna liczba wejściowych<sup>1</sup> na konto magazynu (Europejskiej i regiony wschodniej) | 5 GB/s włączenie GRS/ZRS 10 GB/s dla LRS |
| Maksymalna liczba wyjście<sup>1</sup> na konto magazynu (Europejskiej i regiony wschodniej) | 10 GB/s włączenie RA-GRS/GRS/ZRS, 15 GB/s dla LRS |
| Całkowita liczba żądań stawka za transakcje (w przypadku obiektu o rozmiarze 1 KB) konta magazynu | Too20, 000 IOPS, jednostek na sekundę lub wiadomości na sekundę |

<sup>1</sup> wejściowych odwołuje się tooall danych (liczba żądań) są wysyłane tooa konta magazynu. Transfer danych wychodzących odwołuje się tooall danych (odpowiedzi) odbierane z konta magazynu.

Aby uzyskać więcej informacji, zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](../storage-scalability-targets.md).

Jeśli aplikacji hello musi przekroczyć hello wartości docelowe skalowalności konta magazynu jednego, kompilacji toouse Twojej aplikacji z wielu kont magazynu, a partycji danych przez tych kont magazynu. Alternatywnie można dysków zarządzanych Azure i Azure będzie zarządzać hello partycjonowania i umieszczenia danych dla Ciebie.

### <a name="standard-disks-limits"></a>Dyski standardowe, limity

W przeciwieństwie do dysków Premium hello operacje wejścia/wyjścia na sekundę (IOPS) i przepływności (przepustowość) dyski standardowe nie są udostępnione. Hello wydajności dyski standardowe zależy od hello maszyny Wirtualnej jest dołączony rozmiar toowhich hello dysku, nie toohello rozmiar dysku hello. Można spodziewać się tooachieve się toohello limit wydajności wymienione w poniższej tabeli hello.

**Dyski standardowe limity (zarządzanych i niezarządzanych)**

| **Warstwy maszyny Wirtualnej**            | **Maszyna wirtualna w warstwie podstawowej** | **Maszyna wirtualna w warstwie standardowa** |
|------------------------|-------------------|----------------------|
| Rozmiar maksymalny dysku          | 4095 GB           | 4095 GB              |
| Maksymalna liczba 8 KB IOPS dla każdego dysku | Zapasowej too300         | Zapasowej too500            |
| Maksymalna przepustowość dla każdego dysku | Zapasowej too60 MB/s     | Zapasowej too60 MB/s        |

Jeśli obciążenie wymaga obsługi wysokiej wydajności i małych opóźnieniach dysku, należy rozważyć przy użyciu magazyn w warstwie Premium. tooknow więcej zalet magazyn w warstwie Premium, odwiedź stronę [magazyn w warstwie Premium wysokiej wydajności i dyski maszyny Wirtualnej Azure](../storage-premium-storage.md). 

## <a name="snapshots-and-copy-blob"></a>Migawki i kopii obiektu blob

toohello plik wirtualnego dysku twardego hello magazynu usługi jest stronicowych obiektów blob. Twórz migawki stronicowe obiekty BLOB i skopiuj je tooanother lokalizacji, takiej jak innego konta magazynu.

### <a name="unmanaged-disks"></a>Dyski niezarządzane

Można utworzyć [przyrostowe migawki](../../virtual-machines/windows/incremental-snapshots.md) dla niezarządzanego standard dyski w hello takie same jak migawki z magazynu w warstwie standardowa. Zaleca się tworzenie migawki, a następnie skopiować te konta migawki tooa standardowy magazyn geograficznie nadmiarowy, jeśli dysk źródłowy jest konto magazyn lokalnie nadmiarowy. Aby uzyskać więcej informacji, zobacz [opcje nadmiarowość magazynu Azure](../storage-redundancy.md).

Jeśli dysk jest dołączona tooa maszyny Wirtualnej, niektóre operacje interfejsu API na dyskach hello są niedozwolone. Na przykład nie można wykonać [kopiowania obiektu Blob](/rest/api/storageservices/Copy-Blob) operacji dla tego obiektu blob dysku hello jest dołączony tooa maszyny Wirtualnej. Zamiast tego należy najpierw utworzyć migawkę tego obiektu blob przy użyciu hello [migawki obiektu Blob](/rest/api/storageservices/Snapshot-Blob) metody interfejsu API REST, a następnie wykonaj hello [kopiowania obiektu Blob](/rest/api/storageservices/Copy-Blob) z hello migawki toocopy hello dołączono dysk. Alternatywnie można odłączyć dysku hello, a następnie wykonaj wszystkie niezbędne operacje.

toomaintain geograficznie nadmiarowego kopie z migawki, możesz skopiować migawki z konta standardowe magazynu geograficznie nadmiarowego tooa konto magazyn lokalnie nadmiarowy przy użyciu narzędzia AzCopy lub kopiowania obiektu Blob. Aby uzyskać więcej informacji, zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md) i [kopiowania obiektu Blob](/rest/api/storageservices/Copy-Blob).

Aby uzyskać szczegółowe informacje dotyczące przeprowadzania operacji REST względem stronicowe obiekty BLOB na kontach magazynu w warstwie standardowa, zobacz [interfejsu API REST usług magazynu Azure](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference).

### <a name="managed-disks"></a>Dyski zarządzane

Migawek dla dysków zarządzanych jest tylko do odczytu kopię hello dysków zarządzanych, który jest przechowywany jako standardowych dysków zarządzanych. Przyrostowe migawki nie są obecnie obsługiwane w przypadku dysków zarządzanych, ale będą obsługiwane w przyszłości hello.

Dysków zarządzanych w przypadku dołączonych tooa maszyny Wirtualnej, nie są dozwolone na dyskach hello pewnych operacji interfejsu API. Na przykład nie można wygenerować tooperform sygnatury dostępu Współdzielonego dostępu współdzielonego operacji kopiowania zablokowaniu dysku hello dołączonych tooa maszyny Wirtualnej. Zamiast tego należy najpierw Utwórz migawkę hello dysku, a następnie wykonaj kopię hello hello migawki. Alternatywnie można odłączyć dysku hello, a następnie wygeneruj operacji kopiowania hello tooperform sygnatury dostępu Współdzielonego dostępu współdzielonego.

## <a name="pricing-and-billing"></a>Cennik i rozliczenia

Za pomocą magazynu w warstwie standardowa, hello następujące zagadnienia dotyczące rozliczeń mają zastosowanie:

* Rozmiar dysków/danych niezarządzanych magazynu w warstwie standardowa 
* Dyski standardowe zarządzanych
* Migawki magazynu w warstwie standardowa
* Wychodzące transfery danych
* Transakcje

**Rozmiar magazynu danych i dysku niezarządzanych:** dysków niezarządzanych i innych danych (obiekty BLOB, tabel, kolejek i plików), są naliczane tylko w przypadku hello ilość miejsca, w przypadku korzystania z. Na przykład, jeśli masz maszyny Wirtualnej, w których stronicowych obiektów blob jest udostępniony jako 127 GB, ale hello maszyna wirtualna jest w rzeczywistości tylko przy użyciu 10 GB miejsca, opłaty będą naliczane do 10 GB miejsca. Firma Microsoft obsługuje Standard storage się too8191 GB i niezarządzane dyski standardowe się too4095 GB. 

**Dyski zarządzane:** dysków zarządzane są rozliczane według rozmiaru hello udostępnione. Obsługiwanej dysku jako dysku 10 GB, używane są tylko 5 GB możesz nadal będzie obciążana hello udostępniania rozmiaru 10 GB.

**Migawki**: migawki dyski standardowe są rozliczane hello dodatkowej pojemności używanych przez hello migawki. Aby uzyskać informacji dotyczących migawek, zobacz [tworzenia migawki obiektu Blob](/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

**Transfer danych wychodzących**: [transfery danych wychodzących](https://azure.microsoft.com/pricing/details/data-transfers/) (danych wychodzących z centrów danych Azure) powodują Naliczanie opłat za zużycie przepustowości.

**Transakcja**: $0.0036 na 100 000 transakcji dla magazynu w warstwie standardowa użytkownicy platformy Azure. Transakcje obejmują odczytu i zapisu toostorage operacji.

Aby uzyskać szczegółowe informacje o cenach dla magazynu w warstwie standardowa, maszyn wirtualnych i dysków zarządzanych Zobacz:

* [Cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/)
* [Cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Dyski zarządzane ceny](https://azure.microsoft.com/pricing/details/managed-disks)

## <a name="azure-backup-service-support"></a>Obsługa usługi Kopia zapasowa Azure 

Maszyny wirtualne z dyskami niezarządzane utworzeniem kopii zapasowej za pomocą usługi Kopia zapasowa Azure. [Więcej szczegółów](../../backup/backup-azure-vms-first-look-arm.md).

Za pomocą hello usługi Kopia zapasowa Azure i zarządzane dyski toocreate zadania tworzenia kopii zapasowej na podstawie czasu tworzenia kopii zapasowych, łatwe przywrócenie maszyny Wirtualnej i zasady przechowywania kopii zapasowych. Więcej na temat [usługi przy użyciu kopii zapasowej Azure dla maszyn wirtualnych z dyskami zarządzane](../../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="next-steps"></a>Następne kroki

* [Wprowadzenie tooAzure magazynu](../storage-introduction.md)

* [Tworzenie konta magazynu](../storage-create-storage-account.md)

* [Omówienie usługi Managed Disks](../../virtual-machines/windows/managed-disks-overview.md)

* [Tworzenie maszyny wirtualnej przy użyciu usługi Resource Manager i programu PowerShell](/azure/virtual-machines/windows/quick-create-powershell.md)

* [Utwórz Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 2.0](../../virtual-machines/windows/quick-create-cli.md)
