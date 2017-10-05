---
ms.assetid: 
title: "Usługa Azure Key Vault - sposobu usuwania nietrwałego za pomocą interfejsu wiersza polecenia"
description: "Wielkość przykłady usuwania nietrwałego za pomocą wycinków kodu interfejsu wiersza polecenia"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 3ee2c5dfb99d734cde25894174466b8e49823c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-cli"></a><span data-ttu-id="4670e-103">Jak używać usługi Key Vault soft usunięcie z interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="4670e-103">How to use Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="4670e-104">Funkcja usuwania nietrwałego klucza magazynu Azure umożliwia odzyskiwanie usuniętych magazynów i magazynu obiektów.</span><span class="sxs-lookup"><span data-stu-id="4670e-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="4670e-105">W szczególności soft usunięcie adresy następujących scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="4670e-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="4670e-106">Obsługa możliwych do odzyskania usuwanie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="4670e-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="4670e-107">Obsługa możliwych do odzyskania usuwanie magazynu kluczy obiektów; klucze i klucze tajne, i certyfikaty</span><span class="sxs-lookup"><span data-stu-id="4670e-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4670e-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4670e-108">Prerequisites</span></span>

- <span data-ttu-id="4670e-109">Azure CLI 2.0 — Jeśli nie masz tej instalacji dla danego środowiska, zobacz [Zarządzanie Key Vault za pomocą interfejsu wiersza polecenia 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="4670e-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="4670e-110">Dla usługi Key Vault określone informacje dotyczące interfejsu wiersza polecenia, zobacz [odwołania Azure CLI 2.0 Key Vault](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="4670e-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="4670e-111">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="4670e-111">Required permissions</span></span>

<span data-ttu-id="4670e-112">Operacje usługi Key Vault oddzielnie są zarządzane za pośrednictwem uprawnień kontroli dostępu opartej na rolach w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4670e-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="4670e-113">Operacja</span><span class="sxs-lookup"><span data-stu-id="4670e-113">Operation</span></span> | <span data-ttu-id="4670e-114">Opis</span><span class="sxs-lookup"><span data-stu-id="4670e-114">Description</span></span> | <span data-ttu-id="4670e-115">Uprawnienia użytkownika</span><span class="sxs-lookup"><span data-stu-id="4670e-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="4670e-116">List</span><span class="sxs-lookup"><span data-stu-id="4670e-116">List</span></span>|<span data-ttu-id="4670e-117">Listy usunięte magazynów kluczy.</span><span class="sxs-lookup"><span data-stu-id="4670e-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="4670e-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="4670e-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="4670e-119">Recover</span><span class="sxs-lookup"><span data-stu-id="4670e-119">Recover</span></span>|<span data-ttu-id="4670e-120">Przywrócenie usuniętych magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="4670e-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="4670e-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="4670e-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="4670e-122">Purge</span><span class="sxs-lookup"><span data-stu-id="4670e-122">Purge</span></span>|<span data-ttu-id="4670e-123">Trwale usuwa usunięto magazyn kluczy i całą jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="4670e-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="4670e-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="4670e-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="4670e-125">Aby uzyskać więcej informacji dotyczących uprawnień i kontroli dostępu, zobacz [bezpiecznego magazynu kluczy](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="4670e-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="4670e-126">Włączanie soft-delete</span><span class="sxs-lookup"><span data-stu-id="4670e-126">Enabling soft-delete</span></span>

<span data-ttu-id="4670e-127">Aby można było odzyskać usuniętego magazynu kluczy lub obiekty przechowywane w magazynie kluczy, należy najpierw włączyć soft usunięcie tego klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="4670e-127">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="4670e-128">Istniejący magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="4670e-128">Existing key vault</span></span>

<span data-ttu-id="4670e-129">W przypadku istniejący magazyn kluczy o nazwie ContosoVault włączyć w następujący sposób usuwania nietrwałego.</span><span class="sxs-lookup"><span data-stu-id="4670e-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="4670e-130">Obecnie należy użyć manipulowania zasobów usługi Azure Resource Manager bezpośrednio zapisać *enableSoftDelete* właściwości do zasobu magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="4670e-130">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="4670e-131">Nowy magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="4670e-131">New key vault</span></span>

<span data-ttu-id="4670e-132">Włączanie usuwania nietrwałego nowego magazynu kluczy odbywa w czasie tworzenia, dodając flagi Włącz usuwania nietrwałego Twojej Utwórz polecenie.</span><span class="sxs-lookup"><span data-stu-id="4670e-132">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="4670e-133">Sprawdź usuwania nietrwałego aktywacji</span><span class="sxs-lookup"><span data-stu-id="4670e-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="4670e-134">Aby sprawdzić, czy magazyn kluczy usuwania nietrwałego, włączona, uruchom *Pokaż* poleceń i wyszukaj "nietrwałego usunąć włączony?"</span><span class="sxs-lookup"><span data-stu-id="4670e-134">To verify that a key vault has soft-delete enabled, run the *show* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="4670e-135">atrybut i jego ustawienie wartości true lub false.</span><span class="sxs-lookup"><span data-stu-id="4670e-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="4670e-136">Usuwanie magazynu kluczy chronionych przez soft-delete</span><span class="sxs-lookup"><span data-stu-id="4670e-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="4670e-137">Polecenie, aby usunąć (lub usuń) magazynu kluczy jest taka sama, ale jego zachowanie zmienia się w zależności od tego, czy włączono usuwania nietrwałego lub nie.</span><span class="sxs-lookup"><span data-stu-id="4670e-137">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="4670e-138">Po uruchomieniu poprzedniego polecenia dla magazynu kluczy, który nie ma włączone soft usunięcie spowoduje trwałe usunięcie tego magazynu kluczy i całą jego zawartość bez żadnych opcji odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="4670e-138">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="4670e-139">Sposób usuwania nietrwałego chroni Twoje magazynów kluczy</span><span class="sxs-lookup"><span data-stu-id="4670e-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="4670e-140">Elastyczne delete jest włączona:</span><span class="sxs-lookup"><span data-stu-id="4670e-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="4670e-141">Po usunięciu magazynu kluczy jest usuwane z jego grupa zasobów i umieszczony w zarezerwowaną przestrzenią nazw, które są tylko skojarzone z lokalizacji, w której został utworzony.</span><span class="sxs-lookup"><span data-stu-id="4670e-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="4670e-142">Obiekty Usunięto klucz magazynu, takie jak klucze kluczy tajnych i certyfikaty, są niedostępne i pozostać tak podczas ich zawierającego magazynu kluczy jest w stanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="4670e-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="4670e-143">Nazwy DNS dla magazynu kluczy w stanie usunięty jest nadal zarezerwowany, więc nie można utworzyć nowego magazynu kluczy o tej samej nazwie.</span><span class="sxs-lookup"><span data-stu-id="4670e-143">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="4670e-144">Można wyświetlić stanu usunięcia magazynów kluczy, skojarzonymi z Twoją subskrypcją za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4670e-144">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="4670e-145">*Identyfikator zasobu* w danych wyjściowych odwołuje się do oryginalnego identyfikator zasobu w tym magazynie.</span><span class="sxs-lookup"><span data-stu-id="4670e-145">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="4670e-146">Ponieważ w tym magazynie kluczy jest obecnie w stanie usunięty, żaden z zasobów istnieje z tym identyfikatorem zasobu.</span><span class="sxs-lookup"><span data-stu-id="4670e-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="4670e-147">*Identyfikator* pole służy do identyfikacji zasobu podczas odzyskiwania lub czyszczenie.</span><span class="sxs-lookup"><span data-stu-id="4670e-147">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="4670e-148">*Zaplanowane daty przeczyścić* pole wskazuje, kiedy magazynu zostaną trwale usunięte (przeczyścić) Jeśli nie podjęto żadnej akcji dla tego magazynu usunięte.</span><span class="sxs-lookup"><span data-stu-id="4670e-148">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="4670e-149">Domyślny okres przechowywania, używane do obliczania *zaplanowane daty przeczyścić*, wynosi 90 dni.</span><span class="sxs-lookup"><span data-stu-id="4670e-149">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="4670e-150">Odzyskiwanie magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="4670e-150">Recovering a key vault</span></span>

<span data-ttu-id="4670e-151">Aby odzyskać magazyn kluczy, należy określić nazwę magazynu kluczy, grupy zasobów i lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="4670e-151">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="4670e-152">Należy pamiętać, lokalizacji i grupy zasobów magazynu kluczy usunięte zgodnie z potrzebami dla procesu odzyskiwania magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="4670e-152">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="4670e-153">Po odzyskaniu magazyn kluczy, wynikiem jest nowy zasób z oryginalnego identyfikatora zasobu magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="4670e-153">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="4670e-154">Usunięcie grupy zasobów, której istniała magazynu kluczy można utworzyć nową grupę zasobów o tej samej nazwie, zanim magazyn kluczy, które mogą zostać odzyskane.</span><span class="sxs-lookup"><span data-stu-id="4670e-154">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="4670e-155">Obiekty usługi Key Vault i usuwania nietrwałego</span><span class="sxs-lookup"><span data-stu-id="4670e-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="4670e-156">Dla klucza "ContosoFirstKey" w magazynie kluczy o nazwie "ContosoVault" z usuwania nietrwałego włączone, tutaj w sposób można usuwać tego klucza.</span><span class="sxs-lookup"><span data-stu-id="4670e-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="4670e-157">Z Twoim magazynem kluczy włączone dla usuwania nietrwałego Usunięto klucz jest nadal wyświetlana tak, jak jest usuwany z wyjątkiem, gdy jawnie listy lub pobrać usuniętych kluczy.</span><span class="sxs-lookup"><span data-stu-id="4670e-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="4670e-158">Większość operacji na klucz w stanie usunięty zakończy się niepowodzeniem z wyjątkiem wyświetlania Usunięto klucz, odzyskaniu go lub usunięciu jej zawartości.</span><span class="sxs-lookup"><span data-stu-id="4670e-158">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="4670e-159">Na przykład żądania, aby usunąć listę kluczy w magazynie kluczy, należy użyć następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4670e-159">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="4670e-160">Stan przejścia</span><span class="sxs-lookup"><span data-stu-id="4670e-160">Transition state</span></span> 

<span data-ttu-id="4670e-161">Podczas usuwania klucza w magazynie kluczy usuwania nietrwałego, włączone, gdy może potrwać kilka sekund przejścia.</span><span class="sxs-lookup"><span data-stu-id="4670e-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="4670e-162">W tym stanie przejścia może pojawić się, że klucz nie jest w stanie aktywnym lub w stanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="4670e-162">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="4670e-163">To polecenie spowoduje wyświetlenie listy wszystkich usuniętych kluczy w magazynie kluczy o nazwie "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="4670e-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="4670e-164">Przy użyciu usuwania nietrwałego z obiektami magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="4670e-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="4670e-165">Po prostu jak magazynów kluczy, Usunięto klucz, hasło lub certyfikat pozostanie w stanie usunięty przez 90 dni chyba że odzyskanie go lub go przeczyścić.</span><span class="sxs-lookup"><span data-stu-id="4670e-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="4670e-166">Klucze</span><span class="sxs-lookup"><span data-stu-id="4670e-166">Keys</span></span>

<span data-ttu-id="4670e-167">Aby odzyskać usunięty klucz:</span><span class="sxs-lookup"><span data-stu-id="4670e-167">To recover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="4670e-168">Aby trwale usunąć klucza:</span><span class="sxs-lookup"><span data-stu-id="4670e-168">To permanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="4670e-169">Trwałe usuwanie klucza spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="4670e-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="4670e-170">**Odzyskać** i **przeczyścić** akcji ma swoje własne w zasadach dostępu do magazynu kluczy są skojarzone uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="4670e-170">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="4670e-171">Dla użytkownika lub nazwy głównej usługi, aby można było wykonać **odzyskać** lub **przeczyścić** akcji w zasadach dostępu do magazynu kluczy muszą mieć odpowiednie uprawnienia dla tego obiektu (klucz lub klucz tajny).</span><span class="sxs-lookup"><span data-stu-id="4670e-171">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="4670e-172">Domyślnie **przeczyścić** uprawnienia nie została dodana do magazynu kluczy, zasady dostępu w przypadku używania "all" skrót do wszystkie uprawnienia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4670e-172">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="4670e-173">Należy jawnie udzielić **przeczyścić** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="4670e-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="4670e-174">Na przykład następujące polecenie przyznaje user@contoso.com uprawnień, aby wykonać kilka operacji na klucze w *ContosoVault* tym **przeczyścić**.</span><span class="sxs-lookup"><span data-stu-id="4670e-174">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="4670e-175">Ustawianie zasad dostępu do magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="4670e-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="4670e-176">Jeśli masz istniejący magazyn kluczy, który właśnie miał usuwania nietrwałego, włączona, użytkownik może nie mieć **odzyskać** i **przeczyścić** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="4670e-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="4670e-177">Wpisy tajne</span><span class="sxs-lookup"><span data-stu-id="4670e-177">Secrets</span></span>

<span data-ttu-id="4670e-178">Takie jak klucze kluczy tajnych w magazynie kluczy wykonywane są w ich własnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="4670e-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="4670e-179">Po, są polecenia usuwania, wyświetlanie, odzyskiwania i przeczyszczanie kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="4670e-179">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="4670e-180">Usuń klucz tajny o nazwie SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="4670e-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="4670e-181">Wyświetl listę wszystkich usuniętych kluczy tajnych w magazynie kluczy:</span><span class="sxs-lookup"><span data-stu-id="4670e-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="4670e-182">Odzyskiwanie klucza tajnego w stanie usunięty:</span><span class="sxs-lookup"><span data-stu-id="4670e-182">Recover a secret in the deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="4670e-183">Przeczyść klucza tajnego w stanie usunięty:</span><span class="sxs-lookup"><span data-stu-id="4670e-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="4670e-184">Przeczyszczanie klucz tajny spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="4670e-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="4670e-185">Magazyny przeczyszczania i klucza</span><span class="sxs-lookup"><span data-stu-id="4670e-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="4670e-186">Obiekty magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="4670e-186">Key vault objects</span></span>

<span data-ttu-id="4670e-187">Trwałe usuwanie klucza, hasło lub certyfikat spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="4670e-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="4670e-188">Magazyn kluczy, który zawiera usunięty obiekt jednak pozostaną nienaruszone, podobnie jak wszystkie inne obiekty w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="4670e-188">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="4670e-189">Klucz magazynów jako kontenery</span><span class="sxs-lookup"><span data-stu-id="4670e-189">Key vaults as containers</span></span>
<span data-ttu-id="4670e-190">Podczas przeczyszczania magazynu kluczy są całą jego zawartość, łącznie z kluczy, kluczy tajnych i certyfikaty, trwałe skasowanie.</span><span class="sxs-lookup"><span data-stu-id="4670e-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="4670e-191">Aby przeczyścić magazyn kluczy, należy użyć `az keyvault purge` polecenia.</span><span class="sxs-lookup"><span data-stu-id="4670e-191">To purge a key vault, use the `az keyvault purge` command.</span></span> <span data-ttu-id="4670e-192">Można znaleźć lokalizacji Twojej subskrypcji usunięto magazynów kluczy za pomocą polecenia `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="4670e-192">You can find the location your subscription's deleted key vaults using the command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="4670e-193">Usuwanie magazynu kluczy spowoduje trwałe usunięcie go, co oznacza, że nie będzie możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="4670e-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="4670e-194">Uprawnienia wymagane do przeczyszczenia</span><span class="sxs-lookup"><span data-stu-id="4670e-194">Purge permissions required</span></span>
- <span data-ttu-id="4670e-195">Przeczyścić usunięto magazyn kluczy, tak, aby trwale usunąć magazyn i całą jego zawartość, użytkownik musi RBAC uprawnienia do wykonywania *Microsoft.KeyVault/locations/deletedVaults/purge/action* operacji.</span><span class="sxs-lookup"><span data-stu-id="4670e-195">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="4670e-196">Aby wyświetlić listę Usunięto klucz, magazynie użytkownik będzie potrzebował RBAC uprawnienia do wykonania *Microsoft.KeyVault/deletedVaults/read* uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="4670e-196">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="4670e-197">Domyślnie tylko administrator subskrypcji ma te uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="4670e-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="4670e-198">Zaplanowane przeczyszczenia</span><span class="sxs-lookup"><span data-stu-id="4670e-198">Scheduled purge</span></span>

<span data-ttu-id="4670e-199">Wyświetlanie obiektów usuniętych magazynu kluczy pokazuje, gdy są one schedled zostaną usunięte przez magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="4670e-199">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="4670e-200">*Zaplanowane daty przeczyścić* pole wskazuje, kiedy obiekt magazynu kluczy zostaną trwale usunięte, jeśli nie podjęto żadnej akcji.</span><span class="sxs-lookup"><span data-stu-id="4670e-200">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="4670e-201">Domyślnie okres przechowywania dla obiekt usunięto magazynu kluczy jest 90 dni.</span><span class="sxs-lookup"><span data-stu-id="4670e-201">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="4670e-202">Obiekt magazynu przeczyszczone wyzwalane przez jego *zaplanowane daty przeczyścić* pola, są trwale usuwane.</span><span class="sxs-lookup"><span data-stu-id="4670e-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="4670e-203">Nie jest możliwe do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="4670e-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="4670e-204">Inne zasoby</span><span class="sxs-lookup"><span data-stu-id="4670e-204">Other resources</span></span>

- <span data-ttu-id="4670e-205">Omówienie funkcji usuwania nietrwałego Key Vault, zobacz [omówienie usuwania nietrwałego usługi Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="4670e-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="4670e-206">Ogólne omówienie użycia usługi Azure Key Vault, zobacz [wprowadzenie do usługi Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4670e-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

