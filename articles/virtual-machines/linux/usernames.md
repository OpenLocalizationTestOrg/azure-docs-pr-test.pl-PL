---
title: "aaaSelecting nazwy użytkownika dla systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak nazwa użytkownika tooselect maszyny wirtualnej systemu Linux na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a>Wybieranie nazw użytkowników dla systemu Linux na platformie Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Podczas obsługi administracyjnej maszyny wirtualnej systemu Linux na platformie Azure należy określić nazwę hello użytkownika głównego nie mógł później użyć toolog do hello maszyny Wirtualnej. Możesz wybrać nazwę hello hello nowego użytkownika, lub jeśli Inicjowanie obsługi za pomocą hello klasycznego portalu Azure możesz zaakceptować domyślną hello name "azureuser".

W większości przypadków tego użytkownika nie istnieje na podstawowy obraz powitania i zostanie utworzony podczas procesu udostępniania hello. Jeśli hello użytkownika znajduje się na podstawowy obraz maszyny Wirtualnej hello, agenta systemu Linux Azure hello po prostu skonfiguruje hello hasła lub klucza SSH dla tego użytkownika na podstawie informacji hello, określone podczas tworzenia hello maszyny Wirtualnej.

**Jednak**, Linux definiuje zestaw nazwy użytkownika, które nie powinny być używane. Hello inicjowania obsługi będzie procesu **niepowodzenie** przy próbie tooprovision maszyny Wirtualnej systemu Linux przy użyciu istniejącego użytkownika system, który jest zdefiniowany jako użytkownik z UID 0-99. Typowym przykładem jest hello `root` użytkownika, który ma UID 0.

* Zobacz też: [Linux Standard Base - zakresy identyfikator użytkownika](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)

Witaj poniżej znajduje się lista typowych użytkowników wbudowanych systemu CentOS i Ubuntu, że należy unikać używania podczas inicjowania obsługi administracyjnej maszyny wirtualnej systemu Linux na platformie Azure. Ta lista jest tylko przykładem, zobacz dokumentację toohello dla Twojego tooensure dystrybucji tej nazwie użytkownika hello wybranych nie powoduje konfliktu z istniejącym użytkownikiem systemu.

## <a name="centos"></a>CentOS
* abrt
* usługi adm
* audio
* bin
* CDROM
* cgred
* demon
* dbus
* inicjowania połączeń
* DIP
* dysku
* dyskietek
* FTP
* FTP
* gry
* Gopher
* haldaemon
* zatrzymanie
* kmem
* blokady
* LP
* Poczty
* Man
* pamięci
* nfsnobody
* nikt nie
* NTP
* Operator
* oprofile
* postdrop
* Operatory przyrostka
* qpidd
* główny
* RPC
* rpcuser
* saslauth
* Zamknięcie
* slocate
* sshd
* stapdev
* stapusr
* Synchronizacji
* sys
* taśmy
* Test
* tcpdump
* usługi TTY
* użytkownicy
* utempter
* utmp
* UUCP
* vcsa
* wideo
* koło

## <a name="ubuntu"></a>Ubuntu
* usługi adm
* Administrator
* audio
* kopia zapasowa
* bin
* CDROM
* crontab
* demon
* inicjowania połączeń
* DIP
* dysku
* Faksów
* dyskietek
* Łączenie
* gry
* gnats
* IRC
* kmem
* orientacji poziomej
* libuuid
* Lista
* LP
* Poczty
* Man
* messagebus
* mlocate
* netdev
* Grupy dyskusyjne
* nikt nie
* nogroup
* Operator
* plugdev
* Serwer proxy
* główny
* SASL
* Cień
* src
* SSH
* sshd
* personel
* sudo
* Synchronizacji
* sys
* syslog
* taśmy
* usługi TTY
* użytkownicy
* utmp
* UUCP
* wideo
* głosu
* whoopsie
* dane www

