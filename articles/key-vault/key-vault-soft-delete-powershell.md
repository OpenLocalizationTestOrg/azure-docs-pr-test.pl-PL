---
ms.assetid: 
title: "aaaAzure klucza magazynu — jak toouse soft usunięcie przy użyciu programu PowerShell"
description: "Wielkość przykłady usuwania nietrwałego za pomocą programu PowerShell wycinki kodu"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 4968b700a14f764ea1be7de2bf3697664f255f95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a>Jak toouse Key Vault soft usunięcie przy użyciu programu PowerShell

Funkcja usuwania nietrwałego klucza magazynu Azure umożliwia odzyskiwanie usuniętych magazynów i magazynu obiektów. W szczególności adresy usuwania nietrwałego hello następujące scenariusze:

- Obsługa możliwych do odzyskania usuwanie magazynu kluczy
- Obsługa możliwych do odzyskania usuwanie magazynu kluczy obiektów; klucze i klucze tajne, i certyfikaty

## <a name="prerequisites"></a>Wymagania wstępne

- Program Azure PowerShell 4.0.0 lub później — Jeśli nie masz już tym Instalatora, zainstalować program Azure PowerShell i skojarzyć go z subskrypcją platformy Azure, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview). 

>[!NOTE]
> Brak pliku nieaktualną wersją naszych formatowanie danych wyjściowych klucza magazynu w programie PowerShell **może** być załadowane do środowiska zamiast hello poprawnej wersji. Firma Microsoft są przewidywanie zaktualizowaną wersję środowiska PowerShell toocontain hello potrzebne korekty formatowanie danych wyjściowych hello i zaktualizuje wszystkie informacje w tym temacie w tym czasie. Witaj bieżącego rozwiązania powinien wystąpić problem formatowania jest:
> - Właściwości opisane w tym temacie włączone hello Użyj następującego zapytania, Jeśli zauważysz, że nie występują hello soft usunięcie: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.


