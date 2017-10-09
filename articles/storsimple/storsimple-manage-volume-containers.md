---
title: "aaaManage Twojego kontenery woluminów StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak używasz hello Menedżer StorSimple kontenery woluminów usługi strony tooadd, zmodyfikować lub usunąć kontener woluminów."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a>Użyj kontenery woluminów StorSimple toomanage usługi Menedżer StorSimple hello
## <a name="overview"></a>Omówienie
W tym samouczku wyjaśniono, jak toouse hello toocreate usługi Menedżer StorSimple i zarządzanie nimi kontenery woluminów StorSimple.

Kontener woluminów na urządzeniu Microsoft Azure StorSimple zawiera jeden lub więcej woluminów, które mają konta magazynu, szyfrowania i ustawienia zużycie przepustowości. Urządzenie może mieć wiele kontenerów woluminu dla jego woluminów. 

Kontener woluminów obejmuje hello następujące atrybuty:

* **Woluminy** — hello warstwowej lub woluminów StorSimple, które znajdują się w kontenerze woluminów hello przypięty lokalnie. Kontener woluminów mogą zawierać zapasowe too256 woluminów StorSimple.
* **Szyfrowanie** — klucz szyfrowania, które mogą być definiowane dla każdego kontenera woluminów. Ten klucz jest używany do szyfrowania hello dane są przesyłane z chmury toohello urządzenia StorSimple. Z klasy zbrojnych AES 256-bitowym kluczem służy kluczem hello wprowadzonych przez użytkownika. toosecure danych, zalecamy zawsze włączone szyfrowanie magazynu w chmurze.
* **Konto magazynu** — Witaj konto magazynu dostawcy usług magazynu tooyour połączonych w chmurze. Wszystkie woluminy hello znajdującej się w kontenerze woluminów udostępnić to konto magazynu. Wybierz konto magazynu z istniejącej listy lub Utwórz nowe konto, jeśli Tworzenie kontenera woluminów hello, a następnie określisz hello poświadczeń dostępu dla tego konta.
* **Chmury przepustowości** — Witaj przepustowości przez urządzenie hello, gdy hello dane z urządzenia hello są wysyłane toohello chmury. Można wymusić kontroli przepustowości, określając wartość z zakresu od 1 do 1000 MB/s podczas definiowania tego kontenera. Tooconsume urządzenia hello pełną dostępną przepustowość, ustawić tooUnlimited tego pola. Można również utworzyć i zastosować przepustowości przepustowości tooallocate szablonu na podstawie harmonogramu.

![Strona kontenery woluminów](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

Ta poniższe procedury wyjaśniają, jak toouse hello StorSimple **kontenery woluminów** hello toocomplete strony następujące typowe operacje:

* Dodaj kontener woluminów 
* Modyfikowanie kontenera woluminów 
* Usunięcie kontenera woluminów 

## <a name="add-a-volume-container"></a>Dodaj kontener woluminów
Wykonaj następujące kroki tooadd kontenera woluminów hello.

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a>Modyfikowanie kontenera woluminów
Wykonaj następujące kroki toomodify kontenera woluminów hello.

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Usunięcie kontenera woluminów
Kontener woluminów obejmuje woluminy znajdujące się w nim. Można usunąć tylko wtedy, gdy wszystkie woluminy hello zawarte w niej najpierw zostaną usunięte. Wykonaj następujące kroki toodelete kontenera woluminów hello.

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zarządzania woluminami StorSimple](storsimple-manage-volumes.md). 
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).

