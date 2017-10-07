---
title: aaaManage zasad tworzenia kopii zapasowej StorSimple | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak używać toocreate usługi Menedżer StorSimple hello i zarządzanie ręcznego tworzenia kopii zapasowych, harmonogramy tworzenia kopii zapasowej i przechowywania kopii zapasowych."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a>Użyj zasad tworzenia kopii zapasowych toomanage usługi Menedżer StorSimple hello
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a>Omówienie
W tym samouczku opisano, jak toouse hello usługi Menedżer StorSimple **zasad tworzenia kopii zapasowych** strony toocontrol procesów tworzenia kopii zapasowej i przechowywania kopii zapasowych dla woluminów StorSimple. Opisano również sposób toocomplete ręcznego tworzenia kopii zapasowej.

Witaj **zasad tworzenia kopii zapasowych** strony można toomanage zasad tworzenia kopii zapasowych oraz harmonogram lokalne i migawki w chmurze. (Zasady tworzenia kopii zapasowej są używane tooconfigure harmonogramy tworzenia kopii zapasowej i przechowywania kopii zapasowych dla kolekcji woluminów). Zasady tworzenia kopii zapasowych umożliwiają tootake migawkę wiele woluminów jednocześnie. Oznacza to, że hello kopii zapasowych utworzonych przez zasady tworzenia kopii zapasowej będzie spójna w razie awarii kopie. Ta strona wyświetla hello zasad tworzenia kopii zapasowych, ich typów, hello skojarzone woluminy, hello liczbę kopii zapasowych przechowywane i hello tooenable opcji tych zasad.

Witaj **zasad tworzenia kopii zapasowych** strony można też hello toofilter istniejących zasad tworzenia kopii zapasowych przez jedną lub więcej hello następujące pola:

* **Nazwa zasad** — Witaj nazwy skojarzonej z zasadami hello. Witaj różne typy zasad:
  
  * Zaplanowane zasady, które jawnie są tworzone przez użytkownika hello.
  * Automatyczne zasady, które są tworzone, gdy hello domyślnego tworzenia kopii zapasowej dla tej opcji wolumin został włączony w czasie hello tworzenia woluminu. Te zasady są nazywane jako VolumeName_Default, gdzie nazwa woluminu odwołuje się nazwa toohello hello woluminu StorSimple skonfigurowany przez użytkownika hello w hello klasycznego portalu Azure. zasady automatycznego Hello spowodować codzienne migawki w chmurze od chwili urządzenia 22:30.
  * Zaimportować zasady, które zostały pierwotnie utworzone w hello StorSimple Snapshot Manager. Mają one znacznik hello StorSimple Snapshot Manager hosta, które hello zasady zostały zaimportowane z.
* **Woluminy** — Witaj woluminów skojarzonych z zasadami hello. Wszystkie woluminy hello skojarzonej z zasadami tworzenia kopii zapasowej są grupowane razem, gdy kopie zapasowe są tworzone.
* **Ostatnia kopia zapasowa pomyślnie** — hello Data i godzina hello ostatniego pomyślnego kopii zapasowej, która została wykonana z tymi zasadami.
* **Następną kopią zapasową** — hello Data i godzina hello następnego zaplanowanego tworzenia kopii zapasowej będą inicjowane przez te zasady.
* **Harmonogramy** — Witaj Liczba skojarzonych z zasadami tworzenia kopii zapasowej hello harmonogramów.

operacje Hello często używane, które można wykonywać na tej stronie są:

* Dodawanie zasad kopii zapasowych 
* Dodaj lub zmodyfikuj harmonogram 
* Usuń zasady tworzenia kopii zapasowej 
* Wykonaj kopię zapasową ręczne 
* Tworzenie niestandardowych zasad tworzenia kopii zapasowej z wieloma woluminami i harmonogramów 

## <a name="add-a-backup-policy"></a>Dodawanie zasad kopii zapasowych
Dodaj zasady tworzenia kopii zapasowej tooautomatically Harmonogram kopii zapasowych. Wykonaj następujące kroki w klasycznym portalu Azure tooadd zasad tworzenia kopii zapasowej dla urządzenia StorSimple hello hello. Po dodaniu hello zasad można określić harmonogramu (zobacz [Dodaj lub zmodyfikuj harmonogram](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

![Zobacz film](./media/storsimple-manage-backup-policies/Video_icon.png) **Zobacz film**

toowatch film wideo przedstawiający sposób toocreate lokalnie lub w chmurze kopii zapasowej zasad, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).

## <a name="add-or-modify-a-schedule"></a>Dodaj lub zmodyfikuj harmonogram
Można dodać lub zmodyfikować harmonogram, który jest dołączony tooan istniejących zasad tworzenia kopii zapasowej na urządzeniu StorSimple. Wykonaj następujące kroki w hello Azure classic portal tooadd hello lub zmodyfikować harmonogram.

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a>Usuń zasady tworzenia kopii zapasowej
Wykonaj następujące kroki w hello klasycznego portalu Azure toodelete zasady tworzenia kopii zapasowych w urządzeniu StorSimple hello.

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Wykonaj kopię zapasową ręczne
Wykonaj następujące kroki w hello klasycznego portalu Azure toocreate na żądanie (ręcznie) kopię zapasową pojedynczego woluminu hello.

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a>Tworzenie niestandardowych zasad tworzenia kopii zapasowej z wieloma woluminami i harmonogramów
Wykonaj następujące kroki w klasycznym portalu Azure toocreate niestandardowych zasad tworzenia kopii zapasowej, który zawiera wiele woluminów i harmonogramy hello hello.

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).

