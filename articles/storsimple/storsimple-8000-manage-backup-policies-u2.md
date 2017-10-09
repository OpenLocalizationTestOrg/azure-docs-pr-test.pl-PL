---
title: zasady tworzenia kopii zapasowej serii StorSimple 8000 aaaManage | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak używać toocreate usługi Menedżer StorSimple urządzenia hello i zarządzanie ręcznego tworzenia kopii zapasowych, harmonogramy tworzenia kopii zapasowej i przechowywania kopii zapasowych na urządzeniu z serii StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a>Użyj usługi Menedżer StorSimple urządzenia hello w toomanage portalu Azure zasady tworzenia kopii zapasowej


## <a name="overview"></a>Omówienie

W tym samouczku opisano, jak toouse hello usługi Menedżer StorSimple urządzenia **kopii zapasowej zasad** procesów tworzenia kopii zapasowej toocontrol bloku i przechowywania kopii zapasowych dla woluminów StorSimple. Opisano również sposób toocomplete ręcznego tworzenia kopii zapasowej.

Podczas wykonywania kopii zapasowej woluminu można toocreate migawka lokalna i migawka w chmurze. W przypadku wykonywania kopii zapasowej woluminu przypiętego lokalnie, zaleca się określenie migawka w chmurze. Biorąc dużą liczbę lokalnych migawek woluminu przypiętego lokalnie, w połączeniu z zestawu danych, który ma wiele zmian spowoduje w sytuacji, w którym można szybko uruchomić poza lokalne miejsce. Jeśli wybierzesz tootake migawki lokalne, zaleca się zająć mniej tooback migawki codziennych hello ostatniego stanu, zachować je na dzień, a następnie usuń je.

Podczas wykonywania migawki chmury woluminu przypiętego lokalnie, możesz skopiować tylko zmienione hello danych toohello w chmurze, gdzie jest deduplikowany i skompresowane.

## <a name="hello-backup-policy-blade"></a>Blok zasady tworzenia kopii zapasowej Hello

Witaj **kopii zapasowej zasad** bloku dla urządzenia StorSimple umożliwia toomanage zasad tworzenia kopii zapasowych oraz harmonogram lokalne i migawki w chmurze. Zasady tworzenia kopii zapasowej są używane tooconfigure harmonogramy tworzenia kopii zapasowej i przechowywania kopii zapasowych dla kolekcji woluminów. Zasady tworzenia kopii zapasowych umożliwiają tootake migawkę wiele woluminów jednocześnie. Oznacza to, że hello kopii zapasowych utworzonych przez zasady tworzenia kopii zapasowej będzie spójna w razie awarii kopie.

tabelarycznej listę zasad tworzenia kopii zapasowych Hello umożliwia także możesz toofilter hello istniejących zasad tworzenia kopii zapasowych przez jedną lub więcej hello następujące pola:

* **Nazwa zasad** — Witaj nazwy skojarzonej z zasadami hello. Witaj różne typy zasad:

  * Zaplanowane zasady, które jawnie są tworzone przez użytkownika hello.
  * Zaimportować zasady, które zostały pierwotnie utworzone w hello StorSimple Snapshot Manager. Mają one znacznik hello StorSimple Snapshot Manager hosta, które hello zasady zostały zaimportowane z.

  > [!NOTE]
  > Automatyczne lub domyślne zasady tworzenia kopii zapasowej nie są już włączone w czasie hello tworzenia woluminu.

* **Ostatnia kopia zapasowa pomyślnie** — hello Data i godzina hello ostatniego pomyślnego kopii zapasowej, która została wykonana z tymi zasadami.

* **Następną kopią zapasową** — hello Data i godzina hello następnego zaplanowanego tworzenia kopii zapasowej będą inicjowane przez te zasady.

* **Woluminy** — Witaj woluminów skojarzonych z zasadami hello. Wszystkie woluminy hello skojarzonej z zasadami tworzenia kopii zapasowej są grupowane razem, gdy kopie zapasowe są tworzone.

* **Harmonogramy** — Witaj Liczba skojarzonych z zasadami tworzenia kopii zapasowej hello harmonogramów.

są często używane Hello operacje, które można wykonać dla zasad tworzenia kopii zapasowych:

* Dodawanie zasad kopii zapasowych
* Dodaj lub zmodyfikuj harmonogram
* Dodawanie lub usuwanie woluminu
* Usuń zasady tworzenia kopii zapasowej
* Wykonaj kopię zapasową ręczne

## <a name="add-a-backup-policy"></a>Dodawanie zasad kopii zapasowych

Dodaj zasady tworzenia kopii zapasowej tooautomatically Harmonogram kopii zapasowych. Najpierw należy utworzyć wolumin, nie ma żadnych zasad tworzenia kopii zapasowej domyślne skojarzone z woluminu. Należy go tooadd i przypisać zasady tworzenia kopii zapasowych danych woluminu tooprotect.

Wykonaj następujące kroki w hello tooadd portalu Azure zasady tworzenia kopii zapasowej dla urządzenia StorSimple hello. Po dodaniu hello zasad można określić harmonogramu (zobacz [Dodaj lub zmodyfikuj harmonogram](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a>Dodaj lub zmodyfikuj harmonogram

Można dodać lub zmodyfikować harmonogram, który jest dołączony tooan istniejących zasad tworzenia kopii zapasowej na urządzeniu StorSimple. Wykonaj następujące kroki w hello Azure tooadd portalu hello lub zmodyfikować harmonogram.

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a>Dodawanie lub usuwanie woluminu

Można dodawać i usuwać woluminu przypisane tooa zasady tworzenia kopii zapasowych w urządzeniu StorSimple. Wykonaj następujące kroki w hello Azure tooadd portalu hello, lub Usuń wolumin.

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a>Usuń zasady tworzenia kopii zapasowej

Wykonaj następujące kroki w hello toodelete portalu Azure zasady tworzenia kopii zapasowych w urządzeniu StorSimple hello.

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Wykonaj kopię zapasową ręczne

Wykonaj następujące kroki w hello toocreate portalu Azure na żądanie (ręcznie) kopię zapasową pojedynczego woluminu hello.

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

