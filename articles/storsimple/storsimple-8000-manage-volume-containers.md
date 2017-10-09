---
title: "aaaManage Twojego kontenery woluminów StorSimple na urządzeniu z serii StorSimple 8000 hello | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak używasz hello Menedżera urządzeń StorSimple kontenery woluminów usługi strony tooadd, zmodyfikować lub usunąć kontener woluminów."
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
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a>Użyj kontenery woluminów StorSimple toomanage hello Menedżera urządzeń StorSimple usługi

## <a name="overview"></a>Omówienie
W tym samouczku wyjaśniono, jak toouse hello toocreate usługi Menedżer StorSimple urządzenia i zarządzać kontenery woluminów StorSimple.

Kontener woluminów na urządzeniu Microsoft Azure StorSimple zawiera jeden lub więcej woluminów, które mają konta magazynu, szyfrowania i ustawienia zużycie przepustowości. Urządzenie może mieć wiele kontenerów woluminu dla jego woluminów. 

Kontener woluminów obejmuje hello następujące atrybuty:

* **Woluminy** — hello warstwowej lub woluminów StorSimple, które znajdują się w kontenerze woluminów hello przypięty lokalnie. 
* **Szyfrowanie** — klucz szyfrowania, które mogą być definiowane dla każdego kontenera woluminów. Ten klucz jest używany do szyfrowania hello dane są przesyłane z chmury toohello urządzenia StorSimple. Z klasy zbrojnych AES 256-bitowym kluczem służy kluczem hello wprowadzonych przez użytkownika. toosecure danych, zalecamy zawsze włączone szyfrowanie magazynu w chmurze.
* **Konto magazynu** — Witaj konta magazynu platformy Azure, które jest używane toostore hello danych. Wszystkie woluminy hello znajdującej się w kontenerze woluminów udostępnić to konto magazynu. Wybierz konto magazynu z istniejącej listy lub Utwórz nowe konto, jeśli Tworzenie kontenera woluminów hello, a następnie określisz hello poświadczeń dostępu dla tego konta.
* **Chmury przepustowości** — Witaj przepustowości przez urządzenie hello, gdy hello dane z urządzenia hello są wysyłane toohello chmury. Można wymusić kontroli przepustowości, określając wartość z zakresu od 1 MB/s do 1000 MB/s, podczas tworzenia tego kontenera. Tooconsume urządzenia hello pełną dostępną przepustowość, ustawić tego pola zbyt**nieograniczone**. Można również utworzyć i zastosować przepustowości przepustowości tooallocate szablonu na podstawie harmonogramu.

Witaj poniższe procedury wyjaśniają, jak toouse hello StorSimple **kontenery woluminów** hello toocomplete bloku następujące typowe operacje:

* Dodaj kontener woluminów
* Modyfikowanie kontenera woluminów
* Usunięcie kontenera woluminów

## <a name="add-a-volume-container"></a>Dodaj kontener woluminów
Wykonaj następujące kroki tooadd kontenera woluminów hello.

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a>Modyfikowanie kontenera woluminów
Wykonaj następujące kroki toomodify kontenera woluminów hello.

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Usunięcie kontenera woluminów
Kontener woluminów obejmuje woluminy znajdujące się w nim. Można usunąć tylko wtedy, gdy wszystkie woluminy hello zawarte w niej najpierw zostaną usunięte. Wykonaj następujące kroki toodelete kontenera woluminów hello.

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zarządzania woluminami StorSimple](storsimple-8000-manage-volumes-u2.md). 
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

