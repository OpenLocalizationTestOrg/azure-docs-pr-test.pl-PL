---
title: toouse aaaHow magazynu Azure dla programu SQL Server kopii zapasowej i przywracania | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooback się tooAzure programu SQL Server magazynu. W tym artykule wyjaśniono korzyści hello tworzenia kopii zapasowych tooAzure baz danych SQL magazynu."
services: virtual-machines-windows
documentationcenter: 
author: MikeRayMSFT
manager: jhubbard
tags: azure-service-management
ms.assetid: 0db7667d-ef63-4e2b-bd4d-574802090f8b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: mikeray
ms.openlocfilehash: 67ebe8377be97df1312f8c1345e23576aabe0c4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-for-sql-server-backup-and-restore"></a>Użyj magazynu Azure dla programu SQL Server z kopii zapasowej i przywracania
## <a name="overview"></a>Omówienie
Począwszy od programu SQL Server 2012 z dodatkiem SP1 CU2, możesz teraz zapisać kopii zapasowych serwera SQL bezpośrednio usługi magazynu obiektów Blob platformy Azure toohello. Można użyć tej funkcji tooback się przywrócenie tooand z usługi Azure Blob hello z lokalną bazą danych serwera SQL lub bazy danych programu SQL Server w maszynie wirtualnej platformy Azure. Toocloud kopii zapasowej zapewnia korzyści dostępności, nieograniczona replikacją geograficzną poza nim magazynu i łatwość migracji tooand danych z chmury hello. Przy użyciu języka Transact-SQL lub SMO można wydać instrukcji BACKUP lub RESTORE.

