---
title: "aaaUpload niestandardowego obrazu usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupload niestandardowego obrazu usługi Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>Przekaż obraz niestandardowy usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Utworzono obrazu niestandardowego szablonu lub zaktualizować go ze zmianami, trzeba tooupload biblioteki obrazu usługi Azure RemoteApp tooyour obrazu. Wykonaj następujące kroki.

## <a name="before-you-start"></a>Przed rozpoczęciem
1. Upewnij się, niestandardowy obraz spełnia hello [wymagania dotyczące obrazu](remoteapp-imagereqs.md) i [wymagań aplikacji](remoteapp-appreqs.md).
2. Zainstaluj hello [modułu Azure PowerShell](/powershell/azure/overview).

## <a name="step-by-step-on-how-tooupload-custom-image"></a>Krok po kroku na temat tooupload niestandardowego obrazu
1. Otwórz Portal zarządzania Azure i przejdź toohello RemoteApp strony.
2. Na powitania **obrazy szablonów** , kliknij pozycję **przekazać** u dołu hello hello strony.
3. Wprowadź przyjazną nazwę dla obrazu i określ lokalizację konta magazynu hello. Upewnij się, lokalizacja hello jest hello tej samej lokalizacji co kolekcji usługi RemoteApp lub lokalizację, gdzie ma zostać toocreate jeden.
4. Po wyświetleniu monitu, Pobierz hello skryptu tooyour komputera lokalnego.
5. Skopiuj parametry polecenia hello w Schowku tooyour pole tekstowe hello.
6. Otwórz okno programu Windows PowerShell z podwyższonym poziomem uprawnień.
7. Z hello z podwyższonym poziomem uprawnień okno programu Windows PowerShell Przejdź toohello tym samym katalogu, którego pobrano hello skryptu.
8. Witaj Wklej skopiowane polecenie i naciśnij klawisz **Enter**.
   
   rozpocznie się proces przekazywania Hello i czas trwania może zależeć od wielu czynników, takich jak szybkość sieci, a rozmiar obrazu hello
9. Jeśli Twoje przekazywania nie powiedzie się z powodu przerwy w działaniu sieci lub rzeczy jak, zawsze można wznowić procesu przekazywania hello rozpoczęcia. tooresume przekazanie, uruchom ponownie, używając skrypt hello hello sam wiersza polecenia.

> [!WARNING]
> Nigdy nie należy zmodyfikować skrypt przekazywania hello. Sprawdzania wymagań zostać zaimplementowany tooensure, który hello obraz spełnia hello obrazu wymagania i wymagania dotyczące aplikacji.
> 
> 

## <a name="common-problems"></a>Typowe problemy
* Upewnij się, że używasz programu Windows PowerShell, nie programu Azure PowerShell. Moduł Azure PowerShell hello tooinstall jest potrzebna, ponieważ niektóre moduły są potrzebne podczas procesu przekazywania hello.
* Nigdy nie zmienia hello skryptu, sprawdzanie poprawności istnieją dla Twojej wygody.
* Jeśli plik vhd hello pobiera zablokowane podczas przekazywania, skopiuj plik hello, lub przenieś go tooa nowe przekazywania lokalizacji, a następnie spróbuj ponownie. Może to być niektórych procesu systemu Windows, który uniemożliwia przekazywania.  

