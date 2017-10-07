---
title: "aaaEncrypt dysków na Maszynę wirtualną systemu Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Jak tooencrypt dysków na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 1.0 i modelu wdrażania usługi Resource Manager hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a>Szyfrowanie dysków na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI w wersji 1.0
Ulepszone maszyny wirtualnej (VM) zabezpieczeń i zgodności dyski wirtualne na platformie Azure mogą być szyfrowane w stanie spoczynku. Dyski są szyfrowane za pomocą kluczy kryptograficznych, które są już zabezpieczone w usłudze Azure Key Vault. Kontrolowanie tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania. W tym artykule szczegółowo sposób tooencrypt dysków wirtualnych na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 1.0 i modelu wdrażania usługi Resource Manager hello.

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello

## <a name="quick-commands"></a>Szybkie polecenia
Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły hello podstawowej polecenia tooencrypt dyski wirtualne na maszynie Wirtualnej. Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](#overview-of-disk-encryption).

Należy hello [najnowsze Azure CLI 1.0](../../xplat-cli-install.md) zainstalowane i rejestrowane w trybie hello Resource Manager w następujący sposób:

```azurecli
azure config mode arm
```

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają `myResourceGroup`, `myKeyVault`, i `myVM`.

Najpierw należy włączyć hello dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure i Utwórz grupę zasobów. Witaj poniższy przykład tworzy nazwę grupy zasobów `myResourceGroup` w hello `WestUS` lokalizacji:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Tworzenie usługi Azure Key Vault. Witaj poniższy przykład tworzy magazyn kluczy o nazwie `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Tworzenie klucza kryptograficznego w magazyn kluczy i Włącz szyfrowanie dysków. Witaj poniższym przykładzie jest tworzony klucz o nazwie `myKey`:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

Tworzenie punktu końcowego za pomocą usługi Azure Active Directory do obsługi uwierzytelniania hello i wymiana kluczy kryptograficznych z magazynu kluczy. Witaj `--home-page` i `--identifier-uris` nie ma potrzeby toobe rzeczywiste adresów obsługi routingu. W przypadku hello najwyższy poziom zabezpieczeń kluczy tajnych klientów należy użyć zamiast hasła. Witaj interfejsu wiersza polecenia Azure aktualnie nie można wygenerować kluczy tajnych klientów. Kluczy tajnych klientów mogą być generowane tylko w hello portalu Azure. Witaj poniższy przykład tworzy punkt końcowy usługi Azure Active Directory o nazwie `myAADApp` i używa hasła `myPassword`. Określ własnego hasła w następujący sposób:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Uwaga hello `applicationId` wyświetlany w danych wyjściowych hello z hello poprzedzających polecenia. Ten identyfikator aplikacji jest używany w hello następujące kroki:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

Dodawanie danych tooan dysku, istniejącej maszyny Wirtualnej. Witaj poniższy przykład umożliwia dodanie tooa dysku danych maszyny Wirtualnej o nazwie `myVM`:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Przejrzyj szczegóły hello klucza magazynu kluczy i hello utworzony. Należy hello identyfikator magazynu kluczy, identyfikator URI i klucz adres URL w ostatnim kroku hello. Witaj poniższy przykład przegląda hello szczegółów dla usługi Key Vault o nazwie `myKeyVault` i klucz o nazwie `myKey`:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Szyfrowanie dysków następujące wprowadzania własne nazwy parametru w całym:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Hello Azure CLI nie zapewnia pełne błędy podczas procesu szyfrowania hello. Aby uzyskać dodatkowe informacje dotyczące rozwiązywania problemów, przejrzyj `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`. Jako hello poprzedzających polecenie ma wiele zmiennych i nie może pobrać dużo oznaczenie toowhy hello proces zakończy się niepowodzeniem, przykład pełne polecenie będzie następujące:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Na koniec, sprawdź stan szyfrowania hello ponownie tooconfirm czy dyski wirtualne teraz zostały zaszyfrowane. Witaj poniższy przykład umożliwia sprawdzenie hello stanu maszyny wirtualnej o nazwie `myVM` w hello `myResourceGroup` grupy zasobów:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a>Omówienie szyfrowania dysków
Dyski wirtualne na maszynach wirtualnych systemu Linux są szyfrowane za pomocą rest [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Jest bezpłatna dla szyfrowania dysków wirtualnych na platformie Azure. Klucze szyfrowania są przechowywane w usługi Azure Key Vault przy użyciu ochrony oprogramowania, lub możesz zaimportować lub wygenerować klucze w sprzętowych modułach zabezpieczeń (HSM) certyfikowane tooFIPS 140-2 poziom 2 standardów. Zachowanie kontroli nad tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania. Te klucze szyfrowania są używane tooencrypt i odszyfrowywania tooyour dołączonych dysków wirtualnych maszyny Wirtualnej. Punkt końcowy usługi Azure Active Directory zapewnia mechanizm bezpiecznego do wystawiania tych kluczy kryptograficznych, ponieważ maszyny wirtualne są zasilane i wyłączanie.

proces Hello szyfrowania maszyny Wirtualnej przebiega w następujący sposób:

1. Tworzenie klucza kryptograficznego w usłudze Azure Key Vault.
2. Skonfiguruj hello kryptograficznych klucza toobe można używać do szyfrowania dysków.
3. klucz kryptograficzny hello tooread z hello Azure Key Vault, tworzenie punktu końcowego za pomocą usługi Azure Active Directory z odpowiednimi uprawnieniami hello.
4. Wystawiać tooencrypt polecenia hello wirtualnych dysków, określając punkt końcowy usługi Azure Active Directory hello i odpowiednie toobe klucza kryptograficznego używane.
5. punkt końcowy usługi Azure Active Directory Hello żądań hello wymaganego klucza kryptograficznego z usługi Azure Key Vault.
6. dyski wirtualne Hello są szyfrowane za pomocą klucza kryptograficznego hello podane.

## <a name="supporting-services-and-encryption-process"></a>Obsługa usług i proces szyfrowania
Szyfrowanie dysków opiera się na powitania następujące dodatkowe składniki:

* **Usługa Azure Key Vault** — używane toosafeguard kluczy kryptograficznych i kluczy tajnych używane podczas procesu szyfrowania i odszyfrowywania dysku hello.
  * Jeśli istnieje, można użyć istniejącego magazynu kluczy Azure. Nie masz toodedicate dysków tooencrypting magazynu kluczy.
  * granice administracyjne tooseparate i widoczności klucza, można utworzyć dedykowane Key Vault.
* **Usługa Azure Active Directory** — Witaj uchwytów bezpiecznej wymiany kluczy kryptograficznych wymagane i uwierzytelniania dla żądanej akcji.
  * Zazwyczaj można użyć istniejącego wystąpienia usługi Azure Active Directory, do przechowywania aplikacji.
  * Aplikacja Hello jest więcej punktu końcowego dla hello magazyn kluczy i maszyny wirtualnej usługi toorequest i pobrać wystawiony hello odpowiednich kluczy kryptograficznych. Nie opracowujesz aplikację rzeczywista, która integruje się z usługą Azure Active Directory.

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

## <a name="create-hello-azure-key-vault-and-keys"></a>Utwórz hello Azure Key Vault i kluczy
toocomplete hello pozostałej części tego przewodnika, należy hello [najnowsze Azure CLI 1.0](../../xplat-cli-install.md) zainstalowane i rejestrowane w trybie hello Resource Manager w następujący sposób:

```azurecli
azure config mode arm
```

W przykładach poleceń hello Zamień wszystkie parametry przykład własne nazwy, lokalizacji i wartości klucza. Witaj następujących przykładach użyto Konwencji `myResourceGroup`, `myKeyVault`, `myAADApp`itp.

pierwszym krokiem Hello jest toocreate toostore usługi Azure Key Vault kluczy kryptograficznych. Usługa Azure Key Vault może przechowywać klucze i klucze tajne, lub haseł, które pozwalają toosecurely wdrożyć je w aplikacji i usług. Szyfrowanie dysków wirtualnych Użyj toostore Key Vault klucza kryptograficznego, który jest używany tooencrypt lub odszyfrować wirtualnych dysków.

Włącz hello dostawcy usługi Azure Key Vault w Twojej subskrypcji platformy Azure, a następnie utwórz grupę zasobów. Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `WestUS` lokalizacji:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Hello Azure Key Vault zawierającego hello kluczy kryptograficznych i obliczeniowe skojarzone zasoby, takie jak magazyn i hello samej maszyny Wirtualnej musi znajdować się w hello tego samego regionu. Witaj poniższy przykład tworzy magazynu kluczy Azure o nazwie `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Mogą być przechowywane przy użyciu oprogramowania lub sprzętu modelu zabezpieczeń (HSM) ochronę kluczy kryptograficznych. Użycie modułów HSM wymaga premium magazynu kluczy. Brak dodatkowych kosztów toocreating premium magazynu kluczy, a nie standardowy magazyn kluczy, którego przechowuje klucze chronione przez oprogramowanie. Dodaj premium usługi Key Vault w hello poprzedzających krok toocreate `--sku Premium` toohello polecenia. Witaj poniższym przykładzie użyto klucze chronione oprogramowaniem ponieważ utworzyliśmy standardowy magazyn kluczy.

W przypadku obu modeli ochrony hello platformy Azure musi toobe udzielać dostępu do kluczy kryptograficznych hello toorequest, w przypadku, gdy hello maszyny Wirtualnej wykonuje rozruch toodecrypt hello wirtualnych dysków. Tworzenie klucza szyfrowania w ramach magazyn kluczy, a następnie włącz go do użytku z szyfrowania dysku wirtualnego. Witaj poniższym przykładzie jest tworzony klucz o nazwie `myKey` i umożliwia szyfrowanie dysków:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a>Utwórz aplikację usługi Azure Active Directory hello
Dyski wirtualne są szyfrowane lub odszyfrować, możesz korzystać z uwierzytelniania hello toohandle punktu końcowego i wymiana kluczy kryptograficznych z magazynu kluczy. Ten punkt końcowy, aplikację usługi Azure Active Directory umożliwia toorequest platformy Azure hello hello odpowiednich kluczy kryptograficznych imieniu hello maszyny Wirtualnej. Domyślne wystąpienie usługi Azure Active Directory jest dostępne w Twojej subskrypcji, chociaż w wielu organizacjach są wyposażone w dedykowane katalogów usługi Azure Active Directory.

Jak Pełna aplikacji usługi Azure Active Directory nie jest tworzony, hello `--home-page` i `--identifier-uris` parametry w poniższy przykład hello nie wymagają toobe rzeczywiste adresów obsługi routingu. Witaj poniższy przykład również określa klucz tajny opartego na hasłach zamiast generowania kluczy z wewnątrz hello portalu Azure. Teraz Generowanie kluczy nie można wykonać z hello wiersza polecenia platformy Azure.

Tworzenie aplikacji usługi Azure Active Directory. Witaj poniższy przykład tworzy aplikację o nazwie `myAADApp` i używa hasła `myPassword`. Określ własnego hasła w następujący sposób:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Zanotuj hello `applicationId` który jest zwracany w danych wyjściowych hello z hello poprzedzających polecenia. Ten identyfikator aplikacji jest używany w niektórych hello pozostałe kroki. Następnie należy utworzyć główną nazwę usługi (SPN), aby aplikacja hello jest dostępny w danym środowisku. toosuccessfully zaszyfrować lub odszyfrować dysków wirtualnych, uprawnienia do klucza kryptograficznego hello przechowywane w magazynie klucza musi być kluczy hello tooread zestaw toopermit hello Azure Active Directory aplikacji.

Utwórz hello SPN i ustaw odpowiednie uprawnienia hello w następujący sposób:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a>Dodaj dysk wirtualny i sprawdzać stan szyfrowania
tooactually szyfrowania niektóre dyski wirtualne, umożliwia dodawanie tooan dysku, istniejącej maszyny Wirtualnej. Dodaj 5Gb tooan dysku danych istniejących maszyn wirtualnych w następujący sposób:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

obecnie nie są szyfrowane Hello dysków wirtualnych. Przejrzyj hello bieżącego stanu szyfrowania maszyny Wirtualnej w następujący sposób:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a>Szyfrowanie dysków wirtualnych
toonow szyfrowania dysków wirtualnych hello, zebranie wszystkich hello poprzednie składniki:

1. Określ aplikację usługi Azure Active Directory hello i hasło.
2. Określ hello Key Vault toostore hello metadanych dla zaszyfrowanych dysków.
3. Określ toouse kluczy kryptograficznych hello hello rzeczywiste szyfrowania i odszyfrowywania.
4. Określ, czy tooencrypt hello systemu operacyjnego, dysku dysków z danymi hello lub wszystkie.

Umożliwia szczegółowe hello klucza usługi Azure Key Vault i hello utworzoną przez siebie jako hello identyfikator magazynu kluczy, identyfikator URI, a następnie klucza adresu URL w ostatnim kroku hello:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Szyfrowanie dysków wirtualnych przy użyciu hello dane wyjściowe hello `azure keyvault show` i `azure keyvault key show` polecenia w następujący sposób:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Witaj poprzednie polecenie zawiera wiele zmiennych, hello poniższy przykład jest pełne polecenie hello odwołania:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Hello Azure CLI nie zapewnia pełne błędy podczas procesu szyfrowania hello. Aby uzyskać dodatkowe informacje dotyczące rozwiązywania problemów, przejrzyj `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` na powitania Szyfrujesz maszyny Wirtualnej.

Ponadto pozwala sprawdzać stan szyfrowania hello ponownie tooconfirm czy teraz zostały zaszyfrowane dyski wirtualne:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a>Dodania dodatkowego dysku z danymi
Po zaszyfrowanych dysków z danymi, możesz później dodać tooyour dodatkowych dysków wirtualnych maszyny Wirtualnej i również ich szyfrowania. Po uruchomieniu hello `azure vm enable-disk-encryption` polecenia, wersję sekwencji hello przyrostu za pomocą hello `--sequence-version` parametru. Ten parametr wersji sekwencji umożliwia tooperform powtarzających się operacjach na hello tej samej maszyny Wirtualnej.

Na przykład pozwala dodać drugi tooyour dysku wirtualnego maszyny Wirtualnej w następujący sposób:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Uruchom ponownie teraz Dodawanie hello hello polecenia tooencrypt hello dysków wirtualnych, `--sequence-version` parametr i zwiększającą wartość hello z naszych najpierw uruchomić w następujący sposób:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat zarządzania usługą Azure Key Vault, łącznie z usunięciem kluczy kryptograficznych i magazyny, zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](../../key-vault/key-vault-manage-with-cli2.md).
* Aby uzyskać więcej informacji o szyfrowaniu dysków, takich jak przygotowywanie zaszyfrowanego niestandardowego wirtualna tooupload tooAzure, zobacz [szyfrowania dysków Azure](../../security/azure-security-disk-encryption.md).
