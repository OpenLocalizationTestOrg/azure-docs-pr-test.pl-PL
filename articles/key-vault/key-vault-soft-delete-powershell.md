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
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="07f21-103">Jak toouse Key Vault soft usunięcie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="07f21-103">How toouse Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="07f21-104">Funkcja usuwania nietrwałego klucza magazynu Azure umożliwia odzyskiwanie usuniętych magazynów i magazynu obiektów.</span><span class="sxs-lookup"><span data-stu-id="07f21-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="07f21-105">W szczególności adresy usuwania nietrwałego hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="07f21-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="07f21-106">Obsługa możliwych do odzyskania usuwanie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="07f21-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="07f21-107">Obsługa możliwych do odzyskania usuwanie magazynu kluczy obiektów; klucze i klucze tajne, i certyfikaty</span><span class="sxs-lookup"><span data-stu-id="07f21-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07f21-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="07f21-108">Prerequisites</span></span>

- <span data-ttu-id="07f21-109">Program Azure PowerShell 4.0.0 lub później — Jeśli nie masz już tym Instalatora, zainstalować program Azure PowerShell i skojarzyć go z subskrypcją platformy Azure, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07f21-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="07f21-110">Brak pliku nieaktualną wersją naszych formatowanie danych wyjściowych klucza magazynu w programie PowerShell **może** być załadowane do środowiska zamiast hello poprawnej wersji.</span><span class="sxs-lookup"><span data-stu-id="07f21-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of hello correct version.</span></span> <span data-ttu-id="07f21-111">Firma Microsoft są przewidywanie zaktualizowaną wersję środowiska PowerShell toocontain hello potrzebne korekty formatowanie danych wyjściowych hello i zaktualizuje wszystkie informacje w tym temacie w tym czasie.</span><span class="sxs-lookup"><span data-stu-id="07f21-111">We are anticipating an updated version of PowerShell toocontain hello needed correction for hello output formatting and will update this topic at that time.</span></span> <span data-ttu-id="07f21-112">Witaj bieżącego rozwiązania powinien wystąpić problem formatowania jest:</span><span class="sxs-lookup"><span data-stu-id="07f21-112">hello current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="07f21-113">Właściwości opisane w tym temacie włączone hello Użyj następującego zapytania, Jeśli zauważysz, że nie występują hello soft usunięcie: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="07f21-113">Use hello following query if you notice you're not seeing hello soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="07f21-114">Magazyn kluczy refernece określonych informacji dla programu PowerShell, zobacz [odwołania programu PowerShell magazynu kluczy Azure](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="07f21-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="07f21-115">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="07f21-115">Required permissions</span></span>

<span data-ttu-id="07f21-116">Operacje usługi Key Vault oddzielnie są zarządzane za pośrednictwem uprawnień kontroli dostępu opartej na rolach w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="07f21-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="07f21-117">Operacja</span><span class="sxs-lookup"><span data-stu-id="07f21-117">Operation</span></span> | <span data-ttu-id="07f21-118">Opis</span><span class="sxs-lookup"><span data-stu-id="07f21-118">Description</span></span> | <span data-ttu-id="07f21-119">Uprawnienia użytkownika</span><span class="sxs-lookup"><span data-stu-id="07f21-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="07f21-120">List</span><span class="sxs-lookup"><span data-stu-id="07f21-120">List</span></span>|<span data-ttu-id="07f21-121">Listy usunięte magazynów kluczy.</span><span class="sxs-lookup"><span data-stu-id="07f21-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="07f21-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="07f21-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="07f21-123">Recover</span><span class="sxs-lookup"><span data-stu-id="07f21-123">Recover</span></span>|<span data-ttu-id="07f21-124">Przywrócenie usuniętych magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="07f21-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="07f21-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="07f21-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="07f21-126">Purge</span><span class="sxs-lookup"><span data-stu-id="07f21-126">Purge</span></span>|<span data-ttu-id="07f21-127">Trwale usuwa usunięto magazyn kluczy i całą jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="07f21-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="07f21-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="07f21-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="07f21-129">Aby uzyskać więcej informacji dotyczących uprawnień i kontroli dostępu, zobacz [bezpiecznego magazynu kluczy](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="07f21-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="07f21-130">Włączanie soft-delete</span><span class="sxs-lookup"><span data-stu-id="07f21-130">Enabling soft-delete</span></span>

