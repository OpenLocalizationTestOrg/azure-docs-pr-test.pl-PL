---
title: "Witaj aaaModify dane 0 ustawienia na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse środowiska Windows PowerShell dla StorSimple tooreconfigure hello interfejs sieciowy 0 danych na urządzeniu StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a>Zmodyfikuj ustawienia interfejsu sieciowego 0 danych hello na urządzeniu StorSimple
## <a name="overview"></a>Omówienie
Microsoft Azure StorSimple urządzenie ma sześć interfejsów sieciowych, dane 0 tooDATA 5. Witaj dane 0 interfejsu zawsze jest skonfigurowana za pośrednictwem interfejsu programu Windows PowerShell hello lub konsoli szeregowej hello i jest automatycznie włączoną obsługę chmury. Należy pamiętać, że nie można skonfigurować interfejs sieciowy 0 danych za pośrednictwem hello klasycznego portalu Azure. 

Witaj interfejs został skonfigurowany za pomocą Kreatora instalacji hello podczas pierwszego wdrożenia urządzenia StorSimple hello dane 0. Jeśli urządzenie hello jest w trybie operacyjnych, może być konieczne tooreconfigure dane 0 ustawienia. W tym samouczku udostępnia dwie metody ustawienia sieci 0 danych toomodify, zarówno za pomocą programu Windows PowerShell dla StorSimple.

Po przeczytaniu tego samouczka, będą mieć możliwość:

* Modyfikowanie danych 0 ustawienie za pomocą Kreatora instalacji hello sieci
* Modyfikowanie ustawień sieciowych 0 danych za pośrednictwem hello `Set-HcsNetInterface` polecenia cmdlet

## <a name="modify-data-0-network-settings-through-setup-wizard"></a>Modyfikowanie ustawień sieciowych 0 danych za pomocą Kreatora konfiguracji
Można ponownie skonfigurować ustawienia sieciowe 0 danych, łącząc interfejsu programu Windows PowerShell toohello urządzenia StorSimple i uruchomić sesję kreatora instalacji. Wykonaj hello następujące kroki toomodify dane 0 ustawienia:

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a>Ustawienia sieciowe 0 danych toomodify za pośrednictwem Kreatora instalacji
1. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**. Po wyświetleniu monitu podaj hello **hasło administratora urządzenia**. Witaj domyślne hasło jest `Password1`.
2. Witaj wiersza polecenia wpisz:
   
    `Invoke-HcsSetupWizard`
3. Kreator instalacji pojawi się toohelp skonfigurować hello dane 0 interfejsu urządzenia. Podanie nowej wartości hello adres IP, bramy i maski podsieci.

> [!NOTE]
> Witaj, stałe adresy IP, należy ponownie skonfigurować za pomocą hello toobe kontrolerów **Konfiguruj** strony hello urządzenia StorSimple w hello klasycznego portalu Azure. Aby uzyskać więcej informacji, przejdź zbyt[zmodyfikować interfejsów sieciowych](storsimple-modify-device-config.md#modify-network-interfaces).
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>Modyfikowanie ustawień sieciowych 0 danych za pomocą polecenia cmdlet Set-HcsNetInterface
Alternatywną metodą tooreconfigure dane 0 interfejs sieciowy jest przy użyciu hello hello `Set-HcsNetInterface` polecenia cmdlet. polecenia cmdlet Hello jest wykonywany z interfejsu programu Windows PowerShell hello urządzenia StorSimple. Korzystając z tej procedury, stałe adresy IP kontrolera hello można również skonfigurować w tym miejscu. Wykonaj hello następujące kroki toomodify hello dane 0 ustawienia: 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a>Ustawienia sieci 0 danych toomodify za pomocą polecenia cmdlet hello HcsNetInterface zestawu
1. W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**. Po wyświetleniu monitu podaj hasło administratora urządzenia hello. Witaj domyślne hasło jest `Password1`.
2. Witaj wiersza polecenia wpisz:
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    W nawiasach hello pod kątem wpisz hello następujące wartości dla danych 0:
   
   * Adres IPv4
   * Brama IPv4
   * Maska podsieci IPv4
   * Stały adres IPv4 dla kontrolera 0
   * Stały adres IPv4 dla kontrolera 1
     
     Aby uzyskać więcej informacji na powitania Użyj tego polecenia cmdlet, przejdź zbyt[programu Windows PowerShell dla StorSimple dokumentacji poleceń cmdlet](https://technet.microsoft.com/library/dn688161.aspx).

## <a name="next-steps"></a>Następne kroki
* Interfejsy sieciowe tooconfigure inne niż dane 0, można użyć hello [strony konfiguracji w hello klasycznego portalu Azure](storsimple-modify-device-config.md). 
* Jeśli wystąpią problemy podczas konfigurowania interfejsów sieciowych, zapoznaj się zbyt[Rozwiązywanie problemów dotyczących wdrożenia](storsimple-troubleshoot-deployment.md).

