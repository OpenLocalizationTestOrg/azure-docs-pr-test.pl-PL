---
title: "Szyfrowanie usługi Magazyn danych magazynowanych aaaAzure | Dokumentacja firmy Microsoft"
description: "Użyj usługi magazynu obiektów Blob Azure tooencrypt funkcji szyfrowanie usługi Magazyn Azure powitania po stronie usługi hello podczas zapisywania danych hello, a podczas pobierania danych hello go odszyfrować."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: robinsh
ms.openlocfilehash: 304f1c21200f86f2084ce98788b2fc7ca893d1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-service-encryption-for-data-at-rest"></a>Szyfrowanie usługi Azure Storage dla danych magazynowanych
Azure magazynu usługi szyfrowania (SSE) dla danych magazynowanych pomaga chronić i chronić Twoje toomeet danych organizacji bezpieczeństwa i zgodności zobowiązań. Przy użyciu tej funkcji usługi Azure Storage automatycznie szyfruje toostorage wcześniejsze toopersisting Twojego danych i odszyfrowuje tooretrieval wcześniejszych. Witaj szyfrowania, odszyfrowywania i zarządzania kluczami jest całkowicie przezroczysty toousers.

Witaj poniższe sekcje zawierają szczegółowe wskazówki dotyczące sposobu toouse hello szyfrowanie usługi Magazyn funkcje, a także hello obsługiwane scenariusze i możliwości użytkowników.

## <a name="overview"></a>Omówienie
Usługa Azure Storage zapewnia rozbudowany zestaw funkcji zabezpieczeń, które razem umożliwiają deweloperom toobuild bezpiecznych aplikacji. Dane mogą być chronione przy użyciu przesyłanych między aplikacją a Azure [szyfrowania po stronie klienta](storage-client-side-encryption.md), HTTPs lub SMB 3.0. Szyfrowanie usługi Magazyn zapewnia szyfrowanie magazynowanych, obsługa szyfrowania, odszyfrowywania i zarządzania kluczami w sposób całkowicie przezroczysty. Wszystkie dane są szyfrowane przy użyciu 256-bitowego [szyfrowania AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), jednego bloku najwyższy hello szyfrów dostępne.

SSE działa hello dane są szyfrowane podczas ich zapisywania tooAzure magazynu i może służyć do magazynu obiektów Blob Azure i magazynem. Działa ona hello następujące czynności:

* Standard Storage: Kont magazynu ogólnego przeznaczenia dla obiektów blob i plików magazynu i kont magazynu obiektów Blob
* Premium Storage 
* Nadmiarowość wszystkie poziomy (LRS, ZRS, GRS i RA-GRS)
* Konta magazynu Azure Resource Manager (ale nie klasycznego) 
* Wszystkie regiony.

toolearn więcej, zobacz toohello — często zadawane pytania.

