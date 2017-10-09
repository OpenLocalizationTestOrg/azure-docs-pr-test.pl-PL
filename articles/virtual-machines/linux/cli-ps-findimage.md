---
title: aaaSelect maszyny Wirtualnej systemu Linux obrazy z hello Azure CLI | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello Azure CLI toodetermine hello wydawcy, oferty, jednostki SKU i wersji dla obrazów maszyn wirtualnych w witrynie Marketplace."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a><span data-ttu-id="bac58-103">Jak obrazy toofind maszyny Wirtualnej systemu Linux w programie hello Azure Marketplace z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bac58-103">How toofind Linux VM images in hello Azure Marketplace with hello Azure CLI</span></span>
<span data-ttu-id="bac58-104">W tym temacie opisano, jak toouse hello Azure CLI 2.0 obrazów maszyn wirtualnych toofind w hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bac58-104">This topic describes how toouse hello Azure CLI 2.0 toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="bac58-105">Użyj tej informacji toospecify obrazu z witryny Marketplace, tworząc Maszynę wirtualną systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="bac58-105">Use this information toospecify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="bac58-106">Upewnij się, że zainstalowane w najnowszej hello [Azure CLI 2.0](/cli/azure/install-az-cli2) i są rejestrowane w tooan konto platformy Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="bac58-106">Make sure that you installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in tooan Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="bac58-107">Terminologia</span><span class="sxs-lookup"><span data-stu-id="bac58-107">Terminology</span></span>

<span data-ttu-id="bac58-108">Obrazy Marketplace są identyfikowane w hello interfejsu wiersza polecenia i innych narzędzi platformy Azure, zgodnie z tooa hierarchii:</span><span class="sxs-lookup"><span data-stu-id="bac58-108">Marketplace images are identified in hello CLI and other Azure tools according tooa hierarchy:</span></span>

* <span data-ttu-id="bac58-109">**Wydawca** — Witaj organizacji, który utworzył obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="bac58-109">**Publisher** - hello organization that created hello image.</span></span> <span data-ttu-id="bac58-110">Przykład: kanoniczny</span><span class="sxs-lookup"><span data-stu-id="bac58-110">Example: Canonical</span></span>
* <span data-ttu-id="bac58-111">**Oferują** -grupa powiązanych obrazy utworzone przez wydawcę.</span><span class="sxs-lookup"><span data-stu-id="bac58-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="bac58-112">Przykład: Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="bac58-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="bac58-113">**Jednostka SKU** — wystąpienie oferty, takie jak wydaniem dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="bac58-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="bac58-114">Przykład: 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="bac58-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="bac58-115">**Wersja** — Witaj numer wersji jednostki SKU obrazu.</span><span class="sxs-lookup"><span data-stu-id="bac58-115">**Version** - hello version number of an image SKU.</span></span> <span data-ttu-id="bac58-116">Podczas określania obrazu hello, numer wersji hello z można zastąpić "najnowszej", który wybiera hello najnowszą wersję dystrybucji hello.</span><span class="sxs-lookup"><span data-stu-id="bac58-116">When specifying hello image, you can replace hello version number with "latest", which selects hello latest version of hello distribution.</span></span>

<span data-ttu-id="bac58-117">toospecify obrazu z witryny Marketplace, używane zwykle obraz powitania *URN*.</span><span class="sxs-lookup"><span data-stu-id="bac58-117">toospecify a Marketplace image, you typically use hello image *URN*.</span></span> <span data-ttu-id="bac58-118">te wartości, rozdzielone znakiem dwukropka (:) hello łączy Hello URN: *wydawcy*:*oferują*:*Sku*:*wersji*.</span><span class="sxs-lookup"><span data-stu-id="bac58-118">hello URN combines these values, separated by hello colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="bac58-119">Listy obrazów popularnych</span><span class="sxs-lookup"><span data-stu-id="bac58-119">List popular images</span></span>

