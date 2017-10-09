---
title: "toorun Express emulatora aaaUsing i debugowania platformy Azure w chmurze usługi na komputerze lokalnym | Dokumentacja firmy Microsoft"
description: "Przy użyciu emulatora Express toorun i debugowania usługi w chmurze, na komputerze lokalnym"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a>Przy użyciu emulatora Express toorun i debugowania platformy Azure usługa w chmurze na komputerze lokalnym
Przy użyciu emulatora Express, można testowanie i debugowanie usługi w chmurze bez konieczności uruchamiania programu Visual Studio jako administrator. Możesz ustawić toouse ustawienia Twojego projektu albo Express emulatora lub hello pełnego emulatora, w zależności od wymagań hello usługi w chmurze. Aby uzyskać więcej informacji na temat pełnego emulatora hello, zobacz [uruchomić aplikację Azure w hello obliczeniowe emulatora](storage/common/storage-use-emulator.md).

## <a name="using-emulator-express-in-visual-studio"></a>Przy użyciu ekspresowej wersji emulatora w programie Visual Studio
Podczas tworzenia projektu platformy Azure w wersji 2.3 zestawu SDK platformy Azure lub nowszym Express emulatora automatycznie jest używany. Dla istniejących projektów, które zostały utworzone przy użyciu starszej wersji hello Azure SDK Użyj hello następujące kroki tooselect emulatora Express:

1. Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz z menu kontekstowego hello **właściwości**.

1. Na stronach właściwości projektów hello, wybierz hello **Web** kartę.

    ![Właściwości projektu usługi w chmurze Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. W obszarze **lokalnego serwera wdrożeniowego**, wybierz pozycję **opcję Użyj usługi IIS Express**.

1. W obszarze **emulatora**, wybierz pozycję **Express emulatora użyj**.
   
1. toolaunch hello emulatora Express, uruchom następujące polecenie w wierszu polecenia hello: 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Ograniczenia Express emulatora
znane ograniczenia Express emulatora Hello następujące problemy: 

- Ekspresowej wersji emulatora nie jest zgodny z serwera sieci Web usług IIS.
- Usługi w chmurze może zawierać wiele ról, ale każda rola jest ograniczona tooone wystąpienia.
- Nie można uzyskać dostępu do numerów portów poniżej 1000. Jeśli używasz dostawcę uwierzytelniania, która zwykle używa portu poniżej 1000, może być konieczne toochange tego numeru portu tooa wartość przekracza 1000.
- Ograniczenia dotyczące toohello obliczeniowe emulatora usługi Azure mają zastosowanie również tooEmulator Express. Na przykład nie może mieć więcej niż 50 wystąpień roli dla wdrożenia. Aby uzyskać więcej informacji na temat hello obliczeniowe emulatora usługi Azure, zobacz [uruchomić aplikację Azure w hello obliczeniowe emulatora](http://go.microsoft.com/fwlink/p/?LinkId=623050).

## <a name="next-steps"></a>Następne kroki
[Debugowanie usług w chmurze Azure](https://msdn.microsoft.com/library/azure/ee405479.aspx)
