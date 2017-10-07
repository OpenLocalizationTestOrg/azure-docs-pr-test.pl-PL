---
title: "wymagania dotyczące obrazu usługi RemoteApp aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat wymagań hello tworzenia toobe obrazy używane z usługą Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Wymagania dotyczące usługi Azure RemoteApp obrazów
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Usługa Azure RemoteApp używa toohost obrazu systemu Windows Server 2012 R2, wszystkie programy hello mają tooshare z użytkownikami. toocreate niestandardowego obrazu, można uruchomić z istniejącego obrazu lub [Utwórz nową](remoteapp-create-custom-image.md).

> [!TIP]
> Czy wiesz, że Twoje daje subskrypcji usługi Azure RemoteApp dostęp tooa obrazu systemu Windows Server 2012 R2 w hello galerii maszyny Wirtualnej platformy Azure, których można używać toocreate obrazu szablonu? [Go wyewidencjonować](remoteapp-image-on-azurevm.md).  
> 
> 

Witaj wymagania dotyczące obrazu hello, które mogą być przekazywane do użycia z usługą Azure RemoteApp są:

* Niestandardowych aplikacji nie należy przechowywać dane lokalnie na powitania obrazu. Te obrazy są bezstanowych i powinien zawierać wyłącznie aplikacje.
* Obraz powitania nie zawiera danych, które mogą zostać utracone.
* rozmiar obrazu Hello powinna być wielokrotnością liczby MB. Jeśli spróbujesz tooupload obrazu, który nie jest wielokrotnością hello przekazywanie zakończy się niepowodzeniem.
* Witaj, rozmiar obrazu musi być 127 GB lub mniej.
* Musi znajdować się na plik VHD (pliki VHDX nie są obecnie obsługiwane).
* Witaj wirtualnego dysku twardego nie może być maszyny wirtualnej generacji 2.
* Witaj wirtualnego dysku twardego może być stałym rozmiarze lub dynamicznie powiększających się. Dynamicznie powiększających się dysków VHD jest zalecane, ponieważ trwa tooAzure tooupload mniej czasu niż ustalony rozmiar pliku VHD.
* dysk Hello musi zostać zainicjowany przy użyciu stylu partycjonowania hello główny rekord rozruchowy (MBR). Witaj stylu partycji (GPT tabela) partycji GUID nie jest obsługiwane.
* Witaj dysku VHD musi zawierać jednej instalacji systemu Windows Server 2012 R2. Nazwa może zawierać wiele woluminów, ale tylko jeden zawartych w instalacji systemu Windows.
* Witaj zdalnego pulpitu sesji hosta ról i funkcji Środowisko pulpitu hello musi być zainstalowany.
* Witaj roli Broker połączeń usług pulpitu zdalnego musi *nie* można zainstalować.
* Witaj system szyfrowania plików (EFS) musi być wyłączona.
* Witaj obrazu musi być przetworzonej przez program Sysprep przy użyciu parametrów hello **/oobe / generalize/shutdown** (nie należy używać hello **/mode:vm** parametru).
* Przekazywanie dysk VHD z łańcucha migawek nie jest obsługiwane.

Zobacz [Tworzenie obrazu usługi Azure RemoteApp](remoteapp-imageoptions.md) Aby uzyskać więcej informacji na temat tworzenia obrazów na potrzeby usługi Azure RemoteApp.

