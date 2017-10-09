---
title: "aaaManage rekordy kontroli dostępu w StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak kontroli dostępu toouse rekordy hosty, które mogą się łączyć tooa wolumin w urządzeniu StorSimple hello toodetermine (ACRs)."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Użyj rekordy kontroli dostępu toomanage usługi Menedżer StorSimple hello
## <a name="overview"></a>Omówienie
Rekordy kontroli dostępu (ACRs) pozwalają toospecify hosty, które mogą się łączyć tooa wolumin w urządzeniu StorSimple hello. ACRs są ustawiane tooa określonego woluminu i zawierają hello iSCSI nazwy kwalifikowane (nazw IQN) hello hostów. Gdy host podejmie próbę tooconnect tooa woluminu, hello urządzenia sprawdza powitalne ACR skojarzone z tym woluminie nazwy IQN hello i jeśli istnieje dopasowanie, a następnie hello jest nawiązywane połączenie. Kontrola dostępu Hello rejestruje sekcji na powitania **Konfiguruj** wszystkie rekordy kontroli dostępu hello zostanie wyświetlona strona z hello odpowiadającego nazw IQN hello hostów.

W tym samouczku opisano następujące typowe zadania związane z ACR hello:

* Dodaj rekord kontroli dostępu 
* Edytuj rekord kontroli dostępu 
* Usuń rekord kontroli dostępu 

> [!IMPORTANT]
> * Podczas przypisywania ACR tooa woluminu, należy zadbać czy hello wolumin nie jest jednocześnie dostępna przez więcej niż jednego hosta z systemem innym niż klastrowane, ponieważ może to spowodować uszkodzenie hello woluminu. 
> * Podczas usuwania ACR z woluminu, upewnij się, że odpowiednie hostujących hello nie uzyskuje dostęp do woluminu hello, usunięcia hello może powodować zakłócenia odczytu i zapisu.
> 
> 

## <a name="add-an-access-control-record"></a>Dodaj rekord kontroli dostępu
Użyj usługi Menedżer StorSimple hello **Konfiguruj** tooadd ACRs strony. Zazwyczaj co ACR zostanie skojarzony z jednego woluminu.

Wykonaj następujące kroki tooadd ACR hello.

#### <a name="tooadd-an-access-control-record"></a>tooadd rekord kontroli dostępu
1. Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie nazwę usługi hello, a następnie kliknij hello **Konfiguruj** kartę.
2. W hello tabelarycznej listę pod **rekordy kontroli dostępu**, dostawy **nazwa** dla rekordu ACR.
3. Podaj hello nazwę IQN hosta z systemem Windows w obszarze **Nazwa inicjatora iSCSI**. Witaj tooget IQN hosta z systemem Windows Server, hello następujące:
   
   * Uruchom inicjatora iSCSI firmy Microsoft hello na hoście z systemem Windows.
   * W hello **właściwości inicjatora iSCSI** okna na powitania **konfiguracji** karcie zaznacz i skopiuj ciąg hello z hello **Nazwa inicjatora** pola.
   * Wklej ten ciąg hello **Nazwa inicjatora iSCSI** pola w tabeli ACRs hello w hello klasycznego portalu Azure.
4. Kliknij przycisk **zapisać** hello toosave nowo utworzony ACR. Witaj tabelarycznej listę zostanie zaktualizowany tooreflect można to dodawanie.

## <a name="edit-an-access-control-record"></a>Edytuj rekord kontroli dostępu
Użyj hello **Konfiguruj** strony w hello Azure classic portal tooedit ACRs. 

> [!NOTE]
> Można modyfikować tylko ACRs, które nie są obecnie w użyciu. tooedit ACR skojarzony z woluminem, który jest obecnie używany, musisz najpierw wykonać hello woluminu w trybie offline.
> 
> 

Wykonaj następujące kroki tooedit ACR hello.

#### <a name="tooedit-an-access-control-record"></a>tooedit rekord kontroli dostępu
1. Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie nazwę usługi hello, a następnie kliknij hello **Konfiguruj** kartę.
2. W hello tabelarycznej listę rekordy kontroli dostępu hello, umieść kursor nad hello ACR, że chcesz toomodify.
3. Podaj nową nazwę i/lub IQN dla hello ACR.
4. Kliknij przycisk **zapisać** toosave hello zmodyfikować ACR. Witaj tabelarycznej listę zostanie zaktualizowany tooreflect można tej zmiany.

## <a name="delete-an-access-control-record"></a>Usuń rekord kontroli dostępu
Użyj hello **Konfiguruj** strony w hello Azure classic portal toodelete ACRs. 

> [!NOTE]
> Można usunąć tylko ACRs, które nie są obecnie w użyciu. toodelete ACR skojarzony z woluminem, który jest obecnie używany, musisz najpierw wykonać hello woluminu w trybie offline.
> 
> 

Wykonaj hello następujące kroki toodelete rekord kontroli dostępu.

#### <a name="toodelete-an-access-control-record"></a>toodelete rekord kontroli dostępu
1. Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie nazwę usługi hello, a następnie kliknij hello **Konfiguruj** kartę.
2. W hello tabelarycznej listę rekordy kontroli dostępu hello (ACRs), umieść kursor nad hello ACR, że chcesz toodelete.
3. Ikona usuwania (**x**) będą wyświetlane w hello extreme prawej kolumnie dla hello ACR wybrany. Kliknij przycisk hello **x** ikonę toodelete hello ACR.
4. Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak** toocontinue z hello usunięcia. Hello tabelarycznej listę zostaną zaktualizowane tooreflect hello usunięcia.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [zarządzania woluminami StorSimple](storsimple-manage-volumes.md).
* Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).

