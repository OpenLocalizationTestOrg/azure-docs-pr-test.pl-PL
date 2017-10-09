---
title: aaaRed Hat aktualizacji infrastruktury (RHUI) | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="34736-103">Red Hat aktualizacji infrastruktury (RHUI) na żądanie Red Hat Enterprise Linux w maszynach wirtualnych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="34736-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="34736-104">Maszyny wirtualne utworzone na podstawie hello na żądanie Red Hat Enterprise Linux (RHEL) dostępnych obrazów w portalu Azure Marketplace są hello zarejestrowanych tooaccess Red Hat aktualizacji infrastruktury (RHUI) wdrożona na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="34736-104">Virtual machines created from hello on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered tooaccess hello Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="34736-105">Hello na żądanie RHEL wystąpień mają dostęp tooa regionalnych yum repozytorium i stanie tooreceive aktualizacji przyrostowych.</span><span class="sxs-lookup"><span data-stu-id="34736-105">hello on-demand RHEL instances have access tooa regional yum repository and able tooreceive incremental updates.</span></span>

<span data-ttu-id="34736-106">Witaj yum repozytorium listę, która jest zarządzana przez RHUI, jest skonfigurowany w wystąpieniu RHEL podczas inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="34736-106">hello yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="34736-107">Nie ma potrzeby toodo dodatkowa konfiguracja — Uruchom `yum update` po wystąpieniu RHEL jest gotowy tooget hello najnowsze aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="34736-107">You don't need toodo any additional configuration - run `yum update` after your RHEL instance is ready tooget hello latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="34736-108">We wrześniu 2016 r wdrożyliśmy zaktualizowane RHUI Azure i w stycznia 2017 możemy uruchomić etapowe zamknięcie hello starsze RHUI Azure.</span><span class="sxs-lookup"><span data-stu-id="34736-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of hello older Azure RHUI.</span></span> <span data-ttu-id="34736-109">Jeśli używany był hello RHEL obrazy (lub migawki ich) od września 2016 lub nowszy - prawdopodobnie jest wymagana żadna akcja.</span><span class="sxs-lookup"><span data-stu-id="34736-109">If you have been using hello RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="34736-110">Jeśli jednak masz starszą migawki/VMs, ich konfiguracji należy toobe dodano toohello nieprzerwanego dostępu Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="34736-110">If, however, you have older snapshots/VMs, their configuration needs toobe updated for uninterrupted access toohello Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="34736-111">RHUI aktualizacji infrastruktury platformy Azure</span><span class="sxs-lookup"><span data-stu-id="34736-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="34736-112">Począwszy od września 2016 r. platforma Azure ma nowy zestaw serwerów Red Hat aktualizacji infrastruktury (RHUI).</span><span class="sxs-lookup"><span data-stu-id="34736-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="34736-113">Te serwery zostały wdrożone za pomocą [usługi Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) tak, aby jeden punkt końcowy (rhui 1.microsoft.com) mogą być używane przez żadnej maszyny Wirtualnej, niezależnie od tego regionu.</span><span class="sxs-lookup"><span data-stu-id="34736-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="34736-114">Witaj nowych obrazów RHEL płatność za rzeczywiste użycie (między) w hello Azure Marketplace (wersje z września 2016 lub nowszy) punktu toohello nowych Azure RHUI serwerów i nie wymagają żadnych dodatkowych działań.</span><span class="sxs-lookup"><span data-stu-id="34736-114">hello new RHEL Pay-As-You-Go (PAYG) images in hello Azure Marketplace (versions dated September 2016 or later) point toohello new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="34736-115">Określić, jeśli jest wymagana akcja</span><span class="sxs-lookup"><span data-stu-id="34736-115">Determine if action is required</span></span>
<span data-ttu-id="34736-116">Jeśli występują problemy z połączeniem tooAzure RHUI z maszyny Wirtualnej między RHEL Azure, wykonaj następujące czynności</span><span class="sxs-lookup"><span data-stu-id="34736-116">If you are experiencing problems connecting tooAzure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="34736-117">Sprawdź konfigurację maszyny Wirtualnej dla punktu końcowego Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="34736-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="34736-118">Sprawdź, czy `/etc/yum.repos.d/rh-cloud.repo` plik zawiera odwołanie za`rhui-[1-3].microsoft.com` w baseurl z `[rhui-microsoft-azure-rhel*]` sekcji hello pliku.</span><span class="sxs-lookup"><span data-stu-id="34736-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference too`rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of hello file.</span></span> <span data-ttu-id="34736-119">Jeśli jest — używasz hello nowe RHUI Azure.</span><span class="sxs-lookup"><span data-stu-id="34736-119">If it is - you are using hello new Azure RHUI.</span></span>

    <span data-ttu-id="34736-120">Jeśli go wskazanie lokalizacji tooa hello następującego wzorca `mirrorlist.*cds[1-4].cloudapp.net` — wymagana jest aktualizacja konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="34736-120">If it pointing tooa location with hello following pattern `mirrorlist.*cds[1-4].cloudapp.net` - hello configuration update is required.</span></span>

    <span data-ttu-id="34736-121">Jeśli używasz hello nową konfigurację i nadal nie można połączyć tooAzure RHUI - pliku sprawy pomocy technicznej firmy Microsoft lub Red Hat.</span><span class="sxs-lookup"><span data-stu-id="34736-121">If you are using hello new configuration and still cannot connect tooAzure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="34736-122">RHUI hostowanej tooAzure dostęp jest ograniczony toohello maszyn wirtualnych, w ramach [zakresy IP centrum danych Azure Microsoft](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="34736-122">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="34736-123">Jeśli hello starego RHUI Azure jest nadal dostępny po można w tym celu Sprawdź i chcesz tooautomatically aktualizacji hello konfiguracji, należy wykonać hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="34736-123">If hello old Azure RHUI is still available when you do this check and you would like tooautomatically update hello configuration, execute hello following command:</span></span>

    <span data-ttu-id="34736-124">`sudo yum update RHEL6`lub `sudo yum update RHEL7` w zależności od wersji rodziny RHEL hello.</span><span class="sxs-lookup"><span data-stu-id="34736-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on hello RHEL family version.</span></span>

3. <span data-ttu-id="34736-125">Jeśli nie możesz połączyć toohello starego RHUI Azure, wykonaj hello wymagane ręczne wykonanie czynności opisanych w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="34736-125">If you can no longer connect toohello old Azure RHUI, follow hello manual steps described in hello next section.</span></span>

4. <span data-ttu-id="34736-126">Upewnij się, że maszyna wirtualna wpływ na konfigurację hello tooupdate na powitania źródło obrazu/migawki zainicjowano obsługę administracyjną z.</span><span class="sxs-lookup"><span data-stu-id="34736-126">Make sure tooupdate hello configuration on hello source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a><span data-ttu-id="34736-127">Zamknięcie etapowe hello starego RHUI Azure</span><span class="sxs-lookup"><span data-stu-id="34736-127">Phased shutdown of hello old Azure RHUI</span></span>
<span data-ttu-id="34736-128">Podczas wyłączania hello hello starego RHUI Azure stosujemy ograniczenia dostępu tooit w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="34736-128">During hello shutdown of hello old Azure RHUI we restrict access tooit as follows:</span></span>

1. <span data-ttu-id="34736-129">Bardziej ograniczyć dostępu (ACL) tooset adresów IP, które są już połączenie tooit.</span><span class="sxs-lookup"><span data-stu-id="34736-129">Further restrict access (ACL) tooset of IP addresses that are already connecting tooit.</span></span> <span data-ttu-id="34736-130">Efekty uboczne: Jeśli będziesz kontynuować, przy użyciu starego RHUI Azure hello — nowych maszyn wirtualnych może nie być możliwe tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="34736-130">Possible side-effects: if you continue using hello old Azure RHUI - your new VMs may not be able tooconnect tooit.</span></span> <span data-ttu-id="34736-131">RHEL maszyny wirtualne z dynamicznych adresów IP, który przechodzi przez zamknięcie/cofnąć/start sekwencji może pojawić się nowego adresu IP i dlatego również można uruchomić niepowodzeniem tooconnect toohello starego RHUI Azure</span><span class="sxs-lookup"><span data-stu-id="34736-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing tooconnect toohello old Azure RHUI</span></span>

2. <span data-ttu-id="34736-132">Zamknięcie Serwery dublowane dostarczania zawartości.</span><span class="sxs-lookup"><span data-stu-id="34736-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="34736-133">Efekty uboczne: jak możemy zamknąć więcej CDSes może zostać wyświetlony już `yum update` obsługi czasu więcej limitów czasu do hello punktów podczas można już połączyć toohello starego RHUI Azure.</span><span class="sxs-lookup"><span data-stu-id="34736-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until hello point when you can no longer connect toohello old Azure RHUI.</span></span>

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="34736-134">Witaj adresów IP dla nowych serwerów dostarczania zawartości RHUI hello są</span><span class="sxs-lookup"><span data-stu-id="34736-134">hello IPs for hello new RHUI content delivery servers are</span></span>
<span data-ttu-id="34736-135">Jeśli używasz toofurther konfiguracji sieci ograniczyć dostęp z maszyn wirtualnych między RHEL, upewnij się, hello następujące adresy IP są dozwolone w przypadku `yum update` toowork w zależności od środowiska hello w.</span><span class="sxs-lookup"><span data-stu-id="34736-135">If you are using network configuration toofurther restrict access from RHEL PAYG VMs, make sure hello following IPs are allowed for `yum update` toowork depending on hello environment you are in.</span></span> 

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

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a><span data-ttu-id="34736-136">Ręczna aktualizacja procedury toouse hello nowych Azure RHUI serwerów</span><span class="sxs-lookup"><span data-stu-id="34736-136">Manual update procedure toouse hello new Azure RHUI servers</span></span>
<span data-ttu-id="34736-137">Podpis klucza publicznego hello pobierania (za pośrednictwem curl)</span><span class="sxs-lookup"><span data-stu-id="34736-137">Download (via curl) hello public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="34736-138">Sprawdź klucz hello pobrane</span><span class="sxs-lookup"><span data-stu-id="34736-138">Verify hello downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="34736-139">Sprawdź dane wyjściowe hello, sprawdź `keyid` i `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="34736-139">Check hello output, verify `keyid` and `user ID packet`:</span></span>

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