<span data-ttu-id="bac58-120">Uruchom hello [listy obrazów maszyny wirtualnej az](/cli/azure/vm/image#list) polecenia bez hello `--all` opcji, toosee obrazy listę popularnych maszyny Wirtualnej w programie hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bac58-120">Run hello [az vm image list](/cli/azure/vm/image#list) command, without hello `--all` option, toosee a list of popular VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="bac58-121">Na przykład uruchom następujące polecenie toodisplay hello buforowaną listę popularnych obrazów w formacie tabeli:</span><span class="sxs-lookup"><span data-stu-id="bac58-121">For example, run hello following command toodisplay a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="bac58-122">Hello dane wyjściowe zawierają hello URN (hello wartość hello *Urn* kolumny), który możesz użyć obrazu hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="bac58-122">hello output includes hello URN (hello value in hello *Urn* column), which you use toospecify hello image.</span></span> <span data-ttu-id="bac58-123">Podczas tworzenia maszyny Wirtualnej przy użyciu jednej z tych popularnych obrazów Marketplace, można alternatywnie określić hello URN aliasu, takich jak *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="bac58-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify hello URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a><span data-ttu-id="bac58-124">Znajdowanie określonych obrazów</span><span class="sxs-lookup"><span data-stu-id="bac58-124">Find specific images</span></span>

<span data-ttu-id="bac58-125">toofind określonego obrazu maszyny Wirtualnej w hello Marketplace, użyj hello `az vm image list` z hello `--all` opcji.</span><span class="sxs-lookup"><span data-stu-id="bac58-125">toofind a specific VM image in hello Marketplace, use hello `az vm image list` command with hello `--all` option.</span></span> <span data-ttu-id="bac58-126">Ta wersja polecenia hello przyjmuje niektórych toocomplete czasu i może zwrócić długich danych wyjściowych, co zwykle filtrowanie listy hello `--publisher` lub inny parametr.</span><span class="sxs-lookup"><span data-stu-id="bac58-126">This version of hello command takes some time toocomplete and can return lengthy output, so you usually filter hello list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="bac58-127">Na przykład następujące polecenie hello Wyświetla wszystkie oferty Debian (należy pamiętać, że bez hello `--all` przełącznika, tylko wyszukuje hello lokalnej pamięci podręcznej obrazów wspólnej):</span><span class="sxs-lookup"><span data-stu-id="bac58-127">For example, hello following command displays all Debian offers (remember that without hello `--all` switch, it only searches hello local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="bac58-128">Częściowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bac58-128">Partial output:</span></span> 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

<span data-ttu-id="bac58-129">Stosowanie filtrów podobne z hello `--location`, `--publisher`, i `--sku` opcje.</span><span class="sxs-lookup"><span data-stu-id="bac58-129">Apply similar filters with hello `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="bac58-130">Wyniki pasujące częściowo można wykonywać nawet w filtrze, takie jak wyszukiwanie `--offer Deb` toofind wszystkie obrazy Debian.</span><span class="sxs-lookup"><span data-stu-id="bac58-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` toofind all Debian images.</span></span>

<span data-ttu-id="bac58-131">Jeśli nie określisz określonej lokalizacji z hello `--location` opcji wartości hello `westus` zwracane są domyślnie.</span><span class="sxs-lookup"><span data-stu-id="bac58-131">If you don't specify a particular location with hello `--location` option, hello values for `westus` are returned by default.</span></span> <span data-ttu-id="bac58-132">(Ustaw domyślną inną lokalizację, uruchamiając `az configure --defaults location=<location>`.)</span><span class="sxs-lookup"><span data-stu-id="bac58-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="bac58-133">Na przykład hello następujące polecenie wyświetla listę wszystkich Debian SKU 8 w `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="bac58-133">For example, hello following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="bac58-134">Częściowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bac58-134">Partial output:</span></span>

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-hello-images"></a><span data-ttu-id="bac58-135">Przejdź hello obrazów</span><span class="sxs-lookup"><span data-stu-id="bac58-135">Navigate hello images</span></span> 
<span data-ttu-id="bac58-136">Inny sposób toofind obrazu w lokalizacji jest toorun hello [obrazu maszyny wirtualnej az listy wydawców](/cli/azure/vm/image#list-publishers), [obrazu maszyny wirtualnej az listy oferty](/cli/azure/vm/image#list-offers), i [obrazu maszyny wirtualnej az listy SKU](/cli/azure/vm/image#list-skus) polecenia w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="bac58-136">Another way toofind an image in a location is toorun hello [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="bac58-137">Przy użyciu następujących poleceń można określić te wartości:</span><span class="sxs-lookup"><span data-stu-id="bac58-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="bac58-138">Lista wydawców obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="bac58-138">List hello image publishers.</span></span>
2. <span data-ttu-id="bac58-139">Dla danego wydawcy wyświetl listę ofert.</span><span class="sxs-lookup"><span data-stu-id="bac58-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="bac58-140">Dla danej oferty wyświetl listę wersji SKU.</span><span class="sxs-lookup"><span data-stu-id="bac58-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="bac58-141">Na przykład hello następujące polecenie wyświetla listę wydawców obraz powitania w hello lokalizacji zachodnie stany USA:</span><span class="sxs-lookup"><span data-stu-id="bac58-141">For example, hello following command lists hello image publishers in hello West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="bac58-142">Częściowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bac58-142">Partial output:</span></span>

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
<span data-ttu-id="bac58-143">Użyj tego toofind informacji oferuje od określonego wydawcy.</span><span class="sxs-lookup"><span data-stu-id="bac58-143">Use this information toofind offers from a specific publisher.</span></span> <span data-ttu-id="bac58-144">Na przykład jeśli Canonical wydawcy obrazu w hello lokalizacji zachodnie stany USA, Znajdź ofert uruchamiając `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="bac58-144">For example, if Canonical is an image publisher in hello West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="bac58-145">Przekaż hello lokalizacji i wydawcy hello jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="bac58-145">Pass hello location and hello publisher as in hello following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="bac58-146">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bac58-146">Output:</span></span>

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
<span data-ttu-id="bac58-147">Zostanie wyświetlony w hello regionu zachodnie stany USA, Canonical publikuje hello **UbuntuServer** oferują na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="bac58-147">You see that in hello West US region, Canonical publishes hello **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="bac58-148">Jakie wersje produktu, ale? Uruchom te wartości tooget `azure vm image list-skus` i Ustaw lokalizację hello, wydawcy i oferty, które zostały odnalezione:</span><span class="sxs-lookup"><span data-stu-id="bac58-148">But what SKUs? tooget those values, run `azure vm image list-skus` and set hello location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="bac58-149">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bac58-149">Output:</span></span>

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

<span data-ttu-id="bac58-150">Na koniec użyj hello `az vm image list` toofind polecenia określonej wersji hello wersję produktu, na przykład **16.04 LTS**:</span><span class="sxs-lookup"><span data-stu-id="bac58-150">Finally, use hello `az vm image list` command toofind a specific version of hello SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="bac58-151">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bac58-151">Output:</span></span>

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a><span data-ttu-id="bac58-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bac58-152">Next steps</span></span>
<span data-ttu-id="bac58-153">Teraz można wybrać dokładnie hello obraz ma toouse przez biorąc pod uwagę hello URN wartość.</span><span class="sxs-lookup"><span data-stu-id="bac58-153">Now you can choose precisely hello image you want toouse by taking note of hello URN value.</span></span> <span data-ttu-id="bac58-154">Przekaż tę wartość z hello `--image` parametru podczas tworzenia maszyny Wirtualnej z hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="bac58-154">Pass this value with hello `--image` parameter when you create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="bac58-155">Należy pamiętać, że można opcjonalnie zastąpić numeru wersji hello hello URN "najnowszej".</span><span class="sxs-lookup"><span data-stu-id="bac58-155">Remember that you can optionally replace hello version number in hello URN with "latest".</span></span> <span data-ttu-id="bac58-156">Ta wersja jest zawsze hello najnowszą wersję hello dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="bac58-156">This version is always hello latest version of hello distribution.</span></span> <span data-ttu-id="bac58-157">toocreate maszynę wirtualną, szybko, używając hello URN informacji, zobacz [tworzenie i zarządzanie maszyn wirtualnych systemu Linux z hello Azure CLI](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="bac58-157">toocreate a virtual machine quickly by using hello URN information, see [Create and Manage Linux VMs with hello Azure CLI](tutorial-manage-vm.md).</span></span>
