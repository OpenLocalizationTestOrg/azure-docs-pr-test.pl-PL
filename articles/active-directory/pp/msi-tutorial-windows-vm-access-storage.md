---
title: "Umożliwia dostęp do usługi Azure Storage MSI maszyny Wirtualnej systemu Windows"
description: "Samouczek, który przeprowadzi Cię przez proces przy użyciu systemu Windows maszyny Wirtualnej zarządzane usługi tożsamości (MSI), dostęp do magazynu Azure."
services: active-directory
documentationcenter: 
author: BryanLa
manager: mbaldwin
editor: bryanla
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/15/2017
ms.author: bryanla
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: e7f715acc3ab343a36e0968701894fd29ff8af71
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/22/2017
---
# <a name="use-a-windows-vm-managed-service-identity-to-access-azure-storage-via-access-key"></a>Maszyna wirtualna zarządzane tożsamości usługi systemu Windows umożliwia dostęp do usługi Azure Storage za pomocą klucza dostępu

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

Ten samouczek pokazuje, jak włączyć zarządzane tożsamości usługi (MSI) dla maszyny wirtualnej systemu Windows, a następnie użyć tej tożsamości można pobrać klucze dostępu do konta magazynu. Można użyć w zwykły sposób podczas wykonywania operacji magazynu, na przykład w przypadku korzystania z zestawu SDK usługi Magazyn kluczy dostępu do magazynu. W tym samouczku będziemy przekazywanie i pobieranie obiektów blob przy użyciu programu PowerShell magazynu Azure. Dowiesz się jak:


> [!div class="checklist"]
> * Włącz MSI w maszynie wirtualnej systemu Windows 
> * Przyznać uprawnienia maszyny Wirtualnej do kluczy dostępu do konta magazynu w programie Menedżer zasobów 
> * Uzyskaj token dostępu przy użyciu tożsamości maszyny Wirtualnej i przy jego użyciu pobrać klucze dostępu do magazynu z Menedżera zasobów 

## <a name="prerequisites"></a>Wymagania wstępne

[!INCLUDE [msi-core-prereqs](~/includes/active-directory-msi-core-prereqs-ua.md)]

[!INCLUDE [msi-tut-prereqs](~/includes/active-directory-msi-tut-prereqs.md)]

## <a name="sign-in-to-azure"></a>Logowanie do platformy Azure

