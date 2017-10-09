---
title: aaaUsing hostnames tooregister dynamicznych DNS
description: "Ta strona przedstawia szczegóły na temat tooset się nazwy hostów tooregister dynamicznych DNS w serwerach DNS."
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a>Przy użyciu nazwy hostów tooregister dynamicznych DNS na serwerze DNS
[Platforma Azure udostępnia rozpoznawanie nazw](virtual-networks-name-resolution-for-vms-and-role-instances.md) na maszynach wirtualnych (VM) i wystąpień ról. Jednak gdy programu rozpoznawania nazw musi wykracza poza udostępnianych przez platformę Azure, musisz podać serwery DNS. Dzięki temu hello zasilania tootailor Twojego toosuit rozwiązania DNS określonych potrzeb. Na przykład może być konieczne tooaccess zasobów lokalnych za pomocą kontrolera domeny usługi Active Directory.

Jeśli niestandardowe serwery DNS są hostowane jako maszyny wirtualne Azure może przekazywać nazwy hosta kwerendy o hello takie same nazwy hostów tooresolve tooAzure sieci wirtualnej. Jeśli nie chcesz, aby toouse tej trasy, możesz zarejestrować Twojej nazwy hostów maszyny Wirtualnej na serwerze DNS przy użyciu dynamicznych DNS.  Azure nie ma toodirectly możliwości (np. poświadczenia) hello utworzyć rekordy w serwerach DNS, potrzebne są często alternatywne uzgodnienia. Poniżej przedstawiono kilka typowych scenariuszy z alternatyw.

## <a name="windows-clients"></a>Klienci systemu Windows
Klienci z systemem Windows przyłączonych do domeny inne niż podejmować niezabezpieczona aktualizacji dynamicznych DNS (DDNS), po uruchomieniu lub zmianie ich adresów IP. Nazwa DNS Hello jest hello hostname plus sufiks podstawowej domeny DNS hello. Azure pozostawia sufiks podstawowej domeny DNS hello puste, ale możesz ustawić w hello maszyny Wirtualnej, za pośrednictwem hello [interfejsu użytkownika](https://technet.microsoft.com/library/cc794784.aspx) lub [przy użyciu automatyzacji](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).

Klienci z systemem Windows przyłączonych do domeny rejestrują swoje adresy IP z kontrolerem domeny hello przy użyciu bezpiecznych dynamicznych DNS. proces przyłączania do domeny Hello ustawia sufiks podstawowej domeny DNS hello na powitania klienta i tworzy i obsługuje hello relacji zaufania.

## <a name="linux-clients"></a>Klienci systemu Linux
Klienci systemu Linux zazwyczaj nie rejestrują się z serwerem DNS hello podczas uruchamiania, one przyjęto założenie, że jest powitania serwera DHCP. Serwery DHCP w usłudze Azure ma zdolność hello lub poświadczenia tooregister rekordów w serwera DNS.  Można użyć narzędzia o nazwie *nsupdate*, będące częścią pakietu Bind hello, aktualizacji dynamicznych DNS toosend. Ponieważ hello protokół dynamicznej DNS jest standardowym, można użyć *nsupdate* nawet jeśli nie używasz Bind na powitania serwera DNS.

Można użyć punkty zaczepienia hello, udostępnianych przez toocreate klienta DHCP hello i obsługa hello wpis nazwy hosta w powitania serwera DNS. Cyklu DHCP hello powitania klienta wykonuje hello skryptów w */etc/dhcp/dhclient-exit-hooks.d/*. Może to być używane przy użyciu nowego adresu IP tooregister hello *nsupdate*. Na przykład:

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

Można również użyć hello *nsupdate* tooperform polecenia aktualizacji bezpiecznych dynamicznych DNS. Na przykład podczas korzystania z serwera Bind DNS, to pary kluczy publiczno prywatnych [wygenerowany](http://linux.yyz.us/nsupdate/).  Serwer DNS Hello jest [skonfigurowane](http://linux.yyz.us/dns/ddns-server.html) z hello publicznej części klucza hello, którego nie można zweryfikować podpisu hello na powitania żądania. Należy użyć hello *-k* tooprovide opcji hello para klucz zbyt*nsupdate* aby hello toobe żądania podpisany aktualizacji dynamicznych DNS.

Podczas korzystania z serwera DNS systemu Windows, za pomocą uwierzytelniania Kerberos hello *-g* parametru w *nsupdate* (niedostępne w wersji Windows hello *nsupdate* ). toodo, użyj *kinit* tooload hello poświadczenia (np. z [pliku keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)). Następnie *nsupdate -g* przejmą hello poświadczenia z pamięci podręcznej hello.

W razie potrzeby można dodać tooyour sufiks wyszukiwania DNS maszyn wirtualnych. określono sufiks DNS Hello w hello */etc/resolv.conf* pliku. Większość dystrybucjach systemu Linux automatycznie zarządzać hello zawartość tego pliku, dlatego zazwyczaj nie można edytować go. Jednak można zastąpić sufiks hello przy użyciu klienta DHCP hello *zastępują* polecenia. toodo to w */etc/dhcp/dhclient.conf*, dodać:

        supersede domain-name <required-dns-suffix>;

