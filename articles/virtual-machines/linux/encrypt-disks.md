---
title: "Szyfrowanie dysków na Maszynę wirtualną systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak zaszyfrować dysków wirtualnych w maszyny Wirtualnej systemu Linux, aby zwiększyć bezpieczeństwo, za pomocą 2.0 interfejsu wiersza polecenia platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 172b4c8f5c098d776cb689543f5d8f163b8895b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-linux-vm"></a>Jak zaszyfrować dyski wirtualne na maszynie Wirtualnej systemu Linux
Ulepszone maszyny wirtualnej (VM) zabezpieczeń i zgodności mogą być szyfrowane dyski wirtualne na platformie Azure. Dyski są szyfrowane za pomocą kluczy kryptograficznych, które są już zabezpieczone w usłudze Azure Key Vault. Kontrolowanie tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania. Ten artykuł zawiera szczegóły dotyczące sposobu szyfrowania dysków wirtualnych na Maszynę wirtualną systemu Linux przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure. Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Szybkie polecenia
Jeśli chcesz szybko wykonać zadanie, następujące szczegóły sekcji bazie polecenia do szyfrowania dysków wirtualnych w maszynie Wirtualnej. Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć pozostałej części dokumentu, [uruchamiania tutaj](#overview-of-disk-encryption).

Należy najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login). W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup*, *klucze*, i *myVM*.

