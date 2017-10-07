---
title: aaaIntro tooMicrosoft Azure | Dokumentacja firmy Microsoft
description: "Nowe tooMicrosoft Azure? Ogólne omówienie hello Get oferowanych przez niego usług z przykładami jak są przydatne."
services: " "
documentationcenter: .net
author: rboucher
manager: carolz
editor: 
ms.assetid: 6f47f711-2208-4c21-8c1d-826a54c05c29
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2015
ms.author: robb
ms.openlocfilehash: 6791506abe813e19ca7b04d78d35cb46352a9028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-microsoft-azure"></a>Wprowadzenie do platformy Microsoft Azure
Microsoft Azure to platforma aplikacji firmy Microsoft hello chmury publicznej.  Hello celem tego artykułu jest toogive możesz podstawę do zrozumienia podstaw hello Azure, nawet jeśli nie wiesz nic o chmury obliczeniowej.

**Jak tooread w tym artykule**

Azure rośnie cały czas hello, dlatego jest łatwe tooget przeciążony.  Rozpoczynać hello podstawowe usługi, które są najpierw wymienione w tym artykule, a następnie przejdź na tooadditional usług. Nie oznacza to po prostu hello dodatkowe usługi nie można użyć samodzielnie, ale podstawowe usługi hello tworzą core hello aplikacji działających na platformie Azure.

**Przesyłanie opinii**

Twoja opinia jest ważne. W tym artykule powinien zapewnić skuteczne Omówienie usługi Azure. Jeśli nie, poinformuj nas w sekcji komentarzy hello u dołu hello hello strony. Prześlij niektórych szczegółów na temat co oczekiwano toosee i jak tooimprove hello artykułu.  

