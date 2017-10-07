---
title: "aaaHow toocreate, zarządzania i usuwania konta magazynu w hello klasycznego portalu Azure | Dokumentacja firmy Microsoft"
description: "Utwórz nowe konto magazynu, zarządzanie kluczami dostępu do konta lub usuwania konta magazynu w hello portalu Azure. Więcej informacji na temat kont magazynu (warstwy Standardowa i Premium)."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 5e4f4360-3f81-4d63-a0b1-e7771b67af11
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 6ee2359e02c7c9e9c111e1fc87a6160bb8b785b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Informacje o kontach magazynu Azure
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-try-azure-tools](../../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Omówienie
Konto magazynu Azure zapewnia dostęp toohello usług obiektów Blob platformy Azure, kolejki, tabel i plików w usłudze Azure Storage. Konto magazynu zapewnia unikatową przestrzeń nazw powitania dla obiektów danych usługi Azure Storage. Domyślnie dane hello na Twoim koncie są dostępne tooyou tylko właściciel konta hello.

Istnieją dwa typy kont magazynu:

* Standardowe konto magazynu obejmuje usługi Blob Storage, Table Storage, Queue Storage i File Storage.
* Konto magazynu w warstwie Premium obecnie obsługuje wyłącznie dyski maszyn wirtualnych Azure. Zobacz temat [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md) (Premium Storage: usługa Storage o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure), aby uzyskać szczegółowe informacje o usłudze Premium Storage.

## <a name="storage-account-billing"></a>Rozliczanie konta usługi Storage
Rozliczenie jest przeprowadzane na podstawie wykorzystania usługi Azure Storage w oparciu o Twoje konto magazynu. Koszty usługi Storage są oparte na czterech czynnikach: pojemności magazynu, schemacie replikacji, transakcjach magazynu i wyjściu danych.

* Pojemność magazynu znacznie odwołuje się toohow z przydziału konta magazynu są przy użyciu toostore danych. koszt samego przechowywania danych Hello jest określany przez ilość danych są przechowywane i sposobu ich replikacji.
* Replikacja określa liczbę kopii danych, które są obsługiwane jednocześnie, i ich lokalizacje.
* Transakcje odnoszą się tooall odczytu i zapisu tooAzure operacji magazynu.
* Wyjście danych dotyczy toodata przesyłane poza region platformy Azure. Gdy hello danych na koncie magazynu uzyskuje się dostęp przez aplikację, która nie jest uruchomiony w hello tego samego regionu, czy których aplikacja jest usługą w chmurze lub inny rodzaj aplikacji, a następnie naliczane są opłaty za wyjście danych. (Dla usług Azure, można wykonać kroki toogroup danych i usług w hello tych samych danych Wyśrodkowuje tooreduce lub wyeliminować opłaty za wyjście danych.)  

Witaj [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage) strona zawiera szczegółowe informacje o cenach za pojemność magazynu, replikacji i transakcji. Witaj [szczegóły cennika transferów danych](https://azure.microsoft.com/pricing/details/data-transfers/) strona zawiera szczegółowe informacje o cenach za wyjście danych.

Aby uzyskać szczegółowe informacje o celach dotyczących pojemności i wydajności konta magazynu, zobacz [Cele dotyczące skalowalności i wydajności usługi Azure Storage](storage-scalability-targets.md).

> [!NOTE]
> Podczas tworzenia maszyny wirtualnej platformy Azure, konto magazynu jest tworzony automatycznie w lokalizacji wdrożenia hello Jeśli nie masz już konto magazynu w tej lokalizacji. Dlatego nie jest konieczne toofollow hello kroki toocreate konto magazynu dla dysków maszyny wirtualnej. Nazwa konta magazynu Hello będzie opierać się na powitania nazwę maszyny wirtualnej. Zobacz hello [dokumentacji usługi Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/) więcej szczegółów.
> 
> 

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Kliknij przycisk **nowy** na powitania zadań u dołu hello hello strony. Wybierz kolejno pozycje **Data Services** | **Storage**, a następnie kliknij przycisk **Szybkie tworzenie**.
   
    ![Nowe konto magazynu](./media/storage-create-storage-account-classic-portal/storage_NewStorageAccount.png)
3. W polu **Adres URL** wprowadź nazwę konta magazynu.
   
   > [!NOTE]
   > Nazwy kont usługi Storage muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery.
   > 
   > Nazwa konta magazynu musi być unikatowa w obrębie platformy Azure. Hello klasyczny Portal Azure poinformuje, jeśli hello nazwy konta magazynu, którą wybierzesz jest już zajęta.
   > 
   > 
   
    Zobacz [punkty końcowe konta magazynu](#storage-account-endpoints) poniżej dla szczegółowych informacji o jak nazwa konta magazynu hello będą używane tooaddress obiektów w usłudze Azure Storage.
4. W **grupa lokalizacji/koligacji**, wybierz lokalizację dla konta magazynu, będącą Zamknij tooyou lub tooyour klientów. Jeśli dane na koncie magazynu uzyskuje się dostęp z innej usługi Azure, takich jak maszyny wirtualnej platformy Azure lub usługi w chmurze, możesz tooselect grupę koligacji z toogroup listy hello konta magazynu w hello tym samym centrum danych z innymi usługami Azure Czy używasz tooimprove wydajności i zredukowania kosztów.
   
    Pamiętaj, że grupę koligacji musisz wybrać podczas tworzenia konta magazynu. Nie można przenieść istniejącą grupę koligacji tooan konta. Aby uzyskać więcej informacji o grupach koligacji, zobacz sekcję [Wspólna lokalizacja usługi z grupą koligacji](#service-co-location-with-an-affinity-group) poniżej.
   
   > [!IMPORTANT]
   > toodetermine lokalizacji, które są dostępne dla Twojej subskrypcji, należy wywołać hello [listy wszystkich dostawców zasobów](https://msdn.microsoft.com/library/azure/dn790524.aspx) operacji. toolist dostawców w programie PowerShell, wywołaj [Get-AzureLocation](https://msdn.microsoft.com/library/azure/dn757693.aspx). .NET, użyj funkcji hello [listy](https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.provideroperationsextensions.list.aspx) metody hello klasy ProviderOperationsExtensions.
   > 
   > Ponadto zobacz temat [Regiony systemu Azure](https://azure.microsoft.com/regions/#services), aby uzyskać więcej informacji o tym, które usługi są dostępne w danym regionie.
   > 
   > 
5. Jeśli masz więcej niż jedną subskrypcją platformy Azure, następnie hello **subskrypcji** zostanie wyświetlone pole. W **subskrypcji**, wprowadź hello subskrypcji platformy Azure, który ma konto magazynu hello toouse z.
6. W **replikacji**, wybierz hello żądany poziom replikacji dla konta magazynu. Witaj zalecana opcja replikacji to replikacja geograficznie nadmiarowa, która zapewnia najwyższą trwałość danych. Aby uzyskać więcej szczegółów na temat opcji replikacji usługi Azure Storage, zobacz [Replikacja usługi Azure Storage](storage-redundancy.md).
7. Kliknij pozycję **Utwórz konto usługi Storage**.
   
    Może upłynąć kilka minut toocreate Twojego konta magazynu. Stan hello toocheck, można monitorować powiadomienia hello u dołu hello hello klasycznego portalu Azure. Po utworzeniu konta magazynu hello nowego konta magazynu ma **Online** stanu i jest gotowy do użycia.

![Strona magazynu](./media/storage-create-storage-account-classic-portal/Storage_StoragePage.png)

### <a name="storage-account-endpoints"></a>Punkty końcowe konta usługi Storage
Każdy obiekt, który jest przechowywany w usłudze Azure Storage, ma unikatowy adres URL. Formularze nazwy konta magazynu Hello hello poddomenę tego adresu. Witaj kombinacja nazw poddomeny i domeny, co jest tooeach określonej usługi, formularzy *punktu końcowego* dla konta magazynu.

Na przykład, jeśli nosi nazwę konta magazynu *mojekontomagazynu*, a następnie hello domyślne punkty końcowe konta magazynu są:

* Usługa Blob: http://*mojekontomagazynu*.blob.core.windows.net
* Usługa Table service: http://*mojekontomagazynu*.table.core.windows.net
* Usługa kolejki: http://*mojekontomagazynu*.queue.core.windows.net
* Usługa plików http://*mojekontomagazynu*.file.core.windows.net

Zostanie wyświetlony hello punkty końcowe konta magazynu na pulpicie nawigacyjnym magazynu hello w hello [klasycznego portalu Azure](https://manage.windowsazure.com) po utworzeniu konta hello.

adres URL Hello dla uzyskiwania dostępu do obiektu na koncie magazynu jest tworzony przez dodanie lokalizacji obiektu hello końcowego toohello konta magazynu hello. Przykładowo adres obiektu Blob może mieć następujący format: http://*mojekontomagazynu*.blob.core.windows.net/*mojkontener*/*mojblob*.

Można również skonfigurować toouse nazwy domeny niestandardowej z kontem magazynu. Zobacz temat [Configure a custom domain name for your blob storage endpoint](storage-custom-domain-name.md) (Konfigurowanie niestandardowej nazwy domeny dla punktu końcowego magazynu obiektów Blob), aby uzyskać więcej szczegółów.

### <a name="service-co-location-with-an-affinity-group"></a>Wspólna lokalizacja usługi z grupą koligacji
*Grupa koligacji* to sposób geograficznego grupowania usług i maszyn wirtualnych platformy Azure z kontem usługi Azure Storage. Grupa koligacji może poprawić wydajność usługi poprzez przydzielenie obciążeń komputerowych w hello tych samych danych Centrum lub w jego pobliżu docelowych odbiorców użytkownika hello. Ponadto nie są naliczane opłaty za wyjście po danych na koncie magazynu uzyskuje się dostęp z innej usługi, która jest częścią hello tej samej grupy koligacji.

> [!NOTE]
> toocreate grupy koligacji, otwórz hello <b>ustawienia</b> obszaru hello [klasycznego portalu Azure](https://manage.windowsazure.com), kliknij przycisk <b>grup koligacji</b>, a następnie kliknij przycisk <b>Dodaj Grupa koligacji</b> lub hello <b>Dodaj</b> przycisku. Można również utworzyć i Zarządzaj grupami koligacji za pomocą hello interfejs API zarządzania usługami Azure. Aby uzyskać więcej informacji, zobacz temat <a href="http://msdn.microsoft.com/library/azure/ee460798.aspx">Operations on affinity groups</a> (Operacje na grupach koligacji).
> 
> 

## <a name="view-copy-and-regenerate-storage-access-keys"></a>Wyświetlanie, kopiowanie i ponowne generowanie kluczy dostępu do magazynu
Podczas tworzenia konta magazynu Azure generuje dwa klucze dostępu do magazynu 512-bitowe, które są używane do uwierzytelniania podczas uzyskiwania dostępu do konta magazynu hello. Zapewniając dwa klucze dostępu do magazynu Azure umożliwia tooregenerate hello kluczy bez przeszkód tooyour magazynu usługi i usługa toothat dostępu.

> [!NOTE]
> Nie zaleca się udostępniania kluczy dostępu do magazynu innym osobom. toopermit dostęp do zasobów toostorage bez przekazywania kluczy dostępu, można użyć *sygnatury dostępu współdzielonego*. Sygnatury dostępu współdzielonego zapewnia tooa dostępu do zasobów na koncie przez określony czas, który należy zdefiniować i uprawnieniami hello przez użytkownika. Zobacz [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Używanie sygnatur dostępu współdzielonego), aby uzyskać więcej informacji.
> 
> 

W hello [klasycznego portalu Azure](https://manage.windowsazure.com), użyj **zarządzanie kluczami** na pulpicie nawigacyjnym hello lub hello **magazynu** strony tooview, kopiowania i regenerate hello kluczy dostępu do magazynu, które są używane tooaccess hello obiektów Blob, tabel i kolejek usługi.

### <a name="copy-a-storage-access-key"></a>Kopiowanie klucza dostępu do magazynu
Można użyć **zarządzanie kluczami** toocopy toouse klucza dostępu do magazynu w parametrach połączenia. Parametry połączenia Hello wymaga nazwy konta magazynu hello i klucza toouse podczas uwierzytelniania. Informacje o konfigurowaniu połączenia ciągi tooaccess usług Azure storage, można znaleźć [skonfigurować parametry połączenia magazynu Azure](storage-configure-connection-string.md).

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), kliknij przycisk **magazynu**, a następnie kliknij nazwę hello pulpitu nawigacyjnego hello tooopen hello magazynu konta.
2. Kliknij przycisk **Zarządzanie kluczami**.
   
     Otworzy się okno **Zarządzania kluczami dostępu**.
   
    ![Zarządzanie kluczami](./media/storage-create-storage-account-classic-portal/Storage_ManageKeys.png)
3. toocopy klucz dostępu do magazynu hello wybierz tekst klucza. Kliknij go prawym przyciskiem myszy, a następnie kliknij polecenie **Kopiuj**.

### <a name="regenerate-storage-access-keys"></a>Ponowne generowanie kluczy dostępu do magazynu
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
2. Wygeneruj ponownie hello podstawowy klucz dostępu dla konta magazynu. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), z pulpitu nawigacyjnego hello lub hello **Konfiguruj** kliknij przycisk **zarządzanie kluczami**. Kliknij przycisk **ponownie wygenerować** w obszarze hello podstawowy klucz dostępu, a następnie kliknij przycisk **tak** tooconfirm, które mają toogenerate nowy klucz.
3. Zaktualizuj parametry połączenia hello w Twojej kodu tooreference hello nowego podstawowego klucza dostępu.
4. Wygeneruj ponownie hello pomocniczy klucz dostępu.

## <a name="delete-a-storage-account"></a>Usuwanie konta magazynu
tooremove konta magazynu, które są już używane, użyj **usunąć** na pulpicie nawigacyjnym hello lub hello **Konfiguruj** strony. **Usuń** usuwa hello całe konto magazynu, wraz ze wszystkimi hello obiektów blob, tabel i kolejek na koncie hello.

> [!WARNING]
> Jest nie jest możliwe toorestore usuniętego konta magazynu lub pobrać żadnej hello zawartość, która zawiera go przed usunięciem. Należy się tooback zapasową wszystkich danych, które mają toosave przed usunięciem konta hello. To również jest spełniony dla wszystkich zasobów na koncie hello — po usunięciu obiektu blob, tabeli, kolejki lub pliku spowoduje jego trwałe skasowanie.
> 
> Jeśli Twoje konto magazynu zawiera pliki VHD dla maszyny wirtualnej platformy Azure, musisz usunąć wszystkie obrazy i dyski, które korzystają z tych plików VHD przed usunięciem konta magazynu hello. Najpierw Zatrzymaj hello maszyny wirtualnej, jeśli działa, a następnie usuń ją. dyski toodelete Przejdź toohello **dysków** i Usuń wszystkie dyski w tym miejscu. obrazy toodelete Przejdź toohello **obrazów** i usuń wszelkie obrazy przechowywane na koncie hello.
> 
> 

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), kliknij przycisk **magazynu**.
2. Kliknij w dowolnym miejscu wpisu konta magazynu hello hello nazwę, a następnie kliknij przycisk **usunąć**.
   
     — Lub —
   
    Kliknij nazwę pulpitu nawigacyjnego hello tooopen konta magazynu hello hello, a następnie kliknij przycisk **usunąć**.
3. Kliknij przycisk **tak** tooconfirm, które mają konta magazynu hello toodelete.

## <a name="next-steps"></a>Następne kroki
* toolearn więcej informacji na temat usługi Azure Storage, zobacz hello [dokumentację usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/).
* Odwiedź hello [Blog zespołu usługi Magazyn Azure](http://blogs.msdn.com/b/windowsazurestorage/).
* [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md)