SQL Server 2016 wprowadzono nowe funkcje; można użyć [kopii zapasowej migawki pliku](http://msdn.microsoft.com/library/mt169363.aspx) tooperform niemal natychmiastowe tworzenie kopii zapasowych i przywracania bardzo szybki.

W tym temacie wyjaśniono, dlaczego może wybrać toouse magazynu Azure do przechowywania kopii zapasowych SQL i zawiera opis hello składniki zaangażowane. Korzystając z zasobów hello na końcu hello hello artykułu tooaccess wskazówki i informacje dodatkowe toostart kopii zapasowych programu SQL Server przy użyciu tej usługi.

## <a name="benefits-of-using-hello-azure-blob-service-for-sql-server-backups"></a>Korzyści wynikające z użyciem hello usługi obiektów Blob platformy Azure dla kopii zapasowych serwera SQL
Istnieje kilka wyzwania, które czoła podczas wykonywania kopii zapasowych programu SQL Server. Te problemy obejmują zarządzanie magazynem, ryzyko wystąpienia awarii magazynu, dostęp do witryny toooff magazynu i konfiguracji sprzętu. Wiele z tych problemów są adresowane za pomocą usługi magazynu obiektów Blob platformy Azure hello kopii zapasowych programu SQL Server. Należy wziąć pod uwagę hello następujące korzyści:

* **Łatwość użycia**: przechowywania kopii zapasowych w obiektach blob Azure można użyć opcji poza nim tooaccess wygodne, elastyczne i łatwe. Tworzenia innej lokalizacji magazynu kopii zapasowych programu SQL Server można w prosty jako modyfikowanie istniejące skrypty/zadania toouse hello **tooURL kopii zapasowej** składni. Zwykle poza nim magazynu powinna być wystarczająco daleko od tooprevent lokalizacji bazy danych produkcyjnej hello pojedynczego po awarii, mogą mieć wpływ zarówno wcześniejsze jego hello i lokalizacje baz danych w środowisku produkcyjnym. Wybierając zbyt[obiektów blob platformy Azure replikacja geograficzna](../../../storage/common/storage-redundancy.md), masz dodatkową warstwę ochrony w przypadku powitania po awarii, które mogą wpłynąć na powitania całego regionu.
* **Kopia zapasowa archiwum**: hello usługi Magazyn obiektów Blob Azure oferuje lepszą taśmy alternatywnych toohello często używane tooarchive opcji tworzenia kopii zapasowych. Magazynu taśm może wymagać fizycznego transportu tooan poza nim, jak i środki tooprotect hello nośnika. Przechowywania kopii zapasowych w magazynie obiektów Blob Azure udostępnia moment, wysokiej dostępności i niezawodny archiwizacji opcji.
* **Zarządzane sprzętu**: się nie dodatkowe zarządzania sprzętem z usługami Azure. Usług Azure Zarządzanie sprzętem hello i podaj — replikacja geograficzna nadmiarowości i ochronę przed awariami sprzętu.
* **Nieograniczony magazyn**: przez włączenie blob bezpośredniego tooAzure kopii zapasowej, masz toovirtually dostęp nieograniczony magazyn. Można również tworzenie kopii zapasowej dysku maszyny wirtualnej platformy Azure tooan ma ograniczenia na podstawie rozmiaru maszyny. Brak Ogranicz liczbę toohello dysków można dołączyć tooan maszyny wirtualnej platformy Azure do przechowywania kopii zapasowych. Ten limit jest 16 dysków dla bardzo dużych wystąpienia i mniej wystąpień mniejsze.
* **Wykonaj kopię zapasową dostępności**: kopie zapasowe przechowywane w obiektach blob Azure są dostępne z dowolnego miejsca i w dowolnym momencie i mogą być łatwo dostępne dla tooeither przywraca lokalnego programu SQL Server lub innego serwera SQL działającego w maszynie wirtualnej platformy Azure, bez muszą hello dołączania/odłączania bazy danych lub pobierania i dołączanie hello wirtualnego dysku twardego.
* **Koszt**: płać tylko za hello usługa, która jest używana. Może być ekonomicznego jako opcja archiwum poza nim i tworzenia kopii zapasowej. Zobacz hello [Kalkulator cen platformy Azure](http://go.microsoft.com/fwlink/?LinkId=277060 "Kalkulator cen")i hello [cennik usługi Azure artykułu](http://go.microsoft.com/fwlink/?LinkId=277059 "artykułu cennik") więcej informacje.
* **Magazyn migawek**: Jeśli pliki bazy danych są przechowywane w obiekcie blob Azure i korzystasz z programu SQL Server 2016, możesz użyć [kopii zapasowej migawki pliku](http://msdn.microsoft.com/library/mt169363.aspx) tooperform niemal natychmiastowe tworzenie kopii zapasowych i przywracania bardzo szybki.

Aby uzyskać więcej informacji, zobacz [programu SQL Server z kopii zapasowej i przywracania usługi magazynu obiektów Blob Azure](http://go.microsoft.com/fwlink/?LinkId=271617).

następujące dwie sekcje Hello wprowadzenie hello Azure Blob magazynu usługi, w tym hello wymagane składniki programu SQL Server. Jest ważne toounderstand hello składników i ich interakcji toosuccessfully użycia i przywracania kopii zapasowej z usługi Magazyn obiektów Blob platformy Azure hello.

## <a name="azure-blob-storage-service-components"></a>Składniki usługi magazynu obiektów Blob platformy Azure
Witaj następujące składniki platformy Azure są używane podczas wykonywania kopii zapasowej toohello usługi magazynu obiektów Blob platformy Azure.

| Składnik | Opis |
| --- | --- |
| **Konto magazynu** |Konto magazynu Hello jest hello punkt początkowy dla wszystkich usług magazynu. tooaccess usługi Magazyn obiektów Blob Azure, najpierw utworzyć konto usługi Azure Storage. Aby uzyskać więcej informacji na temat usługi Magazyn obiektów Blob platformy Azure, zobacz [jak toouse hello usługi magazynu obiektów Blob Azure](https://azure.microsoft.com/develop/net/how-to-guides/blob-storage/) |
| **Kontener** |Kontener zawiera grupowanie zestawu obiektów blob i przechowywać nieograniczoną liczbę obiektów blob. toowrite programu SQL Server tooan kopii zapasowej usługi obiektów Blob platformy Azure, użytkownik musi mieć co najmniej hello nadrzędny kontener utworzony. |
| **Obiekt blob** |Typ i rozmiar pliku. Obiekty BLOB mają hello następującego formatu adresu URL: **https://[storage account].blob.core.windows.net/[container]/[blob]**. Aby uzyskać więcej informacji na temat stronicowe obiekty BLOB, zobacz [opis blokowych i stronicowych obiektów blob](http://msdn.microsoft.com/library/azure/ee691964.aspx) |

## <a name="sql-server-components"></a>Składniki programu SQL Server
Witaj następujące składniki programu SQL Server są używane podczas wykonywania kopii zapasowej toohello usługi magazynu obiektów Blob platformy Azure.

| Składnik | Opis |
| --- | --- |
| **ADRES URL** |Adres URL określa identyfikator URI (Uniform Resource) tooa unikatowy plik kopii zapasowej. adres URL Hello jest używany tooprovide hello lokalizację i nazwę pliku kopii zapasowej programu SQL Server hello. Witaj adres URL musi wskazywać tooan rzeczywistego obiektu blob nie tylko kontenerem. Jeśli hello obiektu blob nie istnieje, jest tworzony. Jeśli istniejący obiekt blob jest określony, kopii zapasowej nie powiedzie się, chyba że hello > określono opcję klauzuli WITH FORMAT. Witaj poniżej przedstawiono przykład hello adresu URL należy określić w hello polecenia BACKUP: **http[s]://[storageaccount].blob.core.windows.net/[container]/[FILENAME.bak]**. HTTPS jest zalecane, ale nie jest wymagane. |
| **Poświadczenia** |informacje Hello jest wymagana tooconnect i uwierzytelniania tooAzure usługi magazynu obiektów Blob są przechowywane jako poświadczenie.  Aby dla programu SQL Server toowrite kopii zapasowych tooan obiektów Blob platformy Azure lub Przywróć z niej można utworzyć poświadczeń programu SQL Server. Aby uzyskać więcej informacji, zobacz [poświadczenia serwera SQL](https://msdn.microsoft.com/library/ms189522.aspx). |

> [!NOTE]
> Jeśli wybierz toocopy i przekazać plik kopii zapasowej toohello usługi magazynu obiektów Blob platformy Azure, musi używać typu obiektu blob strony jako opcji magazynu, sieci, jeśli planujesz toouse tego pliku dla operacji przywracania. PRZYWRÓCENIE z typem danych blob bloku zakończy się niepowodzeniem z powodu błędu.
> 
> 

## <a name="next-steps"></a>Następne kroki
1. Utwórz konto platformy Azure, jeśli nie został wcześniej. Jeśli dokonujesz oceny usługi Azure, należy wziąć pod uwagę hello [bezpłatnej wersji próbnej](https://azure.microsoft.com/free/).
2. Następnie przejdź za pomocą jednego z hello następujące samouczki, które opisano tworzenie konta magazynu i operacji przywracania.
   
   * **SQL Server 2014**: [samouczek: SQL Server 2014 w kopii zapasowej i przywracania tooMicrosoft usługi magazynu obiektów Blob Azure](https://msdn.microsoft.com/library/jj720558\(v=sql.120\).aspx).
   * **SQL Server 2016**: [samouczek: przy użyciu usługi magazynu obiektów Blob platformy Azure Microsoft hello z bazami danych programu SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx)
3. Przejrzyj, począwszy od dodatkowej dokumentacji [programu SQL Server z kopii zapasowej i przywracania usługi magazynu obiektów Blob platformy Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

Jeśli masz problemy, przejrzyj temat hello [kopii zapasowej programu SQL Server tooURL najlepsze rozwiązania i rozwiązywanie problemów](https://msdn.microsoft.com/library/jj919149.aspx).

Dla innego serwera SQL z kopii zapasowej i przywracanie opcji, zobacz [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

