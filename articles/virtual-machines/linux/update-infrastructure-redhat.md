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
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a>Red Hat aktualizacji infrastruktury (RHUI) na żądanie Red Hat Enterprise Linux w maszynach wirtualnych na platformie Azure
Maszyny wirtualne utworzone na podstawie hello na żądanie Red Hat Enterprise Linux (RHEL) dostępnych obrazów w portalu Azure Marketplace są hello zarejestrowanych tooaccess Red Hat aktualizacji infrastruktury (RHUI) wdrożona na platformie Azure.  Hello na żądanie RHEL wystąpień mają dostęp tooa regionalnych yum repozytorium i stanie tooreceive aktualizacji przyrostowych.

Witaj yum repozytorium listę, która jest zarządzana przez RHUI, jest skonfigurowany w wystąpieniu RHEL podczas inicjowania obsługi. Nie ma potrzeby toodo dodatkowa konfiguracja — Uruchom `yum update` po wystąpieniu RHEL jest gotowy tooget hello najnowsze aktualizacje.

> [!NOTE]
> We wrześniu 2016 r wdrożyliśmy zaktualizowane RHUI Azure i w stycznia 2017 możemy uruchomić etapowe zamknięcie hello starsze RHUI Azure. Jeśli używany był hello RHEL obrazy (lub migawki ich) od września 2016 lub nowszy - prawdopodobnie jest wymagana żadna akcja. Jeśli jednak masz starszą migawki/VMs, ich konfiguracji należy toobe dodano toohello nieprzerwanego dostępu Azure RHUI.
> 

## <a name="rhui-azure-infrastructure-update"></a>RHUI aktualizacji infrastruktury platformy Azure
Począwszy od września 2016 r. platforma Azure ma nowy zestaw serwerów Red Hat aktualizacji infrastruktury (RHUI). Te serwery zostały wdrożone za pomocą [usługi Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) tak, aby jeden punkt końcowy (rhui 1.microsoft.com) mogą być używane przez żadnej maszyny Wirtualnej, niezależnie od tego regionu. Witaj nowych obrazów RHEL płatność za rzeczywiste użycie (między) w hello Azure Marketplace (wersje z września 2016 lub nowszy) punktu toohello nowych Azure RHUI serwerów i nie wymagają żadnych dodatkowych działań.

