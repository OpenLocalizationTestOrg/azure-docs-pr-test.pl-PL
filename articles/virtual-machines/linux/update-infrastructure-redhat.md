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
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a>Red Hat aktualizacji infrastruktury (RHUI) na żądanie Red Hat Enterprise Linux w maszynach wirtualnych na platformie Azure
Maszyny wirtualne utworzone z obrazów Red Hat Enterprise Linux (RHEL) na żądanie dostępne w portalu Azure Marketplace jest zarejestrowany na dostęp Red Hat aktualizacji infrastruktury (RHUI) wdrożona na platformie Azure.  Wystąpienia na żądanie RHEL mieć dostęp do repozytorium yum regionalnych i może odbierać aktualizacje przyrostowe.

Na liście repozytorium yum, który jest zarządzany przez RHUI, jest skonfigurowany w wystąpieniu RHEL podczas inicjowania obsługi. Nie musisz podejmować żadnych dodatkowych konfiguracji — Uruchom `yum update` po wystąpieniu RHEL jest gotowy do Pobierz najnowsze aktualizacje.

> [!NOTE]
> We wrześniu 2016 r wdrożyliśmy zaktualizowane RHUI Azure i w stycznia 2017 możemy uruchomić etapowe zamknięcie starszych RHUI Azure. Jeśli był używany obrazów RHEL (lub migawki ich) od września 2016 lub nowszy - prawdopodobnie jest wymagana żadna akcja. Jeśli jednak masz starszą migawki/VMs, ich konfiguracji musi zostać zaktualizowany nieprzerwany dostęp do Azure RHUI.
> 

## <a name="rhui-azure-infrastructure-update"></a>RHUI aktualizacji infrastruktury platformy Azure
Począwszy od września 2016 r. platforma Azure ma nowy zestaw serwerów Red Hat aktualizacji infrastruktury (RHUI). Te serwery zostały wdrożone za pomocą [usługi Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) tak, aby jeden punkt końcowy (rhui 1.microsoft.com) mogą być używane przez żadnej maszyny Wirtualnej, niezależnie od tego regionu. Nowych obrazów RHEL płatność za rzeczywiste użycie (między) w portalu Azure Marketplace (wersje z września 2016 lub nowszy) wskaż nowych serwerów Azure RHUI i nie wymagają żadnych dodatkowych działań.

