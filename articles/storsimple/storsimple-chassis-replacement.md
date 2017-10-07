---
title: "Podstawa montażowa aaaReplace na urządzeniu z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooremove i Zamień hello obudowy StorSimple obudowy podstawowego lub EBOD obudowy."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a>Zastąp podstawę hello na urządzeniu StorSimple
## <a name="overview"></a>Omówienie
Ten samouczek wyjaśnia sposób tooremove i Zastąp podstawę urządzenia z serii StorSimple 8000. model Hello StorSimple 8100 to urządzenie jednej obudowie (wspólnej obudowie), hello 8600 jest urządzeniem podwójną obudowy (dwie obudowy). W przypadku modelu 8600 są potencjalnie dwóch obudowy, które może nie działać na urządzeniu hello: hello podstawę dla podstawowego obudowa hello lub hello podstawę dla hello EBOD obudowy.

W obu przypadkach hello zastępczy podstawę, która jest dostarczany przez firmę Microsoft jest pusta. Nie zasilania i chłodzenia modułów (PCMs), moduły kontrolera stacje dysków półprzewodnikowych (SSD), dysków twardych (HDD) lub EBOD moduły będą dołączone.

> [!IMPORTANT]
> Przed usuwanie i zastępowanie hello obudowy, przejrzyj hello bezpieczeństwa informacji w [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="remove-hello-chassis"></a>Usuń hello obudowy
Wykonaj następujące kroki tooremove hello obudowy na urządzeniu StorSimple hello.

#### <a name="tooremove-a-chassis"></a>tooremove podstawę
1. Upewnij się, urządzenia StorSimple hello jest zamknięta i odłączone od wszystkich źródeł zasilania hello.
2. Usuń wszystkie hello sieci i kabli SAS, jeśli ma to zastosowanie.
3. Usuń jednostkę hello z hello stojaku.
4. Usuń poszczególnych dysków hello i zanotuj hello miejsc, w których są usuwane. Aby uzyskać więcej informacji, zobacz [Usuń dysk hello](storsimple-disk-drive-replacement.md#remove-the-disk-drive).
5. Na powitania obudowa EBOD (jeśli jest to hello podstawę, która nie powiodła się) Usuń hello EBOD kontrolera modułów. Aby uzyskać więcej informacji, zobacz [usunąć kontroler EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller). 
   
    Na powitania obudowa głównej (jeśli jest to hello podstawę, która nie powiodła się), Usuń kontrolery hello i pamiętaj hello miejsc, w których są usuwane. Aby uzyskać więcej informacji, zobacz [usunąć kontroler](storsimple-controller-replacement.md#remove-a-controller).

## <a name="install-hello-chassis"></a>Zainstaluj hello obudowy
Wykonaj następujące kroki tooinstall hello obudowy na urządzeniu StorSimple hello.

#### <a name="tooinstall-a-chassis"></a>tooinstall podstawę
1. Zainstaluj obudowy hello w stojaku hello. Aby uzyskać więcej informacji, zobacz [urządzenia w stojaku do urządzenia 8100 StorSimple](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) lub [urządzenia w stojaku do urządzenia 8600 StorSimple](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).
2. Po obudowy hello jest zainstalowany w stojaku hello, zainstalować moduły kontrolera hello w powitalne sam umieszcza poprzednio były zainstalowane w.
3. Zainstaluj hello dysków w hello sam umieszcza i gniazd poprzednio były zainstalowane w.
   
   > [!NOTE]
   > Firma Microsoft zaleca, aby najpierw zainstalować hello dyski SSD w gniazdach hello, a następnie zainstaluj hello dysków twardych.
   > 
   > 
4. Z urządzeniem hello zamontowane w stojaku hello i zainstalowane składniki hello Połącz źródła urządzenia toohello odpowiednie uprawnienia i Włącz hello urządzenia. Aby uzyskać więcej informacji, zobacz [Podłączanie kabli do urządzenia StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) lub [Podłączanie kabli do urządzenia StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).

