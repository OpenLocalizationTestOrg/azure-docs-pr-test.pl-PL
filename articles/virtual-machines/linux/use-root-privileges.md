---
title: "uprawnienia głównego aaaUse na maszynach wirtualnych systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się jak główny toouse uprawnień na maszynie wirtualnej systemu Linux na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="956fa-103">Używanie uprawnień użytkownika root na maszynach wirtualnych systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="956fa-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="956fa-104">Domyślnie program hello `root` użytkownik jest wyłączony na maszynach wirtualnych systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="956fa-104">By default, hello `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="956fa-105">Użytkownicy mogą uruchamiać polecenia z podwyższonym poziomem uprawnień przy użyciu hello `sudo` polecenia.</span><span class="sxs-lookup"><span data-stu-id="956fa-105">Users can run commands with elevated privileges by using hello `sudo` command.</span></span> <span data-ttu-id="956fa-106">Jednak hello obsługi mogą się różnić w zależności od tego, jak hello system zainicjowano obsługę administracyjną.</span><span class="sxs-lookup"><span data-stu-id="956fa-106">However, hello experience may vary depending on how hello system was provisioned.</span></span>

1. <span data-ttu-id="956fa-107">**Klucz SSH i hasło lub hasło tylko** -hello maszyny wirtualnej została zainicjowana obsługa jakikolwiek certyfikat (`.CER` pliku) lub klucza SSH, a także hasła, lub po prostu nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="956fa-107">**SSH key and password OR password only** - hello virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="956fa-108">W takim przypadku `sudo` wyświetli monit o podanie hasła użytkownika hello przed wykonaniem polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="956fa-108">In this case `sudo` will prompt for hello user's password before executing hello command.</span></span>
2. <span data-ttu-id="956fa-109">**Klucz SSH tylko** -maszyny wirtualnej hello zainicjowano przy użyciu certyfikatu (`.cer`, `.pem`, lub `.pub` pliku) lub klucza SSH, ale bez hasła.</span><span class="sxs-lookup"><span data-stu-id="956fa-109">**SSH key only** - hello virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="956fa-110">W takim przypadku `sudo` **nie** monitu o hasło użytkownika hello przed wykonaniem polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="956fa-110">In this case `sudo` **will not** prompt for hello user's password before executing hello command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="956fa-111">SSH klucza i hasło lub tylko hasła</span><span class="sxs-lookup"><span data-stu-id="956fa-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="956fa-112">Zaloguj się do maszyny wirtualnej systemu Linux hello przy użyciu uwierzytelniania SSH klucza lub hasła, a następnie uruchom polecenia przy użyciu `sudo`, na przykład:</span><span class="sxs-lookup"><span data-stu-id="956fa-112">Log into hello Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="956fa-113">W takim przypadku hello użytkownik będzie monitowany o podanie hasła.</span><span class="sxs-lookup"><span data-stu-id="956fa-113">In this case hello user will be prompted for a password.</span></span> <span data-ttu-id="956fa-114">Po wprowadzeniu hasła hello `sudo` uruchomi polecenie hello z `root` uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="956fa-114">After entering hello password `sudo` will run hello command with `root` privileges.</span></span>

<span data-ttu-id="956fa-115">Można również włączyć passwordless sudo, edytując hello `/etc/sudoers.d/waagent` pliku, na przykład:</span><span class="sxs-lookup"><span data-stu-id="956fa-115">You can also enable passwordless sudo by editing hello `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="956fa-116">Ta zmiana pozwoli na passwordless sudo przez użytkownika hello "azureuser".</span><span class="sxs-lookup"><span data-stu-id="956fa-116">This change will allow for passwordless sudo by hello user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="956fa-117">SSH tylko klucza</span><span class="sxs-lookup"><span data-stu-id="956fa-117">SSH Key Only</span></span>
<span data-ttu-id="956fa-118">Zaloguj się do maszyny wirtualnej systemu Linux hello przy użyciu uwierzytelniania klucza SSH, a następnie uruchom polecenia przy użyciu `sudo`, na przykład:</span><span class="sxs-lookup"><span data-stu-id="956fa-118">Log into hello Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="956fa-119">W takim przypadku zostanie użytkownika hello **nie** zostanie wyświetlony monit o hasło.</span><span class="sxs-lookup"><span data-stu-id="956fa-119">In this case hello user will **not** be prompted for a password.</span></span> <span data-ttu-id="956fa-120">Po naciskając klawisz `<enter>`, `sudo` uruchomi polecenie hello z `root` uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="956fa-120">After pressing `<enter>`, `sudo` will run hello command with `root` privileges.</span></span>

