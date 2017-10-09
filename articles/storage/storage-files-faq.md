---
title: "aaaFrequently zadawane pytania dotyczące usługi Magazyn plików Azure | Dokumentacja firmy Microsoft"
description: "Znajdź odpowiedzi toofrequently zadawane pytania dotyczące usługi Magazyn plików Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: ecd685b3094f51e998bbf5dd0567a20732757015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>Często zadawane pytania dotyczące usługi Magazyn plików Azure

## <a name="general"></a>Ogólne
* **Q. Co to jest magazyn plików Azure?**  
   
    Magazyn plików Azure to Rozproszony system plików na platformie Azure. Zapewnia interfejs protokołu SMB, dzięki czemu użytkownicy toomount hello magazynu jako udział natywnego na obsługiwanej maszynie wirtualnej platformy Azure lub komputera lokalnego.

* **Q. Magazyn plików Azure jest przydatne**  
   
    Magazyn plików Azure zapewnia dostęp do udostępnionych danych w wielu maszyn wirtualnych i platform. Odwołuje się zbyt[przydaje się dlaczego Azure File storage](storage-files-introduction.md#why-azure-file-storage-is-useful).

* **Q. Kiedy używać plików Azure vs vs obiektów Blob platformy Azure dysku Azure?**  
   
    Microsoft Azure oferuje kilka możliwości toostore i dostępu do danych w chmurze hello.  
   
    Magazyn plików Azure — udostępnia interfejs SMB, bibliotek klienckich i interfejs REST, który umożliwia łatwy dostęp z dowolnego miejsca plikami toostored.  
   
    Azure obiektów blob — zawiera biblioteki klienta i interfejsu REST, który umożliwia toobe danych niestrukturalnych przechowywane i dostępne w bardzo dużej skali w blokowych obiektów blob.  
   
    Danych Azure dyski — zawiera biblioteki klienta i interfejsu REST, który umożliwia toobe danych trwale przechowywane i dostępne z dołączonego wirtualnego dysku twardego.  
   
    Dowiedz się więcej na [Deciding podczas obiektów blob Azure toouse, pliki Azure lub dyski danych Azure](storage-decide-blobs-files-disks.md)

* **Q. Jak rozpocząć pracę przy użyciu usługi Magazyn plików Azure?**  
   
    Można uruchomić tworzenia udziału plików na platformę Azure. Można utworzyć udziały plików platformy Azure przy użyciu portalu Azure, poleceń cmdlet programu PowerShell magazynu Azure hello, biblioteki klienta magazynu Azure hello lub hello interfejsu API REST magazynu Azure. Z tego samouczka dowiesz się:

    * [Dowiedz się, jak udostępnić toocreate plików platformy Azure przy użyciu hello portalu](storage-file-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [Dowiedz się, jak udostępnić toocreate plików platformy Azure przy użyciu programu Powershell](storage-file-how-to-create-file-share.md#create-file-share-through-powershell)
    * [Dowiedz się, jak udostępnić toocreate plików platformy Azure przy użyciu interfejsu wiersza polecenia](storage-file-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **Q. Jakie replikacji są obsługiwane przez Magazyn plików Azure?**  
   
    Magazyn plików Azure obsługuje tylko LRS lub GRS od razu. Planujemy toosupport RA-GRS, ale nie jeszcze żadnych tooshare osi czasu.

## <a name="security-authentication-and-access-control"></a>Zabezpieczenia, uwierzytelniania i kontroli dostępu

* **Q. Jakie są różne sposoby tooaccess plików w usłudze magazyn plików Azure?**
    
    Udział plików hello można zainstalować na komputerze lokalnym przy użyciu protokołu SMB 3.0 lub użyj narzędzi, takich jak [Eksploratora usługi Storage](http://storageexplorer.com/) tooaccess plików w udziale plików. Z aplikacji można użyć bibliotek klienckich magazynu, interfejsy API REST lub tooaccess programu Powershell, który udziału plików w pliku Azure.

* **Q. Jak zapewniają dostęp tooa określonego pliku w przeglądarce sieci web**
    
    Za pomocą sygnatury dostępu Współdzielonego, można wygenerować tokeny z określonymi uprawnieniami, które są ważne przez ustalony czas. Na przykład można wygenerować tokenu z określonego pliku tooa dostęp tylko do odczytu w określonym okresie czasu. Każdego, kto ma ten adres url można uzyskać dostępu do hello pliku bezpośrednio z dowolnej przeglądarki sieci web jest nieprawidłowy. Klucze sygnatur dostępu współdzielonego można łatwo generować z interfejsu użytkownika, na przykład Eksploratora magazynu.

* **Q. Jest to możliwe toospecify uprawnienia tylko do odczytu lub w trybie tylko do zapisu w folderach w ramach udziału hello?**
    
    W przypadku instalowania hello udziału plików za pośrednictwem protokołu SMB nie masz ten poziom kontroli nad uprawnieniami. Jednak można to osiągnąć, tworząc sygnaturę dostępu współdzielonego (SAS) za pośrednictwem hello interfejsu API REST lub bibliotek klienckich.  

* **Q. Jak można włączyć szyfrowanie po stronie serwera dla usługi Magazyn plików Azure?**

    [Szyfrowanie po stronie serwera](storage-service-encryption.md) Azure pliku magazynu jest ogólnie dostępna we wszystkich regionach i chmur publicznych i national. Można włączyć SSE magazynu plików Azure za pomocą [portalu Azure](https://portal.azure.com/),[interfejsu API dostawcy zasobów magazynu usługi Microsoft Azure](/rest/api/storagerp/storageaccounts), [programu Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) lub [wiersza polecenia platformy Azure ](storage-azure-cli.md).
    
    Po włączeniu SSE na magazyn plików Azure żadnych nowych danych toohello magazyn plików na tym koncie magazynu zostanie automatycznie zaszyfrowane. Ta funkcja jest dostępna dla wszystkich nowych danych tooexisting lub nowe udziały istniejącego lub nowego konta magazynu. Włączenie tej funkcji nie wiąże się z żadną dodatkową opłatą. Dowiedz się więcej na [jak tooenable SSE na magazyn plików Azure](storage-service-encryption.md).

* **Q. Uwierzytelnianie oparte na usłudze Active Directory jest obsługiwana przez Magazyn plików Azure?**
   
    Obecnie nie zapewniamy obsługi uwierzytelniania w usłudze AD dla list kontroli dostępu, ale planujemy dodanie tej funkcji w przyszłości. Teraz klucze konta magazynu Azure hello są udziału plików toohello uwierzytelniania tooprovide używane. Firma Microsoft oferuje za pomocą sygnatur dostępu współdzielonego (SAS) za pomocą biblioteki klienta interfejsu API REST lub hello hello obejście tego problemu. Za pomocą sygnatury dostępu Współdzielonego, można wygenerować tokeny z określonymi uprawnieniami, które są ważne przez ustalony czas. Można na przykład wygenerować token z tooa dostęp tylko do odczytu pliku o upływie 10 minut. Każdy, kto posiada token, gdy jest on prawidłowy ma dostęp tylko do odczytu pliku toothat dla tych 10 minut.
   
    Sygnatury dostępu Współdzielonego jest obsługiwana tylko za pośrednictwem hello interfejsu API REST lub bibliotek klienckich. W przypadku zainstalowania udziału plików hello za pośrednictwem hello protokołu SMB, nie można użyć SAS toodelegate dostępu tooits zawartość. 
    
* **Q. Co to są zasady zgodności danych hello obsługiwane przez Magazyn plików Azure?**

   Magazyn plików Azure działa na hello architektura tego samego magazynu, zgodnie z innych magazynów usługi w usłudze Azure Storage i stosuje hello tych samych danych zasad zgodności. Więcej informacji na temat usługi Azure Storage danych zgodności, możesz pobrać i odwoływać się za[dokumentu ochrony danych Microsoft Azure](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).

## <a name="on-premises-access"></a>Dostęp do lokalnego

* **Q.Do mam toouse Azure ExpressRoute tooconnect tooAzure magazyn plików z lokalnej maszyny Wirtualnej?**
   
    Nie. Jeśli nie masz usługi ExpressRoute, nadal dostępne hello udziału plików z lokalnymi tak długo, jak długo ma port 445 (ruch wychodzący TCP) otwórz dostęp do Internetu. Jednak służy usługi ExpressRoute z usługą Magazyn plików Azure Jeśli chcesz.

* **Q. Sposób instalacji udziału plików platformy Azure na komputerze lokalnym** 
    
    Można zainstalować udział plików hello za pośrednictwem protokołu SMB hello tak długo, jak jest otwarty port 445 (ruch wychodzący TCP) i klient obsługuje protokół SMB 3.0 hello (na przykład używasz systemu Windows 10 lub Windows Server 2012). Należy skontaktować się z lokalnego usługodawcy internetowego dostawcy toounblock hello portu. W hello tymczasowe, można wyświetlić plików za pomocą [Eksploratora usługi Storage](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).


## <a name="billing-and-pricing"></a>Rozliczeniach i cenach
* **Q. Hello ruchu sieciowego między maszyny Wirtualnej platformy Azure a udziałem plików jest liczony jako zewnętrzne użycie przepustowości i rozliczany toohello subskrypcji?**
   
    Jeśli udział plików hello i maszyny Wirtualnej znajdują się w hello tego samego regionu Azure, hello zwolnieniu ruch między nimi. Jeśli są w różnych regionach, ruch hello między nimi będzie obciążana jako zewnętrzne użycie przepustowości.

## <a name="backup"></a>Tworzenie kopii zapasowych

* **Q. Jak utworzyć kopię zapasową mojej udział plików Azure**
    
    Można użyć narzędzia AzCopy, RoboCopy, lub 3rd strony narzędzia kopii zapasowych, który można utworzyć kopię zapasową udziału zainstalowanego pliku. Oczekujemy toohave hello możliwości tootake migawki udziałów plików w hello niemal przyszłości; będziesz w stanie toouse udziału pliku Azure toobackup tej funkcji.

## <a name="performance"></a>Wydajność

* **Q. Jakie są limity skalowania hello magazynu plików Azure?**
    Aby uzyskać informacje na obiekty docelowe skalowalności i wydajności usługi Magazyn plików Azure, zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).

* **Q. Moje wydajności przebiegało powoli, podczas próby toounzip plików do usługi Magazyn plików Azure. Co zrobić?**
    
    tootransfer dużą liczbę plików do usługi Magazyn plików Azure, zalecane jest użycie narzędzia AzCopy (z systemem Windows, Linux/Unix w wersji zapoznawczej) lub Azure Powershell jak te narzędzia są zoptymalizowane pod kątem transferu sieciowego.

* **Q. Poprawki, co zostało zwolnione toofix zmniejszyć wydajność problem z usługą Magazyn plików Azure?**
    
    zespół Windows Hello wydał ostatnio toofix poprawkę rozwiązującą problem z wydajnością, gdy powitania klienta uzyskuje dostęp do usługi Magazyn plików Azure z Windows 8.1 lub Windows Server 2012 R2. Należy uzyskać więcej informacji, wyewidencjonowanie hello skojarzonego artykułu KB [powolne działanie, gdy uzyskujesz dostęp do usługi Magazyn plików Azure z Windows 8.1 lub Server 2012 R2](https://support.microsoft.com/kb/3114025).

## <a name="features-and-interoperability-with-other-services"></a>Funkcje i współdziałanie z innymi usługami
* **Q. To jest "Monitora udziału plików" dla klastra trybu failover z jednym hello zastosowań usługi Magazyn plików Azure?**
   
    To nie jest obecnie obsługiwane.

* **Q. Jest to operacja zmiany nazwy w hello interfejsu API REST?**
   
    Nie w tej chwili.

* **Q. Czy można zagnieżdżać udziały, innymi słowy, udział w udziale?**
    
    Nie. udział plików Hello jest hello sterownik wirtualny, który można zainstalować, dlatego zagnieżdżanie nie są obsługiwane.

* **Q. Przy użyciu usługi Magazyn plików Azure z programem IBM MQ**
    
    Firma IBM wydała dokument tooguide IBM MQ klienci podczas konfigurowania usługi Magazyn plików Azure z usługi. Aby uzyskać więcej informacji, zapoznaj się [jak toosetup IBM MQ Multi instance menedżera kolejek z usługi Microsoft Azure pliku](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).


## <a name="troubleshooting"></a>Rozwiązywanie problemów
* **Q. Jak naprawiać błędy magazyn plików Azure?**
    
    Można odwoływać się za[magazyn plików Azure Rozwiązywanie problemów z artykułu](storage-troubleshoot-file-connection-problems.md) end-to-end wskazówki dotyczące rozwiązywania problemów. 


## <a name="see-also"></a>Zobacz też
Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.

### <a name="conceptual-articles-and-videos"></a>Artykuły koncepcyjne i filmy
* [Azure File Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Azure File Storage: płynnie działający system plików SMB w chmurze dla systemów Windows i Linux)
* [Jak toouse magazyn plików Azure z systemem Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Narzędzia dostępne dla usługi Magazyn plików
* [Używanie programu Azure PowerShell z usługą Azure Storage](storage-powershell-guide-full.md)
* [Jak toouse AzCopy z usługi Magazyn Microsoft Azure](storage-use-azcopy.md)
* [Przy użyciu hello wiersza polecenia platformy Azure z usługą Azure Storage](storage-azure-cli.md)
* [Rozwiązywanie problemów z usługą Azure File Storage](storage-troubleshoot-file-connection-problems.md)

### <a name="blog-posts"></a>Wpisy na blogach
* [Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/) (Usługa Azure File Storage została udostępniona publicznie)
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Za kulisami usługi Azure File Storage)
* [Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx) (Wprowadzenie do usługi plików platformy Microsoft Azure)
* [Migrowanie danych tooAzure magazyn plików](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Dokumentacja
* [Dokumentacja biblioteki klienta usługi Storage dla programu .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Dokumentacja interfejsu API REST usługi plików](http://msdn.microsoft.com/library/azure/dn167006.aspx)
