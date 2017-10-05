---
title: Red Hat aktualizacji infrastruktury (RHUI) | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o Red Hat aktualizacji infrastruktury (RHUI) dla wystąpień Red Hat Enterprise Linux na żądanie w systemie Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: 07815d691ffe57f0349f7a90ced4a2fcc1ab834f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="03c85-103">Red Hat aktualizacji infrastruktury (RHUI) na żądanie Red Hat Enterprise Linux w maszynach wirtualnych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="03c85-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="03c85-104">Maszyny wirtualne utworzone z obrazów Red Hat Enterprise Linux (RHEL) na żądanie dostępne w portalu Azure Marketplace jest zarejestrowany na dostęp Red Hat aktualizacji infrastruktury (RHUI) wdrożona na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="03c85-104">Virtual machines created from the on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered to access the Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="03c85-105">Wystąpienia na żądanie RHEL mieć dostęp do repozytorium yum regionalnych i może odbierać aktualizacje przyrostowe.</span><span class="sxs-lookup"><span data-stu-id="03c85-105">The on-demand RHEL instances have access to a regional yum repository and able to receive incremental updates.</span></span>

<span data-ttu-id="03c85-106">Na liście repozytorium yum, który jest zarządzany przez RHUI, jest skonfigurowany w wystąpieniu RHEL podczas inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="03c85-106">The yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="03c85-107">Nie musisz podejmować żadnych dodatkowych konfiguracji — Uruchom `yum update` po wystąpieniu RHEL jest gotowy do Pobierz najnowsze aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="03c85-107">You don't need to do any additional configuration - run `yum update` after your RHEL instance is ready to get the latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="03c85-108">We wrześniu 2016 r wdrożyliśmy zaktualizowane RHUI Azure i w stycznia 2017 możemy uruchomić etapowe zamknięcie starszych RHUI Azure.</span><span class="sxs-lookup"><span data-stu-id="03c85-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of the older Azure RHUI.</span></span> <span data-ttu-id="03c85-109">Jeśli był używany obrazów RHEL (lub migawki ich) od września 2016 lub nowszy - prawdopodobnie jest wymagana żadna akcja.</span><span class="sxs-lookup"><span data-stu-id="03c85-109">If you have been using the RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="03c85-110">Jeśli jednak masz starszą migawki/VMs, ich konfiguracji musi zostać zaktualizowany nieprzerwany dostęp do Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="03c85-110">If, however, you have older snapshots/VMs, their configuration needs to be updated for uninterrupted access to the Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="03c85-111">RHUI aktualizacji infrastruktury platformy Azure</span><span class="sxs-lookup"><span data-stu-id="03c85-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="03c85-112">Począwszy od września 2016 r. platforma Azure ma nowy zestaw serwerów Red Hat aktualizacji infrastruktury (RHUI).</span><span class="sxs-lookup"><span data-stu-id="03c85-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="03c85-113">Te serwery zostały wdrożone za pomocą [usługi Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) tak, aby jeden punkt końcowy (rhui 1.microsoft.com) mogą być używane przez żadnej maszyny Wirtualnej, niezależnie od tego regionu.</span><span class="sxs-lookup"><span data-stu-id="03c85-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="03c85-114">Nowych obrazów RHEL płatność za rzeczywiste użycie (między) w portalu Azure Marketplace (wersje z września 2016 lub nowszy) wskaż nowych serwerów Azure RHUI i nie wymagają żadnych dodatkowych działań.</span><span class="sxs-lookup"><span data-stu-id="03c85-114">The new RHEL Pay-As-You-Go (PAYG) images in the Azure Marketplace (versions dated September 2016 or later) point to the new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="03c85-115">Określić, jeśli jest wymagana akcja</span><span class="sxs-lookup"><span data-stu-id="03c85-115">Determine if action is required</span></span>
<span data-ttu-id="03c85-116">Jeśli występują problemy z połączeniem z maszyny Wirtualnej Azure RHEL między Azure RHUI, wykonaj następujące czynności</span><span class="sxs-lookup"><span data-stu-id="03c85-116">If you are experiencing problems connecting to Azure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="03c85-117">Sprawdź konfigurację maszyny Wirtualnej dla punktu końcowego Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="03c85-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="03c85-118">Sprawdź, czy `/etc/yum.repos.d/rh-cloud.repo` plik zawiera odwołanie do `rhui-[1-3].microsoft.com` w baseurl z `[rhui-microsoft-azure-rhel*]` sekcji pliku.</span><span class="sxs-lookup"><span data-stu-id="03c85-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference to `rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of the file.</span></span> <span data-ttu-id="03c85-119">— Jeśli używasz nowego RHUI Azure.</span><span class="sxs-lookup"><span data-stu-id="03c85-119">If it is - you are using the new Azure RHUI.</span></span>

    <span data-ttu-id="03c85-120">Jeśli go wskazuje lokalizację przy użyciu następującego wzorca `mirrorlist.*cds[1-4].cloudapp.net` — wymagana jest aktualizacja konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="03c85-120">If it pointing to a location with the following pattern `mirrorlist.*cds[1-4].cloudapp.net` - the configuration update is required.</span></span>

    <span data-ttu-id="03c85-121">Jeśli używasz nową konfigurację i nadal nie można połączyć się Azure RHUI - pliku sprawy pomocy technicznej firmy Microsoft lub Red Hat.</span><span class="sxs-lookup"><span data-stu-id="03c85-121">If you are using the new configuration and still cannot connect to Azure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="03c85-122">Dostęp do RHUI hostowanymi na platformie Azure jest ograniczona do maszyn wirtualnych w ramach [zakresy IP centrum danych Azure Microsoft](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="03c85-122">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="03c85-123">Jeśli stary RHUI Azure jest nadal dostępna, gdy zostanie w tym celu Sprawdź i chcesz automatycznie zaktualizować konfigurację, wykonaj następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="03c85-123">If the old Azure RHUI is still available when you do this check and you would like to automatically update the configuration, execute the following command:</span></span>

    <span data-ttu-id="03c85-124">`sudo yum update RHEL6`lub `sudo yum update RHEL7` w zależności od wersji rodziny RHEL.</span><span class="sxs-lookup"><span data-stu-id="03c85-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on the RHEL family version.</span></span>

3. <span data-ttu-id="03c85-125">Jeśli nie można nawiązać starego RHUI Azure, wykonaj ręcznie czynności opisane w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="03c85-125">If you can no longer connect to the old Azure RHUI, follow the manual steps described in the next section.</span></span>

4. <span data-ttu-id="03c85-126">Upewnij się zaktualizować konfigurację w źródle obrazu/migawki wpływ na udostępniony z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="03c85-126">Make sure to update the configuration on the source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-the-old-azure-rhui"></a><span data-ttu-id="03c85-127">Zamknięcie etapowe starego RHUI Azure</span><span class="sxs-lookup"><span data-stu-id="03c85-127">Phased shutdown of the old Azure RHUI</span></span>
<span data-ttu-id="03c85-128">Podczas zamykania starego RHUI Azure możemy ograniczyć dostęp do jej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="03c85-128">During the shutdown of the old Azure RHUI we restrict access to it as follows:</span></span>

1. <span data-ttu-id="03c85-129">Dalsze ograniczenie dostępu (ACL), aby ustawić adresów IP, które już połączenie z jego.</span><span class="sxs-lookup"><span data-stu-id="03c85-129">Further restrict access (ACL) to set of IP addresses that are already connecting to it.</span></span> <span data-ttu-id="03c85-130">Efekty uboczne: Jeśli będziesz kontynuować, przy użyciu starego RHUI Azure — nowych maszyn wirtualnych nie można połączyć się z nim.</span><span class="sxs-lookup"><span data-stu-id="03c85-130">Possible side-effects: if you continue using the old Azure RHUI - your new VMs may not be able to connect to it.</span></span> <span data-ttu-id="03c85-131">RHEL maszyny wirtualne z dynamicznych adresów IP, który przechodzi przez zamknięcie/cofnąć/start sekwencji może pojawić się nowego adresu IP i dlatego również można uruchomić brakiem połączenia między starym RHUI Azure</span><span class="sxs-lookup"><span data-stu-id="03c85-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing to connect to the old Azure RHUI</span></span>

2. <span data-ttu-id="03c85-132">Zamknięcie Serwery dublowane dostarczania zawartości.</span><span class="sxs-lookup"><span data-stu-id="03c85-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="03c85-133">Efekty uboczne: jak możemy zamknąć więcej CDSes może zostać wyświetlony już `yum update` obsługi czasu, więcej przekroczeń limitu czasu, aż do momentu, gdy nie można nawiązać starego RHUI Azure.</span><span class="sxs-lookup"><span data-stu-id="03c85-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until the point when you can no longer connect to the old Azure RHUI.</span></span>

### <a name="the-ips-for-the-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="03c85-134">Adresy IP dla nowych serwerów dostarczania zawartości RHUI są</span><span class="sxs-lookup"><span data-stu-id="03c85-134">The IPs for the new RHUI content delivery servers are</span></span>
<span data-ttu-id="03c85-135">Jeśli konfiguracja sieci używane są bardziej ograniczyć dostęp z maszyn wirtualnych między RHEL, upewnij się, że następujące adresy IP, są dozwolone dla `yum update` do pracy w zależności od środowiska są w.</span><span class="sxs-lookup"><span data-stu-id="03c85-135">If you are using network configuration to further restrict access from RHEL PAYG VMs, make sure the following IPs are allowed for `yum update` to work depending on the environment you are in.</span></span> 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-to-use-the-new-azure-rhui-servers"></a><span data-ttu-id="03c85-136">Procedura ręcznej aktualizacji do używania nowych serwerów Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="03c85-136">Manual update procedure to use the new Azure RHUI servers</span></span>
<span data-ttu-id="03c85-137">Pobierz (za pośrednictwem curl) podpis klucza publicznego</span><span class="sxs-lookup"><span data-stu-id="03c85-137">Download (via curl) the public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="03c85-138">Sprawdź klucz pobrany</span><span class="sxs-lookup"><span data-stu-id="03c85-138">Verify the downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="03c85-139">Sprawdź dane wyjściowe, sprawdź `keyid` i `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="03c85-139">Check the output, verify `keyid` and `user ID packet`:</span></span>

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

