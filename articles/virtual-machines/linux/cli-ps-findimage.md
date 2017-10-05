---
title: "Wybierz obrazów maszyny Wirtualnej systemu Linux za pomocą wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać interfejsu wiersza polecenia Azure w celu określenia wydawcy, oferty, jednostki SKU i wersji dla obrazów maszyn wirtualnych w witrynie Marketplace."
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
ms.openlocfilehash: e0c27a7ee9e9a7ab1a3b004e070fa556b56a36a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-find-linux-vm-images-in-the-azure-marketplace-with-the-azure-cli"></a><span data-ttu-id="289d1-103">Jak znaleźć maszyny Wirtualnej systemu Linux obrazów w portalu Azure Marketplace z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="289d1-103">How to find Linux VM images in the Azure Marketplace with the Azure CLI</span></span>
<span data-ttu-id="289d1-104">W tym temacie opisano sposób użycia 2.0 interfejsu wiersza polecenia platformy Azure można znaleźć obrazów maszyn wirtualnych w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="289d1-104">This topic describes how to use the Azure CLI 2.0 to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="289d1-105">Dzięki tym informacjom można określić obrazu z witryny Marketplace, podczas tworzenia maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="289d1-105">Use this information to specify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="289d1-106">Upewnij się, że jest zainstalowana najnowsza wersja [Azure CLI 2.0](/cli/azure/install-az-cli2) i zalogować się do konta platformy Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="289d1-106">Make sure that you installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in to an Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="289d1-107">Terminologia</span><span class="sxs-lookup"><span data-stu-id="289d1-107">Terminology</span></span>

<span data-ttu-id="289d1-108">Obrazy Marketplace są identyfikowane w interfejsu wiersza polecenia i innych narzędzi platformy Azure zgodnie z hierarchii:</span><span class="sxs-lookup"><span data-stu-id="289d1-108">Marketplace images are identified in the CLI and other Azure tools according to a hierarchy:</span></span>

* <span data-ttu-id="289d1-109">**Wydawca** -organizacji, który utworzył obraz.</span><span class="sxs-lookup"><span data-stu-id="289d1-109">**Publisher** - The organization that created the image.</span></span> <span data-ttu-id="289d1-110">Przykład: kanoniczny</span><span class="sxs-lookup"><span data-stu-id="289d1-110">Example: Canonical</span></span>
* <span data-ttu-id="289d1-111">**Oferują** -grupa powiązanych obrazy utworzone przez wydawcę.</span><span class="sxs-lookup"><span data-stu-id="289d1-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="289d1-112">Przykład: Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="289d1-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="289d1-113">**Jednostka SKU** — wystąpienie oferty, takie jak wydaniem dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="289d1-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="289d1-114">Przykład: 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="289d1-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="289d1-115">**Wersja** — numer wersji jednostki SKU obrazu.</span><span class="sxs-lookup"><span data-stu-id="289d1-115">**Version** - The version number of an image SKU.</span></span> <span data-ttu-id="289d1-116">Podczas określania obrazu, można zastąpić numer wersji z "najnowszej", który wybiera najnowszej wersji programu dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="289d1-116">When specifying the image, you can replace the version number with "latest", which selects the latest version of the distribution.</span></span>

<span data-ttu-id="289d1-117">Aby określić obrazu z witryny Marketplace, zwykle użyć obrazu *URN*.</span><span class="sxs-lookup"><span data-stu-id="289d1-117">To specify a Marketplace image, you typically use the image *URN*.</span></span> <span data-ttu-id="289d1-118">Nazwy URN łączy tych wartości, rozdzielone znakiem dwukropka (:): *wydawcy*:*oferują*:*Sku*:*wersji*.</span><span class="sxs-lookup"><span data-stu-id="289d1-118">The URN combines these values, separated by the colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="289d1-119">Listy obrazów popularnych</span><span class="sxs-lookup"><span data-stu-id="289d1-119">List popular images</span></span>

