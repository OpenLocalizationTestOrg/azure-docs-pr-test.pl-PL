---
title: "aaaWhat jest lista kontroli dostępu sieci platformy Azure?"
description: "Więcej informacji na temat list kontroli dostępu na platformie Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 83d66c84-8f6b-4388-8767-cd2de3e72d76
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a2681af035d162362771e6df9864bbe838f16352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-endpoint-access-control-list"></a>Co to jest punkt końcowy listy kontroli dostępu?

> [!IMPORTANT]
> Platforma Azure ma dwa różne [modele wdrażania](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) do tworzenia i pracy z zasobami: Resource Manager i model klasyczny. W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać modelu wdrażania usługi Resource Manager hello. 

Punkt końcowy listy kontroli dostępu (ACL) jest ulepszenie zabezpieczeń, dostępne dla danego wdrożenia usługi Azure. Listy ACL zapewnia hello możliwości tooselectively zezwolenia lub odmowy ruchu dla punktu końcowego maszyny wirtualnej. Ta możliwość filtrowania pakietów zapewnia dodatkową warstwę zabezpieczeń. Można określić listy ACL tylko punktów końcowych sieci. Nie można określić listy ACL dla sieci wirtualnej lub określonej podsieci zawarte w sieci wirtualnej. Zalecane jest toouse sieciowych grup zabezpieczeń (NSG) zamiast listy kontroli dostępu, jeśli to możliwe. Zobacz toolearn więcej informacji na temat grup NSG, [omówienie grupy zabezpieczeń sieci](virtual-networks-nsg.md)