<span data-ttu-id="07f21-131">toobe toorecover stanie usunięte magazynu kluczy lub obiekty przechowywane w kluczu magazynu, należy najpierw włączyć soft usunięcie tego klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="07f21-131">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="07f21-132">Istniejący magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="07f21-132">Existing key vault</span></span>

<span data-ttu-id="07f21-133">W przypadku istniejący magazyn kluczy o nazwie ContosoVault włączyć w następujący sposób usuwania nietrwałego.</span><span class="sxs-lookup"><span data-stu-id="07f21-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="07f21-134">Obecnie należy toouse usługi Azure Resource Manager zasobów manipulowania toodirectly zapisu hello *enableSoftDelete* toohello właściwości zasobu magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="07f21-134">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="07f21-135">Nowy magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="07f21-135">New key vault</span></span>

<span data-ttu-id="07f21-136">Włączanie usuwania nietrwałego nowego magazynu kluczy jest wykonywane w czasie tworzenia, dodając flagi Włącz usuwania nietrwałego hello tooyour Utwórz polecenie.</span><span class="sxs-lookup"><span data-stu-id="07f21-136">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="07f21-137">Sprawdź usuwania nietrwałego aktywacji</span><span class="sxs-lookup"><span data-stu-id="07f21-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="07f21-138">tooverify z magazynu kluczy usuwania nietrwałego, włączona, uruchom hello *uzyskać* poleceń i poszukaj hello "Nietrwałego usunąć włączony?"</span><span class="sxs-lookup"><span data-stu-id="07f21-138">tooverify that a key vault has soft-delete enabled, run hello *get* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="07f21-139">atrybut i jego ustawienie wartości true lub false.</span><span class="sxs-lookup"><span data-stu-id="07f21-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="07f21-140">Usuwanie magazynu kluczy chronionych przez soft-delete</span><span class="sxs-lookup"><span data-stu-id="07f21-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="07f21-141">Witaj polecenie toodelete (lub usuń) magazynu kluczy pozostaje hello sam, ale jego zmiany sposobu działania w zależności od tego, czy włączono soft usunięcie lub nie.</span><span class="sxs-lookup"><span data-stu-id="07f21-141">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="07f21-142">Po uruchomieniu hello poprzedniego polecenia dla magazynu kluczy, który nie ma włączone soft usunięcie spowoduje trwałe usunięcie tego magazynu kluczy i całą jego zawartość bez żadnych opcji odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="07f21-142">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="07f21-143">Sposób usuwania nietrwałego chroni Twoje magazynów kluczy</span><span class="sxs-lookup"><span data-stu-id="07f21-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="07f21-144">Elastyczne delete jest włączona:</span><span class="sxs-lookup"><span data-stu-id="07f21-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="07f21-145">Po usunięciu magazynu kluczy jest usuwane z jego grupa zasobów i umieszczony w zarezerwowaną przestrzenią nazw, które są tylko skojarzona z lokalizacją hello, w której został utworzony.</span><span class="sxs-lookup"><span data-stu-id="07f21-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="07f21-146">Obiekty Usunięto klucz magazynu, takie jak klucze kluczy tajnych i certyfikaty, są niedostępne i pozostają, gdy ich zawierającego magazynu kluczy jest w stanie usunięty hello.</span><span class="sxs-lookup"><span data-stu-id="07f21-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="07f21-147">Hello nazwy DNS dla magazynu kluczy w stanie usunięty jest nadal zarezerwowany, więc nie można utworzyć nowego magazynu kluczy o tej samej nazwie.</span><span class="sxs-lookup"><span data-stu-id="07f21-147">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="07f21-148">Może wyświetlać magazynów kluczy stanie usunięty, skojarzonymi z Twoją subskrypcją przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="07f21-148">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

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

