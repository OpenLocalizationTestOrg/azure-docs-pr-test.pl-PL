---
title: "aaaEncrypt dysków na Maszynę wirtualną systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak tooencrypt dysków wirtualnych na maszynę Wirtualną systemu Linux przy użyciu zwiększone zabezpieczenia hello Azure CLI 2.0"
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
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a>Jak tooencrypt dysków wirtualnych na Maszynę wirtualną systemu Linux
Ulepszone maszyny wirtualnej (VM) zabezpieczeń i zgodności mogą być szyfrowane dyski wirtualne na platformie Azure. Dyski są szyfrowane za pomocą kluczy kryptograficznych, które są już zabezpieczone w usłudze Azure Key Vault. Kontrolowanie tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania. W tym artykule szczegółowo sposób tooencrypt dysków wirtualnych na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 2.0. Można również wykonać te kroki hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Szybkie polecenia
Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły hello podstawowej polecenia tooencrypt dyski wirtualne na maszynie Wirtualnej. Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](#overview-of-disk-encryption).

Najnowsza wersja należy hello [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login). Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup*, *klucze*, i *myVM*.

Najpierw włączyć hello dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure z [az dostawcy rejestru](/cli/azure/provider#register) i utworzyć nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy nazwę grupy zasobów *myResourceGroup* w hello *eastus* lokalizacji:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Tworzenie usługi Azure Key Vault z [az keyvault utworzyć](/cli/azure/keyvault#create) i Włącz hello Key Vault służących do szyfrowania dysku. Określ unikatową nazwę usługi Key Vault *keyvault_name* w następujący sposób:

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Tworzenie klucza kryptograficznego w magazyn kluczy o [Utwórz klucz keyvault az](/cli/azure/keyvault/key#create). Witaj poniższym przykładzie jest tworzony klucz o nazwie *klucze*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

Tworzenie nazwy głównej usługi za pomocą usługi Azure Active Directory z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac). uchwyty główna usługi Hello hello uwierzytelniania i wymiany kluczy kryptograficznych z magazynu kluczy. Poniższy przykład Hello odczytuje hello wartości dla nazwy głównej usługi hello Id i hasło do użycia w poleceniach nowsze:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

hasło Hello jest tylko dane wyjściowe w przypadku tworzenia hello nazwy głównej usługi. W razie potrzeby, widok i rejestrowanie hello hasła (`echo $sp_password`). Możesz wyświetlić listę Twojej nazwy główne usług z [listy sp ad az](/cli/azure/ad/sp#list) i wyświetlić dodatkowe informacje o określonej usługi głównej z [az ad sp Pokaż](/cli/azure/ad/sp#show).

Ustaw uprawnienia na magazyn kluczy o [keyvault az set-policy](/cli/azure/keyvault#set-policy). W hello poniższy przykład hello usługi identyfikator podmiotu zabezpieczeń jest dostarczana z hello poprzedzających polecenia:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) i dołączenie dysku danych 5 Gb. Niektóre obrazy marketplace obsługuje szyfrowanie dysków. Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu **CentOS 7.2n** obrazu:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour maszynę Wirtualną przy użyciu hello `publicIpAddress` wyświetlany w danych wyjściowych hello hello poprzedzających polecenia. Tworzenie partycji i systemu plików, a następnie zainstalować dysk danych hello. Aby uzyskać więcej informacji, zobacz [połączyć tooa maszyny Wirtualnej systemu Linux toomount hello nowy dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Zamknij sesję SSH.

Szyfrowanie maszyny Wirtualnej z [włączyć szyfrowanie maszyny wirtualnej az](/cli/azure/vm/encryption#enable). Witaj poniższym przykładzie użyto hello `$sp_id` i `$sp_password` zmienne z poprzednim hello `ad sp create-for-rbac` polecenia:

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

Trwa trochę czasu, zanim toocomplete proces szyfrowania dysku hello. Monitorowanie stanu hello hello procesu z [Pokaż szyfrowania maszyny wirtualnej az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Witaj pokazuje stan **EncryptionInProgress**. Zaczekaj na stan hello raportów dysku systemu operacyjnego hello **VMRestartPending**, ponowne uruchomienie maszyny Wirtualnej z [ponownego uruchomienia maszyny wirtualnej az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Witaj procesu szyfrowania dysku zostanie sfinalizowana podczas procesu rozruchu hello, więc odczekaj kilka minut przed sprawdzeniem stanu hello szyfrowania ponownie, podając **Pokaż szyfrowania maszyny wirtualnej az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Stan Hello teraz Zgłoś dyskach hello systemu operacyjnego i dysku danych jako **zaszyfrowane**.

## <a name="overview-of-disk-encryption"></a>Omówienie szyfrowania dysków
Dyski wirtualne na maszynach wirtualnych systemu Linux są szyfrowane za pomocą rest [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Jest bezpłatna dla szyfrowania dysków wirtualnych na platformie Azure. Klucze szyfrowania są przechowywane w usługi Azure Key Vault przy użyciu ochrony oprogramowania, lub możesz zaimportować lub wygenerować klucze w sprzętowych modułach zabezpieczeń (HSM) certyfikowane tooFIPS 140-2 poziom 2 standardów. Zachowanie kontroli nad tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania. Te klucze szyfrowania są używane tooencrypt i odszyfrowywania tooyour dołączonych dysków wirtualnych maszyny Wirtualnej. Nazwy głównej usługi Azure Active Directory zapewnia mechanizm bezpiecznego do wystawiania tych kluczy kryptograficznych, ponieważ maszyny wirtualne są zasilane i wyłączanie.

proces Hello szyfrowania maszyny Wirtualnej przebiega w następujący sposób:

1. Tworzenie klucza kryptograficznego w usłudze Azure Key Vault.
2. Skonfiguruj hello kryptograficznych klucza toobe można używać do szyfrowania dysków.
3. klucz kryptograficzny hello tooread z hello Azure Key Vault, Utwórz usługę Azure Active Directory podmiotu zabezpieczeń z odpowiednimi uprawnieniami hello.
4. Wystawiać tooencrypt polecenia hello wirtualnych dysków, określenie nazwy głównej usługi Azure Active Directory hello i odpowiednie toobe klucza kryptograficznego używane.
5. główne żądania usługi Azure Active Directory Hello hello wymaganego klucza kryptograficznego z usługi Azure Key Vault.
6. dyski wirtualne Hello są szyfrowane za pomocą klucza kryptograficznego hello podane.

## <a name="encryption-process"></a>Proces szyfrowania
Szyfrowanie dysków opiera się na powitania następujące dodatkowe składniki:

* **Usługa Azure Key Vault** — używane toosafeguard kluczy kryptograficznych i kluczy tajnych używane podczas procesu szyfrowania i odszyfrowywania dysku hello.
  * Jeśli istnieje, można użyć istniejącego magazynu kluczy Azure. Nie masz toodedicate dysków tooencrypting magazynu kluczy.
  * granice administracyjne tooseparate i widoczności klucza, można utworzyć dedykowane Key Vault.
* **Usługa Azure Active Directory** — Witaj uchwytów bezpiecznej wymiany kluczy kryptograficznych wymagane i uwierzytelniania dla żądanej akcji.
  * Zazwyczaj można użyć istniejącego wystąpienia usługi Azure Active Directory, do przechowywania aplikacji.
  * nazwy głównej usługi Hello zapewnia toorequest mechanizmu bezpiecznego i wydawane hello odpowiednich kluczy kryptograficznych. Nie opracowujesz aplikację rzeczywista, która integruje się z usługą Azure Active Directory.

## <a name="requirements-and-limitations"></a>Wymagania i ograniczenia
Obsługiwane scenariusze i wymagania dotyczące szyfrowania dysków:

* powitania po Linux server jednostki SKU - Ubuntu, CentOS, SUSE i SUSE Linux Enterprise Server (SLES) i Red Hat Enterprise Linux.
* Wszystkie zasoby (na przykład usługi Key Vault, konta magazynu i maszyny Wirtualnej) musi być w hello tego samego regionu Azure i subskrypcji.
* Standardowa A, D DS, G i GS seria maszyn wirtualnych.

Szyfrowanie dysków nie jest obecnie obsługiwane w hello następujące scenariusze:

* Maszyny wirtualne warstwy podstawowa.
* Maszyny wirtualne utworzone za pomocą hello klasycznego modelu wdrożenia.
* Wyłączenie szyfrowania dysku systemu operacyjnego na maszynach wirtualnych systemu Linux.
* Aktualizowanie kluczy kryptograficznych hello na już zaszyfrowany maszyny Wirtualnej systemu Linux.

## <a name="create-azure-key-vault-and-keys"></a>Tworzenie usługi Azure Key Vault i kluczy
Najnowsza wersja należy hello [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login). Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup*, *klucze*, i *myVM*.

pierwszym krokiem Hello jest toocreate toostore usługi Azure Key Vault kluczy kryptograficznych. Usługa Azure Key Vault może przechowywać klucze i klucze tajne, lub haseł, które pozwalają toosecurely wdrożyć je w aplikacji i usług. Szyfrowanie dysków wirtualnych Użyj toostore Key Vault klucza kryptograficznego, który jest używany tooencrypt lub odszyfrować wirtualnych dysków.

Włącz hello dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure z [az dostawcy rejestru](/cli/azure/provider#register) i utworzyć nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy nazwę grupy zasobów *myResourceGroup* w hello `eastus` lokalizacji:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Hello Azure Key Vault zawierającego hello kluczy kryptograficznych i obliczeniowe skojarzone zasoby, takie jak magazyn i hello samej maszyny Wirtualnej musi znajdować się w hello tego samego regionu. Tworzenie usługi Azure Key Vault z [az keyvault utworzyć](/cli/azure/keyvault#create) i Włącz hello Key Vault służących do szyfrowania dysku. Określ unikatową nazwę usługi Key Vault *keyvault_name* w następujący sposób:

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Mogą być przechowywane przy użyciu oprogramowania lub sprzętu modelu zabezpieczeń (HSM) ochronę kluczy kryptograficznych. Użycie modułów HSM wymaga premium magazynu kluczy. Brak dodatkowych kosztów toocreating premium magazynu kluczy, a nie standardowy magazyn kluczy, którego przechowuje klucze chronione przez oprogramowanie. Dodaj premium usługi Key Vault w hello poprzedzających krok toocreate `--sku Premium` toohello polecenia. Witaj poniższym przykładzie użyto klucze chronione oprogramowaniem ponieważ utworzyliśmy standardowy magazyn kluczy.

W przypadku obu modeli ochrony hello platformy Azure musi toobe udzielać dostępu do kluczy kryptograficznych hello toorequest, w przypadku, gdy hello maszyny Wirtualnej wykonuje rozruch toodecrypt hello wirtualnych dysków. Tworzenie klucza kryptograficznego w magazyn kluczy o [Utwórz klucz keyvault az](/cli/azure/keyvault/key#create). Witaj poniższym przykładzie jest tworzony klucz o nazwie *klucze*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Utwórz hello nazwy głównej usługi Azure Active Directory
Gdy dyski wirtualne są szyfrowane lub odszyfrować, należy określić konto toohandle hello uwierzytelniania i wymiana kluczy kryptograficznych z magazynu kluczy. To konto, nazwy głównej usługi Azure Active Directory umożliwia toorequest platformy Azure hello hello odpowiednich kluczy kryptograficznych imieniu hello maszyny Wirtualnej. Domyślne wystąpienie usługi Azure Active Directory jest dostępne w Twojej subskrypcji, chociaż w wielu organizacjach są wyposażone w dedykowane katalogów usługi Azure Active Directory.

Tworzenie nazwy głównej usługi za pomocą usługi Azure Active Directory z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac). Poniższy przykład Hello odczytuje hello wartości dla nazwy głównej usługi hello Id i hasło do użycia w poleceniach nowsze:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

hasło Hello jest wyświetlana tylko po utworzeniu usługi hello podmiotu zabezpieczeń. W razie potrzeby, widok i rejestrowanie hello hasła (`echo $sp_password`). Możesz wyświetlić listę Twojej nazwy główne usług z [listy sp ad az](/cli/azure/ad/sp#list) i wyświetlić dodatkowe informacje o określonej usługi głównej z [az ad sp Pokaż](/cli/azure/ad/sp#show).

toosuccessfully zaszyfrować lub odszyfrować dysków wirtualnych, uprawnienia do klucza kryptograficznego hello przechowywane w magazynie klucza musi być klucze hello tooread główną usługi Azure Active Directory zestaw toopermit hello. Ustaw uprawnienia na magazyn kluczy o [keyvault az set-policy](/cli/azure/keyvault#set-policy). W hello poniższy przykład hello usługi identyfikator podmiotu zabezpieczeń jest dostarczana z hello poprzedzających polecenia:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej
tooactually szyfrowania niektóre dyski wirtualne, umożliwia tworzenie maszyny Wirtualnej i Dodaj dysk danych. Utwórz tooencrypt maszyny Wirtualnej, z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) i dołączenie dysku danych 5 Gb. Niektóre obrazy marketplace obsługuje szyfrowanie dysków. Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* przy użyciu **CentOS 7.2n** obrazu:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour maszynę Wirtualną przy użyciu hello `publicIpAddress` wyświetlany w danych wyjściowych hello hello poprzedzających polecenia. Tworzenie partycji i systemu plików, a następnie zainstalować dysk danych hello. Aby uzyskać więcej informacji, zobacz [połączyć tooa maszyny Wirtualnej systemu Linux toomount hello nowy dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Zamknij sesję SSH.


## <a name="encrypt-virtual-machine"></a>Szyfrowanie maszyny wirtualnej
dyski wirtualne hello tooencrypt, przełączeniem razem wszystkie poprzednie składniki hello:

1. Określ hello nazwy głównej usługi Azure Active Directory i hasło.
2. Określ hello Key Vault toostore hello metadanych dla zaszyfrowanych dysków.
3. Określ toouse kluczy kryptograficznych hello hello rzeczywiste szyfrowania i odszyfrowywania.
4. Określ, czy tooencrypt hello systemu operacyjnego, dysku dysków z danymi hello lub wszystkie.

Szyfrowanie maszyny Wirtualnej z [włączyć szyfrowanie maszyny wirtualnej az](/cli/azure/vm/encryption#enable). Witaj poniższym przykładzie użyto hello `$sp_id` i `$sp_password` zmienne z poprzednim hello `ad sp create-for-rbac` polecenia:

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

Trwa trochę czasu, zanim toocomplete proces szyfrowania dysku hello. Monitorowanie stanu hello hello procesu z [Pokaż szyfrowania maszyny wirtualnej az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Witaj danych wyjściowych jest toohello podobnie poniższy przykład skrócona:

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

Zaczekaj na stan hello raportów dysku systemu operacyjnego hello **VMRestartPending**, ponowne uruchomienie maszyny Wirtualnej z [ponownego uruchomienia maszyny wirtualnej az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Witaj procesu szyfrowania dysku zostanie sfinalizowana podczas procesu rozruchu hello, więc odczekaj kilka minut przed sprawdzeniem stanu hello szyfrowania ponownie, podając **Pokaż szyfrowania maszyny wirtualnej az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Stan Hello teraz Zgłoś dyskach hello systemu operacyjnego i dysku danych jako **zaszyfrowane**.


## <a name="add-additional-data-disks"></a>Dodania dodatkowego dysku z danymi
Po zaszyfrowanych dysków z danymi, możesz później dodać tooyour dodatkowych dysków wirtualnych maszyny Wirtualnej i również ich szyfrowania. Na przykład pozwala dodać drugi tooyour dysku wirtualnego maszyny Wirtualnej w następujący sposób:

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

Ponownie uruchom dysków wirtualnych tooencrypt hello hello polecenia w następujący sposób:

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
* Aby uzyskać więcej informacji o szyfrowaniu dysków, takich jak przygotowywanie zaszyfrowanego niestandardowego wirtualna tooupload tooAzure, zobacz [szyfrowania dysków Azure](../../security/azure-security-disk-encryption.md).