Magazyn kluczy refernece określonych informacji dla programu PowerShell, zobacz [odwołania programu PowerShell magazynu kluczy Azure](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

## <a name="required-permissions"></a>Wymagane uprawnienia

Operacje usługi Key Vault oddzielnie są zarządzane za pośrednictwem uprawnień kontroli dostępu opartej na rolach w następujący sposób:

| Operacja | Opis | Uprawnienia użytkownika |
|:--|:--|:--|
|List|Listy usunięte magazynów kluczy.|Microsoft.KeyVault/deletedVaults/read|
|Recover|Przywrócenie usuniętych magazynu kluczy.|Microsoft.KeyVault/vaults/write|
|Purge|Trwale usuwa usunięto magazyn kluczy i całą jego zawartość.|Microsoft.KeyVault/locations/deletedVaults/purge/action|

Aby uzyskać więcej informacji dotyczących uprawnień i kontroli dostępu, zobacz [bezpiecznego magazynu kluczy](key-vault-secure-your-key-vault.md).

## <a name="enabling-soft-delete"></a>Włączanie soft-delete

toobe toorecover stanie usunięte magazynu kluczy lub obiekty przechowywane w kluczu magazynu, należy najpierw włączyć soft usunięcie tego klucza magazynu.

### <a name="existing-key-vault"></a>Istniejący magazyn kluczy

W przypadku istniejący magazyn kluczy o nazwie ContosoVault włączyć w następujący sposób usuwania nietrwałego. 

>[!NOTE]
>Obecnie należy toouse usługi Azure Resource Manager zasobów manipulowania toodirectly zapisu hello *enableSoftDelete* toohello właściwości zasobu magazynu kluczy.

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a>Nowy magazyn kluczy

Włączanie usuwania nietrwałego nowego magazynu kluczy jest wykonywane w czasie tworzenia, dodając flagi Włącz usuwania nietrwałego hello tooyour Utwórz polecenie.

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a>Sprawdź usuwania nietrwałego aktywacji

tooverify z magazynu kluczy usuwania nietrwałego, włączona, uruchom hello *uzyskać* poleceń i poszukaj hello "Nietrwałego usunąć włączony?" atrybut i jego ustawienie wartości true lub false.

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>Usuwanie magazynu kluczy chronionych przez soft-delete

Witaj polecenie toodelete (lub usuń) magazynu kluczy pozostaje hello sam, ale jego zmiany sposobu działania w zależności od tego, czy włączono soft usunięcie lub nie.

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
>Po uruchomieniu hello poprzedniego polecenia dla magazynu kluczy, który nie ma włączone soft usunięcie spowoduje trwałe usunięcie tego magazynu kluczy i całą jego zawartość bez żadnych opcji odzyskiwania.

### <a name="how-soft-delete-protects-your-key-vaults"></a>Sposób usuwania nietrwałego chroni Twoje magazynów kluczy

Elastyczne delete jest włączona:

- Po usunięciu magazynu kluczy jest usuwane z jego grupa zasobów i umieszczony w zarezerwowaną przestrzenią nazw, które są tylko skojarzona z lokalizacją hello, w której został utworzony. 
- Obiekty Usunięto klucz magazynu, takie jak klucze kluczy tajnych i certyfikaty, są niedostępne i pozostają, gdy ich zawierającego magazynu kluczy jest w stanie usunięty hello. 
- Hello nazwy DNS dla magazynu kluczy w stanie usunięty jest nadal zarezerwowany, więc nie można utworzyć nowego magazynu kluczy o tej samej nazwie.  

Może wyświetlać magazynów kluczy stanie usunięty, skojarzonymi z Twoją subskrypcją przy użyciu hello następujące polecenie:

```powershell
PS C:\> Get-AzureRmKeyVault -InRemovedStateVault 

Name           : ContosoVault
Location             : westus
Id                   : /subscriptions/xxx/providers/Microsoft.KeyVault/locations/westus/deletedVaults/ContosoVault
Resource ID          : /subscriptions/xxx/resourceGroups/ContosoVault/providers/Microsoft.KeyVault/vaults/ContosoVault
Deletion Date        : 5/9/2017 12:14:14 AM
Scheduled Purge Date : 8/7/2017 12:14:14 AM
Tags                 :
```

Witaj *identyfikator zasobu* w hello odnosi się dane wyjściowe toohello pierwotny identyfikator zasobu tym magazynie. Ponieważ w tym magazynie kluczy jest obecnie w stanie usunięty, żaden z zasobów istnieje z tym identyfikatorem zasobu. Witaj *identyfikator* pole może być używane tooidentify hello zasobów podczas odzyskiwania lub czyszczenie. Hello *zaplanowane daty przeczyścić* pole wskazuje, kiedy magazynu hello zostaną trwale usunięte (przeczyścić) Jeśli nie podjęto żadnej akcji dla tego magazynu usunięte. Witaj domyślne przechowywania toocalculate okresu, używana Witaj *zaplanowane daty przeczyścić*, wynosi 90 dni.

## <a name="recovering-a-key-vault"></a>Odzyskiwanie magazyn kluczy

toorecover magazyn kluczy, należy nazwa magazynu kluczy hello toospecify, lokalizacji i grupy zasobów. Uwaga hello lokalizacji i hello grupa zasobów hello usunąć magazyn kluczy, zgodnie z potrzebami dla procesu odzyskiwania magazynu kluczy.

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

Po odzyskaniu magazynu kluczy wynik hello jest nowy zasób o identyfikatorze magazynu kluczy hello oryginalnego zasobów. Usunięcie grupy zasobów hello, gdy istniał hello magazynu kluczy było hello magazynu kluczy można odzyskać musi utworzyć nową grupę zasobów o tej samej nazwie.

## <a name="key-vault-objects-and-soft-delete"></a>Obiekty usługi Key Vault i usuwania nietrwałego

Dla klucza "ContosoFirstKey" w magazynie kluczy o nazwie "ContosoVault" z usuwania nietrwałego włączone, tutaj w sposób można usuwać tego klucza.

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

Z Twoim magazynem kluczy włączone dla usuwania nietrwałego Usunięto klucz jest nadal wyświetlana tak, jak jest usuwany z wyjątkiem, gdy jawnie listy lub pobrać usuniętych kluczy. Większość operacji na klucz w stanie usunięty hello zakończy się niepowodzeniem z wyjątkiem wyświetlania Usunięto klucz, odzyskaniu go lub usunięciu jej zawartości. 

Na przykład toorequest toolist usunięte kluczy w magazynie kluczy, użyj hello następujące polecenie:

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a>Stan przejścia 

Podczas usuwania klucza w magazynie kluczy usuwania nietrwałego, włączone, gdy może potrwać kilka sekund na powitania toocomplete przejścia. W tym stanie przejścia mogą występować tego klucza hello nie jest w stanie aktywnym hello lub stan hello usunięte. To polecenie spowoduje wyświetlenie listy wszystkich usuniętych kluczy w magazynie kluczy o nazwie "ContosoVault".

```powershell
  Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
  Vault Name           : ContosoVault
  Name                 : ContosoFirstKey
  Id                   : https://ContosoVault.vault.azure.net:443/keys/ContosoFirstKey
  Deleted Date         : 2/14/2017 8:20:52 PM
  Scheduled Purge Date : 5/15/2017 8:20:52 PM
  Enabled              : True
  Expires              :
  Not Before           :
  Created              : 2/14/2017 8:16:07 PM
  Updated              : 2/14/2017 8:16:07 PM
  Tags                 :
```

### <a name="using-soft-delete-with-key-vault-objects"></a>Przy użyciu usuwania nietrwałego z obiektami magazyn kluczy

Tylko jak magazynów kluczy, Usunięto klucz, hasło lub certyfikat pozostanie w stanie usunięty się dni too90 chyba że odzyskanie go lub go przeczyścić. 

#### <a name="keys"></a>Klucze

Usunięto klucz toorecover:

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

toopermanently usunąć klucza:

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
>Trwałe usuwanie klucza spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.

Witaj **odzyskać** i **przeczyścić** akcji ma swoje własne w zasadach dostępu do magazynu kluczy są skojarzone uprawnienia. Dla użytkownika lub usługę podmiotu zabezpieczeń toobe stanie tooexecute **odzyskać** lub **przeczyścić** akcji w zasadach dostępu do magazynu kluczy hello muszą mieć hello odpowiednich uprawnień dla tego obiektu (klucz lub klucz tajny). Domyślnie program hello **przeczyścić** uprawnienia nie została dodana magazynu kluczy tooa zasad dostępu, gdy hello skrótu "all" jest używane toogrant wszystkie uprawnienia tooa użytkownika. Należy jawnie udzielić **przeczyścić** uprawnienia. Na przykład Witaj następujące polecenie przyznaje user@contoso.com tooperform uprawnienia kilka operacji na klucze w *ContosoVault* tym **przeczyścić**.

#### <a name="set-a-key-vault-access-policy"></a>Ustawianie zasad dostępu do magazynu kluczy

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> Jeśli masz istniejący magazyn kluczy, który właśnie miał usuwania nietrwałego, włączona, użytkownik może nie mieć **odzyskać** i **przeczyścić** uprawnienia.

#### <a name="secrets"></a>Wpisy tajne

Takie jak klucze kluczy tajnych w magazynie kluczy wykonywane są w ich własnych poleceń. Po, są hello polecenia usuwania, wyświetlanie, odzyskiwania i przeczyszczanie kluczy tajnych.

- Usuń klucz tajny o nazwie SQLPassword: 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- Wyświetl listę wszystkich usuniętych kluczy tajnych w magazynie kluczy: 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- Odzyskiwanie klucza tajnego w stanie usunięty hello: 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- Przeczyść klucza tajnego w stanie usunięty: 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
>Przeczyszczanie klucz tajny spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.

## <a name="purging-and-key-vaults"></a>Magazyny przeczyszczania i klucza

### <a name="key-vault-objects"></a>Obiekty magazyn kluczy

Trwałe usuwanie klucza, hasło lub certyfikat spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania. Podobnie jak wszystkie inne obiekty w magazynie kluczy hello Hello magazyn kluczy, który zawiera hello usunięty obiekt jednak pozostaną nienaruszone. 

### <a name="key-vaults-as-containers"></a>Klucz magazynów jako kontenery
Podczas przeczyszczania magazynu kluczy są całą jego zawartość, łącznie z kluczy, kluczy tajnych i certyfikaty, trwałe skasowanie. toopurge magazyn kluczy, użyj hello `Remove-AzureRmKeyVault` polecenie z opcją hello `-InRemovedState` i określając hello lokalizacja magazynu kluczy hello usunięte z hello `-Location location` argumentu. Można znaleźć lokalizacji hello usunięto magazynu, za pomocą polecenia hello `Get-AzureRmKeyVault -InRemovedState`.

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
>Usuwanie magazynu kluczy spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.

### <a name="purge-permissions-required"></a>Uprawnienia wymagane do przeczyszczenia
- toopurge usunięto magazyn kluczy, tak, aby trwale usunąć magazyn hello i całą jego zawartość, użytkownik hello musi tooperform uprawnienia RBAC *Microsoft.KeyVault/locations/deletedVaults/purge/action* operacji. 
- toolist hello usunięty klucz magazynu hello użytkownik musi tooperform uprawnienia RBAC *Microsoft.KeyVault/deletedVaults/read* uprawnienia. 
- Domyślnie tylko administrator subskrypcji ma te uprawnienia. 

### <a name="scheduled-purge"></a>Zaplanowane przeczyszczenia

Wyświetlanie listy obiektów usuniętych magazynu kluczy pokazuje, gdy są toobe schedled przy Key Vault. Witaj *zaplanowane daty przeczyścić* pole wskazuje, kiedy obiekt magazynu kluczy zostaną trwale usunięte, jeśli nie podjęto żadnej akcji. Domyślnie okres przechowywania hello obiektów usuniętych magazynu kluczy to 90 dni.

>[!NOTE]
>Obiekt magazynu przeczyszczone wyzwalane przez jego *zaplanowane daty przeczyścić* pola, są trwale usuwane. Nie jest możliwe do odzyskania.

## <a name="other-resources"></a>Inne zasoby

- Omówienie funkcji usuwania nietrwałego Key Vault, zobacz [omówienie usuwania nietrwałego usługi Azure Key Vault](key-vault-ovw-soft-delete.md).
- Ogólne omówienie użycia usługi Azure Key Vault, zobacz [wprowadzenie do usługi Azure Key Vault](key-vault-get-started.md).

