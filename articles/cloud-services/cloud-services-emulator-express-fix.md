---
title: "Instalacji ekspresowej wersji emulatora do debugowania aplikacji usługi w chmurze w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak instalowanie pakietu redystrybucyjnego C++, aby włączyć emulatora Express programu Visual Studio"
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
ms.openlocfilehash: 05d672dcb1335c617bb8d8cae43947bcd5e9ab3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-emulator-express-to-debug-cloud-services-application-in-vs-2017"></a>Debugowanie aplikacji usługi w chmurze w VS 2017 przy użyciu emulatora Express
W tym artykule wyjaśniono, jak użyć emulatora Express do debugowania aplikacji usługi w chmurze w VS 2017 r.

## <a name="background-context"></a>Kontekst tła
Ekspresowej wersji emulatora jest używany domyślnie do debugowania role sieci Web usługi w chmurze i proces roboczy w programie Visual Studio. To ustawienie jest określone na stronie właściwości projektu usługi w chmurze.

![Otwórz właściwości projektu][0]

![Emulator express został wybrany jako domyślny][1]

[Visual C++ Redistributable] [ Visual C++ Redistributable] express dla programu Visual Studio jest wymagany przez Emulator. Obecnie nie jest instalowana z obciążeniem, platformy Azure. Po gestu F5 debugowanie aplikacji usługi w chmurze Visual Studio będzie monit Zainstaluj ten składnik i kontynuować debugowanie.

![Monituj o zainstaluj pakiet redystrybucyjny programu C++][2]

Kliknij przycisk Tak, aby zainstalować pakiet redystrybucyjny programu C++.

![Instalowanie pakietu redystrybucyjnego C++][3]

Naciśnij klawisz F5, aby ponownie uruchomić sesji debugowania.

![Rozpocznij debugowanie][4]

![Debugowanie powiodło się][5]

> Uwaga: Instalowanie pakietu redystrybucyjnego Visual C++ jest jednorazowe nakładu pracy. Jeśli zostały uaktualniania ze starszej wersji zestawu SDK platformy Azure i zainstalowaniu emulatora Express nie wystąpi ten problem.
> 
> 

## <a name="manual-workaround"></a>Obejście ręczne
Można także zainstalować [Visual C++ Redistributable] [ Visual C++ Redistributable] ręcznie i zostaną one zastosowane sam efekt, jak jak Visual Studio na nim zainstalowany w tym systemie.

[VCRedist_x86.exe][vcredist_x86.exe]

[VCRedist_x64.exe][vcredist_x64.exe]

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o przy użyciu emulatora usługi Azure komputera do debugowania aplikacji usługi w chmurze w programie Visual Studio: [przy użyciu emulatora Express by przeprowadzić debugowanie usługi w chmurze na komputerze lokalnym][Using Emulator Express to run and debug a cloud service on a local machine]

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express to run and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