<span data-ttu-id="07f21-149">Witaj *identyfikator zasobu* w hello odnosi się dane wyjściowe toohello pierwotny identyfikator zasobu tym magazynie.</span><span class="sxs-lookup"><span data-stu-id="07f21-149">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="07f21-150">Ponieważ w tym magazynie kluczy jest obecnie w stanie usunięty, żaden z zasobów istnieje z tym identyfikatorem zasobu.</span><span class="sxs-lookup"><span data-stu-id="07f21-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="07f21-151">Witaj *identyfikator* pole może być używane tooidentify hello zasobów podczas odzyskiwania lub czyszczenie.</span><span class="sxs-lookup"><span data-stu-id="07f21-151">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="07f21-152">Hello *zaplanowane daty przeczyścić* pole wskazuje, kiedy magazynu hello zostaną trwale usunięte (przeczyścić) Jeśli nie podjęto żadnej akcji dla tego magazynu usunięte.</span><span class="sxs-lookup"><span data-stu-id="07f21-152">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="07f21-153">Witaj domyślne przechowywania toocalculate okresu, używana Witaj *zaplanowane daty przeczyścić*, wynosi 90 dni.</span><span class="sxs-lookup"><span data-stu-id="07f21-153">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="07f21-154">Odzyskiwanie magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="07f21-154">Recovering a key vault</span></span>

<span data-ttu-id="07f21-155">toorecover magazyn kluczy, należy nazwa magazynu kluczy hello toospecify, lokalizacji i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="07f21-155">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="07f21-156">Uwaga hello lokalizacji i hello grupa zasobów hello usunąć magazyn kluczy, zgodnie z potrzebami dla procesu odzyskiwania magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="07f21-156">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="07f21-157">Po odzyskaniu magazynu kluczy wynik hello jest nowy zasób o identyfikatorze magazynu kluczy hello oryginalnego zasobów.</span><span class="sxs-lookup"><span data-stu-id="07f21-157">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="07f21-158">Usunięcie grupy zasobów hello, gdy istniał hello magazynu kluczy było hello magazynu kluczy można odzyskać musi utworzyć nową grupę zasobów o tej samej nazwie.</span><span class="sxs-lookup"><span data-stu-id="07f21-158">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="07f21-159">Obiekty usługi Key Vault i usuwania nietrwałego</span><span class="sxs-lookup"><span data-stu-id="07f21-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="07f21-160">Dla klucza "ContosoFirstKey" w magazynie kluczy o nazwie "ContosoVault" z usuwania nietrwałego włączone, tutaj w sposób można usuwać tego klucza.</span><span class="sxs-lookup"><span data-stu-id="07f21-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="07f21-161">Z Twoim magazynem kluczy włączone dla usuwania nietrwałego Usunięto klucz jest nadal wyświetlana tak, jak jest usuwany z wyjątkiem, gdy jawnie listy lub pobrać usuniętych kluczy.</span><span class="sxs-lookup"><span data-stu-id="07f21-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="07f21-162">Większość operacji na klucz w stanie usunięty hello zakończy się niepowodzeniem z wyjątkiem wyświetlania Usunięto klucz, odzyskaniu go lub usunięciu jej zawartości.</span><span class="sxs-lookup"><span data-stu-id="07f21-162">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="07f21-163">Na przykład toorequest toolist usunięte kluczy w magazynie kluczy, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="07f21-163">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="07f21-164">Stan przejścia</span><span class="sxs-lookup"><span data-stu-id="07f21-164">Transition state</span></span> 