<span data-ttu-id="03c85-140">Zainstaluj klucz publiczny</span><span class="sxs-lookup"><span data-stu-id="03c85-140">Install the public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="03c85-141">Pobierz, sprawdź i zainstaluj klienta obr. / min</span><span class="sxs-lookup"><span data-stu-id="03c85-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="03c85-142">Pobieranie: Dla RHEL 6</span><span class="sxs-lookup"><span data-stu-id="03c85-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="03c85-143">Dla RHEL 7</span><span class="sxs-lookup"><span data-stu-id="03c85-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="03c85-144">Sprawdź:</span><span class="sxs-lookup"><span data-stu-id="03c85-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="03c85-145">Sprawdzanie w danych wyjściowych tego podpisu pakietu jest OK</span><span class="sxs-lookup"><span data-stu-id="03c85-145">Check in output that signature of the package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="03c85-146">Zainstaluj obr. / min</span><span class="sxs-lookup"><span data-stu-id="03c85-146">Install the RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="03c85-147">Po zakończeniu upewnij się, że masz dostęp formularza Azure RHUI maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="03c85-147">Upon completion, verify that you can access Azure RHUI form the VM</span></span>

### <a name="all-in-one-script-for-automating-the-preceding-task"></a><span data-ttu-id="03c85-148">W jednym skryptów do automatyzacji poprzedniego zadania</span><span class="sxs-lookup"><span data-stu-id="03c85-148">All-in-one script for automating the preceding task</span></span>
<span data-ttu-id="03c85-149">Użyj następującego skryptu, zgodnie z potrzebami, aby zautomatyzować zadanie aktualizacji odpowiednich maszyn wirtualnych na nowe serwery Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="03c85-149">Use the following script as needed to automate the task of updating affected VMs to the new Azure RHUI servers.</span></span>

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a><span data-ttu-id="03c85-150">Omówienie RHUI</span><span class="sxs-lookup"><span data-stu-id="03c85-150">RHUI overview</span></span>
<span data-ttu-id="03c85-151">[Red Hat aktualizacji infrastruktury](https://access.redhat.com/products/red-hat-update-infrastructure) oferuje wysoce skalowalną rozwiązanie do zarządzania zawartością repozytorium yum dla wystąpienia chmury Red Hat Enterprise Linux hostowanych przez dostawców chmury certyfikowane Red Hat.</span><span class="sxs-lookup"><span data-stu-id="03c85-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution to manage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="03c85-152">W oparciu o nadrzędnego projektu masa, RHUI umożliwia dostawcom usług chmury lokalnie hostowanych Red Hat repozytorium zawartości, Utwórz niestandardowe repozytoria z własną zawartość i udostępnić te repozytoria dużą grupę użytkowników końcowych za pośrednictwem równoważenia obciążenia system dostarczania zawartości.</span><span class="sxs-lookup"><span data-stu-id="03c85-152">Based on the upstream Pulp project, RHUI allows cloud providers to locally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available to a large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="03c85-153">Regionach, gdzie RHUI jest dostępny</span><span class="sxs-lookup"><span data-stu-id="03c85-153">Regions where RHUI is available</span></span>
<span data-ttu-id="03c85-154">RHUI jest dostępna we wszystkich regionach, gdzie RHEL obrazów na żądanie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="03c85-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="03c85-155">Obecnie obejmuje wszystkie regiony publicznego wymienione na [pulpitu nawigacyjnego platformy Azure stan](https://azure.microsoft.com/status/) strony regiony platformy Azure instytucji rządowych Stanów Zjednoczonych i Niemczech Azure.</span><span class="sxs-lookup"><span data-stu-id="03c85-155">It currently includes all public regions listed on the [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="03c85-156">RHUI dostępu dla maszyn wirtualnych z RHEL obrazów na żądanie znajduje się w ich ceny.</span><span class="sxs-lookup"><span data-stu-id="03c85-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="03c85-157">Dostępność dodatkowe chmury regionalne/national zostaną zaktualizowane, jak możemy rozwiń dostępności na żądanie RHEL w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="03c85-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="03c85-158">Dostęp do RHUI hostowanymi na platformie Azure jest ograniczona do maszyn wirtualnych w ramach [zakresy IP centrum danych Azure Microsoft](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="03c85-158">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="03c85-159">Pobierz aktualizacje z innego repozytorium aktualizacji</span><span class="sxs-lookup"><span data-stu-id="03c85-159">Get updates from another update repository</span></span>
<span data-ttu-id="03c85-160">Jeśli trzeba uzyskać aktualizacje z repozytorium inną aktualizację, (a nie RHUI hostowanymi na platformie Azure), należy najpierw wyrejestrować swoich wystąpień z RHUI.</span><span class="sxs-lookup"><span data-stu-id="03c85-160">If you need to get updates from a different update repository (instead of Azure-hosted RHUI), first you need to unregister your instances from RHUI.</span></span> <span data-ttu-id="03c85-161">Następnie należy ponownie zarejestrować ich przy użyciu infrastruktury żądaną aktualizacji (na przykład Red Hat satelity lub Red Hat klienta portalu CDN).</span><span class="sxs-lookup"><span data-stu-id="03c85-161">Then you need to re-register them with the desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="03c85-162">Można będzie konieczne odpowiednie Red Hat subskrypcji dla tych usług i rejestracji [Red Hat chmury dostępu w usłudze Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="03c85-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="03c85-163">Aby wyrejestrować RHUI i ponownie zarejestruj do infrastruktury aktualizacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="03c85-163">To unregister RHUI and reregister to your update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="03c85-164">Edytuj /etc/yum.repos.d/rh-cloud.repo i zmień wszystkich `enabled=1` do `enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="03c85-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` to `enabled=0`.</span></span> <span data-ttu-id="03c85-165">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="03c85-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="03c85-166">Edytuj /etc/yum/pluginconf.d/rhnplugin.conf i zmienić `enabled=0` do `enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="03c85-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` to `enabled=1`.</span></span>
3. <span data-ttu-id="03c85-167">Zarejestruj żądany infrastruktury, na przykład Red Hat klienta portalu.</span><span class="sxs-lookup"><span data-stu-id="03c85-167">Then register with the desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="03c85-168">Wykonaj Red Hat rozwiązania wskazówki na [sposobie rejestracji i subskrypcji systemu do portalu Red Hat klienta](https://access.redhat.com/solutions/253273).</span><span class="sxs-lookup"><span data-stu-id="03c85-168">Follow Red Hat solution guide on [how to register and subscribe a system to the Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="03c85-169">Dostęp do RHUI hostowanymi na platformie Azure jest uwzględniony w cenie obrazu RHEL płatność za rzeczywiste użycie (między).</span><span class="sxs-lookup"><span data-stu-id="03c85-169">Access to the Azure-hosted RHUI is included in the RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="03c85-170">Wyrejestrowywanie między RHEL maszyny Wirtualnej z RHUI hostowanymi na platformie Azure nie konwersji maszyny wirtualnej na typ Bring-Your-właścicielem-License (BYOL) maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="03c85-170">Unregistering a PAYG RHEL VM from the Azure-hosted RHUI does not convert the virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="03c85-171">Jeśli zarejestrujesz tej samej maszyny Wirtualnej z innego źródła aktualizacji, użytkownik może naliczania opłat dwa razy: Azure RHEL opłata oprogramowania i drugim dla subskrypcji Red Hat po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="03c85-171">If you register the same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and the second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="03c85-172">Jeśli musisz użyć infrastruktury aktualizacji innych niż spójnie RHUI hostowanymi na platformie Azure należy wziąć pod uwagę tworzenia i wdrażania obrazów (BYOL-type) zgodnie z opisem w [tworzenie i przekazywanie Red Hat maszyn wirtualnych na platformie Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artykułu.</span><span class="sxs-lookup"><span data-stu-id="03c85-172">If you consistently need to use an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="03c85-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="03c85-173">Next steps</span></span>
<span data-ttu-id="03c85-174">Aby utworzyć maszynę Wirtualną Red Hat Enterprise Linux z obrazu Azure Marketplace płatność za rzeczywiste użycie i wykorzystać RHUI hostowanymi na platformie Azure, przejdź do [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="03c85-174">To create a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="03c85-175">Można użyć `yum update` wystąpienia RHEL bez żadnej dodatkowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="03c85-175">You will be able to use `yum update` in your RHEL instance without any additional setup.</span></span>

