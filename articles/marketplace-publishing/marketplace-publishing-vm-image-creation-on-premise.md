---
title: aaaCreating obrazu maszyny wirtualnej lokalnymi hello Azure Marketplace | Dokumentacja firmy Microsoft
description: "Zrozumienie i wykonać hello kroki toocreate lokalnej obrazu maszyny Wirtualnej i wdrożenie toohello portalu Azure Marketplace innym toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a>Tworzenie obrazu maszyny wirtualnej lokalnymi hello Azure Marketplace
Zdecydowanie zaleca się tworzenie Azure wirtualnych dysków twardych (VHD) bezpośrednio w chmurze hello przy użyciu protokołu Remote Desktop Protocol. Jednak jeśli użytkownik musi jest możliwe toodownload wirtualnego dysku twardego i opracowanie go za pomocą infrastruktury lokalnej.  

Dla rozwoju lokalnych, należy pobrać systemu operacyjnego hello hello utworzony dysk VHD maszyny Wirtualnej. Te kroki nastąpiłoby w ramach kroku 3.3 powyżej.  

## <a name="download-a-vhd-image"></a>Pobranie obrazu wirtualnego dysku twardego
### <a name="locate-a-blob-url"></a>Znajdź adres URL obiektu blob
W kolejności toodownload hello dysku VHD w pierwszej kolejności zlokalizować adresu URL obiektu blob hello hello dysku systemu operacyjnego.

