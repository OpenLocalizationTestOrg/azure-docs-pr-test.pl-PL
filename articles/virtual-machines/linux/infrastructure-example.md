---
title: "aaaExample wskazówki infrastruktury platformy Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello klucza projekt i implementację wskazówki dotyczące wdrażania infrastruktury przykład na platformie Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6b307c0112203aa83e1fada81966fc265397a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a>Przykład wskazówki infrastruktury platformy Azure dla maszyn wirtualnych systemu Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

W tym artykule przedstawiono zbudowaniu przykład infrastruktury aplikacji. Firma Microsoft szczegółowo projektowania infrastruktury dla prostego sklepu online, która gromadzi wszystkie hello wskazówki i decyzji dotyczących konwencji nazewnictwa, zestawów dostępności, sieci wirtualnych i usług równoważenia obciążenia i faktycznie wdrażania maszyn wirtualnych (VM).

## <a name="example-workload"></a>Przykładowe obciążenie
Firma Adventure Works Cycles chce toobuild na platformie Azure, która składa się z aplikacji sklepu online:

* Dwa serwery nginx z powitania klienta frontonu w warstwa sieci web
* Dwa serwery nginx, przetwarzanie danych i zamówień w warstwie aplikacji
* Dwie bazy danych MongoDB serwerów częścią podzielonej klastra do przechowywania danych produktu i zamówień w warstwy bazy danych
* Dwa kontrolery domeny usługi Active Directory dla konta klienta i dostawców w warstwie uwierzytelniania
* Wszystkie serwery hello znajdują się w dwóch podsieci:
  * podsieci frontonu hello serwerów sieci web 
  * podsieć wewnętrznych serwerów aplikacji hello, bazy danych MongoDB klastra i kontrolerów domeny

![Diagram różnych warstw dla infrastruktury aplikacji](./media/infrastructure-example/example-tiers.png)

Bezpieczne przychodzącego ruchu w sieci web muszą być równoważeniem obciążenia między serwerami sieci web hello jak klienci Przeglądaj hello sklepu online. Kolejność przetwarzania ruchu sieciowego w postaci hello HTTP żąda od hello sieci web, które serwery muszą być równoważeniem obciążenia między serwerami aplikacji hello. Ponadto należy zaprojektować hello infrastruktury wysokiej dostępności.

Projekt wynikowy Hello musi uwzględniać:

* Subskrypcja platformy Azure i konta
* Pojedyncza grupa zasobów
* Azure Managed Disks
* Sieć wirtualną z dwiema podsieciami
* Zestawy dostępności dla hello maszyn wirtualnych z podobną rolę
* Maszyny wirtualne

Wszystkie powyższe hello wykonaj te konwencji nazewnictwa:

* Adventure Works Cycles używa **[obciążenia IT]-[lokalizacja]-[zasobów platformy Azure]** jako prefiksu
  * Na przykład "**azos**" (magazyn Azure On-line) jest hello imię i nazwisko obciążenia IT i "**użyj**" hello lokalizacji jest (wschodnie stany USA 2)
* W sieciach wirtualnych za pomocą AZOS-użycie-VN**[numer]**
* Zestawy dostępności używać azos-Użyj — jako-**[rola]**
* Nazwy maszyn wirtualnych użyć azos-Użyj-vm -**[vmname]**

## <a name="azure-subscriptions-and-accounts"></a>Subskrypcje platformy Azure i konta
Adventure Works Cycles korzysta z ich subskrypcją przedsiębiorstwa, o nazwie Adventure Works Enterprise subskrypcji, rozliczeń dla tej obciążenia IT tooprovide.

## <a name="storage"></a>Magazyn
Firma Adventure Works Cycles ustalić, czy powinny używać dysków zarządzanych Azure. Podczas tworzenia maszyn wirtualnych, są używane zarówno warstw magazynowania dostępne magazynu:

* **Magazynu w warstwie standardowa** hello serwerów sieci web, serwerów aplikacji i kontrolerów domeny i dysków z danymi.
* **Magazyn w warstwie Premium** hello bazy danych MongoDB podzielonej klastra serwerów i dysków z danymi.

## <a name="virtual-network-and-subnets"></a>Sieć wirtualna i podsieci
Ponieważ hello sieci wirtualnej sieci lokalnej cykle pracy Adventure toohello bieżące połączenie nie jest konieczne, zdecydowano, że w sieci wirtualnej tylko w chmurze.

One tworzone tylko na chmurze sieci wirtualnej z następującego ustawienia za pomocą portalu Azure hello hello:

* Nazwa: AZOS-użycie VN01
* Lokalizacji: Wschodnie stany USA 2
* Przestrzeń adresową sieci wirtualnej: 10.0.0.0/8
* Pierwszej podsieci:
  * Nazwa: frontonu
  * Przestrzeń adresowa: 10.0.1.0/24
* Drugi podsieci:
  * Nazwa: wewnętrznej bazy danych
  * Przestrzeń adresowa: 10.0.2.0/24

## <a name="availability-sets"></a>Zestawy dostępności
Wysoka dostępność toomaintain wszystkie cztery warstwy ich magazynu online, firma Adventure Works Cycles na cztery zestawy dostępności:

* **azos używany jako web** hello serwerów sieci web
* **azos używany jako aplikacji** dla serwerów aplikacji hello
* **azos używany jako db** hello serwerów w klastrze podzielonej hello bazy danych MongoDB
* **azos używany jako dc** hello kontrolerów domeny

## <a name="virtual-machines"></a>Maszyny wirtualne
Firma Adventure Works Cycles na powitania po nazw dla swoich maszynach wirtualnych platformy Azure:

* **azos użycie vm-web01** dla hello na pierwszym serwerze sieci web
* **azos użycie vm-web02** hello drugiego serwera sieci web
* **azos użycie vm-app01** dla pierwszego serwera aplikacji hello
* **azos użycie vm-app02** dla drugiego serwera aplikacji hello
* **azos użycie vm-db01** dla pierwszego serwera bazy danych MongoDB hello hello klastra
* **azos użycie vm-db02** hello drugiego serwera bazy danych MongoDB w klastrze hello
* **azos użycie vm-dc01** dla hello pierwszego kontrolera domeny
* **azos użycie vm-dc02** dla hello kontrolera domeny

Oto hello Wynikowa konfiguracja.

![Infrastruktura aplikacji końcowego wdrożona na platformie Azure](./media/infrastructure-example/example-config.png)

Ta konfiguracja obejmuje:

* Tylko w chmurze sieci wirtualnej z dwoma podsieciami (frontonu i wewnętrznej bazy danych)
* Dyskach platformy Azure zarządzanych za pomocą dysków w wersjach Standard i Premium
* Cztery zestawy dostępności, jeden dla każdej warstwy hello sklep online
* maszyny wirtualne Hello hello czterech warstw
* Zestaw o zrównoważonym obciążeniu zewnętrznych dla ruchu web oparty na protokole HTTPS z serwerów sieci web toohello internetowych hello
* Zestaw dla ruchu w sieci web niezaszyfrowane z serwerów aplikacji toohello serwerów sieci web hello o zrównoważonym obciążeniu wewnętrzny
* Pojedyncza grupa zasobów
