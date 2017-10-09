---
title: "aaaHow toocreate, zarządzania i usuwania konta magazynu w portalu Azure hello | Dokumentacja firmy Microsoft"
description: "Utwórz nowe konto magazynu, zarządzanie kluczami dostępu do konta lub usuwania konta magazynu w hello portalu Azure. Więcej informacji na temat kont magazynu (warstwy Standardowa i Premium)."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 87c37da0-6cc6-4d88-a330-ef2896a1531d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
f1_keywords: sql13.swb.windowsazurestorage.connect.f1
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 3a2a07c4131fbe594c7007f59950bf94339809fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Informacje o kontach magazynu Azure
[!INCLUDE [storage-selector-portal-create-storage-account](../../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>Omówienie
Konto usługi Azure storage zapewnia toostore unikatową przestrzeń nazw i dostęp do obiektów danych usługi Azure Storage. Wszystkie obiekty w koncie magazynu są rozliczane wspólnie jako grupa. Domyślnie dane hello na Twoim koncie są dostępne tooyou tylko właściciel konta hello.

[!INCLUDE [storage-account-types-include](../../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a>Rozliczanie konta usługi Storage
[!INCLUDE [storage-account-billing-include](../../../includes/storage-account-billing-include.md)]

> [!NOTE]
> Podczas tworzenia maszyny wirtualnej platformy Azure, konto magazynu jest tworzony automatycznie w lokalizacji wdrożenia hello Jeśli nie masz już konto magazynu w tej lokalizacji. Dlatego nie jest konieczne toofollow hello kroki toocreate konto magazynu dla dysków maszyny wirtualnej. Nazwa konta magazynu Hello będzie opierać się na powitania nazwę maszyny wirtualnej. Zobacz hello [dokumentacji usługi Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/) więcej szczegółów.
> 
> 

## <a name="storage-account-endpoints"></a>Punkty końcowe konta usługi Storage
Każdy obiekt, który jest przechowywany w usłudze Azure Storage, ma unikatowy adres URL. Formularze nazwy konta magazynu Hello hello poddomenę tego adresu. Witaj kombinacja nazw poddomeny i domeny, co jest tooeach określonej usługi, formularzy *punktu końcowego* dla konta magazynu.

Na przykład, jeśli nosi nazwę konta magazynu *mojekontomagazynu*, a następnie hello domyślne punkty końcowe konta magazynu są:

* Usługa Blob: http://*mojekontomagazynu*.blob.core.windows.net
* Usługa Table service: http://*mojekontomagazynu*.table.core.windows.net
* Usługa kolejki: http://*mojekontomagazynu*.queue.core.windows.net
* Usługa plików http://*mojekontomagazynu*.file.core.windows.net

> [!NOTE]
> Konto magazynu obiektów Blob przedstawia tylko punkt końcowy usługi Blob hello.
> 
> 

adres URL Hello dla uzyskiwania dostępu do obiektu na koncie magazynu jest tworzony przez dodanie lokalizacji obiektu hello końcowego toohello konta magazynu hello. Przykładowo adres obiektu Blob może mieć następujący format: http://*mojekontomagazynu*.blob.core.windows.net/*mojkontener*/*mojblob*.

Można również skonfigurować toouse nazwy domeny niestandardowej z kontem magazynu. Aby uzyskać więcej informacji, zobacz [Konfigurowanie niestandardowej nazwy domeny dla punktu końcowego usługi Blob Storage](../blobs/storage-custom-domain-name.md). Można ją także skonfigurować przy użyciu programu PowerShell. Aby uzyskać więcej informacji, zobacz hello [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) polecenia cmdlet.  


## <a name="create-a-storage-account"></a>Tworzenie konta magazynu
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum hello wybierz **nowy** -> **magazynu** -> **konta magazynu**.
3. Wprowadź nazwę konta magazynu. Zobacz [punkty końcowe konta magazynu](#storage-account-endpoints) dla szczegółowych informacji o jak nazwa konta magazynu hello będą używane tooaddress obiektów w usłudze Azure Storage.
   
   > [!NOTE]
   > Nazwy kont usługi Magazyn muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery.
   > 
   > Nazwa konta magazynu musi być unikatowa w obrębie platformy Azure. Hello Azure portal poinformuje, czy hello nazwy konta magazynu, którą wybierzesz jest już używany.
   > 
   > 
4. Określ toobe modelu wdrażania hello używane: **Resource Manager** lub **klasycznego**. **Menedżer zasobów** hello zaleca modelu wdrażania. Aby uzyskać więcej informacji, zobacz [Understanding Resource Manager deployment and classic deployment](../../azure-resource-manager/resource-manager-deployment-model.md) (Omówienie wdrożenia z usługą Resource Manager oraz wdrożenia klasycznego).
   
   > [!NOTE]
   > Konta magazynu obiektów blob można tworzyć tylko przy użyciu modelu wdrażania usługi Resource Manager hello.

5. Wybierz typ konta magazynu hello: **ogólnego przeznaczenia** lub **magazynu obiektów Blob**. **Ogólnego przeznaczenia** jest domyślnym hello.
   
    Jeśli **ogólnego przeznaczenia** została wybrana, a następnie określ warstwę wydajności hello: **standardowe** lub **Premium**. Domyślnie Hello **standardowe**. Więcej szczegółów na kontach magazynu standard i premium, zobacz [tooMicrosoft wprowadzenie usługi Azure Storage](storage-introduction.md) i [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](storage-premium-storage.md).
   
    Jeśli **magazynu obiektów Blob** została wybrana, a następnie określ warstwę dostępu hello: **gorąca** lub **chłodnych**. Domyślnie Hello **gorąca**. Zobacz temat [Azure Blob Storage: Cool and Hot tiers](../blobs/storage-blob-storage-tiers.md) (Azure Blob Storage: warstwy Chłodna i Gorąca), aby uzyskać więcej szczegółów.
6. Wybierz opcję replikacji powitania dla konta magazynu hello: **LRS**, **GRS**, **RA-GRS**, lub **ZRS**. Domyślnie Hello **RA-GRS**. Aby uzyskać więcej szczegółów na temat opcji replikacji usługi Azure Storage, zobacz [Replikacja usługi Azure Storage](storage-redundancy.md).
7. Wybierz subskrypcję hello, w której ma zostać toocreate hello nowe konto magazynu.
8. Określ nową grupę zasobów lub wybierz istniejącą grupę zasobów. Więcej informacji na temat grup zasobów znajduje się w temacie [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).
9. Wybierz lokalizację geograficzną hello konta magazynu. Aby uzyskać więcej informacji na temat dostępności usług w poszczególnych regionach, zobacz temat [Regiony świadczenia usługi Azure](https://azure.microsoft.com/regions/#services).
10. Kliknij przycisk **Utwórz** konta magazynu hello toocreate.

## <a name="manage-your-storage-account"></a>Zarządzanie kontem magazynu
### <a name="change-your-account-configuration"></a>Zmiana konfiguracji konta
Po utworzeniu konta magazynu, można zmodyfikować jego konfigurację, np. zmiana hello opcję replikacji używaną wobec konta hello lub zmieniania hello warstwy dostępu dla konta magazynu obiektów Blob. W hello [portalu Azure](https://portal.azure.com), przejdź do konta magazynu tooyour, Znajdź i kliknij przycisk **konfiguracji** w obszarze **ustawienia** tooview i/lub zmiana konfiguracji konta hello.

> [!NOTE]
> W zależności od hello warstwy wydajności wybranej podczas tworzenia konta magazynu hello niektóre opcje replikacji mogą nie być dostępne.
> 
> 

Zmiana opcji replikacji hello spowoduje zmianę cen.. Aby uzyskać więcej informacji, zobacz stronę [Cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/).

Dla obiektów Blob, który może pociągnąć za sobą kont magazynu Zmiana warstwy dostępu hello opłat za hello zmianę dodatkowo toochanging cen. Zobacz hello [konta usługi Blob storage — cennik i rozliczenia](../blobs/storage-blob-storage-tiers.md#pricing-and-billing) więcej szczegółów.

### <a name="manage-your-storage-access-keys"></a>Zarządzanie kluczami dostępu do magazynu
Podczas tworzenia konta magazynu Azure generuje dwa klucze dostępu do magazynu 512-bitowe, które są używane do uwierzytelniania podczas uzyskiwania dostępu do konta magazynu hello. Zapewniając dwa klucze dostępu do magazynu Azure umożliwia tooregenerate hello kluczy bez przeszkód tooyour magazynu usługi i usługa toothat dostępu.

> [!NOTE]
> Nie zaleca się udostępniania kluczy dostępu do magazynu innym osobom. toopermit dostęp do zasobów toostorage bez przekazywania kluczy dostępu, można użyć *sygnatury dostępu współdzielonego*. Sygnatury dostępu współdzielonego zapewnia tooa dostępu do zasobów na koncie przez określony czas, który należy zdefiniować i uprawnieniami hello przez użytkownika. Zobacz [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Używanie sygnatur dostępu współdzielonego), aby uzyskać więcej informacji.
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a>Wyświetlanie i kopiowanie kluczy dostępu do magazynu
W hello [portalu Azure](https://portal.azure.com)Przejdź tooyour konta magazynu, kliknij przycisk **wszystkie ustawienia** , a następnie kliknij przycisk **klucze dostępu** tooview, kopiowanie i ponowne generowanie kluczy dostępu do Twojego konta. Witaj **klucze dostępu** blok zawiera również wstępnie skonfigurowane parametry połączenia wykorzystujące Twoje klucze podstawowe i pomocnicze skopiowania toouse aplikacji.

#### <a name="regenerate-storage-access-keys"></a>Ponowne generowanie kluczy dostępu do magazynu
Firma Microsoft zaleca zmianę kluczy dostępu hello magazynu tooyour okresowo konta zachowuje toohelp bezpiecznego połączenia z magazynem. Dwa klucze dostępu są przypisane, dzięki czemu można zachować konta magazynu toohello połączeń przy użyciu jednego klucza dostępu, jednocześnie ponownie generując hello drugi klucz dostępu.

> [!WARNING]
> Trwa ponowne generowanie kluczy dostępu może mieć wpływ na usługi platformy Azure, jak również własne aplikacje, które są zależne od konta magazynu hello. Wszystkich klientów, którzy używają konta magazynu hello hello dostępu tooaccess klucza musi być zaktualizowany toouse hello nowego klucza.
> 
> 

**Usługa Media services** — Jeśli masz usługi media services, które są zależne od konta magazynu, musisz ponownie zsynchronizować klucze dostępu hello z usługą multimediów po ponownym wygenerowaniu kluczy hello.

**Aplikacje** — Jeśli masz aplikacje sieci web lub użyj tego konta magazynu hello usług w chmurze, utracisz połączenia hello ponownego generowania kluczy, chyba że wdrożysz klucze.

**Eksploratory usługi Storage** — Jeśli używasz dowolnej [aplikacji Eksploratora magazynu](storage-explorers.md), prawdopodobnie zajdzie klucza magazynu hello tooupdate używane przez te aplikacje.

Oto proces związany z rotacją kluczy dostępu do magazynu hello:

1. Zaktualizuj parametry połączenia hello w Twojej aplikacji kod tooreference hello pomocniczy klucz dostępu konta magazynu hello.
2. Wygeneruj ponownie hello podstawowy klucz dostępu dla konta magazynu. Na powitania **klucze dostępu** bloku, kliknij przycisk **Generuj ponownie klucz1**, a następnie kliknij przycisk **tak** tooconfirm, które mają toogenerate nowy klucz.
3. Zaktualizuj parametry połączenia hello w Twojej kodu tooreference hello nowego podstawowego klucza dostępu.
4. Pomocniczy dostęp regenerate hello klucza w hello sam sposób.

## <a name="delete-a-storage-account"></a>Usuwanie konta magazynu
tooremove konta magazynu, które są już używane, przejdź toohello konta magazynu w hello [portalu Azure](https://portal.azure.com)i kliknij przycisk **usunąć**. Usunięcie konta magazynu powoduje usunięcie całego konta hello, w tym wszystkie dane na koncie hello.

> [!WARNING]
> Jest nie jest możliwe toorestore usuniętego konta magazynu lub pobrać żadnej hello zawartość, która zawiera go przed usunięciem. Należy się tooback zapasową wszystkich danych, które mają toosave przed usunięciem konta hello. To również jest spełniony dla wszystkich zasobów na koncie hello — po usunięciu obiektu blob, tabeli, kolejki lub pliku spowoduje jego trwałe skasowanie.
> 

Jeśli spróbujesz toodelete skojarzone konto magazynu maszyny wirtualnej platformy Azure, może wystąpić błąd o koncie magazynu hello nadal są nadal używane. Aby uzyskać pomoc w rozwiązaniu tego problemu, zobacz [Rozwiązywanie problemów związanych z błędami podczas usuwania kont magazynu](../common/storage-resource-manager-cannot-delete-storage-account-container-vhd.md).

## <a name="next-steps"></a>Następne kroki
* [Eksplorator magazynu Microsoft Azure](../../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.
* [Azure Blob Storage: warstwy Chłodna i Gorąca](../blobs/storage-blob-storage-tiers.md)
* [Replikacja usługi Azure Storage](storage-redundancy.md)
* [Konfiguracja parametrów połączenia usługi Azure Storage](../storage-configure-connection-string.md)
* [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md)
* Odwiedź hello [Blog zespołu usługi Magazyn Azure](http://blogs.msdn.com/b/windowsazurestorage/).