Listy kontroli dostępu można skonfigurować przy użyciu programu PowerShell lub hello portalu Azure. tooconfigure sieci listy ACL za pomocą programu PowerShell, zobacz [listy kontroli dostępu zarządzanie dla punktów końcowych przy użyciu programu PowerShell](virtual-networks-acl-powershell.md). tooconfigure sieci listy ACL za pomocą hello Azure portalu, zobacz [jak tooset maszyny wirtualnej tooa punkty końcowe](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Za pomocą listy kontroli dostępu w sieci, można wykonać następujące hello:

* Selektywnie akceptowanie lub odrzucanie ruchu przychodzącego na podstawie zdalnego podsieci IPv4 adres zakresu tooa wejściowy punkt końcowy maszyny wirtualnej.
* Czarna lista adresów IP
* Tworzenie wielu reguł dla punktu końcowego maszyny wirtualnej
* Użyć reguły kolejności hello tooensure poprawny zestaw reguł są stosowane w punkcie końcowym podanej maszyny wirtualnej (najniższy toohighest)
* Określ listy ACL dla określonej podsieci zdalnego adresu IPv4.

Zobacz hello [Azure ogranicza](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) artykułu limitów listy ACL.

## <a name="how-acls-work"></a>Jak działają listy kontroli dostępu
Lista ACL jest obiekt, który zawiera listę reguł. Po utworzeniu listy ACL i zastosować je tooa punktu końcowego maszyny wirtualnej, filtrowanie pakietów odbywa się na powitania węzła hosta maszyny wirtualnej. Oznacza to, że ruch hello z zdalne adresy IP są filtrowane według węzła hosta hello pasujących reguł listy ACL zamiast na maszynie Wirtualnej. Zapobiega to wydatków na filtrowanie pakietów hello cenny cykli Procesora maszyny Wirtualnej.

Po utworzeniu maszyny wirtualnej, domyślne listy ACL jest umieszczany w miejscu tooblock cały ruch przychodzący. Jednak jeśli punkt końcowy jest tworzony dla (port 3389), następnie domyślnego hello lista ACL jest modyfikowany tooallow cały ruch przychodzący dla tego punktu końcowego. Ruch przychodzący z żadnych podsieci zdalnej jest następnie dozwolone toothat punktu końcowego i nie obsługi zapory jest wymagany. Wszystkie inne porty są blokowane dla ruchu przychodzącego, chyba że dla tych portów są tworzone punkty końcowe. Domyślnie jest mogą ruchu wychodzącego.

**Przykład tabeli domyślnej listy kontroli dostępu**

| **Reguła #** | **Podsieci zdalnej** | **Punkt końcowy** | **Akceptowanie/odrzucanie** |
| --- | --- | --- | --- |
| 100 |0.0.0.0/0 |3389 |Zezwolenie na |

## <a name="permit-and-deny"></a>Zezwalaj i Odmów
Można selektywnie zezwolenie na lub zezwalają na ruch sieciowy wejściowego punktu końcowego maszyny wirtualnej przez utworzenie reguły określające "zezwala na" lub "odmowy". Jest ważne toonote, że domyślnie po utworzeniu punktu końcowego, cały ruch jest dozwolony toohello punktu końcowego. Dlatego ważne jest, toounderstand jak toocreate akceptowanie/odrzucanie reguł i umieścić je w hello właściwej kolejności, jeśli chcesz szczegółową kontrolę nad sieci hello ruchu, który możesz wybrać tooallow tooreach hello — punktu końcowego maszyny wirtualnej.

Tooconsider punktów:

1. **Nie listy ACL —** domyślnie po utworzeniu punktu końcowego, firma Microsoft zezwala na wszystkie dla punktu końcowego hello.
2. **Zezwolenie na -** podczas dodawania co najmniej jeden "zezwala na" zakresów, domyślnie Odrzucasz innych zakresów. Tylko pakiety z hello dozwolony zakres adresów IP będą mogli toocommunicate z hello punktu końcowego maszyny wirtualnej.
3. **Odmów -** podczas dodawania co najmniej jeden "odmowy" zakresów, można wprowadzać innych zakresów ruchu domyślnie.
4. **Kombinacja zezwalanie i odmowa -** za pomocą kombinacji "zezwolenia" i "odrzucanie" ma toocarve limit określony adres IP zakresu toobe może lub nie.

## <a name="rules-and-rule-precedence"></a>Pierwszeństwo reguły i zasady
Listy kontroli dostępu sieciowego można skonfigurować w punktach końcowych określonej maszyny wirtualnej. Na przykład można określić sieci listy ACL dla punktu końcowego protokołu RDP utworzone na maszynie wirtualnej, które blokad klawisz dostępu dla niektórych adresów IP. Witaj w poniższej tabeli przedstawiono sposób toogrant dostępu toopublic wirtualnych adresów IP (VIP) niektórych zakresu toopermit dostępu protokołu RDP. Wszystkie inne zdalne adresy IP są odrzucane. Firma Microsoft wykonaj *najniższa ma pierwszeństwo przed* reguły kolejności.

### <a name="multiple-rules"></a>Wiele reguł
W poniższym przykładzie hello, jeśli chcesz, aby punkt końcowy protokołu RDP toohello dostępu tooallow tylko z dwa zakresy publicznych adresów IPv4 (65.0.0.0/8 i 159.0.0.0/8), można to osiągnąć, określając dwa *zezwolenie na* reguły. W takim przypadku od chwili utworzenia RDP jest domyślnie dla maszyny wirtualnej, może być toolock dół portem RDP toohello dostępu na podstawie podsieci zdalnej. Witaj w poniższym przykładzie pokazano sposób toogrant dostępu toopublic wirtualnych adresów IP (VIP) niektórych zakresu toopermit dostępu protokołu RDP. Wszystkie inne zdalne adresy IP są odrzucane. Dzieje się tak, ponieważ sieci listy kontroli dostępu można skonfigurować dla punktu końcowego określonej maszyny wirtualnej, i domyślnie odmówiono dostępu.

**Przykład — wiele reguł**

| **Reguła #** | **Podsieci zdalnej** | **Punkt końcowy** | **Akceptowanie/odrzucanie** |
| --- | --- | --- | --- |
| 100 |65.0.0.0/8 |3389 |Zezwolenie na |
| 200 |159.0.0.0/8 |3389 |Zezwolenie na |

### <a name="rule-order"></a>Kolejność reguł
Ponieważ wiele reguł można określić dla punktu końcowego, musi istnieć reguły tooorganize sposób reguły, które ma pierwszeństwo przed toodetermine kolejności. kolejność reguł Hello określa priorytet. Następujące listy ACL sieci *najniższa ma pierwszeństwo przed* reguły kolejności. W poniższym przykładzie hello, punkt końcowy hello na porcie 80 selektywnie otrzymuje tooonly dostępu do określonych zakresów adresów IP. tooconfigure, mamy regułę Odmów (zasada \# 100) adresów hello 175.1.0.1/24 miejsca. Następnie określono drugą regułę z ustawieniem pierwszeństwa czy zezwolenia na dostęp do tooall innych adresów w obszarze 175.0.0.0/8 200.

**Przykład — pierwszeństwo reguły**

| **Reguła #** | **Podsieci zdalnej** | **Punkt końcowy** | **Akceptowanie/odrzucanie** |
| --- | --- | --- | --- |
| 100 |175.1.0.1/24 |80 |Zablokuj |
| 200 |175.0.0.0/8 |80 |Zezwolenie na |

## <a name="network-acls-and-load-balanced-sets"></a>Sieci listy kontroli dostępu i zestawy równoważeniem obciążenia
Listy kontroli dostępu w sieci można określić dla punktu końcowego zestawu o zrównoważonym obciążeniu. Jeśli listy ACL jest określona dla zestawu o zrównoważonym obciążeniu, sieci hello listy ACL jest stosowane tooall maszyn wirtualnych w tym zestawu o zrównoważonym obciążeniu. Na przykład jeżeli zestaw o zrównoważonym obciążeniu jest tworzony z "Port 80" i zestawu o zrównoważonym obciążeniu hello zawiera 3 maszyn wirtualnych, sieci hello ACL utworzone w punkcie końcowym "Port 80" jednej maszyny Wirtualnej zostanie automatycznie zastosować toohello innych maszyn wirtualnych.

![Sieci listy kontroli dostępu i zestawy równoważeniem obciążenia](./media/virtual-networks-acl/IC674733.png)

## <a name="next-steps"></a>Następne kroki
[Zarządzanie listami kontroli dostępu dla punktów końcowych przy użyciu programu PowerShell](virtual-networks-acl-powershell.md)

