---
title: "aaaCreate na maszynie Wirtualnej platformy Azure na podstawie obrazu usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate obrazu usługi Azure RemoteApp, zaczynając od maszyny wirtualnej platformy Azure."
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
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>Tworzenie obrazu usługi Azure RemoteApp oparte na maszynie wirtualnej platformy Azure
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Z maszyny wirtualnej platformy Azure, można tworzyć obrazy usługi Azure RemoteApp, (przechowujących aplikacji hello udostępnianych w kolekcji). Możesz również wybrać toouse dodaliśmy toohello galerii obrazu maszyny Wirtualnej platformy Azure, które spełnia wszystkie wymagania dotyczące obrazu usługi Azure RemoteApp hello obrazu maszyny wirtualnej — można tego obrazu maszyny Wirtualnej jako punkt początkowy dla własnego maszyny Wirtualnej, jeśli chcesz. Po prostu wyszukaj hello obrazu "Systemu Windows serwera hosta sesji pulpitu zdalnego" w bibliotece hello.

Istnieją dwa toocreate kroki własny obraz oparty na maszynie Wirtualnej platformy Azure — Tworzenie obrazu hello, a następnie przekaż z hello Azure VM biblioteki tooAzure programów RemoteApp.

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>Utworzyć obraz niestandardowy oparty na maszynie Wirtualnej platformy Azure
Użyj tych kroków toocreate obraz oparty na maszynie Wirtualnej platformy Azure.

1. Utwórz maszynę wirtualną platformy Azure. Można użyć hello "Systemu Windows serwera hosta sesji pulpitu zdalnego" lub "Windows Server zdalnego pulpitu sesji hosta z Microsoft Office 365 ProPlus" obraz powitania z galerii obrazu maszyny wirtualnej platformy Azure hello. Ten obraz spełnia wszystkie wymagania obrazu szablonu usługi Azure RemoteApp hello.
   
    Aby uzyskać więcej informacji, zobacz [tworzenia maszyny Wirtualnej z systemem Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Połącz toohello maszyny Wirtualnej i instalowanie i konfigurowanie aplikacji hello, które mają tooshare za pośrednictwem usługi RemoteApp. Upewnij się, że tooperform żadnych dodatkowych konfiguracji systemu Windows wymagane przez aplikacje.
   
    Aby uzyskać więcej informacji, zobacz [jak tooLog na tooa maszyny wirtualnej z systemu Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Jeśli używasz jednego z obrazów hosta sesji usług pulpitu zdalnego serwera Windows hello jest skrypt dołączone weryfikacji, który zapewni, że maszyna wirtualna spełnia RemoteApp hello pre-reqs. toorun skrypt, kliknij dwukrotnie **ValidateRemoteAppImage** hello pulpitu. Upewnij się, że wszystkie błędy zgłoszone przez skrypt hello zostały usunięte przed kontynuowaniem toohello następnego kroku.
4. Narzędzie SYSPREP Uogólnij i Przechwyć obraz powitania. Zobacz [jak tooCapture tooUse maszyny wirtualnej systemu Windows, jako szablon](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) instrukcje.

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a>Importowanie obraz powitania Biblioteka obrazów hello Azure RemoteApp
Użyj tych kroków tooimport hello nowy obraz do usługi Azure RemoteApp:

1. W hello **obrazy szablonów** karty:
   
   * Jeśli nie masz żadnych istniejących obrazów, kliknij przycisk **przekazać lub zaimportować obrazu szablonu**.
   * Jeśli masz już co najmniej jeden obraz, kliknij przycisk  **+**  tooadd nowy obraz.
2. Wybierz **Import obrazów z maszyn wirtualnych** biblioteki, a następnie kliknij przycisk **dalej**.
3. Na następnej stronie powitania wybierz z listy hello niestandardowego obrazu i upewnij się, że zostały wykonane kroki hello podczas tworzenia obrazu. Kliknij przycisk **Dalej**.
4. Wprowadź nazwę dla nowego obrazu usługi RemoteApp hello i wybierz lokalizację, hello, a następnie kliknij proces importowania hello hello znacznikiem wyboru toostart.

> [!NOTE]
> Obrazy można importować z dowolnej lokalizacji platformy Azure obsługiwane przez maszyny wirtualne Azure tooany lokalizacji platformy Azure obsługiwane przez usługę Azure RemoteApp. W zależności od lokalizacji hello hello importowania może potrwać too25 minut.
> 
> 

Teraz możesz są gotowe toocreate nowej kolekcji, albo [chmury](remoteapp-create-cloud-deployment.md) kolekcji lub [hybrydowego](remoteapp-create-hybrid-deployment.md), w zależności od potrzeb.