<span data-ttu-id="07f21-165">Podczas usuwania klucza w magazynie kluczy usuwania nietrwałego, włączone, gdy może potrwać kilka sekund na powitania toocomplete przejścia.</span><span class="sxs-lookup"><span data-stu-id="07f21-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="07f21-166">W tym stanie przejścia mogą występować tego klucza hello nie jest w stanie aktywnym hello lub stan hello usunięte.</span><span class="sxs-lookup"><span data-stu-id="07f21-166">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="07f21-167">To polecenie spowoduje wyświetlenie listy wszystkich usuniętych kluczy w magazynie kluczy o nazwie "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="07f21-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="07f21-168">Przy użyciu usuwania nietrwałego z obiektami magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="07f21-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="07f21-169">Tylko jak magazynów kluczy, Usunięto klucz, hasło lub certyfikat pozostanie w stanie usunięty się dni too90 chyba że odzyskanie go lub go przeczyścić.</span><span class="sxs-lookup"><span data-stu-id="07f21-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="07f21-170">Klucze</span><span class="sxs-lookup"><span data-stu-id="07f21-170">Keys</span></span>

<span data-ttu-id="07f21-171">Usunięto klucz toorecover:</span><span class="sxs-lookup"><span data-stu-id="07f21-171">toorecover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="07f21-172">toopermanently usunąć klucza:</span><span class="sxs-lookup"><span data-stu-id="07f21-172">toopermanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="07f21-173">Trwałe usuwanie klucza spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="07f21-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="07f21-174">Witaj **odzyskać** i **przeczyścić** akcji ma swoje własne w zasadach dostępu do magazynu kluczy są skojarzone uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="07f21-174">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="07f21-175">Dla użytkownika lub usługę podmiotu zabezpieczeń toobe stanie tooexecute **odzyskać** lub **przeczyścić** akcji w zasadach dostępu do magazynu kluczy hello muszą mieć hello odpowiednich uprawnień dla tego obiektu (klucz lub klucz tajny).</span><span class="sxs-lookup"><span data-stu-id="07f21-175">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="07f21-176">Domyślnie program hello **przeczyścić** uprawnienia nie została dodana magazynu kluczy tooa zasad dostępu, gdy hello skrótu "all" jest używane toogrant wszystkie uprawnienia tooa użytkownika.</span><span class="sxs-lookup"><span data-stu-id="07f21-176">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="07f21-177">Należy jawnie udzielić **przeczyścić** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="07f21-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="07f21-178">Na przykład Witaj następujące polecenie przyznaje user@contoso.com tooperform uprawnienia kilka operacji na klucze w *ContosoVault* tym **przeczyścić**.</span><span class="sxs-lookup"><span data-stu-id="07f21-178">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="07f21-179">Ustawianie zasad dostępu do magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="07f21-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="07f21-180">Jeśli masz istniejący magazyn kluczy, który właśnie miał usuwania nietrwałego, włączona, użytkownik może nie mieć **odzyskać** i **przeczyścić** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="07f21-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="07f21-181">Wpisy tajne</span><span class="sxs-lookup"><span data-stu-id="07f21-181">Secrets</span></span>

<span data-ttu-id="07f21-182">Takie jak klucze kluczy tajnych w magazynie kluczy wykonywane są w ich własnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="07f21-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="07f21-183">Po, są hello polecenia usuwania, wyświetlanie, odzyskiwania i przeczyszczanie kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="07f21-183">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="07f21-184">Usuń klucz tajny o nazwie SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="07f21-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="07f21-185">Wyświetl listę wszystkich usuniętych kluczy tajnych w magazynie kluczy:</span><span class="sxs-lookup"><span data-stu-id="07f21-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="07f21-186">Odzyskiwanie klucza tajnego w stanie usunięty hello:</span><span class="sxs-lookup"><span data-stu-id="07f21-186">Recover a secret in hello deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="07f21-187">Przeczyść klucza tajnego w stanie usunięty:</span><span class="sxs-lookup"><span data-stu-id="07f21-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="07f21-188">Przeczyszczanie klucz tajny spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="07f21-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="07f21-189">Magazyny przeczyszczania i klucza</span><span class="sxs-lookup"><span data-stu-id="07f21-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="07f21-190">Obiekty magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="07f21-190">Key vault objects</span></span>

