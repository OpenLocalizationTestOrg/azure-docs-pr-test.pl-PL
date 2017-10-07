---
title: "Omówienie usługi Azure StorSimple danych Manager aaaMicrosoft | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie hello usługi Menedżer StorSimple danych (w podglądzie prywatnym)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a>Omówienie Menedżera danych StorSimple (podglądzie prywatnym)

## <a name="overview"></a>Omówienie

Microsoft Azure StorSimple jest rozwiązanie magazynu hybrydowego chmury, które adresy hello złożoności danych niestrukturalnych zwykle powiązanych ze udziałów plików. StorSimple używa magazynu w chmurze, jak rozszerzenie hello lokalnego rozwiązania i automatycznie warstwy danych przez Magazyn lokalne powitania i magazynu w chmurze. Zintegrowana ochrony danych z lokalnego i w chmurze migawek, eliminuje potrzebę hello sprawling infrastruktury magazynu. Archiwalne i odzyskiwanie po awarii jest również bezproblemowe z chmurą hello działający jako lokalizacji poza siedzibą firmy.

Hello usługi przekształcania danych, która wprowadzamy w tym dokumencie umożliwia możesz tooseamlessly dostępu hello danych StorSimple w chmurze hello. Ta usługa udostępnia interfejsy API tooextract dane z StorSimple i prezentować tooother Azure usług w formatach, które mogą być łatwo używane. w tej wersji zapoznawczej obsługiwane formaty Hello są obiekty BLOB platformy Azure i zasoby usługi Azure Media Services. Ta transformacja umożliwia możesz tooeasily przewodowy usług, takich jak usługi Azure Media Services, Azure HDInsight uczenie maszynowe Azure i usługi Azure Search dane toooperate na urządzeniu lokalnym serii StorSimple 8000.

Poniżej przedstawiono diagram blokowy wysokiego poziomu pokazujący to.

![Diagram ogólny](./media//storsimple-data-manager-overview/high-level-diagram.png)

W tym dokumencie opisano, jak można założyć prywatnej wersji zapoznawczej tej usługi. Wyjaśniono również, jak skorzystać z tej aplikacji toowrite usługi, które używają danych StorSimple i innymi usługami Azure w chmurze hello.

## <a name="sign-up-for-data-manager-preview"></a>Załóż Data Manager w wersji zapoznawczej
Przed zarejestrowaniem się usługi Menedżera danych hello Przejrzyj hello następujące wymagania wstępne.

### <a name="prerequisites"></a>Wymagania wstępne

Tym ćwiczeniu przyjęto założenie, że masz
* Aktywną subskrypcją platformy Azure.
* Access tooa zarejestrowane urządzenia serii StorSimple 8000 z aktualizacją
* Witaj wszystkie klucze skojarzone z urządzenia z serii StorSimple 8000 hello.

### <a name="sign-up"></a>Rejestrowanie

Witaj Menedżer StorSimple danych znajduje się w prywatnej wersji zapoznawczej. Wykonaj hello następujące kroki toosign konto w prywatnej wersji zapoznawczej tej usługi:

1.  Zaloguj się do hello portalu Azure z rozszerzeniem Menedżer StorSimple danych hello w: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager). Użyj toolog Twoje poświadczenia platformy Azure w.

2.  Kliknij przycisk hello  **+**  toocreate ikonę usługi. Kliknij przycisk **magazynu** , a następnie kliknij przycisk **Zobacz wszystkie** w otwartym bloku hello.

    ![Ikona danych Menedżera StorSimple wyszukiwania](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. Ikona Menedżer StorSimple danych hello jest widoczna.

    ![Wybierz ikonę Menedżera StorSimple danych](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. Kliknij ikonę Menedżer StorSimple danych, a następnie kliknij przycisk **Utwórz**. Wybierz subskrypcję hello mają tooenable hello prywatnej wersji zapoznawczej, a następnie kliknij przycisk **Zapisz się!**

    ![Zapisz się](./media/storsimple-data-manager-overview/sign-me-up.png)

5. To wysyła tooonboard żądania użytkownik. Firma Microsoft będzie dołączyć należy jak najszybciej. Po włączeniu subskrypcji można utworzyć usługi Menedżer StorSimple danych.

6. tooeasily dostępu do usługi Menedżer StorSimple danych hello, kliknij przycisk toopin ikonę gwiazdki hello go tooyour Ulubione.

    ![Dostęp do danych StorSimple menedżerów](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a>Następne kroki

[Użyj interfejsu użytkownika Menedżera danych StorSimple tootransform danych](storsimple-data-manager-ui.md).