Najpierw włączyć dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure z [az dostawcy rejestru](/cli/azure/provider#register) i utworzyć nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Poniższy przykład tworzy nazwę grupy zasobów *myResourceGroup* w *eastus* lokalizacji:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Tworzenie usługi Azure Key Vault z [az keyvault utworzyć](/cli/azure/keyvault#create) i włączyć usługi Key Vault służących do szyfrowania dysku. Określ unikatową nazwę usługi Key Vault *keyvault_name* w następujący sposób:

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Tworzenie klucza kryptograficznego w magazyn kluczy o [Utwórz klucz keyvault az](/cli/azure/keyvault/key#create). W poniższym przykładzie jest tworzony klucz o nazwie *klucze*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

Tworzenie nazwy głównej usługi za pomocą usługi Azure Active Directory z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac). Nazwy głównej usługi obsługuje uwierzytelnianie i wymiany kluczy kryptograficznych z magazynu kluczy. Poniższy przykład odczytuje wartości dla nazwy głównej usługi Id i hasło do wykorzystania w późniejszym polecenia:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

Hasło jest tylko dane wyjściowe w przypadku tworzenia nazwy głównej usługi. W razie potrzeby można wyświetlać i Zapisz hasło (`echo $sp_password`). Możesz wyświetlić listę Twojej nazwy główne usług z [listy sp ad az](/cli/azure/ad/sp#list) i wyświetlić dodatkowe informacje o określonej usługi głównej z [az ad sp Pokaż](/cli/azure/ad/sp#show).

Ustaw uprawnienia na magazyn kluczy o [keyvault az set-policy](/cli/azure/keyvault#set-policy). W poniższym przykładzie identyfikator podmiotu zabezpieczeń usługi jest dostarczana przez poprzednie polecenie:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) i dołączenie dysku danych 5 Gb. Niektóre obrazy marketplace obsługuje szyfrowanie dysków. Poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu **CentOS 7.2n** obrazu:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH przy użyciu maszyny Wirtualnej `publicIpAddress` wyświetlany w danych wyjściowych poprzednie polecenie. Tworzenie partycji i systemu plików, a następnie zainstalować dysk z danymi. Aby uzyskać więcej informacji, zobacz [Połącz z maszyny Wirtualnej systemu Linux, aby zainstalować nowy dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Zamknij sesję SSH.

Szyfrowanie maszyny Wirtualnej z [włączyć szyfrowanie maszyny wirtualnej az](/cli/azure/vm/encryption#enable). W poniższym przykładzie użyto `$sp_id` i `$sp_password` zmienne z poprzednim `ad sp create-for-rbac` polecenie:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Trwa pewien czas na ukończenie procesu szyfrowania dysku. Monitorowanie stanu procesu z [Pokaż szyfrowania maszyny wirtualnej az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Pokazuje stan **EncryptionInProgress**. Poczekaj, aż stan systemu operacyjnego na dysku raporty **VMRestartPending**, ponowne uruchomienie maszyny Wirtualnej z [ponownego uruchomienia maszyny wirtualnej az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Proces szyfrowania dysku zostanie sfinalizowana podczas rozruchu, więc odczekaj kilka minut przed sprawdzeniem stanu szyfrowania ponownie, podając **Pokaż szyfrowania maszyny wirtualnej az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Stan Zgłoś teraz dysk systemu operacyjnego i dysku danych jako **zaszyfrowane**.

## <a name="overview-of-disk-encryption"></a>Omówienie szyfrowania dysków
Dyski wirtualne na maszynach wirtualnych systemu Linux są szyfrowane za pomocą rest [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Jest bezpłatna dla szyfrowania dysków wirtualnych na platformie Azure. Klucze szyfrowania są przechowywane w usługi Azure Key Vault przy użyciu ochrony oprogramowania, lub możesz zaimportować lub wygenerować klucze w sprzętowych modułach zabezpieczeń (HSM) certyfikowane do FIPS 140-2 poziom 2 standardów. Zachowanie kontroli nad tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania. Te klucze szyfrowania są używane do szyfrowania i odszyfrowywania wirtualnych dysków dołączonych do maszyny Wirtualnej. Nazwy głównej usługi Azure Active Directory zapewnia mechanizm bezpiecznego do wystawiania tych kluczy kryptograficznych, ponieważ maszyny wirtualne są zasilane i wyłączanie.

Proces szyfrowania maszyny Wirtualnej jest następujący:

1. Tworzenie klucza kryptograficznego w usłudze Azure Key Vault.
2. Skonfiguruj klucza kryptograficznego, który może być używany do szyfrowania dysków.
3. Aby odczytać klucza kryptograficznego z usługi Azure Key Vault, utworzyć usługę Azure Active Directory podmiot z odpowiednimi uprawnieniami.
4. Wydaj polecenie wirtualnych dysków, określając usługi Azure Active Directory usługa podmiotu zabezpieczeń i odpowiednie klucza kryptograficznego używanego do szyfrowania.
5. Nazwy głównej usługi Azure Active Directory żądań wymaganego klucza kryptograficznego z usługi Azure Key Vault.
6. Dyski wirtualne są szyfrowane za pomocą podanego klucza kryptograficznego.

## <a name="encryption-process"></a>Proces szyfrowania
Szyfrowanie dysków opiera się na następujące dodatkowe składniki:

* **Usługa Azure Key Vault** — używane do ochrony kluczy kryptograficznych i kluczy tajnych używanych przez proces szyfrowania i odszyfrowywania dysku.
  * Jeśli istnieje, można użyć istniejącego magazynu kluczy Azure. Nie trzeba przeznaczyć magazyn kluczy szyfrowania dysków.
  * Aby rozdzielić granice administracyjne i widoczności klucza, możesz utworzyć dedykowany magazyn kluczy.
* **Usługa Azure Active Directory** — obsługuje bezpiecznej wymiany wymagane klucze szyfrowania i uwierzytelniania dla żądanej akcji.
  * Zazwyczaj można użyć istniejącego wystąpienia usługi Azure Active Directory, do przechowywania aplikacji.
  * Nazwy głównej usługi zapewnia mechanizm bezpiecznego do żądania i wydawane odpowiednich kluczy kryptograficznych. Nie opracowujesz aplikację rzeczywista, która integruje się z usługą Azure Active Directory.

## <a name="requirements-and-limitations"></a>Wymagania i ograniczenia
Obsługiwane scenariusze i wymagania dotyczące szyfrowania dysków:

* Następujący serwer z systemem Linux jednostki SKU - Ubuntu, CentOS, SUSE i SUSE Linux Enterprise Server (SLES) i Red Hat Enterprise Linux.
* Wszystkie zasoby (na przykład usługi Key Vault, konta magazynu i maszyny Wirtualnej) muszą być w tym samym regionie Azure i subskrypcji.
* Standardowa A, D DS, G i GS seria maszyn wirtualnych.

Szyfrowanie dysku nie jest obecnie obsługiwane w następujących scenariuszach:

* Maszyny wirtualne warstwy podstawowa.
* Maszyny wirtualne utworzone przy użyciu klasycznego modelu wdrożenia.
* Wyłączenie szyfrowania dysku systemu operacyjnego na maszynach wirtualnych systemu Linux.
* Aktualizowanie kluczy kryptograficznych w już zaszyfrowany maszyny Wirtualnej systemu Linux.

## <a name="create-azure-key-vault-and-keys"></a>Tworzenie usługi Azure Key Vault i kluczy
Należy najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login). W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup*, *klucze*, i *myVM*.

Pierwszym krokiem jest do utworzenia magazynu kluczy Azure do przechowywania kluczy kryptograficznych. Usługa Azure Key Vault można przechowywać kluczy, kluczy tajnych lub haseł, które umożliwiają bezpieczne wdrożenie ich w aplikacji i usług. Szyfrowanie dysków wirtualnych Key Vault służy do przechowywania klucza kryptograficznego używanego do szyfrowania lub odszyfrowywania dysków wirtualnych.

Włącz dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure z [az dostawcy rejestru](/cli/azure/provider#register) i utworzyć nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Poniższy przykład tworzy nazwę grupy zasobów *myResourceGroup* w `eastus` lokalizacji:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Usługa Azure Key Vault zawierający klucze kryptograficzne i zasoby obliczeniowe skojarzone, takie jak magazyn i samej maszyny Wirtualnej musi znajdować się w tym samym regionie. Tworzenie usługi Azure Key Vault z [az keyvault utworzyć](/cli/azure/keyvault#create) i włączyć usługi Key Vault służących do szyfrowania dysku. Określ unikatową nazwę usługi Key Vault *keyvault_name* w następujący sposób:

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Mogą być przechowywane przy użyciu oprogramowania lub sprzętu modelu zabezpieczeń (HSM) ochronę kluczy kryptograficznych. Użycie modułów HSM wymaga premium magazynu kluczy. Brak dodatkowych kosztów tworzenia premium magazynu kluczy, a nie standardowy magazyn kluczy, którego przechowuje klucze chronione przez oprogramowanie. Aby utworzyć premium magazynu kluczy, w poprzednim kroku Dodaj `--sku Premium` do polecenia. W poniższym przykładzie użyto klucze chronione przez oprogramowanie, ponieważ utworzono standardowe magazynu kluczy.

W przypadku obu modeli ochrony platformy Azure musi otrzymać dostęp do żądania kluczy kryptograficznych, podczas rozruchu maszyny Wirtualnej do odszyfrowania dysków wirtualnych. Tworzenie klucza kryptograficznego w magazyn kluczy o [Utwórz klucz keyvault az](/cli/azure/keyvault/key#create). W poniższym przykładzie jest tworzony klucz o nazwie *klucze*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-the-azure-active-directory-service-principal"></a>Tworzenie nazwy głównej usługi Azure Active Directory
Podczas dyski wirtualne są zaszyfrowanie lub odszyfrowanie, należy określić konto w celu obsługi uwierzytelniania i wymiany kluczy kryptograficznych z magazynu kluczy. To konto, nazwy głównej usługi Azure Active Directory umożliwia platformy Azure zażądać odpowiednich kluczy kryptograficznych w imieniu maszyny Wirtualnej. Domyślne wystąpienie usługi Azure Active Directory jest dostępne w Twojej subskrypcji, chociaż w wielu organizacjach są wyposażone w dedykowane katalogów usługi Azure Active Directory.

Tworzenie nazwy głównej usługi za pomocą usługi Azure Active Directory z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac). Poniższy przykład odczytuje wartości dla nazwy głównej usługi Id i hasło do wykorzystania w późniejszym polecenia:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

Hasło jest wyświetlane tylko, tworząc usługę podmiotu zabezpieczeń. W razie potrzeby można wyświetlać i Zapisz hasło (`echo $sp_password`). Możesz wyświetlić listę Twojej nazwy główne usług z [listy sp ad az](/cli/azure/ad/sp#list) i wyświetlić dodatkowe informacje o określonej usługi głównej z [az ad sp Pokaż](/cli/azure/ad/sp#show).

Pomyślnie szyfrowania lub odszyfrowywania dysków wirtualnych, uprawnienia do klucza kryptograficznego, przechowywane w magazynie klucz musi mieć ustawioną zezwolenie na nazwę główną usługi Azure Active Directory do odczytu kluczy. Ustaw uprawnienia na magazyn kluczy o [keyvault az set-policy](/cli/azure/keyvault#set-policy). W poniższym przykładzie identyfikator podmiotu zabezpieczeń usługi jest dostarczana przez poprzednie polecenie:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej
Do szyfrowania faktycznie niektóre dyski wirtualne, umożliwia tworzenie maszyny Wirtualnej i Dodaj dysk danych. Utwórz maszynę Wirtualną do szyfrowania z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) i dołączenie dysku danych 5 Gb. Niektóre obrazy marketplace obsługuje szyfrowanie dysków. Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* przy użyciu **CentOS 7.2n** obrazu:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH przy użyciu maszyny Wirtualnej `publicIpAddress` wyświetlany w danych wyjściowych poprzednie polecenie. Tworzenie partycji i systemu plików, a następnie zainstalować dysk z danymi. Aby uzyskać więcej informacji, zobacz [Połącz z maszyny Wirtualnej systemu Linux, aby zainstalować nowy dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Zamknij sesję SSH.


## <a name="encrypt-virtual-machine"></a>Szyfrowanie maszyny wirtualnej
Do szyfrowania dysków wirtualnych, można przenosić ze sobą wszystkie poprzednie składniki:

1. Podaj nazwę główną usługi Azure Active Directory i hasło.
2. Określ Key Vault w celu przechowywania metadanych dla zaszyfrowanych dysków.
3. Określ klucze kryptograficzne służące do rzeczywistego szyfrowania i odszyfrowywania.
4. Określ, czy chcesz zaszyfrować dysk systemu operacyjnego, dyski danych lub all.

Szyfrowanie maszyny Wirtualnej z [włączyć szyfrowanie maszyny wirtualnej az](/cli/azure/vm/encryption#enable). W poniższym przykładzie użyto `$sp_id` i `$sp_password` zmienne z poprzednim `ad sp create-for-rbac` polecenie:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Trwa pewien czas na ukończenie procesu szyfrowania dysku. Monitorowanie stanu procesu z [Pokaż szyfrowania maszyny wirtualnej az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Wynik jest podobny do poniższego przykładu skrócona:

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

Poczekaj, aż stan systemu operacyjnego na dysku raporty **VMRestartPending**, ponowne uruchomienie maszyny Wirtualnej z [ponownego uruchomienia maszyny wirtualnej az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Proces szyfrowania dysku zostanie sfinalizowana podczas rozruchu, więc odczekaj kilka minut przed sprawdzeniem stanu szyfrowania ponownie, podając **Pokaż szyfrowania maszyny wirtualnej az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Stan Zgłoś teraz dysk systemu operacyjnego i dysku danych jako **zaszyfrowane**.


## <a name="add-additional-data-disks"></a>Dodania dodatkowego dysku z danymi
Po zaszyfrowanych dysków z danymi, możesz później dodać dodatkowych dysków wirtualnych do maszyny Wirtualnej i również ich szyfrowania. Na przykład pozwala dodać drugi wirtualny dysk do maszyny Wirtualnej w następujący sposób:

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

Uruchom ponownie polecenie do szyfrowania dysków wirtualnych w następujący sposób:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat zarządzania usługą Azure Key Vault, łącznie z usunięciem kluczy kryptograficznych i magazyny, zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](../../key-vault/key-vault-manage-with-cli2.md).
* Aby uzyskać więcej informacji o szyfrowaniu dysków, takich jak przygotowywanie zaszyfrowanego niestandardowego maszyny Wirtualnej do przekazania do platformy Azure, zobacz [szyfrowania dysków Azure](../../security/azure-security-disk-encryption.md).