### <a name="determine-if-action-is-required"></a>Określić, jeśli jest wymagana akcja
Jeśli występują problemy z połączeniem z maszyny Wirtualnej Azure RHEL między Azure RHUI, wykonaj następujące czynności
1. Sprawdź konfigurację maszyny Wirtualnej dla punktu końcowego Azure RHUI

    Sprawdź, czy `/etc/yum.repos.d/rh-cloud.repo` plik zawiera odwołanie do `rhui-[1-3].microsoft.com` w baseurl z `[rhui-microsoft-azure-rhel*]` sekcji pliku. — Jeśli używasz nowego RHUI Azure.

    Jeśli go wskazuje lokalizację przy użyciu następującego wzorca `mirrorlist.*cds[1-4].cloudapp.net` — wymagana jest aktualizacja konfiguracji.

    Jeśli używasz nową konfigurację i nadal nie można połączyć się Azure RHUI - pliku sprawy pomocy technicznej firmy Microsoft lub Red Hat.

    > [!NOTE]
    > Dostęp do RHUI hostowanymi na platformie Azure jest ograniczona do maszyn wirtualnych w ramach [zakresy IP centrum danych Azure Microsoft](https://www.microsoft.com/download/details.aspx?id=41653).
    > 

2. Jeśli stary RHUI Azure jest nadal dostępna, gdy zostanie w tym celu Sprawdź i chcesz automatycznie zaktualizować konfigurację, wykonaj następujące polecenie:

    `sudo yum update RHEL6`lub `sudo yum update RHEL7` w zależności od wersji rodziny RHEL.

3. Jeśli nie można nawiązać starego RHUI Azure, wykonaj ręcznie czynności opisane w następnej sekcji.

4. Upewnij się zaktualizować konfigurację w źródle obrazu/migawki wpływ na udostępniony z maszyny Wirtualnej.

### <a name="phased-shutdown-of-the-old-azure-rhui"></a>Zamknięcie etapowe starego RHUI Azure
Podczas zamykania starego RHUI Azure możemy ograniczyć dostęp do jej w następujący sposób:

1. Dalsze ograniczenie dostępu (ACL), aby ustawić adresów IP, które już połączenie z jego. Efekty uboczne: Jeśli będziesz kontynuować, przy użyciu starego RHUI Azure — nowych maszyn wirtualnych nie można połączyć się z nim. RHEL maszyny wirtualne z dynamicznych adresów IP, który przechodzi przez zamknięcie/cofnąć/start sekwencji może pojawić się nowego adresu IP i dlatego również można uruchomić brakiem połączenia między starym RHUI Azure

2. Zamknięcie Serwery dublowane dostarczania zawartości. Efekty uboczne: jak możemy zamknąć więcej CDSes może zostać wyświetlony już `yum update` obsługi czasu, więcej przekroczeń limitu czasu, aż do momentu, gdy nie można nawiązać starego RHUI Azure.

### <a name="the-ips-for-the-new-rhui-content-delivery-servers-are"></a>Adresy IP dla nowych serwerów dostarczania zawartości RHUI są
Jeśli konfiguracja sieci używane są bardziej ograniczyć dostęp z maszyn wirtualnych między RHEL, upewnij się, że następujące adresy IP, są dozwolone dla `yum update` do pracy w zależności od środowiska są w. 

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

### <a name="manual-update-procedure-to-use-the-new-azure-rhui-servers"></a>Procedura ręcznej aktualizacji do używania nowych serwerów Azure RHUI
Pobierz (za pośrednictwem curl) podpis klucza publicznego

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

Sprawdź klucz pobrany

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

Sprawdź dane wyjściowe, sprawdź `keyid` i `user ID packet`:

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

Zainstaluj klucz publiczny

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

Pobierz, sprawdź i zainstaluj klienta obr. / min

Pobieranie: Dla RHEL 6

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

Dla RHEL 7

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

Sprawdź:

```bash
rpm -Kv azureclient.rpm
```

Sprawdzanie w danych wyjściowych tego podpisu pakietu jest OK

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

Zainstaluj obr. / min

```bash
sudo rpm -U azureclient.rpm
```

Po zakończeniu upewnij się, że masz dostęp formularza Azure RHUI maszyny Wirtualnej

### <a name="all-in-one-script-for-automating-the-preceding-task"></a>W jednym skryptów do automatyzacji poprzedniego zadania
Użyj następującego skryptu, zgodnie z potrzebami, aby zautomatyzować zadanie aktualizacji odpowiednich maszyn wirtualnych na nowe serwery Azure RHUI.

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

## <a name="rhui-overview"></a>Omówienie RHUI
[Red Hat aktualizacji infrastruktury](https://access.redhat.com/products/red-hat-update-infrastructure) oferuje wysoce skalowalną rozwiązanie do zarządzania zawartością repozytorium yum dla wystąpienia chmury Red Hat Enterprise Linux hostowanych przez dostawców chmury certyfikowane Red Hat. W oparciu o nadrzędnego projektu masa, RHUI umożliwia dostawcom usług chmury lokalnie hostowanych Red Hat repozytorium zawartości, Utwórz niestandardowe repozytoria z własną zawartość i udostępnić te repozytoria dużą grupę użytkowników końcowych za pośrednictwem równoważenia obciążenia system dostarczania zawartości.

## <a name="regions-where-rhui-is-available"></a>Regionach, gdzie RHUI jest dostępny
RHUI jest dostępna we wszystkich regionach, gdzie RHEL obrazów na żądanie są dostępne. Obecnie obejmuje wszystkie regiony publicznego wymienione na [pulpitu nawigacyjnego platformy Azure stan](https://azure.microsoft.com/status/) strony regiony platformy Azure instytucji rządowych Stanów Zjednoczonych i Niemczech Azure. RHUI dostępu dla maszyn wirtualnych z RHEL obrazów na żądanie znajduje się w ich ceny. Dostępność dodatkowe chmury regionalne/national zostaną zaktualizowane, jak możemy rozwiń dostępności na żądanie RHEL w przyszłości.

> [!NOTE]
> Dostęp do RHUI hostowanymi na platformie Azure jest ograniczona do maszyn wirtualnych w ramach [zakresy IP centrum danych Azure Microsoft](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

## <a name="get-updates-from-another-update-repository"></a>Pobierz aktualizacje z innego repozytorium aktualizacji
Jeśli trzeba uzyskać aktualizacje z repozytorium inną aktualizację, (a nie RHUI hostowanymi na platformie Azure), należy najpierw wyrejestrować swoich wystąpień z RHUI. Następnie należy ponownie zarejestrować ich przy użyciu infrastruktury żądaną aktualizacji (na przykład Red Hat satelity lub Red Hat klienta portalu CDN). Można będzie konieczne odpowiednie Red Hat subskrypcji dla tych usług i rejestracji [Red Hat chmury dostępu w usłudze Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).

Aby wyrejestrować RHUI i ponownie zarejestruj do infrastruktury aktualizacji, wykonaj następujące kroki:

1. Edytuj /etc/yum.repos.d/rh-cloud.repo i zmień wszystkich `enabled=1` do `enabled=0`. Na przykład:
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. Edytuj /etc/yum/pluginconf.d/rhnplugin.conf i zmienić `enabled=0` do `enabled=1`.
3. Zarejestruj żądany infrastruktury, na przykład Red Hat klienta portalu. Wykonaj Red Hat rozwiązania wskazówki na [sposobie rejestracji i subskrypcji systemu do portalu Red Hat klienta](https://access.redhat.com/solutions/253273).

> [!NOTE]
> Dostęp do RHUI hostowanymi na platformie Azure jest uwzględniony w cenie obrazu RHEL płatność za rzeczywiste użycie (między). Wyrejestrowywanie między RHEL maszyny Wirtualnej z RHUI hostowanymi na platformie Azure nie konwersji maszyny wirtualnej na typ Bring-Your-właścicielem-License (BYOL) maszyny Wirtualnej. Jeśli zarejestrujesz tej samej maszyny Wirtualnej z innego źródła aktualizacji, użytkownik może naliczania opłat dwa razy: Azure RHEL opłata oprogramowania i drugim dla subskrypcji Red Hat po raz pierwszy. 
> 
> Jeśli musisz użyć infrastruktury aktualizacji innych niż spójnie RHUI hostowanymi na platformie Azure należy wziąć pod uwagę tworzenia i wdrażania obrazów (BYOL-type) zgodnie z opisem w [tworzenie i przekazywanie Red Hat maszyn wirtualnych na platformie Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artykułu.
> 

## <a name="next-steps"></a>Następne kroki
Aby utworzyć maszynę Wirtualną Red Hat Enterprise Linux z obrazu Azure Marketplace płatność za rzeczywiste użycie i wykorzystać RHUI hostowanymi na platformie Azure, przejdź do [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/). Można użyć `yum update` wystąpienia RHEL bez żadnej dodatkowej konfiguracji.