Znajdź nowego adresu URL obiektu blob hello z hello [portalu Microsoft Azure](https://portal.azure.com):

1. Przejdź za**Przeglądaj** > **maszyn wirtualnych**, i wybierz opcję hello wdrożeniu maszyny Wirtualnej.
2. W obszarze **Konfiguruj**, wybierz pozycję hello **dysków** kafelka, która otwiera blok dysków hello.
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. Wybierz hello **dysk systemu operacyjnego**, która otwiera blok innego, który wyświetla właściwości dysku, w tym hello lokalizacja wirtualnego dysku twardego.
4. Skopiuj ten adres URL obiektu blob.
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. Teraz, Usuń hello wdrożyć maszyny Wirtualnej bez usuwania hello zapasowy dysków. Można też zatrzymać hello maszyny Wirtualnej, zamiast usuwania. Nie pobieraj systemu operacyjnego hello wirtualnego dysku twardego, gdy hello maszyna wirtualna jest uruchomiona.
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a>Pobieranie wirtualnego dysku twardego
Po określeniu adresu URL obiektu blob hello hello wirtualnego dysku twardego można pobrać przy użyciu hello [portalu Azure](http://manage.windowsazure.com/) lub programu PowerShell.  

> [!NOTE]
> Na powitania czasu utworzenia tego przewodnika toodownload funkcji hello dysku VHD nie ma jeszcze w hello nowego portalu Microsoft Azure.  
> 
> 

**Pobierz system operacyjny hello wirtualnego dysku twardego za pomocą bieżącego hello [portalu Azure](http://manage.windowsazure.com/)**

1. Jeśli nie zostało to jeszcze zrobione, zaloguj się w toohello portalu Azure.
2. Kliknij przycisk hello **magazynu** kartę.
3. Wybierz konto magazynu hello, w których hello wirtualnego dysku twardego są przechowywane.
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. Spowoduje to wyświetlenie właściwości konta magazynu. Wybierz hello **kontenery** kartę.
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. Wybierz kontener hello, w których hello wirtualnego dysku twardego są przechowywane. Domyślnie podczas tworzenia z portalu hello hello wirtualnego dysku twardego przechowywanego w kontenera VHD.
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. Wybierz hello poprawny system operacyjny dysku VHD, porównując hello toohello adres URL, jeden zapisany.
7. Kliknij pozycję **Pobierz**.
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a>Pobierz dysku VHD za pomocą programu PowerShell
Ponadto toousing hello portalu Azure, możesz użyć hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) wirtualnego dysku twardego systemu operacyjnego hello toodownload polecenia cmdlet.

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
Na przykład Zapisz-AzureVhd-źródła "https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd" - LocalFilePath "C:\Users\Administrator\Desktop\baseimagevm.vhd" - atrybutu StorageKey<String>

> [!NOTE]
> **Zapisz-AzureVhd** ma również **NumberOfThreads** opcji, które mogą być używane do pobrania hello tooincrease równoległości toomake hello najlepsze wykorzystanie przepustowości.
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a>Przekaż wirtualne dyski twarde tooan konta magazynu Azure
Przygotowane wirtualne dyski twarde lokalnej, należy najpierw tooupload je do magazynu konta w usłudze Azure. Ten krok ma miejsce po tworzenie dysk VHD lokalnie, ale przed uzyskaniem certyfikacji dla obrazu maszyny Wirtualnej.

### <a name="create-a-storage-account-and-container"></a>Utwórz konto magazynu i kontener
Zaleca się, że wirtualne dyski twarde można przekazać do konta magazynu w regionie hello Stanów Zjednoczonych. Wszystkie wirtualne dyski twarde dla jednej jednostki SKU powinna zostać umieszczona w jeden kontener w ramach konta pojedynczy magazyn.

toocreate konto magazynu, można użyć hello [portalu Microsoft Azure](https://portal.azure.com/), programu PowerShell lub narzędzia wiersza polecenia hello systemu Linux.  

**Utwórz konto magazynu z portalu Microsoft Azure hello**

1. Kliknij przycisk **Nowy**.
2. Wybierz **magazynu**.
3. Wprowadź nazwę konta magazynu hello, a następnie wybierz lokalizację.
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. Kliknij przycisk **Utwórz**.
5. Witaj bloku hello utworzono konto magazynu powinien być otwarty. Jeśli nie, wybierz **Przeglądaj** > **kont magazynu**. Na powitania magazynu konto bloku, wybierz utworzone konto magazynu hello.
6. Wybierz **kontenery**.
   
   ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. W bloku kontenery hello, wybierz **Dodaj**, a następnie wprowadź uprawnień kontenera kontenera, jak nazwa i hello. Wybierz **prywatnej** uprawnienia do kontenera.

> [!TIP]
> Firma Microsoft zaleca utworzenie jednego kontenera na planowania toopublish jednostki SKU.
> 
> 

  ![Rysowanie](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a>Utwórz konto magazynu przy użyciu programu PowerShell
Przy użyciu programu PowerShell, Utwórz konto magazynu przy użyciu hello [AzureStorageAccount nowy](http://msdn.microsoft.com/library/dn495115.aspx) polecenia cmdlet.

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

Następnie można utworzyć kontener w ramach tego konta magazynu przy użyciu hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) polecenia cmdlet.

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> Te polecenia przyjęto założenie, że ten kontekst hello bieżącego konta magazynu został już ustawiony w programie PowerShell.   Odwołuje się zbyt[Konfigurowanie programu Azure PowerShell](marketplace-publishing-powershell-setup.md) uzyskać więcej informacji dotyczących instalacji programu PowerShell.  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a>Utwórz konto magazynu przy użyciu narzędzia wiersza polecenia hello for Mac i Linux
> Z [narzędzia wiersza polecenia systemu Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), Utwórz konto magazynu w następujący sposób.
> 
> 

        azure storage account create mystorageaccount --location "West US"

Utwórz kontener w następujący sposób.

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a>Przekazywanie wirtualnego dysku twardego
Po utworzeniu hello konto magazynu i kontener, możesz przekazać go przygotować dyski VHD. Można użyć programu PowerShell, narzędzia wiersza polecenia systemu Linux hello lub innych narzędzi do zarządzania usługi Azure Storage.

### <a name="upload-a-vhd-via-powershell"></a>Przekazywanie wirtualnego dysku twardego za pomocą programu PowerShell
Użyj hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) polecenia cmdlet.

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a>Przekazywanie wirtualnego dysku twardego za pomocą narzędzia wiersza polecenia hello for Mac i Linux
Z hello [narzędzia wiersza polecenia systemu Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), poniższych hello: Tworzenie obrazu maszyny wirtualnej azure <image name> — lokalizacji <Location of hello data center> — system operacyjny Linux<LocationOfLocalVHD>

## <a name="see-also"></a>Zobacz też
* [Tworzenie obrazu maszyny wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-creation.md)
* [Konfigurowanie programu Azure PowerShell](marketplace-publishing-powershell-setup.md)