<span data-ttu-id="34736-140">Zainstaluj klucz publiczny hello</span><span class="sxs-lookup"><span data-stu-id="34736-140">Install hello public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="34736-141">Pobierz, sprawdź i zainstaluj klienta obr. / min</span><span class="sxs-lookup"><span data-stu-id="34736-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="34736-142">Pobieranie: Dla RHEL 6</span><span class="sxs-lookup"><span data-stu-id="34736-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="34736-143">Dla RHEL 7</span><span class="sxs-lookup"><span data-stu-id="34736-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="34736-144">Sprawdź:</span><span class="sxs-lookup"><span data-stu-id="34736-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="34736-145">Sprawdzanie w danych wyjściowych tego podpisu pakietów hello jest OK</span><span class="sxs-lookup"><span data-stu-id="34736-145">Check in output that signature of hello package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="34736-146">Zainstaluj hello obr. / min</span><span class="sxs-lookup"><span data-stu-id="34736-146">Install hello RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="34736-147">Po zakończeniu upewnij się, że masz dostęp hello formularza Azure RHUI maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="34736-147">Upon completion, verify that you can access Azure RHUI form hello VM</span></span>

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a><span data-ttu-id="34736-148">W jednym skryptów do automatyzacji hello poprzedzających zadań</span><span class="sxs-lookup"><span data-stu-id="34736-148">All-in-one script for automating hello preceding task</span></span>
<span data-ttu-id="34736-149">Użyj następującego skryptu jako zadanie hello tooautomate wymaganych aktualizacji odpowiednich maszyn wirtualnych toohello nowe Azure RHUI serwerach hello.</span><span class="sxs-lookup"><span data-stu-id="34736-149">Use hello following script as needed tooautomate hello task of updating affected VMs toohello new Azure RHUI servers.</span></span>

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

