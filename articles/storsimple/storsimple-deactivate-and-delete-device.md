---
title: "aaaDeactivate i usuwanie urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooremove urządzenia StorSimple z usługi najpierw dezaktywowanie go, a następnie usuwając go."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed86bcd089aa957128e14b1709c836d938c131a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a>Dezaktywuj i usuwanie urządzenia StorSimple 8000 serii za pomocą usługi Menedżer StorSimple
## <a name="overview"></a>Omówienie
Możesz tootake urządzenia StorSimple poza usługi (na przykład, jeśli są zastępowanie lub uaktualnianie urządzenia lub jeśli już używasz StorSimple). Jeśli w przypadku hello należy toodeactivate hello urządzenia przed jego usunięciem. Dezaktywowanie, serwery hello połączenie między urządzeniem hello a hello odpowiedniej usługi Menedżer StorSimple. Ten samouczek wyjaśnia sposób tooremove urządzenia StorSimple z usługi najpierw dezaktywowanie go, a następnie usuwając go. 

Po dezaktywacji urządzenia żadnych danych, które były przechowywane lokalnie na urządzeniu hello nie będzie już dostępny. Można odzyskać tylko dane hello skojarzone z hello urządzenia, które były przechowywane w chmurze hello.  

> [!WARNING]
> Dezaktywacja jest operacją trwałe i nie można cofnąć. Nie można zarejestrować dezaktywować urządzenie przy użyciu usługi Menedżer StorSimple hello, chyba że jest najpierw Resetowanie ustawień fabrycznych domyślne toohello. 
> 
> Fabryka Hello zresetować proces usuwania wszystkich danych hello, które były przechowywane lokalnie na urządzeniu. Dlatego istotne jest utworzyć migawkę chmury wszystkich danych, aby dezaktywować urządzenie. Pozwoli to toorecover hello wszystkich danych, aby w późniejszym terminie.
> 
> 

Ten samouczek wyjaśnia, jak:

* Dezaktywować urządzenie i usunięcie danych hello
* Dezaktywować urządzenie i zachowywanie danych hello

Wyjaśniono również sposób Dezaktywacja i usuwanie działa na urządzeniu wirtualnym StorSimple.

> [!NOTE]
> Przed dezaktywacją urządzenia fizyczne lub wirtualne StorSimple, upewnij się, że toostop lub usunąć klientów i hosty, które są zależne od tego urządzenia.
> 
> 

## <a name="deactivate-and-delete-data"></a>Dezaktywuj i usuwanie danych
Jeśli planuje się usuwanie urządzeń hello całkowicie i nie ma danych hello tooretain na urządzeniu hello, następnie wykonaj następujące kroki hello.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate hello urządzenia i delete hello danych
1. Wcześniejsze toodeactivating urządzenie, musisz usunąć wszystkie hello woluminu kontenery (i woluminy hello) skojarzone z urządzeniem hello. Kontenery woluminów można usunąć tylko po usunięciu hello skojarzonych kopii zapasowych.
2. Dezaktywować urządzenie hello w następujący sposób:
   
   1. Na powitania usługi Menedżer StorSimple **urządzeń** strony, wybierz opcję hello urządzenia mają toodeactivate i, u dołu hello hello strony, kliknij przycisk **Dezaktywuj**.
   2. Zostanie wyświetlony komunikat potwierdzenia. Kliknij przycisk **tak** toocontinue. Witaj Dezaktywuj proces uruchomi i potrwać kilka minut toocomplete.
3. Po dezaktywacji możesz całkowicie usunąć urządzenie hello. Usuwanie urządzenia spowoduje usunięcie jej z listy hello usługi toohello podłączonych urządzeń. Usługa Hello można zarządzać już hello usunąć urządzenia. Użyj hello następujące kroki toodelete hello urządzenia:
   
   1. Na powitania usługi Menedżer StorSimple **urządzeń** wybierz dezaktywować urządzenie, że chcesz toodelete.
   2. Na dolnej hello na stronie powitania kliknij **usunąć**.
   3. Pojawi się monit o potwierdzenie. Kliknij przycisk **tak** toocontinue.
      
      Może upłynąć kilka minut, aż toobe urządzenia hello usunięte.

## <a name="deactivate-and-retain-data"></a>Dezaktywuj i Zachowaj dane
Jeśli są zainteresowani usuwanie hello urządzenia, ale tooretain hello danych, wypełnij hello następujące kroki.

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate urządzenia i zachowywanie danych hello
1. Dezaktywowanie hello urządzenia. Witaj wszystkie kontenery woluminów i pozostanie migawki hello hello urządzenia.
   
   1. Na powitania usługi Menedżer StorSimple **urządzeń** strony, wybierz opcję hello urządzenia mają toodeactivate i, u dołu hello hello strony, kliknij przycisk **Dezaktywuj**.
   2. Zostanie wyświetlony komunikat potwierdzenia. Kliknij przycisk **tak** toocontinue. Witaj Dezaktywuj proces uruchomi i potrwać kilka minut toocomplete.
2. Możesz teraz w trybie Failover hello kontenery woluminów i hello skojarzone migawki. Procedur można przejść za[trybu Failover i odzyskiwania po awarii dla urządzenia StorSimple](storsimple-device-failover-disaster-recovery.md).
3. Po dezaktywacji i trybu failover można całkowicie usunąć urządzenie hello. Usuwanie urządzenia spowoduje usunięcie jej z listy hello usługi toohello podłączonych urządzeń. Usługa Hello można zarządzać już hello usunąć urządzenia. Wykonaj następujące kroki toodelete hello urządzenia hello:
   
   1. Na powitania usługi Menedżer StorSimple **urządzeń** wybierz dezaktywować urządzenie, że chcesz toodelete.
   2. Na dolnej hello na stronie powitania kliknij **usunąć**.
   3. Pojawi się monit o potwierdzenie. Kliknij przycisk **tak** toocontinue.
      
      Może upłynąć kilka minut, aż toobe urządzenia hello usunięte.

## <a name="deactivate-and-delete-a-virtual-device"></a>Zdezaktywować i usunąć urządzenie wirtualne
Dla urządzenia wirtualnego StorSimple dezaktywacji cofa alokację hello maszyny wirtualnej. Następnie można usunąć maszyny wirtualnej hello i zasoby hello utworzone podczas inicjowania jej obsługi. Po dezaktywacji urządzenia wirtualnego hello, nie można go przywrócić tooits poprzedniego stanu. 

Dezaktywacja powoduje hello następujące akcje:

* Urządzenie wirtualne StorSimple Hello jest usuwany.
* Witaj OSDisk i dyski danych utworzone dla urządzenia wirtualnego StorSimple hello są usuwane.
* Witaj usługi hostowanej i sieci wirtualnej, które zostały utworzone podczas inicjowania obsługi administracyjnej są zachowywane. Jeśli nie używasz te jednostki, należy usunąć je ręcznie.
* Migawki w chmurze utworzone przez urządzenie wirtualne StorSimple hello są zachowywane.

## <a name="next-steps"></a>Następne kroki
* toorestore hello domyślne toofactory dezaktywować urządzenie znajduje się zbyt[przywrócić ustawienia domyślne toofactory urządzenia hello](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Aby uzyskać pomoc techniczną [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md).
* więcej informacji o toolearn, jak hello toouse usługi Menedżer StorSimple, przejdź za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md). 