<span data-ttu-id="289d1-120">Uruchom [listy obrazów maszyny wirtualnej az](/cli/azure/vm/image#list) polecenia bez `--all` opcję, aby wyświetlić listę popularnych obrazów maszyn wirtualnych w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="289d1-120">Run the [az vm image list](/cli/azure/vm/image#list) command, without the `--all` option, to see a list of popular VM images in the Azure Marketplace.</span></span> <span data-ttu-id="289d1-121">Na przykład uruchom następujące polecenie, aby wyświetlić listę buforowanych popularnych obrazów w formacie tabeli:</span><span class="sxs-lookup"><span data-stu-id="289d1-121">For example, run the following command to display a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="289d1-122">Dane wyjściowe zawiera nazwy URN (wartość w *Urn* kolumny), który służy do określania obrazu.</span><span class="sxs-lookup"><span data-stu-id="289d1-122">The output includes the URN (the value in the *Urn* column), which you use to specify the image.</span></span> <span data-ttu-id="289d1-123">Podczas tworzenia maszyny Wirtualnej przy użyciu jednej z tych popularnych obrazów Marketplace, można alternatywnie określić aliasu URN, takie jak *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="289d1-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify the URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
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

## <a name="find-specific-images"></a><span data-ttu-id="289d1-124">Znajdowanie określonych obrazów</span><span class="sxs-lookup"><span data-stu-id="289d1-124">Find specific images</span></span>

<span data-ttu-id="289d1-125">Aby znaleźć określony obraz maszyny Wirtualnej w portalu Marketplace, użyj `az vm image list` z `--all` opcji.</span><span class="sxs-lookup"><span data-stu-id="289d1-125">To find a specific VM image in the Marketplace, use the `az vm image list` command with the `--all` option.</span></span> <span data-ttu-id="289d1-126">Ta wersja polecenia wymaga pewnego czasu do zakończenia i mogą zwracać długich danych wyjściowych, dlatego zazwyczaj przefiltrować listę wg `--publisher` lub inny parametr.</span><span class="sxs-lookup"><span data-stu-id="289d1-126">This version of the command takes some time to complete and can return lengthy output, so you usually filter the list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="289d1-127">Na przykład następujące polecenie wyświetla wszystkie oferty Debian (należy pamiętać, że bez `--all` przełącznika, przeszukiwane tylko w lokalnej pamięci podręcznej obrazów wspólnej):</span><span class="sxs-lookup"><span data-stu-id="289d1-127">For example, the following command displays all Debian offers (remember that without the `--all` switch, it only searches the local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="289d1-128">Częściowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="289d1-128">Partial output:</span></span> 
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

<span data-ttu-id="289d1-129">Stosowanie filtrów podobne z `--location`, `--publisher`, i `--sku` opcje.</span><span class="sxs-lookup"><span data-stu-id="289d1-129">Apply similar filters with the `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="289d1-130">Wyniki pasujące częściowo można wykonywać nawet w filtrze, takie jak wyszukiwanie `--offer Deb` można znaleźć wszystkie obrazy Debian.</span><span class="sxs-lookup"><span data-stu-id="289d1-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` to find all Debian images.</span></span>

<span data-ttu-id="289d1-131">Jeśli nie określisz określonej lokalizacji z `--location` opcji wartości `westus` zwracane są domyślnie.</span><span class="sxs-lookup"><span data-stu-id="289d1-131">If you don't specify a particular location with the `--location` option, the values for `westus` are returned by default.</span></span> <span data-ttu-id="289d1-132">(Ustaw domyślną inną lokalizację, uruchamiając `az configure --defaults location=<location>`.)</span><span class="sxs-lookup"><span data-stu-id="289d1-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="289d1-133">Na przykład następujące polecenie wyświetla listę wszystkich Debian SKU 8 w `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="289d1-133">For example, the following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="289d1-134">Częściowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="289d1-134">Partial output:</span></span>

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

## <a name="navigate-the-images"></a><span data-ttu-id="289d1-135">Przejdź obrazów</span><span class="sxs-lookup"><span data-stu-id="289d1-135">Navigate the images</span></span> 
<span data-ttu-id="289d1-136">Innym sposobem znajdowania obrazu w lokalizacji jest uruchomienie [obrazu maszyny wirtualnej az listy wydawców](/cli/azure/vm/image#list-publishers), [obrazu maszyny wirtualnej az listy oferty](/cli/azure/vm/image#list-offers), i [obrazu maszyny wirtualnej az listy SKU](/cli/azure/vm/image#list-skus) polecenia w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="289d1-136">Another way to find an image in a location is to run the [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="289d1-137">Przy użyciu następujących poleceń można określić te wartości:</span><span class="sxs-lookup"><span data-stu-id="289d1-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="289d1-138">Wyświetl listę wydawców obrazów.</span><span class="sxs-lookup"><span data-stu-id="289d1-138">List the image publishers.</span></span>
2. <span data-ttu-id="289d1-139">Dla danego wydawcy wyświetl listę ofert.</span><span class="sxs-lookup"><span data-stu-id="289d1-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="289d1-140">Dla danej oferty wyświetl listę wersji SKU.</span><span class="sxs-lookup"><span data-stu-id="289d1-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="289d1-141">Na przykład następujące polecenie wyświetla listę wydawców obrazu w lokalizacji zachodnie stany USA:</span><span class="sxs-lookup"><span data-stu-id="289d1-141">For example, the following command lists the image publishers in the West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="289d1-142">Częściowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="289d1-142">Partial output:</span></span>

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
<span data-ttu-id="289d1-143">Dzięki tym informacjom można znaleźć ofert od określonego wydawcy.</span><span class="sxs-lookup"><span data-stu-id="289d1-143">Use this information to find offers from a specific publisher.</span></span> <span data-ttu-id="289d1-144">Na przykład jeśli Canonical wydawcy obrazu w lokalizacji zachodnie stany USA, Znajdź ofert uruchamiając `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="289d1-144">For example, if Canonical is an image publisher in the West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="289d1-145">Przekaż lokalizacji i wydawcy, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="289d1-145">Pass the location and the publisher as in the following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="289d1-146">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="289d1-146">Output:</span></span>

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
<span data-ttu-id="289d1-147">Zobacz, czy w regionu zachodnie stany USA Canonical publikuje **UbuntuServer** oferują na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="289d1-147">You see that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="289d1-148">Ale o jakie wersje SKU chodzi?</span><span class="sxs-lookup"><span data-stu-id="289d1-148">But what SKUs?</span></span> <span data-ttu-id="289d1-149">Aby uzyskać te wartości, należy uruchomić `azure vm image list-skus` i Ustaw lokalizację, wydawcy i oferty, które zostały odnalezione:</span><span class="sxs-lookup"><span data-stu-id="289d1-149">To get those values, run `azure vm image list-skus` and set the location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="289d1-150">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="289d1-150">Output:</span></span>

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

<span data-ttu-id="289d1-151">Na koniec użyj `az vm image list` polecenia, można znaleźć określonej wersji jednostki SKU, na przykład **16.04 LTS**:</span><span class="sxs-lookup"><span data-stu-id="289d1-151">Finally, use the `az vm image list` command to find a specific version of the SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="289d1-152">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="289d1-152">Output:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="289d1-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="289d1-153">Next steps</span></span>
<span data-ttu-id="289d1-154">Teraz można precyzyjnie obraz, który ma być używany przez biorąc pod uwagę wartość URN.</span><span class="sxs-lookup"><span data-stu-id="289d1-154">Now you can choose precisely the image you want to use by taking note of the URN value.</span></span> <span data-ttu-id="289d1-155">Przekaż tę wartość z `--image` parametru podczas tworzenia maszyny Wirtualnej z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="289d1-155">Pass this value with the `--image` parameter when you create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="289d1-156">Należy pamiętać, że można opcjonalnie zastąpić numeru wersji w nazwy URN "r".</span><span class="sxs-lookup"><span data-stu-id="289d1-156">Remember that you can optionally replace the version number in the URN with "latest".</span></span> <span data-ttu-id="289d1-157">Ta wersja jest zawsze najnowszą wersję dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="289d1-157">This version is always the latest version of the distribution.</span></span> <span data-ttu-id="289d1-158">Aby szybko utworzyć maszynę wirtualną, korzystając z informacji URN, zobacz [tworzenie i zarządzanie maszyn wirtualnych systemu Linux z wiersza polecenia platformy Azure](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="289d1-158">To create a virtual machine quickly by using the URN information, see [Create and Manage Linux VMs with the Azure CLI](tutorial-manage-vm.md).</span></span>
