---
title: "aplikacje usługi w chmurze toodebug w programie Visual Studio express emulatora aaaSetup | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooinstall hello C++ tooenable pakietu redystrybucyjnego emulatora Express programu Visual Studio"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 6fb506f0b1384f2e52310799eb5ae2a102d777bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a>Używanie emulatora Express toodebug aplikacji usługi w chmurze w VS 2017
W tym artykule opisano sposób aplikacji Express emulatora usługi w chmurze toodebug toouse w VS 2017 r.

## <a name="background-context"></a>Kontekst tła
Ekspresowej wersji emulatora jest używany domyślnie do debugowania role sieci Web usługi w chmurze i proces roboczy w programie Visual Studio. To ustawienie jest określone na stronie właściwości projektu usługi w chmurze hello.

![Otwórz właściwości projektu][0]

![Emulator express został wybrany jako domyślny][1]

Witaj [Visual C++ Redistributable] [ Visual C++ Redistributable] express dla programu Visual Studio jest wymagany przez Emulator. Obecnie nie jest instalowany z hello Azure obciążenia. Po F5 gestu toodebug aplikacji usługi w chmurze, Visual Studio będzie monitować tooinstall ten składnik i kontynuować debugowanie.

![Monituj o zainstaluj pakiet redystrybucyjny programu C++][2]

Kliknij przycisk Tak tooinstall C++ Redistributable.

![Instalowanie pakietu redystrybucyjnego C++][3]

Naciśnij klawisz F5 ponownie toolaunch sesji debugowania.

![Rozpocznij debugowanie][4]

![Debugowanie powiodło się][5]

> Uwaga: Instalowanie pakietu redystrybucyjnego Visual C++ jest jednorazowe nakładu pracy. Jeśli zostały uaktualniania ze starszej wersji zestawu SDK platformy Azure i zainstalowaniu emulatora Express nie wystąpi ten problem.
> 
> 

## <a name="manual-workaround"></a>Obejście ręczne
Można także zainstalować hello [Visual C++ Redistributable] [ Visual C++ Redistributable] ręcznie i zostaną one zastosowane sam efekt, jak jak Visual Studio na nim zainstalowany w tym systemie.

[VCRedist_x86.exe][vcredist_x86.exe]

[VCRedist_x64.exe][vcredist_x64.exe]

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o przy użyciu emulatora usługi Azure komputera toodebug aplikacji usługi w chmurze w programie Visual Studio: [toorun przy użyciu emulatora Express i debugowania usługi w chmurze na komputerze lokalnym][Using Emulator Express toorun and debug a cloud service on a local machine]

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express toorun and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