Zaloguj się do witryny Azure Portal pod adresem [https://portal.azure.com](https://portal.azure.com).

## <a name="create-a-windows-virtual-machine-in-a-new-resource-group"></a>Utwórz maszynę wirtualną systemu Windows w nowej grupy zasobów

W tym samouczku utworzymy nową maszynę Wirtualną systemu Windows. Można również włączyć MSI na istniejącej maszyny Wirtualnej.

1.  Kliknij przycisk **+/ Utwórz nową usługę** znaleziono przycisku w lewym górnym rogu portalu Azure.
2.  Wybierz pozycję **Wystąpienia obliczeniowe**, a następnie wybierz pozycję **Windows Server 2016 Datacenter**. 
3.  Wprowadź informacje o maszynie wirtualnej. **Username** i **hasło** utworzony, w tym miejscu jest poświadczeń umożliwia logowanie do maszyny wirtualnej.
4.  Wybierz odpowiednią **subskrypcji** dla maszyny wirtualnej na liście rozwijanej.
5.  Aby wybrać nowy **grupy zasobów** chcesz maszynę wirtualną można utworzyć w, wybierz **Utwórz nowy**. Po zakończeniu kliknij przycisk **OK**.
6.  Wybierz rozmiar maszyny wirtualnej. Aby wyświetlić więcej rozmiarów, wybierz pozycje **Wyświetl wszystkie** lub zmień filtr **Obsługiwany typ dysku**. W bloku ustawień pozostaw ustawienia domyślne i kliknij przycisk **OK**.

    ![Tekst alternatywny obrazu](~/articles/active-directory/media/msi-tutorial-windows-vm-access-arm/msi-windows-vm.png)

## <a name="enable-msi-on-your-vm"></a>Włącz MSI na maszynie Wirtualnej

MSI maszyny wirtualnej umożliwia pobieranie tokenów dostępu z usługi Azure AD bez konieczności umieścić poświadczeń w kodzie. W obszarze obejmuje włączenie MSI wykonuje dwie czynności: instalacji rozszerzenia maszyny Wirtualnej MSI w maszynie Wirtualnej i umożliwia korzystanie z pliku MSI dla maszyny wirtualnej.  

1. Przejdź do grupy zasobów nowej maszyny wirtualnej, a następnie wybierz maszynę wirtualną, utworzony w poprzednim kroku.
2. W obszarze VM "Ustawienia", po lewej stronie kliknij **konfiguracji**.
3. Aby zarejestrować i włączyć MSI, wybierz **tak**, jeśli chcesz ją wyłączyć, wybierz opcję nie.
4. Upewnij się, możesz kliknąć przycisk **zapisać** Aby zapisać konfigurację.

    ![Tekst alternatywny obrazu](~/articles/active-directory/media/msi-tutorial-linux-vm-access-arm/msi-linux-extension.png)

5. Jeśli chcesz sprawdzić, które rozszerzenia na maszynie Wirtualnej, kliknij przycisk **rozszerzenia**. Po włączeniu MSI **ManagedIdentityExtensionforWindows** pojawią się na liście.

    ![Tekst alternatywny obrazu](~/articles/active-directory/media/msi-tutorial-linux-vm-access-arm/msi-extension-value.png)

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu 

Jeśli nie masz jeszcze jeden, teraz utworzysz konto magazynu. Można również pominąć ten krok i przyznać uprawnienia MSI maszyny Wirtualnej do istniejącego konta magazynu kluczy. 

1. Kliknij przycisk **+/ Utwórz nową usługę** znaleziono przycisku w lewym górnym rogu portalu Azure.
2. Kliknij przycisk **magazynu**, następnie **konta magazynu**, i wyświetli nowy panel "Tworzenie konta magazynu".
3. Wprowadź nazwę konta magazynu, który będzie używany w później.  
4. **Model wdrażania** i **konta rodzaju** powinien być ustawiony odpowiednio na "Resource manager" i "Ogólnego przeznaczenia". 
5. Upewnij się, **subskrypcji** i **grupy zasobów** odpowiadały określony podczas tworzenia maszyny Wirtualnej w poprzednim kroku.
6. Kliknij przycisk **Utwórz**.

    ![Utwórz nowe konto magazynu](~/articles/active-directory/media/msi-tutorial-linux-vm-access-storage/msi-storage-create.png)

## <a name="create-a-blob-container-in-the-storage-account"></a>Tworzenie kontenera obiektów blob na koncie magazynu

Firma Microsoft będzie później przekazywanie i pobranie pliku do nowego konta magazynu. Ponieważ pliki wymagają magazynu obiektów blob, należy utworzyć kontener obiektów blob do przechowywania pliku.

1. Przejdź z powrotem do użytkownika nowo utworzone konto magazynu.
2. Kliknij przycisk **kontenery** łącze w z lewej strony, w obszarze "Usługa Blob".
3. Kliknij przycisk **+ kontener** górnej części strony, a "nowy kontener" panelu slajdów wychodzących.
4. Nadaj nazwę kontenera, wybierz poziom dostępu, a następnie kliknij przycisk **OK**. Podana nazwa będzie używana później w samouczku. 

    ![Tworzenie kontenera magazynu](~/articles/active-directory/media/msi-tutorial-linux-vm-access-storage/create-blob-container.png)

## <a name="grant-your-vms-msi-access-to-use-storage-account-access-keys"></a>Przyznanie dostępu MSI z maszyną Wirtualną do używania kluczy dostępu do konta magazynu 

Magazyn Azure nie obsługuje natywnie uwierzytelniania usługi Azure AD.  Jednak można użyć Instalatora MSI można pobrać klucze dostępu do konta magazynu z Menedżera zasobów, a następnie użyć klucza dostępu do magazynu.  W tym kroku należy przyznać uprawnienia MSI maszyny Wirtualnej do kluczy do konta magazynu.   

1. Przejdź z powrotem do użytkownika nowo utworzone konto magazynu.  
2. Kliknij przycisk **(IAM) kontroli dostępu** łącze w lewym panelu.  
3. Kliknij przycisk **+ Dodaj** u góry strony, aby dodać nowe przypisanie roli dla maszyny Wirtualnej
4. Ustaw **roli** do "Magazynu konta klucza usługi roli operatora", w prawej części strony. 
5. Na liście rozwijanej dalej, ustaw **przypisany dostęp** zasobu "Maszyny wirtualnej".  
6. Następnie sprawdź odpowiednie subskrypcji znajduje się w **subskrypcji** listy rozwijanej, a następnie ustaw **grupy zasobów** do "Wszystkie grupy zasobów".  
7. Ponadto w obszarze **wybierz** wybierz maszynę wirtualną systemu Windows na liście rozwijanej, a następnie kliknij przycisk **zapisać**. 

    ![Tekst alternatywny obrazu](~/articles/active-directory/media/msi-tutorial-linux-vm-access-storage/msi-storage-role.png)

## <a name="get-an-access-token-using-the-vms-identity-and-use-it-to-call-azure-resource-manager"></a>Uzyskaj token dostępu przy użyciu tożsamości maszyny Wirtualnej i użyć go do wywołania usługi Azure Resource Manager 

W pozostałej części tego samouczka firma Microsoft będzie działać z maszyny Wirtualnej, utworzony wcześniej. 

Należy użyć poleceń cmdlet programu PowerShell usługi Azure Resource Manager w tej części.  Jeśli nie jest zainstalowany, [Pobierz najnowszą wersję](https://docs.microsoft.com/powershell/azure/overview) przed kontynuowaniem.

1. W portalu Azure, przejdź do **maszyn wirtualnych**, przejdź do maszyny wirtualnej systemu Windows, następnie z **omówienie** kliknij **Connect** u góry. 
2. Wprowadź w Twojej **Username** i **hasło** dla którego zostanie dodane po utworzeniu maszyny Wirtualnej systemu Windows. 
3. Teraz, po utworzeniu **Podłączanie pulpitu zdalnego** z maszyną wirtualną, Otwórz program PowerShell w sesji zdalnej.
4. Przy użyciu programu Powershell w Invoke-WebRequest, Wyślij żądanie do lokalnego punktu końcowego MSI do Uzyskaj token dostępu usługi Azure Resource Manager.

    ```powershell
       $response = Invoke-WebRequest -Uri http://localhost:50342/oauth2/token -Method GET -Body @{resource="https://management.azure.com/"} -Headers @{Metadata="true"}
    ```
    
    > [!NOTE]
    > Wartość parametru "zasobu" musi być dokładnego dopasowania dla oczekiwano przez usługę Azure AD. Podczas korzystania z usługi Azure Resource Manager identyfikator zasobu, należy dołączyć końcowy ukośnik w identyfikatorze URI.
    
    Następnie wyodrębnić elementu "Zawartość", który jest przechowywany jako ciąg w formacie JavaScript Object Notation (JSON) w obiekcie $response. 
    
    ```powershell
    $content = $response.Content | ConvertFrom-Json
    ```
    Następnie Wyodrębnij token dostępu z odpowiedzi.
    
    ```powershell
    $ArmToken = $content.access_token
    ```
 
## <a name="get-storage-account-access-keys-from-azure-resource-manager-to-make-storage-calls"></a>Uzyskaj z usługi Azure Resource Manager w celu wykonywania wywołań magazynu kluczy dostępu do konta magazynu  

Do wywołania usługi Resource Manager przy użyciu tokenu dostępu, możemy pobrany w poprzedniej sekcji za pomocą programu PowerShell można pobrać klucz dostępu do magazynu. Po klucz dostępu do magazynu, firma Microsoft może nazywa się operacje przekazywania/Pobierz magazynu.

```powershell
$keysResponse = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/<SUBSCRIPTION-ID>/resourceGroups/<RESOURCE-GROUP>/providers/Microsoft.Storage/storageAccounts/<STORAGE-ACCOUNT>/listKeys/?api-version=2016-12-01 -Method POST -Headers @{Authorization="Bearer $ARMToken"}
```
> [!NOTE] 
> Adres URL jest rozróżniana wielkość liter, dlatego upewnij się, użyj tego samego dokładnej używane wcześniej, gdy nazwa grupy zasobów, w tym wielkie litery "G" w "resourceGroups." 

```powershell
$keysContent = $keysResponse.Content | ConvertFrom-Json
$key = $keysContent.keys[0].value
```

Następnie tworzymy plik o nazwie "test.txt". Następnie użyj klucz dostępu do magazynu do uwierzytelniania za pomocą `New-AzureStorageContent` polecenia cmdlet, przekazać go do naszego kontenera obiektów blob, a następnie Pobierz plik.

```bash
echo "This is a test text file." > test.txt
```

Upewnij się, najpierw zainstaluj polecenia cmdlet usługi Azure Storage za pomocą `Install-Module Azure.Storage`. Następnie przekazania obiektu blob nowo utworzone przy użyciu `Set-AzureStorageBlobContent` polecenia cmdlet programu PowerShell:

```powershell
$ctx = New-AzureStorageContext -StorageAccountName <STORAGE-ACCOUNT> -StorageAccountKey $key
Set-AzureStorageBlobContent -File test.txt -Container <CONTAINER-NAME> -Blob testblob -Context $ctx
```

Odpowiedź:

```powershell
ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob
BlobType          : BlockBlob
Length            : 56
ContentType       : application/octet-stream
LastModified      : 9/13/2017 6:14:25 PM +00:00
SnapshotTime      :
ContinuationToken :
Context           : Microsoft.WindowsAzure.Commands.Storage.AzureStorageContext
Name              : testblob
```

Możesz również pobrać przekazanym właśnie, za pomocą obiektu blob `Get-AzureStorageBlobContent` polecenia cmdlet programu PowerShell:

```powershell
Get-AzureStorageBlobContent -Blob testblob -Container <CONTAINER-NAME> -Destination test2.txt -Context $ctx
```

Odpowiedź:

```powershell
ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob
BlobType          : BlockBlob
Length            : 56
ContentType       : application/octet-stream
LastModified      : 9/13/2017 6:14:25 PM +00:00
SnapshotTime      :
ContinuationToken :
Context           : Microsoft.WindowsAzure.Commands.Storage.AzureStorageContext
Name              : testblob
```


## <a name="related-content"></a>Zawartość pokrewna

- Omówienie MSI, zobacz [omówienie zarządzane tożsamość usługi](msi-overview.md).
- Aby dowiedzieć się, jak to zrobić to opisane w tym samouczku przy użyciu magazynu poświadczeń sygnatury dostępu Współdzielonego, zobacz [umożliwia dostęp do usługi Azure Storage za pomocą poświadczeń sygnatury dostępu Współdzielonego wirtualna zarządzane tożsamości usługi systemu Windows](msi-tutorial-windows-vm-access-storage-sas.md)
- Aby uzyskać więcej informacji o funkcji sygnatury dostępu Współdzielonego konta usługi Azure Storage zobacz:
  - [Przy użyciu sygnatury dostępu współdzielonego (SAS)](~/articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)
  - [Utworzenie sygnatury dostępu Współdzielonego usługi](/rest/api/storageservices/Constructing-a-Service-SAS.md)

Użyj następujących sekcji komentarzy wyrazić swoją opinię i pomóc nam dostosować i kształtu zawartość


