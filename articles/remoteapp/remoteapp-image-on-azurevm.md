---
title: "Tworzenie obrazu usługi Azure RemoteApp opartego na maszynie Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia obrazu usługi Azure RemoteApp, zaczynając od maszyny wirtualnej platformy Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ee64b86835af8e6237cddcd8acc779fc6dac8214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>Tworzenie obrazu usługi Azure RemoteApp oparte na maszynie wirtualnej platformy Azure
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Z maszyny wirtualnej platformy Azure, można tworzyć obrazy usługi Azure RemoteApp, (które przechowywania aplikacji, którą można udostępniać w kolekcji). Można również użyć obrazu maszyny wirtualnej, dodane do galerii obrazu maszyny Wirtualnej platformy Azure, które spełnia wszystkie wymagania obrazu usługi Azure RemoteApp — można tego obrazu maszyny Wirtualnej jako punkt początkowy dla własnego maszyny Wirtualnej, jeśli chcesz. Po prostu wyszukaj obraz "Systemu Windows serwera hosta sesji pulpitu zdalnego" w bibliotece.

Istnieją dwa kroki, aby utworzyć własny obraz oparty na maszynie Wirtualnej platformy Azure — Tworzenie obrazu i przekaż go w bibliotece maszyny Wirtualnej platformy Azure do usługi Azure RemoteApp.

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>Utworzyć obraz niestandardowy oparty na maszynie Wirtualnej platformy Azure
Wykonaj te kroki, aby utworzyć obraz oparty na maszynie Wirtualnej platformy Azure.

1. Utwórz maszynę wirtualną platformy Azure. Można użyć "systemu Windows serwera hosta sesji pulpitu zdalnego" lub "Windows Server zdalnego pulpitu sesji hosta z Microsoft Office 365 ProPlus" obrazu z galerii obrazu maszyny wirtualnej platformy Azure. Ten obraz spełnia wszystkie usługi Azure RemoteApp szablonu obrazu wymagania.
   
    Aby uzyskać więcej informacji, zobacz [tworzenia maszyny Wirtualnej z systemem Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Połączenie z maszyną Wirtualną i zainstaluj i skonfiguruj aplikacje, które ma zostać udostępniona za pośrednictwem usługi RemoteApp. Upewnij się, że wykonywać żadnych dodatkowych konfiguracji systemu Windows wymagane przez aplikacje.
   
    Aby uzyskać więcej informacji, zobacz [jak Zaloguj się do maszyny wirtualnej systemem Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Jeśli używasz jednego z obrazów hosta sesji usług pulpitu zdalnego serwera systemu Windows jest dołączony weryfikacji skrypt, który zapewni, że maszyna wirtualna spełnia RemoteApp pre-reqs. Aby uruchomić skrypt, kliknij dwukrotnie **ValidateRemoteAppImage** na pulpicie. Upewnij się, że wszystkie błędy zgłoszone przez skrypt zostały usunięte przed przejściem do następnego kroku.
4. Programu SYSPREP Uogólnij i Przechwyć obraz. Zobacz [jak przechwycić maszynę wirtualną systemu Windows do użycia jako szablon](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) instrukcje.

## <a name="import-the-image-into-the-azure-remoteapp-image-library"></a>Zaimportować go do usługi Azure RemoteApp Biblioteka obrazów
Aby zaimportować nowy obraz do usługi Azure RemoteApp, wykonaj następujące kroki:

1. W **obrazy szablonów** karty:
   
   * Jeśli nie masz żadnych istniejących obrazów, kliknij przycisk **przekazać lub zaimportować obrazu szablonu**.
   * Jeśli masz już co najmniej jeden obraz, kliknij przycisk  **+**  Aby dodać nowy obraz.
2. Wybierz **Import obrazów z maszyn wirtualnych** biblioteki, a następnie kliknij przycisk **dalej**.
3. Na następnej stronie wybierz niestandardowy obraz z listy i upewnij się, że zostały wykonane kroki podczas tworzenia obrazu. Kliknij przycisk **Dalej**.
4. Wprowadź nazwę dla nowego obrazu usługi RemoteApp i wybierz lokalizację, a następnie kliknij znacznik wyboru, aby rozpocząć proces importowania.

> [!NOTE]
> Obrazy można importować z dowolnej lokalizacji platformy Azure obsługiwane przez maszyny wirtualne Azure do dowolnej lokalizacji platformy Azure obsługiwane przez usługę Azure RemoteApp. W zależności od lokalizacji importowania może potrwać maksymalnie 25 minut.
> 
> 

Teraz można przystąpić do tworzenia nowej kolekcji, albo [chmury](remoteapp-create-cloud-deployment.md) kolekcji lub [hybrydowego](remoteapp-create-hybrid-deployment.md), w zależności od potrzeb.

