---
title: tooa pulpitu aaaRemote maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooinstall i konfigurowanie pulpitu zdalnego tooconnect tooa maszyny Wirtualnej systemu Linux Azure firmy Microsoft dla hello klasycznego modelu wdrożenia"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a><span data-ttu-id="c1ac5-103">Przy użyciu pulpitu zdalnego tooconnect tooa maszyny Wirtualnej systemu Linux programu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c1ac5-103">Using Remote Desktop tooconnect tooa Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="c1ac5-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c1ac5-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c1ac5-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="c1ac5-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="c1ac5-107">Witaj zaktualizowanej wersji Menedżera zasobów w tym artykule, można znaleźć [tutaj](../use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="c1ac5-107">For hello updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="c1ac5-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c1ac5-108">Overview</span></span>
<span data-ttu-id="c1ac5-109">RDP (Remote Desktop Protocol) jest zastrzeżonym protokołem używane dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="c1ac5-110">Jak możemy użyć tooa tooconnect RDP maszyny Wirtualnej systemu Linux (maszyna wirtualna) zdalnie?</span><span class="sxs-lookup"><span data-stu-id="c1ac5-110">How can we use RDP tooconnect tooa Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="c1ac5-111">W tych wskazówkach zapewni hello odpowiedzi!</span><span class="sxs-lookup"><span data-stu-id="c1ac5-111">This guidance will give you hello answer!</span></span> <span data-ttu-id="c1ac5-112">Ułatwi to xrdp tooinstall i konfiguracji na programu Microsoft Azure maszyny Wirtualnej systemu Linux, które umożliwia nawiązanie połączenia tooit przy użyciu pulpitu zdalnego na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-112">It will help you tooinstall and config xrdp on your Microsoft Azure Linux VM, which lets you connect tooit with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="c1ac5-113">Używamy systemem Ubuntu lub OpenSUSE jako przykład Witaj w tych wskazówkach maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-113">We will use Linux VM running Ubuntu or OpenSUSE as hello example in this guidance.</span></span>

<span data-ttu-id="c1ac5-114">Narzędzie xrdp Hello jest typu open source, serwer protokołu RDP, któremu tooconnect serwera systemu Linux przy użyciu pulpitu zdalnego na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-114">hello xrdp tool is an open source RDP server that allows you tooconnect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="c1ac5-115">RDP ma lepszą wydajność niż VNC (wirtualnych sieci przetwarzania danych).</span><span class="sxs-lookup"><span data-stu-id="c1ac5-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="c1ac5-116">VNC renderuje przy użyciu grafiki jakość JPEG i może działać powoli, protokołu RDP jest szybkie i krystalicznie czyste.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="c1ac5-117">Musi już mieć maszyny Wirtualnej platformy Microsoft Azure systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="c1ac5-118">toocreate i skonfiguruj Maszynę wirtualną systemu Linux, zobacz hello [samouczek maszyny Wirtualnej systemu Linux Azure](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="c1ac5-118">toocreate and set up a Linux VM, see hello [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="c1ac5-119">Tworzenie punktu końcowego dla pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="c1ac5-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="c1ac5-120">Używamy hello domyślny punkt końcowy 3389 dla pulpitu zdalnego w tym dokumencie. Konfigurowanie 3389 punktu końcowego jako `Remote Desktop` tooyour maszyny Wirtualnej systemu Linux, takich jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="c1ac5-120">We will use hello default endpoint 3389 for Remote Desktop in this doc. Set up 3389 endpoint as `Remote Desktop` tooyour Linux VM like below:</span></span>

![Obraz](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="c1ac5-122">Jeśli nie znasz tooset się punkt końcowy dla maszyny Wirtualnej, zobacz temat [w tych wskazówkach](setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="c1ac5-122">If you don't know how tooset up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="c1ac5-123">Zainstaluj Gnome pulpitu</span><span class="sxs-lookup"><span data-stu-id="c1ac5-123">Install Gnome Desktop</span></span>
<span data-ttu-id="c1ac5-124">Połącz tooyour maszyny Wirtualnej systemu Linux za pomocą `putty`i zainstaluj `Gnome Desktop`.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-124">Connect tooyour Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="c1ac5-125">Ubuntu użyć:</span><span class="sxs-lookup"><span data-stu-id="c1ac5-125">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="c1ac5-126">Dla OpenSUSE użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="c1ac5-126">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="c1ac5-127">Zainstaluj xrdp</span><span class="sxs-lookup"><span data-stu-id="c1ac5-127">Install xrdp</span></span>
<span data-ttu-id="c1ac5-128">Ubuntu użyć:</span><span class="sxs-lookup"><span data-stu-id="c1ac5-128">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="c1ac5-129">Dla OpenSUSE użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="c1ac5-129">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="c1ac5-130">Zaktualizuj wersję OpenSUSE hello wersją hello używanego w hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-130">Update hello OpenSUSE version with hello version you are using in hello following command.</span></span> <span data-ttu-id="c1ac5-131">w poniższym przykładzie Hello jest przeznaczony dla `OpenSUSE 13.2`.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-131">hello example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="c1ac5-132">Uruchom xrdp i skonfiguruj xdrp w górę rozruchu</span><span class="sxs-lookup"><span data-stu-id="c1ac5-132">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="c1ac5-133">Dla OpenSUSE użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="c1ac5-133">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="c1ac5-134">Dla Ubuntu, zostanie rozpoczęta xrdp i eanbled w górę rozruchu automatycznie po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-134">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="c1ac5-135">Przy użyciu xfce, jeśli używasz wersji Ubuntu później niż Ubuntu 12.04LTS</span><span class="sxs-lookup"><span data-stu-id="c1ac5-135">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="c1ac5-136">Ponieważ bieżąca wersja xrdp hello nie obsługuje Gnome pulpitu dla wersji Ubuntu później niż Ubuntu 12.04LTS, będziemy używać `xfce` pulpitu zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-136">Because hello current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="c1ac5-137">tooinstall `xfce`, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="c1ac5-137">tooinstall `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="c1ac5-138">Następnie Włącz `xfce` za pomocą tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="c1ac5-138">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="c1ac5-139">Edytuj plik konfiguracji hello `/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="c1ac5-139">Edit hello config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="c1ac5-140">Dodaj wiersz hello `xfce4-session` przed wierszem hello `/etc/X11/Xsession`.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-140">Add hello line `xfce4-session` before hello line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="c1ac5-141">toorestart hello xrdp usługi, użyj tego:</span><span class="sxs-lookup"><span data-stu-id="c1ac5-141">toorestart hello xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="c1ac5-142">Połączenie z maszyną Wirtualną systemu Linux z komputera z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="c1ac5-142">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="c1ac5-143">Na maszynie z systemem Windows uruchom klienta pulpitu zdalnego hello i wprowadź nazwę DNS maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-143">In a Windows machine, start hello Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="c1ac5-144">Lub przejdź toohello pulpitu nawigacyjnego w portalu Azure hello maszyny wirtualnej i kliknij polecenie `Connect` tooconnect maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-144">Or go toohello Dashboard of your VM in hello Azure portal and click `Connect` tooconnect your Linux VM.</span></span> <span data-ttu-id="c1ac5-145">W takim przypadku zostaną wyświetlone powitalne okno logowania:</span><span class="sxs-lookup"><span data-stu-id="c1ac5-145">In that case, you see hello login window:</span></span>

![Obraz](./media/remote-desktop/no2.png)

<span data-ttu-id="c1ac5-147">Zaloguj się za pomocą hello nazwy użytkownika i hasła maszyny wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c1ac5-147">Log in with hello user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1ac5-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c1ac5-148">Next steps</span></span>
<span data-ttu-id="c1ac5-149">Aby uzyskać więcej informacji na temat używania xrdp, zobacz [http://www.xrdp.org/](http://www.xrdp.org/).</span><span class="sxs-lookup"><span data-stu-id="c1ac5-149">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