## <a name="rhui-overview"></a><span data-ttu-id="34736-150">Omówienie RHUI</span><span class="sxs-lookup"><span data-stu-id="34736-150">RHUI overview</span></span>
<span data-ttu-id="34736-151">[Red Hat aktualizacji infrastruktury](https://access.redhat.com/products/red-hat-update-infrastructure) oferuje wysoce skalowalna toomanage yum repozytorium zawartości dla wystąpienia chmury Red Hat Enterprise Linux hostowanych przez dostawców chmury certyfikowane Red Hat.</span><span class="sxs-lookup"><span data-stu-id="34736-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution toomanage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="34736-152">Na podstawie hello nadrzędnego masy projektu, RHUI umożliwia dostawcom usług w chmurze zawartości hostowanej Red Hat repozytorium dublowany toolocally, utworzyć niestandardowe repozytoria z własną zawartość i dołączyć tych repozytoria dostępne tooa dużą grupę użytkowników końcowych za pośrednictwem równoważenia obciążenia system dostarczania zawartości.</span><span class="sxs-lookup"><span data-stu-id="34736-152">Based on hello upstream Pulp project, RHUI allows cloud providers toolocally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available tooa large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="34736-153">Regionach, gdzie RHUI jest dostępny</span><span class="sxs-lookup"><span data-stu-id="34736-153">Regions where RHUI is available</span></span>
<span data-ttu-id="34736-154">RHUI jest dostępna we wszystkich regionach, gdzie RHEL obrazów na żądanie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="34736-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="34736-155">Obecnie obejmuje wszystkie publiczne regionów wymienionych na powitania [pulpitu nawigacyjnego platformy Azure stan](https://azure.microsoft.com/status/) strony regiony platformy Azure instytucji rządowych Stanów Zjednoczonych i Niemczech Azure.</span><span class="sxs-lookup"><span data-stu-id="34736-155">It currently includes all public regions listed on hello [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="34736-156">RHUI dostępu dla maszyn wirtualnych z RHEL obrazów na żądanie znajduje się w ich ceny.</span><span class="sxs-lookup"><span data-stu-id="34736-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="34736-157">Dodatkowe chmury regionalne/national dostępności zostaną zaktualizowane, jak firma Microsoft rozwiń RHEL dostępności na żądanie w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="34736-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="34736-158">RHUI hostowanej tooAzure dostęp jest ograniczony toohello maszyn wirtualnych, w ramach [zakresy IP centrum danych Azure Microsoft](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="34736-158">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="34736-159">Pobierz aktualizacje z innego repozytorium aktualizacji</span><span class="sxs-lookup"><span data-stu-id="34736-159">Get updates from another update repository</span></span>
<span data-ttu-id="34736-160">Jeśli potrzebujesz tooget aktualizacje z repozytorium inną aktualizację (zamiast RHUI hostowanymi na platformie Azure), należy najpierw toounregister swoich wystąpień z RHUI.</span><span class="sxs-lookup"><span data-stu-id="34736-160">If you need tooget updates from a different update repository (instead of Azure-hosted RHUI), first you need toounregister your instances from RHUI.</span></span> <span data-ttu-id="34736-161">Następnie należy zarejestrować toore z hello odpowiednią aktualizację infrastruktury (na przykład Red Hat satelity lub Red Hat klienta portalu CDN).</span><span class="sxs-lookup"><span data-stu-id="34736-161">Then you need toore-register them with hello desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="34736-162">Można będzie konieczne odpowiednie Red Hat subskrypcji dla tych usług i rejestracji [Red Hat chmury dostępu w usłudze Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="34736-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="34736-163">toounregister RHUI i ponownie zarejestruj tooyour aktualizacji infrastruktury, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="34736-163">toounregister RHUI and reregister tooyour update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="34736-164">Edytuj /etc/yum.repos.d/rh-cloud.repo i zmień wszystkich `enabled=1` zbyt`enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="34736-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` too`enabled=0`.</span></span> <span data-ttu-id="34736-165">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="34736-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="34736-166">Edytuj /etc/yum/pluginconf.d/rhnplugin.conf i zmienić `enabled=0` zbyt`enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="34736-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` too`enabled=1`.</span></span>
3. <span data-ttu-id="34736-167">Zarejestruj żądany infrastruktury hello, na przykład portalu klienta Red Hat.</span><span class="sxs-lookup"><span data-stu-id="34736-167">Then register with hello desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="34736-168">Wykonaj Red Hat rozwiązania wskazówki na [jak tooregister i subskrybowania toohello systemu Red Hat klienta Portal](https://access.redhat.com/solutions/253273).</span><span class="sxs-lookup"><span data-stu-id="34736-168">Follow Red Hat solution guide on [how tooregister and subscribe a system toohello Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="34736-169">Dostęp toohello RHUI hostowanymi na platformie Azure jest uwzględniony w cenie obrazu RHEL płatność za rzeczywiste użycie (między) hello.</span><span class="sxs-lookup"><span data-stu-id="34736-169">Access toohello Azure-hosted RHUI is included in hello RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="34736-170">Wyrejestrowywanie między RHEL maszyny Wirtualnej z hello RHUI hostowanymi na platformie Azure nie konwertowanie maszyny wirtualnej hello Bring-Your-właścicielem-License (BYOL) typu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="34736-170">Unregistering a PAYG RHEL VM from hello Azure-hosted RHUI does not convert hello virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="34736-171">Jeśli zarejestrujesz hello tej samej maszyny Wirtualnej z innego źródła aktualizacji może naliczania opłat podwójne: po raz pierwszy opłata oprogramowania Azure RHEL i powitania dla subskrypcji Red Hat po raz drugi.</span><span class="sxs-lookup"><span data-stu-id="34736-171">If you register hello same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and hello second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="34736-172">Jeśli potrzebujesz spójnie toouse infrastruktury aktualizacji niż RHUI hostowanymi na platformie Azure należy wziąć pod uwagę tworzenia i wdrażania obrazów (BYOL-type) zgodnie z opisem w [tworzenie i przekazywanie Red Hat maszyn wirtualnych na platformie Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artykułu.</span><span class="sxs-lookup"><span data-stu-id="34736-172">If you consistently need toouse an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="34736-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34736-173">Next steps</span></span>
<span data-ttu-id="34736-174">toocreate Red Hat Enterprise Linux maszyny Wirtualnej z obrazu Azure Marketplace płatność za rzeczywiste użycie i wykorzystać RHUI hostowanymi na platformie Azure, przejdź zbyt[portalu Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="34736-174">toocreate a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="34736-175">Będziesz w stanie toouse `yum update` wystąpienia RHEL bez żadnej dodatkowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="34736-175">You will be able toouse `yum update` in your RHEL instance without any additional setup.</span></span>