### <a name="determine-if-action-is-required"></a>Określić, jeśli jest wymagana akcja
Jeśli występują problemy z połączeniem tooAzure RHUI z maszyny Wirtualnej między RHEL Azure, wykonaj następujące czynności
1. Sprawdź konfigurację maszyny Wirtualnej dla punktu końcowego Azure RHUI

    Sprawdź, czy `/etc/yum.repos.d/rh-cloud.repo` plik zawiera odwołanie za`rhui-[1-3].microsoft.com` w baseurl z `[rhui-microsoft-azure-rhel*]` sekcji hello pliku. Jeśli jest — używasz hello nowe RHUI Azure.

    Jeśli go wskazanie lokalizacji tooa hello następującego wzorca `mirrorlist.*cds[1-4].cloudapp.net` — wymagana jest aktualizacja konfiguracji hello.

    Jeśli używasz hello nową konfigurację i nadal nie można połączyć tooAzure RHUI - pliku sprawy pomocy technicznej firmy Microsoft lub Red Hat.

    > [!NOTE]
    > RHUI hostowanej tooAzure dostęp jest ograniczony toohello maszyn wirtualnych, w ramach [zakresy IP centrum danych Azure Microsoft](https://www.microsoft.com/download/details.aspx?id=41653).
    > 

2. Jeśli hello starego RHUI Azure jest nadal dostępny po można w tym celu Sprawdź i chcesz tooautomatically aktualizacji hello konfiguracji, należy wykonać hello następujące polecenie:

    `sudo yum update RHEL6`lub `sudo yum update RHEL7` w zależności od wersji rodziny RHEL hello.

3. Jeśli nie możesz połączyć toohello starego RHUI Azure, wykonaj hello wymagane ręczne wykonanie czynności opisanych w następnej sekcji hello.

4. Upewnij się, że maszyna wirtualna wpływ na konfigurację hello tooupdate na powitania źródło obrazu/migawki zainicjowano obsługę administracyjną z.

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a>Zamknięcie etapowe hello starego RHUI Azure
Podczas wyłączania hello hello starego RHUI Azure stosujemy ograniczenia dostępu tooit w następujący sposób:

1. Bardziej ograniczyć dostępu (ACL) tooset adresów IP, które są już połączenie tooit. Efekty uboczne: Jeśli będziesz kontynuować, przy użyciu starego RHUI Azure hello — nowych maszyn wirtualnych może nie być możliwe tooconnect tooit. RHEL maszyny wirtualne z dynamicznych adresów IP, który przechodzi przez zamknięcie/cofnąć/start sekwencji może pojawić się nowego adresu IP i dlatego również można uruchomić niepowodzeniem tooconnect toohello starego RHUI Azure

2. Zamknięcie Serwery dublowane dostarczania zawartości. Efekty uboczne: jak możemy zamknąć więcej CDSes może zostać wyświetlony już `yum update` obsługi czasu więcej limitów czasu do hello punktów podczas można już połączyć toohello starego RHUI Azure.

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a>Witaj adresów IP dla nowych serwerów dostarczania zawartości RHUI hello są
Jeśli używasz toofurther konfiguracji sieci ograniczyć dostęp z maszyn wirtualnych między RHEL, upewnij się, hello następujące adresy IP są dozwolone w przypadku `yum update` toowork w zależności od środowiska hello w. 

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

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a>Ręczna aktualizacja procedury toouse hello nowych Azure RHUI serwerów
Podpis klucza publicznego hello pobierania (za pośrednictwem curl)

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

Sprawdź klucz hello pobrane

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

Sprawdź dane wyjściowe hello, sprawdź `keyid` i `user ID packet`:

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

Zainstaluj klucz publiczny hello

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

Sprawdzanie w danych wyjściowych tego podpisu pakietów hello jest OK

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

Zainstaluj hello obr. / min

```bash
sudo rpm -U azureclient.rpm
```

Po zakończeniu upewnij się, że masz dostęp hello formularza Azure RHUI maszyny Wirtualnej

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a>W jednym skryptów do automatyzacji hello poprzedzających zadań
Użyj następującego skryptu jako zadanie hello tooautomate wymaganych aktualizacji odpowiednich maszyn wirtualnych toohello nowe Azure RHUI serwerach hello.

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
[Red Hat aktualizacji infrastruktury](https://access.redhat.com/products/red-hat-update-infrastructure) oferuje wysoce skalowalna toomanage yum repozytorium zawartości dla wystąpienia chmury Red Hat Enterprise Linux hostowanych przez dostawców chmury certyfikowane Red Hat. Na podstawie hello nadrzędnego masy projektu, RHUI umożliwia dostawcom usług w chmurze zawartości hostowanej Red Hat repozytorium dublowany toolocally, utworzyć niestandardowe repozytoria z własną zawartość i dołączyć tych repozytoria dostępne tooa dużą grupę użytkowników końcowych za pośrednictwem równoważenia obciążenia system dostarczania zawartości.

## <a name="regions-where-rhui-is-available"></a>Regionach, gdzie RHUI jest dostępny
RHUI jest dostępna we wszystkich regionach, gdzie RHEL obrazów na żądanie są dostępne. Obecnie obejmuje wszystkie publiczne regionów wymienionych na powitania [pulpitu nawigacyjnego platformy Azure stan](https://azure.microsoft.com/status/) strony regiony platformy Azure instytucji rządowych Stanów Zjednoczonych i Niemczech Azure. RHUI dostępu dla maszyn wirtualnych z RHEL obrazów na żądanie znajduje się w ich ceny. Dodatkowe chmury regionalne/national dostępności zostaną zaktualizowane, jak firma Microsoft rozwiń RHEL dostępności na żądanie w przyszłości hello.

> [!NOTE]
> RHUI hostowanej tooAzure dostęp jest ograniczony toohello maszyn wirtualnych, w ramach [zakresy IP centrum danych Azure Microsoft](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

## <a name="get-updates-from-another-update-repository"></a>Pobierz aktualizacje z innego repozytorium aktualizacji
Jeśli potrzebujesz tooget aktualizacje z repozytorium inną aktualizację (zamiast RHUI hostowanymi na platformie Azure), należy najpierw toounregister swoich wystąpień z RHUI. Następnie należy zarejestrować toore z hello odpowiednią aktualizację infrastruktury (na przykład Red Hat satelity lub Red Hat klienta portalu CDN). Można będzie konieczne odpowiednie Red Hat subskrypcji dla tych usług i rejestracji [Red Hat chmury dostępu w usłudze Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).

toounregister RHUI i ponownie zarejestruj tooyour aktualizacji infrastruktury, wykonaj następujące kroki:

1. Edytuj /etc/yum.repos.d/rh-cloud.repo i zmień wszystkich `enabled=1` zbyt`enabled=0`. Na przykład:
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. Edytuj /etc/yum/pluginconf.d/rhnplugin.conf i zmienić `enabled=0` zbyt`enabled=1`.
3. Zarejestruj żądany infrastruktury hello, na przykład portalu klienta Red Hat. Wykonaj Red Hat rozwiązania wskazówki na [jak tooregister i subskrybowania toohello systemu Red Hat klienta Portal](https://access.redhat.com/solutions/253273).

> [!NOTE]
> Dostęp toohello RHUI hostowanymi na platformie Azure jest uwzględniony w cenie obrazu RHEL płatność za rzeczywiste użycie (między) hello. Wyrejestrowywanie między RHEL maszyny Wirtualnej z hello RHUI hostowanymi na platformie Azure nie konwertowanie maszyny wirtualnej hello Bring-Your-właścicielem-License (BYOL) typu maszyny Wirtualnej. Jeśli zarejestrujesz hello tej samej maszyny Wirtualnej z innego źródła aktualizacji może naliczania opłat podwójne: po raz pierwszy opłata oprogramowania Azure RHEL i powitania dla subskrypcji Red Hat po raz drugi. 
> 
> Jeśli potrzebujesz spójnie toouse infrastruktury aktualizacji niż RHUI hostowanymi na platformie Azure należy wziąć pod uwagę tworzenia i wdrażania obrazów (BYOL-type) zgodnie z opisem w [tworzenie i przekazywanie Red Hat maszyn wirtualnych na platformie Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artykułu.
> 

## <a name="next-steps"></a>Następne kroki
toocreate Red Hat Enterprise Linux maszyny Wirtualnej z obrazu Azure Marketplace płatność za rzeczywiste użycie i wykorzystać RHUI hostowanymi na platformie Azure, przejdź zbyt[portalu Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/). Będziesz w stanie toouse `yum update` wystąpienia RHEL bez żadnej dodatkowej konfiguracji.