<span data-ttu-id="07f21-191">Trwałe usuwanie klucza, hasło lub certyfikat spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="07f21-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="07f21-192">Podobnie jak wszystkie inne obiekty w magazynie kluczy hello Hello magazyn kluczy, który zawiera hello usunięty obiekt jednak pozostaną nienaruszone.</span><span class="sxs-lookup"><span data-stu-id="07f21-192">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="07f21-193">Klucz magazynów jako kontenery</span><span class="sxs-lookup"><span data-stu-id="07f21-193">Key vaults as containers</span></span>
<span data-ttu-id="07f21-194">Podczas przeczyszczania magazynu kluczy są całą jego zawartość, łącznie z kluczy, kluczy tajnych i certyfikaty, trwałe skasowanie.</span><span class="sxs-lookup"><span data-stu-id="07f21-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="07f21-195">toopurge magazyn kluczy, użyj hello `Remove-AzureRmKeyVault` polecenie z opcją hello `-InRemovedState` i określając hello lokalizacja magazynu kluczy hello usunięte z hello `-Location location` argumentu.</span><span class="sxs-lookup"><span data-stu-id="07f21-195">toopurge a key vault, use hello `Remove-AzureRmKeyVault` command with hello option `-InRemovedState` and by specifying hello location of hello deleted key vault with hello `-Location location` argument.</span></span> <span data-ttu-id="07f21-196">Można znaleźć lokalizacji hello usunięto magazynu, za pomocą polecenia hello `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="07f21-196">You can find hello location of a deleted vault using hello command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="07f21-197">Usuwanie magazynu kluczy spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="07f21-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="07f21-198">Uprawnienia wymagane do przeczyszczenia</span><span class="sxs-lookup"><span data-stu-id="07f21-198">Purge permissions required</span></span>
- <span data-ttu-id="07f21-199">toopurge usunięto magazyn kluczy, tak, aby trwale usunąć magazyn hello i całą jego zawartość, użytkownik hello musi tooperform uprawnienia RBAC *Microsoft.KeyVault/locations/deletedVaults/purge/action* operacji.</span><span class="sxs-lookup"><span data-stu-id="07f21-199">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="07f21-200">toolist hello usunięty klucz magazynu hello użytkownik musi tooperform uprawnienia RBAC *Microsoft.KeyVault/deletedVaults/read* uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="07f21-200">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="07f21-201">Domyślnie tylko administrator subskrypcji ma te uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="07f21-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="07f21-202">Zaplanowane przeczyszczenia</span><span class="sxs-lookup"><span data-stu-id="07f21-202">Scheduled purge</span></span>

<span data-ttu-id="07f21-203">Wyświetlanie listy obiektów usuniętych magazynu kluczy pokazuje, gdy są toobe schedled przy Key Vault.</span><span class="sxs-lookup"><span data-stu-id="07f21-203">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="07f21-204">Witaj *zaplanowane daty przeczyścić* pole wskazuje, kiedy obiekt magazynu kluczy zostaną trwale usunięte, jeśli nie podjęto żadnej akcji.</span><span class="sxs-lookup"><span data-stu-id="07f21-204">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="07f21-205">Domyślnie okres przechowywania hello obiektów usuniętych magazynu kluczy to 90 dni.</span><span class="sxs-lookup"><span data-stu-id="07f21-205">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="07f21-206">Obiekt magazynu przeczyszczone wyzwalane przez jego *zaplanowane daty przeczyścić* pola, są trwale usuwane.</span><span class="sxs-lookup"><span data-stu-id="07f21-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="07f21-207">Nie jest możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="07f21-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="07f21-208">Inne zasoby</span><span class="sxs-lookup"><span data-stu-id="07f21-208">Other resources</span></span>

- <span data-ttu-id="07f21-209">Omówienie funkcji usuwania nietrwałego Key Vault, zobacz [omówienie usuwania nietrwałego usługi Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="07f21-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="07f21-210">Ogólne omówienie użycia usługi Azure Key Vault, zobacz [wprowadzenie do usługi Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="07f21-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

