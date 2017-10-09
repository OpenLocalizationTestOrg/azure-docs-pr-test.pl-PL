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
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a>Używanie uprawnień użytkownika root na maszynach wirtualnych systemu Linux na platformie Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Domyślnie program hello `root` użytkownik jest wyłączony na maszynach wirtualnych systemu Linux na platformie Azure. Użytkownicy mogą uruchamiać polecenia z podwyższonym poziomem uprawnień przy użyciu hello `sudo` polecenia. Jednak hello obsługi mogą się różnić w zależności od tego, jak hello system zainicjowano obsługę administracyjną.

1. **Klucz SSH i hasło lub hasło tylko** -hello maszyny wirtualnej została zainicjowana obsługa jakikolwiek certyfikat (`.CER` pliku) lub klucza SSH, a także hasła, lub po prostu nazwę użytkownika i hasło. W takim przypadku `sudo` wyświetli monit o podanie hasła użytkownika hello przed wykonaniem polecenia hello.
2. **Klucz SSH tylko** -maszyny wirtualnej hello zainicjowano przy użyciu certyfikatu (`.cer`, `.pem`, lub `.pub` pliku) lub klucza SSH, ale bez hasła.  W takim przypadku `sudo` **nie** monitu o hasło użytkownika hello przed wykonaniem polecenia hello.

## <a name="ssh-key-and-password-or-password-only"></a>SSH klucza i hasło lub tylko hasła
Zaloguj się do maszyny wirtualnej systemu Linux hello przy użyciu uwierzytelniania SSH klucza lub hasła, a następnie uruchom polecenia przy użyciu `sudo`, na przykład:

    # sudo <command>
    [sudo] password for azureuser:

W takim przypadku hello użytkownik będzie monitowany o podanie hasła. Po wprowadzeniu hasła hello `sudo` uruchomi polecenie hello z `root` uprawnienia.

Można również włączyć passwordless sudo, edytując hello `/etc/sudoers.d/waagent` pliku, na przykład:

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

Ta zmiana pozwoli na passwordless sudo przez użytkownika hello "azureuser".

## <a name="ssh-key-only"></a>SSH tylko klucza
Zaloguj się do maszyny wirtualnej systemu Linux hello przy użyciu uwierzytelniania klucza SSH, a następnie uruchom polecenia przy użyciu `sudo`, na przykład:

    # sudo <command>

W takim przypadku zostanie użytkownika hello **nie** zostanie wyświetlony monit o hasło. Po naciskając klawisz `<enter>`, `sudo` uruchomi polecenie hello z `root` uprawnienia.

