---
title: "tooAzure aaaConnect usługi Data Lake Store z sieciami wirtualnymi | Dokumentacja firmy Microsoft"
description: "Łączenie z sieciami wirtualnymi platformy Azure tooAzure Data Lake Store"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>Dostęp do usługi Azure Data Lake Store z maszyn wirtualnych w ramach sieci Wirtualnej platformy Azure
Azure Data Lake Store jest usługą PaaS, która działa na publiczne adresy Internet IP. Dowolnego serwera, który można połączyć z zwykle toohello publicznego Internetu może połączyć się z tooAzure również końcowych usługi Data Lake Store. Domyślnie wszystkie maszyny wirtualne, które znajdują się w sieci wirtualnych platformy Azure mogą uzyskiwać dostęp do Internetu hello i dlatego mogą uzyskiwać dostęp do usługi Azure Data Lake Store. Jest jednak możliwe tooconfigure VMs w toonot sieci Wirtualnej mają toohello dostęp do Internetu. Dla tych maszyn wirtualnych dostępu tooAzure Data Lake Store jest ograniczone również. Blokowanie publiczny dostęp do Internetu dla maszyn wirtualnych w sieci wirtualnych platformy Azure może odbywać się przy użyciu dowolnego hello następujące podejście.

* Konfigurując grupy zabezpieczeń sieci (NSG)
* Konfigurując użytkownika zdefiniowanych tras przez
* Poprzez wymianę tras za pomocą protokołu BGP (standardowego dynamiczny routing protokołu) stosowania tego bloku ExpressRoute dostępu toohello Internet

W tym artykule dowiesz się, jak tooenable dostęp toohello Azure Data Lake Store z maszyn wirtualnych platformy Azure, które zostały tooaccess ograniczone, który zasobów przy użyciu jednej z trzech metod hello wymienionych powyżej.

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a>Włączanie tooAzure łączność usługi Data Lake Store z maszyn wirtualnych z ograniczeniami łączności
tooaccess Azure Data Lake przechowywania z tych maszyn wirtualnych, należy je skonfigurować adres IP hello tooaccess gdzie hello konta usługi Azure Data Lake Store jest dostępny. Możesz określić adresy IP powitania dla kont usługi Data Lake Store za rozpoznawania nazw DNS hello kont (`<account>.azuredatalakestore.net`). Dla tego można użyć narzędzia takie jak **nslookup**. Otwórz wiersz polecenia na komputerze, a następnie uruchom następujące polecenie hello.

    nslookup mydatastore.azuredatalakestore.net

Witaj dane wyjściowe podobne hello następującego. Witaj wartość względem **adres** właściwość jest hello adresu IP skojarzonego z kontem usługi Data Lake Store.

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>Włączenie łączności z ograniczeniami przy użyciu NSG maszyn wirtualnych
Stosowania reguły NSG tooblock dostępu toohello Internet, możesz utworzyć inną NSG, umożliwiająca dostęp toohello adres IP sklepu Lake danych. Więcej informacji na temat reguły NSG są dostępne pod adresem [co to jest grupa zabezpieczeń sieci?](../virtual-network/virtual-networks-nsg.md). Aby uzyskać instrukcje dotyczące grup NSG toocreate zobacz temat [jak grupy NSG toomanage przy użyciu hello portalu Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>Włączenie łączności z ograniczeniami przy użyciu przez lub ExpressRoute maszyn wirtualnych
Gdy trasy, Udr lub wymieniane BGP trasy są używane tooblock toohello dostępu do Internetu, specjalne trasy musi toobe skonfigurowane tak, aby maszyn wirtualnych w podsieciach takie mogą uzyskiwać dostęp do punktów końcowych usługi Data Lake Store. Aby uzyskać więcej informacji, zobacz [co to są trasy zdefiniowane przez użytkownika?](../virtual-network/virtual-networks-udr-overview.md). Aby uzyskać instrukcje dotyczące tworzenia Udr, zobacz [utworzyć Udr w Menedżerze zasobów](../virtual-network/virtual-network-create-udr-arm-ps.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>Włączenie łączności z ograniczeniami przy użyciu usługi ExpressRoute maszyn wirtualnych
Po skonfigurowaniu obwodu usługi ExpressRoute, serwery lokalne powitania można uzyskać dostępu do usługi Data Lake Store za pośrednictwem publicznej komunikacji równorzędnej. Więcej informacji na temat konfigurowania usługi ExpressRoute dla publicznej komunikacji równorzędnej jest dostępne pod adresem [ExpressRoute — często zadawane pytania](../expressroute/expressroute-faqs.md).

## <a name="see-also"></a>Zobacz też
* [Omówienie usługi Azure Data Lake Store](data-lake-store-overview.md)
* [Zabezpieczanie danych przechowywanych w usłudze Azure Data Lake Store](data-lake-store-security-overview.md)

