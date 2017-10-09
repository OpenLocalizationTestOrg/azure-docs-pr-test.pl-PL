---
title: "aaaPublish aplikacji w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toopublish aplikacji i zasobów w usłudze Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a>Jak toopublish aplikacji w usłudze RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Po utworzeniu kolekcji usługi RemoteApp, potrzebujesz aplikacji hello toopublish lub zasoby, które chcesz toomake dostępne dla użytkowników. Witaj obrazy szablonów zapewnionej w ramach subskrypcji mieć tylko kilka aplikacji opublikowanych przez domyślnie — tooshare hello inne aplikacje, należy toopublish je.

> [!NOTE]
> Potrzebujesz tooupdate aplikacji? Będziesz potrzebować zbyt[obraz powitania aktualizacji](remoteapp-update.md) pierwszy.
> 
> 

Na powitania **publikowania** w portalu hello, kliknij pozycję **publikowania**. Można dodać aplikację z obrazu szablonu **Start** menu lub podaj hello ścieżki toowhere hello aplikacja jest zainstalowana na powitania obrazu szablonu. Jeśli wybierzesz tooadd z hello **Start** menu, wybierz z listy hello toopublish aplikacji hello. Jeśli wybierzesz tooprovide hello ścieżki toohello aplikacji, wprowadź nazwę aplikacji hello i hello ścieżki toohello aplikacji. Używania zmiennych w ścieżce hello — na przykład "% systemdrive %" zamiast "c:\".

> [!NOTE]
> Jeśli chcesz tooadd aplikacji z hello **Start** menu, należy toohave *dodane toohello tej aplikacji **Start** menu w obrazie szablonu.* W przeciwnym razie RemoteApp zostanie wyświetlony tylko co *jest* na powitania **Start** należy mylić menu, a. 
> 
> toomake się, że aplikacja jest w hello **Start** menu, umieść plik skrótu - **lnk** — znajduje się w folderze Start\Programy %systemdrive%\ProgramData\Microsoft\Windows\Start hello.
> 
> Jeśli nie pamiętasz toohello aplikacji hello tooadd **Start** menu podczas tworzenia szablonu hello wybierz tooadd hello ścieżki toohello aplikacji. (Lub Utwórz ponownie obrazu szablonu, ale jest dość nieco więcej pracy).
> 
> 

