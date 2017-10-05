---
title: "Przekaż obraz niestandardowy usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przekazać obraz niestandardowy usługi Azure RemoteApp"
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
ms.openlocfilehash: 5a235fac88d6e95ea294bda197641108acb4a09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>Przekaż obraz niestandardowy usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Teraz, gdy utworzono obrazu niestandardowego szablonu lub zaktualizować go ze zmianami, musisz przekazać go do biblioteki obrazu usługi Azure RemoteApp. Wykonaj następujące kroki.

## <a name="before-you-start"></a>Przed rozpoczęciem
1. Upewnij się, niestandardowy obraz spełnia [wymagania dotyczące obrazu](remoteapp-imagereqs.md) i [wymagań aplikacji](remoteapp-appreqs.md).
2. Zainstaluj [modułu Azure PowerShell](/powershell/azure/overview).

## <a name="step-by-step-on-how-to-upload-custom-image"></a>Krok po kroku na temat przekazywania niestandardowego obrazu
1. Otwórz Portal zarządzania Azure i przejdź do strony usługi RemoteApp.
2. Na **obrazy szablonów** , kliknij pozycję **przekazać** w dolnej części strony.
3. Wprowadź przyjazną nazwę dla obrazu i określ lokalizację konta magazynu. Upewnij się, że lokalizacja jest tej samej lokalizacji co kolekcji usługi RemoteApp lub lokalizację, w której chcesz utworzyć.
4. Po wyświetleniu monitu można pobrać skryptu do komputera lokalnego.
5. Skopiuj parametry polecenia w polu tekstowym do Schowka.
6. Otwórz okno programu Windows PowerShell z podwyższonym poziomem uprawnień.
7. W oknie programu Windows PowerShell z podwyższonym poziomem uprawnień przejdź do katalogu, w której pobrano skrypt.
8. Wklej skopiowane polecenie i naciśnij klawisz **Enter**.
   
   Rozpocznie się proces przekazywania i czas trwania może zależeć od wielu czynników, takich jak szybkość sieci, a rozmiar obrazu
9. W przypadku przekazania nie powiedzie się z powodu przerwy w działaniu sieci lub rzeczy jak, zawsze można wznowić procesu przekazywania zostanie rozpoczęcia. Aby wznowić przekazywania, uruchom skrypt ponownie, używając tego samego wiersza polecenia.

> [!WARNING]
> Nigdy nie zmodyfikować skrypt przekazywania. Aby upewnić się, że obraz spełnia wymagania dotyczące obrazów i wymagania dotyczące aplikacji została zaimplementowana konkretnych testów.
> 
> 

## <a name="common-problems"></a>Typowe problemy
* Upewnij się, że używasz programu Windows PowerShell, nie programu Azure PowerShell. Musisz zainstalować moduł Azure PowerShell, ponieważ niektóre moduły są wymagane podczas procesu przekazywania.
* Nigdy nie zmodyfikować skrypt, sprawdzanie poprawności istnieją dla Twojej wygody.
* Jeśli plik vhd pobiera zablokowane podczas przekazywania, skopiuj plik, lub przenieś go do nowego przekazywania lokalizacji, a następnie spróbuj ponownie. Może to być niektórych procesu systemu Windows, który uniemożliwia przekazywania.  