tooenable lub wyłącz szyfrowanie usługi Magazyn dla konta magazynu, zaloguj się do hello [portalu Azure](https://portal.azure.com) i wybierz konto magazynu. W bloku ustawień hello Wyszukaj hello sekcji usługi obiektów Blob, jak pokazano w tym zrzucie ekranu pokazano, a następnie kliknij przycisk szyfrowania.

![Opcja szyfrowania portalu zrzut ekranu przedstawiający](./media/storage-service-encryption/image1.png)
<br/>*Rysunek 1: Włącz SSE dla usługi obiektów Blob (krok 1.)*

![Opcja szyfrowania portalu zrzut ekranu przedstawiający](./media/storage-service-encryption/image3.png)
<br/>*Rysunek 2: Włącz SSE dla usługi plików (krok 1.)*

Po kliknięciu ustawienie szyfrowania hello, można włączyć lub wyłączyć szyfrowanie usługi magazynu.

![Właściwości szyfrowania portalu zrzut ekranu przedstawiający](./media/storage-service-encryption/image2.png)
<br/>*Rysunek 3: Włącz SSE dla obiekt Blob i plików usługi (Step2)*

## <a name="encryption-scenarios"></a>Scenariusze szyfrowania
Można włączyć szyfrowanie usługi magazynu na poziomie konta magazynu. Po włączeniu klienci wybierze które tooencrypt usług. Obsługuje ona hello następujących scenariuszy:

* Szyfrowanie magazynu obiektów Blob i magazyn plików na kontach usługi Resource Manager.
* Szyfrowanie obiektów Blob i usługa plików w klasycznych kont magazynu po migracji kont magazynu Menedżera tooResource.

SSE ma hello następujące ograniczenia:

* Szyfrowanie klasycznych kont magazynu nie jest obsługiwane.
* Istniejące dane - SSE szyfruje dane nowo utworzony po włączeniu szyfrowania hello. Jeśli na przykład można utworzyć nowe konto magazynu Resource Manager, ale nigdy nie włączaj szyfrowania, a następnie przekaż obiekty BLOB lub zarchiwizowane konta magazynu toothat wirtualne dyski twarde i Włącz SSE, te obiekty BLOB nie będą szyfrowane, chyba że są one ulegną lub kopiowane.
* Obsługa Marketplace - Włącz szyfrowanie maszyny wirtualne utworzone na podstawie hello Marketplace przy użyciu hello [portalu Azure](https://portal.azure.com), programu PowerShell i interfejsu wiersza polecenia Azure. Obraz podstawowy dysk VHD Hello pozostanie niezaszyfrowane; Jednak wszelkie zapisy wykonać po hello maszyna wirtualna ma przejścia będą szyfrowane.
* Tabeli i kolejek dane nie będą szyfrowane.

## <a name="getting-started"></a>Wprowadzenie
### <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Krok 1: [Utwórz nowe konto magazynu](storage-create-storage-account.md).
### <a name="step-2-enable-encryption"></a>Krok 2: Włączanie szyfrowania.
Można włączyć szyfrowanie przy użyciu hello [portalu Azure](https://portal.azure.com).

> [!NOTE]
> Jeśli chcesz tooprogrammatically Włącz lub wyłącz hello szyfrowanie usługi Magazyn na koncie magazynu, można użyć hello [interfejsu API REST dostawcy zasobów magazynu Azure](https://msdn.microsoft.com/library/azure/mt163683.aspx), hello [biblioteki klienta dostawcy zasobów magazynu dla platformy .NET](https://msdn.microsoft.com/library/azure/mt131037.aspx), [programu Azure PowerShell](/powershell/azureps-cmdlets-docs), lub hello [interfejsu wiersza polecenia Azure](storage-azure-cli.md).
> 
> 

### <a name="step-3-copy-data-toostorage-account"></a>Krok 3: Kopiowanie danych toostorage konta
Jeśli włączysz SSE dla hello usługa Blob, wszystkie obiekty BLOB zapisywane toothat konta magazynu będą szyfrowane. Wszystkie obiekty BLOB już znajduje się na tym koncie magazynu nie będą szyfrowane, dopóki ich napisany od nowa. Można skopiować danych hello z tooone konta magazynu jednego z SSE zaszyfrowane, lub nawet włączyć SSE i skopiuj hello obiekty BLOB z toosure tooanother jeden kontener, że poprzednie dane są zaszyfrowane. Można go użyć żadnego powitania po tooaccomplish narzędzia. To jest tekst hello takie samo zachowanie do przechowywania plików oraz.

#### <a name="using-azcopy"></a>Przy użyciu narzędzia AzCopy
AzCopy to narzędzie wiersza polecenia systemu Windows przeznaczone do kopiowania tooand danych z magazynu obiektów Blob Microsoft Azure, plików i tabeli przy użyciu prostych poleceń z optymalną wydajnością. Z obiektów blob lub plików z jednego tooanother konta magazynu, który ma włączoną SSE, można użyć tego toocopy. 

toolearn więcej, odwiedź stronę [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md).

#### <a name="using-smb"></a>Za pomocą protokołu SMB
Magazyn plików Azure oferuje udziały plików w chmurze hello przy użyciu standardowego protokołu SMB hello. Można zainstalować udział plików z klienta lokalnie lub na platformie Azure. Po zainstalowaniu, narzędzi, takich jak Robocopy może być używane toocopy plików za pośrednictwem tooAzure, który udziałów plików. Aby uzyskać więcej informacji, zobacz [jak toomount, udział plików na platformę Azure, w systemie Windows](storage-file-how-to-use-files-windows.md) i [jak udostępnić toomount plików Azure w systemie Linux](storage-how-to-use-files-linux.md).


#### <a name="using-hello-storage-client-libraries"></a>Za pomocą biblioteki klienta magazynu hello
Możesz skopiować tooand danych obiektów blob lub plik z magazynu obiektów blob lub między kontami magazynu przy użyciu naszego bogaty zestaw biblioteki klienta magazynu w tym .NET, C++, Java, Android, Node.js, PHP, Python i Ruby.

toolearn więcej, odwiedź stronę naszych [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md).

#### <a name="using-a-storage-explorer"></a>Za pomocą Eksploratora magazynu
Można używać kont magazynu toocreate Eksploratora magazynu, przekazywanie i pobieranie danych, wyświetlanie zawartości obiektów blob i przeglądanie katalogów. Można użyć jednej z tych konta magazynu tooyour obiekty BLOB tooupload z włączone szyfrowanie. Niektóre eksploratory usługi storage można także skopiować dane z istniejącego kontenera magazynu obiektów blob tooa różnych na koncie magazynu hello lub nowe konto magazynu, który ma włączoną SSE.

toolearn więcej, odwiedź stronę [eksploratory usługi Storage Azure](storage-explorers.md).

### <a name="step-4-query-hello-status-of-hello-encrypted-data"></a>Krok 4: Hello kwerenda o stan hello zaszyfrowanych danych
Zaktualizowaną wersję biblioteki klienta magazynu hello została wdrożona umożliwiająca stan hello tooquery toodetermine obiektu zaszyfrowanych lub nie. To jest obecnie dostępny tylko dla magazynu obiektów Blob. Obsługa magazynu plików znajduje się na plan hello. 

W hello międzyczasie możesz wywołać [Get właściwości konta](https://msdn.microsoft.com/library/azure/mt163553.aspx) tooverify, który hello konto magazynu ma włączone szyfrowanie lub widok hello właściwości konta magazynu w hello portalu Azure.

## <a name="encryption-and-decryption-workflow"></a>Szyfrowanie i odszyfrowywanie przepływu pracy
Poniżej przedstawiono krótki opis przepływu pracy szyfrowania i odszyfrowywania hello:

* powitania klienta włącza szyfrowanie na powitania konta magazynu.
* Gdy powitania klienta zapisuje nowe tooBlob danych (umieszczanie obiektu Blob, PUT bloku, umieść stronę itp. umieścić plik) lub magazyn plików; każdego zapisu jest szyfrowana przy użyciu 256-bitowego [szyfrowania AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), jednego bloku najwyższy hello szyfrów dostępne.
* Powitania klienta wymaga danych tooaccess (Pobierz obiekt Blob itp.), przed zwróceniem toohello użytkownika jest automatycznie odszyfrowania danych.
* Jeśli szyfrowanie jest wyłączone, nowe zapisy nie są szyfrowane i zaszyfrowane dane pozostaną zaszyfrowane, dopóki nowy tekst hello użytkownika. Gdy włączone jest szyfrowanie, zapisuje tooBlob lub magazyn plików będą szyfrowane. Stan Hello danych nie zmienia się z użytkownikiem hello przełączania się między włączenie/wyłączenie szyfrowania dla konta magazynu hello.
* Wszystkie klucze szyfrowania są przechowywane, zaszyfrowana i zarządzany przez firmę Microsoft.

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Często zadawane pytania dotyczące szyfrowanie usługi Magazyn danych w stanie spoczynku
**Pytanie: czy masz istniejące konto magazynu klasycznego. Można włączyć SSE na nim?**

Odpowiedź: nie SSE jest obsługiwana tylko na kontach magazynu Menedżera zasobów.

**Pytanie: jak szyfrować dane w moim koncie magazynu classic**

Odpowiedź: można utworzyć nowe konto magazynu Resource Manager i skopiować przy użyciu danych [AzCopy](storage-use-azcopy.md) z istniejącego konta magazynu classic tooyour nowo utworzone konto magazynu Menedżera zasobów. 

W przypadku migrowania z klasycznym magazynu tooa konta Menedżera zasobów konta magazynu, ta operacja jest natychmiastowe, zmienia hello typ konta, ale nie mają wpływ istniejących danych. Żadnych nowych danych zostanie zaszyfrowana tylko po włączeniu szyfrowania. Aby uzyskać więcej informacji, zobacz [platformy obsługiwane migracji z zasobów IaaS z klasycznym tooResource Menedżera](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/). Należy pamiętać, że jest to obsługiwane tylko dla usług obiektów Blob i pliku.

**Pytanie: czy masz istniejące konto magazynu Menedżera zasobów. Można włączyć SSE na nim?**

Odpowiedź: tak, ale tylko nowo zapisywane dane będą szyfrowane. Nie Przejdź wstecz i szyfrowania danych, który został już istnieje. To nie jest jeszcze obsługiwana dla hello podglądu pliku magazynu.

**Pytanie: Chcę tooencrypt hello bieżące dane istniejącego konta magazynu usługi Resource Manager?**

Odp.: Aby umożliwić SSE w dowolnym momencie na koncie magazynu Menedżera zasobów. Jednak dane, które były obecne nie będą szyfrowane. tooencrypt istniejących danych, można skopiować je tooanother nazwy lub innego kontenera, a następnie usuń wersje hello bez szyfrowania.

**Pytanie: czy używany Magazyn w warstwie Premium; można użyć SSE?**

A: tak SSE jest obsługiwany w standardowych magazynu i Magazyn w warstwie Premium.  Magazyn w warstwie Premium nie jest obsługiwana dla hello usługi plików.

**Pytanie: czy I Utwórz nowe konto magazynu i włączyć SSE, a następnie utwórz nową maszynę Wirtualną za pomocą tego konta magazynu, to znaczy czy Moje maszyny Wirtualnej są szyfrowane?**

Odpowiedź: tak. Żadnych dysków utworzone nowe konto magazynu hello będą szyfrowane, pod warunkiem, będą one tworzone po włączeniu SSE. Jeśli maszyna wirtualna została utworzona przy użyciu platformę handlową platformy Azure, obraz podstawowy dysk VHD hello powitalne pozostanie niezaszyfrowane; Jednak wszelkie zapisy wykonać po hello maszyna wirtualna ma przejścia będą szyfrowane.

**Pytanie: czy można utworzyć nowego konta magazynu z SSE włączyć za pomocą programu Azure PowerShell i interfejsu wiersza polecenia Azure?**

Odpowiedź: tak.

**Pytanie: jak bardziej usługi Azure Storage koszt włączenie SSE?**

Odpowiedź: nie istnieje bez dodatkowych kosztów.

**Pytanie: zarządzająca hello klucze szyfrowania?**

A: Witaj klucze są zarządzane przez firmę Microsoft.

**Pytanie: czy można użyć własnych kluczy szyfrowania?**

Odpowiedź: pracujemy nad zapewnia możliwości dla klientów toobring własne klucze szyfrowania.

**Pytanie: czy mogę Odwołaj klucze szyfrowania toohello dostępu?**

Odpowiedź: nie w tej chwili; klucze Hello pełni są zarządzane przez firmę Microsoft.

**Pytanie: jest SSE domyślnie włączona, tworząc nowe konto magazynu?**

Odpowiedź: SSE nie jest włączona domyślnie; Witaj tooenable portalu Azure można użyć go. Można również programowo włączyć tę funkcję za pomocą interfejsu API REST dostawcy zasobów magazynu hello.

**Pytanie: jak różni się od szyfrowania dysków Azure?**

Odpowiedź: Ta funkcja jest używana tooencrypt danych w magazynie obiektów Blob Azure. Witaj szyfrowania dysków Azure jest tooencrypt używanego systemu operacyjnego i dysków z danymi w maszyn wirtualnych IaaS. Aby uzyskać więcej informacji, odwiedź stronę naszych [przewodnik zabezpieczeń magazynu](storage-security-guide.md).

**Pytanie: co zrobić, jeśli I włączyć SSE, a następnie go w programie i włączyć szyfrowania dysków Azure na dyskach hello?**

A: to będzie działać bezproblemowo. Dane będą szyfrowane za pomocą obu metod.

**Pytanie: moim koncie magazynu skonfigurowano toobe replikowane geograficznie nadmiarowości. Jeżeli jest włączone SSE, nadmiarowych kopii także będą zaszyfrowane?**

A: tak, wszystkie kopie hello konta magazynu są szyfrowane, a wszystkie opcje nadmiarowości — lokalnie nadmiarowego magazynu (LRS), magazynu strefy nadmiarowy (ZRS), Magazyn geograficznie nadmiarowy (GRS) i Magazyn geograficznie nadmiarowy dostęp do odczytu (RA-GRS) — są obsługiwane.

**Pytanie: nie można włączyć szyfrowanie na moim koncie magazynu.**

A: to konto magazynu Resource Manager? Klasycznych kont magazynu nie są obsługiwane. 

**Pytanie: jest SSE dozwolone tylko w określonych regionach?**

Odpowiedź: hello SSE jest dostępna we wszystkich regionach dla magazynu obiektów Blob. Sprawdź, czy hello sekcji dostępności magazynu plików. 

**Pytanie: jak można skontaktować się z osobą czy wystąpienia jakichkolwiek problemów lub mają tooprovide opinii?**

Odpowiedź: Skontaktuj się z pomocą [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) problemów związanych z tooStorage usługi szyfrowania.

## <a name="next-steps"></a>Następne kroki
Usługa Azure Storage zapewnia rozbudowany zestaw funkcji zabezpieczeń, które razem umożliwiają deweloperom toobuild bezpiecznych aplikacji. Aby uzyskać więcej informacji, odwiedź stronę hello [przewodnik zabezpieczeń magazynu](storage-security-guide.md).