## <a name="hello-components-of-azure"></a>Witaj składniki platformy Azure
Azure grup usług na kategorie w hello portalu zarządzania i w różne wizualne, takie jak hello [co to jest Azure Infographic](https://azure.microsoft.com/documentation/infographics/azure/) . Witaj portalu zarządzania, które jest używane toomanage najbardziej (ale nie wszystkie) usługi na platformie Azure.

W tym artykule będzie używać **innej organizacji** tootalk o usługach na podstawie podobnych funkcji i toocall się ważne usługi podrzędne, które należą do nich większe.  

![Składniki platformy Azure](./media/fundamentals-introduction-to-azure/AzureComponentsIntroNew780.png)   
 *Rysunek: Azure zapewnia dostęp do Internetu usług aplikacji uruchomionych w centrach danych platformy Azure.*

## <a name="management-portal"></a>Portal zarządzania
Platforma Azure ma interfejs sieci web o nazwie hello [portalu zarządzania](http://manage.windowsazure.com) która pozwala administratorom tooaccess i zarządzać nim funkcje większości, ale nie wszystkie platformy Azure.  Firma Microsoft udostępnia zwykle hello nowszej interfejsu użytkownika portalu w wersji beta przed jego wycofaniem stary. Witaj nowszej jest nazywany hello ["Portalu Azure w wersji zapoznawczej"](https://portal.azure.com/).

Istnieje zwykle długie nakładają się na siebie, gdy oba portali są aktywne. Gdy w obu portalach pojawi się podstawowe usługi, nie wszystkie funkcje mogą być dostępne w obu. Nowsza usług może wyświetlani w hello nowszej portalu pierwszy i starszych usługi i funkcje mogą znajdować się tylko w hello stary.  w tym miejscu wiadomość Hello jest który Jeżeli nie można znaleźć elementu w hello starszy portal, sprawdź hello nowszą i na odwrót.

## <a name="compute"></a>Wystąpienia obliczeniowe
Jedną z najprostszych czynności hello, platformy w chmurze nie jest wykonywania aplikacji. Każda hello modeli obliczeń platformy Azure ma własną tooplay roli.

Można używać tych technologii osobno lub łączyć je stosownie do potrzeb foundation prawo hello toocreate aplikacji. Możesz wybrać, zależy od metody Hello na jakie problemy próbujesz toosolve.

### <a name="azure-virtual-machines"></a>Azure Virtual Machines
![Maszyny wirtualne Azure ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_VirtualMachinesIntroNew_12345.png)   
*Rysunek: Maszyny wirtualne platformy Azure umożliwia pełną kontrolę nad wystąpień maszyn wirtualnych w chmurze hello.*

Witaj toocreate możliwości maszyny wirtualnej na żądanie, czy za pomocą standardowego obrazu lub z jednej z podanych, może być bardzo przydatne. Takie podejście, powszechnie znane jako infrastruktura jako usługa (IaaS), jest zawiera maszyny wirtualne platformy Azure. Na rysunku 2 przedstawiono kombinację, jak działa maszyna wirtualna (VM) i jak toocreate jedną z dysku VHD.  

toocreate maszyny Wirtualnej, określ rozmiar które wirtualnego dysku twardego toouse i hello maszyny Wirtualnej.  Następnie płacisz za czas hello powitalne tej maszyny Wirtualnej jest uruchomiona. Płacisz za minutę hello i tylko wtedy, gdy jest uruchomiona, ale istnieje opłat minimalnego magazynu do przechowywania hello wirtualnego dysku twardego dostępna. System Azure oferuje galerii zasobów wirtualnych dysków twardych (nazywanych "obrazy") zawierających toostart rozruchowego systemu operacyjnego, z. Należą do firmy Microsoft i partnerów opcje, takie jak Windows Server i Linux, SQL Server, Oracle i wiele innych. W przypadku wolnego toocreate wirtualne dyski twarde i obrazów, a następnie przekazać je samodzielnie. Możesz nawet przekazać wirtualne dyski twarde, które zawierają tylko dane i uzyskiwanie do nich dostępu z uruchomionych maszyn wirtualnych.

Wszędzie tam, gdzie hello wirtualnego dysku twardego pochodzi z, można przechowywać trwale wszelkie zmiany dokonywane w uruchomionej maszyny Wirtualnej. Witaj następnym utworzyć Maszynę wirtualną z tego dysku VHD, czynności wybierz pracę. Witaj VHD z powrotem hello maszyny wirtualne są przechowywane w obiektach blob magazynu Azure, które są omawiane później.  Oznacza to, że możesz uzyskać tooensure nadmiarowość, które maszyny wirtualne nie będą znikają powodu awarii toohardware i dysku. Jego również możliwe toocopy hello zmienić wirtualnego dysku twardego z platformy Azure, uruchomić je lokalnie.

Aplikacja działa w co najmniej jednej maszyny wirtualnej, w zależności od tego, jak utworzyć go przed lub zdecydować, toocreate ją od podstaw teraz.

Toocloud tego podejścia dość ogólny komputerowe mogą być używane tooaddress wiele różnych problemów.

**Scenariusze maszyny wirtualnej**

1. **Tworzenie/testowanie** — można ich używać toocreate niedrogich platformy prac deweloperskich i testowych, które można zamknąć po zakończeniu korzystania z niego. Może również tworzenie i uruchamianie aplikacji, które używają niezależnie od języków i chcesz bibliotek. Te aplikacje mogą używać hello danych zarządzania opcje, które platforma Azure udostępnia i można także toouse programu SQL Server lub innego systemu DBMS uruchomiona w co najmniej jednej maszyny wirtualnej.
2. **Przenieś aplikacje tooAzure (przyrostu i zmiana)** — "Przyrostu i shift" odwołuje się toomoving aplikacji podobnie jak zwykłych toomove widłowego dużego obiektu.  Możesz "przyrostu" hello wirtualnego dysku twardego z lokalnego centrum danych i "shift" on tooAzure i uruchom go brak.  Zazwyczaj konieczne będzie toodo dotyczą pracy tooremove zależności w innych systemach. Jeżeli istnieją zbyt wiele, można wybrać opcję 3 zamiast tego.  
3. **Rozszerzanie centrum danych** -maszynach wirtualnych platformy Azure używana jako rozszerzenie lokalnego centrum danych, programem SharePoint lub inne aplikacje. toosupport, jest możliwe toocreate domen systemu Windows w chmurze hello uruchamiając usługi Active Directory w maszynach wirtualnych platformy Azure. Umożliwia tootie sieci wirtualnej platformy Azure (wymienionych później) sieci lokalnej i sieci na platformie Azure razem.

### <a name="web-apps"></a>Web Apps
![ROBBCSIART_TEST aplikacji sieci Web platformy Azure](./media/fundamentals-introduction-to-azure/mscsiart_AzureWebsitesIntroNew_12345.png)   
 *Rysunek: Azure aplikacje sieci Web uruchamia aplikację witryny sieci Web w chmurze hello bez konieczności toomanage powitania serwera sieci web.*

Jedno hello najbardziej typowych rzeczy, które użytkownicy wykonują w chmurze hello jest uruchomienie witryny sieci Web i aplikacji sieci web. Maszyn wirtualnych platformy Azure pozwala na to, ale nadal można pozostawia odpowiada hello administrowania maszyn wirtualnych i hello bazowy systemów operacyjnych. Można to zrobić przez role sieci web usługi w chmurze, ale wdrażania i konserwowania je nadal trwa pracy administracyjnej.  Co zrobić, jeśli chcesz witryny sieci Web w przypadku gdy ktoś inny włączył zajmuje się hello czynności administracyjnych dla Ciebie?

Jest to dokładnie, aplikacje sieci Web udostępnia. Ten model obliczeń oferuje środowisko sieci web zarządzanej, za pomocą portalu zarządzania Azure hello, a także interfejsów API. Można przenieść istniejącą aplikację witryny sieci Web do aplikacji sieci Web bez zmian lub można utworzyć nową bezpośrednio w chmurze hello. Po uruchomieniu witryna sieci Web, można dodawać lub usuń wystąpienia dynamicznie, zależne aplikacje sieci Web Azure tooload równoważenie żądań między nimi. Aplikacje platformy Azure oferuje zarówno udostępnionego opcja, w którym witryny sieci Web jest uruchomiona na maszynie wirtualnej z innymi lokacjami, i standardowych opcji, która umożliwia toorun lokacji na jego własnej maszynie Wirtualnej. Opcja standardowa Hello umożliwia również zwiększenie rozmiaru hello (mocy obliczeniowej) swoich wystąpień, w razie potrzeby.

Do tworzenia aplikacji aplikacje sieci Web obsługuje .NET, PHP, Node.js, Java i Python oraz bazy danych SQL i MySQL (od ClearDB, partnera firmy Microsoft) dla relacyjnego magazynu. Udostępnia także wbudowaną obsługę dla kilku popularnych aplikacji, w tym WordPress, Joomla i Drupal. Celem Hello jest tooprovide ekonomicznych, skalowalnych i szeroko użyteczny platforma do tworzenia witryn sieci Web i aplikacji sieci web w chmurze publicznej hello.

**Scenariusze aplikacji sieci Web**

Aplikacje sieci Web jest zamierzone toobe przydatne w przypadku firm, deweloperzy i agencje projektu sieci web. W firmach jest łatwy w zarządzaniu, skalowalnej, bardzo bezpieczny i wysokiej dostępności rozwiązanie służące do uruchamiania obecności witryn sieci Web. Jeśli potrzebujesz tooset zapasowej witryny sieci Web jest najlepszym toostart z aplikacjami sieci Web platformy Azure i kontynuować tooCloud usługi, gdy potrzebujesz funkcji, która nie jest dostępna. Zobacz hello koniec sekcji "Obliczeniowe" hello więcej łączy, które mogą ułatwić toochoose między opcjami hello.

### <a name="cloud-services"></a>Cloud Services
![Usługi w chmurze Azure](./media/fundamentals-introduction-to-azure/CloudServicesIntroNew.png)   
*Rysunek: Usługi w chmurze Azure udostępnia miejsce toorun wysoce skalowalna niestandardowy kod na platformie jako środowiska usługa (PaaS)*

Załóżmy, że chcesz toobuild aplikacji w chmurze, która może obsługiwać wiele równoczesnych użytkowników, nie wymaga dużo administracji i nigdy nie przestanie działać. Może być nawiązane oprogramowania dostawcy, na przykład to jest podjęcie decyzji w sprawie tooembrace oprogramowanie jako usługa (SaaS) przez tworzenie wersji jednej z aplikacji w chmurze hello. Lub może być uruchamiania, tworzenia aplikacji konsumenta oczekiwanego wzrośnie szybkie. Jeśli tworzysz na platformie Azure, model, który wykonanie zasadny skorzystać?

Aplikacje sieci Web platformy Azure umożliwia tworzenie tego rodzaju aplikacji sieci web, ale istnieją pewne ograniczenia. Nie masz dostępu administracyjnego, na przykład, co oznacza, że nie można zainstalować dowolne oprogramowanie. Maszyn wirtualnych platformy Azure zapewnia dużą elastyczność, łącznie z dostępem administracyjnym pewnością umożliwia toobuild słaba skalowalność aplikacji, a będziesz mieć toohandle wiele aspektów niezawodność i administrowanie samodzielnie. Co chcesz to opcja, która umożliwia hello kontroli potrzebne, ale również obsługiwać większość pracy hello wymaganej niezawodność i administrowania.

Jest to dokładnie, co to jest zapewniana przez usługi w chmurze Azure. Ta technologia jest zaprojektowany wyraźnie toosupport skalowalne, niezawodne i niski — administrator aplikacji, i jest przykładem co ma często wywołuje platforma jako usługa (PaaS). toouse, tworzenie aplikacji przy użyciu technologii hello wybierzesz, takich jak C#, Java, PHP, Python, Node.js lub innego elementu. Kod następnie wykonuje na maszynach wirtualnych (tooas określonego wystąpienia) z wersją systemu Windows Server.

Jednak te maszyny wirtualne różnią się od hello utworzonymi przez tworzenie maszyn wirtualnych z platformy Azure. Na rzecz Azure sama zarządza ich funkcji, takich jak instalowanie poprawek systemu operacyjnego i automatycznie wprowadza nowe poprawianie obrazów. Oznacza to, że aplikacja nie powinien zarządzania stanem w sieci web lub procesu roboczego wystąpień roli; Zamiast tego powinien być dobrze w jednej opcji zarządzania usługi Azure data hello opisany w następnej sekcji hello. Azure monitoruje także tych maszyn wirtualnych, w każdym ponownym uruchomieniu działających w trybie. Można ustawić chmury usługi tooautomatically utworzyć więcej lub mniej wystąpień w toodemand odpowiedzi. Dzięki temu można toohandle zwiększenie użycia i skali ponownie, więc nie są płatności tyle po mniej użycia.

Masz dwie role toochoose podczas tworzenia wystąpienia, oparte na systemie Windows Server. Hello podstawowa różnica między hello dwa polega na tym, że wystąpienie roli sieci web uruchomione usługi IIS, a wystąpienie roli proces roboczy nie. Zarówno są zarządzane w hello wspólne dla aplikacji toouse zarówno przez sam sposób, jednak i. Na przykład wystąpienie roli sieci web może akceptować żądania od użytkowników, a następnie przekazać je tooa wystąpienia roli procesu roboczego do przetwarzania. tooscale aplikacji w górę lub w dół, mogą żądać więcej wystąpień roli albo utwórz Azure lub zamknij istniejącego wystąpienia. I podobne tooAzure maszyny wirtualne są naliczane opłaty tylko raz hello działa każde wystąpienie roli sieci web lub procesu roboczego.

**Scenariusze usług w chmurze**

Usługi w chmurze są idealne toosupport dużego skalowania w poziomie, gdy wymagają więcej kontrolę nad platformy hello niż udostępniane przez aplikacje sieci Web Azure, ale nie ma potrzeby kontrolę nad hello system operacyjny.

#### <a name="choosing-a-compute-model"></a>Wybieranie modelu obliczeń
Strona Hello [porównania Azure Web Apps, usługi w chmurze i maszyn wirtualnych](app-service-web/choose-web-site-cloud-service-vm.md) zawiera bardziej szczegółowe informacje na temat toochoose modelu obliczeń.

## <a name="data-management"></a>Zarządzanie danymi
Aplikacje muszą danych, i różnego rodzaju aplikacje wymagają różnych typów danych. W związku z tym Azure zapewnia kilka różnych sposobów toostore danych i zarządzać nimi. Platforma Azure udostępnia wiele opcji dotyczących magazynów, ale wszystkie są przeznaczone dla bardzo trwałego magazynu.  Za pomocą dowolnego z tych opcji są zawsze 3 kopie danych utrzymywane w synchronizacji między centrum danych Azure — 6, jeśli zezwolisz na tooback nadmiarowość geograficzna Azure toouse się datacenter tooanother co najmniej 300 mil optymalizacji.     

### <a name="in-virtual-machines"></a>W przypadku maszyn wirtualnych
istnieją już wymienione Hello toorun możliwości programu SQL Server lub innego systemu DBMS w maszyny Wirtualnej utworzonej z maszyn wirtualnych platformy Azure. Należy pamiętać, że ta opcja jest ograniczona toorelational systemów. Możesz również wolnego toorun NoSQL technologii, takich jak bazy danych MongoDB i Cassandra. Uruchamianie systemu bazy danych jest proste it są replikowane co to jest używane tooin naszych centrach danych-, ale wymagany jest również obsługa hello administracyjnej z tego systemu DBMS.  W innych opcji Azure obsługuje więcej lub hello administracji dla Ciebie.

Ponownie stan hello hello maszyny wirtualnej i dyskami dodatkowe dane w przypadku utworzenia lub Przekaż obsługiwanych przez magazynu obiektów blob, (który omawianiu później).  

### <a name="azure-sql-database"></a>Usługa Azure SQL Database
![Baza danych SQL Azure Storage](./media/fundamentals-introduction-to-azure/StorageAzureSQLDatabaseIntroNew.png)   

*Rysunek: Baza danych SQL Azure udostępnia usługę zarządzanych relacyjnej bazy danych w chmurze hello.*

Dla relacyjnego magazynu Azure oferuje funkcję hello bazy danych SQL. Nie zezwala na powitania nazewnictwa oszukiwania użytkownika. To jest inny niż typowe bazy danych SQL programu SQL Server uruchomiony na systemie Windows Server.  

Nazywanych SQL Azure, baza danych SQL Azure udostępnia wszystkie hello najważniejsze funkcje relacyjnej bazy danych system zarządzania tym atomic transakcji, dostępu do danych równoczesnych przez wielu użytkowników o integralności danych, zapytania ANSI SQL i znanych programowania model. Jak SQL Server, bazy danych SQL jest możliwy przy użyciu programu Entity Framework, ADO.NET, JDBC i innych znanych danych dostępu do technologii. Obsługuje ona również większość hello języka T-SQL, a także udostępnia narzędzia programu SQL Server, takich jak SQL Server Management Studio. Każdy zapoznać się z programu SQL Server (lub innego relacyjnej bazy danych), przy użyciu bazy danych SQL jest proste.

Baza danych SQL nie jest po prostu systemu DBMS w hello it chmury do usługi typu PaaS. Nadal kontrolować danych i który można do niego dostęp, ale hello administracyjne grunt pracy, takich jak zarządzanie hello sprzętu infrastruktury i automatycznie utrzymywanie hello oprogramowania bazy danych i systemu operacyjnego w górę toodate zajmuje bazy danych SQL. Baza danych SQL zapewnia wysoką dostępność, automatyczne kopie zapasowe, w momencie przywracania możliwości i może replikować kopie w regionach geograficznych.  

**Scenariusze dotyczące bazy danych SQL**

Jeśli tworzysz aplikację Azure (przy użyciu dowolnego modelu obliczeń hello) wymagające relacyjnego magazynu bazy danych SQL może być dobrym rozwiązaniem. Aplikacje działające poza hello chmury można również użyć tej usługi, jednak, więc istnieje wiele innych scenariuszy. Na przykład dane przechowywane w bazie danych SQL są dostępne z systemów innego klienta, w tym komputerów stacjonarnych, laptopów, tabletów i telefonów. I ponieważ udostępnia wbudowaną wysoką dostępność w ramach replikacji, przy użyciu bazy danych SQL można zminimalizować czas przestoju.

### <a name="tables"></a>Tabele
![Tabele usługi Azure Storage](./media/fundamentals-introduction-to-azure/StorageTablesIntroNew.png)  

*Rysunek: Tabel Azure udostępnia prosty danych toostore sposób NoSQL.*

Ta funkcja jest niekiedy nazywany różnych warunków w ramach większych funkcji o nazwie "Magazyn Azure". Jeśli widzisz "tabele", "Tabelach platformy Azure" lub "tabel do przechowywania", to wszystkie hello samo.  

I nie należy mylić według nazwy hello: Ta technologia nie udostępnia magazyn relacyjny. W rzeczywistości jest przykładem podejścia NoSQL określana magazyn kluczy i wartości. Tabele Azure umożliwiają aplikacji przechowywania właściwości różnych typów, takich jak ciągów, liczb całkowitych i daty. Następnie aplikacja może pobrać grupy właściwości, zapewniając Unikatowy klucz dla tej grupy. Podczas operacji złożonych takich jak sprzężenia nie są obsługiwane, tabele oferują szybki dostęp tootyped danych. Są one również słaba skalowalność z pojedynczej tabeli toohold stanie jak terabajtów danych. I dopasowywanie ich prostotę, tabele są toouse zazwyczaj mniej kosztowne niż relacyjnego magazynu bazy danych SQL.

**Scenariusze dotyczące tabel**

Załóżmy, że chcesz toocreate aplikacji Azure, wymagającym szybki dostęp do danych tootyped, może być on wiele, ale nie wymaga tooperform złożonych zapytań SQL na tych danych. Na przykład załóżmy, że tworzony aplikacji klienta, która wymaga informacji o profilu klienta toostore dla każdego użytkownika. Aplikacji będzie toobe bardzo popularna, więc należy tooallow dla duże ilości danych, ale nie zrobisz wiele z tych danych oprócz przechowywania, pobierania jej w prosty sposób. Jest to dokładnie hello rodzaj scenariusz, w którym sens tabel Azure.

### <a name="blobs"></a>Obiekty blob
![Obiekty BLOB magazynu Azure](./media/fundamentals-introduction-to-azure/StorageBlobsIntroNew.png)    
*Rysunek: Obiekty BLOB platformy Azure udostępnia bez struktury danych binarnych.*  

Obiekty BLOB platformy Azure (ponownie "Magazynu obiektów Blob" i po prostu "obiektów blob magazynu" są hello samo) jest zaprojektowana toostore bez struktury danych binarnych. Jak tabele obiekty BLOB udostępnia niedrogich magazynów, a pojedynczego obiektu blob może być większy niż 1TB (jeden terabajt). Aplikacjami platformy Azure można także używać dysków Azure, które umożliwiają trwałe przechowywanie plików systemu Windows zainstalowane w wystąpieniu usługi Azure blob. Aplikacja Hello widzi zwykłe pliki systemu Windows, ale zawartość hello są przechowywane w obiekcie blob.

Magazyn obiektów blob jest używany przez wiele innych funkcji platformy Azure (w tym maszyny wirtualne), więc obciążeń na pewno może obsługiwać zbyt.

**Scenariusze dotyczące obiektów blob**

Aplikację, która przechowuje pliki wideo, duże lub inne informacje binarne można używać proste i tanie magazynu obiektów blob. Obiekty BLOB są również powszechnie używane w połączeniu z innymi usługami, takich jak Content Delivery Network, który będzie omawianiu później.  

### <a name="import--export"></a>Import/eksport
![Usługa eksportu importowania platformy Azure](./media/fundamentals-introduction-to-azure/ImportExportIntroNew.png)  

*Rysunek: Azure importu / eksportu zawiera hello możliwości tooship tooor fizyczny dysk twardy z platformy Azure dla zbiorczego szybsze i tańsze importu lub eksportu.*  

Czasami ma toomove dużych ilości danych na platformie Azure. Który może zająć dużo czasu, być może przez kilka dni, a następnie użyj partii przepustowości. W takich przypadkach można użyć Import/Eksport Azure, dzięki czemu możesz tooship zaszyfrowane przez funkcję Bitlocker 3,5" dysków twardych SATA bezpośrednio tooAzure centrów danych, których Microsoft będzie transferu danych hello do magazynu obiektów blob dla Ciebie.  Po zakończeniu przekazywania hello firmy Microsoft jest dostarczany tooyou wstecz hello dysków.  Możesz również poprosić o czy dużych ilości danych z magazynu obiektów Blob można wyeksportować na dyski twarde i wysłać wstecz tooyou za pośrednictwem poczty.

**Scenariusze dotyczące Import / Eksport**

* **Duże migracji danych** — w dowolnym momencie masz dużych ilości danych (terabajty) czy ma tooupload tooAzure, hello usługi Import/Eksport jest często dużo szybsze i tańsze prawdopodobnie niż jego przesyłania za pośrednictwem hello internet. Po hello danych w obiektach blob może przetwarzać go do innych formularzy, takie jak magazyn tabel lub bazy danych SQL.
* **Archiwizowane danych odzyskiwania** — można użyć importu/eksportu toohave Microsoft transfer dużych ilości danych przechowywanych w magazynie obiektów Blob Azure urządzenie magazynujące tooa wysyłania i wybrać urządzenie dostarczyć lokalizacji wstecz tooa chcesz. Ponieważ to zajmie trochę czasu, nie jest dobra opcja w przypadku odzyskiwania po awarii. Najlepiej niepotrzebnych szybki dostęp do danych archiwalnych.

### <a name="file-service"></a>Usługi plików
![Usługi plików na platformę Azure](./media/fundamentals-introduction-to-azure/FileServiceIntroNew.png)    
*Rysunek: Azure usługi plików zapewniają SMB \\ \\server\share ścieżki dla aplikacji działających w chmurze hello.*

W infrastrukturze lokalnej, jest typowe toohave dużych ilości magazynu plików są dostępne przy użyciu protokołu bloku komunikatów serwera (SMB) hello \\ \\Server\share format. Azure ma teraz usługa umożliwiająca toouse tego protokołu w chmurze hello. Aplikacje działające na platformie Azure może być używany tooshare plików między maszynami wirtualnymi przy użyciu systemu plików znanych interfejsów API, takich jak ReadFile i WriteFile. Ponadto hello pliki można również jest dostępny pod adresem hello jednocześnie za pośrednictwem interfejsu REST, dzięki czemu udziałów hello tooaccess z lokalnymi konfigurując również sieci wirtualnej. Usługa pliki Azure jest oparty na powitania usługa blob, dziedziczy hello tego samego dostępności, trwałości, skalowalność i nadmiarowość geograficzna wbudowana w usłudze Azure Storage.

**Scenariusze dotyczące plików platformy Azure**

* **Migrowanie istniejących aplikacji toohello chmury** — jego łatwiejsze toomigrate lokalnej aplikacji toohello chmurze używane pliku udostępnia dane tooshare między częściami aplikacji hello. Każda maszyna wirtualna połączenie toohello udziału plików i następnie może odczytywać i zapisywać pliki, podobnie jak jego czy względem pliku lokalnego udziału.
* **Udostępnionych ustawień aplikacji** -toohave pliki konfiguracji w centralnej lokalizacji, gdzie są one dostępne z wielu różnych maszyn wirtualnych jest wspólnego wzorca dla aplikacji rozproszonych. Te pliki konfiguracji można przechowywane w udziale plików Azure i odczytywane przez wszystkich wystąpień aplikacji. Ustawienia Hello odbywa się za pośrednictwem interfejsu REST hello, co umożliwia dostęp na całym świecie toohello plików konfiguracyjnych.
* **Udział diagnostycznych** — można zapisywać i udostępniać pliki diagnostyczne, takie jak dzienniki, metryki, i zrzuty awaryjne. Te pliki, które są dostępne za pośrednictwem interfejsu REST i hello SMB umożliwia różnych narzędzi analizy do przetwarzania i analizowania danych diagnostycznych hello toouse aplikacji.
* **Dev/Test/Debug** — w przypadku pracy z maszyn wirtualnych w chmurze hello, deweloperzy i Administratorzy często muszą zestaw narzędzi. Instalowanie i rozpowszechnianie tych narzędzi na każdej maszynie wirtualnej jest czasochłonne. W przypadku plików Azure dewelopera lub administratora można przechowywać ich ulubionych narzędzi w udziale plików i połączyć toothem z dowolnej maszyny wirtualnej.

## <a name="networking"></a>Sieć
Azure obecnie działa w wielu centrach danych rozmieszczenie hello world. Podczas uruchamiania aplikacji lub przechowywania danych, można wybrać co najmniej jednego z tych toouse centrów danych. Umożliwia też łączność centrów danych toothese na różne sposoby, za pomocą usług hello poniżej.

### <a name="virtual-network"></a>Virtual Network
![VirtualNetwork](./media/fundamentals-introduction-to-azure/VirtualNetworkIntroNew.png)   

*Rysunek: Sieci wirtualnych zapewnia sieci prywatnej w chmurze hello tak różnych usług można rozmawiać tooeach innych lub zasobów lokalnych tooon po skonfigurowaniu połączenia sieci VPN między lokalizacjami.*  

Tootreat jest jeden toouse wygodny sposób chmury publicznej jako rozszerzenie własnego centrum danych.

Ponieważ maszyn wirtualnych można utworzyć na żądanie, następnie usuń je (i zatrzymać, zwracając) nie są już potrzebne, można tak skonfigurować mocy obliczeniowej, tylko wtedy, gdy jest to konieczne. I ponieważ maszyny wirtualne Azure umożliwia tworzenie maszyn wirtualnych z programem SharePoint, usługi Active Directory i inne oprogramowanie znanych lokalnymi, takie podejście może współpracować z aplikacji hello już istnieje.

toomake to naprawdę przydatny, jednak użytkownicy powinna tootreat stanie toobe te aplikacje tak, jakby działały we własnym centrum danych. Jest to dokładnie, umożliwia sieci wirtualnej platformy Azure. Za pomocą urządzenia bramy sieci VPN, administrator może skonfigurować wirtualnej sieci prywatnej (VPN) między sieci lokalnej i sieci maszyn wirtualnych, które są wdrożone tooa sieci wirtualnej na platformie Azure. Ponieważ przypisać własnego adresu IP w wersji 4 adresy toohello chmury maszyn wirtualnych, pojawią się one toobe we własnej sieci. Użytkownicy w organizacji mają dostęp do aplikacji hello tych maszyn wirtualnych zawierają tak, jakby były uruchomione lokalnie.

Aby uzyskać więcej informacji na temat planowania i tworzenia sieci wirtualnej, który można wyświetlić [sieci wirtualnej](virtual-network/virtual-networks-overview.md).

### <a name="express-route"></a>ExpressRoute
![ExpressRoute](./media/fundamentals-introduction-to-azure/ExpressRouteIntroNew.png)   

*Rysunek: Używa ExpressRoute sieci wirtualnej platformy Azure, ale trasy połączenia za pośrednictwem dedykowanej szybciej wierszy zamiast hello publicznej sieci Internet.*  

Jeśli potrzebujesz więcej przepustowości lub zabezpieczeń niż sieci wirtualnej platformy Azure zapewniają połączenia, można sprawdzić w ExpressRoute. W niektórych przypadkach ExpressRoute można także zmniejszyć koszty. Nadal będziesz potrzebować sieci wirtualnej na platformie Azure, ale powiązanie hello Azure i witryny sieci Web używa dedykowanego połączenia nie przechodzi przez hello publicznej sieci Internet. W kolejności toouse tej usługi, należy toohave umowę z dostawcą usługi sieciowej lub dostawcy programu exchange.

Konfigurowanie połączenia ExpressRoute wymaga więcej czasu i planowania, dlatego może być toostart z sieci VPN lokacja lokacja, a następnie tooan połączenia ExpressRoute.

Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz [opis techniczny ExpressRoute](expressroute/expressroute-introduction.md).

### <a name="traffic-manager"></a>Traffic Manager
![TrafficManager](./media/fundamentals-introduction-to-azure/TrafficManagerIntroNew.png)   

*Rysunek: Usługi Azure Traffic Manager umożliwia możesz tooroute globalne tooyour ruchu na podstawie reguł inteligentnego.*

Jeśli aplikacja Azure jest uruchomiona w wielu centrach danych, używając usługi Azure Traffic Manager tooroute żądania od użytkowników inteligentnie między wystąpieniami aplikacji hello. Można również kierować ruchem tooservices nie działają na platformie Azure tak długo, jak są one dostępne z hello internet.  

Aplikacja Azure z użytkownikami w jednej części Witaj świecie może działać w centrum danych Azure tylko jeden. Z użytkownikami aplikacji rozproszonych na całym świecie hello, jednak, jest prawdopodobnie bardziej toorun w wielu centrach danych, może nawet wszystkich z nich. W tej drugiej sytuacji czoła problem: jak można inteligentnie bezpośrednie wystąpienia tooapplication użytkowników? W większości przypadków hello, prawdopodobnie potrzebna będzie każdego użytkownika tooaccess hello datacenter najbliższego tooher, ponieważ prawdopodobnie zapewni jego hello najlepsze czas odpowiedzi. Ale co zrobić, jeśli to wystąpienie aplikacji hello jest przeciążony lub jest niedostępny? W takim przypadku będzie można jej żądania nieuprzywilejowany toodirect automatycznie tooanother centrum danych. Jest to dokładnie, co jest wykonywane przez usługę Azure Traffic Manager.

Właściciel aplikacji Hello definiuje reguły, które Określ sposób żądania od użytkowników powinny być ukierunkowanej toodatacenters, a następnie zależy od usługi Traffic Manager toocarry te zasady. Na przykład użytkownicy normalnie mogą być ukierunkowanej toohello podczas najbliższego centrum danych Azure, ale jest wysyłana tooanother jedną gdy czas reakcji hello z ich domyślne centrum danych przekracza hello czas odpowiedzi z innych centrów danych. W przypadku aplikacji rozproszonych globalnie z wieloma użytkownikami problemów toohandle wbudowanej usługi, takich jak te przydaje się.

Menedżer ruchu używa końcowych tooservice użytkowników tooroute katalogu Name Service (DNS), ale dalsze ruch przechodzi przez Menedżera ruchu po ustanowieniu tego połączenia. Dzięki temu Menedżera ruchu jest wąskie gardło, może to spowolnić komunikacji usługi.

## <a name="developer-services"></a>Usługi dla deweloperów
Azure oferuje wiele narzędzi toohelp deweloperów i informatyków, tworzyć i obsługiwać aplikacje w chmurze hello.  

### <a name="azure-sdk"></a>Zestaw Azure SDK
Ponownie w 2008 hello pierwszego wersji wstępnej programu Azure obsługiwane tylko .NET — rozwój. Już dziś jednak można utworzyć aplikacje platformy Azure w niemal dowolnym języku. Firma Microsoft udostępnia obecnie specyficzny dla języka zestawy SDK dla platformy .NET, Java, PHP, Node.js, Ruby i Python. Istnieje również ogólne zestawu Azure SDK, który zapewnia podstawową pomocą techniczną dla dowolnego języka, takich jak C++.  

Te zestawy SDK ułatwiają tworzenie, wdrażanie i zarządzanie aplikacjami platformy Azure. Są one dostępne albo z [www.microsoftazure.com](https://azure.microsoft.com/downloads/) lub GitHub i ich można używać z programu Visual Studio i Eclipse. System Azure oferuje także narzędzi wiersza polecenia, które deweloperzy mogą używać w innych środowiskach edytora lub rozwoju, w tym narzędzia do wdrażania aplikacji tooAzure z systemów Linux i komputerów Macintosh.

Wraz z pomaga tworzyć aplikacje platformy Azure, te zestawy SDK udostępniają bibliotek klienckich, które ułatwiają tworzenie oprogramowania używa usług Azure. Na przykład możesz utworzyć aplikację, która odczytuje i zapisuje obiekty BLOB platformy Azure, lub utworzyć narzędziem wdraża aplikacje platformy Azure za pomocą interfejsu zarządzania Azure hello.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services
Visual Studio Team Services jest nazwą marketing, obejmującego numer usługi, które pomagają toodevelop aplikacji hello Azure.

pomyłek tooavoid — nie zapewnia ona oparta na sieci Web lub obsługiwanych wersji programu Visual Studio. Nadal potrzebujesz uruchomionych lokalną kopię programu Visual Studio. Jednak udostępnia wiele narzędzi, które mogą być bardzo przydatne.

Posiada system kontroli źródła hostowanej o nazwie Team Foundation Service, która oferuje kontroli wersji oraz śledzenie elementu roboczego.  Jeśli wolisz, która nawet umożliwia Git kontroli wersji. I może różnić się hello systemu kontroli źródła, używanego przez projekt. Możesz utworzyć projekty zespołowe prywatnej nieograniczone dostępna z dowolnego miejsca w hello world.  

Visual Studio Team Services udostępnia usługę testowania obciążenia. Można wykonywać utworzone w programie Visual Studio na maszynach wirtualnych w chmurze hello testów obciążenia. Określ hello całkowita liczba użytkowników, dla których chcesz tooload test o i Visual Studio Team Services automatycznie określić, ile agenci są potrzebne, aż hello wymagane maszyn wirtualnych i wykonywanie testów obciążenia. Jeśli jesteś subskrybentem MSDN, możesz uzyskać tysiące wolnego użytkownika minut miesięcznie testowania obciążenia.

Visual Studio Team Services oferuje również obsługę elastyczne programowanie za pomocą funkcji, takich jak kompilacje ciągłej integracji i tablic Kanban pokoje zespołów wirtualnego.

**Visual Studio Team Services scenariuszy**

Visual Studio Team Services jest dobra opcja w przypadku firm, które wymagają toocollaborate na całym świecie, a nie mają jeszcze infrastruktury hello w miejscu toodo tak. Możesz pobrać Instalatora w minutach, wybierz system kontroli źródła i rozpocząć pisanie kodu i tworzenia tego dnia.  narzędzia zespołowego Hello służą do koordynacji i współpracy i dodatkowe narzędzia hello zapewnić analizy hello potrzebne tootest i szybko dostrajania aplikacji.

Jednak organizacje, które mają już lokalnego systemu można przetestować nowe projekty na toosee Visual Studio Team Services, jeśli jest bardziej wydajne.   

### <a name="application-insights"></a>Application Insights
![Application Insights](./media/fundamentals-introduction-to-azure/ApplicationInsights.png)  

*Rysunek: Usługi Application Insights monitory wydajności i użycia aktywnej aplikacji sieci web lub urządzenia.*

Kiedy czy jest uruchamiany na urządzeniach przenośnych, komputerów stacjonarnych lub przeglądarki sieci web — po opublikowaniu aplikacji - usługi Application Insights informuje, jak działa prawidłowo, i co robią użytkownicy z nim. Spowoduje zachowanie liczbę awarii (Crash) i powolna odpowiedź, alertów Jeśli rysunki hello cross niedopuszczalne progów i pomóc w zdiagnozowaniu problemów.

W przypadku tworzenia nowej funkcji należy planować toomeasure jej poprawnego działania użytkowników. Analizując wzorce użycia, zrozumieć, co jest najlepsza dla klientów i Zwiększ możliwości swoich aplikacji w każdym cyklu programowania.

Mimo że jest ona hostowana na platformie Azure, usługi Application Insights działa w przypadku szeroką gamę rosnącym aplikacji, zarówno w i poza Azure. Zarówno J2EE i platformy ASP.NET sieci web, które aplikacje są objęte, a także iOS, aplikacje dla systemu Android, OS x i Windows. Dane telemetryczne są wysyłane z zestawu SDK skompilowanej za pomocą aplikacji hello toobe przeanalizowany i wyświetlane w hello usługa Application Insights na platformie Azure.

Analiza wyspecjalizowanego, wyeksportować hello telemetrii strumienia tooa bazy danych, lub tooPower BI lub innych narzędzi.

**Application Insights scenariuszy**

Tworzysz aplikację. Może być aplikacja sieci web lub aplikacji urządzenia lub aplikacji przez urządzenia z sieci web zaplecza.

* Dostrajaniu hello aplikacji po jej opublikowania lub gdy jest testowanie obciążenia.  Usługa Application Insights agreguje dane telemetryczne z wszystkich wystąpień hello zainstalowany i stanowi wykresy czasy odpowiedzi, żądanie i liczby wyjątków, zależności czasów odpowiedzi i innych wskaźników wydajności. Te pomagają dostrajania wydajności aplikacji. Możesz wstawić kod tooreport bardziej szczegółowe dane, jeśli zajdzie taka potrzeba.
* Wykrywanie i diagnozowanie problemów w aktywnej aplikacji. Alerty można uzyskać za pośrednictwem poczty e-mail, jeśli wskaźniki wydajności między progami akceptowalne. Można zbadać sesji użytkownika, na przykład żądania hello toosee, który spowodował wyjątek.
* Śledzenie użycia tooassess hello Powodzenie każdej nowej funkcji. Podczas projektowania nowego wątku użytkownika planowanie toomeasure, ile jest używany i czy użytkownicy zapewnienia ich oczekiwane cele. Usługi Application Insights udostępnia podstawowe dane dotyczące użycia takich jak widoki strony sieci web i środowisko użytkownika hello tootrack kodu można wstawić bardziej szczegółowo.

### <a name="automation"></a>Automatyzacja
Nikt nie lubi toowaste czasu wykonywania hello tego samego ręcznego przetwarza samodzielnego. Automatyzacja Azure umożliwia dla toocreate można monitorować, zarządzanie i wdrażanie zasobów w środowisku platformy Azure.  

Automatyzacji używa "elementów runbook", który korzysta z przepływów pracy programu Windows PowerShell (a właśnie regularne programu PowerShell) w obszarze obejmuje hello. Elementy Runbook mają toobe wykonywane bez interakcji z użytkownikiem. Przepływy pracy środowiska PowerShell umożliwia hello stan toobe skryptu, zapisać punkty kontrolne wzdłuż hello sposób. Następnie, jeśli wystąpi błąd, nie masz toostart skryptu od początku hello. Możesz uruchomić go ponownie na powitania ostatniego punktu kontrolnego. Zapisuje dużo pracy każdy możliwy błąd w trakcie toomake hello skryptu dojścia.

**Scenariusze automatyzacji**

Automatyzacja Azure jest dobry wybór ręcznego hello tooautomate, długotrwałe, podatne na błędy i często powtarzanych zadań na platformie Azure.

### <a name="api-management"></a>API Management
Tworzenie i publikowanie interfejsów programowania aplikacji (API) na powitania internet jest typowe tooapplications usług tooprovide sposób. Jeśli te usługi są resellable (na przykład dane o pogodzie), organizacji, można zezwolić osoby trzecie tooaccess te same usługi za opłatą. Podczas skalowania toomore partnerów, zazwyczaj będzie konieczne toooptimize i kontrola dostępu.  Niektórzy partnerzy mogą musi nawet hello danych w innym formacie.

Zarządzanie interfejsami API Azure ułatwia toopartners interfejsów API toopublish organizacji, pracowników i innych firm bezpiecznie i na dużą skalę. Zapewnia z innym punktem końcowym interfejsu API i działania jako proxy toocall hello rzeczywisty punkt końcowy, zapewniając usługi, takie jak buforowanie, przekształcania, ograniczanie dostępu kontroli i agregacji analytics.

**Scenariusze zarządzania interfejsu API**

Załóżmy, że Twoja firma ma wszystkie wymagane toocall tooa zapasowego Centrum obsługi tooget danych — na przykład firma wysyłania, która ma urządzeń w każdym ciężarówka na drodze hello urządzeń.  Na pewno hello firmy będą tooset się tootrack systemu jest własnych pojazdów więc można niezawodnie prognozowania i zaktualizuj czas dostawy. Umożliwia wiedzieć, ile pojazdów ma i odpowiednio zaplanować.  Każdy ciężarówka należy wywołuje tooa centralnej lokalizacji z jego pozycjonowanie i szybkość danych i prawdopodobnie inne urządzenie.

Klient hello Firma spedycyjna prawdopodobnie również korzystać z uzyskiwania tych pozycji danych.  powitania klienta można go użyć tooknow, jak daleko produkty mają tootravel, gdzie są zatrzymywane, ile ich płatności wzdłuż niektórych tras (jeśli są połączone z co ich płatnej tooship). Jeśli Firma spedycyjna hello już agreguje dane, wielu klientów może zwrócić dla niego.  Ale następnie hello Firma spedycyjna tooprovide sposób toogive klientom Witaj danych. Po zapewniają toocustomers dostęp, może nie mieć kontrolę nad jak często hello danych jest poddawany kwerendzie. Mają one tooprovide reguł dotyczących kto ma dostęp do danych. Wszystkie te reguły miałyby toobe wbudowanych w ich zewnętrznego interfejsu API. Jest to, gdzie ułatwiają zarządzanie interfejsami API.  

## <a name="identity-and-access"></a>Tożsamość i dostęp
Praca z tożsamości jest częścią większości aplikacji. Znajomość użytkownika umożliwia aplikacji zdecydować, jak powinna interakcji z użytkownikiem. Azure udostępnia tożsamość Śledź toohelp usług jak zintegrować ją z magazyny tożsamości, które mogą być już używany.

### <a name="active-directory"></a>Usługa Active Directory
Podobnie jak większość usług katalogowych usługi Azure Active Directory są przechowywane informacje o użytkownikach i organizacji hello, które należą do. Umożliwia użytkownikom zalogowanie się następnie dostarcza je z tokenami może ona tooapplications tooprove tożsamości. Umożliwia także synchronizację danych użytkownika z systemu Windows Server Active Directory uruchomiony lokalnie w sieci lokalnej. Mechanizmy hello i formatów danych używanych przez usługę Azure Active Directory nie są identyczne z tymi używanymi w usłudze Active Directory systemu Windows Server, funkcje hello, którą wykonuje są bardzo podobne.

Jego ważne toounderstand czy usługi Azure Active Directory jest przeznaczony głównie do użytku przez aplikacje w chmurze. Może służyć aplikacje działające na platformie Azure, na przykład lub na innych platformach chmury. Jest on również używany przez aplikacje w chmurze firmy Microsoft, takich jak zasoby w usłudze Office 365. Jeśli chcesz tooextend centrum danych w chmurze hello przy użyciu maszyn wirtualnych platformy Azure i siecią wirtualną platformy Azure, jednak usługi Azure Active Directory nie jest właściwie hello. Zamiast tego należy toorun Windows Server Active Directory w przypadku maszyn wirtualnych.

aplikacje toolet dostęp do informacji hello, które zawiera, Azure Active Directory oferuje usługi Azure Active Directory Graph wywołuje interfejs API RESTful. Ten interfejs API umożliwia aplikacji działających na dowolnym obiektów katalogu dostępu platformy i hello relacji między nimi.  Na przykład autoryzowanych aplikacji mogą używać tego interfejsu API toolearn o użytkownika, należy on do grupy hello i inne informacje. Aplikacje można również sprawdzić relacje między ich użytkowników społecznego wynajmowanie wykres ich działania więcej inteligentnie hello połączeń między osób.

Kolejna możliwość to usługi Azure Active Directory kontrola dostępu ułatwia tworzenie informacji o aplikacji tooaccept tożsamości z usługi Facebook, Google, Identyfikatora Windows Live i innych dostawców tożsamości popularnych. Zamiast konieczności hello aplikacji toounderstand hello danych w różnych formatach i protokołach używanych przez każdy z tych dostawców, kontrolę dostępu tłumaczy wszystkich z nich na jeden format wspólnej. Ponadto pozwala on usłudze aplikacji zaakceptować logowania z jednego lub więcej domen usługi Active Directory. Dostawcy, zapewniając aplikacji SaaS może na przykład użyć usługi Azure Active Directory kontroli dostępu toogive użytkowników w każdej aplikacji toohello rejestracji jednokrotnej jej klientów.

Usługi katalogowe są podstawa core dla lokalnych obliczeniowych. Nie powinien być zaskakująco, że są one również ważne w chmurze hello.

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
![Azure Multi-Factor Authentication](./media/fundamentals-introduction-to-azure/MFAIntroNew.png)   

*Rysunek: Usługi Multi-Factor Authentication udostępnia funkcję hello dla twojej aplikacji tooverify więcej niż jednej formy identyfikacji*

Ważne jest zawsze zabezpieczeń. Uwierzytelnianie wieloskładnikowe (MFA) pomaga upewnić się, że tylko użytkownicy sami dostęp do swoich kont. Uwierzytelnianie wieloskładnikowe (znanej także jako dwuskładnikowego uwierzytelniania lub "2FA") wymaga użytkownicy dostarczają dwa z tych trzech metod weryfikacji tożsamości użytkownika logowania i transakcji.

* Coś znasz (zwykle hasła)
* Coś (zaufanych urządzeń, który nie jest łatwo zduplikowany, takich jak telefon)
* Coś jest (biometria)

Tak więc po zalogowaniu użytkownik może wymagać ich tooalso weryfikację tożsamości z aplikacji mobilnej, połączenia telefonicznego lub wiadomości tekstowej w połączeniu z swoje hasło. Domyślnie program Azure Active Directory obsługuje hello przy użyciu hasła jako jedynej metody uwierzytelniania logowania użytkownika. Można użyć uwierzytelniania MFA, wraz z usługą Azure AD lub niestandardowych aplikacji i katalogów przy użyciu hello zestawu SDK usługi MFA. Umożliwia także go razem z aplikacjami lokalnymi za pomocą aplikacji serwer Multi-Factor Authentication.

**Scenariusze uwierzytelniania Wieloskładnikowego**

Ochrona logowania na kontach poufnych, takich jak nazwy bankowych logowania i gdzie nieautoryzowanego wejścia może mieć wysokiego finansowych lub prawa własności intelektualnej koszt dostęp do kodu źródłowego.   

## <a name="mobile"></a>Komórkowy
W przypadku tworzenia aplikacji dla urządzeń przenośnych, Azure może pomóc przechowywania danych w chmurze hello, uwierzytelniania użytkowników i wysyłać powiadomienia wypychane bez konieczności toowrite dużą ilość kodu niestandardowego.

Gdy na pewno można tworzyć hello wewnętrznej bazy danych dla aplikacji mobilnej przy użyciu aplikacji sieci Web, usługi w chmurze lub maszyny wirtualnej, może przeznaczyć znacznie mniej hello zapisu czasu podstawowych składników usługi za pomocą usług Azure.

### <a name="mobile-apps"></a>Mobile Apps
![Mobile Apps](./media/fundamentals-introduction-to-azure/MobileServicesIntroNew.png)

*Rysunek: Aplikacje mobilne udostępnia funkcje najczęściej wymagane przez aplikacje, które z urządzeń przenośnych.*

Aplikacje mobilne platformy Azure oferuje wiele przydatne funkcje, które mogą pomóc zaoszczędzić czas podczas tworzenia zaplecza aplikacji mobilnych. Umożliwia zarządzanie danymi przechowywanymi w bazie danych SQL i toodo prostego udostępniania. Kod po stronie serwera można łatwo opcje magazynu dodatkowe dane, takie jak magazyn obiektów blob lub bazy danych MongoDB. Mobile Apps zapewnia obsługę powiadomień, chociaż w niektórych przypadkach należy użyć usługi Notification Hubs zgodnie z opisem.  Usługa Hello ma również interfejs API REST wywołać tooget pracy aplikacji mobilnej. Mobile Apps udostępnia również możliwości hello tooauthenticate użytkowników za pośrednictwem firmy Microsoft i usługi Active Directory, a także innych dostawców tożsamości dobrze znany, takich jak Facebook, Twitter i Google.   

Można użyć innych usług Azure, takich jak usługi Service Bus i roli proces roboczy i połączyć systemów lokalnych tooon. Można nawet korzystać z 3 dodatki firm z hello dodatkowe funkcje tooprovide magazynu Azure (na przykład SendGrid do obsługi poczty e-mail).

Aplikacja Native client biblioteki dla systemu Android, iOS, HTML/JavaScript, Windows Phone i Sklep Windows był łatwiej toodevelop dla aplikacji na wszystkich głównych platform urządzeń przenośnych. Interfejs API REST umożliwia toouse danych usługi Mobile Services i funkcje uwierzytelniania przy użyciu aplikacji na różnych platformach. Jednej usługi mobilnej można utworzyć kopię wielu aplikacji klienta, więc zapewnia spójny interfejs użytkownika na urządzeniach.

Ponieważ Azure obsługuje już bardzo dużej skali, może obsługiwać ruch hello, wraz ze wzrostem więcej popularnych aplikacji.  Monitorowanie i rejestrowanie są obsługiwane toohelp rozwiązywania problemów i zarządzanie nimi wydajności.

### <a name="notification-hubs"></a>Notification Hubs
![NotificationHubs](./media/fundamentals-introduction-to-azure/NotificationHubsIntroNew.png)  

*Rysunek: Usługi Notification Hubs zapewnia funkcje najczęściej wymagane przez aplikacje, które z urządzeń przenośnych.*

Centra powiadomień można napisać kod toodo powiadomienia w usłudze Azure Mobile Apps, jest zoptymalizowany toobroadcast miliony powiadomień wypychanych spersonalizowanych w ciągu minut.  Nie masz tooworry o szczegóły, takie jak operator przenośnych ani producenta urządzenia. Możesz zastosować osoba lub miliony użytkowników przy użyciu jednego wywołania interfejsu API.

Centra powiadomień jest zaprojektowana toowork z dowolnego zaplecza. Możesz użyć usługi Azure Mobile Apps, niestandardowe wewnętrznej bazy danych w chmurze hello systemem u innego dostawcy lub wewnętrznej bazy danych lokalnych.

**Scenariusze dotyczące Centrum powiadomień** podczas pisania przenośnych gry, w którym odtwarzacze miał włącza toonotify player 2 może być konieczne jej Włącz Zakończono tego player 1. Jeśli jest potrzebna toodo, można użyć tylko aplikacje mobilne. Ale jeśli masz 100 000 użytkowników z gry i ma toosend razem, gdy hello lepszym rozwiązaniem jest bezpłatna oferta poufnych tooeveryone, centra powiadomień.

Możesz wysłać najważniejszych wiadomości sportowych zdarzenia i produktu anonsu powiadomienia toomillions użytkowników z niskim opóźnieniem. Przedsiębiorstwa mogą wyświetlać powiadomienia pracownikom o nowe poufnych łączności w czasie, takie jak potencjalnych klientach, pracownicy nie muszą tooconstantly Sprawdź adres e-mail lub innych toostay aplikacji informacji. Można również wysłać jednorazowe hasła wymagane do uwierzytelniania wieloskładnikowego.

## <a name="back-up"></a>Tworzenie kopii zapasowych
Każdy przedsiębiorstwa musi toobackup i przywracania danych. Można użyć Azure toobackup i przywrócić aplikacji w chmurze hello lub lokalnie. System Azure oferuje toohelp różne opcje w zależności od typu hello kopii zapasowej.

### <a name="site-recovery"></a>Site Recovery
Usługa Azure Site Recovery (dawniej Menedżera odzyskiwania funkcji Hyper-V) może pomóc chronić ważne aplikacje poprzez koordynowanie replikacji hello i odzyskiwania między lokacjami. Usługa Site Recovery zapewnia możliwość tooprotect aplikacje oparte na funkcji Hyper-v, VMWare lub ALTERNATYWNA nazwa podmiotu tooyour własnej lokacji dodatkowej, witryna dostawcy usług hostingowych tooa lub tooAzure i uniknąć hello wydatków i złożoności tworzenie i zarządzanie nią dodatkowej lokalizacji. Azure szyfruje dane i komunikacji i że masz opcję hello zbyt włączyć szyfrowanie danych w pozostałej.

Stale monitoruje kondycję hello usług i ułatwia automatyzację hello uporządkowany odzyskiwania usług w przypadku hello awarii lokacji, na powitania podstawowego centrum danych. Maszyny wirtualne mogą być wprowadzane w sposób zorkiestrowana toohelp przywracania usługi szybkie, nawet w przypadku złożonych wielowarstwowych obciążeń.

Usługa Site Recovery współpracuje z istniejących technologii, takich jak Hyper-V Replica, System Center i SQL Server AlwaysOn. Zapoznaj się z [Omówienie usługi Azure Site Recovery](site-recovery/site-recovery-overview.md) więcej szczegółów.

### <a name="azure-backup"></a>Azure Backup
![Azure Backup](./media/fundamentals-introduction-to-azure/AzureBackupIntroNew.png)  

*Rysunek: Kopia zapasowa Azure wykonuje kopię zapasową danych z lokalnych systemów Windows Server w chmurze hello.*  

Kopia zapasowa Azure wykonuje kopię zapasową danych lokalnych z serwerów z systemem Windows Server w chmurze hello. Kopie zapasowe można zarządzać bezpośrednio z hello narzędzia tworzenia kopii zapasowych w systemie Windows Server 2012, Windows Server 2012 Essentials lub System Center 2012 — Data Protection Manager. Alternatywnie można użyć specjalne agenta kopii zapasowej.

Dane jest bezpieczniejsza, ponieważ szyfrowane są kopie zapasowe przed transmisją i przechowywane zaszyfrowane na platformie Azure i chronione za pomocą certyfikatu, który należy przekazać. Usługa Hello używa hello znaleziono tej samej ochrony danych nadmiarowe i wysokiej dostępności w magazynie Azure.  Można tworzyć kopie zapasowe plików i folderów, zgodnie z ustalonym harmonogramem lub od razu, Uruchamianie pełnego lub przyrostowych kopii zapasowych. Po danych jest kopii zapasowej toohello chmury, autoryzowanych użytkowników można łatwo odzyskać serwer tooany kopii zapasowych. Zapewnia także zasady przechowywania danych można skonfigurować, kompresji danych oraz transferów danych ograniczanie, więc można zarządzać hello koszt toostore i transferu danych.

**Scenariusze dotyczące kopii zapasowej systemu Azure**

Jeśli możesz już przy użyciu systemu Windows Server lub programu System Center, fizycznych rozwiązania do tworzenia kopii zapasowych serwerów systemu plików, maszyn wirtualnych i baz danych programu SQL Server jest kopia zapasowa Azure.  Działa on z pliki zaszyfrowane, rozrzedzonych i skompresowane. Istnieją pewne ograniczenia, zaleca się [Sprawdź wymagania wstępne usługi Kopia zapasowa Azure hello](http://technet.microsoft.com/library/dn296608.aspx) pierwszy.

## <a name="messaging-and-integration"></a>Komunikaty i integracja
Niezależnie od tego, co wykonywanie operacji kod często wymaga toointeract z innego kodu.  W niektórych sytuacjach potrzebne jest podstawowej obsługi wiadomości w kolejce. W innych przypadkach wymagane są bardziej złożone interakcji. Platforma Azure udostępnia kilka różnych sposobów toosolve tych problemów. Rysunek 5 przedstawia możliwości hello.

### <a name="queues"></a>Kolejki
![Przekaźnik magistrali usług Azure](./media/fundamentals-introduction-to-azure/QueuesIntroNew.png)

*Rysunek: Kolejki Zezwalaj utracić sprzężenia między częściami aplikacji i ułatwić skalowanie.*  

Usługi kolejkowania wiadomości jest prosty: jedną aplikację umieszcza wiadomości w kolejce, a ten komunikat jest ostatecznie odczytu przez inną aplikację. Jeśli aplikacja wymaga tylko usługa prostego, kolejek Azure może być hello najlepszym rozwiązaniem.

Z powodu powitalne sposób hello Azure zwiększył się wraz z upływem czasu kolejek magazynu Azure i kolejek usługi Service Bus zapewniają podobne usługi kolejkowania wiadomości. Dlaczego warto toouse jeden nad hello innych przyczyn Hello zostały omówione w dokumencie dość techniczne hello [kolejek Azure i kolejek usługi Service Bus - porównywane i odróżniające](http://msdn.microsoft.com/library/azure/hh767287.aspx).  W wielu scenariuszach albo będzie działać.

**Scenariusze kolejki**

Witaj jednego z typowych użycie kolejek dzisiaj toolet wystąpienia roli sieci web komunikować się z wystąpienia roli proces roboczy w ramach tej samej aplikacji usługi w chmurze.

Na przykład załóżmy, że tworzenie Azure aplikacji do udostępniania wideo. Aplikacja Hello składa się z kodu PHP w roli sieci web, który umożliwia użytkownikom przekazywanie i filmy, wraz z rolą proces roboczy zaimplementowana w języku C# konwertująca przekazany wideo w różnych formatach.

Gdy wystąpienie roli sieci web pobiera nowe wideo z użytkownikiem, go można przechowywać hello wideo w obiekcie blob, a następnie wysłać komunikatu rola proces roboczy tooa za pośrednictwem kolejki podjęcie decyzji, gdzie toofind nowy wideo. Rola procesu roboczego wystąpienia it nie niezależnie od tego, które wiadomości powitania co zostanie następnie odczytu z kolejki hello i przeprowadzić hello wymagane tłumaczeń wideo w tle hello.

Struktury aplikacji w ten sposób pozwala na przetwarzanie asynchroniczne, a także udostępnia również hello tooscale łatwiejsze aplikacji, ponieważ hello liczbę wystąpień roli sieci web i wystąpień roli procesu roboczego można zmieniać niezależnie. Rozmiar kolejki hello służy również jako wyzwalacz tooscale hello liczbę roli proces roboczy w górę i w dół. Zbyt duże i dodać jedną rolę. Gdy otrzymuje niższe, pozwala zmniejszyć liczbę hello uruchomionych ról toosave pieniędzy.  

Można użyć tego samego wzorca między wiele różnych części aplikacji, nawet jeśli nie używają role sieci web i proces roboczy.  Umożliwia tooscale części powitania po obu stronach kolejki hello górę i w dół jako żądanie i wymaga czasu przetwarzania.

### <a name="service-bus"></a>Service Bus
Czy działają w chmurze hello, w centrum danych, na urządzeniu przenośnym lub w innym miejscu, aplikacje muszą toointeract. Celem Hello Azure Service Bus jest toolet aplikacje niemal dowolnego miejsca wymiany danych.

W dodatku toohello kolejki (mapowanie) opisana wcześniej usługi Service Bus udostępnia tooother metody komunikacji.

#### <a name="service-bus-relay"></a>Service Bus Relay
![Przekaźnik magistrali usług Azure](./media/fundamentals-introduction-to-azure/ServiceBusRelayIntroNew.png)

*Rysunek: Service Bus Relay umożliwia komunikację między aplikacjami na różnych stronach zapory.*

Usługi Service Bus umożliwia bezpośrednią komunikację za pośrednictwem jej usługi przekazywania danych, zapewniając toointeract bezpieczny sposób za pośrednictwem zapór. Przekaźników usługi Service Bus włączyć toocommunicate aplikacji, wymiana wiadomości za pośrednictwem punktu końcowego hostowanych w chmurze hello, a nie lokalnie.

**Scenariusze przekaźnik magistrali usług**

Aplikacje, które komunikują się za pośrednictwem usługi Service Bus może być Azure aplikacji lub oprogramowania uruchomionego na inne platformy w chmurze. Może to być również aplikacje działające poza hello chmury, jednak. Na przykład traktować linii lotniczych, który implementuje usługi rezerwacji w komputerach wewnątrz własnego centrum danych. Witaj linii lotniczych musi tooexpose tych klientów toomany usług, w tym kiosków odprawy na lotniskach, rezerwacji agenta terminale i mogą być również klientów telefonów. Można w nim korzystać toodo usługi Service Bus to tworzenie luźno powiązanych interakcji między hello różnych aplikacji.

#### <a name="service-bus-topics-and-subscriptions"></a>Tematy i subskrypcje usługi Service Bus
![Tematów usługi Azure Service Bus](./media/fundamentals-introduction-to-azure/ServiceBusTopicsSubsIntroNew.png)   
 *Rysunek: Tematów usługi Service Bus umożliwia wiele komunikatów toopost aplikacje i inne komunikaty tooreceive toosubscribe aplikacje, które spełniają określone kryteria.*

Usługa Service Bus udostępnia mechanizm publikowania i subskrybowania o nazwie tematów i subskrypcji. Publish-subscribe aplikacja może wysłać wiadomości tooa tematu, podczas gdy inne aplikacje można tworzyć subskrypcje tematu toothis. Dzięki temu jeden do wielu komunikacji między zestaw aplikacji, dzięki czemu hello tę samą wiadomość jej odczytanie przez wielu adresatów.

**Scenariusze subskrypcje i tematów usługi Service Bus**

W dowolnym momencie konfigurowania których istnieje wiele komunikatów, które są wszystkie ważne, ale różne systemy klienckie potrzebują tylko toolisten toodiffering podzbiór tych komunikacji, temat magistrali usług i subskrypcji są dobrym rozwiązaniem.

### <a name="biztalk-services"></a>BizTalk Services
![Usługi BizTalk Services](./media/fundamentals-introduction-to-azure/BizTalkServicesIntroNew.png)   
 *Rysunek: Usługi BizTalk Services udostępnia formaty wiadomości powitania możliwości tootransform XML w chmurze hello.*

Czasami należy połączyć z systemów, które komunikują się przy użyciu różnych formatach obsługi wiadomości. Bardzo często schematy innej bazy danych toohave biznesowych i XML wiadomości formatów, nawet wtedy, gdy common standard jest dostępna. Zamiast zapisu partii niestandardowego kodu toointegrate lokalnymi BizTalk Server można użyć różnych systemów.  Usługi BizTalk Azure udostępnia hello tego samego typu usługi, ale w chmurze hello. Możesz zapłacić tylko co używane i nie martwić się o skali, tak jak miałoby tooon lokalnych.

**Scenariusze usługi BizTalk**

Interakcje między firmami (B2B) zwykle wymagają tego typu tłumaczenia.  Na przykład firma tworzenia potrzeb samolotów tooorder części z niego jest różnych dostawców części. Będzie mieć wielu dostawców części.  Zamówień powinny być automatyczne toogo bezpośrednio z hello samolotowy konstruktorów systemów do hello dostawców systemów.  Żadna firm chce toochange ich core systemów i formaty wiadomości i jest bardzo mało prawdopodobne, że te formaty są hello takie same. Usługi BizTalk Services może zająć wiadomości i tłumaczenia hello nowe formaty w obu kierunkach. Dostawca samolotowy albo hello można hello tootranslate pracy lub hello różnych dostawców może w zależności od tego, kto chce więcej hello i kontroli ilości tłumaczenia potrzebne.     

## <a name="compute-assistance"></a>Obliczenia bazy danych pomocy
Platforma Azure udostępnia pomocy dla usług, które nie są toorun cały czas hello.  

### <a name="scheduler"></a>Scheduler
![Azure Scheduler](./media/fundamentals-introduction-to-azure/SchedulerIntroNew.png)   
*Rysunek: Harmonogram Azure udostępnia tooschedule sposób zadań w określonym czasie o określony czas.*

Aplikacje muszą czasami tylko toorun w określonym czasie. Na platformie Azure można zapisać pieniędzy tego typu aplikacji, zamiast czekać po prostu działanie 24 x 7 oczekiwanie na tooprocess danych aplikacji. Harmonogram systemu Azure umożliwia tooschedule aplikacji nie powinna działać na podstawie interwału czasu lub kalendarza. Jest niezawodne i sprawdź, czy proces działa nawet w przypadku awarii Centrum sieci, komputera i danych. Możesz użyć toomanage interfejsu API REST harmonogramu hello te akcje.

W przypadku zaplanowanego alarm harmonogramu wysyła HTTP lub HTTPS wiadomości tooa określonego punktu końcowego lub można umieścić wiadomości w kolejce magazynu.  Warto toohave aplikacji ma dostępnym punkcie końcowym lub została ona monitorowania kolejki magazynu. Następnie po otrzymuje wiadomość hello, można wykonać akcji, niezależnie od jej zaplanowano do.

**Scenariusze harmonogramu**

* Cykliczne akcji aplikacji: na przykład usługa może okresowo Pobierz dane z serwisem twitter i zebrać dane hello w regularnych źródła danych.
* Konserwacja: Dziennik przetwarzania lub oczyszczeniem, wykonywanie kopii zapasowych i innych sporadycznie Planowanie zadań.
* Zadania, które będą uruchamiane w nocy.
* Zadania aplikacji sieci Web, takie jak codzienne oczyszczania dzienników kopii zapasowych, a inne zadania konserwacji. Administrator może wybrać toobackup swojej bazy danych na 1: 00 każdego dnia dla hello dalej 9 miesięcy, na przykład.

Hello harmonogramu API umożliwia toocreate, zaktualizować usunąć, wyświetlać i programowe zarządzanie kolekcje zadań i zaplanowanych zadań.

## <a name="performance"></a>Wydajność
Wydajność zawsze jest ważne dla aplikacji. Aplikacje zazwyczaj tooaccess samodzielnego hello tych samych danych. Jednym ze sposobów tooimprove wydajności jest tookeep kopii tej aplikacji danych bliżej toohello, minimalizując hello czasu potrzebnego tooretrieve go. Platforma Azure oferuje różne usługi dla tej czynności.

### <a name="azure-caching"></a>Buforowanie Azure
![Buforowanie Azure](./media/fundamentals-introduction-to-azure/AzureCacheIntroNew.png)   
 **Rysunek: Aplikacja Azure może buforować dane w pamięci i nawet podzielić go na wiele ról procesów roboczych**

Uzyskiwanie dostępu do danych przechowywanych w żadnym z platformy Azure, zarządzanie danymi usługi SQL Database, tabel lub obiekty BLOB — jest dość szybki. Jeszcze dostęp do danych przechowywanych w pamięci jest szybszy. W związku z tym przechowywania kopii rzadziej używanych danych w pamięci może poprawić wydajność aplikacji. Możesz użyć toodo buforowanie w pamięci systemu Azure.

Aplikacji usługi w chmurze mogą przechowywać dane w pamięci podręcznej, a następnie pobrać go bezpośrednio, bez konieczności tooaccess magazynu trwałego. Witaj w pamięci podręcznej mogą być obsługiwane się, że toocaching wyłącznie wewnątrz aplikacji na maszynach wirtualnych lub udostępniane przez maszyny wirtualne w wersji dedykowanej. W obu przypadkach mogą być dystrybuowane hello pamięci podręcznej, z danymi hello zawiera rozpowszechniania między wieloma maszynami wirtualnymi w centrum danych Azure.

Platforma Azure ma szereg różnych pamięci podręcznej technologie, które mają przesunięte wraz z upływem czasu. W kolejności hello zostały wprowadzone, jest udostępnionym, w roli, zarządzane i pamięci podręcznej Redis. buforowanie Hello udostępnionych to technologia starsze i nie należy tworzyć nowych wdrożeń z nim. Witaj zarządzane pamięć podręczna ma hello te same funkcje hello w roli pamięci podręcznej, ale jako zarządzana usługa poza hello portalu zarządzania Azure. pamięć podręczna Redis Hello jest w wersji zapoznawczej. Implementacja Redis Hello ma hello największą liczbę funkcji i jest zalecana w przypadku pisanie nowego kodu buforowania.

**Scenariusze pamięć podręczna Azure**

Aplikacja, która odczytuje wielokrotnie katalog produktów mogą korzystać z tego rodzaju buforowania, na przykład od danych hello go wymaga staną się dostępne szybciej. Technologia Hello obsługuje również blokowania, dzięki czemu on być używany z odczytu/zapisu, a także danych tylko do odczytu. I aplikacji programu ASP.NET można użyć danych sesji toostore usługi hello właśnie zmianą konfiguracji.

### <a name="content-delivery-network"></a>Content Delivery Network
![Usługa Azure CDN](./media/fundamentals-introduction-to-azure/CDNIntroNew.png)   
 **Rysunek: Mogą być buforowane kopie obiektu blob w lokacjach wokół hello world.**

Załóżmy, że należy toostore danych obiektów blob, której będą mieli dostęp przez użytkowników wokół hello world. Może być to wideo hello najnowsze świata dopasowania, na przykład aktualizacje sterowników lub popularnych Książka elektroniczna. Przechowywanie kopii danych hello w wielu centrach danych platformy Azure może pomóc, ale w przypadku wielu użytkowników, prawdopodobnie nie jest wystarczająco dużo. Aby zwiększyć wydajność można użyć hello Azure CDN.

Witaj CDN ma dziesiątki witryn wokół Witaj świecie może przechowywania kopii obiekty BLOB platformy Azure. Witaj pierwszego dostępu użytkownika w niektórych części Witaj świecie do określonego obiektu blob, hello informacje o nim zostaną skopiowane z centrum danych Azure do lokalnego magazynu w sieci CDN w tej lokalizacji geograficznej. Po to, użyje dostęp z części hello world hello kopii obiektu blob w pamięci podręcznej w sieci CDN hello — nie potrzebują toogo wszystkie toohello sposób hello najbliższego centrum danych Azure. wynik Hello jest szybszy dostęp toofrequently dostęp do danych przez użytkowników w dowolnym miejscu hello world.

**Scenariusze CDN**

Jest typowe toouse CDN z usługi Media Services toodeliver wideo na całym świecie. Wideo jest zwykle duży i wymagają dużej przepustowości.  Usługa Media Services jest omówiono w innym miejscu na tej stronie.

## <a name="big-data-and-big-compute"></a>Dane big Data i duży obliczeń
### <a name="hdinsight-hadoop"></a>Usługa HDInsight (Hadoop)
![HDInsight](./media/fundamentals-introduction-to-azure/HDInsightIntroNew.png)   
 **Rysunek: HDInsight ułatwiające hello zbiorczego przetwarzania dużych ilości danych**

Przez wiele lat zbiorczego hello analizy danych zostało wykonane w relacyjnej bazie danych przechowywanych w magazynie danych skompilowanej za pomocą relacyjne systemu DBMS. Tego rodzaju analiz biznesowych jest nadal ważny, i będzie toocome dużo czasu. Ale co zrobić, jeśli mają tooanalyze dane hello jest tak duży, że relacyjnych baz danych po prostu nie może obsłużyć go? I Załóżmy, że hello danych nie jest relacyjna? Może to być dzienniki serwera w centrum danych, na przykład dane historyczne zdarzenia z czujników lub coś innego. W takich sytuacjach należy określane jako problem danych big data. Innym rozwiązaniem jest konieczne.

Technologia dominującą Hello o analizy danych big data jest Hadoop. Apache Otwórz projekt źródłowy, ta technologia przechowuje dane przy użyciu hello systemu Distributed plików Hadoop (HDFS), a następnie umożliwia deweloperom tworzenie tooanalyze zadań MapReduce tych danych. System plików HDFS rozprzestrzenia dane na wielu serwerach, a następnie przetworzenie fragmentów uruchamia zadania MapReduce hello na każdej z nich, dzięki czemu dane big data hello równolegle.

HDInsight to nazwa hello hello Azure usługa Apache Hadoop. HDInsight umożliwia HDFS przechowywanie danych w klastrze hello i rozpowszechniają wiele maszyn wirtualnych. Rozprzestrzenia się również logikę hello zadania MapReduce na tych maszynach wirtualnych. Tak jak z lokalną platformą Hadoop, dane są przetworzonych lokalnie hello logikę i dane hello działa na znajdują się w tej samej maszyny Wirtualnej hello- i równolegle w celu zapewnienia lepszej wydajności. HDInsight można przechowywać dane w Azure magazynu magazynu (ASV), który używa obiektów blob.  Użycie ASV umożliwia toosave pieniądze, ponieważ usunięcie z klastrem usługi HDInsight nieużywane, ale nadal przechowywanie danych w chmurze hello.

HDinsight obsługuje inne składniki ekosystemu Hadoop hello także, w tym Hive i Pig. Firma Microsoft opracowała również składników, dzięki którym łatwiej toowork z dane utworzone przez usługi HDInsight przy użyciu tradycyjnych narzędzi do analizy Biznesowej, takich jak karty HiveODBC hello i Eksplorator danych, który pracy przy użyciu programu Excel.

### <a name="high-performance-computing-big-compute"></a>Wysokiej wydajności przetwarzania danych (Big obliczeniowe)
Jedną z najbardziej atrakcyjne hello toouse sposoby platformy w chmurze jest toorun wysokiej wydajności (HPC) i innych aplikacjach "Obliczeniowe Big". Przykłady specjalne engineering toouse aplikacje utworzone hello standardowy komunikat interfejsu (Passing Interface), a także tak zwane embarrassingly równoległych aplikacje, takie modele finansowych ryzyka.

właśnie Hello Big obliczeniowe wykonuje kod na wielu komputerach w hello tym samym czasie. Na platformie Azure oznacza to, jednocześnie działa wiele maszyn wirtualnych wszystkie pracy w równoległych toosolve pewien problem. Wymaga to pewnych sposób tooresources i tooschedule aplikacji, np. toodistribute pracy w tych wystąpieniach. Bezpłatne firmy Microsoft HPC Pack i innych rozwiązań klastra obliczeniowego mogą wykonywać również w Azure, korzystając z usług platformy Azure obliczeniowych i infrastruktury tooadd pojemności na żądanie tooan lokalnymi klaster obliczeniowy lub uruchamiania aplikacji Big obliczeniowe całkowicie w hello Chmura.

Platforma Azure udostępnia zakresu wirtualna rozmiary wystąpienia o różnych konfiguracjach rdzeni Procesora, pamięci, pojemność dysku i inne wymagania hello toomeet właściwości z różnych aplikacji. Witaj ostatnio wprowadzone A8 i A9 wystąpień pracy oraz dla wielu obliczeniowe intensywnych obciążeń i aplikacje równoległe MPI w szczególności, ponieważ mają one dużej szybkości, wielordzeniowych procesorów i dużych ilości pamięci. W niektórych konfiguracjach wystąpień hello korzystać z aplikacji o małym opóźnieniu i dużej przepustowości sieci w chmurze hello, która obejmuje technologii dostępu do (pamięci RDMA) zdalnego pamięci z maksymalną wydajnością aplikacje równoległe MPI.

Azure oferuje również Big obliczeniowe deweloperzy aplikacji i partnerów pełny zestaw obliczeniowa, usług, opcji architektury i narzędzia deweloperskie. Azure obsługuje niestandardowe przepływy Big obliczeniowe obejmujące danych specjalistyczne przepływów pracy i zadania i planowania wzorców, które mogą być skalowane toothousands z zadań obliczeniowe rdzeni.

## <a name="media"></a>Multimedia
![Usługi Azure Media Services](./media/fundamentals-introduction-to-azure/MediaServicesIntroNew.png)   
 **Rysunek: Usługi Media Services to platforma dla aplikacji, które zapewniają wideo i innych tooclients nośnika wokół hello world.**

Film wideo stanowi dużą część ruchu internetowego dzisiaj, i wartość procentowa będzie jeszcze większym jutro. Jeszcze dostarczanie wideo w sieci web hello jest proste. Istnieje wiele zmiennych, takich jak hello kodowania algorytmu i hello wyświetlenia rozdzielczości ekranu hello użytkownika. Wideo zwykle również seria toohave popytu, takich jak kolekcji nocy sobota, gdy wielu użytkownikom zdecydować, że chciałby toowatch filmów w trybie online.

Podana jego popularne, jest sejfie trafienia, będzie można utworzyć wideo użyj wiele nowych aplikacji. Jeszcze wszystkich z nich będzie konieczne toosolve niektóre z hello tego samego problemów oraz zwiększeniem każdej z nich rozwiązać te problemy we własnym ma sensu. Lepszym rozwiązaniem jest toocreate platforma, która udostępnia typowe rozwiązania dla wielu toouse aplikacji. I tworzenia tej platformy w chmurze hello niektóre zalety Wyczyść. Może być szeroko dostępne w oparciu o płatności obejmujące i może również obsługiwać hello zmienności żądanie, które aplikacje wideo często stają przed.

Usługa Azure Media Services rozwiązuje ten problem. Zapewnia zestaw składników chmury, które ułatwić życia dla osób, tworzenie i uruchamianie aplikacji przy użyciu nośnika wideo i innych.

Jak pokazano na rysunku hello, Media Services udostępnia zestaw składników dla aplikacji, które współpracują z wideo i innych nośników. Na przykład zawiera nośników pozyskiwania składnika tooupload wideo do usługi Media Services (gdy jest ona przechowywana w obiektach blob Azure), kodowania składnik, który obsługuje różne formaty wideo i audio, składnik ochrony zawartości, który umożliwia zarządzanie prawami cyfrowymi składnik do wstawiania reklam do strumienia wideo, składniki do przesyłania strumieniowego i inne. Partnerzy firmy Microsoft można również Podaj składniki platformy hello, a następnie program Microsoft dystrybucji tych składników i fakturowania w ich imieniu.

Na platformie Azure lub w innym miejscu, można uruchomić aplikacji, które używają tej platformy. Na przykład aplikacja dla domu wideo produkcji zezwolić użytkownikom na jego przekazywanie usług tooMedia wideo, następnie go przetworzyć na różne sposoby. Alternatywnie usługi opartej na chmurze zarządzanie zawartością działających na platformie Azure mogą polegać na tooprocess Media Services i dystrybuować wideo. Wszędzie tam, gdzie działa i tak jest, każda aplikacja wybierze składniki, które wymaga toouse dostępu do nich za pośrednictwem interfejsów RESTful.

toodistribute co generuje, aplikacja może użyć hello Azure CDN innego CDN lub po prostu wyślij bezpośrednio bits toousers. Jednak pobiera, wideo, utworzone za pomocą usługi Media Services może być zużyte przez różnych systemów klienckich, w tym systemu Windows, Macintosh HTML 5, iOS, Android, Windows Phone, Flash i Silverlight. Celem Hello jest toomake go łatwiejsze toocreate nowoczesnych aplikacji.

**Odwołania**

Aby uzyskać bardziej czytelny i jak działa usługa Media Services, Pobierz hello [Azure Media Services plakat][Azure Media Services Poster].

## <a name="commerce"></a>Handel
wzrost Hello oprogramowanie jako usługa jest przekształcanie, jak możemy utworzyć aplikacje. Jest także przekształcanie, jak firma Microsoft sprzedać aplikacji. Ponieważ aplikacja SaaS znajduje się w chmurze hello, warto wygląda jego potencjalnych klientów dla rozwiązania w trybie online. I zmiana ta dotyczy toodata, a także tooapplications. Dlaczego osób nie powinien wyglądać toohello chmury dla zestawów danych dostępnych na rynku? Microsoft adresów oba te problemy z hello [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/).

![Azure Commerce](./media/fundamentals-introduction-to-azure/CommerceIntroNew.png)   
 **Rysunek: Witrynę Azure Marketplace i Magazyn Azure można znaleźć i kupowanie aplikacjami platformy Azure i komercyjnych zestawów danych i ich używać jako części aplikacji Azure.**

Witaj różnicę między dwoma hello jest Marketplace znajduje się poza hello portalu zarządzania Azure, że magazyn hello są dostępne z wewnątrz hello portalu. Potencjalni klienci mogą szukać toofind Azure aplikacji, które własnych potrzeb. Klientów można wyszukiwać komercyjnych zestawów danych oraz, w tym danych demograficznych, danych finansowych, dane geograficzne i. Gdy znajdą coś one, takich jak ich do niego dostęp z dostawcą hello bezpośrednio za pośrednictwem hello Marketplace lub lokalizacji magazynu sieci web lub w niektórych przypadkach z hello portalu zarządzania. Aplikacje mogą również używać hello API wyszukiwania usługi Bing za pośrednictwem hello Marketplace, zapewniając im dostępu toohello wyniki wyszukiwania w sieci web.

**Scenariusze Commerce**

SendGrid to aplikacja w hello magazynu Azure, który pozwala toosend wiadomości e-mail. Zapewnia dodatkowe funkcje takie jak niezawodnego dostarczania i statystyki.  Można kupić tej aplikacji i powiązane usługi zamiast samodzielnie spróbuj toobuild tej infrastruktury.  

## <a name="getting-started"></a>Wprowadzenie
Teraz, gdy masz hello duży obraz powitania następnym krokiem jest toowrite pierwszej aplikacji platformy Azure. Wybierz język, [uzyskać hello SDK odpowiednie](/downloads/)i przejdź na jej. Chmury obliczeniowej jest nowym domyślnym hello — Rozpocznij teraz.

[Azure Media Services Poster]: http://azure.microsoft.com/documentation/infographics/media-services/
