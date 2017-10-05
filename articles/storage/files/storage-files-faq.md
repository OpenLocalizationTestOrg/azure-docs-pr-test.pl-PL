---
title: "Często zadawane pytania dotyczące usługi Magazyn plików Azure | Dokumentacja firmy Microsoft"
description: "Odpowiedzi na często zadawane pytania dotyczące usługi Magazyn plików Azure."
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
ms.openlocfilehash: 17868591e1056ff2bddde0e082695af529f58f02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>Często zadawane pytania dotyczące usługi Magazyn plików Azure

## <a name="general"></a>Ogólne
* **Q. Co to jest magazyn plików Azure?**  
   
    Magazyn plików Azure to Rozproszony system plików na platformie Azure. Zapewnia interfejs protokołu SMB, co umożliwi użytkownikom można zainstalować magazyn jako udział natywnego na obsługiwanej maszynie wirtualnej platformy Azure lub komputera lokalnego.

* **Q. Magazyn plików Azure jest przydatne**  
   
    Magazyn plików Azure zapewnia dostęp do udostępnionych danych w wielu maszyn wirtualnych i platform. Zapoznaj się [przydaje się dlaczego Azure File storage](storage-files-introduction.md#why-azure-file-storage-is-useful).

* **Q. Kiedy używać plików Azure vs vs obiektów Blob platformy Azure dysku Azure?**  
   
    Microsoft Azure oferuje kilka metod do przechowywania i uzyskać dostęp do danych w chmurze.  
   
    Magazyn plików Azure — udostępnia interfejs SMB, bibliotek klienckich i interfejsu REST, który umożliwia łatwe dostęp z dowolnego miejsca do przechowywanych plików.  
   
    Azure obiektów blob — zawiera biblioteki klienta i interfejsu REST, który umożliwia danych bez struktury przechowywanych i dostępne w bardzo dużej skali w blokowych obiektów blob.  
   
    Danych Azure dyski — zawiera biblioteki klienta i interfejsu REST, który umożliwia danych trwale przechowywane i uzyskać dostęp z dołączonego wirtualnego dysku twardego.  
   
    Dowiedz się więcej na [decydowania, kiedy używać obiektów blob Azure, Azure pliki i dyski danych Azure](../common/storage-decide-blobs-files-disks.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)

* **Q. Jak rozpocząć pracę przy użyciu usługi Magazyn plików Azure?**  
   
    Można uruchomić tworzenia udziału plików na platformę Azure. Można utworzyć udziały plików platformy Azure przy użyciu portalu Azure, poleceń cmdlet programu PowerShell magazynu Azure, biblioteki klienta magazynu Azure lub interfejsu API REST magazynu Azure. Z tego samouczka dowiesz się:

    * [Dowiedz się, jak utworzyć udział plików Azure przy użyciu portalu](storage-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [Dowiedz się, jak utworzyć udział plików Azure przy użyciu programu Powershell](storage-how-to-create-file-share.md#create-file-share-through-powershell)
    * [Dowiedz się, jak utworzyć udział plików Azure przy użyciu interfejsu wiersza polecenia](storage-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **Q. Jakie replikacji są obsługiwane przez Magazyn plików Azure?**  
   
    Magazyn plików Azure obsługuje tylko LRS lub GRS od razu. Planujemy dodanie obsługi modelu RA-GRS, ale jeszcze nie wiemy, kiedy to nastąpi.

## <a name="security-authentication-and-access-control"></a>Zabezpieczenia, uwierzytelniania i kontroli dostępu

* **Q. Jakie są różne sposoby na dostęp do plików w usłudze magazyn plików Azure?**
    
    Udziałów plików na komputerze lokalnym przy użyciu protokołu SMB 3.0 lub użyj narzędzi, takich jak [Eksploratora usługi Storage](http://storageexplorer.com/) na dostęp do plików w udziale plików. Z aplikacji można użyć bibliotek klienckich magazynowania, interfejsów API REST lub programu Powershell, aby uzyskać dostęp do plików w udziale plików Azure.

* **Q. Jak zapewniają dostęp do określonego pliku w przeglądarce sieci web**
    
    Za pomocą sygnatury dostępu Współdzielonego, można wygenerować tokeny z określonymi uprawnieniami, które są ważne przez ustalony czas. Na przykład można wygenerować token z dostępem tylko do odczytu do konkretnego pliku przez określony czas. Każdy, kto posiada ten adres url dostępu do pliku bezpośrednio z dowolnej przeglądarki sieci web, gdy jest on nieprawidłowy. Klucze sygnatur dostępu współdzielonego można łatwo generować z interfejsu użytkownika, na przykład Eksploratora magazynu.

* **Q. Jest to, można określić tylko do odczytu lub uprawnienia tylko do zapisu w folderach w ramach udziału?**
    
    W przypadku udziałów plików instalowanych za pomocą protokołu SMB nie masz takiej kontroli nad uprawnieniami. Jednak możesz to zrobić, tworząc sygnaturę dostępu współdzielonego za pośrednictwem interfejsu API REST lub bibliotek klienckich.  

* **Q. Jak można włączyć szyfrowanie po stronie serwera dla usługi Magazyn plików Azure?**

    [Szyfrowanie po stronie serwera](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) Azure pliku magazynu jest ogólnie dostępna we wszystkich regionach i chmur publicznych i national. Można włączyć SSE magazynu plików Azure za pomocą [portalu Azure](https://portal.azure.com/),[interfejsu API dostawcy zasobów magazynu usługi Microsoft Azure](/rest/api/storagerp/storageaccounts), [programu Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) lub [wiersza polecenia platformy Azure ](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).
    
    Po włączeniu SSE na magazyn plików Azure żadnych nowych danych do przechowywania plików na tym koncie magazynu zostanie automatycznie zaszyfrowane. Funkcja ta jest dostępna dla wszystkich nowych danych zapisywanych w istniejących lub nowych udziałach na istniejącym lub nowym koncie magazynu. Włączenie tej funkcji nie wiąże się z żadną dodatkową opłatą. Dowiedz się więcej na [jak SSE, Włącz magazyn plików Azure](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

* **Q. Uwierzytelnianie oparte na usłudze Active Directory jest obsługiwana przez Magazyn plików Azure?**
   
    Obecnie nie zapewniamy obsługi uwierzytelniania w usłudze AD dla list kontroli dostępu, ale planujemy dodanie tej funkcji w przyszłości. Tymczasem do uwierzytelniania w udziale plików używane są klucze kont usługi Azure Storage. Ponadto dostępne jest obejście w formie sygnatur dostępu współdzielonego, których można używać za pośrednictwem interfejsu API REST lub bibliotek klienckich. Za pomocą sygnatury dostępu Współdzielonego, można wygenerować tokeny z określonymi uprawnieniami, które są ważne przez ustalony czas. Można na przykład wygenerować token z dostępem tylko do odczytu do danego pliku o upływie 10 minut. Każdy, kto posiada token, gdy jest on prawidłowy ma dostęp tylko do odczytu do tego pliku dla tych 10 minut.
   
    Sygnatury dostępu współdzielonego są obsługiwane wyłącznie za pośrednictwem interfejsu API REST lub bibliotek klienckich. Jeśli udziałów plików za pomocą protokołu SMB, nie mogą delegować dostęp do zawartości za pomocą sygnatury dostępu Współdzielonego. 
    
* **Q. Co to są zasady zgodności danych obsługiwane przez Magazyn plików Azure?**

   Magazyn plików Azure działa w oparciu o takiej samej architekturze magazynu jako inne usługi magazynu w usłudze Azure Storage i stosuje się te same zasady zgodności danych. Więcej informacji na temat usługi Azure Storage danych zgodności, możesz pobrać i odwoływać się do [dokumentu ochrony danych Microsoft Azure](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).

## <a name="on-premises-access"></a>Dostęp do lokalnego

* **Q.Do użycie do połączenia z magazynem plików Azure z lokalnej maszyny Wirtualnej Azure ExpressRoute?**
   
    Nie. Nawet jeśli nie masz usługi ExpressRoute, możesz uzyskiwać dostęp do udziału plików z zasobów lokalnych, o ile masz otwarty port 445 (ruch wychodzący TCP) dla połączeń internetowych. Jednak służy usługi ExpressRoute z usługą Magazyn plików Azure Jeśli chcesz.

* **Q. Sposób instalacji udziału plików platformy Azure na komputerze lokalnym** 
    
    W przypadku zainstalowania udziału plików przy użyciu protokołu SMB, tak długo, jak jest otwarty port 445 (ruch wychodzący TCP) i klient obsługuje protokół SMB 3.0 (na przykład używasz systemu Windows 10 lub Windows Server 2012). Poproś swojego usługodawcę internetowego o odblokowanie portu. W międzyczasie, można wyświetlić plików za pomocą [Eksploratora usługi Storage](../../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).


## <a name="billing-and-pricing"></a>Rozliczeniach i cenach
* **Q. Czy ruch sieciowy między maszyny Wirtualnej platformy Azure a udziałem plików jest liczony jako zewnętrzne użycie przepustowości i rozliczany subskrypcji?**
   
    Jeśli udział plików i maszyna wirtualna znajdują się w tym samym regionie Azure, ruch między nimi jest bezpłatna. Jeśli są w różnych regionach, ruch między nimi będzie rozliczany jako zewnętrzne użycie przepustowości.

## <a name="backup"></a>Tworzenie kopii zapasowych

* **Q. Jak utworzyć kopię zapasową mojej udział plików Azure**
    
    Można użyć narzędzia AzCopy, RoboCopy, lub 3rd strony narzędzia kopii zapasowych, który można utworzyć kopię zapasową udziału zainstalowanego pliku. Oczekuje się mieć możliwość migawek udziałów plików w niedalekiej przyszłości. będzie można użyć tej funkcji do kopii zapasowej z udziału plików platformy Azure.

## <a name="performance"></a>Wydajność

* **Q. Jakie są limity skalowania magazynu plików Azure?**
    Aby uzyskać informacje na obiekty docelowe skalowalności i wydajności usługi Magazyn plików Azure, zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#scalability-targets-for-blobs-queues-tables-and-files).

* **Q. Moje wydajności przebiegało powoli, rozpakowywanie plików do usługi Magazyn plików Azure. Co zrobić?**
    
    Aby przetransferować dużą liczbę plików do usługi Magazyn plików Azure, zalecane jest użycie narzędzia AzCopy (z systemem Windows, Linux/Unix w wersji zapoznawczej) lub Azure Powershell jak te narzędzia są zoptymalizowane pod kątem transferu sieciowego.

* **Q. Co poprawek została wydana Aby rozwiązać problem z wydajnością powolna z usługi Magazyn plików Azure?**
    
    Zespół systemu Windows wydał ostatnio poprawkę rozwiązującą problem z wydajnością, gdy klient uzyskuje dostęp do usługi Magazyn plików Azure z Windows 8.1 lub Windows Server 2012 R2. Aby uzyskać więcej informacji, zapoznaj się z odpowiednim artykułem KB [powolne działanie, gdy uzyskujesz dostęp do usługi Magazyn plików Azure z Windows 8.1 lub Server 2012 R2](https://support.microsoft.com/kb/3114025).

## <a name="features-and-interoperability-with-other-services"></a>Funkcje i współdziałanie z innymi usługami
* **Q. To jest "Monitora udziału plików" dla klastra trybu failover, jeden z przypadków użycia usługi Azure File Storage?**
   
    To nie jest obecnie obsługiwane.

* **Q. Jest to operacja zmiany nazwy w interfejsie API REST?**
   
    Nie w tej chwili.

* **Q. Czy można zagnieżdżać udziały, innymi słowy, udział w udziale?**
    
    Nie. Udział plików to sterownik wirtualny z możliwością instalacji, dlatego zagnieżdżanie nie jest obsługiwane.

* **Q. Przy użyciu usługi Magazyn plików Azure z programem IBM MQ**
    
    Firma IBM wydała dokument oprogramowania IBM mq podczas konfigurowania usługi Magazyn plików Azure z usługi. Aby uzyskać więcej informacji, zobacz: [How to setup IBM MQ Multi instance queue manager with Microsoft Azure File Service](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service) (Jak skonfigurować menedżera kolejki z wieloma wystąpieniami programu IBM MQ do działania z usługą Magazyn plików Azure).


## <a name="troubleshooting"></a>Rozwiązywanie problemów
* **Q. Jak naprawiać błędy magazyn plików Azure?**
    
    Można to sprawdzić [magazyn plików Azure artykułu Rozwiązywanie problemów](storage-troubleshoot-windows-file-connection-problems.md) end-to-end wskazówki dotyczące rozwiązywania problemów. 


## <a name="see-also"></a>Zobacz też
Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.

### <a name="conceptual-articles-and-videos"></a>Artykuły koncepcyjne i filmy
* [Azure File Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Azure File Storage: płynnie działający system plików SMB w chmurze dla systemów Windows i Linux)
* [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md) (Jak używać usługi Azure File Storage z systemem Linux)

### <a name="tooling-support-for-file-storage"></a>Narzędzia dostępne dla usługi Magazyn plików
* [How to use AzCopy with Microsoft Azure Storage](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) (Jak używać narzędzia AzCopy z usługą Microsoft Azure Storage)
* [Używanie interfejsu wiersza polecenia platformy Azure z usługą Azure Storage](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Rozwiązywanie problemów z usługą Azure File Storage](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a>Wpisy na blogach
* [Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/) (Usługa Azure File Storage została udostępniona publicznie)
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Za kulisami usługi Azure File Storage)
* [Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx) (Wprowadzenie do usługi plików platformy Microsoft Azure)
* [Migrowanie danych do usługi Magazyn plików Azure](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Dokumentacja
* [Dokumentacja biblioteki klienta usługi Storage dla programu .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Dokumentacja interfejsu API REST usługi plików](http://msdn.microsoft.com/library/azure/dn167006.aspx)
