---
ms.assetid: 
title: "aaaAzure klucza magazynu — jak usunąć toouse nietrwałego z interfejsu wiersza polecenia"
description: "Wielkość przykłady usuwania nietrwałego za pomocą wycinków kodu interfejsu wiersza polecenia"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a><span data-ttu-id="16a39-103">Jak toouse Key Vault soft usunięcie z interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="16a39-103">How toouse Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="16a39-104">Funkcja usuwania nietrwałego klucza magazynu Azure umożliwia odzyskiwanie usuniętych magazynów i magazynu obiektów.</span><span class="sxs-lookup"><span data-stu-id="16a39-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="16a39-105">W szczególności adresy usuwania nietrwałego hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="16a39-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="16a39-106">Obsługa możliwych do odzyskania usuwanie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="16a39-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="16a39-107">Obsługa możliwych do odzyskania usuwanie magazynu kluczy obiektów; klucze i klucze tajne, i certyfikaty</span><span class="sxs-lookup"><span data-stu-id="16a39-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16a39-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16a39-108">Prerequisites</span></span>

- <span data-ttu-id="16a39-109">Azure CLI 2.0 — Jeśli nie masz tej instalacji dla danego środowiska, zobacz [Zarządzanie Key Vault za pomocą interfejsu wiersza polecenia 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="16a39-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="16a39-110">Dla usługi Key Vault określone informacje dotyczące interfejsu wiersza polecenia, zobacz [odwołania Azure CLI 2.0 Key Vault](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="16a39-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="16a39-111">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="16a39-111">Required permissions</span></span>

<span data-ttu-id="16a39-112">Operacje usługi Key Vault oddzielnie są zarządzane za pośrednictwem uprawnień kontroli dostępu opartej na rolach w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="16a39-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="16a39-113">Operacja</span><span class="sxs-lookup"><span data-stu-id="16a39-113">Operation</span></span> | <span data-ttu-id="16a39-114">Opis</span><span class="sxs-lookup"><span data-stu-id="16a39-114">Description</span></span> | <span data-ttu-id="16a39-115">Uprawnienia użytkownika</span><span class="sxs-lookup"><span data-stu-id="16a39-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="16a39-116">List</span><span class="sxs-lookup"><span data-stu-id="16a39-116">List</span></span>|<span data-ttu-id="16a39-117">Listy usunięte magazynów kluczy.</span><span class="sxs-lookup"><span data-stu-id="16a39-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="16a39-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="16a39-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="16a39-119">Recover</span><span class="sxs-lookup"><span data-stu-id="16a39-119">Recover</span></span>|<span data-ttu-id="16a39-120">Przywrócenie usuniętych magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="16a39-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="16a39-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="16a39-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="16a39-122">Purge</span><span class="sxs-lookup"><span data-stu-id="16a39-122">Purge</span></span>|<span data-ttu-id="16a39-123">Trwale usuwa usunięto magazyn kluczy i całą jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="16a39-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="16a39-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="16a39-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="16a39-125">Aby uzyskać więcej informacji dotyczących uprawnień i kontroli dostępu, zobacz [bezpiecznego magazynu kluczy](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="16a39-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="16a39-126">Włączanie soft-delete</span><span class="sxs-lookup"><span data-stu-id="16a39-126">Enabling soft-delete</span></span>

<span data-ttu-id="16a39-127">toobe toorecover stanie usunięte magazynu kluczy lub obiekty przechowywane w kluczu magazynu, należy najpierw włączyć soft usunięcie tego klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="16a39-127">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="16a39-128">Istniejący magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="16a39-128">Existing key vault</span></span>

<span data-ttu-id="16a39-129">W przypadku istniejący magazyn kluczy o nazwie ContosoVault włączyć w następujący sposób usuwania nietrwałego.</span><span class="sxs-lookup"><span data-stu-id="16a39-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="16a39-130">Obecnie należy toouse usługi Azure Resource Manager zasobów manipulowania toodirectly zapisu hello *enableSoftDelete* toohello właściwości zasobu magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="16a39-130">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="16a39-131">Nowy magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="16a39-131">New key vault</span></span>

<span data-ttu-id="16a39-132">Włączanie usuwania nietrwałego nowego magazynu kluczy jest wykonywane w czasie tworzenia, dodając flagi Włącz usuwania nietrwałego hello tooyour Utwórz polecenie.</span><span class="sxs-lookup"><span data-stu-id="16a39-132">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="16a39-133">Sprawdź usuwania nietrwałego aktywacji</span><span class="sxs-lookup"><span data-stu-id="16a39-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="16a39-134">tooverify z magazynu kluczy usuwania nietrwałego, włączona, uruchom hello *Pokaż* poleceń i poszukaj hello "Nietrwałego usunąć włączony?"</span><span class="sxs-lookup"><span data-stu-id="16a39-134">tooverify that a key vault has soft-delete enabled, run hello *show* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="16a39-135">atrybut i jego ustawienie wartości true lub false.</span><span class="sxs-lookup"><span data-stu-id="16a39-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="16a39-136">Usuwanie magazynu kluczy chronionych przez soft-delete</span><span class="sxs-lookup"><span data-stu-id="16a39-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="16a39-137">Witaj polecenie toodelete (lub usuń) magazynu kluczy pozostaje hello sam, ale jego zmiany sposobu działania w zależności od tego, czy włączono soft usunięcie lub nie.</span><span class="sxs-lookup"><span data-stu-id="16a39-137">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="16a39-138">Po uruchomieniu hello poprzedniego polecenia dla magazynu kluczy, który nie ma włączone soft usunięcie spowoduje trwałe usunięcie tego magazynu kluczy i całą jego zawartość bez żadnych opcji odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="16a39-138">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="16a39-139">Sposób usuwania nietrwałego chroni Twoje magazynów kluczy</span><span class="sxs-lookup"><span data-stu-id="16a39-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="16a39-140">Elastyczne delete jest włączona:</span><span class="sxs-lookup"><span data-stu-id="16a39-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="16a39-141">Po usunięciu magazynu kluczy jest usuwane z jego grupa zasobów i umieszczony w zarezerwowaną przestrzenią nazw, które są tylko skojarzona z lokalizacją hello, w której został utworzony.</span><span class="sxs-lookup"><span data-stu-id="16a39-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="16a39-142">Obiekty Usunięto klucz magazynu, takie jak klucze kluczy tajnych i certyfikaty, są niedostępne i pozostają, gdy ich zawierającego magazynu kluczy jest w stanie usunięty hello.</span><span class="sxs-lookup"><span data-stu-id="16a39-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="16a39-143">Hello nazwy DNS dla magazynu kluczy w stanie usunięty jest nadal zarezerwowany, więc nie można utworzyć nowego magazynu kluczy o tej samej nazwie.</span><span class="sxs-lookup"><span data-stu-id="16a39-143">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="16a39-144">Może wyświetlać magazynów kluczy stanie usunięty, skojarzonymi z Twoją subskrypcją przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="16a39-144">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="16a39-145">Witaj *identyfikator zasobu* w hello odnosi się dane wyjściowe toohello pierwotny identyfikator zasobu tym magazynie.</span><span class="sxs-lookup"><span data-stu-id="16a39-145">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="16a39-146">Ponieważ w tym magazynie kluczy jest obecnie w stanie usunięty, żaden z zasobów istnieje z tym identyfikatorem zasobu.</span><span class="sxs-lookup"><span data-stu-id="16a39-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="16a39-147">Witaj *identyfikator* pole może być używane tooidentify hello zasobów podczas odzyskiwania lub czyszczenie.</span><span class="sxs-lookup"><span data-stu-id="16a39-147">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="16a39-148">Hello *zaplanowane daty przeczyścić* pole wskazuje, kiedy magazynu hello zostaną trwale usunięte (przeczyścić) Jeśli nie podjęto żadnej akcji dla tego magazynu usunięte.</span><span class="sxs-lookup"><span data-stu-id="16a39-148">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="16a39-149">Witaj domyślne przechowywania toocalculate okresu, używana Witaj *zaplanowane daty przeczyścić*, wynosi 90 dni.</span><span class="sxs-lookup"><span data-stu-id="16a39-149">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="16a39-150">Odzyskiwanie magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="16a39-150">Recovering a key vault</span></span>

<span data-ttu-id="16a39-151">toorecover magazyn kluczy, należy nazwa magazynu kluczy hello toospecify, lokalizacji i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="16a39-151">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="16a39-152">Uwaga hello lokalizacji i hello grupa zasobów hello usunąć magazyn kluczy, zgodnie z potrzebami dla procesu odzyskiwania magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="16a39-152">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="16a39-153">Po odzyskaniu magazynu kluczy wynik hello jest nowy zasób o identyfikatorze magazynu kluczy hello oryginalnego zasobów.</span><span class="sxs-lookup"><span data-stu-id="16a39-153">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="16a39-154">Usunięcie grupy zasobów hello, gdy istniał hello magazynu kluczy było hello magazynu kluczy można odzyskać musi utworzyć nową grupę zasobów o tej samej nazwie.</span><span class="sxs-lookup"><span data-stu-id="16a39-154">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="16a39-155">Obiekty usługi Key Vault i usuwania nietrwałego</span><span class="sxs-lookup"><span data-stu-id="16a39-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="16a39-156">Dla klucza "ContosoFirstKey" w magazynie kluczy o nazwie "ContosoVault" z usuwania nietrwałego włączone, tutaj w sposób można usuwać tego klucza.</span><span class="sxs-lookup"><span data-stu-id="16a39-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="16a39-157">Z Twoim magazynem kluczy włączone dla usuwania nietrwałego Usunięto klucz jest nadal wyświetlana tak, jak jest usuwany z wyjątkiem, gdy jawnie listy lub pobrać usuniętych kluczy.</span><span class="sxs-lookup"><span data-stu-id="16a39-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="16a39-158">Większość operacji na klucz w stanie usunięty hello zakończy się niepowodzeniem z wyjątkiem wyświetlania Usunięto klucz, odzyskaniu go lub usunięciu jej zawartości.</span><span class="sxs-lookup"><span data-stu-id="16a39-158">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="16a39-159">Na przykład toorequest toolist usunięte kluczy w magazynie kluczy, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="16a39-159">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="16a39-160">Stan przejścia</span><span class="sxs-lookup"><span data-stu-id="16a39-160">Transition state</span></span> 

<span data-ttu-id="16a39-161">Podczas usuwania klucza w magazynie kluczy usuwania nietrwałego, włączone, gdy może potrwać kilka sekund na powitania toocomplete przejścia.</span><span class="sxs-lookup"><span data-stu-id="16a39-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="16a39-162">W tym stanie przejścia mogą występować tego klucza hello nie jest w stanie aktywnym hello lub stan hello usunięte.</span><span class="sxs-lookup"><span data-stu-id="16a39-162">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="16a39-163">To polecenie spowoduje wyświetlenie listy wszystkich usuniętych kluczy w magazynie kluczy o nazwie "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="16a39-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="16a39-164">Przy użyciu usuwania nietrwałego z obiektami magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="16a39-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="16a39-165">Tylko jak magazynów kluczy, Usunięto klucz, hasło lub certyfikat pozostanie w stanie usunięty się dni too90 chyba że odzyskanie go lub go przeczyścić.</span><span class="sxs-lookup"><span data-stu-id="16a39-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="16a39-166">Klucze</span><span class="sxs-lookup"><span data-stu-id="16a39-166">Keys</span></span>

<span data-ttu-id="16a39-167">Usunięto klucz toorecover:</span><span class="sxs-lookup"><span data-stu-id="16a39-167">toorecover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="16a39-168">toopermanently usunąć klucza:</span><span class="sxs-lookup"><span data-stu-id="16a39-168">toopermanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="16a39-169">Trwałe usuwanie klucza spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="16a39-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="16a39-170">Witaj **odzyskać** i **przeczyścić** akcji ma swoje własne w zasadach dostępu do magazynu kluczy są skojarzone uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="16a39-170">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="16a39-171">Dla użytkownika lub usługę podmiotu zabezpieczeń toobe stanie tooexecute **odzyskać** lub **przeczyścić** akcji w zasadach dostępu do magazynu kluczy hello muszą mieć hello odpowiednich uprawnień dla tego obiektu (klucz lub klucz tajny).</span><span class="sxs-lookup"><span data-stu-id="16a39-171">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="16a39-172">Domyślnie program hello **przeczyścić** uprawnienia nie została dodana magazynu kluczy tooa zasad dostępu, gdy hello skrótu "all" jest używane toogrant wszystkie uprawnienia tooa użytkownika.</span><span class="sxs-lookup"><span data-stu-id="16a39-172">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="16a39-173">Należy jawnie udzielić **przeczyścić** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="16a39-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="16a39-174">Na przykład Witaj następujące polecenie przyznaje user@contoso.com tooperform uprawnienia kilka operacji na klucze w *ContosoVault* tym **przeczyścić**.</span><span class="sxs-lookup"><span data-stu-id="16a39-174">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="16a39-175">Ustawianie zasad dostępu do magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="16a39-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="16a39-176">Jeśli masz istniejący magazyn kluczy, który właśnie miał usuwania nietrwałego, włączona, użytkownik może nie mieć **odzyskać** i **przeczyścić** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="16a39-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="16a39-177">Wpisy tajne</span><span class="sxs-lookup"><span data-stu-id="16a39-177">Secrets</span></span>

<span data-ttu-id="16a39-178">Takie jak klucze kluczy tajnych w magazynie kluczy wykonywane są w ich własnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="16a39-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="16a39-179">Po, są hello polecenia usuwania, wyświetlanie, odzyskiwania i przeczyszczanie kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="16a39-179">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="16a39-180">Usuń klucz tajny o nazwie SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="16a39-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="16a39-181">Wyświetl listę wszystkich usuniętych kluczy tajnych w magazynie kluczy:</span><span class="sxs-lookup"><span data-stu-id="16a39-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="16a39-182">Odzyskiwanie klucza tajnego w stanie usunięty hello:</span><span class="sxs-lookup"><span data-stu-id="16a39-182">Recover a secret in hello deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="16a39-183">Przeczyść klucza tajnego w stanie usunięty:</span><span class="sxs-lookup"><span data-stu-id="16a39-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="16a39-184">Przeczyszczanie klucz tajny spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="16a39-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="16a39-185">Magazyny przeczyszczania i klucza</span><span class="sxs-lookup"><span data-stu-id="16a39-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="16a39-186">Obiekty magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="16a39-186">Key vault objects</span></span>

<span data-ttu-id="16a39-187">Trwałe usuwanie klucza, hasło lub certyfikat spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="16a39-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="16a39-188">Podobnie jak wszystkie inne obiekty w magazynie kluczy hello Hello magazyn kluczy, który zawiera hello usunięty obiekt jednak pozostaną nienaruszone.</span><span class="sxs-lookup"><span data-stu-id="16a39-188">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="16a39-189">Klucz magazynów jako kontenery</span><span class="sxs-lookup"><span data-stu-id="16a39-189">Key vaults as containers</span></span>
<span data-ttu-id="16a39-190">Podczas przeczyszczania magazynu kluczy są całą jego zawartość, łącznie z kluczy, kluczy tajnych i certyfikaty, trwałe skasowanie.</span><span class="sxs-lookup"><span data-stu-id="16a39-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="16a39-191">toopurge magazyn kluczy, użyj hello `az keyvault purge` polecenia.</span><span class="sxs-lookup"><span data-stu-id="16a39-191">toopurge a key vault, use hello `az keyvault purge` command.</span></span> <span data-ttu-id="16a39-192">Można znaleźć lokalizacji hello swoją subskrypcję usunięto magazynów kluczy za pomocą polecenia hello `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="16a39-192">You can find hello location your subscription's deleted key vaults using hello command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="16a39-193">Usuwanie magazynu kluczy spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="16a39-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="16a39-194">Uprawnienia wymagane do przeczyszczenia</span><span class="sxs-lookup"><span data-stu-id="16a39-194">Purge permissions required</span></span>
- <span data-ttu-id="16a39-195">toopurge usunięto magazyn kluczy, tak, aby trwale usunąć magazyn hello i całą jego zawartość, użytkownik hello musi tooperform uprawnienia RBAC *Microsoft.KeyVault/locations/deletedVaults/purge/action* operacji.</span><span class="sxs-lookup"><span data-stu-id="16a39-195">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="16a39-196">toolist hello usunięty klucz magazynu hello użytkownik musi tooperform uprawnienia RBAC *Microsoft.KeyVault/deletedVaults/read* uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="16a39-196">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="16a39-197">Domyślnie tylko administrator subskrypcji ma te uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="16a39-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="16a39-198">Zaplanowane przeczyszczenia</span><span class="sxs-lookup"><span data-stu-id="16a39-198">Scheduled purge</span></span>

<span data-ttu-id="16a39-199">Wyświetlanie listy obiektów usuniętych magazynu kluczy pokazuje, gdy są toobe schedled przy Key Vault.</span><span class="sxs-lookup"><span data-stu-id="16a39-199">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="16a39-200">Witaj *zaplanowane daty przeczyścić* pole wskazuje, kiedy obiekt magazynu kluczy zostaną trwale usunięte, jeśli nie podjęto żadnej akcji.</span><span class="sxs-lookup"><span data-stu-id="16a39-200">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="16a39-201">Domyślnie okres przechowywania hello obiektów usuniętych magazynu kluczy to 90 dni.</span><span class="sxs-lookup"><span data-stu-id="16a39-201">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="16a39-202">Obiekt magazynu przeczyszczone wyzwalane przez jego *zaplanowane daty przeczyścić* pola, są trwale usuwane.</span><span class="sxs-lookup"><span data-stu-id="16a39-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="16a39-203">Nie jest możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="16a39-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="16a39-204">Inne zasoby</span><span class="sxs-lookup"><span data-stu-id="16a39-204">Other resources</span></span>

- <span data-ttu-id="16a39-205">Omówienie funkcji usuwania nietrwałego Key Vault, zobacz [omówienie usuwania nietrwałego usługi Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="16a39-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="16a39-206">Ogólne omówienie użycia usługi Azure Key Vault, zobacz [wprowadzenie do usługi Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="16a39-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

